# Day 1 - Clean Architecture Notes

## One-line Meaning

Clean Architecture means keeping business logic separate from technical details.

Technical details:
- Database
- EF Core
- Redis
- RabbitMQ
- Email
- ASP.NET Controllers
- External APIs

## Memory Diagram

```text
HTTP Request
   |
   v
ProductsController      API Layer
   |
   v
ProductService          Application Layer
   |
   v
IProductRepository      Application Interface
   |
   v
ProductRepository       Infrastructure Layer
   |
   v
AppDbContext            Infrastructure Layer
   |
   v
Database
```

## What Goes in Each Layer

### API Layer

Receives HTTP requests and returns HTTP responses.

Contains:
- Controllers or endpoints
- Middleware
- Swagger/OpenAPI
- Authentication
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
- Business rules

Examples:
- Product
- Order
- Payment
- OrderStatus

Memory line: Domain is the heart of the system.

### Infrastructure Layer

Contains technical implementation.

Contains:
- Repository implementations
- EF Core later
- AppDbContext later
- SQL Server later
- Redis
- RabbitMQ
- Email service

Memory line: Infrastructure is replaceable.

## Important Terms

Product = Domain entity.

ProductService = Application service or use case.

IProductRepository = Interface or contract used by the Application layer.

ProductRepository = Actual repository implementation in Infrastructure.

AppDbContext = EF Core bridge between C# classes and database tables.

DTO = Data Transfer Object used to move data between layers or across HTTP.

Example DTO: CreateProductRequest.

## Dependency Rule

```text
API -> Application -> Domain

Infrastructure -> Application -> Domain

Domain depends on nobody.
```

## Final Recall

Controller calls Service.

Service calls Repository Interface.

Infrastructure implements Repository.

Repository uses DbContext.

DbContext talks to Database.
