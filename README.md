# ArepDockerApplication

Spring Boot Docker Application - AREP Project

## Description

This is a Spring Boot application containerized with Docker. The project demonstrates the implementation of a web application using Spring Boot framework and Docker containerization.

## Technologies Used

- Java 17
- Spring Boot 3.5.5
- Maven
- Docker
- Docker Compose

## Project Structure

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

## Requirements

- Java 17 or higher
- Maven 3.6+
- Docker
- Docker Compose (optional)

## How to Run

### Using Maven

```bash
# Build the project
mvn clean package

# Run the application
java -jar target/docker-0.0.1-SNAPSHOT.jar
```

### Using Docker

```bash
# Build the Docker image
docker build -t arep-docker-app .

# Run the container
docker run -p 6000:6000 arep-docker-app
```

### Using Docker Compose

```bash
# Start the application
docker-compose up

# Start in detached mode
docker-compose up -d

# Stop the application
docker-compose down
```

## Configuration

- **Port:** 6000 (configurable via PORT environment variable)
- **Profile:** Default Spring Boot profiles

## API Endpoints

The application runs on `http://localhost:6000`

## Development

### Building the project

```bash
mvn clean compile
```

### Running tests

```bash
mvn test
```

### Building JAR

```bash
mvn clean package
```

## Docker Configuration

The application uses a multi-stage Docker build process:

- **Base Image:** `openjdk:17-jdk-slim`
- **Working Directory:** `/usrapp/bin`
- **Port:** 6000
- **Entry Point:** Java application with classpath configuration

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## License

This project is part of the AREP (Arquitecturas Empresariales) coursework.

## Author

- **Name:** [Your Name]
- **Email:** [Your Email]
- **University:** [Your University]
- **Course:** AREP - Arquitecturas Empresariales
