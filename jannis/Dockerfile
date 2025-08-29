FROM golang:1.23.2 AS build

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY main.go ./

RUN CGO_ENABLED=0 GOOS=linux go build -o ./docker-example

# non-build image
FROM alpine
WORKDIR /app

COPY --from=build /app/docker-example .

EXPOSE 8080

CMD ["./docker-example"]