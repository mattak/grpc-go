FROM golang:1.21.1-alpine AS builder

ENV ROOT=/go/src/app
WORKDIR ${ROOT}

RUN apk upgrade && apk add git
ADD greeter_server greeter_server
ADD helloworld helloworld
COPY go.mod go.sum ./
RUN go mod download
RUN go build -o main greeter_server/main.go

FROM golang:1.21.1-alpine AS runner

ENV ROOT=/go/src/app
WORKDIR ${ROOT}

COPY --from=0 /go/src/app/main ./
CMD ["./main"]
