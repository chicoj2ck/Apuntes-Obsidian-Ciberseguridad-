___
- tags: #xss 
___
Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without any validation.
## Potential Impacts
The attacker could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting theme to execute code on their browser, potentially revealing session or customer information.
### How to test for Reflected XSS
You'll need to test every possible point of entry; these include:
- Parameters in the URL Query String.
- URL File Path.
- Sometimes HTTP Headers (although unlikely exploitable in practice)
Once you've found some data which is being reflected in the web application, you'll then need to confirm that you can successfully run your payload.
