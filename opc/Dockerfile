FROM registry.access.redhat.com/ubi9/go-toolset:1.20@sha256:4b9c0a15e3be72c8455ee5398069c74bcde6d827a139c2c3b5f2db779c5b1db8 AS builder

WORKDIR /app
COPY . .
RUN go build -buildvcs=false -mod=vendor -o /app/opc main.go

FROM registry.access.redhat.com/ubi9/ubi-minimal:latest@sha256:bc552efb4966aaa44b02532be3168ac1ff18e2af299d0fe89502a1d9fabafbc5
LABEL name="opc" \
      com.redhat.component="opc" \
      io.k8s.display-name="opc" \
      summary="A CLI for OpenShift Pipeline" \
      description="opc makes it easy to work with Tekton resources in OpenShift Pipelines. It is built on top of tkn and tkn-pac and expands their capablities to the functionality and user-experience that is available on OpenShift." \
      io.k8s.description="opc makes it easy to work with Tekton resources in OpenShift Pipelines. It is built on top of tkn and tkn-pac and expands their capablities to the functionality and user-experience that is available on OpenShift." \
      io.openshift.tags="pipelines,tekton"
COPY --from=builder /app/opc /usr/bin
RUN mkdir /licenses
COPY LICENSE /licenses/.
RUN microdnf install -y shadow-utils
RUN groupadd -r -g 65532 nonroot && useradd --no-log-init -r -u 65532 -g nonroot nonroot
USER 65532
