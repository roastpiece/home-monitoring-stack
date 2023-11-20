FROM golang:1.21.4 as build

WORKDIR /build
COPY go.mod go.sum unbound-exporter.go ./

RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build 
RUN strip unbound-exporter


FROM gcr.io/distroless/base-nossl-debian12
COPY --from=build /build/unbound-exporter /unbound-exporter

ENTRYPOINT ["/unbound-exporter"]
