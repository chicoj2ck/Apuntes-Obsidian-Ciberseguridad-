___
- tags: #xss 
___
Blind XSS is similar to a stored XSS (which we covered in task 4) in that your payload gets stored on the website for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first.
## Potential impacts
Using the correct payload, the attacker's JavaScript could make calls back to an attacker's website, revealing the staff member's cookies, and even the contents of the portal page that is beign viewed.
A popular tool for Blind XSS attacks is [XSS Hunter Express]([XSS Hunter Express](https://github.com/mandatoryprogrammer/xsshunter-express)). Altough it's possible to make your own tool in JavaScript, this tool will automatically capture cookies, URLs, page contents and more.
