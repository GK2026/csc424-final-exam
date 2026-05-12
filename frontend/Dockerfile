# syntax=docker/dockerfile:1

# Build stage
FROM node:22-alpine AS builder

WORKDIR /app

# Install dependencies
COPY package*.json ./

RUN npm install --no-fund --no-audit

# Copy source code
COPY . .

# Build React app
RUN npm run build

# Production stage
FROM nginx:1.27-alpine

# Copy React production build
COPY --from=builder /app/dist /usr/share/nginx/html
# Expose nginx port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
