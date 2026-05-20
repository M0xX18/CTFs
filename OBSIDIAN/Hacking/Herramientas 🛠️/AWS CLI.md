---------- 
##### TAGS: #cloud #aws #herramientas #terminal  

------ 
# CONCEPTO 

> **AWS CLI** (Amazon Web Services Command Line Interface) es una herramienta oficial que permite interactuar con los servicios de **AWS** desde la línea de comandos. Facilita la administración de recursos en la [Nube](https://www.cloudflare.com/es-es/learning/cloud/what-is-the-cloud/) como instancias EC2, buckets S3, usuarios IAM y bases de datos, automatizando tareas sin necesidad de usar la consola web.

------------
## CONFIGURACIÓN INICIAL: 

Antes de usarla, se debe configurar con credenciales válidas:

```BASH 
aws configure
```

**Se solicitará:**
- AWS Access Key ID
- AWS Secret Access Key
- Región por defecto
- Formato de salida (json, text, table)

## USO: 

### Listar buckets S3:

```BASH 
aws s3 ls
```
### Listar instancias EC2:

```BASH 
aws ec2 describe-instances
```
### Listar usuarios en IAM:

```BASH 
aws iam list-users
```

### Subir un archivo del S3:

```BASH 
aws s3 cp malware.py s3://victim-bucket/
```

### Descargar un archivo del S3:

```BASH 
aws s3 cp s3://victim-bucket/passwords.txt .
```

#### Proyecto de GitHub: 
- **GitHub by AWS** [AWS CLI](https://github.com/aws/aws-cli)