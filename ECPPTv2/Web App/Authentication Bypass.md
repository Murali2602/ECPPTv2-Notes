
### Username Enumeration - 

Suppose you have a webpage with signup form that has a signup page and outputs error message saying that the username already exists we can make a list of usernames that can be used for other attacks.
![](https://i.imgur.com/Zx10TK2.png)

`ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.68.83/customers/signup -mr "username already exists"`

Output - 
![](https://i.imgur.com/nIaQi5Y.png)

---

### Bruteforcing Username and Password using ffuf -

`ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.68.83/customers/login -fc 200`

Here, we use W1 as our first placeholder for our username field and then we will use W2 as our second placeholder for our password field. We will give the http header type using `-X` which is POST in this case. We will specify the field attributes using `-d` and provide the placeholders which are W1 and W2 we will also use `-H` to provide the `Content-Type`. Finally we will use `-fc 200` to matching anything other than status code 200 because when we find a valid credentials it will usually redirect which would be a 301/302.

Output of the above command - 
![](https://i.imgur.com/Tt7o9ez.png)


---

### Cookie Tampering - 

##### Plaintext - 

Using cURL - 
`curl -H "Cookie: logged_in=true; admin=false" http://10.10.68.83/cookie-test`
We can set a cookie like this.

##### Hashed Cookie - 

Some cookies are hashed and they can be cracked using stuff like - `crackstation.net`

##### Encoding - 

Some cookies are encoded usually with base64, this is because encoding converts binary data to human-readable form and can be passed in urls/mediums

