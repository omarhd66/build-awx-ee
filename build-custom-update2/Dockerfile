FROM quay.io/omarelhaoudar/awx-ee:latest
COPY . /var/lib/awx/key
ENV ANSIBLE_VAULT_PASSWORD_FILE=/var/lib/awx/key/.key
ENV SUPERVISOR_WEB_CONFIG_PATH=/etc/supervisord.conf