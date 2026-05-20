---------- 
##### TAGS: #red #escaneo #herramientas #terminal 

------ 
# CONCEPTO 

> **NMAP** es una herramienta de código abierto especializada en el escaneo de redes y la identificación de dispositivos conectados. Facilita la evaluación de la seguridad al revelar puertos abiertos, servicios en ejecución y detalles sobre los sistemas en una red. Ampliamente utilizado para auditorías de seguridad y mapeo de topologías de red. 

------------
## USO: 
Para realizar un escaneo básico en una red, se puede ejecutar el siguiente comando en la terminal: 

```BASH 
nmap -v -sP 192.168.1.0/24
```

Si se desea realizar un escaneo más detallado, identificando versiones de servicios y sistemas operativos, se puede usar el siguiente comando:

```BASH 
nmap -v -A 192.168.1.1
```
### Escaneo común al hacer Maquinas o CTFs:

Recordar que este escaneo escanea todos los puertos abiertos y usa _-sS_ y no emite paquetes mas lentos que 5000 _(--min-rate 5000)_ y todo el escaneo queda registrado y es exportado en formato grepeable en el archivo allPorts

```BASH 
nmap -p- --open -T5 -sS --min-rate 5000 -vvv -n -Pn 192.168.0.20 -oG allPorts
```
### Escaneo silencioso general:

Este escaneo se realiza de forma lenta rápida y segura:

```BASH 
nmap -p- --open -T2 -sT -vvv -n -Pn 192.168.0.20 -oG allPorts
```
## PARÁMETROS:

* ***-n***
 El parámetro _"-n"_ sirve para no utilizar resolución DNS en el proceso.

```BASH 
nmap -p- 192.168.1.1 -n
```

* ***-p***
 Algunos otros parámetros útiles son _"-p21"_ para definir los puertos a escanear por ejemplo el 21, o escanear un rango por ejemplo _"-p1-100"_ para enumerar los primeros 100 puertos o para escanear todos los puertos usar _"-p-"_  para enumerar los 100 puertos mas comunes se utilizaría  _"--top-ports 100"_ o para enumerar varios puertos y específicos _"-p22,80"_.

```BASH 
nmap -p- 192.168.1.1 | nmap -p21- 192.168.1.1 | nmap -p1-100 192.168.1.1 | nmap --top-ports 100 192.168.1.1 | nmap -p22,80 192.168.1.1
```

* ***-T***
 El parámetro _"-T"_ es usado para establecer una velocidad en el escaneo siendo _"-T1"_ el mas lento pero mas silencioso o que pasa mas desapercibido y el _"-T5"_ el mas rápido o el mas agresivo que es el que hace mas ruido por así decirlo.

```BASH 
nmap -p- -T1 192.168.1.1 | nmap -p- -T2 192.168.1.1 | nmap -p- -T3 192.168.1.1 | nmap -p- -T4 192.168.1.1 | nmap -p- -T5 192.168.1.1
```

* ***-sS***
El parámetro _"-sS"_ en **NMAP** se utiliza para realizar un escaneo SYN, que es más rápido que un escaneo TCP completo (_-sT_). El escaneo SYN envía paquetes SYN al objetivo para determinar la disponibilidad de los puertos. Hay que tener en cuenta que **algunos sistemas de seguridad pueden detectar este tipo de escaneo.**

```BASH 
nmap -p22 -sS 192.168.1.1
```

* ***-sV***
**NMAP** ofrece la capacidad de realizar un escaneo de vulnerabilidades mediante el uso de scripts especializados con  _"-sV"_. Estos scripts permiten identificar posibles debilidades en servicios y sistemas, proporcionando información crucial para fortalecer la seguridad y se puede definir que tipo de script usar con  _"--script=(tipo de script)"_. Cabe resaltar que estos scripts están programados en [[Lua 🌕]] y puedes crear tus propios scripts.

```BASH 
nmap -sV --script=vuln 192.168.1.1
```

Scripts Disponibles:
	★ `vuln`: Escaneo de vulnerabilidades básico.
	★ `smb-vuln-*`: Escaneo de vulnerabilidades en servicios SMB.
	★ `ftp-vuln-*`: Escaneo de vulnerabilidades en servicios FTP.

* ***-sn***
Un parámetro útil para detectar que equipos están activos en la red es  _"-sn"_ el cual hace múltiples pings a todos los posibles equipos en la red con trazas [ICMP](https://es.wikipedia.org/wiki/Protocolo_de_control_de_mensajes_de_Internet) también llamado ["Ping Sweep"](https://en.wikipedia.org/wiki/Ping_sweep)

```BASH 
nmap -sn 192.168.1.0/24
```

* ***-sT***
El parámetro _"-sT"_ en **NMAP** especifica un escaneo TCP, que realiza una conexión completa con el objetivo para determinar la disponibilidad de los servicios en los puertos seleccionados. Este método establece una conexión completa con el puerto de destino para evaluar si está abierto o cerrado. Lo que hace es enviar una traza utilizando el SYN/ACK de TCP para determinar si esta cerrado o abierto el puerto

```BASH 
nmap -p22 -sT 192.168.1.1
```

* ***-sU***
 El parámetro _"-sU"_ en sirve para hacer el escaneo en UDP.

```BASH 
nmap -sU 192.168.1.1
```

* ***OTROS UTILES***
	 - El parámetro _"--open"_ reporta únicamente los puertos abiertos.
	 - El parámetro _"-v"_ de verbose sirve para mostrar los puertos a medida que los descubre.
	 - El parámetro _"-Pn"_ sirve para marcar todas las direcciones como activas, es comúnmente utilizado ya que si **NMAP** detecta que el host no esta activo no realizara el procedimiento.
	 - Para conocer otros parámetros y ver mas información de la herramienta se puede usar   _"--help"_ que desplegará todas las opciones que tiene la herramienta.

```BASH 
nmap -p- --open 192.168.1.1 -v -Pn
```
----------------
```BASH 
nmap --help
```

Además, **NMAP** puede generar un mapa visual de la red mediante la opción _"-sn"_ para escaneo de hosts y _"--topology"_ para generar un mapa topológico.

```BASH 
nmap -sn -T4 -oX output.xml 192.168.1.0/24 
nmap --topology -oX topology.xml 192.168.1.0/24
```
#### Proyecto de GitHub: 
- **GitHub by Nmap** [Nmap](https://github.com/nmap/nmap)