# payara-production-domain-builder
Build payara production docmain template from source that can be used to create domains

#### Dockerfile sample to create a domain with default user name `admin` & password `admin`
```Dockerfile
FROM docker.io/payara/server-full:6.2023.3-jdk17
ADD --chown=payara:payara https://github.com/pretsa-xyz/payara-production-domain-builder/releases/download/v6.2023.3/production-domain.jar /opt/payara/production-domain.jar
ENV DOMAIN_NAME=my-domain
RUN ${PAYARA_DIR}/bin/asadmin --user=${ADMIN_USER} --passwordfile=${PASSWORD_FILE} create-domain --template /opt/payara/production-domain.jar ${DOMAIN_NAME} && \
    ${PAYARA_DIR}/bin/asadmin --user=${ADMIN_USER} --passwordfile=${PASSWORD_FILE} start-domain ${DOMAIN_NAME} && \
    ${PAYARA_DIR}/bin/asadmin --user=${ADMIN_USER} --passwordfile=${PASSWORD_FILE} enable-secure-admin && \
    ${PAYARA_DIR}/bin/asadmin --user=${ADMIN_USER} --passwordfile=${PASSWORD_FILE} stop-domain ${DOMAIN_NAME}
```
