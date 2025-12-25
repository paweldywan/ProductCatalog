# ProductCatalog

A full-stack product catalog application built with ASP.NET Core (C#) for the backend and React (TypeScript, Vite) for the frontend. The application provides a modern, responsive interface for browsing products, viewing detailed information, and reading reviews.

**Live Application:** https://productcatalog.paweldywan.com/

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Database](#database)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

ProductCatalog is a full-stack product catalog application showcasing modern development practices with .NET 8 and React. The application implements a clean, layered architecture separating concerns across Data Access, Business Logic, and Presentation layers. It features a RESTful API backend with Entity Framework Core for data persistence and a responsive React frontend built with TypeScript and Vite.

## Key Features

- **Product Catalog:** Browse and search through a comprehensive product database
- **Detailed Product Views:** View complete product information including images, specifications, and pricing
- **Product Reviews:** Read customer reviews and ratings for each product
- **Responsive Design:** Mobile-friendly interface using Bootstrap and Reactstrap
- **RESTful API:** Well-structured API endpoints for product data access
- **Swagger Documentation:** Interactive API documentation for developers
- **Database Seeding:** Automatic data population for quick setup and testing
- **Modular Architecture:** Clean separation of concerns using DAL, BLL, and Server layers
- **Type Safety:** TypeScript implementation for frontend reliability

## Architecture

The application follows a three-tier architecture pattern:

```
ProductCatalog Solution
|
+-- ProductCatalog.DAL (Data Access Layer)
|   +-- Entities (Product, Review, Tag, Image, Dimensions, Meta)
|   +-- ProductCatalogContext (EF Core DbContext)
|   +-- Migrations (Database schema versioning)
|   +-- Models (DTOs and data models)
|   +-- ProductCatalogSeeder (Database initialization)
|
+-- ProductCatalog.BLL (Business Logic Layer)
|   +-- Interfaces (IProductService)
|   +-- Services (ProductService)
|
+-- ProductCatalog.Server (Presentation Layer - API)
|   +-- Controllers (ProductController)
|   +-- Program.cs (Application startup and configuration)
|
+-- productcatalog.client (Frontend SPA)
    +-- src
        +-- components (Reusable UI components)
        +-- Views (Page components)
        +-- hooks (Custom React hooks)
        +-- assets (Static resources)
```

### Layer Responsibilities

- **DAL (Data Access Layer):** Handles all database operations, entity definitions, and data persistence using Entity Framework Core with PostgreSQL
- **BLL (Business Logic Layer):** Contains business rules, validations, and service implementations
- **Server (API Layer):** Exposes RESTful endpoints, handles HTTP requests, and manages application configuration
- **Client (Presentation Layer):** React-based single-page application providing the user interface

## Technology Stack

### Backend

- **.NET 8.0:** Modern, cross-platform framework for building web applications
- **ASP.NET Core:** Web API framework for building RESTful services
- **Entity Framework Core 8.0:** Object-relational mapper (ORM) for database operations
- **PostgreSQL:** Open-source relational database (via Npgsql provider)
- **Swagger/OpenAPI:** API documentation and testing interface
- **Dependency Injection:** Built-in DI container for loose coupling

### Frontend

- **React 18:** Modern JavaScript library for building user interfaces
- **TypeScript 5:** Typed superset of JavaScript for enhanced development experience
- **Vite 5:** Fast build tool and development server
- **React Router 6:** Client-side routing for single-page application navigation
- **Bootstrap 5 & Reactstrap 9:** Responsive UI component library
- **FontAwesome:** Icon library for visual elements
- **ESLint:** Code linting and quality assurance

### Development Tools

- **Visual Studio / Visual Studio Code:** Recommended IDEs
- **npm:** Package manager for frontend dependencies
- **Entity Framework Core Tools:** Database migration management

## Getting Started

### Prerequisites

Before running the application, ensure you have the following installed:

- [.NET 8 SDK](https://dotnet.microsoft.com/download) or later
- [Node.js](https://nodejs.org/) (v18 or later) and npm
- [PostgreSQL](https://www.postgresql.org/download/) (v12 or later)
- Git for cloning the repository

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/paweldywan/ProductCatalog.git
   cd ProductCatalog
   ```

2. **Configure the database connection:**
   
   Update the connection string in `ProductCatalog.Server/appsettings.Development.json`:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Host=localhost;Database=ProductCatalog;Username=your_username;Password=your_password"
     }
   }
   ```

3. **Restore backend dependencies:**
   ```bash
   dotnet restore
   ```

4. **Build the solution:**
   ```bash
   dotnet build
   ```

5. **Apply database migrations:**
   ```bash
   cd ProductCatalog.DAL
   dotnet ef database update --startup-project ../ProductCatalog.Server
   cd ..
   ```

6. **Install frontend dependencies:**
   ```bash
   cd productcatalog.client
   npm install
   cd ..
   ```

### Running the Application

#### Option 1: Run Backend and Frontend Separately

**Start the backend API:**
```bash
cd ProductCatalog.Server
dotnet run
```
The API will be available at `https://localhost:5001` (or the port specified in launchSettings.json)

**Start the frontend development server (in a separate terminal):**
```bash
cd productcatalog.client
npm run dev
```
The frontend will be available at `https://localhost:5173`

#### Option 2: Run as Integrated Application

Run the server project, which will automatically start the frontend via SPA proxy:
```bash
cd ProductCatalog.Server
dotnet run
```

Access the application at the backend URL. The frontend will be served through the ASP.NET Core SPA proxy.

### First Run

On the first run, the application will automatically seed the database with sample product data using the `ProductCatalogSeeder`. This provides a populated catalog for immediate testing and demonstration.

## API Documentation

The API provides RESTful endpoints for product management. When running in development mode, Swagger UI is available for interactive API exploration.

### Access Swagger UI

Navigate to: `https://localhost:5001/swagger` (adjust port as needed)

### Available Endpoints

#### GET /api/product
Retrieves all products in the catalog.

**Response:** `200 OK` with array of product objects

**Example Response:**
```json
[
  {
    "id": 1,
    "title": "Product Name",
    "description": "Product description",
    "category": "Category Name",
    "price": 99.99,
    "discountPercentage": 10.5,
    "rating": 4.5,
    "stock": 50,
    "tags": ["tag1", "tag2"],
    "images": [...],
    "reviews": [...]
  }
]
```

#### GET /api/product/{id}
Retrieves a specific product by ID.

**Parameters:**
- `id` (path parameter): Product identifier

**Response:** 
- `200 OK` with product object if found
- `404 Not Found` if product doesn't exist

**Example Request:**
```
GET /api/product/1
```

## Project Structure

```
ProductCatalog/
|
+-- ProductCatalog.DAL/
|   +-- Entities/
|   |   +-- Product.cs
|   |   +-- Review.cs
|   |   +-- Tag.cs
|   |   +-- Image.cs
|   |   +-- Dimensions.cs
|   |   +-- Meta.cs
|   +-- Migrations/
|   +-- Models/
|   |   +-- ProductsModel.cs
|   +-- ProductCatalogContext.cs
|   +-- ProductCatalogSeeder.cs
|   +-- ProductCatalog.DAL.csproj
|
+-- ProductCatalog.BLL/
|   +-- Interfaces/
|   |   +-- IProductService.cs
|   +-- Services/
|   |   +-- ProductService.cs
|   +-- ProductCatalog.BLL.csproj
|
+-- ProductCatalog.Server/
|   +-- Controllers/
|   |   +-- ProductController.cs
|   +-- Program.cs
|   +-- appsettings.json
|   +-- appsettings.Development.json
|   +-- ProductCatalog.Server.csproj
|
+-- productcatalog.client/
|   +-- src/
|   |   +-- components/
|   |   +-- Views/
|   |   +-- hooks/
|   |   +-- assets/
|   |   +-- App.tsx
|   |   +-- main.tsx
|   +-- public/
|   +-- package.json
|   +-- tsconfig.json
|   +-- vite.config.ts
|
+-- README.md
```

## Database

The application uses PostgreSQL as its database system with Entity Framework Core for data access.

### Entity Relationships

- **Product:** Main entity containing product information
- **Review:** Customer reviews linked to products (one-to-many)
- **Tag:** Product categorization tags (many-to-many)
- **Image:** Product images (one-to-many)
- **Dimensions:** Physical product dimensions (one-to-one)
- **Meta:** Additional metadata (one-to-one)

### Migrations

Database schema is managed through EF Core migrations. To create a new migration:

```bash
cd ProductCatalog.DAL
dotnet ef migrations add MigrationName --startup-project ../ProductCatalog.Server
dotnet ef database update --startup-project ../ProductCatalog.Server
```

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please ensure your code follows the existing style and includes appropriate tests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

**Pawel Dywan**
- GitHub: [@paweldywan](https://github.com/paweldywan)
- Website: [https://paweldywan.com/](https://paweldywan.com/)

## Acknowledgments

- Built with [ASP.NET Core](https://dotnet.microsoft.com/apps/aspnet)
- Frontend powered by [React](https://reactjs.org/) and [Vite](https://vitejs.dev/)
- UI components from [Bootstrap](https://getbootstrap.com/) and [Reactstrap](https://reactstrap.github.io/)
- Icons by [FontAwesome](https://fontawesome.com/)
- Database management with [Entity Framework Core](https://docs.microsoft.com/ef/core/)
- API documentation via [Swagger](https://swagger.io/)

---

For questions, issues, or suggestions, please open an issue on GitHub or contact the author through the website.
