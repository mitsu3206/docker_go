# Build stage for deploy
# 必要に応じて、Goのバージョンを指定する。
# https://hub.docker.com/_/golang
FROM golang:latest AS builder

WORKDIR /go/src
# COPY go.mod ./
# COPY go.sum ./
# RUN go mod download
# COPY *.go ./
# RUN go build -o /main


# Local stage
FROM builder AS dev

WORKDIR /go/src
RUN go install github.com/air-verse/air@latest
# ENTRYPOINT [ "air" ]


# Deploy stage
FROM gcr.io/distroless/base AS deploy

WORKDIR /
COPY --from=builder /main /main
EXPOSE 8080
USER nonroot:nonroot
ENTRYPOINT [ "/main" ]
