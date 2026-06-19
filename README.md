# Bootcamp Configuration Repository

Repositorio centralizado de configuraciones para todos los microservicios del sistema bancario.

## Estructura

- `ms-transaction.yaml` - Configuración de Transaction Microservice
- `ms-account.yaml` - Configuración de Account Microservice
- `ms-gateway.yaml` - Configuración de API Gateway
- etc.

Cada microservicio obtiene su configuración del Config Server que lee desde este repositorio.
