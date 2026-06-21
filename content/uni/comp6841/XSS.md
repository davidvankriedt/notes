---
title: XSS
draft: false
tags:
  - computer-science
  - cybersec
---
[[XSS]] (__Cross Site Scripting__) - A vulnerability that allows an attacker to run code on the client's web browser as if it were part of the website itself.

Original name came from being able to invoke a script from another website, across sites. These days it also includes scripts that are written and injected directly into the page. It can basically be called "JavaScript Injection".


### What can you do with XSS
- stealing sessions
- credential theft
- create a botnet
- mine crypto
- AdSense fraud
- anything you can do in JS

### Notable XSS Exploits
- Google search
- Counter Strike panorama XSS
- Self retweeting tweet
  
  
### Types of XSS

#### Stored
- code that is executed on a victim's browser is stored by an attacker into a database somewhere on the web application.
- classic example is a blog post or a comment.

#### Reflected
- A parameter sent from the user is reflected back onto the page.
- Usually requires phishing to exploit another person.
- Most common attack is to steal a session cookie.

#### Self
- This is a reflected XSS that can only affect yourself - e.g. reflected XSS where your own username is vulnerable.
- This is not usually paid out as a genuine vulnerability.

#### DOM
- Looks kinda like reflected XSS but you're writing to the [[DOM]] of the web page rather than returning the payload in the response - for more, COMP6843.

## More to look at:
CORS
burp suite
owasp
