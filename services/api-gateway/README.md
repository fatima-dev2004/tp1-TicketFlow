# api-gateway

> Single entry point for TicketFlow microservices.

## Concept illustrated
Spring Cloud Gateway routes client requests to the correct backend service.
This first version uses static routing. Service discovery with Eureka will come
later.

## Overview
- **Port:** 8080
- **Depends on:** customer-service
- **Routes to:** `customer-service` on port 8081

| Client path | Destination |
|---|---|
| `/api/customers/**` | `customer-service` |

## Run locally
Start `customer-service` first:

    ./mvnw -pl services/customer-service spring-boot:run

Then start the gateway:

    ./mvnw -pl services/api-gateway spring-boot:run

Test through the gateway:

    curl http://localhost:8080/api/customers

## Run with Docker
    docker compose -f infra/docker-compose.yml up --build api-gateway

## Configuration
The local default route is:

    CUSTOMER_SERVICE_URL=http://localhost:8081

Docker Compose overrides it with:

    CUSTOMER_SERVICE_URL=http://customer-service:8081
