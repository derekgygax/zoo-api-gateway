# Kong API Gateway for Zoo Microservices

## Overview
This repository contains the configuration for **Kong API Gateway** in **DB-less mode** to route requests to various zoo microservices.

## Microservices Routed Through Kong
| Service Name            | Kong Route       | Internal Service URL      |
|-------------------------|-----------------|---------------------------|
| **zoo-animals-service** | `/animals`      | `http://localhost:8100`   |
| **zoo-food-service**    | `/food`         | `http://localhost:8101`   |
| **zoo-staff-service**   | `/staff`        | `http://localhost:8102`   |
| **zoo-breeding-service**| `/breeding`     | `http://localhost:8103`   |
| **zoo-enclosures-service** | `/enclosures` | `http://localhost:8104`   |
| **zoo-reports-service** | `/reports`      | `http://localhost:8105`   |

Kong acts as a **reverse proxy**, forwarding incoming requests to the correct microservice based on the route.

---

## Setup Instructions

### 1. Install Docker
Ensure **Docker** and **Docker Compose** are installed.  
If not, install them:

- [Docker Install Guide](https://docs.docker.com/get-docker/)
- [Docker Compose Install Guide](https://docs.docker.com/compose/install/)

### 2. Clone the Repository
```sh
git clone https://github.com/your-repo/zoo-kong.git
cd zoo-kong
```

### 3. Start Kong
Run the following command to **start Kong**:
```sh
docker-compose up -d
```

This will:
- Start Kong in **DB-less mode**.
- Load the routes defined in `kong.yml`.

---

## Usage Instructions

### Check if Kong is Running
To confirm Kong is up, run:
```sh
curl -i http://localhost:8001
```
This should return a response from the **Kong Admin API**.

### Test Routing to a Microservice
Try sending a request to one of your microservices through Kong:
```sh
curl -i http://localhost:8000/animals
```
This should proxy the request to `zoo-animals-service` (`http://localhost:8100`).

#### Example: Fetching Reports
```sh
curl -i http://localhost:8000/reports
```
This will route the request to `zoo-reports-service` (`http://localhost:8105`).

---

## Managing Kong Configuration

### Modify Routes
If you need to **add, remove, or update** routes:
1. Edit `kong.yml` with the necessary changes.
2. Restart Kong for the changes to take effect:
   ```sh
   docker-compose down && docker-compose up -d
   ```

### Stopping Kong
To stop Kong, run:
```sh
docker-compose down
```

---

## Notes
- Kong runs in **DB-less mode**, meaning all configuration is stored in `kong.yml`.
- Any changes to `kong.yml` require a **restart** to take effect.
- Ensure your **microservices are running** before making requests via Kong.

---

## Debugging Issues

### Kong Not Starting?
Check logs with:
```sh
docker logs kong-gateway
```

### Routes Not Working?
- Ensure the microservices are running.
- Check `kong.yml` for incorrect service URLs.
- Restart Kong after updating `kong.yml`:
  ```sh
  docker-compose down && docker-compose up -d
  ```

---

## Next Steps
- Add **Rate Limiting** plugins to protect services from abuse.
- Implement **JWT Authentication** for securing endpoints.
- Enable **Logging & Monitoring** for API requests.

---