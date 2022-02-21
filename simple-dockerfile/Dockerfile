FROM registry.access.redhat.com/ubi8/ubi:8.4

LABEL io.openshift.expose-services="8080:http"

RUN yum install -y httpd && \
    yum clean all && \ 
    sed -i 's/Listen 80/Listen 8080/g' /etc/httpd/conf/httpd.conf 

RUN chgrp -R 0 /var/www /run/httpd /var/log/httpd /etc/httpd/logs && \
    chmod -R g=u  /var/www /run/httpd /var/log/httpd /etc/httpd/logs

USER 1001

EXPOSE 8080

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
