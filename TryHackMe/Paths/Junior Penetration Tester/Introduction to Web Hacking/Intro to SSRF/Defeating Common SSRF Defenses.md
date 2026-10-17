___
- tags: #ssrf 
___
There are usually two approaches to this, either deny list or an allow list.
## Deny List
A Deny List is where all request are accepted apart from resources specified in a list or matching a particular pattern. A Web Application may employ a deny list to protect sensitive endpoints. IP addresses or domains from being accessed by the public while still allowing access to other locations.

Attacker can bypass a Deny List by using alternative localhost references such as :
``` txt
0, 0.0.0.0, 0000, 127.1, 127.*.*.*, 2130706433, 017700000001 or subdomains that have a DNS record which resolves to the IP Address 127.0.0.1 such as 127.0.0.1.nip.io.
```

Also, in cloud environment, it would be beneficial to block access to the IP address 169.254.169.254, which  contains metadata fot the deployed cloud server, incluiding possibly sensitive information. An attacker can bypass this by registering a subdomain on their own domain with a DNS record that points to the IP Address 169.254.169.254.
## Allow List
An allow list is where all request get denied unless they appear on a list or match a particular pattern.

### Example
```shell
# oficial site
https://website.thm

# attacker domain
https://website.thm.attacker-domain.thm.
```
## Open Redirect
If the above bypasses do not work, there is one more trick up the attacker's sleeve. An open redirect is an endpoint on the server where the website visitor gets automatically redirected to another website address.
### Example
```txt
https://website.thm/link?url=https://tryhackme.com
```


