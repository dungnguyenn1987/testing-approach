# Payment Test
## Types of Payment gateways
<details>
  
- **Hosted payment gateways**: These gateways **redirect the customer to the payment service provider’s platform to complete the transaction**. After the customer completes the payment, they are redirected to the business’s website. This method benefits businesses because it outsources most of the security requirements to the payment service provider. Examples of hosted payment gateways include **PayPal and Stripe**.

- **Self-hosted payment gateways**: These gateways **collect payment details from the customer within the business’s website or application, then send the data to the payment gateway’s URL**. Some gateways require the business to capture the payment data in a specific format, while others offer more flexibility. This method puts greater security obligations on the business because it needs to handle and secure the payment data.

- **API-hosted payment gateways**: These gateways **let businesses integrate payment processing capabilities into their websites or mobile applications using the gateway’s application programming interface (API)**. API-hosted payment gateways provide a better user experience because customers do not need to leave the business’s platform to complete the transaction, as required with hosted gateways. Note that this type of payment gateway has the same security obligations as self-hosted payment gateways.

- **Local bank integration gateways**: This type of gateway **redirects the customer to the website of their chosen BANK to complete the payment**. After the transaction is processed, the customer is redirected to the business’s site, where the payment status is displayed. This method is straightforward but might not provide the best user experience because the customer has to leave the business’s site to complete the payment.

</details>

## Test approach
<details>

![image](https://github.com/user-attachments/assets/4304f929-a0ef-4197-b848-7d9623116306)

**Functional testing**: This type of testing checks that the payment system operates according to its specified requirements by verifying payment processing, transaction statuses, refunds, chargebacks, and reconciliation processes.
- Transaction processing
  - Successful transaction: Verify that a payment can be processed successfully using valid payment details. Check whether the transaction status is updated correctly and whether the funds are transferred as expected.
  - Failed transaction: Test with invalid card details or insufficient funds to check whether the transaction fails as expected and the user receives a clear error message.
  - Pending transaction: Some transactions might not be processed instantly and could be marked as pending. Verify that pending transactions are handled correctly and updated once they are processed.
- Card information
  - Card validity: Test with expired, invalid, or blocked cards to check whether the system properly validates card details.
  - Save card information: If the gateway lets users save their card details for future transactions, test the save functionality to confirm the data is securely stored and correctly retrieved for subsequent transactions.

- Refunds and chargebacks
  - Initiate refunds: Test the process of initiating a refund through the gateway, and verify that the transaction reverses correctly.
  - Chargeback process: Test the workflow for handling chargebacks, confirming the business can respond to and manage chargeback disputes.

- Error handling and messaging
  - Connection issues: Simulate network or server issues to test how the gateway handles connection failures, checking that users receive clear and appropriate messages.
  - Timeouts: Test how the system handles timeouts, at the front end (user interface) and back end (server or API level).

**Integration testing**
- API integration: Verify that the payment gateway’s API correctly integrates with the business’s system.
- Third-party integrations: If the gateway integrates with other services (such as shipping, tax calculation, or fraud detection), test these integrations for correct functionality.

</details>

# Test your app with 3rd parties
## Test approach
<details>

Testing third-party APIs is super important to make sure our apps work properly with external services.
Depending on the type and purpose of the third-party API, different testing approaches may be necessary to verify integration with your web app. 
- On testing environments, developers integrated to the provided sandbox to test functionality (e.g payment gateways like Paypal, Stripe..). On Production, integrated to real systems, teser should use test account (that registered to bank) to perform testing
- Mocking involves creating a simulated version of the third-party API that mimics its behavior,
- while stubbing involves creating a simplified version that returns predefined responses.
- Contract testing verifies that the third-party API adheres to a predefined contract or specification,
- and live testing calls the actual API and observes its responses and behavior.

Mocking and stubbing are useful for testing logic and edge cases without relying on external service availability or performance, while contract testing is beneficial for verifying compatibility and consistency. Live testing is best for testing performance, reliability, and security, but requires more resources, time, and caution.

</details>

## Mock techniques
<details>

With mocking, developers can create dummy responses from the API to imitate different situations like success, failures, timeouts, and dealing with big data. This way, we can run tests without relying on external services, making sure our results are consistent and predictable.

Scenarios for using mock in Third Party API

1. **Scenario 1: Testing Error Handling**
Your application interacts with a payment gateway API to process transactions. You need to test how your application handles error responses from the payment gateway, such as insufficient balance, expired tokens, or server errors.

Why Mocking is Needed:

Despite having the test or sandbox environment setup, it is always super hard to test insufficient balance scenarios as the external providers do not care about giving test support for these. Mocking the payment gateway API allows you to simulate error responses and test your application’s error-handling logic without affecting real data or transactions.

2. **Scenario 2: Testing Rate Limiting**
In your application, you’ve connected with a weather forecast API to keep users updated on the weather. This API has set limits to maintain fairness and prevent misuse. Now, you’re tasked with checking how your application handles situations where the weather forecast API sends back rate-limited responses. This means you’ll need to simulate scenarios where the API reaches its limits and see how your application responds accordingly, ensuring a seamless user experience despite these limitations.

Why Mocking is Needed:

Testing rate limiting with the live weather forecast API may lead to your application being temporarily blocked or restricted due to exceeding the rate limits. Mocking the weather forecast API allows you to simulate rate-limited responses and test how your application gracefully handles such scenarios, such as implementing retry logic or displaying informative messages to users.

3. **Scenario 3: Testing Network Errors**
Your application depends on a third-party geolocation API to fetch location data for user profiles. Now, it’s crucial to examine how your application reacts when confronted with network errors such as connection timeouts, DNS resolution failures, or server unavailability. This entails conducting rigorous testing to replicate these error conditions and assess your application’s resilience. By simulating these network error scenarios during testing, you can verify that your application handles them effectively, ensuring uninterrupted functionality for users even in the face of network challenges.

Why Mocking is Needed:

Trying to test network errors with the actual geolocation API may not always work well because network conditions can change and give you unreliable test results. Instead, using a mock geolocation API lets you create and control network errors in a safe setup. This way, you can make sure your app handles these errors correctly, like showing error messages to users or trying requests again if they fail.

4. **Scenario 4: Testing Large Data Responses**
Your application interacts with a third-party product catalog API to retrieve product information for an e-commerce platform. You need to test how your application handles large data responses from the product catalog API, such as paginated responses or responses with a high number of products.

Why Mocking is Needed:

Testing large data responses with the live product catalog API may impact performance and scalability, especially during automated tests or continuous integration pipelines. Mocking the product catalog API allows you to generate mock responses with large data sets and test how your application efficiently processes and displays the data, such as implementing pagination or optimising resource usage.

In each of these scenarios, mocking the third-party API is essential to simulate various conditions and behaviours without relying on live production environments. Mocking enables you to conduct thorough and controlled tests, ensuring that your application behaves as expected under different scenarios and conditions while minimising risks and dependencies on external services.

</details>
