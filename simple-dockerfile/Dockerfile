FROM registry.access.redhat.com/ubi8/ubi:8.4 

MAINTAINER Red Hat Training <training@redhat.com>

LABEL io.openshift.expose-services="8080:http"

# DocumentRoot for Apache
ENV DOCROOT /var/www/html 

RUN   yum install -y --disableplugin=subscription-manager httpd && \ 
      yum clean all --disableplugin=subscription-manager -y && \
      echo "Hello from the httpd-parent container!" > ${DOCROOT}/index.html  && \ 
      sed -i 's/Listen 80/Listen 8080/g' /etc/httpd/conf/httpd.conf 

# Allows child images to inject their own content into DocumentRoot
ONBUILD COPY src/ ${DOCROOT}/ 

EXPOSE 8080

# This stuff is needed to ensure a clean start
RUN rm -rf /run/httpd && mkdir /run/httpd

# Run as the root user
USER root

ADD scripts/docker-entrypoint.sh /

RUN chmod +x /docker-entrypoint.sh

# Launch httpd
CMD /docker-entrypoint.sh

