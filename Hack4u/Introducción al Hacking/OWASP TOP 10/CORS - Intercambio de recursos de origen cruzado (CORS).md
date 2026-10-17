___
- tags: #owasp  #cors
____
El **Intercambio de recursos de origen cruzado** (**CORS**) es un mecanismo que permite que un servidor web **restrinja** el **acceso a recursos** de **diferentes orígenes**, es decir, de diferentes dominios o protocolos. CORS se utiliza para proteger la privacidad y seguridad de los usuarios al evitar que otros sitios web accedan a información confidencial sin permiso.
## Laboratorio práctico
### Imagen del laboratorio
```shell
docker pull blabla1337/owasp-skf-lab:cors
```
### Corriendo la imagen descargada
```shell
docker run -ti -p 127.0.0.1:5000:5000 blabla1337/owasp-skf-lab:cors
```