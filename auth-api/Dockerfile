FROM golang:1.21-alpine AS builder

WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy the source code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-api .

# Use a minimal alpine image for the final stage
FROM alpine:latest

WORKDIR /app

# Add ca-certificates for HTTPS requests
RUN apk --no-cache add ca-certificates

# Copy the binary from the builder stage
COPY --from=builder /app/auth-api .

# Expose the port your application runs on (adjust if different)
EXPOSE 8081

# Run the application
CMD ["./auth-api"]
