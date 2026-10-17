___
- tags: #owasp #axfr
___
## Full Zone Transfer
Los ataques de zona, también conocido como ataques **AXFR**, son un tipo de ataque que se dirige a los servidores **DNS** y que permite a los atacantes obtener información sobre los dominios de una organización.

```shell
# axf => tipo de consulta 
# @127.0.0.1 => ip pública o privada
# chicoj2ck.org => dominio 

dig axfr @127.0.0.1 chicoj2ck.org
```