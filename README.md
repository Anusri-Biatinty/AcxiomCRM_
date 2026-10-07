# AcxiomCRM

AcxiomCRM is an ASP.NET Core MVC customer relationship management application. It provides role-based tools for managing customers, leads, sales opportunities, and follow-ups, along with dashboards, reports, audit logging, and a small authenticated REST API.

## Features

- Customer, lead, and opportunity management
- Follow-up scheduling and tracking
- Dashboard summaries and sales pipeline charts
- Customer, lead, opportunity, pipeline, follow-up, audit, and user activity reports
- ASP.NET Core Identity authentication and role-based authorization
- Audit logging for selected user actions
- Authenticated API endpoints for customers, leads, and opportunities

## Technology

- .NET 8 / ASP.NET Core MVC
- Entity Framework Core 8
- SQL Server
- ASP.NET Core Identity

## Prerequisites

- .NET 8 SDK
- A running SQL Server instance
- The `dotnet-ef` command-line tool for applying EF Core migrations

Install the EF Core CLI tool if it is not already installed:

```powershell
dotnet tool install --global dotnet-ef --version 8.0.0
```

## Configuration

The default connection string is in `AcxiomCRM/appsettings.json`:

```json
"DefaultConnection": "Server=localhost;Database=AcxiomCRM;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true"
```

Update `Server=localhost` to match your SQL Server instance if necessary. Keep credentials and production-specific settings out of source control; use user secrets or environment variables for sensitive configuration.

## Run Locally

From the repository root, run:

```powershell
cd .\AcxiomCRM
dotnet restore
dotnet ef database update
dotnet run
```

Open the local URL printed by `dotnet run`. The default route opens the login page. The application creates its Identity roles and demo users during startup after the database has been migrated.

## Development Accounts

The startup seed creates these accounts when they do not already exist:

| Role | Email | Password |
| --- | --- | --- |
| Admin | `admin@acxiomcrm.com` | `Admin@123456` |
| Manager | `manager@acxiomcrm.com` | `Manager@123456` |
| SalesExecutive | `sales@acxiomcrm.com` | `Sales@123456` |

These are development/demo credentials only. Change or remove them before deploying the application.

## API

The authenticated API routes are:

- `/api/customers`
- `/api/leads`
- `/api/opportunities`

The API uses ASP.NET Core authorization; sign in through the application to establish an authenticated session.

## Database Migrations

The initial schema migration is included in `AcxiomCRM/Migrations`. After changing the data model, create and apply a migration from the project directory:

```powershell
dotnet ef migrations add <MigrationName>
dotnet ef database update
```
