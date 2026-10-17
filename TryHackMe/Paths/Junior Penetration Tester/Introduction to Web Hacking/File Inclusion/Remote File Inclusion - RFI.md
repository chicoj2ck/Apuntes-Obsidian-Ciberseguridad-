___
- tags: #rfi 
___
Remote File Inclusion (RFI) is a technique to include remote files into a vulnerable application.
One requirement for RFI is that the **allow_url_fopen** option needs to be **on**.
The risk of RFI is higher than LFI since RFI vulnerabilities allow an attacker to gain Remote Command Execution (RCE) on te server. Other consequences of a successful RFI attack include:
- Sensitive Information Disclosure
- Cross-site Scripting (XSS)
- Denial of Service (DoS)
![[Pasted image 20250905024525.png]]