# http-bouncer 

[![Build Status](https://travis-ci.org/raelgor/http-bouncer.svg?branch=master)](https://travis-ci.org/raelgor/http-bouncer)

A small IP and JSON API request based HTTP security system for express apps.

### Install

```
npm install http-bouncer
```

### Example

```js
var express = require('express'),
    app = express(),
    bouncer = require('http-bouncer'),
    bodyParser = require('body-parser');

// You need this to use the bouncer for JSON API calls
app.use(bodyParser.json({}));

// Configure the bouncer
bouncer.config = {

    // These values mean that 40 requests will be answered
    // per IP address every 10 secs
    GLOBAL_IP_CHECK_INTERVAL: 10000,
    GLOBAL_IP_PER_INTERVAL: 40,
    
    JSON_API_CALLS: [
        {
            MATCH: {
                    api: "core",
                    request: "login"
            },
            INTERVAL: 10000,
            LIMIT: 10,
            INCLUDE_IP: true,
            INCLUDE_FROM_MATCH: ["username"]
        }
        
        // More matches...
    
    ]

};

app.use('*',bouncer);

// Next route...
```
