# CropTrader – Components and Interfaces (Week 3)

## Components

| # | Component | Runs on | Responsibility |
|---|-----------|---------|----------------|
| 1 | React frontend (TypeScript) | User's browser | Pages for register, login, listings, search, ordering and order management; sends JSON requests to the API. |
| 2 | ASP.NET Core Web API (controllers) | Application server | Receives HTTP requests, checks the request format, calls the right service, returns JSON and status codes. |
| 3 | Authentication and authorisation module | Application server | Registers users, hashes passwords, issues a JWT with the user ID and role, checks the role on protected endpoints. |
| 4 | Business services + EF Core (ListingService, OrderService) | Application server | Validation and business rules; creates orders and reduces stock in one transaction. |
| 5 | Microsoft SQL Server (LocalDB in development) | Database server | Stores Users, Listings and Orders; only the API can reach it. |

Trust boundary: everything that comes from the browser is untrusted and is validated again on the server.

## Planned REST API endpoints

All requests and responses use JSON over HTTPS. Protected endpoints need the header `Authorization: Bearer <JWT>`.
Status: **planned**, implemented in Weeks 4–5.

| Method | Endpoint | Access | Purpose | Requirement |
|--------|----------|--------|---------|-------------|
| POST | `/api/auth/register` | Public | Create a farmer or consumer account | FR-01 |
| POST | `/api/auth/login` | Public | Check email and password, return a JWT | FR-01 |
| GET | `/api/listings?search=&category=&location=` | Public | List active listings with search and filters | FR-03, NFR-01 |
| GET | `/api/listings/{id}` | Public | Show one listing | FR-03 |
| POST | `/api/listings` | Farmer | Create a listing | FR-02, NFR-03 |
| POST | `/api/orders` | Consumer | Place an order (cash on delivery) and reduce stock | FR-04, FR-05, NFR-02 |
| GET | `/api/orders/mine` | Consumer | See own orders and their status | US-03 |
| GET | `/api/orders/received` | Farmer | See orders placed on own listings | FR-06 |
| PATCH | `/api/orders/{id}/status` | Farmer | Change status to Pending, Preparing or Delivered | FR-06, NFR-03 |

## Example: POST /api/orders

Request
```json
{ "listingId": 12, "quantity": 10, "deliveryAddress": "Bakırköy, Istanbul" }
```

Response `201 Created`
```json
{
  "orderId": 57, "listingId": 12, "quantity": 10,
  "unitPriceAtOrder": 25.00, "totalPrice": 250.00,
  "paymentMethod": "CashOnDelivery", "status": "Pending", "remainingQuantity": 40
}
```

Error `400 Bad Request` (quantity larger than stock, NFR-02)
```json
{ "title": "Invalid quantity", "status": 400, "detail": "Requested 60 kg but only 50 kg is available." }
```

Other error codes: `401` missing or expired token, `403` wrong role, `404` listing not found, `409` stock changed by another order at the same time.

## Data model

See [er-diagram.png](er-diagram.png). Entities: **User** (Id, FullName, Email, PasswordHash, Role, PhoneNumber, CreatedAt), **Listing** (Id, FarmerId, ProductName, Category, UnitPrice, Unit, AvailableQuantity, Location, IsActive, CreatedAt, RowVersion), **Order** (Id, ListingId, ConsumerId, Quantity, UnitPriceAtOrder, TotalPrice, PaymentMethod, Status, DeliveryAddress, CreatedAt).
