FROM golang:1.24.3@sha256:39d9e7d9c5d9c9e4baf0d8fff579f06d5032c0f4425cdec9e86732e8e4e374dc AS build
WORKDIR /xds-server

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/xds-server -v main/main.go

FROM alpine:3.16@sha256:e4cdb7d47b06ba0a062ad2a97a7d154967c8f83934594d9f2bd3efa89292996b AS final
RUN apk --no-cache add ca-certificates && apk --no-cache update
COPY --from=build /go/bin/xds-server /bin/xds-server
ENTRYPOINT [ "/bin/xds-server" ]
