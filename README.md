# Kong API Gateway for Zoo Microservices

## Overview
This repository contains the configuration for **Kong API Gateway** in DB-less mode to route requests to various zoo microservices.

## Microservices Routed Through Kong
- **zoo-animals-service** → `/animals`
- **zoo-reports-service** → `/reports`
- **zoo-staff-service** → `/staff`
- **zoo-food-service** → `/food`
- **zoo-breeding-service** → `/breeding`
- **zoo-enclosures-service** → `/enclosures`

## Setup

### 1. Install Docker
Ensure **Docker** and **Docker Compose** are installed.

### 2. Clone the Repository
```sh
git clone https://github.com/your-repo/zoo-kong.git
cd zoo-kong
