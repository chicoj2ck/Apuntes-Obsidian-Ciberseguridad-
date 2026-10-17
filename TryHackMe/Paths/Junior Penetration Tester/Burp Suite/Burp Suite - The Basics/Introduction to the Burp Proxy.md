___
- tags: #burp_suite 
___
## Key Points to Understand About the Proxy
### Intercepting Requests
 When requests are made through the Burp Proxy, they are intercepted and held back from reaching the target server.
The requests appear in the Proxy tab, allowing for further actions such as forwarding, dropping, editing, or sending them to other Burp modules.
### Taking Control
THe ability to intercept requests empowers testers to gain complete control over web traffic, making it invaluable for testing web applications.
### Capture and Logging
Captures and logs requests made through the proxy by default, even when the interception is turned off. This logging functionality can be helpful for later analysis and review of prior requests.
### WebSocket Support
Burp Suite also captures and logs WebSocket communication, providing additional assistance when analysing web applications.
### Logs and History
The captured requests can be viewed in the HTTP history and WebSocket history sub-tabs, allowing for retrospective analysis and sending the request to other Burp modules as needed.
## Some Notable Feature in the Proxy settings
### Response Interception
By default, the proxy does not intercept server responses unless explicity requested on a per-request basis. The "intercept responses based on the following rules" checkbox, along with the defined rules, allows for a more flexible response interception.
### Match and Replace
The "Match and Replace" section in the **Proxy settings** enables the use of regular expressions (regex) to modify incoming and outgoing requests. This feature allows for dynamic changes, such as modifying the user agent or manipulating cookies.