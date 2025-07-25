
# 🏦 High-Level Payment System Architecture (Enhanced + Optional Enhancements)

```
[Client] 
   --> [Load Balancer] 
       --> [App Servers] "Idempotent transactions"
           --> [Rate Limiter]
           --> [Retry Queue] 
               --> [Payment Gateway] 
                   --> [Fraud Detection Service]
                       --> [Database]
                           --> [Audit Logger]
                               --> [Notification Service]
[Retry Queue] --> [Dead Letter Queue]

[Monitoring / Alerting] -- monitors --> [Payment Gateway], [Fraud Detection Service], [Retry Queue]
```

## 🔖 Component Descriptions

- **[Client]**  
  UI/mobile/web app initiating a payment request.

- **[Load Balancer]**  
  Distributes traffic across app servers.

- **[App Servers]**  
  - Label: `"Idempotent transactions"`  
  - Validates request, applies idempotency key, logs request.

- **[Rate Limiter]**  
  Prevents abuse/fraud by limiting requests per user/IP.

- **[Retry Queue]**  
  Buffers messages for reliable delivery in case of temporary downstream issues (Kafka/RabbitMQ).

- **[Dead Letter Queue]**  
  Catches and stores failed/undeliverable transactions for manual or automated reprocessing.

- **[Payment Gateway]**  
  Handles secure communication with external payment providers.

- **[Fraud Detection Service]**  
  Runs rules or ML-based anomaly detection before payment commitment.

- **[Database]**  
  Stores transaction data, user metadata, status logs.

- **[Audit Logger]**  
  Writes to a secure, immutable audit trail for compliance.

- **[Notification Service]**  
  Notifies clients of transaction success/failure (email, SMS, push).

- **[Monitoring / Alerting]**  
  Observability layer for critical components (Prometheus/Grafana, ELK, CloudWatch).
