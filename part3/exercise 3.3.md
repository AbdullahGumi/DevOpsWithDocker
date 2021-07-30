### backend 
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

ENV REQUEST_ORIGIN http://localhost:5000

RUN go build

RUN go test ./...


RUN useradd -m gumi

USER gumi

### frontend
FROM node:14

WORKDIR /usr/src/app

COPY . .

ENV REACT_APP_BACKEND_URL http://localhost:8080

RUN node -v && npm -v

RUN npm install 

RUN npm install -g serve 

RUN npm run build 

RUN useradd -m gumi

USER gumi