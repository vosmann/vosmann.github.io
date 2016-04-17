---
layout: post
title:  "URL encoding inconsistencies"
date:   2016-01-20 12:00:00 +0100
categories: encoding http api url 
---

The specification expects basically every character to get URL-encoded, but some server implementations
such as Apache _don't_ allow some characters, the slash `/` for example, to get URL-encoded.

http://stackoverflow.com/questions/3235219/urlencoded-forward-slash-is-breaking-url


