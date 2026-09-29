# Day 13 — Distributed Food Ordering & Delivery Platform 🍔

Java 17 + Spring Boot microservices portfolio project for orders, restaurants, payments, delivery dispatch and notifications.

## Services
Order 8081 | Restaurant 8082 | Payment 8083 | Delivery 8084 | Notification 8085 | PostgreSQL 5432 | Redis 6379 | Kafka 9092 | Prometheus 9090 | Grafana 3000

## Run
```powershell
cd distributed-food-delivery-day13
docker compose up --build
```

## Test
```powershell
mvn -B test
```

## Create order
```powershell
$body='{"customerId":"customer-101","restaurantId":"restaurant-22","total":349.50}'
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders -ContentType 'application/json' -Body $body
```

## Order lifecycle
Replace ORDER_ID with the returned UUID:
```powershell
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/CONFIRMED
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/PAYMENT_PENDING
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/PAID
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/PREPARING
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/READY_FOR_PICKUP
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/OUT_FOR_DELIVERY
Invoke-RestMethod -Method Post -Uri http://localhost:8081/api/orders/ORDER_ID/status/DELIVERED
```

## Payment idempotency
```powershell
$payment='{"orderId":"ORDER_UUID","amount":349.50,"idempotencyKey":"order-ORDER_UUID-payment-1"}'
Invoke-RestMethod -Method Post -Uri http://localhost:8083/api/payments -ContentType 'application/json' -Body $payment
```

## Delivery partner
```powershell
$partner='{"name":"Partner One","lat":26.8467,"lng":80.9462}'
Invoke-RestMethod -Method Post -Uri http://localhost:8084/api/delivery/partners -ContentType 'application/json' -Body $partner
```

## GitHub
Create an empty repo named `distributed-food-delivery-day13`, then:
```powershell
git init
git add .
git commit -m "Day 13: distributed food delivery platform"
git branch -M main
git remote add origin https://github.com/Vermaaditya@3030/distributed-food-delivery-day13.git
git push -u origin main
```

## Included
Order state machine, restaurant/menu APIs, payment idempotency/refund, nearest delivery partner using Haversine distance, Redis/Kafka infrastructure, Docker Compose, Prometheus/Grafana, JUnit tests and GitHub Actions.

## Production roadmap
JWT/RBAC, Kafka consumers + transactional outbox, retry/DLT, Redis GEO, distributed locks, WebSocket/SSE tracking, real payment gateway/webhooks, OpenTelemetry, rate limiting and TLS.
