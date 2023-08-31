
## Basic Usage - 

`ffuf -w wordlist.txt -u http://127.0.0.1:8080/FUZZ -o

#### Check for extensions - 
`ffuf -u http://10.10.30.225/indexFUZZ -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt`

Imp -> 
`ffuf -u http://10.10.30.225/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -e .php,.txt`


#### Filtering Responses -

Hiding 403 responses ->
We basically add `-fc 403`, here `-fc` is filter code and it will hide all the 403 responses
`ffuf -u http://10.10.30.225/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fc 403`

#### Matching Responses -

If you want to match only certain responses like get output of only 200, you can use `-mc 200`


#### Regex to find all files except ones starting with a dot

`ffuf -u http://10.10.30.225/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fr '/\..*'`