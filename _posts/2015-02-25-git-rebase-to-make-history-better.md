---
layout: post
title: "Git rebase to change history for the better"
description: "Squash your local history of work-in-progress commits into a single commit of a working feature to keep history clean across a shared codebase"
category: 
tags: ["git", "source control"]
---
{% include JB/setup %}


Having recently written this post up as a wiki page for a project in work, I figured it'd be nice to share it with the wide world for anyone working on a shared codebase with occasionally messy git history.

### Git What?

`git rebase`

Squash your commits together after you've finished working on a feature so that the net result of what you're adding to master is the complete and working functionality.

**Do this before pushing your commits to a remote branch, i.e. before code review or pull request.**

If you have pushed your branch and still want to rebase, skip down to Advanced Topics at the bottom to read more.

*To do this you'll need to use git itself. If you're using SourceTree, you will need to read their documentation on how to do this. So use git. It's actually pretty easy.*

### Why?

Change history so that instead of your commit log looking like this:

    abcde123 fixed tests, forgot to add the semi-colon to the end of the method call     <- now it all works!
    dabce321 added tests for notification templates     <- check this out for partially working codebase with broken tests
    bcdea213 missed base template file from notifications sender     <- check this out for partially working codebase with no tests
    cedab132 Created the template for notifications     <- check this out for incomplete work-in-progress
    eadcb231 Added the message extractor service     <- check this out for fully working codebase with this feature

It looks like this wonderful thing:

    abcde123 Added the templates for notifications      <- check this out for fully working codebase with this feature
    eadcb231 Added the message extractor service     <- check this out for fully working codebase with this feature

This makes it easier to work with revisions and the log for the repository shows clearly the work we've been adding.

### How?

Follow the steps below to rebase three commits into a single aggregated change.

    $ touch new_file.txt

You've added your new file. Full of potential, waiting to be filled with wonderful code or data.

    $ echo "one change" >> new_file.txt
    $ git add new_file.txt
    $ git commit -m "added new file"

    $ echo "second change" >> new_file.txt
    $ git add new_file.txt
    $ git commit -m "updated the new file"

    $ echo "third change" >> new_file.txt
    $ git add new_file.txt
    $ git commit -m "made a third change"

Typical development workflow - you make some changes, then you commit to save your work. That's all good. Commit to your local repository as many times as you want. Please also use better and more descriptive commit messages than I have for this example.

However, throughout the process, even if you've only got a working piece of code on the final commit, this is what your git log will look like:

    commit 5838dcb...
    Author: Will Hamill 
    Date:   <date>

        made a third change

    commit 52f0741...
    Author: Will Hamill 
    Date:   <date>

        updated the new file

    commit 491ea1e...
    Author: Will Hamill 
    Date:   <date>

        added new file

So in order to squash these commits together into a single commit of glorious working tested code, here's what you want:

    $ git rebase -i HEAD~3

This will rebase the current branch, using the latest three changes (three back from HEAD inclusively). Change the number to include as many commits in the rebase as necessary.

    pick 491ea1e added new file
    pick 52f0741 updated the new file
    pick 5838dcb made a third change

    # Rebase 9305b58..5838dcb onto 9305b58

The -i modifier for rebase means 'interactive' so now a screen will show up giving you this prompt, and showing you your three separate commits listed.

    pick 491ea1e added new file
    squash 52f0741 updated the new file
    squash 5838dcb made a third change

    # Rebase 9305b58..5838dcb onto 9305b58

Changing the second and third options (press i to edit and then move around like in vim) to 'squash' means that the second and third commits will be rolled up into the first one, as if they'd been part of that commit all along. Be careful: If you delete a line, that commit will not be included in the new version of history! (This can be useful for removing specific mistakes, but that's one for another story)

Saving the changes (with esc -> :wq, or esc -> ZZ, like in vim) will select those commits for the new version of history and git will prompt you to pick a commit message for the commit being modified:

    # This is a combination of 3 commits.
    # The first commit's message is:
    added new file

    # This is the 2nd commit message:

    updated the new file

    # This is the 3rd commit message:

    made a third change

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    #
    # Date:     <date>
    #
    # rebase in progress; onto 9305b58
    # You are currently editing a commit while rebasing branch 'rebase_demo_branch' on '9305b58'.
    #
    # Changes to be committed:
    #       new file:   new_file.txt

The default behaviour here is to present you all of the commit messages for the commits you're including in the rebase, listed one after another. Now you can ensure that the right message shows up in the log for this combined change.

    # This is a combination of 3 commits.
    # The first commit's message is:
    added new file and added the second and third changes
    # This is the 2nd commit message:
    # This is the 3rd commit message:
    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    #
    # Date:      <date>
    #
    # rebase in progress; onto 9305b58
    # You are currently editing a commit while rebasing branch 'rebase_demo_branch' on '9305b58'.
    #
    # Changes to be committed:
    #       new file:   new_file.txt

You've modified the first line to include a message that's relevant to the changes made across all the commits, and deleted the second and third commit messages. Remember to make the commit message concise yet meaningful - it will be read in the context of the whole log, not in the context of your current task.

Now check your `git log` to see the cleaner history:

    $ git log
    
    commit d84709...
    Author: Will Hamill
    Date:   <date>

        added new file and added the second and third changes

Et voilà, your file and its updates are all merged into one commit. Now nobody will ever know you forgot to add the third change in with the second commit. Your secret is safe with git.

### Pulling changes from master

It is worth to pull changes from master frequently into your local branch while you work on your feature. If you want to retain ability to squash all your commits even after pulling changes from master, use git rebase instead of git merge. To do that run

    git rebase origin/master

How does it work? 

It takes your commits aside then puts the new commits from master on top of your branch, finally your commits are put back on top of that. In the process **your existing commits are changed** (rebased). If any conflicts arise, git will let you know and ask you to fix them commit by commit.

What is the result?

Your commits are still on the top of your branch, the commits from master are put beneath them, your commits are not the same anymore.


### Advanced Topics

*"I've already pushed my branch for a code review/created a pull request. I want to combine the commits I made before and after the review"*

That's fine, but it'll cause problems for anyone who has already checked out your branch if you change history and push again, as their version of the tree will conflict with yours. 

One approach to this is (if you're very sure), is to do a `git push origin your_branch_name --force` to forcibly set the version of the branch that the remote has to be yours, then ask the other people to delete their copy of the branch and pull it down again. 

This can be done after code review to squash any further commits into the previously rebased one. **Never do a push with --force on master unless know what you are doing.**

_"I've pulled master and merged it into my branch already, how do I squash all my previous commits together?"_

The short answer is "don't". Just pick out the commits for squashing after the latest master commits - and certainly don't modify any commits already on master made by anyone else. Anything more complex probably isn't worth the hassle. Avoid this by developing your features in small pieces and merging your work back into master more frequently. Long-lived branches build up more chances for merge issues and keep you out of sync with the rest of the team for longer.

