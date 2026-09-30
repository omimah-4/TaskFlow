# TaskFlow API

## Project Description

TaskFlow API is a containerized RESTful Task Management API developed using FastAPI, PostgreSQL, Nginx, Docker, and Docker Compose.

The system provides a complete CRUD API for managing tasks and demonstrates containerization, service isolation, reverse proxy configuration, database integration, persistent storage, container security, failure recovery, and reproducible deployment.

---
## Architecture

The TaskFlow API follows a containerized three-tier architecture.

The system consists of three main services:

- Nginx: Acts as a reverse proxy and the only service exposed to the host.
- FastAPI: Provides the RESTful API and handles application logic.
- PostgreSQL: Stores task data persistently using a named Docker volume.

The communication flow is:

Client → Nginx → FastAPI → PostgreSQL → Named Volume

All services communicate through an internal Docker bridge network, while only Nginx publishes a port to the host.

### Architecture Diagram

```text
                    Client
                       |
                       | HTTP :8080
                       v
              +----------------+
              |     Nginx      |
              | Reverse Proxy  |
              +----------------+
                       |
                       | Internal Network
                       v
              +----------------+
              |    FastAPI     |
              |      API       |
              +----------------+
                       |
                       | Internal Network
                       v
              +----------------+
              |  PostgreSQL    |
              |    Database    |
              +----------------+
                       |
                       v
              +----------------+
              | Named Volume   |
              |    db-data      |
              +----------------+
```

### Network Isolation

The FastAPI and PostgreSQL services are not directly exposed to the host machine.

Only Nginx is accessible from the host through port `8080`.

This architecture improves service isolation, security, and maintainability.

## Technology Stack

- Python 3.12
- FastAPI
- PostgreSQL 16
- SQLAlchemy
- Nginx
- Docker
- Docker Compose
- REST API
- OpenAPI / Swagger UI

The application uses FastAPI for the backend API, PostgreSQL for persistent data storage, Nginx as a reverse proxy, and Docker Compose to manage and orchestrate the services.

## Project Structure

```text
TaskFlow/
├── api/
│   ├── src/
│   │   ├── main.py
│   │   ├── database.py
│   │   ├── models.py
│   │   └── schemas.py
│   ├── tests/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── requirements.txt
├── nginx/
│   └── nginx.conf
├── database/
├── docs/
├── compose.yaml
├── README.md
└── .gitignore
```

The project is organized into separate components for the API, reverse proxy, database configuration, documentation, and Docker Compose orchestration.

## Prerequisites

Before running TaskFlow API, make sure the following software is installed:

- Docker Desktop
- Git
- A web browser such as Microsoft Edge or Google Chrome

Docker Desktop must be running before starting the application.

No local installation of Python or PostgreSQL is required to run the complete system because the application and database run inside Docker containers.

## Quick Start

Clone the repository and move into the project directory:

```bash
git clone <REPOSITORY_URL>
cd TaskFlow
```

Start the complete system using Docker Compose:

```bash
docker compose up -d
```

Check the running containers:

```bash
docker compose ps
```

The application is available through Nginx at:

```text
http://localhost:8080
```

The interactive API documentation is available at:

```text
http://localhost:8080/docs
```

To stop the system:

```bash
docker compose down
```
## API Documentation

TaskFlow provides a RESTful API for managing tasks.

The interactive Swagger UI documentation is available at:

```text
http://localhost:8080/docs
```

### Available Endpoints

- `GET /api/tasks` - Get all tasks
- `GET /api/tasks/{task_id}` - Get a specific task
- `POST /api/tasks` - Create a new task
- `PUT /api/tasks/{task_id}` - Update an existing task
- `DELETE /api/tasks/{task_id}` - Delete a task

The API supports standard HTTP status codes such as `200`, `201`, `204`, and `404`.

## Docker Registry

The TaskFlow API image is hosted on Docker Hub.

Docker Hub Repository:

```text
https://hub.docker.com/r/omimah4/tastflow_api
```

Available image tags:

- `v1.0.0` - Versioned release image
- `latest` - Latest available image

The Docker image can be pulled using:

```bash
docker pull omimah4/tastflow_api:v1.0.0
```

The project uses versioned Docker images to support reproducible deployments and consistent application versions.

## Version Information

Current application version: `1.0.0`

Docker image version: `v1.0.0`

The project uses versioned Docker images to make deployments reproducible and to clearly identify the released version of the application.

The `latest` tag is also maintained as the latest available image.

## Team Members

This project was developed as a team project for the Cloud Computing and Containerization course.

- Team Member 1: Omimah Ghailan
- Team Member 2: Abeer 
- Team Member 3: Asmaa
- Team Member 4: _________
- Team Member 5: ________

## Project Features

TaskFlow API provides the following features:

- Complete CRUD operations for tasks.
- PostgreSQL database integration.
- Persistent database storage using a named Docker volume.
- Nginx reverse proxy configuration.
- Internal Docker bridge network.
- API port isolation from the host.
- Non-root API container execution.
- Health check for the PostgreSQL service.
- Containerized deployment using Docker Compose.
- Versioned Docker images hosted on Docker Hub.
- API testing through Swagger UI and HTTP requests.
- Failure and recovery testing for the API and database services.