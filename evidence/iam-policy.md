
# IAM Policy

Esta evidencia muestra la política de permisos asociada al IAM Role de la instancia EC2.

## Permisos

La política permite operaciones de lectura y escritura sobre objetos de respaldo en S3.

Los permisos utilizados incluyen:

- `s3:GetObject`
- `s3:PutObject`

El acceso está limitado a:

`arn:aws:s3:::cloud-returnal-2999/backup/*`

## Principio de mínimo privilegio

La política no concede acceso administrativo a S3.

Los permisos están limitados a las operaciones necesarias sobre los objetos ubicados dentro del prefijo `backup/`.

Durante las pruebas, una operación no autorizada como `s3:ListBucket` produjo un error `AccessDenied`.

Esto permitió comprobar que la política estaba restringiendo correctamente los permisos del Role.
