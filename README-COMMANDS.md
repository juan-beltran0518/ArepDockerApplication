# 📋 Resumen completo de comandos utilizados en el desarrollo del proyecto

## 🚀 **Comandos Maven**

```bash
# Limpiar y compilar el proyecto
mvn clean install
# Descripción: Limpia el directorio target, compila el código, ejecuta tests y genera el JAR

# Copiar dependencias al directorio target/dependency
mvn dependency:copy-dependencies -DoutputDirectory=target/dependency
# Descripción: Copia todas las dependencias JAR necesarias para ejecutar la aplicación

# Ejecutar la aplicación Spring Boot
mvn spring-boot:run
# Descripción: Ejecuta la aplicación directamente usando el plugin de Spring Boot

# Ejecutar con puerto personalizado
PORT=8080 mvn spring-boot:run
# Descripción: Ejecuta la aplicación en el puerto 8080 usando variable de entorno
```

## ☕ **Comandos Java**

```bash
# Ejecutar usando JAR compilado
java -jar target/docker-0.0.1-SNAPSHOT.jar
# Descripción: Ejecuta la aplicación usando el JAR "fat" generado por Spring Boot

# Ejecutar con puerto personalizado
PORT=8080 java -jar target/docker-0.0.1-SNAPSHOT.jar
# Descripción: Ejecuta el JAR con puerto específico usando variable de entorno

# Ejecutar usando classpath
java -cp "target/classes:target/dependency/*" com.arep.docker.DockerApplication
# Descripción: Ejecuta la aplicación usando classpath manual con clases y dependencias
```

## 🐳 **Comandos Docker - Instalación y verificación**

```bash
# Instalar Docker usando Homebrew
brew install --cask docker
# Descripción: Instala Docker Desktop en macOS usando Homebrew

# Verificar versión de Docker
docker --version
# Descripción: Muestra la versión instalada de Docker para verificar la instalación
```

## 🏗️ **Comandos Docker - Construcción de imágenes**

```bash
# Construir imagen Docker desde Dockerfile
docker build --tag dockersparkprimer .
# Descripción: Construye una imagen Docker usando el Dockerfile del directorio actual

# Listar todas las imágenes Docker
docker images
# Descripción: Muestra todas las imágenes Docker disponibles en el sistema local
```

## 🚢 **Comandos Docker - Ejecución de contenedores**

```bash
# Ejecutar contenedor en modo interactivo
docker run -p 6000:6000 dockersparkprimer
# Descripción: Ejecuta el contenedor mapeando el puerto 6000 en modo foreground

# Ejecutar contenedor en modo detached (background)
docker run -d -p 34000:6000 --name firstdockercontainer dockersparkprimer
docker run -d -p 34001:6000 --name firstdockercontainer2 dockersparkprimer
docker run -d -p 34002:6000 --name firstdockercontainer3 dockersparkprimer
# Descripción: Ejecuta 3 contenedores independientes en segundo plano con puertos diferentes
```

## 📊 **Comandos Docker - Gestión de contenedores**

```bash
# Listar contenedores activos
docker ps
# Descripción: Muestra todos los contenedores que están ejecutándose actualmente

# Listar todos los contenedores (activos e inactivos)
docker ps -a
# Descripción: Muestra todos los contenedores del sistema, incluyendo los parados

# Parar contenedores específicos
docker stop firstdockercontainer firstdockercontainer2 firstdockercontainer3
# Descripción: Detiene múltiples contenedores especificados por nombre

# Remover contenedores parados
docker rm firstdockercontainer3
# Descripción: Elimina completamente un contenedor parado del sistema

# Ver logs de un contenedor
docker logs firstdockercontainer
# Descripción: Muestra los logs de salida de un contenedor específico
```

## 🏷️ **Comandos Docker Hub - Tagging y Push**

```bash
# Crear tag para repositorio remoto
docker tag dockersparkprimer juanbeltra/firstprkwebapprepo
# Descripción: Crea una referencia (tag) de la imagen local hacia el repositorio de Docker Hub

# Verificar imagen etiquetada
docker images | grep juanbeltra/firstprkwebapprepo
# Descripción: Verifica que el tag se creó correctamente

# Login a Docker Hub
docker login
# Descripción: Autentica con Docker Hub usando credenciales (usuario y contraseña)

# Subir imagen a Docker Hub
docker push juanbeltra/firstprkwebapprepo
# Descripción: Sube la imagen etiquetada al repositorio público de Docker Hub
```

## 🐙 **Comandos Docker Compose**

