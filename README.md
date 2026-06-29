# Bootcamp Configuration Repository

Repositorio centralizado de configuraciones para todos los microservicios del sistema bancario.

## Estructura

```
config/
├── ms-accounts/
│   ├── application.yaml          (base)
│   ├── application-dev.yaml      (desarrollo)
│   └── application-prod.yaml     (producción - cifrado)
├── ms-customer/
│   ├── application.yaml
│   ├── application-dev.yaml
│   └── application-prod.yaml
├── ms-credits/
├── ms-transaction/               (con Kafka)
├── ms-balance/
├── service-eureka/
└── service-gateway/              (enrutamiento)
```

## Cómo funciona

1. **Config Server** (service-config-server) lee desde este repositorio
2. Cada microservicio solicita su configuración por nombre (`spring.application.name`)
3. Config Server busca en `config/{application-name}/application-{profile}.yaml`
4. Descifra automáticamente valores con prefijo `{cipher}` usando su clave de encriptación

## Perfiles

- **application.yaml** - Configuración base (localhost)
- **application-dev.yaml** - Desarrollo local (logging, bases de datos locales)
- **application-prod.yaml** - Producción (credenciales cifradas, URLs remotas)

## Seguridad

Las contraseñas en `application-prod.yaml` están cifradas con `{cipher}` prefix:

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://user:{cipher}VALOR_CIFRADO@host:27017/db
```

El Config Server las descifra automáticamente usando la clave en `ENCRYPT_KEY`.

Ver [ENCRYPTION_GUIDE.md](../service-config-server/ENCRYPTION_GUIDE.md) en service-config-server para detalles.
