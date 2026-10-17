___
- tags: #path_traversal 
___
Also known as **Directory Traversal**, a web security vulnerability allows an attacker to read operating system resources, such as local files on the server running an application. The attacker exploits this vulnerability by manipulating and abusing the web application's URL to locate and access files or directories stored outside the application's root directory.
Path traversal vulnerabilities occur when the user's input is passed to a function such as file_get_contents in PHP.
## Location
### /etc/issue
Contains a message or system identification to be printed before the login prompt.
### /etc/profile
Controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived.
### /proc/version
Specifies the version of the Linux kernel.
### /etc/passwd
Has all registered users that have access to a system.
### /etc/shadow
Contains information about the system's user's passwords.
### /root/.bash_history
Contains the history commands for **root** user.
### /var/log/dmessage
Contains global system messages, incluiding the messages that are logged during system startup.
### /var/mail/root
All emails for **root** user.
### /root/.ssh/id_rsa
Private SSH keys foor a root or any known valid user on the server.
### /var/log/apache2/access.log
The accessed request for Apache web server.
### C:\boot.ini
Contains the boot options for computers with BIOS firmware.