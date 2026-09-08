# MuleSoft Order Management Integration

A production-style Order Management Integration built using MuleSoft Anypoint Platform, APIkit, DataWeave, MySQL, and MUnit.

## 📌 Project Overview

This project implements an end-to-end Order Management API using MuleSoft as the integration layer.

The Main Order Management API receives an order request, validates the input, checks product availability through an external Product API, calculates the order amount and applicable discount, creates the order through an Order Management API, and sends a customer notification through a Notification API.

## 🏗️ Architecture

```text
                    Client
                      |
                      v
          +------------------------+
          | Main Order Management  |
          |       API :8080        |
          +------------------------+
                      |
                 Validate Request
                      |
                      v
          +------------------------+
          |      Product API       |
          |        :8081           |
          +------------------------+
                      |
                  MySQL DB
                      |
                Price + Stock
                      |
                      v
              Calculate Amount
              Apply Discount
                      |
                      v
          +------------------------+
          |   Order Management     |
          |       API :8082        |
          +------------------------+
                      |
                  MySQL DB
                      |
                  Order ID
                      |
                      v
          +------------------------+
          |   Notification API     |
          |        :8083           |
          +------------------------+
                      |
                      v
              Final Response
````

## 🔄 Order Processing Flow

1. Client sends an order request.
2. Main API validates the request.
3. Product API is called for each product.
4. Product price and stock are retrieved.
5. Requested quantity is compared with available stock.
6. Order subtotal is calculated.
7. A 10% discount is applied when the subtotal is greater than ₹10,000.
8. Order Management API creates the order.
9. Notification API sends the customer notification.
10. Main API returns the final order response.

## 💰 Business Rules

* Order must contain at least one item.
* Product ID is mandatory.
* Quantity must be greater than 0.
* Product must exist.
* Requested quantity must not exceed available stock.
* Subtotal is calculated using product price × quantity.
* A 10% discount is applied when:

```text
Subtotal > ₹10,000
```

* Final amount:

```text
Total Amount = Subtotal - Discount
```

## 🔌 APIs

### Main Order Management API

```text
POST /api/orders
```

Example request:

```json
{
  "customerId": "CUST001",
  "customerName": "Dilshan",
  "email": "dilshan@example.com",
  "items": [
    {
      "productId": "P001",
      "quantity": 2
    }
  ]
}
```

### Product API

```text
GET /products/{productId}
```

Returns product information including:

* Product ID
* Product name
* Price
* Available stock

### Order Management API

```text
POST /orders
```

Creates and stores the confirmed order.

### Notification API

```text
POST /notifications
```

Sends the customer order confirmation notification.

## ⚠️ Error Handling

The application handles the following scenarios:

| Status | Scenario                     |
| ------ | ---------------------------- |
| 400    | Invalid order request        |
| 404    | Product not found            |
| 409    | Insufficient stock           |
| 502    | External service unavailable |
| 500    | Internal server error        |

All errors follow a common structure:

```json
{
  "status": 400,
  "message": "Invalid order request"
}
```

## 🗄️ Database

MySQL is used for persistent data storage.

### Products

Stores:

* Product ID
* Product name
* Price
* Stock

### Orders

Stores:

* Order ID
* Customer ID
* Subtotal
* Discount
* Total amount
* Order status

### Order Items

Stores:

* Order item ID
* Order ID
* Product ID
* Quantity
* Unit price
* Total price

## 🛠️ Technologies

* MuleSoft Anypoint Platform
* Anypoint Studio
* APIkit
* RAML 1.0
* DataWeave
* HTTP Connector
* Database Connector
* MySQL
* Postman
* MUnit
* GitHub

## 🧪 Testing

MUnit tests are used to validate:

* Successful order processing
* Invalid order requests
* Product not found
* Insufficient stock
* External service failures
* Unexpected errors
* Discount calculation
* Order creation
* Notification handling

## 🔐 Security

API security policies are planned through Anypoint API Manager.

The project will use appropriate API policies for protecting and controlling access to the Main Order Management API.

## 📁 Repository Structure

```text
order-management-mulesoft/
│
├── main-order-api/
├── product-api/
├── order-system-api/
├── notification-api/
│
├── raml/
├── munit/
├── docs/
│
├── .gitignore
└── README.md
```

## 🚀 How to Run

1. Clone the repository.
2. Import the MuleSoft projects into Anypoint Studio.
3. Configure MySQL database connection.
4. Start the Product API.
5. Start the Order Management API.
6. Start the Notification API.
7. Start the Main Order Management API.
8. Use Postman to send requests to:

```text
POST http://localhost:8080/api/orders
```

## 👥 Team

This project is developed as a collaborative MuleSoft integration project.

Team members and individual responsibilities will be documented here.

## 📄 Documentation

Additional project documentation will include:

* API specification
* System architecture
* Database design
* Integration flow
* Error handling
* MUnit test cases
* API security policies

