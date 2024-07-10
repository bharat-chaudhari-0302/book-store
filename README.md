
```markdown
# Book Store Application

This repository contains a Book Store application, which includes a catalog service. The project uses Docker for containerization, and Taskfile for task automation.

## Prerequisites

- [Docker](https://www.docker.com/get-started) installed
- [Task](https://taskfile.dev/installation/) installed
- [SDKMAN!](https://sdkman.io/install) installed
- Java 21 (managed via SDKMAN!)
- Maven 3.9.6 (managed via SDKMAN!)

## Project Structure

- **docker-compose.yml**: Configuration for Docker Compose.
- **.sdkmanrc**: Configuration file for SDKMAN to manage Java and Maven versions.
- **pom.xml**: Maven project configuration file.
- **Taskfile.yml**: Taskfile configuration for automating tasks.
```
## Setup

### 1. Install SDKMAN! and Set Up Environment

Install SDKMAN! by following the instructions on [SDKMAN!](https://sdkman.io/install).

Use SDKMAN! to install the required Java and Maven versions:

```bash
sdk env install
```

### 2. Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

### 3. Install Task

Install Task by following the instructions on [Taskfile.dev](https://taskfile.dev/installation/).

### 4. Build and Run the Application

To build and run the application locally, follow these steps:

#### a. Build the Project

This will format the code and build the Docker image for the `catalog-service` Spring Boot application:

```bash
task build
```

#### b. Start Infrastructure Services

Start the infrastructure services (like the database) using Docker Compose:

```bash
task start_infra
```

#### c. Start Application Services

Start the application services using Docker Compose:

```bash
task start
```
**You Can directly Start the task**

### 5. Access the Application

- **Catalog Service**: The catalog service will be available at `http://localhost:8081`.

### 6. Stop Services

To stop the services, run:

```bash
task stop
```

## Configuration Details

### Docker Compose

- **catalog-service**: The main service for the catalog, exposed on port 8081.
- **catalog-db**: The PostgreSQL database for the catalog service, exposed on port 15432.

### Taskfile

- **default**: Runs the `test` task.
- **test**: Formats the code and runs Maven tests.
- **format**: Formats the code using Spotless.
- **build**: Builds the Docker image for the catalog service.
- **start_infra**: Starts the infrastructure services using Docker Compose.
- **stop_infra**: Stops and removes the infrastructure services.
- **restart_infra**: Restarts the infrastructure services.
- **start**: Builds the project and starts both infrastructure and application services.
- **stop**: Stops and removes both infrastructure and application services.
- **restart**: Restarts both infrastructure and application services.
- **sleep**: Pauses execution for a specified duration.

## Environment Variables

The following environment variables are used in `docker-compose.yml` for the `catalog-service`:

- `SPRING_PROFILES_ACTIVE=docker`
- `DB_URL=jdbc:postgresql://catalog-db:5432/postgres`
- `DB_USERNAME=postgres`
- `DB_PASSWORD=postgres`
- `SWAGGER_API_GATEWAY_URL=http://api-gateway:8989/catalog`
- `MANAGEMENT_TRACING_ENABLED=true`
- `MANAGEMENT_ZIPKIN_TRACING_ENDPOINT=http://tempo:9411`

## Additional Configuration

### .sdkmanrc

This file ensures the correct Java and Maven versions are used:

```properties
java=21.0.1-tem
maven=3.9.6
```

### Maven Configuration (pom.xml)

The `pom.xml` file is configured for a multi-module project with the following properties:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>21</java.version>
    <maven.compiler.release>${java.version}</maven.compiler.release>
    <spotless-maven-plugin.version>2.43.0</spotless-maven-plugin.version>
</properties>
```

It includes a Spotless plugin configuration for code formatting.
