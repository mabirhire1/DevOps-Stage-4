FROM node:12 AS builder

WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy project files
COPY . .

# Build the app
RUN npm run build

ARG PORT
ARG AUTH_API_ADDRESS
ARG TODOS_API_ADDRESS

ENV PORT=${PORT} \
    AUTH_API_ADDRESS=${AUTH_API_ADDRESS} \
    TODOS_API_ADDRESS=${TODOS_API_ADDRESS}

# Production stage
FROM nginx:alpine

# Copy built files
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]    
