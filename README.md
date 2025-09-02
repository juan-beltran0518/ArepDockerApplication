# ArepDockerApplication

Aplicación Spring Boot con Docker - Proyecto AREP

## Descripción

Esta es una aplicación Spring Boot containerizada con Docker. El proyecto demuestra la implementación de una aplicación web utilizando el framework Spring Boot y containerización con Docker.

## Tecnologías Utilizadas

- Java 17
- Spring Boot 3.5.5
- Maven
- Docker
- Docker Compose

## Estructura del Proyecto

```
├── src/
│   ├── main/
│   │   ├── java/
│   │   └── resources/
│   └── test/
├── infra/
│   └── docker/
│       └── .dockerignore
├── Dockerfile
├── docker-compose.yml
├── pom.xml
└── README.md
```

## Requisitos

- Java 17 o superior
- Maven 3.6+
- Docker
- Docker Compose (opcional)

## Cómo Ejecutar

### Usando Maven

```bash
# Construir el proyecto
mvn clean package

# Ejecutar la aplicación
java -jar target/docker-0.0.1-SNAPSHOT.jar
```

### Usando Docker

```bash
# Construir la imagen Docker
docker build -t arep-docker-app .

# Ejecutar el contenedor
docker run -p 6000:6000 arep-docker-app
```

### Usando Docker Compose

```bash
# Iniciar la aplicación
docker-compose up

# Iniciar en modo detached
docker-compose up -d

# Detener la aplicación
docker-compose down
```

## Configuración

- **Puerto:** 6000 (configurable mediante la variable de entorno PORT)
- **Perfil:** Perfiles por defecto de Spring Boot

## Endpoints de la API

La aplicación se ejecuta en `http://localhost:6000`

## Desarrollo

### Construir el proyecto

```bash
mvn clean compile
```

### Ejecutar pruebas

```bash
mvn test
```

### Construir JAR

```bash
mvn clean package
```

## Configuración de Docker

La aplicación utiliza un proceso de construcción Docker multi-etapa:

- **Imagen Base:** `openjdk:17-jdk-slim`
- **Directorio de Trabajo:** `/usrapp/bin`
- **Puerto:** 6000
- **Punto de Entrada:** Aplicación Java con configuración de classpath

## Licencia

Este proyecto es parte del curso AREP (Arquitecturas Empresariales).

