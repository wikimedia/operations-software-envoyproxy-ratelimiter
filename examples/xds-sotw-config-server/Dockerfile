FROM golang:1.23.3@sha256:d56c3e08fe5b27729ee3834854ae8f7015af48fd651cd25d1e3bcf3c19830174 AS build
WORKDIR /xds-server

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/xds-server -v main/main.go

FROM alpine:3.16@sha256:e4cdb7d47b06ba0a062ad2a97a7d154967c8f83934594d9f2bd3efa89292996b AS final
RUN apk --no-cache add ca-certificates && apk --no-cache update
COPY --from=build /go/bin/xds-server /bin/xds-server
ENTRYPOINT [ "/bin/xds-server" ]