```bash
# Ejecutar servicios definidos en docker-compose.yml
docker-compose up
# Descripción: Levanta todos los servicios definidos en el archivo compose (web + MongoDB)

# Ejecutar en modo detached
docker-compose up -d
# Descripción: Levanta servicios en segundo plano sin mostrar logs en consola

# Ver estado de los servicios
docker-compose ps
# Descripción: Muestra el estado actual de todos los servicios del compose

# Ver logs de todos los servicios
docker-compose logs
# Descripción: Muestra los logs combinados de todos los servicios del compose

# Ver logs de un servicio específico
docker-compose logs web
docker-compose logs db
# Descripción: Muestra logs de un servicio individual (web o base de datos)

# Parar todos los servicios
docker-compose down
# Descripción: Para y remueve todos los contenedores, redes y volúmenes del compose

# Parar servicios y remover volúmenes
docker-compose down -v
# Descripción: Para servicios y también elimina los volúmenes de datos persistentes
```

## 🌐 **URLs de testing utilizadas**

```bash
# Testing de la aplicación en diferentes puertos:
http://localhost:5000/greeting
http://localhost:8080/greeting
http://localhost:6000/greeting
http://localhost:34000/greeting
http://localhost:34001/greeting
http://localhost:34002/greeting
http://localhost:8087/greeting

# Testing con parámetros:
http://localhost:8087/greeting?name=TuNombre
# Descripción: URLs utilizadas para probar los endpoints REST en diferentes configuraciones de puertos
```

## 📁 **Archivos creados durante el proyecto**

### Dockerfile
```dockerfile
FROM openjdk:17-jdk-slim

COPY target/dependency /usrapp/bin/dependency

COPY target/classes /usrapp/bin

WORKDIR /usrapp/bin

CMD ["java", "-cp", ".:dependency/*", "com.arep.docker.DockerApplication"]
```

### docker-compose.yml
```yaml
version: '3.8'

services:
  web:
    image: dockersparkprimer
    ports:
      - "8087:6000"
    environment:
      - PORT=6000
    depends_on:
      - db

  db:
    image: mongo:4.4
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

### HelloRestController.java
```java
package com.arep.docker;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloRestController {

    @GetMapping("/greeting")
    public String greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format("Hello, %s!", name);
    }
}
```

### RestServiceApplication.java
```java
package com.arep.docker;

import org.springframework.boot.SpringApplication;

public class RestServiceApplication {

    public static void main(String[] args) {
        String port = System.getenv("PORT");
        if (port == null) {
            port = "5000";
        }
        System.setProperty("server.port", port);
        SpringApplication.run(RestServiceApplication.class, args);
    }
}
```

## 🎯 **Resumen de tecnologías y herramientas utilizadas**

- **Maven 3.x**: Gestión de dependencias y construcción del proyecto
- **Spring Boot 3.5.5**: Framework de aplicación web con servidor Tomcat embebido
- **Java 17**: Lenguaje de programación y runtime
- **Docker Desktop**: Plataforma de containerización
- **Docker Hub**: Repositorio público de imágenes Docker
- **Docker Compose v2**: Orquestación de múltiples contenedores
- **MongoDB 4.4**: Base de datos NoSQL (en contenedor separado)
- **macOS Terminal**: Interfaz de línea de comandos
- **Homebrew**: Gestor de paquetes para instalar Docker en macOS

## 🔄 **Flujo completo del proyecto**

1. **Desarrollo**: Creación de controladores REST con Spring Boot
2. **Compilación**: `mvn clean install` para generar JAR y dependencias
3. **Containerización**: `docker build` para crear imagen Docker
4. **Testing local**: `docker run` con diferentes puertos
5. **Múltiples instancias**: Despliegue de 3 contenedores simultáneos
6. **Orquestación**: `docker-compose` con web service + MongoDB
7. **Distribución**: `docker tag` y `docker push` a Docker Hub

## 📊 **Puertos utilizados en el proyecto**

| Puerto | Uso | Comando |
|--------|-----|---------|
| 5000 | Puerto por defecto de la app | `java -jar target/docker-0.0.1-SNAPSHOT.jar` |
| 6000 | Puerto dentro del contenedor | Dockerfile y docker-compose |
| 8080 | Puerto personalizado local | `PORT=8080 mvn spring-boot:run` |
| 8087 | Puerto externo docker-compose | `docker-compose up -d` |
| 34000-34002 | Puertos para múltiples instancias | `docker run -d -p 34000:6000` |
| 27017 | Puerto MongoDB | docker-compose.yml |

## 📋 **Comandos de limpieza**

```bash
# Parar todos los contenedores
docker stop $(docker ps -q)

# Remover todos los contenedores parados
docker rm $(docker ps -aq)

# Remover imágenes no utilizadas
docker image prune

# Limpiar completamente Docker
docker system prune -a
```

---
*Proyecto: Spring Boot REST API con Docker*  
*Fecha: Septiembre 2025*  
*Tecnologías: Java 17, Spring Boot 3.5.5, Maven, Docker, Docker Compose, MongoDB*
