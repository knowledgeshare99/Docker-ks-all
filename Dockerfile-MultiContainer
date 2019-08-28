FROM centos:5

RUN yum install -y epel-release && \
    yum update -y && \
    yum install -y exim \
                   httpd \
                   mysql-server \
                   supervisor && \
    yum clean all

RUN /sbin/service mysqld start && \
    mysqladmin -u root password ''

RUN echo "[supervisord]" > /etc/supervisord.conf && \
    echo "nodaemon=true" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:exim]" >> /etc/supervisord.conf && \
    echo "command=/usr/sbin/exim -bd -q1h" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:mysqld]" >> /etc/supervisord.conf && \
    echo "command=/usr/bin/mysqld_safe" >> /etc/supervisord.conf && \
    echo "" >> /etc/supervisord.conf && \
    echo "[program:httpd]" >> /etc/supervisord.conf && \
    echo "command=/usr/sbin/apachectl -D FOREGROUND" >> /etc/supervisord.conf

CMD ["/usr/bin/supervisord"]
