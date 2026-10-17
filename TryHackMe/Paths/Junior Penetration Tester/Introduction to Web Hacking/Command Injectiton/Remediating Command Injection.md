___
- tags: #command_injection 
___
Command Injection can be prevented in a variety of ways. The examples below are of the PHP programming language; however ; the same principles can be extended to many other languages.
## Vulnerable Functions
In PHP, many functions interact with the operating system to execute commands via shell; these include:
- Exec
- Passthru
- System
## Input Sanitisation
Sanitising any input from a user that an application uses is a great way to prevent command injection. This is a process of specifying the formats or types of data that a user can submit.

## Bypassing Filters
Applications will employ numerouts techniques in filtering and sanitising data that is taken from a user's input.
These filters will restrict you to specific payloads; however, we can abuse the logic behind application to bypass these filters.