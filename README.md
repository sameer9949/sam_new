# Clean Architecture .NET Learning

This repository is for learning Clean Architecture and .NET system design step by step.

## What Clean Architecture Means

Clean Architecture means separating business logic from technical details.

Business rules should not directly depend on databases, EF Core, Redis, RabbitMQ, email, ASP.NET Controllers, or external APIs. Those details can change, but the core business rules should stay stable.

## The 4 Layers

```text
src/
├── CleanArchitectureDemo.Api
├── CleanArchitectureDemo.Application
├── CleanArchitectureDemo.Domain
└── CleanArchitectureDemo.Infrastructure
```

### API Layer

Receives HTTP requests and returns HTTP responses.

Contains:
- Controllers or endpoints
- Middleware
- Swagger/OpenAPI
- Authentication setup
- HTTP status codes

Memory line: Controller should be thin.

### Application Layer

Contains use cases and business actions.

Contains:
- Services
- Interfaces
- DTOs
- Validation
- Business flow

Memory line: Application decides what should happen.

### Domain Layer

Contains pure business objects and business rules.

Contains:
- Entities
- Enums
- Value objects
- Core business rules

Memory line: Domain is the heart of the system.

### Infrastructure Layer

Contains technical implementation details.

Contains:
- Repository implementations
- EF Core setup later
- AppDbContext later
- SQL Server later
- Redis, RabbitMQ, email, and external services later

Memory line: Infrastructure is replaceable.

## Request Flow

```text
Controller
   ↓
Service
   ↓
Repository Interface
   ↓
Repository Implementation
   ↓
DbContext
   ↓
Database
```

Example:

```text
ProductsController
   ↓
ProductService
   ↓
IProductRepository
   ↓
ProductRepository
   ↓
AppDbContext
   ↓
Database
```

## Dependency Rule

Dependencies should point inward toward the business rules.

```text
Domain depends on nobody.
Application depends on Domain.
Infrastructure depends on Application and Domain.
API depends on Application.
```

Current project references:

```text
CleanArchitectureDemo.Api → CleanArchitectureDemo.Application
CleanArchitectureDemo.Application → CleanArchitectureDemo.Domain
CleanArchitectureDemo.Infrastructure → CleanArchitectureDemo.Application
CleanArchitectureDemo.Infrastructure → CleanArchitectureDemo.Domain
CleanArchitectureDemo.Domain → nobody
```

## Day 1 Goal

Understand the basic flow:

```text
Controller → Service → Repository Interface → Repository Implementation → DbContext → Database
```

For now, this repository does not include EF Core or a database. It only contains the starter solution structure and learning notes.
