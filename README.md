# Hercle REST API Collection

This Postman collection provides a comprehensive implementation of the Hercle REST API, covering:

- OTC price quoting and order execution  
- Deposits and withdrawals (crypto and fiat)  
- Request-for-Quote (RFQ) flows  
- Address whitelisting  
- Balance, trade, and transaction history

It is designed to support both manual testing and automated workflows, using Postman environments, built-in test scripts, and response validation logic.

---

## How to Import and Configure the Collection

### 1. Import the Collection
1. Open Postman.
2. Click **Import** → **File**, and select the `.postman_collection.json` file.

### 2. Import the Environment
1. Click **Import** again, and select the `.postman_environment.json` file (e.g., Hercle Sandbox or Hercle Prod).
2. Set the imported environment as active using the top-right environment selector.

#### Environment Variables

| Variable | Description                                                       |
|----------|-------------------------------------------------------------------|
| `host`   | Base URL for the API (e.g., `https://publicapi.hercle.financial`) |
| `token`  | Bearer token used for authentication (to be set manually)         |

---

## How to Set Up the Token

Authentication uses a Bearer token, applied via Postman’s Authorization helper:

1. Open **Environments** in Postman.
2. Select the active environment.
3. Set the `token` variable to your JWT token:
   ```
   token | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```
4. Save the environment.

All requests in the collection automatically apply this token using:
```
Authorization: Bearer {{token}}
```

---

## Response Validation and Dynamic Variable Chaining

This collection includes built-in features to streamline testing and request chaining.

### Response Schema Validation
Each request includes test scripts to validate the presence and structure of key fields. These help ensure API responses conform to expected formats, including object and array structures.

### Dynamic Variable Assignment
Several requests store response values into environment variables, allowing chained execution without manual input. For example:

| Variable    | Source Endpoint                   | Used In                         |
|-------------|------------------------------------|----------------------------------|
| `pair`      | First item from `/pairs`           | Quoting, RFQ, Order placement    |
| `priceId`   | `/price/{pair}/{size}`             | `/orders`                        |
| `rfqId`     | `/rfq`                             | `/rfq/accept`                    |
| `addressId` | `/addresses/whitelist`             | Address deletion, withdrawals    |

This enables automated flows like: fetch pairs → get price → place order → submit withdrawal, with no need for manual copy-pasting.

---

## Accessing Full Documentation

### In Postman
1. Click the collection name in the sidebar.
2. Click **View complete documentation** in the right-hand pane.
- This includes endpoint descriptions, sample requests/responses, and test behavior.

### Online
You can also access the full API reference here:  
**[https://documentation.hercle.financial/rest.html](https://documentation.hercle.financial/rest.html)**


