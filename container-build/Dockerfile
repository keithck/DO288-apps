# Use the httpd-parent image as base
FROM quay.io/redhattraining/httpd-parent
MAINTAINER RED Hat Training <training@redhat.com>

ENV DOCROOT=/var/www/html

RUN yum install -y --no-docs --disableplugin=subscription-manager httpd && \
 yum clean all --disableplugin=subscription-manager -y && \
 echo "Hello from the httpd-parent container!" > ${DOCROOT}/index.html

ONBUILD COPY src/ ${DOCROOT}

LABEL io.openshift.expose.services="8080:http"

LABEL io.k8s.description="A basic Apache HTTP Service" \
      io.k8s.display-name="Apache HTTP Server" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="apache.httpd"


RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf

RUN chgrp -R 0 /var/log/httpd /var/run/httpd && \
    chmod -R g=u /var/log/httpd /var/run/httpd


EXPOSE 8080

RUN rm -fr /run/httpd && mkdir /run/httpd

USER 1001

CMD /usr/sbin/httpd -DFOREGROUND
