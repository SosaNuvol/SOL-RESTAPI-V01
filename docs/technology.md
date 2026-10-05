# Proposed languages and stack

Status: recommendation for review before implementation. Documentation checked October 5, 2026.

| Area | Recommendation | Reason |
| --- | --- | --- |
| Backend and background jobs | C#, ASP.NET Core on .NET 10 LTS | Strong types, transactional business logic, mature SQL Server tooling, and one backend for all clients |
| ERP web application | TypeScript, React | Matches the requested frontend and adds compile-time checks for complex forms and API contracts |
| Installer mobile application | TypeScript, React Native with Expo | Native camera/device access and shared frontend language; local SQLite for assigned-job records and queued changes |
| Sales representative mobile application | TypeScript, React Native with Expo | Separate sales workflow while sharing authentication, API client, and reusable mobile components |
| Central database | Microsoft SQL Server; T-SQL | Required database; relational constraints and transactions fit attribution, equipment, payments, and history |
| Data access | Entity Framework Core SQL Server provider | Migrations and transactional relational access; use targeted SQL for complex reporting when justified |
| Photos and documents | Private object storage, such as Azure Blob Storage | Store binary files separately; keep metadata, access control references, and relationships in SQL Server |
| API contracts | REST with OpenAPI; generate TypeScript clients | Share checked contracts across web and mobile without exposing database tables directly |

My recommendation is C# + TypeScript + T-SQL. C# owns business rules; TypeScript owns the web and mobile experiences. Do not connect mobile or browser clients directly to SQL Server.

Microsoft lists .NET 10 support through November 15, 2028 in its lifecycle table, and provides an official EF Core SQL Server provider. Confirm current patches and dependency versions when implementation starts.

Alternative: a TypeScript backend using NestJS can reduce the number of languages if the development team primarily knows JavaScript. It is viable, but I prefer C# for this SQL Server centered ERP. Python can be useful later for analytics; introducing a second backend language is unnecessary for the initial scope. Flutter/Dart would introduce another language for mobile without a demonstrated need.

Start with a modular monolith: one API, one SQL database, and a background worker built from the same codebase. Split services only when operations or scale justify it. SQL Server may be hosted on an existing server or Azure SQL after infrastructure review; Azure services are suggestions, not commitments.

Expo SQLite provides device persistence, not a complete synchronization system. Offline authorization, attachment transfers, conflict handling, and server reconciliation must be explicitly built and tested.

Sources:

- [Microsoft .NET lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/microsoft-net-and-net-core)
- [EF Core SQL Server provider](https://learn.microsoft.com/en-us/ef/core/providers/sql-server/)
- [Expo local-first architecture](https://docs.expo.dev/guides/local-first/)
- [Expo SQLite](https://docs.expo.dev/versions/latest/sdk/sqlite/)
