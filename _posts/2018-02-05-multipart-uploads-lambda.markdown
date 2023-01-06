---
layout: post
title:  "Handling Multipart Uploads in AWS Lambda"
date:   2018-02-05 01:00:00 -0600
categories: projects programming
---
![AWS Lambda](/assets/lambda.jpg)

I’ve been really vibing with the AWS Lambda + API Gateway combo a lot lately. If you don’t know about AWS Lambda, you really should check it out. It’s an event-driven, server-less compute system. Which is great for simple task based operations like handling a sign-up form, or resizing a user-uploaded image.

One problem I ran into was that out-of-the-box, Lambda doesn’t seem to completely handle `multipart/form-data`. So, of course, I wrote a very basic library today for doing just this. A big thanks to @myshenin for the tip on the API Gateway settings.

Checkout the source on GitHub:

https://github.com/dudewheresmycode/node-lambda-multipart

Here’s a basic example:

First install the library using NPM

```bash
npm install -S lambda-multipart
```

Now, we can parse the incoming multipart request from API Gateway Proxy in our Lambda function. Huzzah! 🎉

```javascript
var Multipart = require('lambda-multipart');

exports.handler = function(event, context, callback){

 //pass the event
 var parser = new Multipart(event);
 //or pass custom body/headers
 //var parser = new Multipart({headers:customHeaders, body:customBody});

 //emitted for each field detected
 parser.on('field',function(key, value){
   console.log('received field', key, value);
 });
 //emitted for each file/part detected
 parser.on('file',function(file){
   //file.headers['content-type']
   file.pipe(fs.createWriteStream(__dirname+"/downloads/"+file.filename));
 });
 //or wait until everything is done...
 parser.on('finish',function(result){
   //result.files (array of file streams)
   //result.fields (object of field key/values)
   console.log("Finished")
 });
}
```