# Build stage
FROM golang:1.21 as builder

WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o go-app .

# Runtime stage
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/go-app .
EXPOSE 8080
CMD ["./go-app"]