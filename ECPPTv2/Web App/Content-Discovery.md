
1. Check Robots.txt 
2. Favicon - It can give us info about the framework used in a website - https://wiki.owasp.org/index.php/OWASP_favicon_database
Manually finding infor about the favicon - 
First find the favicon image by inspecting the page and then find the md5 hash of that image and compare it with the md5 hash in the website mentioned above.

3. Sitemap.xml - This is the opposite of robots.txt(basically list of files to be indexed by search engines will be listed here.)
You can usually access this by - /sitemap.xml

4. Google Dorking - 
![](https://i.imgur.com/l8MQrXN.png)

5. Subdomain Enumeration - Use - [Subfinder](https://github.com/projectdiscovery/subfinder)
You can also brute force subdomains using ***ffuf*** - 
` ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.29.13`
Here ffuf modifies the Host header to check for subdomain
But this will output everything and this is not what we need so we need to filter the response by response size using `-fs {}`
Eg: ` ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.29.13 -fs 2395`