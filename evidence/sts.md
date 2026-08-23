
# AWS STS

Esta evidencia muestra la identidad utilizada por la instancia EC2 al realizar una llamada a AWS STS.

## Prueba

Se ejecutó:

`aws sts get-caller-identity`

La respuesta mostró que la instancia estaba utilizando:

`EC2-s3-BackupRole`

## Qué demuestra

La EC2 obtiene credenciales temporales mediante el IAM Role asociado a su Instance Profile.

No fue necesario configurar Access Keys permanentes dentro de la instancia.

El flujo utilizado fue:

EC2
↓
Instance Profile
↓
EC2-s3-BackupRole
↓
Credenciales temporales
↓
AWS STS
