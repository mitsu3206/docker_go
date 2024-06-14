# Build stage for deploy
# 必要に応じて、Goのバージョンを指定する。
# https://hub.docker.com/_/golang
FROM golang:latest AS builder

WORKDIR /go/src/dev
COPY . .
RUN go mod download
RUN go build -o /main ./cmd/go-dev


# Local stage
FROM builder AS dev

WORKDIR /go/src/dev
RUN go install github.com/air-verse/air@latest
ENTRYPOINT [ "air" ]


# Deploy stage
FROM gcr.io/distroless/base AS deploy

WORKDIR /
COPY --from=builder /main /main
EXPOSE 8080
USER nonroot:nonroot
ENTRYPOINT [ "/main" ]
