FROM registry.access.redhat.com/ubi9/go-toolset:1.20 AS builder

WORKDIR /app
COPY . .
RUN go build -buildvcs=false -mod=vendor -o /app/opc main.go

FROM registry.redhat.io/ubi9/ubi-minimal:latest
COPY --from=builder /app/opc /usr/bin
RUN microdnf install -y shadow-utils
RUN groupadd -r -g 65532 nonroot && useradd --no-log-init -r -u 65532 -g nonroot nonroot
USER 65532