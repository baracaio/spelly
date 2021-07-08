include .env
export

.PHONY: all build run up deps

GOPATH ?= $(HOME)/go

all: build

build:
	GOOS=linux GOARCH=amd64 go build -o main -a -v

run:
	go run -race main.go api