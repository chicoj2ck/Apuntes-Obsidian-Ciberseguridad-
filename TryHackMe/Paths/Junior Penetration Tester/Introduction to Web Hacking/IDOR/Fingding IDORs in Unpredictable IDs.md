___
- tags: #idor 
___
## Unpredictable IDs
If the Id cannot be detected using the above methods, an excellent method of IDOR[^1] detection is to create two accounts and swap the Id numbers between them. If you can view the others users'content using their Id number while still being logged in with a defferent account (or not logged in at all), you've found a valid IDOR vulnerability.
____
## Referencia
[^1]: [[What is an IDOR ...]].
