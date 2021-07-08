FROM golang:1.16.5-alpine3.14

RUN apk add -U --no-cache ca-certificates curl git make gcc g++

WORKDIR /app

COPY ./src/go.mod ./
COPY ./src/go.sum ./

RUN go mod download

COPY ./src .

RUN make

FROM alpine:latest

ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
ARG APP_STAGE
ENV APP_STAGE $APP_STAGE

RUN apk add -U --no-cache ca-certificates curl tzdata

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /app
COPY --from=0 /app/ .
COPY build/entrypoint.sh .

ENTRYPOINT ["/bin/sh", "/app/entrypoint.sh"]