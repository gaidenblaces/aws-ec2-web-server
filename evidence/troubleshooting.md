
# SSH Troubleshooting

Durante el laboratorio se presentó un problema de conexión SSH.

## Problema

La conexión hacia la instancia EC2 producía:

`Connection timed out`

## Investigación

Se revisaron diferentes componentes de la infraestructura:

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

## Causa

La dirección IP pública del cliente había cambiado.

El Security Group todavía tenía autorizada una dirección IP anterior mediante una regla `/32`.

## Solución

Se actualizó la regla SSH del Security Group para permitir la dirección IP actual.

Después de realizar el cambio, se recuperó el acceso SSH.

## Qué aprendí

Un error `Connection timed out` no significa necesariamente que SSH esté fallando.

El problema puede encontrarse en diferentes capas de la infraestructura, por lo que es necesario comprobar la conectividad de forma sistemática.
