# Azure Microservices Deployment Lab - Sample Project

This is a beginner-friendly sample project following a microservices architecture style.

For now, it includes:
- A **Gateway service** (Node.js + Express)
- A simple **Frontend** (`index.html`) that calls the gateway
- Docker support for container-based deployment

## Project Structure

```text
root/
  gateway/
    server.js
    package.json
    Dockerfile
  frontend/
    index.html
  docker-compose.yml
  README.md
```

## Gateway Endpoints

- `GET /` -> `Gateway is running`
- `GET /health` -> `{ "status": "ok" }`
- `GET /api/products` -> sample product JSON data

## Local Run (Without Docker)

```bash
cd gateway
npm install
npm start
```

Gateway runs on:
- `http://localhost:3000`

Then open frontend file in browser:
- `frontend/index.html`

## Docker Build and Run

From project root:

```bash
docker build -t gateway-service ./gateway
```

```bash
docker run -p 3000:3000 -e PORT=3000 --name gateway-service gateway-service
```

## Docker Compose (Optional)

From project root:

```bash
docker compose up --build
```

## Azure Container Deployment Notes

- App uses `PORT` environment variable (`process.env.PORT || 3000`) for compatibility with Azure container hosting.
- Container exposes port `3000` in Dockerfile.
- Gateway uses CORS and JSON middleware.
- Includes basic request logging and centralized error handling middleware.

## Quick API Test

After service is running:

```bash
curl http://localhost:3000/
curl http://localhost:3000/health
curl http://localhost:3000/api/products
```
