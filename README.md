# Automated HR Support API

A backend RESTful Web API built with **C# .NET** and **SQL Server** to manage and automate internal Human Resources support tickets. 

This project was built to demonstrate foundational full-stack backend skills, focusing on relational database management, automated business logic, and API architecture.

## Features

* **Automated Ticket Categorization:** Implemented a C# algorithm that scans incoming ticket descriptions. It automatically assigns the ticket to the correct department (e.g., routing "payslip" issues to Payroll, and "holiday" requests to Time Off), eliminating the need for manual HR triage.
* **RESTful Architecture:** Standardized API endpoints to handle incoming requests securely and efficiently.
* **Database Integration:** Utilizes Entity Framework (EF) Core as an ORM to securely map C# objects directly to a local SQL Server database.

## Tech Stack

* **Language:** C#
* **Framework:** ASP.NET Core Web API
* **Database:** Microsoft SQL Server (T-SQL)
* **ORM:** Entity Framework Core
* **Tools:** Visual Studio, Git, Swagger UI

## API Endpoints

The API is fully documented using Swagger. Once running locally, navigate to `/swagger` to test the endpoints.

| HTTP Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/Tickets` | Retrieves a list of all current HR support tickets from the SQL database. |
| `POST` | `/api/Tickets` | Submits a new ticket. Triggers the automated categorization logic and saves to the database. |

## The Logic Behind the Automation

When a `POST` request is sent with a new ticket, the API does not just save the raw data. It intercepts the `IssueDescription` and applies basic business logic:
```csharp
// Example of the categorization logic intercepting the request
string desc = newTicket.IssueDescription.ToLower();

if (desc.Contains("payslip") || desc.Contains("salary"))
    newTicket.Category = "Payroll";
else if (desc.Contains("holiday") || desc.Contains("leave"))
    newTicket.Category = "Time Off";
else
    newTicket.Category = "General IT";
