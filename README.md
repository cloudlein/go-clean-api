# Go Clean Architecture API

This repository serves as a template for building RESTful APIs using Go (Golang), adhering to Clean Architecture principles. It is designed to demonstrate separation of concerns, scalability, and testability without reliance on specific frameworks or databases.

## Architecture Overview

The project follows the Clean Architecture pattern, organizing code into concentric layers. The dependency rule ensures that inner layers (Domain) contain no dependencies on outer layers (Infrastructure, Delivery).

### Layer Description

- **Domain (`internal/domain`)**: The core layer containing enterprise business rules. It includes entities (structs) and repository/usecase interfaces. This layer has zero dependencies.
- **Usecase (`internal/usecase`)**: Contains application business rules. It implements the business logic and orchestrates data flow using domain interfaces.
- **Repository (`internal/repository`)**: Interface adapters for persistence. It implements the domain repository interfaces, handling database operations (e.g., using GORM).
- **Delivery (`internal/delivery`)**: The external layer handling HTTP requests and responses. It uses the Gin framework to route requests to the appropriate usecases.

## Project Structure

```text
go-clean-api/
├── cmd/
│   └── api/            # Application entry point (main.go)
├── internal/
│   ├── domain/         # Entities and Interfaces
│   ├── usecase/        # Business Logic
│   ├── repository/     # Data Access Layer
│   ├── delivery/       # HTTP Handlers (Gin)
│   └── mocks/          # Mock objects for unit testing
├── pkg/
│   └── database/       # Shared infrastructure code (e.g., DB connection)
├── tests/              # Integration and End-to-End tests
├── .github/            # GitHub Actions CI/CD workflows
├── docker-compose.yml  # Container orchestration
└── Makefile            # Build and utility commands
```

## Prerequisites

- Go 1.20 or higher
- Docker and Docker Compose

## Getting Started

### 1. Configuration

Copy the example environment file and configure it according to your environment.

```bash
cp .env.example .env
```

### 2. Database Setup

Start the PostgreSQL database container using Docker Compose.

```bash
docker-compose up -d
```

### 3. Running the Application

Execute the application from the entry point.

```bash
go run cmd/api/main.go
```

The API will be accessible at `http://localhost:8080`.

## Testing

### Unit Tests

Unit tests are located alongside the source code in the `internal` directory. They utilize `stretchr/testify` for assertions and mocking.

### Integration Tests

Integration tests are located in the `tests/` directory and test the interaction between multiple components or the system as a whole.

### Running Tests

To execute all tests in the project:

```bash
go test -v ./...
```

## CI/CD

This project includes a GitHub Actions configuration (`.github/workflows/ci.yml`) that automatically runs builds and tests on every push and pull request to the main branch.
