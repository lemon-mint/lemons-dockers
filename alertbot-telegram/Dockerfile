FROM golang:alpine as build

RUN apk update
RUN apk add git upx
WORKDIR /
RUN git clone https://github.com/lemon-mint/alertbot-telegram.git
RUN cp -R /alertbot-telegram /app
WORKDIR /app
RUN go build -ldflags="-s -w" -v main.go
RUN upx --lzma /app/main

FROM alpine:latest
COPY --from=build /app /app
EXPOSE 16745
WORKDIR /app
CMD /app/main

