# CropTrader – Design Decisions (Week 3)

## Requirements that drive the design

| ID | Design response |
|----|-----------------|
| FR-02 | Listing form → `POST /api/listings` → ListingService → Listings table linked to the farmer. |
| FR-04 | `POST /api/orders` → OrderService creates an order (Pending, CashOnDelivery); no payment service needed. |
| FR-05 | Order insert and stock update in one database transaction, with a rowversion concurrency check on Listing. |
| NFR-02 | Validation in the React form and again in the OrderService; invalid orders return 400 and change nothing. |
| NFR-03 | JWT with a role claim; listing and order-status endpoints require the Farmer role (403 otherwise). |

## ADR-01 – Frontend/backend approach
- **Issue:** How should the user interface and the server logic be built and connected?
- **Selected:** React + TypeScript single-page application calling a separate ASP.NET Core Web API (JSON).
- **Alternative:** Server-rendered ASP.NET Core MVC or Razor Pages.
- **Reason / trade-off:** The app needs interactive search, ordering and order-status pages and an API that a future mobile app could reuse. Cost: two projects, CORS and token handling, more security care. Search-engine visibility is not a goal of the prototype.
- **References:**
  - https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/choose-between-traditional-web-and-single-page-apps
  - https://learn.microsoft.com/en-us/aspnet/core/tutorials/choose-web-ui

## ADR-02 – Database
- **Issue:** Which database should store users, listings and orders?
- **Selected:** Microsoft SQL Server (Express LocalDB in development) with the EF Core SQL Server provider.
- **Alternative:** PostgreSQL with Npgsql; a document database (MongoDB) was rejected.
- **Reason / trade-off:** The data is relational and the order flow needs transactions. SQL Server has an official EF Core provider and LocalDB needs almost no setup on Windows with Visual Studio. EF Core optimistic concurrency (rowversion) protects the stock. Trade-off: less portable outside Windows; Week 7 can use a SQL Server Docker image.
- **References:**
  - https://learn.microsoft.com/en-us/ef/core/providers/sql-server/
  - https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/sql-server-express-localdb
  - https://learn.microsoft.com/en-us/ef/core/saving/concurrency

## Risks

| Risk | Mitigation / verification |
|------|---------------------------|
| R1 – Wrong stock when two orders arrive at the same time | Transaction + rowversion. Test: two parallel orders for the last 10 kg → one 201, one 409, stock ends at 0. |
| R2 – Frontend and API do not work together (CORS, URLs, tokens) | Build the thinnest end-to-end path first in Week 4; configure CORS and Swagger at the start. |

## Week 4 prototype goal
A farmer who has registered and logged in creates a listing in the React form; it passes through `POST /api/listings`, the auth module, ListingsController, ListingService and EF Core into SQL Server LocalDB, and a consumer's search for "tomato" (`GET /api/listings?search=tomato`) shows it. Evidence: screenshots, Swagger output (including 401 without a token) and the new database row.
