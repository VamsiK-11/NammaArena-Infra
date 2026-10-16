# NammaArena - Infra

Infrastructure and orchestration repository for the NammaArena microservices architecture. Contains Docker Compose configuration to run all services together with a single command.

## Overview

NammaArena is a turf booking platform built with a microservices architecture. This repository contains the `docker-compose.yml` to spin up the entire backend stack including MySQL, all microservices and the API Gateway.

## Services

| Service | Port | Description |
|---|---|---|
| MySQL | 3307 | Database for all services |
| Eureka Server | 8761 | Service Discovery |
| API Gateway | 8080 | Entry point for all requests |
| Auth Service | 8081 | Authentication and Authorization |
| Turf Service | 8082 | Turf Management |
| Booking Service | 8083 | Booking Management |
| Payment Service | 8084 | Payment Processing via Stripe |

## Prerequisites
- Docker
- Docker Compose
- Each service repo cloned and jars built locally

## Getting Started

### 1. Clone all service repositories
```bash
git clone https://github.com/VamsiK-11/NammaArena-EurekaServer.git eureka-server
git clone https://github.com/VamsiK-11/NammaArena-APIGateway.git api-gateway
git clone https://github.com/VamsiK-11/NammaArena-AuthService.git auth-service
git clone https://github.com/VamsiK-11/NammaArena-TurfService.git turf-service
git clone https://github.com/VamsiK-11/NammaArena-BookingService.git booking-service
git clone https://github.com/VamsiK-11/NammaArena-PaymentService.git payment-service
```

### 2. Build each service
```bash
cd eureka-server && mvn clean package -DskipTests && cd ..
cd api-gateway && mvn clean package -DskipTests && cd ..
cd auth-service && mvn clean package -DskipTests && cd ..
cd turf-service && mvn clean package -DskipTests && cd ..
cd booking-service && mvn clean package -DskipTests && cd ..
cd payment-service && mvn clean package -DskipTests && cd ..
```

### 3. Run all services
```bash
docker-compose up --build
```

### 4. Stop all services
```bash
docker-compose down
```

### 5. Stop and remove volumes (wipe database)
```bash
docker-compose down -v
```

## Startup Order
Docker Compose handles the startup order automatically:
1. `mysql` — starts first with a healthcheck
2. `eureka-server` — starts after MySQL is healthy
3. `auth-service`, `turf-service`, `booking-service`, `payment-service` — start after Eureka is up
4. `api-gateway` — starts last after all services are up

## Accessing Services
| Service | URL |
|---|---|
| API Gateway | http://localhost:8080 |
| Eureka Dashboard | http://localhost:8761 |

## Microservices Repositories
| Service | Repository |
|---|---|
| Eureka Server | [NammaArena-EurekaServer](https://github.com/VamsiK-11/NammaArena-EurekaServer) |
| API Gateway | [NammaArena-APIGateway](https://github.com/VamsiK-11/NammaArena-APIGateway) |
| Auth Service | [NammaArena-AuthService](https://github.com/VamsiK-11/NammaArena-AuthService) |
| Turf Service | [NammaArena-TurfService](https://github.com/VamsiK-11/NammaArena-TurfService) |
| Booking Service | [NammaArena-BookingService](https://github.com/VamsiK-11/NammaArena-BookingService) |
| Payment Service | [NammaArena-PaymentService](https://github.com/VamsiK-11/NammaArena-PaymentService) |
