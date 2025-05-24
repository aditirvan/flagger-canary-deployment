FROM golang:latest AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm64 go build -o myapp

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/myapp .
EXPOSE 8000
ENTRYPOINT ["./myapp"]