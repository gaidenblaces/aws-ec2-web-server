
# Security Group

Esta evidencia muestra las reglas de entrada y salida utilizadas por la instancia EC2.

## Reglas principales

- **SSH:** TCP `22` restringido a una dirección IP mediante `/32`.
- **HTTP:** TCP `80` permitido desde `0.0.0.0/0`.
- **Salida:** tráfico permitido hacia `0.0.0.0/0`.

## Qué demuestra

El Security Group fue utilizado como firewall virtual para controlar el acceso a la instancia EC2.

El acceso SSH se restringió para evitar permitir conexiones desde cualquier dirección de Internet.

Durante el laboratorio también se realizó troubleshooting de SSH. La dirección IP pública del cliente cambió y la regla SSH todavía contenía una dirección anterior, provocando:

`Connection timed out`

La revisión de las reglas del Security Group permitió identificar la causa y posteriormente recuperar el acceso SSH.
