# AWS Infrastructure Lab

Laboratorio práctico de infraestructura realizado en Amazon Web Services (AWS).

## Objetivo

Construir y configurar una infraestructura básica en AWS utilizando una instancia EC2, networking, acceso SSH, Nginx, almacenamiento S3 e IAM.

El laboratorio también incluyó pruebas de permisos y resolución de problemas de conectividad.

## Arquitectura

```text
Internet
   │
   ▼
VPC
   │
   ▼
Subnet
   │
   ▼
EC2
Ubuntu 24.04 LTS
   │
   ├── SSH
   │
   ├── Nginx
   │
   └── IAM Instance Profile
            │
            ▼
         IAM Role
            │
            ▼
       IAM Policy
            │
            ▼
            S3 
```text

EC2
Sistema operativo: Ubuntu 24.04 LTS
Instance Type: t3.micro
Región: us-east-1
Zona de disponibilidad: us-east-1c

La instancia EC2 fue utilizada como servidor Linux para practicar administración del sistema, acceso remoto, servicios y comunicación con otros servicios de AWS.

Networking

La infraestructura utilizó una VPC con el bloque:

172.31.0.0/16

Dentro de la VPC se utilizó una subnet:

172.31.16.0/20
Route Table

Se configuraron rutas para permitir comunicación local dentro de la VPC y salida hacia Internet mediante un Internet Gateway.

172.31.0.0/16 → local
0.0.0.0/0     → Internet Gateway
Internet Gateway

La VPC utiliza un Internet Gateway para permitir comunicación entre la red y el Internet público cuando las demás configuraciones de red lo permiten.

Security Group

Se configuró un Security Group para controlar el acceso a la instancia.

Reglas principales:

SSH  TCP 22  → IP del cliente /32
HTTP TCP 80  → 0.0.0.0/0

El acceso SSH se restringió a una dirección IP específica mediante /32.

Network ACL

También se revisó la Network ACL asociada a la subnet para comprobar que no estuviera bloqueando la comunicación.

SSH

La instancia fue administrada remotamente mediante SSH utilizando una clave privada.

Se practicó el uso de claves SSH y la protección de archivos de clave mediante permisos de Linux.

Nginx

Se instaló y verificó el servicio Nginx dentro de la instancia EC2.

También se comprobó la comunicación HTTP mediante el puerto 80.

S3

Se creó el bucket:

cloud-returnal-2999

Se utilizó S3 para practicar almacenamiento y operaciones con objetos mediante AWS CLI.

Los objetos de respaldo se organizaron bajo:

backup/

También se practicaron operaciones como:

Subir objetos.
Eliminar objetos.
Consultar metadatos.
Revisar permisos.
Trabajar con las claves de objetos de S3.
IAM

Se creó un IAM Role para permitir que la instancia EC2 interactuara con S3 sin almacenar Access Keys permanentes dentro del servidor.

IAM Role
EC2-s3-BackupRole
Instance Profile
EC2-S3-BackupProfile

La relación utilizada fue:

EC2
 ↓
Instance Profile
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3
Trust Policy

La Trust Policy permite que el servicio EC2 pueda asumir el Role mediante STS.

Permission Policy

El Role recibió permisos limitados sobre los objetos ubicados dentro de:

arn:aws:s3:::cloud-returnal-2999/backup/*

Los permisos utilizados incluyeron operaciones de lectura y escritura de objetos.

Principio de mínimo privilegio

Se practicó el principio de mínimo privilegio otorgando al Role solamente los permisos necesarios para trabajar con los objetos de respaldo.

Durante las pruebas, la instancia pudo realizar operaciones permitidas sobre los objetos, mientras que una operación no autorizada como listar el contenido del bucket produjo un error AccessDenied.

Esto permitió comprobar que los permisos IAM estaban siendo aplicados correctamente.

STS

Se utilizó AWS Security Token Service (STS) para comprobar qué identidad estaba utilizando la instancia EC2.

La comprobación permitió verificar que la instancia estaba utilizando el Role:

EC2-s3-BackupRole

en lugar de Access Keys configuradas manualmente dentro de la instancia.

Troubleshooting

Durante el laboratorio se presentó un problema de conexión SSH:

Connection timed out

Se investigó la conectividad revisando diferentes componentes de la infraestructura:

EC2
 ↓
Status Checks
 ↓
IP pública
 ↓
Route Table
 ↓
Internet Gateway
 ↓
Network ACL
 ↓
Security Group
 ↓
SSH

El problema se relacionó con la dirección IP autorizada en el Security Group.

La IP pública del cliente había cambiado, mientras que la regla SSH todavía permitía la dirección anterior.

Después de identificar y corregir la regla correspondiente, se pudo restablecer el acceso SSH.

Este proceso permitió practicar troubleshooting básico de infraestructura y conectividad en AWS.

Lo que practiqué
Administración básica de Linux.
SSH.
EC2.
VPC.
Subnets.
Route Tables.
Internet Gateway.
Security Groups.
Network ACL.
Elastic IP.
S3.
AWS CLI.
IAM Users.
IAM Roles.
IAM Policies.
Trust Policies.
Instance Profiles.
STS.
Principio de mínimo privilegio.
Troubleshooting de conectividad.
Configuración básica de servicios en una instancia Linux.
Nota

Este repositorio documenta un laboratorio práctico realizado en AWS. Algunas de las configuraciones y pruebas originales fueron realizadas directamente mediante AWS CLI y AWS Management Console y no todas las sesiones de terminal fueron conservadas como archivos.

Por este motivo, la documentación se centra en la infraestructura configurada, los conceptos practicados y las pruebas que pueden ser verificadas nuevamente.
