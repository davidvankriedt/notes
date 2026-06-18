---
title: More about the web
draft: false
tags:
  - computer-science
  - cybersec
---
## MVC (Model View Controller Model)![[Screenshot 2026-06-18 at 11.05.14.png]]

### Alternative![[Screenshot 2026-06-18 at 11.05.39.png]]

## Cookies and Sessions
- HTTP is "stateless", to remember client data, we need "sessions", sessions are stored in the browser through "cookies" - cookies are a subset of sessions handled by the browser that lets domains remember you.
- Cookies can have restrictions like "HTTP-only", meaning it can only be accessed by HTTP, css nor js can access it (e.g. document.cookie wouldn't list cookies with that restriction).

## Hosting your own scripts

- use requestbin or webhook.site as a way to redirect traffic
- Setting up a Digital Ocean droplet and hosting an apache/nginx server.
- Using the uni systems - you have a way to host files.
- Anything tested locally can be done with a makeshift server:
  `$ python3 -m http.server 8000`

### Setting up on uni
- You can host static web files and PHP files on the uni system:
	- Make sure you've got a public_html folder with the right permissions, and files in that folder have the right permissions:
	- ```
		  $ ssh uni
		  % mkdir ~/public_html && chmod 755 ~/public_html
		  % cd ~/public_html
		  % echo "<script>alert('hello!')</script>" > ./test_script.js
		  % chmod 644 ./test_script.js
	  ```
	- Now the site http://www.cse.unsw.edu.au/~z5XXXXXX/test_script.js will be an alert script.
	- Remember this is public. Anyone can see this and all code executes will be run UNDER YOUR NAME.

## More Advanced XSS

- [Mining bitcoin](https://github.com/progranism/Bitcoin-JavaScript-Miner)
- [Keylogging](https://gist.github.com/abhineet97/445c25b29d1c25d9a13f)
## The XSS Run Through
1. Verify you have HTML injection and then XSS.
2. Bypass the WAF if you can.
3. Pop an alert on yourself.
4. Steal your own cookies. If you don't have a cookie for the application, set one.
5. Steal an admin's cookie.
6. Write about it. What you tried, what did work, what didn't work, what you would do next.

Front-end security is NOT real security - can bypass through [Burp](https://portswigger.net/burp)

[Blind SQLi](https://portswigger.net/web-security/sql-injection/blind)

** Check slides for more **