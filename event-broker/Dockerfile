FROM golang:alpine as build

RUN apk update
RUN apk add git upx
WORKDIR /
RUN git clone https://github.com/lemon-mint/event-broker.git
RUN cp -R /event-broker /app
WORKDIR /app
RUN go build -ldflags="-s -w" -v eventserver.go
RUN upx --lzma /app/eventserver

FROM alpine:latest
COPY --from=build /app /app
EXPOSE 16745
WORKDIR /app
CMD /app/eventserver
