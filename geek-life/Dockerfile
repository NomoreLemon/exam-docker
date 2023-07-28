# first stage : compile golant to binary
FROM golang:1.20-alpine AS build

WORKDIR /app

COPY go.mod ./

COPY  go.sum ./

RUN go mod download

ADD . /app/

RUN go build -o geek-life 

FROM alpine:3.9.6

WORKDIR /app

COPY --from=build /app/geek-life  .

ENTRYPOINT ["./geek-life "]
