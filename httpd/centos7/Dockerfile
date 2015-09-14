FROM centos:latest
MAINTAINER http://www.centos.org
LABEL Vendor="CentOS"
LABEL License=GPLv2
LABEL Version=2.4.6-31

RUN yum -y update && yum clean all
RUN yum -y install httpd && yum clean all

# use a port other than 80 so we don't have to run as root
RUN sed -i -e 's/Listen 80/Listen 8080/' /etc/httpd/conf/httpd.conf 
EXPOSE 8080

# Simple startup script to avoid some issues observed with container restart 
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh 

RUN chown -R 1001:0 /run/httpd && \
    chown -R 1001:0 /etc/httpd && \
    chown -R 1001:0 /var/log/httpd
USER 1001
CMD ["/run-httpd.sh"]
