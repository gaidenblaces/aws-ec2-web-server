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
