# TinyURL - URL Shortening Service

A simple URL shortening service built with Java and Spring Boot, inspired by services like TinyURL and Bitly. This application allows users to create short, easily shareable URLs that redirect to longer, original URLs.

## Features

- **URL Shortening**: Generate a unique short URL for any long URL.
- **URL Redirection**: Redirect users from a short URL to the original long URL.
- **Database Integration**: Store URL mappings using MongoDB, Redis, or Cassandra (configurable).
- **Docker Support**: Easily deployable using Docker and Docker Compose.

## Table of Contents

- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Docker Image](#docker-image)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
- [Technology Stack](#technology-stack)
- [License](#license)

## Getting Started

Follow these instructions to set up and run the project on your local machine.

### Prerequisites

- **Java 11** or higher
- **Maven** for building the project
- **Docker** and **Docker Compose** for containerized deployment

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/handson-academy/kerenc-tinyurl.git
   cd kerenc-tinyurl
   ```

2. **Build the Project**:
   Run the following command to build the project and generate a JAR file:
   ```bash
   mvn clean package
   ```

3. **Set Up Environment with Docker Compose**:
   Start the application and its dependencies (like MongoDB, Redis, or Cassandra) using Docker Compose:
   ```bash
   docker-compose up -d
   ```

   This will start all required services in the background.

## Usage

Once the application is running, you can interact with it via API endpoints or by accessing the service in your browser.

### Access the Service

- Open your browser and navigate to `http://localhost:8080` (or the port specified in your `application.properties`).
- Use the `/shorten` endpoint to create short URLs.
- Use the short URL (e.g., `http://localhost:8080/abc123`) to test redirection.

## Docker Image

This project is available as a Docker image on Docker Hub, making it easy to deploy and run.

### Pulling the Docker Image

To pull the Docker image from Docker Hub, use:

```bash
docker pull kerenco/kerenc-tinyurl:latest
```

### Running the Docker Container

After pulling the image, you can run it with:

```bash
docker run -p 8080:8080 kerenco/kerenc-tinyurl:latest
```

- This command maps port `8080` on your local machine to port `8080` in the container. Adjust this port if your application uses a different one.
- The application should now be accessible at `http://localhost:8080`.

### Building and Running Locally (Optional)

If you prefer to build and run the Docker image locally from this repository, use:

```bash
docker build -t kerenco/kerenc-tinyurl .
docker run -p 8080:8080 kerenco/kerenc-tinyurl
```

## Configuration

Customize the configuration by editing the `src/main/resources/application.properties` file. You can specify the database connection settings, server port, and other options.

#### Example Configuration Options

```properties
# Server configuration
server.port=8080

# MongoDB configuration (if using MongoDB)
spring.data.mongodb.uri=mongodb://mongo:27017/tinyurl

# Redis configuration (if using Redis)
spring.redis.host=redis
spring.redis.port=6379

# Cassandra configuration (if using Cassandra)
spring.data.cassandra.contact-points=cassandra
spring.data.cassandra.port=9042
```

## API Endpoints

| Method | Endpoint           | Description                                |
|--------|---------------------|--------------------------------------------|
| POST   | `/shorten`         | Creates a new short URL for a given URL.   |
| GET    | `/{shortCode}`     | Redirects to the original URL based on the short code. |

### Example Usage

#### Shorten a URL
- **Request**:
  ```http
  POST /shorten
  Content-Type: application/json
  {
    "url": "https://example.com/some/very/long/url"
  }
  ```

- **Response**:
  ```json
  {
    "shortUrl": "http://localhost:8080/abc123"
  }
  ```

#### Redirect with Short URL
- **Request**:
  ```http
  GET /abc123
  ```
  This redirects to `https://example.com/some/very/long/url`.

## Technology Stack

- **Java 11**
- **Spring Boot** - Backend framework
- **MongoDB, Redis, Cassandra** - Database (choose based on your configuration)
- **Docker & Docker Compose** - For containerization and deployment

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
