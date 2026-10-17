___
- tags: #lfi 
___
With PHP, using functions such as include, require, include_once, and require_once often contribute to vulnerable web applications.

## LFI Continued
We disscussed couple techniques to bypass filter within the include function.

### #3 lab - includes
We performing black box testing.
```txt
http://webapp.thm/index.php?lang=EN
```

The error message discloses significant information. By entering THM as input, an error message shows what the include function looks like: `include(languages/THM.php);`.

Also, the error message disclosed another important piece of information about the full web application directory path which is `/var/www/html/THM-4/`.

```php
It seems we could move out of the PHP directory but still, the include function reads the input with `.php` at the end! This tells us that the developer specifies the file type to pass to the include function. To bypass this scenario, we can use the NULL BYTE, which is `%00`.
```

It seems we could move out of the PHP directory but still, the include function reads the input with `.php` at the end! This tells us that the developer specifies the file type to pass to the include function. To bypass this scenario, we can use the NULL BYTE, which is `%00`.

```txt
../../../../etc/passwd%00")."php");
```

### #4 lab - file-get-contents
Developer decided to filter keywords to avoid disclosing sensitive information!.
There are two possible methods to bypass the filter. First, by using NullByte %00 or the current directory tick at the end the filtered keyword /..
Similary, if we try /etc/passwd/.., it result to be /etc/ and that's because we moved one to the root. Now if we try **/etc/passwd/.,** the result will be **/etc/passwd** since dot refers to current directory.

### #5 - include

```python
# try this
http://webapp.thm/index.php?lang=../../../../etc/passwd

#-> response
#-> include(includes/etc/passwd) [function.include]: failed to open stream:
```
If we check the warining message in the include(languages/etc/passwd) section, we know that the web application replaces the ../ with empty string. There are couples techniques we can use to bypass this.
First, we can send the following payload to bypass it: ....//....//....//....//etc/passwd
![[Pasted image 20250905023707.png]]

### #6 - include
Developer forces the include to read from a defined directory!