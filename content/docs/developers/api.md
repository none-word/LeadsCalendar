+++
title = 'Api'
+++

# API Description for Integration

LeadsCalendar integrates with three main APIs: Google Calendar API, PayPal REST API, and Binance Pay API. Below is a description of each API and its functionalities within the LeadsCalendar application:

## 1. Google Calendar API:

- **Description:**
  - The Google Calendar API allows LeadsCalendar to interact with users' Google Calendar accounts, enabling them to create, update, and delete events programmatically.
- **Functionalities:**
  - **Event Management:** Enables the creation, retrieval, updating, and deletion of events on users' Google Calendar.
  - **Authentication:** Utilizes OAuth 2.0 for user authentication and authorization to access their Google Calendar data securely.
  - **Real-Time Updates:** Provides real-time updates and notifications for changes made to events, ensuring synchronization between LeadsCalendar and Google Calendar.
- **Endpoints:**
  - `GET /events`: Retrieve events from the user's calendar.
  - `POST /events`: Create a new event on the user's calendar.
  - `PUT /events/{eventId}`: Update an existing event.
  - `DELETE /events/{eventId}`: Delete an event from the calendar.
- **Authentication:**
  - OAuth 2.0 is used for user authentication and authorization.
- **Sample Request (Create Event):**
  ```http
  POST /events HTTP/1.1
  Host: www.googleapis.com/calendar/v3
  Authorization: Bearer {access_token}
  Content-Type: application/json
  
  {
    "summary": "Sample Event",
    "start": {
      "dateTime": "2024-04-11T10:00:00",
      "timeZone": "America/Los_Angeles"
    },
    "end": {
      "dateTime": "2024-04-11T12:00:00",
      "timeZone": "America/Los_Angeles"
    }
  }
  ```

## 2. PayPal REST API:

- **Description:**
  - The PayPal REST API enables LeadsCalendar to process payments securely using PayPal's payment gateway.
- **Functionalities:**
  - **Payment Processing:** Allows users to make payments using PayPal's payment methods (e.g., PayPal balance, credit/debit cards).
  - **Order Management:** Manages orders, captures payments, and retrieves transaction details.
  - **Webhooks:** Provides webhooks for receiving payment notifications and order updates.
- **Endpoints:**
  - `POST /v2/checkout/orders`: Create a new payment order.
  - `GET /v2/checkout/orders/{orderId}`: Retrieve details of a specific order.
  - `POST /v2/checkout/orders/{orderId}/capture`: Capture payment for an order.
  - Webhooks endpoints for receiving payment notifications.
- **Authentication:**
  - Requires API credentials (Client ID and Secret) for authentication.
- **Sample Request (Create Order):**
  ```http
  POST /v2/checkout/orders HTTP/1.1
  Host: api.paypal.com
  Authorization: Basic {base64_encoded(client_id:client_secret)}
  Content-Type: application/json
  
  {
    "intent": "CAPTURE",
    "purchase_units": [{
      "amount": {
        "currency_code": "USD",
        "value": "1.00"
      }
    }]
  }
  ```

## 3. Binance Pay API:

- **Description:**
  - The Binance Pay API facilitates cryptocurrency payments within LeadsCalendar using Binance's payment gateway.
- **Functionalities:**
  - **Cryptocurrency Payments:** Allows users to make payments using supported cryptocurrencies (e.g., BTC, ETH, USDT).
  - **Wallet Order Management:** Manages wallet orders, retrieves payment details, and generates payment URLs.
  - **Webhooks:** Provides webhooks for receiving payment notifications and order updates.
- **Endpoints:**
  - `POST /wallet/order`: Create a new wallet order for cryptocurrency payment.
  - `GET /wallet/order/{orderId}`: Retrieve details of a specific wallet order.
  - Webhooks endpoints for receiving payment notifications.
- **Authentication:**
  - Requires API key and secret for authentication.
- **Sample Request (Create Wallet Order):**
  ```http
  POST /wallet/order HTTP/1.1
  Host: api.binance.com
  X-MBX-APIKEY: {api_key}
  Content-Type: application/json
  
  {
    "currency": "USDT",
    "amount": "1.00",
    "productDetail": "Event Payment",
    "productId": "EVENT123"
  }
  ```