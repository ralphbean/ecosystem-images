FROM registry.access.redhat.com/ubi9/go-toolset:1.20.12-3.1713832665-source AS builder

WORKDIR /app
COPY . .
RUN go build -buildvcs=false -mod=vendor -o /app/opc main.go

FROM registry.access.redhat.com/ubi9/ubi-minimal:9.3-1612-source
COPY --from=builder /app/opc /usr/bin
RUN microdnf install -y shadow-utils
RUN groupadd -r -g 65532 nonroot && useradd --no-log-init -r -u 65532 -g nonroot nonroot
USER 65532
