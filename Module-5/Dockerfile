# Stage 1: Build Go binary
FROM golang:1.17 AS builder

# Set necessary environment variables
ARG APP_NAME=myapp
ARG APP_PATH=/go/src/app

# Set the current working directory inside the container
WORKDIR $APP_PATH

# Copy go.mod and go.sum files to the working directory
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy the entire source code to the working directory
COPY . .

# Build the Go binary
RUN CGO_ENABLED=0 GOOS=linux go build -o $APP_NAME .

# Stage 2: Create a minimal image
FROM alpine:latest

# Set necessary environment variables
ARG APP_NAME=myapp
ARG APP_PATH=/usr/local/bin/
ENV PORT = 8080
# Set the current working directory inside the container
WORKDIR $APP_PATH

# Copy the binary from the builder stage to the working directory in the new stage
COPY --from=builder /go/src/app/$APP_NAME .


# Expose the port on which the Go application will run 
EXPOSE 8080
# Define environment variable for port 
ENV PORT=8080
# Set the command to run the Go binary
CMD ["./myapp"]
