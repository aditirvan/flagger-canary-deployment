FROM golang:latest as builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine:latest as release
WORKDIR /app
COPY --from=builder /app/myapp .
EXPOSE 8000
ENTRYPOINT ["./myapp"]


