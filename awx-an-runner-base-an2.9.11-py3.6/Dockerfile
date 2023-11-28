ARG EE_BASE_IMAGE=quay.io/ansible/ansible-runner:devel
ARG EE_BUILDER_IMAGE=quay.io/ansible/ansible-builder:latest

FROM $EE_BASE_IMAGE as galaxy
ARG ANSIBLE_GALAXY_CLI_COLLECTION_OPTS=
ARG ANSIBLE_GALAXY_CLI_ROLE_OPTS=
USER root

FROM $EE_BUILDER_IMAGE as builder

FROM $EE_BASE_IMAGE
USER root
RUN rm -rf /usr/local/share/ansible-runner
RUN rm -rf /usr/local/bin/ansible*
RUN rm -rf /usr/local/lib/python3.8/site-packages/ansible*
RUN rm -rf /home/runner/.ansible
RUN dnf install python36 -y
COPY --from=builder /output/ /output/
RUN /output/install-from-bindep && rm -rf /output/wheels
RUN unlink /usr/bin/python3
RUN ln -s /usr/libexec/platform-python3.6 /usr/bin/python3
RUN /usr/bin/python3 -m pip install --upgrade pip==19.2
RUN pip3 install --upgrade pip setuptools
RUN /usr/bin/python3 -m pip install --upgrade pip==19.2
RUN pip install ansible==2.9.11
LABEL ansible-execution-environment=true