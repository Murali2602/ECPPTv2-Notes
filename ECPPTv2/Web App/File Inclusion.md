***Note: URL encode "/" using "%2f" so to like perform path traversal - you could use ..%2f..%2f..%2f***

Essential Parts of a URL - 
![](https://i.imgur.com/EwUoYia.png)

File Inclusion occurs when the user input is not sanitized/properly validated.

With File Inclusion the attacker can read sensitive data and also if somehow the attacker can write to the web app then they can also get Remote Code Execution i.e. reverse shell.

---

### Path Traversal -

Path/Directory Traversal is a vulnerability that allows an attacker to read operating system resources, such as local files on the server running an application. 

To test if Path Traversal vulnerability exists or not we can use `../../` syntax to move between directories. 
For example -
`http://webapp.thm/get.php?file=../../../../etc/passwd`

Here we can see that by going back few directories we can read the passwd file which contains the usernames in a linux system.

Interesting files for Path Traversal - 

![](https://i.imgur.com/96zND0a.png)
![](https://i.imgur.com/ldrdLgC.png)

---

### LFI (Local File Inclusion) - 

##### Basics -

This is when we can access/Invoke a local file inside the web server.
For example:
`http://webapp.thm/get.php?file=/etc/passwd`

Sometimes the webserver will have some kind of restriction such as only certain include function can call pages. 
For example:
`http://webapp.thm/index.php?lang=../../../../etc/passwd`
Here `lang` is the include function, we can pair this with the directory traversal method to read the contents of /etc/passwd.

---

##### Deep Dive into LFI -

**Bypassing Include Function Filters -**

Sometimes LFI works but the input is somewhat filtered out like the extension being fixed and stuff. 

For example if you want to access ../../../../../etc/passwd --> the filter would apply to it converting the input to ../../../../../etc/passwd.php which makes the file unreadable.
Eg: ![](https://i.imgur.com/XciiUFa.png)


We can bypass this particular filter using ***NULL BYTE***  - 
Null byte is basically used to terminate a string. Null bytes are represented using - `%00` in encoding and `0x00` in hex.
***The idea of using null byte is basically it terminates everything after it.***
>**NOTE**: the %00 trick is fixed and not working with PHP ***5.3.4*** and above.

Eg: `http://10.10.50.162/lab3.php?file=../../../../../../../etc/passwd%00`

Here, anything after `%00` is basically ignored by php

---

**Reading filtered files -** 

Sometimes some sensitive files might be filtered out which makes the file unreadable with normal tricks. For this we can either use Null Byte trick or the `/.`  which basically reads file from that directory.

---
**Reading from Input validation in place -**

Sometimes the input validation might be in place. For example with this the `../../../../` are all striped out and replace with empty strings.
Eg: ![](https://i.imgur.com/XZ2Mdtf.png)

**Bypass this issue -** 
![](https://i.imgur.com/wttcLyK.png)

Eg. Output:
![](https://i.imgur.com/M13Ew2F.png)

---

**Reading from forced/defined directory -**

This kind of LFI attack is when the webserver forces or allows stuff to work only from a certain directory. 

**Bypass** - We can bypass this by including the directory too in the path traversal. 

Eg: ![](https://i.imgur.com/XoA75Wd.png)

Eg. of bypass -
![](https://i.imgur.com/bvf06vU.png)



---

## RFI (Remote File Inclusion) -

RFI is when the attacker can inject remote files into the webserver and this can lead a variety of things such as RCE, DOS attacks etc.
> **Note**: One requirement for RFI is that the allow_url_fopen option needs to be on

**Basic php RFI syntax -** 
`<?PHP echo "Hello THM"; ?>`


### Apache .htaccess file

so if you can upload to a certain directory and the server is apache but they wont let you upload certain file extensions you could upload a .htaccess file and instruct it to allow your required extension file and execute em and then you could upload the actual file which would then work.

### Obfuscating File extensions 

1. You could try and see if its case sensitive or not like - 
`shell.php --> shell.pHp`
2. Provide multiple extensions. Depending on the algorithm used to parse the filename, the following file may be interpreted as either a PHP file or JPG image: **exploit.php.jpg**
3. Add trailing characters. Some components will strip or ignore trailing whitespaces, dots, and suchlike: **exploit.php.**
4. Try using the URL encoding (or double URL encoding) for dots, forward slashes, and backward slashes. If the value isn't decoded when validating the file extension, but is later decoded server-side, this can also allow you to upload malicious files that would otherwise be blocked: **exploit%2Ephp**
5. Add semicolons or URL-encoded null byte characters before the file extension. If validation is written in a high-level language like PHP or Java, but the server processes the file using lower-level functions in C/C++, for example, this can cause discrepancies in what is treated as the end of the filename: **exploit.asp;.jpg or exploit.asp%00.jpg**
6. Try using multibyte unicode characters, which may be converted to null bytes and dots after unicode conversion or normalization. Sequences like **xC0 x2E, xC4 xAE or xC0 xAE** may be translated to **x2E** if the filename parsed as a UTF-8 string, but then converted to ASCII characters before being used in a path.
7.  Other defenses involve stripping or replacing dangerous extensions to prevent the file from being executed. If this transformation isn't applied recursively, you can position the prohibited string in such a way that removing it still leaves behind a valid file extension. For example, consider what happens if you strip .php from the following filename: **`exploit.p.phphp`**




