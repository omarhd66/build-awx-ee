ARG EE_BASE_IMAGE=quay.io/omarelhaoudar/awx-ee:custom-update2
ARG EE_BUILDER_IMAGE=quay.io/ansible/ansible-builder:latest

FROM $EE_BASE_IMAGE as galaxy
ARG ANSIBLE_GALAXY_CLI_COLLECTION_OPTS=
ARG ANSIBLE_GALAXY_CLI_ROLE_OPTS=
USER root


FROM $EE_BUILDER_IMAGE as builder

FROM $EE_BASE_IMAGE
USER root
RUN rm -rf $(find / -name *ansible*)
RUN pip3 install --upgrade pip setuptools
COPY --from=builder /output/ /output/
RUN /output/install-from-bindep && rm -rf /output/wheels
RUN pip install ansible==2.9.11
LABEL ansible-execution-environment=true