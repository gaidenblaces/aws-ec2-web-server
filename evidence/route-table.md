# Route Table

Esta evidencia muestra la tabla de enrutamiento utilizada por la subnet de la instancia EC2.

## Rutas principales

- `172.31.0.0/16` → `local`
- `0.0.0.0/0` → Internet Gateway

## Qué demuestra

La ruta `172.31.0.0/16` permite la comunicación dentro de la VPC.

La ruta `0.0.0.0/0` dirige el tráfico destinado a Internet hacia el Internet Gateway.

Esta configuración permite que los recursos de la subnet puedan comunicarse con Internet cuando las demás reglas de red lo permiten.
