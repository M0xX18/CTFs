----------
##### TAGS: #web #reconocimiento #herramientas #terminal #python 

------
# CONCEPTO

> **WPSeku** es una herramienta de seguridad de código abierto diseñada para auditar la seguridad de sitios web basados en [[WordPress]]. Su objetivo es identificar y enumerar las posibles vulnerabilidades presentes en una instalación de WordPress. La herramienta está escrita en [[Python 🐍]] y utiliza una base de datos de vulnerabilidades conocidas y problemas de seguridad para realizar los escaneos.

------------
## USO:
**WPSeku**  busca de vulnerabilidades conocidas en la versión de WordPress, en los plugins y temas instalados se puede ejecutar este escaneo de vulnerabilidades con el siguiente comando:

```BASH
python wpseku.py --url https://google.com
```

Si lo que quisiéramos es enumerar los usuarios existentes en el [[WordPress]] como gestor de contenido de esta pagina, debemos agregar el parámetro _"--enumerate"_ y le indicamos el valor _"u"_ para usuarios:

```BASH
python wpseku.py --url http://google.com --enumerate u
```

De la misma forma puede identificar la versión de WordPress instalada, así como la de los plugins y temas con el valor _"v"_:

```BASH
python wpseku.py --url http://example.com --enumerate v
```

Y proporciona información de plugins y temas instalados con el valor _"p"_ en el mismo parámetro

```BASH
python wpseku.py --url http://example.com --enumerate p
```

#### Proyecto de GitHub:
- **GitHub by andripwn** [WPSeku](https://github.com/andripwn/WPSeku)
