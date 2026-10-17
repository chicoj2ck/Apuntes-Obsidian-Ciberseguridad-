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
Con Gobuster vamos a realizar la enumeracion por fuerza bruta de la api
### /api/v1/admin/
