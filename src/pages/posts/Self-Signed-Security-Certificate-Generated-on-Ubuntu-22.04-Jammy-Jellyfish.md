---
layout: ../../layouts/MarkdownPostLayout.astro
title: 'Self-Signed Security Certificate Generated on Ubuntu 22.04 Jammy Jellyfish'
pubDate: 2023-06-11
description: 'A brief tutorial on creating an HTTPS web server in Node using Express.'
author: 'Cloud Huxley'
image:
    url: '/img/blog/security_certificate_generation.png'
    alt: 'Pulsar screengrab'
tags: ["self-signed", "certificate", "security", "HTTPS", "ubuntu"]
---
### Self-Signed Security Certificate Generated on Ubuntu 22.04 Jammy Jellyfish

The following article is for testing purposes only. This code was developed to help you understand the pieces required to build an HTTPS server using Node and Express.

#### **Prerequisites**
* [Install Node](/posts/Installing-Node-on-Ubuntu-22.04)
* [Install Pulsar](/posts/Installing-Pulsar-on-Ubuntu-22.04)

#### 1. Create a new project directory.
Replace `<directory_name>` with any name of your choosing. Do not include `<` or `>`, as they were only added to clarify semantics. From your terminal, enter these commands:</p>

```bash
$ mkdir <directory_name> && cd <directory_name>
```

```bash
$ mkdir node_https_express && cd node_https_express
```

#### 2. Create a hidden directory
by placing a period (`.`) in front of the directory name. This is where your certificate and key will live

```bash
$ mkdir .private
```

#### 3. Generate your security certificates

```bash
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout .private/localhost.key -out .private/localhost.crt -subj "/C=US/ST=Washington/L=Port Angeles/O=The Huxley Cloud/CN=localhost"
```

Note: To understand this command better check out the OpenSSL manpages

```bash
$ man openssl
```

#### 4. Initialize your working directory for NPM
```bash
$ npm init -y
```

#### 5. Open your project in Pulsar
```bash
$ pulsar .
```

#### 6. Install and configure Express
```bash
$ npm i --save express
```
```bash
$ touch index.js
```

#### 7. Open `index.js` in pulsar and add the following:
```js
// index.js
var fs = require('fs');
var http = require('http');
var https = require('https');
var privateKey  = fs.readFileSync('./.private/localhost.key', 'utf8');
var certificate = fs.readFileSync('./.private/localhost.crt', 'utf8');
var credentials = {key: privateKey, cert: certificate};
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('Hello World');
});

var httpServer = http.createServer(app);
var httpsServer = https.createServer(credentials, app);
httpServer.listen(8080);
httpsServer.listen(8443);
```

#### 8. Run your code as a super-user in order to access HTTPS
```bash
$ sudo node index
```

#### 9. Open your browser to the following location
[https://localhost:8443](https://localhost:8443/)

You should see a security warning. This is because the certificate is self-signed. Self-signed certificates are good for development, but unsafe for production servers.
<img src="/img/blog/potential_security_risk.png" class="img-fluid" alt="Potential Security Risk"/>

Click the “Advanced” button, and select “Accept the Risk and Continue”. Your site should now be loaded with a traditional “Hello World!” message.

#### Wrapping Up
Your test server is up and running. It isn’t much to look at, but it is my hope that you now understand the mechanics of using a security certificate to wrap your data in.
