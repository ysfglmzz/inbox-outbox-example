FROM golang:1.18.3-alpine3.15 as builder

WORKDIR /app

ENV CGO_ENABLED=0

COPY . .

RUN go mod download
RUN go build cmd/consumer-service/main.go

FROM alpine

COPY --from=builder /app/main /app/main
COPY --from=builder /app/resource/config.yaml /app/config.yaml
COPY --from=builder /app/resource/queue.yaml /app/queue.yaml


WORKDIR /app

CMD [ "./main" ]