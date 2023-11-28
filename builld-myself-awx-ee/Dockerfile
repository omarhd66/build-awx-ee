FROM quay.io/omarelhaoudar/awx-ee:latest


USER root

RUN rm -rf /usr/local/bin/ansible* /usr/local/lib/python3.8/site-packages/ansible*  /home/runner/.ansible
RUN for dir in /home/runner/.ansible /home/runner/.ansible/tmp ; do  mkdir -m 0775 -p $dir ; chmod -R g+rwx $dir ; chgrp -R root $dir ; done
RUN python3 -m pip install ansible==2.9.11

CMD ["/bin/sh" "-c" "/run.sh"]

USER 1000

RUN git lfs install
COPY . /var/lib/awx/key
ENV ANSIBLE_VAULT_PASSWORD_FILE=/var/lib/awx/key/.key
ENV SUPERVISOR_WEB_CONFIG_PATH=/etc/supervisord.conf
LABEL ansible-execution-environment=true