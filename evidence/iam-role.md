
# IAM Role

Esta evidencia muestra el IAM Role utilizado por la instancia EC2 para acceder a S3.

## Configuración

- **Role:** `EC2-s3-BackupRole`
- **Instance Profile:** `EC2-S3-BackupProfile`
- **Duración máxima de sesión:** 1 hora

## Qué demuestra

La instancia EC2 utiliza un IAM Role para obtener permisos temporales de AWS.

Esto evita tener que almacenar Access Keys permanentes dentro del servidor.

La relación utilizada es:

EC2
↓
Instance Profile
↓
IAM Role
↓
IAM Policy
↓
S3
