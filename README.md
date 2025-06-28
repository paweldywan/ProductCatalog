# ProductCatalog

A full-stack product catalog application built with ASP.NET Core (C#) for the backend and React (TypeScript, Vite) for the frontend.

## Features
- Product listing, details, and reviews
- Modern, responsive UI
- Modular architecture (DAL, BLL, Server, Client)
- Entity Framework Core for data access
- RESTful API

## Project Structure
- `ProductCatalog.DAL/` - Data Access Layer (EF Core, entities, migrations)
- `ProductCatalog.BLL/` - Business Logic Layer (services, interfaces)
- `ProductCatalog.Server/` - ASP.NET Core Web API (controllers, configuration)
- `productcatalog.client/` - React frontend (Vite, TypeScript, components)

## Getting Started

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [Node.js & npm](https://nodejs.org/)

### Backend Setup
1. Navigate to the solution root:
   ```pwsh
   cd ProductCatalog
   ```
2. Restore and build the solution:
   ```pwsh
   dotnet restore
   dotnet build
   ```
3. Apply database migrations:
   ```pwsh
   cd ProductCatalog.DAL
   dotnet ef database update
   cd ..
   ```
4. Run the server:
   ```pwsh
   cd ProductCatalog.Server
   dotnet run
   ```

### Frontend Setup
1. Navigate to the client folder:
   ```pwsh
   cd productcatalog.client
   ```
2. Install dependencies:
   ```pwsh
   npm install
   ```
3. Start the development server:
   ```pwsh
   npm run dev
   ```

## Usage
- The backend API will be available at `https://localhost:5001` (or as configured).
- The frontend will be available at `http://localhost:5173` by default.

## Development
- Backend: C#, ASP.NET Core, Entity Framework Core
- Frontend: React, TypeScript, Vite

## License
MIT License

---

Live demo: https://productcatalog.paweldywan.com/
