# 📝 Guía Técnica — MicroservicioV2

Microservicio REST desarrollado con Java + Spring Boot 3.5 que permite CRUD de productos y generación de boletas, con integración a Oracle Cloud (base de datos) y AWS S3 (almacenamiento de archivos). El proyecto ha sido dockerizado y preparado para despliegue.

---

## 📁 Estructura principal del repositorio

| Carpeta / Archivo            | Descripción                                      |
|-----------------------------|--------------------------------------------------|
| `src/`                      | Código fuente Java del microservicio             |
| `pom.xml`                   | Configuración de dependencias Maven              |
| `application.properties`    | Configuración del datasource y S3 (sin secretos) |
| `Dockerfile`                | Instrucciones para generar imagen Docker         |
| `Wallet_AZTBT.../`          | Archivos del wallet de Oracle Cloud              |
| `.vscode/`                  | Configuración local del entorno (VS Code)        |

---

## ▶️ Cómo compilar y ejecutar localmente

### 1. Limpiar y compilar:

```bash
mvn clean package
```

### 2. Ejecutar con Spring Boot:

```bash
mvn spring-boot:run
```

La API estará disponible en:  
📍 `http://localhost:8080`

---

## 🌐 Endpoints principales

| Método | Ruta                     | Descripción                                 |
|--------|--------------------------|---------------------------------------------|
| GET    | `/productos`             | Lista todos los productos                   |
| POST   | `/productos`             | Crea un nuevo producto                      |
| POST   | `/compras`               | Procesa compra y genera boleta              |
| POST   | `/api/s3/upload`         | Sube un archivo a AWS S3                    |
| GET    | `/api/s3/list`           | Lista archivos del bucket S3                |

---

## ☁️ Conexión a Oracle Cloud

- Se utiliza el wallet descargado de Oracle Cloud.
- El `application.properties` apunta a la ruta local del wallet:

```properties
spring.datasource.url=jdbc:oracle:thin:@dbname_high?TNS_ADMIN=Wallet_AZTBT2DD4GDVU52W
spring.datasource.username=usuario
spring.datasource.password=clave
```

---

## ☁️ Conexión a AWS S3 (temporal)

> Las claves fueron retiradas por seguridad.

Para conectarse nuevamente:
1. Crea un archivo `.env` con las siguientes variables:

```dotenv
AWS_ACCESS_KEY=AKIA...
AWS_SECRET_KEY=...
AWS_SESSION_TOKEN=...
```

2. Configura `AwsS3Service` para leer desde variables de entorno.

---

## 🐳 Dockerización

### 1. Construir imagen:

```bash
docker build -t microservicio-v2 .
```

### 2. Ejecutar contenedor:

```bash
docker run -p 8080:8080 microservicio-v2
```

---

## ✅ Estado actual

- [x] Subido correctamente a GitHub.
- [x] Credenciales sensibles eliminadas del historial.
- [x] Funciona con Oracle Cloud y AWS S3.
- [x] Listo para revisión, despliegue o pruebas.

---

