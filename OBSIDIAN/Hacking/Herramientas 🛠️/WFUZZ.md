----------
##### TAGS: #web #fuzzing #herramientas #terminal #bruteforce #enumeracion

------  
# CONCEPTO  
  
> **WFUZZ** es una herramienta de fuzzing web diseñada para descubrir recursos ocultos, parámetros vulnerables y posibles fallos en aplicaciones web. Funciona reemplazando la palabra clave **FUZZ** (o variantes como FUZ2Z) dentro de una URL, parámetro, header o cuerpo POST por valores de un diccionario [Wordlist](https://www.kali.org/tools/wordlists/). Es utilizada en pruebas de penetración y CTFs para enumeracion de directorios, parámetros y credenciales. Para mas info [WFUZZ](https://www.kali.org/tools/wfuzz/)
  
------------  
## USO:

#### Mas Común

La estructura básica de uso es:
  
```BASH  
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hc 404 http://www.google.com/FUZZ
```

Donde **FUZZ** será reemplazado por cada valor del diccionario.

#### Para GET

```BASH  
wfuzz -c -w users.txt "http://www.google.com/index.php?user=FUZZ" --hc 404
```
#### Para POST

```BASH  
wfuzz -c -w users.txt -w passwords.txt -m product -d "user=FUZZ&pass=FUZ2Z" --hc 401 http://192.168.0.20/login.php
```
## Parámetros:

* ***-c***
 El parámetro _"-c"_ sirve para que el output de wfuzz salga con colores.

```BASH 
wfuzz -c -w google.txt http://www.google.com/FUZZ
```

* ***-w***
 El parámetro _"-w"_ sirve para indicarle que [[WordLists]] deberia usarse en el fuzzing.

```BASH 
wfuzz -w /usr/share/SecLists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt http://www.google.com/FUZZ
```

* ***-t***
 El parámetro _"-t"_ sirve para manejar hilos lo que permite ir mas rapido en el proceso, pero genera mas ruido.

```BASH 
wfuzz -t 50 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://www.google.com/FUZZ
```

 **¿Cuántos hilos usar?**
- 10–20 → Sigiloso
- 30–50 → Balanceado
- 80–150 → Agresivo
- 200+ → Puede romper el target o red

⚠️ Demasiados hilos pueden causar:
- rate limiting
- bloqueos
- falsos negativos
- pérdida de paquetes

* ***--hc***
 El parámetro _"--hc"_ permite ocultar los codigos de respuesta especificos por ejemplo el codigo 404
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hc 404 http://www.google.com/FUZZ
```

* ***--sc***
 El parámetro _"--sc"_ sirve para mostrar los codigos de respuesta especificos por ejemplo el codigo 204
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --sc 204 http://www.google.com/FUZZ
```

* ***--hl***
 El parámetro _"--hl"_ permite ocultar un numero especifico de lineas en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hl 11 http://www.google.com/FUZZ
```

* ***--sl***
 El parámetro _"--sl"_ permite mostrar un numero especifico de lineas en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --sl 6 http://www.google.com/FUZZ
```

* ***--hw***
 El parámetro _"--hw"_ permite ocultar un numero especifico de palabras en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hw 11 http://www.google.com/FUZZ
```

* ***--sw***
 El parámetro _"--sw"_ permite mostrar un numero especifico de palabras en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --sw 6 http://www.google.com/FUZZ
```

* ***--hh***
 El parámetro _"--hh"_ permite ocultar un numero especifico de caracteres en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hh 11 http://www.google.com/FUZZ
```

* ***--sh***
 El parámetro _"--sh"_ permite mostrar un numero especifico de caracteres en la respuesta.
 
```BASH 
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --sh 6 http://www.google.com/FUZZ
```

* ***--d***
 El parámetro _"--d"_ permite enviar datos por POST.
 
```BASH 
wfuzz -w wordlist.txt -d "id=FUZZ" http://www.google.com/FUZZ
```

* ***--H***
 El parámetro _"--H"_ permite agregar headers a las solicitudes HTTP.
 
```BASH 
wfuzz -w tokens.txt -H "Authorization: Bearer FUZZ" http://www.google.com/FUZZ
```

* ***--X***
 El parámetro _"--X"_ permite especificar el metodo HTTP por ejemplo PUT.
 
```BASH 
wfuzz -X PUT -w wordlist.txt http://www.google.com/FUZZ
```

* ***--b***
 El parámetro _"--b"_ permite enviar cookies personalizadas en cada petición. Es útil cuando la aplicación requiere sesión activa o cuando quieres fuzzear el valor de una cookie específica.
 
```BASH 
wfuzz -c -w tokens.txt -b "session=FUZZ" --hc 404 http://www.google.com/
```

#### Proyecto de GitHub: 
- **GitHub by xmendez** [WFUZZ](https://github.com/xmendez/wfuzz)