___
- tags: #xss 
___
As the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.
## Potential Impact
The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.
### How to test for Stored XSS
You'll need to test every possible point of entry where it seems data is stored and then shown back in areas that others users have access to; a small example of these could be:
- Comments on a blog
- User profile information
- Website Listings
Sometimes developers think limiting input values on the client-side is good enough protection, so changing values to something the web application wouldn't be expecting is a good source of discovering stored XSS.