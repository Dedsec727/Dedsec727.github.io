---
layout: post
title: Production Ready Express App
date: 2020-09-06 10:20
category: 
author: Prasanth Kanna
tags: [Express, NodeJS, Docker]
description: Explains how to implement a production ready web app using Express
image: express-production-ready-app/img.jpg
---

Express is one of the popular NodeJS frameworks to create web servers. Going through [Getting started](https://expressjs.com/en/starter/installing.html){:target="_blank"} page is enough to learn about Express but to make it into production a few best practices are mandatory. In this post, we implement a simple Express web server with all the best practices for production. It will contain following features:

* [GETTING STARTED](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Setup](#setup)
  
* [PERFORMANCE](#performance)
  * [Process Manager](#process-manager)
  * [Compression](#compression)
  * [Reverse Proxy](#reverse-proxy)
  * [Dockerization](#dockerization)
  
* [SECURITY](#security)
  * [Secrets](#secrets)
  * [Migrating to HTTPS](#migrating-to-https)
  * [Helmet](#helmet)
  * [Securing Session Cookies](#securing-session-cookies)
  * [Securing Dependencies](#securing-dependencies)

# Getting Started

## Prerequisites

* [Node & NPM (LTS)](https://nodejs.org/en/download/){:target="_blank"}
* [make (optional)](http://gnuwin32.sourceforge.net/packages/make.htm){:target="_blank"}
* [OpenSSL (optional)](https://slproweb.com/products/Win32OpenSSL.html){:target="_blank"}

## Setup

Run following commands to create a simple Express server:

{% highlight cmd %}
npm init (NOTE: Change the entrypoint to `app.js`)
npx express-generator --view=pug --git
npm i
npm install pug 
{% endhighlight %}

# PERFORMANCE

## Process Manager

> _RULE: Never run your app with 'npm start' in production_

If our web app crashes, we don't want our application to be offline until we manually restart our web app.

Using [PM2](https://www.npmjs.com/package/pm2){:target="_blank"} as process manager will handle following cases:

* Restarts our app if it crashes
* Reloads with zero downtime when invoked
* Built-in load balancer

**PM2 Setup**

* Run following cmd to install PM2:

{% highlight cmd %}
npm i pm2 -g
{% endhighlight %}

* Install node-cmd to launch our app in a console:

{% highlight cmd %}
npm i node-cmd
{% endhighlight %}

* Add file named `scripts.js` at our app's root with contents:

{% highlight js %}
var cmd = require('node-cmd');

switch (process.argv.slice(2)[0]) {
    case 'dev':
        cmd.run('npm run-script start:dev');
        break;
    case 'test':
        cmd.run('npm run-script start:test');
        break;
    case 'prod':
        cmd.run('npm run-script start:prod');
        break;
    default:
        console.log('Invalid env argument');
        process.exit(1);
}
{% endhighlight %}

* Add file named `ecosystem.config.js` (pm2 config file) at app's root with following contents:

{% highlight js %}
module.exports = {
  apps: [{
    name: 'Express-production-ready-template', // PM2 App name
    script: 'scripts.js', // script to execute
    instances: "max", // max instances of our app
    exec_mode: 'cluster', // runs our app with multiple instances
    env: {
      NODE_ENV: "development", // sets runtime environment
      args: 'dev', // arguments to the script
      watch: true // reloads when app changes
    },
    env_test: {
      NODE_ENV: "production",
      args: 'test',
    },
    env_production: {
      NODE_ENV: "production",
      args: 'prod',
    },
  }]
};
{% endhighlight %}

* Execute any of the following cmds to start our app using PM2 according to environment:

For Dev: `pm2 start ecosystem.config.js`

For Test: `pm2 start ecosystem.config.js --env test`

For Production: `pm2 start ecosystem.config.js --env production`

* Refer to [PM2 CheatSheet](https://pm2.keymetrics.io/docs/usage/quick-start/#cheatsheet){:target="_blank"} to learn all the commands for managing our server running on PM2

## Compression

**NOTE: ONLY REQUIRED WHEN NOT USING REVERSE PROXY**

[Gzip](https://www.gzip.org/){:target="_blank"} compressing can greatly decrease the size of the response body and hence increase the speed of a web app. 
Use the compression middleware for gzip compression in your Express app.

* Install [compression module](https://www.npmjs.com/package/compression){:target="_blank"} and import in `app.js`:

{% highlight cmd %}
npm i compression
{% endhighlight %}

{% highlight js %}
var compression = require('compression')
{% endhighlight %}

* Add compression middleware in `app.js`:

{% highlight js %}
app.use(compression()); //after app is initialized
{% endhighlight %}

## Reverse Proxy

* A reverse proxy sits in front of a web app and performs supporting operations on the requests, apart from directing requests to the app.
* It can handle error pages, compression, caching, serving files, and load balancing among other things.
* Handing over tasks that do not require knowledge of application state to a reverse proxy frees up Express to perform specialized application tasks.

**(COMING UP...)**

## Dockerization

* Dockerization can make it easy to ship our app to production
* It can auto start our app on server boot

**(COMING UP...)**

# SECURITY

## SECRETS

### Setting up Secrets

* We have to keep certain variables, like PORT, DB URL etc., configurable. We can do this by adding config.js and storing the values there. But this approach makes a compiled config.

* In order to achieve runtime config, we need to store our config values as environmental variables and load them to config.js. A simple [dotenv](https://www.npmjs.com/package/dotenv){:target="_blank"} approach is fair enough.
 
* But to load configs based upon the environment, it's better to user `.env-cmdrc` from [env-cmd](https://www.npmjs.com/package/env-cmd){:target="_blank"} module

Run following command to install env-cmd:

{% highlight cmd %}
npm install env-cmd
{% endhighlight %}

Create `.env-cmdrc` file at the root of the project with contents in following format:

{% highlight json %}
{
  "development": {
    "HTTPS_PORT": "3443",
    "SECRET_KEY": "Your server secret",
    "MONGO_URL": "Your MongoDB Connection string in dev",
    "JWT_EXPIRY_IN_SEC": "1800"
  },
  "test": {
    "HTTPS_PORT": "3443",
    "SECRET_KEY": "Your server secret",
    "MONGO_URL": "Your MongoDB Connection string in test",
    "JWT_EXPIRY_IN_SEC": "1800"
  },
  "production": {
    "HTTPS_PORT": "3443",
    "SECRET_KEY": "Your server secret",
    "MONGO_URL": "Your MongoDB Connection string in prod",
    "JWT_EXPIRY_IN_SEC": "1800"
  }
}
{% endhighlight %}

You can also add configs for staging environment if required

In `package.json` change the scripts to following:

{% highlight json %}
"scripts": {
    "start:dev": "env-cmd -e development node ./bin/www",
    "start:test": "env-cmd -e test node ./bin/www",
    "start:prod": "env-cmd -e production node ./bin/www"
  }
{% endhighlight %}

Now you can run any of the following commands(according to the environment) to start your application. All your configs will be loaded to environmental variables:

{% highlight cmd %}
npm run-script start:dev
npm run-script start:test
npm run-script start:prod
{% endhighlight %}

### Reading Secrets

* You can directly read the config values set in `.env-cmdrc` in any of your project's JS file as:

{% highlight js %}
process.env.HTTPS_PORT
process.env.SECRET_KEY
process.env.MONGO_URL
process.env.JWT_EXPIRY_IN_SEC
{% endhighlight %}

* But we have to remember the exact name of the config in `.env-cmdrc` and use them appropriately
* To read the config values in a comfortable manner, add a new folder `config` and create a file `config.js` and add following content to the file:

{% highlight js %}
const httpsPort = parseInt(process.env.HTTPS_PORT, 10)
const secretKey = process.env.SECRET_KEY;
const mongoURL = process.env.MONGO_URL;
const jwtExpiryInSec = parseInt(process.env.JWT_EXPIRY_IN_SEC, 10)

module.exports = {
    httpsPort,
    secretKey,
    mongoURL,
    jwtExpiryInSec
};
{% endhighlight %}

* You can now get the config values anywhere in your project as simply as:

{% highlight js %}
var config = require('../config/config');

var httpsPort = config.httpsPort;
var secretKey = config.secretKey;
var mongoURL = config.mongoURL;
var jwtExpiryInSec = config.jwtExpiryInSec
{% endhighlight %}

### Securing Secrets

> _RULE: Never commit your secrets file to source control_

We should not expose our secrets file to public. There are three approaches to do this:

* Store the secrets file on your own premises somewhere secure
* Commit a prototype of your secrets file with dummy values as a reference
* Encrypt the secrets file with a password and commit the encrypted file

OPTIONAL: First two approaches are straight forward. I'm going to implement the 3rd approach using makefile. I'll be using OpenSSL to encrypt the file.

* Add file named `makefile` to root of the project with following contents:
  {% highlight plain %}
  .PHONY: _pwd_prompt decrypt_conf encrypt_conf
  CONF_FILE=.env-cmdrc
  # 'private' task for echoing instructions
  _pwd_prompt:
    @echo Contact <your_email> for the password
  # to create .env-cmdrc
  decrypt_conf: _pwd_prompt
    openssl cast5-cbc -d -in ${CONF_FILE}.cast5 -out ${CONF_FILE}
    chmod 600 ${CONF_FILE}
  # for encrypting .env-cmdrc
  encrypt_conf: _pwd_prompt
    openssl cast5-cbc -e -in ${CONF_FILE} -out ${CONF_FILE}.cast5
  {% endhighlight %}

* Execute following command to encrypt the secrets file:

{% highlight cmd %}
make encrypt_conf
{% endhighlight %}

* To decrypt:

{% highlight cmd %}  
make decrypt_conf
{% endhighlight %}

* Enter password when prompted to encrypt/decrypt the file

## Migrating to HTTPS

npx-generator creates a basic HTTP server for us. But we must always use HTTPS for our server while in production.

* Get yourself a SSL Certificate for your server and store the certificate files(cert.pem & private key file) in a new folder named `certificates` in your project's root.

* Generating Self-signed Certificate:
  
  **ONLY FOR DEVELOPMENT PURPOSES. SKIP THIS STEP FOR PRODUCTION AND MAKE SURE YOU HAVE A CA SIGNED SSL CERTIFICATE**

  To generate a self-signed certificate, run following command in `certificates` folder:

{% highlight cmd %}  
openssl req -x509 -newkey rsa:4096 -keyout private.key -out cert.pem -days 365 -subj /CN=localhost -nodes
{% endhighlight %}

  The above command will generate two files: `cert.pem` and `private.key`. The private key will be unprotected without any passphrase & the certificate will be registered for the domain: `localhost` and valid for 365 days.

* Add following imports to `bin/www` file:
  
  {% highlight js %}
  var https = require('https');
  var fs = require('fs');
  var path = require('path');
  var config = require('../config/config')
  {% endhighlight %}

* replace each of the following striped lines accordingly

  ~~var port = normalizePort(process.env.PORT \|\| '3000');~~
  {% highlight js %}
  var httpsPort = normalizePort(process.env.PORT || config.httpsPort);
  {% endhighlight %}

  ~~app.set('port', port);~~
  {% highlight js %}
  app.set('httpsPort', httpsPort);
  {% endhighlight %}

  ~~var server = http.createServer(app);~~
  {% highlight js %}
  var options = {
    key: fs.readFileSync(path.join(__dirname, '../certificates/key.pem')),
    cert: fs.readFileSync(path.join(__dirname, '../certificates/cert.pem'))
  };
  var server = https.createServer(options, app);
  {% endhighlight %}

  ~~server.listen(port);~~
  {% highlight js %}
  server.listen(
    app.get('httpsPort'),
    () => {
      console.log('HTTPS Server listening on port: ', app.get('httpsPort'));
    }
  );
  {% endhighlight %}

* Now run your server and check at corresponding https URL

## Helmet

> _RULE: Never expose X-Powered-By header_

[Helmet](https://www.npmjs.com/package/helmet){:target="_blank"} can help protect your app from some well-known web vulnerabilities by setting HTTP headers appropriately.

Helmet is actually just a collection of smaller middleware functions that set security-related HTTP response headers:

* [csp](https://github.com/helmetjs/csp){:target="_blank"} sets the Content-Security-Policy header to help prevent cross-site scripting attacks and other cross-site injections.
* [hidePoweredBy](https://github.com/helmetjs/hide-powered-by){:target="_blank"} removes the X-Powered-By header.
* [hsts](https://github.com/helmetjs/hsts){:target="_blank"} sets Strict-Transport-Security header that enforces secure (HTTP over SSL/TLS) connections to the server.
* [ieNoOpen](https://github.com/helmetjs/ienoopen){:target="_blank"} sets X-Download-Options for IE8+.
* [noCache](https://github.com/helmetjs/nocache){:target="_blank"} sets Cache-Control and Pragma headers to disable client-side caching.
* [noSniff](https://github.com/helmetjs/dont-sniff-mimetype){:target="_blank"} sets X-Content-Type-Options to prevent browsers from MIME-sniffing a response away from the declared content-type.
* [frameguard](https://github.com/helmetjs/frameguard){:target="_blank"} sets the X-Frame-Options header to provide clickjacking protection.
* [xssFilter](https://github.com/helmetjs/x-xss-protection){:target="_blank"} sets X-XSS-Protection to enable the Cross-site scripting (XSS) filter in most recent web browsers.

### Setup

* Install helmet module and import it in `app.js`

{% highlight cmd %}
npm i helmet
{% endhighlight %}

{% highlight js %}
var helmet = require('helmet');
{% endhighlight %}

* Add helmet to express in `app.js`

{% highlight js %}
app.use(helmet()); //after app is initialized
{% endhighlight %}

## Securing Session Cookies

> _RULE: Always enable secure & httpOnly flags for all cookies_

* Install express-session module and import in `app.js`

{% highlight cmd %}
npm i express-session
{% endhighlight %}

{% highlight js %}
var session = require('express-session');
{% endhighlight %}

* Add session middleware in `app.js`

{% highlight js %}
  // session setup
  app.use(session({
    name: 'session-ID', //prevents fingerprinting our server so that the attacker will not know that backend is powered by express
    secret: config.secretKey, // used to sign session cookie
    resave: true, 
    saveUninitialized: true,
    cookie: {
      secure: true, // session is stored only over HTTPS
      httpOnly: true, // session is sent only over HTTP(S), not client JavaScript, helping to protect against cross-site scripting attacks.
      domain: 'localhost', // your app's domain in production
      maxAge: config.jwtExpiryInSec * 1000 // sets expiry time
    }
  }));
{% endhighlight %}

## Securing Dependencies

> _RULE: Always make sure you run `npm audit` and there are 0 vulnerabilities whenever you install a new npm module_
