# Overview 
This solution implements an integration service between Infosilem Academic (course scheduling system) and Thesis (Student Information System).

The two integration points are:
- Infosilem Academic Suite API
- Thesis Unit4 Student Management API

## How does it work?
![Thesis Infosilem Integration Macro Architecture](docs/media/macro-architecture.png)

From a conceptual level, the web application manages the integration process. Users can define the Infosilem databases to use as sources for the integration, create schedules for the automatic execution of the integration process, and manually execute an integration. Users can also export professors and courses from Thesis as CSV files and import them in Infosilem. There is also a dashboard for displaying the results of the most recent integration executions. The web application uses Azure AD authentication.

The integration process is hosted in Azure Functions and uses orchestrator functions to implement a fan-out/fan-in pattern. This pattern allows for processing multiple courses in parallel and aggregating the results. The Azure Functions also host a REST API to allow operations personnel to manage the integration process programmatically.

Once the integration process completes, it broadcasts a message with the results using Azure SignalR. If the web application is active, it receives the message and displays its contents in a toast window. The process also sends a report with the results to a configurable email account using the Mailgun email service.

The Azure SQL server hosts a database to keep track of the Infosilem databases, execution schedules, and historical process executions.

## Components

* [Azure Functions](docs/functions.md)
* [Web Application](docs/webapp.md)
* [SQL Database](docs/database.md)

## Additional information

* [Mapping details](docs/mapping.md)
* [Technical information](docs/technical.md)
