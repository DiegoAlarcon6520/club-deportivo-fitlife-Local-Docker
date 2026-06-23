# Club Deportivo FitLife — Sistema de Gestión Integral

## Descripción

Club Deportivo FitLife es un sistema de gestión integral desarrollado como arquitectura de microservicios para administrar todas las operaciones de un club deportivo. El sistema permite gestionar socios, membresías, clases, asistencia, pagos, nutrición, equipamiento e instructores de forma independiente y escalable, con comunicación entre servicios mediante OpenFeign y descubrimiento de servicios a través de Eureka.

---

## Equipo de desarrollo

| Nombre | Rol |
|--------|-----|
| Diego Alarcon | Desarrollador |
| Sebastian Perez | Desarrollador |

**Profesor:** Christian Acuña  
**Asignatura:** Fullstack I — Sección 0_10D

---

## Microservicios implementados

| Microservicio | Puerto | Base de datos | Descripción |
|---------------|--------|---------------|-------------|
| `eureka` | 8761 | — | Servidor de descubrimiento de servicios |
| `config-server` | 8888 | — | Servidor de configuración centralizada |
| `socios-service` | dinámico | bd_socios | Gestión de socios, categorías y contactos de emergencia |
| `instructores-service` | dinámico | bd_instructores | Gestión de instructores, especialidades y cargas horarias |
| `equipamiento-service` | dinámico | bd_equipamiento | Gestión de equipos, salas y mantenimientos |
| `membresias-service` | dinámico | bd_membresias | Gestión de planes, membresías y congelamientos |
| `clases-service` | dinámico | bd_clases | Gestión de clases, horarios e inscripciones |
| `asistencia-service` | dinámico | bd_asistencia | Gestión de sesiones y registros de asistencia |
| `pagos-service` | dinámico | bd_pagos | Gestión de pagos, métodos de pago y deudas |
| `nutricion-service` | dinámico | bd_nutricion | Gestión de nutricionistas, planes nutricionales y evaluaciones |
| `api-gateway` | 8080 | — | Puerta de entrada única al sistema |

---

## Rutas principales del Gateway

### Socios
| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/v1/socios` | Listar todos los socios |
| GET | `/api/v1/socios/{id}` | Buscar socio por ID |
| POST | `/api/v1/socios` | Registrar nuevo socio |
| PUT | `/api/v1/socios/{id}` | Actualizar socio |
| DELETE | `/api/v1/socios/{id}` | Eliminar socio |
| GET | `/api/v1/socios/listado` | Listar socios como DTO |
| GET | `/api/v1/socios/reporte/estado` | Filtrar por estado |
| GET | `/api/v1/socios/reporte/rut` | Buscar por RUT |
| GET | `/api/v1/categorias/**` | Gestión de categorías |
| GET | `/api/v1/contactos/**` | Gestión de contactos de emergencia |

### Membresías
| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/v1/membresias` | Listar todas las membresías |
| GET | `/api/v1/membresias/{id}` | Buscar membresía por ID |
| POST | `/api/v1/membresias` | Registrar nueva membresía |
| PUT | `/api/v1/membresias/{id}` | Actualizar membresía |
| GET | `/api/v1/membresias/listado` | Listar membresías con socio hidratado |
| GET | `/api/v1/membresias/reporte/estado` | Filtrar por estado |
| GET | `/api/v1/planes/**` | Gestión de planes |
| GET | `/api/v1/congelamientos/**` | Gestión de congelamientos |

### Clases
| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/v1/clases` | Listar todas las clases |
| POST | `/api/v1/clases` | Registrar nueva clase |
| GET | `/api/v1/clases/reporte/nivel` | Filtrar por nivel de dificultad |
| GET | `/api/v1/inscripciones` | Listar inscripciones |
| POST | `/api/v1/inscripciones` | Inscribir socio a clase |
| GET | `/api/v1/inscripciones/listado` | Listado con socio hidratado |
| GET | `/api/v1/horarios/**` | Gestión de horarios |

### Pagos
| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/v1/pagos` | Listar todos los pagos |
| POST | `/api/v1/pagos` | Registrar nuevo pago |
| GET | `/api/v1/pagos/listado` | Listado con socio hidratado |
| GET | `/api/v1/pagos/reporte/estado` | Filtrar por estado |
| GET | `/api/v1/deudas` | Listar deudas |
| GET | `/api/v1/deudas/reporte/estado` | Filtrar deudas por estado |
| GET | `/api/v1/metodos-pago/**` | Gestión de métodos de pago |

---

## Documentación Swagger

La documentación interactiva está disponible a través del API Gateway:

| Servicio | URL Swagger | URL JSON |
|----------|-------------|----------|
| Swagger UI (todos) | http://localhost:8080/swagger-ui.html | — |
| Socios | — | http://localhost:8080/v3/api-docs/socios |
| Membresías | — | http://localhost:8080/v3/api-docs/membresias |
| Clases | — | http://localhost:8080/v3/api-docs/clases |
| Pagos | — | http://localhost:8080/v3/api-docs/pagos |

---

## Instrucciones de ejecución

### Modalidad Local (XAMPP)

**Requisitos:**
- Java 25
- Maven 3.9+
- IntelliJ IDEA
- XAMPP con MySQL activo

**Pasos:**

1. Inicia XAMPP y activa MySQL
2. Crea las bases de datos en MySQL (si no existen):
```sql
CREATE DATABASE IF NOT EXISTS bd_socios;
CREATE DATABASE IF NOT EXISTS bd_instructores;
CREATE DATABASE IF NOT EXISTS bd_equipamiento;
CREATE DATABASE IF NOT EXISTS bd_membresias;
CREATE DATABASE IF NOT EXISTS bd_clases;
CREATE DATABASE IF NOT EXISTS bd_asistencia;
CREATE DATABASE IF NOT EXISTS bd_pagos;
CREATE DATABASE IF NOT EXISTS bd_nutricion;
```
3. Ejecuta los microservicios en IntelliJ en este orden:
```
1. eureka
2. config-server
3. socios-service
4. instructores-service
5. equipamiento-service
6. membresias-service
7. clases-service
8. asistencia-service
9. pagos-service
10. nutricion-service
11. api-gateway
```
4. Espera ~30 segundos y accede a:
   - Swagger UI: http://localhost:8080/swagger-ui.html
   - Eureka Dashboard: http://localhost:8761

---

### Modalidad Docker

**Requisitos:**
- Docker Desktop instalado y en ejecución

**Pasos:**

1. Abre una terminal en la raíz del proyecto
2. Ejecuta:
```bash
docker compose up --build
```
3. Espera que todos los contenedores estén en estado `running` (~3-5 minutos)
4. Accede a:
   - Swagger UI: http://localhost:8080/swagger-ui.html
   - Eureka Dashboard: http://localhost:8761

**Para detener:**
```bash
docker compose down
```

**Para detener y limpiar volúmenes (reinicio completo):**
```bash
docker compose down -v
```

---

## Stack tecnológico

| Tecnología | Versión |
|------------|---------|
| Java | 25 |
| Spring Boot | 4.0.6 |
| Spring Cloud | 2025.1.1 |
| Spring Cloud Gateway | WebFlux |
| Spring Cloud Netflix Eureka | 5.0.1 |
| Spring Cloud OpenFeign | 5.0.1 |
| Spring Cloud Config | 5.0.1 |
| Flyway | 11.x |
| MySQL | 8.0 |
| Lombok | 1.18.x |
| SpringDoc OpenAPI | 3.0.2 |
| Docker | — |
