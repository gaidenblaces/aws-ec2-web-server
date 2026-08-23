# ☁️ AWS Infrastructure Lab

Laboratorio práctico de infraestructura realizado en **AWS**.

Implementé y configuré una instancia **EC2** conectada a una **VPC**, con acceso **SSH**, servidor **Nginx**, almacenamiento **S3** y permisos mediante **IAM** y **AWS CLI**.

---

## 🎯 Objetivo

Practicar la creación, configuración y troubleshooting de infraestructura básica en AWS.

---

## 🏗️ Arquitectura

**Internet → VPC → Subnet → EC2 → IAM Role → S3**

---

## ☁️ EC2

| Configuración     | Valor            |
| ----------------- | ---------------- |
| Sistema operativo | Ubuntu 24.04 LTS |
| Instance Type     | `t3.micro`       |
| Región            | `us-east-1`      |
| Zona              | `us-east-1c`     |

La instancia se utilizó como servidor Linux para practicar administración, acceso remoto y comunicación con servicios de AWS.

---

## 🌐 Networking

| Recurso          | Configuración         |
| ---------------- | --------------------- |
| VPC              | `172.31.0.0/16`       |
| Subnet           | `172.31.16.0/20`      |
| Internet Gateway | Configurado           |
| Route Table      | Ruta local + Internet |
| Network ACL      | Revisada              |
| Security Group   | SSH + HTTP            |

### Security Group

* **SSH** → TCP `22` → IP del cliente `/32`
* **HTTP** → TCP `80` → `0.0.0.0/0`

El acceso SSH fue restringido a una dirección IP específica.

---

## 🔑 SSH

La instancia fue administrada remotamente mediante **SSH** utilizando una clave privada.

También se practicó la protección de la clave mediante permisos de Linux.

---

## 🌐 Nginx

Se instaló y verificó **Nginx** dentro de la instancia EC2 y se comprobó el acceso mediante HTTP.

---

## 🪣 S3

**Bucket:** `cloud-returnal-2999`

Los objetos de respaldo se organizaron bajo:

`backup/`

Se practicaron:

* Subida de objetos
* Eliminación de objetos
* Consulta de metadatos
* Control de permisos

---

## 🔐 IAM

**IAM Role:** `EC2-s3-BackupRole`

**Instance Profile:** `EC2-S3-BackupProfile`

Flujo de permisos:

**EC2 → Instance Profile → IAM Role → IAM Policy → S3**

Los permisos fueron limitados a los objetos dentro de:

`cloud-returnal-2999/backup/*`

---

## 🛡️ Mínimo privilegio

Se configuraron permisos específicos para las operaciones necesarias sobre los objetos de respaldo.

Durante las pruebas, una operación no autorizada como listar el bucket produjo:

`AccessDenied`

Esto permitió comprobar que los permisos IAM estaban siendo aplicados correctamente.

---

## 🔎 Troubleshooting

Durante el laboratorio apareció:

`Connection timed out`

Se investigó la conectividad revisando:

**EC2 → Status Checks → IP pública → Route Table → Internet Gateway → Network ACL → Security Group → SSH**

La causa fue una regla SSH que todavía utilizaba una dirección IP anterior.

La IP pública del cliente había cambiado. Después de actualizar la regla correspondiente, se recuperó el acceso SSH.

---

## 📚 Lo que practiqué

**Linux · SSH · EC2 · VPC · Subnets · Route Tables · Internet Gateway · Security Groups · Network ACL · Elastic IP · S3 · AWS CLI · IAM · IAM Roles · IAM Policies · STS · Mínimo privilegio · Troubleshooting**

---

## 📸 Evidencias

Las configuraciones y pruebas principales del laboratorio están documentadas en [`evidence/`](./evidence/).

Incluyen:

* EC2
* Networking
* Security Group
* VPC y Subnet
* Route Table
* Internet Gateway
* S3
* IAM Role
* IAM Policy
* STS
* Troubleshooting

---

## 📌 Nota

Este repositorio documenta un laboratorio práctico realizado mediante **AWS Management Console y AWS CLI**.

No todas las sesiones originales de terminal fueron conservadas, por lo que la documentación se centra en la infraestructura configurada, las decisiones tomadas y las pruebas realizadas.
