# ☁️ AWS Infrastructure Lab

Laboratorio práctico de infraestructura realizado en **AWS**.

Trabajé con **EC2, VPC, SSH, Nginx, S3, IAM y AWS CLI**, además de practicar troubleshooting de conectividad y permisos.

---

## 🎯 Objetivo

Practicar la creación y administración de infraestructura básica en AWS.

---

## 🏗️ Arquitectura

```text
Internet
    │
    ▼
   VPC
    │
  Subnet
    │
    ▼
   EC2
 Ubuntu 24.04
    │
    ▼
Instance Profile
    │
    ▼
 IAM Role
    │
    ▼
 IAM Policy
    │
    ▼
   S3
☁️ EC2
Configuración	Valor
Sistema operativo	Ubuntu 24.04 LTS
Instance Type	t3.micro
Región	us-east-1
Zona	us-east-1c

La instancia fue utilizada como servidor Linux para practicar administración, acceso remoto y comunicación con servicios de AWS.

🌐 Networking
Recurso	Configuración
VPC	172.31.0.0/16
Subnet	172.31.16.0/20
Internet Gateway	Configurado
Route Table	Ruta local + Internet
Network ACL	Revisada
Security Group	SSH + HTTP
Security Group
SSH  → TCP 22 → IP del cliente /32
HTTP → TCP 80 → 0.0.0.0/0

El acceso SSH fue restringido a una dirección IP específica.

🔑 SSH

Administré la instancia mediante SSH utilizando una clave privada.

También practiqué la protección de la clave mediante permisos de Linux.

🌐 Nginx

Instalé y verifiqué Nginx dentro de la instancia EC2 y comprobé el acceso mediante HTTP.

🪣 S3

Bucket:

cloud-returnal-2999

Los objetos de respaldo se organizaron bajo:

backup/

Se practicaron operaciones de:

Subida de objetos.
Eliminación de objetos.
Consulta de metadatos.
Control de permisos.
🔐 IAM

Para permitir que EC2 interactuara con S3 utilicé un IAM Role:

EC2-s3-BackupRole

Instance Profile:

EC2-S3-BackupProfile

Flujo de permisos:

EC2
 ↓
Instance Profile
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3

Los permisos fueron limitados a:

cloud-returnal-2999/backup/*
🛡️ Mínimo privilegio

Se configuraron permisos específicos para las operaciones necesarias sobre los objetos de respaldo.

Durante las pruebas, una operación no autorizada como listar el bucket produjo:

AccessDenied

Esto permitió comprobar que los permisos IAM estaban funcionando correctamente.

🔎 Troubleshooting

Durante el laboratorio apareció:

Connection timed out

Se investigó la conectividad siguiendo esta cadena:

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

La causa fue una regla SSH que todavía utilizaba una dirección IP anterior.

La IP pública del cliente había cambiado.

Después de actualizar la regla correspondiente, se recuperó el acceso SSH.

📚 Lo que practiqué
Linux
SSH
EC2
VPC
Subnets
Route Tables
Internet Gateway
Security Groups
Network ACL
Elastic IP
S3
AWS CLI
IAM
IAM Roles
IAM Policies
STS
Principio de mínimo privilegio
Troubleshooting de infraestructura
📌 Nota

Este repositorio documenta un laboratorio práctico realizado mediante AWS Management Console y AWS CLI.

No todas las sesiones originales de terminal fueron conservadas, por lo que el repositorio documenta principalmente la infraestructura configurada, las decisiones tomadas y las pruebas que pueden verificarse nuevamente.
