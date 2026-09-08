# Order Management - Notification API

## Overview
This repository contains the Notification API for the Order Management System, built using MuleSoft. This API is responsible for triggering and routing outbound notifications (such as Email, SMS, or system alerts) to customers and downstream applications whenever there are updates to an order's lifecycle.

## Prerequisites
To build and run this application locally, you will need:
* **Anypoint Studio** 7.x
* **Mule Runtime** 4.x
* **Apache Maven** 3.x
* **Postman** (or any API testing tool)

## Setup and Installation
1. Clone this repository to your local machine:
   `git clone <repository-url>`
2. Open Anypoint Studio and import the project: 
   `File` -> `Import` -> `Anypoint Studio Project from File System`.
3. Configure the local environment variables in `src/main/resources/properties/local.yaml` (e.g., SMTP credentials, SMS gateway keys, or Base URIs).
4. Run the project locally by right-clicking the project in the Package Explorer and selecting `Run As` -> `Mule Application`.

## API Interface
### POST `/api/v1/notifications`
Dispatches a notification based on an order event.

**Sample Request Payload:**
```json
{
  "orderId": "ORD-987654321",
  "customerId": "CUST-001",
  "channel": "EMAIL",
  "eventType": "ORDER_SHIPPED",
  "recipient": "customer@example.com",
  "message": "Great news! Your order has been shipped and is on its way."
}
