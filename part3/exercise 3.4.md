### backend 
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

ENV REQUEST_ORIGIN http://localhost:5000

RUN go build && \
    go test ./... && \
    useradd -m gumi

USER gumi

### frontend
FROM node:14

WORKDIR /usr/src/app

COPY . .

ENV REACT_APP_BACKEND_URL http://localhost:8080

RUN node -v && npm -v  && \ 
    npm install && \
    npm install -g serve && \ 
    npm run build && \
    useradd -m gumi
    
USER gumi