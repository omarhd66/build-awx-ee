ARG EE_BASE_IMAGE=quay.io/ansible/ansible-runner:devel
ARG EE_BUILDER_IMAGE=quay.io/ansible/ansible-builder:latest

FROM $EE_BASE_IMAGE as galaxy
USER root


FROM $EE_BUILDER_IMAGE as builder

FROM $EE_BASE_IMAGE
USER root
COPY --from=builder /output/ /output/
RUN /output/install-from-bindep && rm -rf /output/wheels
LABEL ansible-execution-environment=true