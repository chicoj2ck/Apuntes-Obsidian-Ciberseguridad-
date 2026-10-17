___
- tags: #ssrf 
___
## What is an SSRF?
Stands for Server-Side Request Forgery. It's a vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the resource  of the attacker's choosing.
## Type of SSRF
There are two types of SSRF vulnerability
### Regular SSRF
Where data is returned to attacker's screen.
### Blind SSRF
Where SSRF occurs, but no information is returned to the attacker's screen.
## What's the impact?
A successsful SSRF attack can result in any of the following:
- Access to unauthorised areas.
- Access to customer/organisational data.
- Ability to Scale to internal networks.
- Reveal authentication token/credentials.
