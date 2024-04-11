+++
title = 'Code Configuration and Samples'
+++

# Code Configuration and Samples

## Configuration:

1. **Google Calendar API Configuration:**
    - Obtain the Google Cloud project credentials (service account JSON file).
    - Ensure the Google Calendar API is enabled for the project.
    - Set up OAuth consent screen and obtain OAuth client ID and client secret.

2. **PayPal REST API Configuration:**
    - Sign up for a PayPal Business account or use sandbox credentials.
    - Generate API credentials (Client ID and Secret) from the PayPal Developer Dashboard.
    - Configure webhooks for receiving payment notifications.

3. **Binance Pay API Configuration:**
    - Register for a Binance account and enable Binance Pay.
    - Generate API key and secret from the Binance Developer Dashboard.
    - Set up webhooks for handling payment callbacks.

## Code Samples:

1. **Google Calendar API Integration (Python):**
    - Initialize Google Calendar service using service account credentials:
      ```python
      from google.oauth2 import service_account
      import googleapiclient.discovery
      
      SCOPES = ['https://www.googleapis.com/auth/calendar']
      SERVICE_ACCOUNT_FILE = 'path/to/service_account.json'
      
      credentials = service_account.Credentials.from_service_account_file(SERVICE_ACCOUNT_FILE, scopes=SCOPES)
      service = googleapiclient.discovery.build('calendar', 'v3', credentials=credentials)
      ```

2. **PayPal REST API Integration (JavaScript - Node.js):**
    - Create a PayPal order for payment:
      ```javascript
      const paypal = require('@paypal/checkout-server-sdk');
      
      const clientId = 'YOUR_CLIENT_ID';
      const clientSecret = 'YOUR_CLIENT_SECRET';
      
      const environment = new paypal.core.SandboxEnvironment(clientId, clientSecret);
      const client = new paypal.core.PayPalHttpClient(environment);
      
      const request = new paypal.orders.OrdersCreateRequest();
      request.prefer('return=representation');
      request.requestBody({
          intent: 'CAPTURE',
          purchase_units: [{
              amount: {
                  currency_code: 'USD',
                  value: '1.00'
              }
          }]
      });
      
      const createOrder = async () => {
          const response = await client.execute(request);
          return response.result.id;
      };
      
      createOrder().then(orderId => {
          console.log('Created order with ID:', orderId);
          // Redirect user to PayPal for payment approval
      }).catch(error => {
          console.error('Error creating order:', error);
      });
      ```

3. **Binance Pay API Integration (Java):**
    - Create a wallet order for cryptocurrency payment:
      ```java
      import com.binance.pay.APIFactory;
      import com.binance.pay.PayClient;
      import com.binance.pay.impl.PayClientImpl;
      import com.binance.pay.model.enums.Currency;
      import com.binance.pay.model.wallet.WalletOrderRequest;
      
      public class BinancePayExample {
          public static void main(String[] args) {
              String apiKey = "YOUR_API_KEY";
              String apiSecret = "YOUR_API_SECRET";
      
              APIFactory factory = new APIFactory(apiKey, apiSecret);
              PayClient payClient = new PayClientImpl(factory);
      
              WalletOrderRequest orderRequest = new WalletOrderRequest();
              orderRequest.setCurrency(Currency.USDT);
              orderRequest.setAmount("1.00");
              orderRequest.setProductDetail("Event Payment");
              orderRequest.setProductId("EVENT123");
      
              String paymentUrl = payClient.createWalletOrder(orderRequest);
              System.out.println("Payment URL: " + paymentUrl);
          }
      }
      ```

These code samples demonstrate the configuration steps and basic usage of the Google Calendar, PayPal, and Binance Pay APIs within the LeadsCalendar project. Ensure to replace placeholders such as `YOUR_CLIENT_ID`, `YOUR_CLIENT_SECRET`, `YOUR_API_KEY`, and `YOUR_API_SECRET` with your actual credentials.