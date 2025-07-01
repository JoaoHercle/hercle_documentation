# Hercle REST API Collection
This Postman collection provides complete access to the Hercle REST API, including:
 - OTC price quotes and order execution
- Deposits and withdrawals (crypto and fiat)
- Request-for-Quote (RFQ) flow
- Whitelisting addresses
- Balance, trade, and transaction history

It’s designed to simplify both manual testing and automated flows, using Postman environments, dynamic test scripts, and response validation logic.

---
### How to Import and Configure the Collection
1. Import the Collection
 1.1. Open Postman.
 1.2. Click Import → File → Select the .postman_collection.json.
 2. Import the Environment
 2.1. Click Import → Select the .postman_environment.json (e.g., Hercle Sandbox or Hercle Prod).
 2.2. Select the environment from the top-right dropdown.

The imported environment includes:

| Variable | Description                                                   |
| -------- | ------------------------------------------------------------- |
| `host`   | API base URL (e.g., `https://publicapi.dev.hercle.financial`) |
| `token`  | Bearer token used for authorization (to be set manually)      |

---
### How to Set Up the Token
Authentication is handled through Bearer Token, set via Postman’s Authorization helper.
1. Open Environments.
2. Select your active environment.
3. Paste your JWT token into the token variable
4. Save the environment.

All requests in the collection will now use this token automatically via Authorization: Bearer {{token}}.

---
### Response Validation and Dynamic Variable Chaining
For ease of use and testing, the collection includes:

##### High-Level Response Schema Tests
Every endpoint has built-in Postman test scripts to validate:
- Expected keys/fields in the response
 - Array/object structures

This ensures each response matches the correct schema.

##### Dynamic Post-Test Variables
Certain endpoints extract values from responses and save them as variables for use in subsequent requests:

| Variable    | Set From                             | Used In                      |
| ----------- | ------------------------------------ | ---------------------------- |
| `pair`      | First item in `/pairs` response      | Quoting, RFQs, Orders        |
| `priceId`   | From `/price/{pair}/{size}`          | `/orders`                    |
| `rfqId`     | From `/rfq`                          | `/rfq/accept`                |
| `addressId` | From `/addresses/whitelist` response | For deletion and withdrawals |


This enables step-by-step testing (e.g., get price → place order → verify) without manually copying IDs.

---
### Accessing Full Documentation
You can explore the API in two ways:

##### In Postman
1. Click the collection name in the sidebar.
2. Then click "View complete documentation" on the right-hand pane.
3. This provides details for each endpoint: descriptions, sample requests/responses, test info, etc.

##### Online
Access the official REST API reference:
🔗 https://documentation.hercle.financial/rest.html

