# Postman API Automation – Ticket Management

This project demonstrates automated API testing using Postman for a ticket management system.  
It covers full CRUD operations with authentication and data-driven testing using CSV files.

---

## Project Overview

The collection performs the following workflow:

1. Authenticate and retrieve session token
2. Retrieve all tickets
3. Create a new ticket (data-driven via CSV)
4. Verify created ticket
5. Update the ticket
6. Verify updated ticket
7. Delete the ticket
8. Verify ticket deletion

Each iteration represents a complete ticket lifecycle.

---

## Technologies Used

- Postman
- JavaScript (Postman test scripts)
- CSV (data-driven testing)
- Environment & global variables
- REST API

---

## Authentication

The `Get token` request:

- Sends login credentials via form-data
- Extracts `token` from response
- Stores it as a environment variable: `session_token`
- Validates status code (200)

Authorization header used in protected endpoints: Token {{session_token}}

## Test Flow Details

### 1️. Get Token
- POST `/api/login`
- Extracts and stores session token

### 2️. Get All Tickets
- GET `/api/tickets`

### 3️. Create a Ticket
- POST `/api/tickets`
- Uses CSV variables:
  - title
  - description
  - due_date
  - submitter_email
  - queue
  - status
  - resolution
  - priority
- Saves created ticket ID as `id_ticket`
- Validates all response fields against CSV data

### 4️. Get Created Ticket
- GET `/api/tickets/{{id_ticket}}`
- Validates fields match original CSV input

### 5️. Update Ticket
- PUT `/api/tickets/{{id_ticket}}`
- Uses update fields from CSV:
  - new_title
  - new_description
  - new_due_date
  - new_queue
- Validates updated values

### 6️. Get Updated Ticket
- GET `/api/tickets/{{id_ticket}}`
- Confirms updated values are saved

### 7️. Delete Ticket
- DELETE `/api/tickets/{{id_ticket}}`
- Validates status code 204

### 8️. Verify Deletion
- GET `/api/tickets/{{id_ticket}}`
- Validates 404 response

---

## Data-Driven Testing

The collection uses CSV input with Postman Collection Runner.

Each CSV row represents a full test scenario:

- Initial ticket values
- Updated ticket values

Example columns:

---

## Test Validations

The collection validates:

- Status codes (200, 201, 204, 404)
- Field-level response validation
- Correct ID handling
- Date formatting validation
- Updated field consistency

---

## How to Run

1. Import the collection
2. Import the environment
3. Open Collection Runner
4. Upload CSV file
5. Run collection

---

## Key Testing Techniques Demonstrated

- Data-driven API testing
- Dynamic variable handling
- Token-based authentication
- CRUD validation
- End-to-end API scenario testing
- Response body validation with JavaScript

---

## Example Repository structure postman-api-automation
collection/
Contains the exported Postman collection (v2.1 format).

environment/
Contains Postman environment variables (base_url, login, session_token, etc.).

data/
Contains CSV file used for data-driven testing with Collection Runner.

README.md
