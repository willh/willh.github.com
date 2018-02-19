---
layout: post
title: "Get alerts when an S3 bucket is made public in your AWS account"
description: "Avoid accidentally leaking customer data: using CloudTrail logs, CloudWatch Events, a NodeJS lambda function and Amazon SNS you can get email alerts when someone creates or modifies an S3 bucket to be public in your account."
category: 
tags: ["aws", "nodejs", "lambda", "henry"]
---
{% include JB/setup %}

### Nobody wants to be in the news for leaking customer data

If it's a slow news day (or if it's a [particularly egregious breach](http://www.bbc.co.uk/news/technology-41147513)) then [open S3 buckets](http://www.bbc.co.uk/news/amp/technology-40124146) [leaking customer data](http://www.bbc.co.uk/news/technology-42166004) seems to be [pretty common](http://www.bbc.co.uk/news/technology-43057681) to find in the [headlines](http://www.bbc.co.uk/news/technology-36128745). Accidentally leaving backups and other data in [Amazon S3](https://aws.amazon.com/s3/) storage 'buckets' which have public read - or worse, write - access enabled seems to be a common mistake.

### There's a hole in the bucket, dear Liza, dear Liza

To be fair, Amazon makes S3 buckets default to private, and they make it pretty hard to create a public S3 bucket without realising what you're doing when using the UI console: there are big banner warnings, and a bright orange 'public' marker next to any bucket in the list, but it seems people keep doing it. 

Perhaps people are creating the bucket via the command line, or setting up their resources via [CloudFormation](https://aws.amazon.com/cloudformation/) or [Terraform](https://www.terraform.io/intro/index.html) and not setting the right permissions parameters. Maybe they meant to make it public to test something, then secure it ["later"](http://www.dictionary.com/browse/never) and forgot. Maybe a nefarious hacker complete with Anonymous mask and dark hoodie has gotten in and is making your data easier to [hoover up](https://media.giphy.com/media/ZgWZKjoDaxs5y/giphy.gif). Maybe it was an intentionally public bucket that got reused for some reason.

Whatever the reason, it's probably good to know when someone in your organisation is creating a public S3 bucket, or modifying an existing bucket to grant public read or write access, just so you can check and see why and if that's what you really want.

### Get alerted when people create public S3 buckets in your account

To help with this, I've put together a couple of scripts that I'm calling [Henry](https://github.com/willh/henry) which can set up and stitch together a handful of AWS services to find when a bucket is created or modified to be open, and send you an email alert. The [source is available on GitHub](https://github.com/willh/henry), and it's pretty simple overall. Here's how it works:

![Process flow from S3 permission change to email alert](../../../assets/images/20180219_alert_open_s3_buckets.png)

This is based on a [NodeJS lambda function](https://aws.amazon.com/lambda/) triggered by a Cloudwatch Event rule, processing CloudTrail API logs to find S3 bucket permissions changes, and sending a notification via SNS (pronounced 'snooze', fact) if the bucket has public read or public write access.

Once you've been notified, you can go do something about it! Close the bucket off to public access, or stop worrying after talking to whoever created it and being satisfied with the use case. This setup won't _prevent_ a public bucket being created, and it's not quite realtime either (CloudTrail logs seem to take a minute or two to aggregate and be processed) but at least now you know. And [knowing is half the battle!](https://www.youtube.com/watch?v=ogEtfIdgjpY)

### Using Henry

Henry is really just a Terraform script which creates the audit trail, log event rule, triggers, etc and adds the code for the lambda function and ensures all the right permissions are set up so that the various services can talk to each other. If you want to just get to it, you can zip up the lambda function into `lambda.zip` and run the `henry.tf` script after [installing Terraform](https://www.terraform.io/intro/getting-started/install.html) and the [AWS CLI tools](https://aws.amazon.com/cli/). 

Henry requires AWS CLI tools to set up the email subscription, and it and Terraform require [your AWS credentials](https://www.terraform.io/docs/providers/aws/#shared-credentials-file). When you run the script it'll prompt you for the name of your audit trail log bucket, which has to be globally unique, and the email address to which you want it to send the alerts - like an Ops Team distribution list, for example. 

You can also just take the event-processing lambda function in `index.js` out by itself and set up your own preferred event triggers or results.

### What about item-level public access?

Good question! S3 buckets have permissions which apply as the default permissions to all bucket items, but it's entirely possible to specify override permissions on a per-item basis. Which is a long way to say you might have a private bucket but still have items that are publicly readable.  Henry is so simple that it barely justifies having a name, so it doesn't do anything like item-level permission change auditing yet. CloudTrail doesn't log S3 item-level operations by default, so this will require some changes to Henry's log trail setup.

If you want to audit bucket item-levels and in fact automatically set them back to private, there's a [blog post from AWS themselves here](https://aws.amazon.com/blogs/security/how-to-detect-and-automatically-remediate-unintended-permissions-in-amazon-s3-object-acls-with-cloudwatch-events/) which will set a similar set of event triggers and a lambda up for you (though it doesn't have a nice single package like a Terraform or CloudFormation script 😉)

### Future development

I've got some notes in the project `README.md` on where it can be extended in the future, but feel free to fork and send a pull request if there's something you think it should do. I'm [not exactly swimming in free time](https://en.wikipedia.org/wiki/Parenting) these days so the current points might take me a while.
