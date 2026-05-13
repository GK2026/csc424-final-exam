## DevOps Setup
Run the stack locally
To start all services locally with Docker Compose:

```bash
docker compose up --build -d

## Application Ports and Testing

The application is exposed through **port 80** using Nginx as a reverse proxy.

You can test the services using the following URLs:

- Frontend: http://localhost  
- Backend API: http://localhost/api/ping  

All traffic is routed through Nginx on port 80, which forwards requests to the appropriate frontend or backend service.

## Services Overview

### Frontend
The frontend is a React/Vite web application that provides the user interface. It runs in a Docker container and is served through Nginx. Users interact with the system through this layer.

### Backend
The backend is a Node.js/Express API service that handles application logic and processes API requests. It runs as two separate container instances (`backend-1` and `backend-2`) to support load balancing and scalability.

### Nginx
Nginx acts as a reverse proxy and load balancer. It:
- Serves the frontend application
- Routes API requests (`/api/*`) to the backend services
- Distributes traffic across multiple backend containers using round-robin load balancing

---

## CI/CD Pipeline

This project uses GitHub Actions for continuous integration and deployment.

When code is pushed to the `main` branch, the pipeline automatically:

1. Builds Docker images for:
   - frontend
   - backend
   - nginx

2. Pushes the images to Docker Hub using version tag `latest`.

3. Deploys the application to a self-hosted VM using Docker Compose.

4. The VM pulls the latest images and restarts the containers automatically.

This ensures every change to the codebase is automatically built, published, and deployed without manual intervention.
