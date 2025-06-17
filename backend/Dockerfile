# Prepare builder
FROM golang:1.23.9-alpine AS builder
RUN apk add --no-cache git
WORKDIR /app
COPY . .

# Build
RUN go mod download
RUN go build -a -installsuffix cgo -o main ./cmd/api

# Prepare runner
FROM alpine:3.22
RUN apk add --no-cache ca-certificates tzdata && update-ca-certificates
RUN adduser -D -g '' runner
WORKDIR /app
COPY --from=builder /app/main .
USER runner
EXPOSE 8080

# Run the application
CMD ["./main"]