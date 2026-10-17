___
- tags: #lfi 
___
## What is File Inclusion?
Is a security vulnerability that occurs when a web application allows users to include files from the local file system.
![[Pasted image 20250902010321.png]]
## Why do File inclusion vulnerabilities happen?
File inclusion vulnerabilities are commonly found and exploited in various programming languages for web applications, such as PHP that are poorly written and implemented. The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. When the input is not validated, the user can pass any input to the function, causing the vulnerability.
## What is the risk of File inclusion?
By default, an attacker can leverage file inclusion vulnerabilities to leak data, such as code, credentials or other important files related to web application or operating system. Moreover, if  the attacker can write files to the server by any other means, file inclusion might be used in tandem to gain remote command execution **(RCE)**.
