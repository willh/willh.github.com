---
layout: post
title: "AWS API Gateway Java lambda proxy request and response objects"
description: "Use these request and response classes in order to access the whole HTTP request using an AWS Lambda proxy integration in API Gateway"
category: 
tags: ["aws", "lambda", "java", "configuration"]
---
{% include JB/setup %}

After my previous post on [configuring AWS Lambdas](http://willhamill.com/2016/11/09/aws-lambda-java-configuration-in-dynamodb) I've been playing around a bit more with using them in conjunction with [AWS API Gateway](http://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) to create a web application. 

If you're using API Gateway as the entry point for your [AWS Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html), it's probably going to be useful to have access to the path and query parameters as well as the headers for the HTTP request. If you create a [request mapping template](http://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-mapping-template-reference.html) in API Gateway, you can pick out each of these parameters and insert them into a custom request object sent to your lambda function. Any time you want to pick out a new query parameter, path parameter or header value then as well as updating your Lambda code you'll need to update your request mapping template and redeploy your API Gateway definition, which for something that's meant to just act as a front to a lambda seems like a lot of hassle.

If you configure your API Gateway to act as a lambda proxy instead of just as a function invocation then you can get the whole request passed into your lambda as a parameter. Check this magic box to have API Gateway pass the request straight through to your lambda function.

![AWS API Gateway lambda proxy configuration](../../../../assets/images/20161212_lambda_proxy_configuration.png)

However according to the tooltip on the AWS console:

> Requests will be proxied to Lambda with request details available in the `context` of your handler function  

I suspect this is a mistake, as it is contradicted by the [API Gateway simple proxy for lambda page](http://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-set-up-simple-proxy.html#api-gateway-simple-proxy-for-lambda-input-format):

> API Gateway maps the entire client request to the input event parameter of the back-end Lambda function  

Either way, the `context` object has no placeholder property into which a request can be shoved, so your `event` input parameter is the place to access these request params. If you're using [Node.JS](http://docs.aws.amazon.com/lambda/latest/dg/programming-model.html) or [Python](http://docs.aws.amazon.com/lambda/latest/dg/python-programming-model.html) as your lambda language of choice then dynamic typing is your saviour and you can just use the `event` properties that you need, but if you're [using Java](http://docs.aws.amazon.com/lambda/latest/dg/java-programming-model.html) like me (or in fact [C#](http://docs.aws.amazon.com/lambda/latest/dg/dotnet-programming-model.html) now that support has been added) then you'll need to define an input class matching the request object format.

The documentation on the above page is also slightly incorrect in that it shows a `message` object at the same level as an `input` object in the request, but the `message` is a response value returned by the example lambda from the documentation, and the `input` object's properties are in fact the top level properties on the request object. There's also an additional property called `isBae64Encoded` that will be attached to the request which I have included.

<br />

### POJO for the request object

Use the following ApiGatewayRequest object to properly map the incoming request to a POJO with access to headers, query parameters and path parameters. If you want to handle a POST body in the request, this is where you'll need to update your `body` property from `String` type to the POJO defining your HTTP POST request payload, otherwise for handling GET requests you can leave it as-is and it'll just be null. The sub-objects referenced inside can be found along with this class in my [lambda Github repository](https://github.com/willh/lambda-helloworld-config)

<script src="https://gist.github.com/willh/dc55a31467aa6be38497e1de19cf342b.js"></script>

Which depends on the RequestContext object

<script src="https://gist.github.com/willh/cb68cad2486565d87d4d3d7f961e1e05.js"></script>

Which in turn depends on the Identity object

<script src="https://gist.github.com/willh/4c40dd310f9fa205c406e1103f849f16.js"></script>

Please note: these object definitions are reverse-engineered from the actual data sent to a Java Lambda and may likely change in future based on updates to the AWS APIs!


### POJO for the response object

API Gateway proxy integrated lambdas need to return a response object containing a status code, any custom headers (to be merged with any AWS will add for you, like the X-Amzn-Trace-Id which will enable [AWS X-Ray](https://aws.amazon.com/xray/)), so the docs are fine in this regard. The return type from my lambda function is a string (the "hello world" message) so the `body` property is defined as a String here - if your lambda needs to return any more complex responses then is where you will add your POJO response object. I've included the example from my lambda definition below for reference.

<script src="https://gist.github.com/willh/24c98231591355d68534826211198d40.js"></script>

