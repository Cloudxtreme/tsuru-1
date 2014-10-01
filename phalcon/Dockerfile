FROM centos:centos6
MAINTAINER Long TRAN <long.tran@glandoresystems.com>
RUN sed -i '/distroverpkg=centos-release/a tsflags=nodocs' /etc/yum.conf
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN sed -i.bak /etc/yum.repos.d/epel.repo -e '6s/0/1/'
RUN rpm --import http://rpms.famillecollet.com/RPM-GPG-KEY-remi
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN sed -i.bak /etc/yum.repos.d/remi.repo -e '5s/0/1/'
RUN yum update -y
RUN yum install python-setuptools -y
RUN easy_install supervisor
RUN mkdir -p /var/log/supervisord
RUN yum install which -y
#RUN yum install wget -y
RUN yum install git -y
RUN yum install httpd -y
RUN useradd -r -M supervisord
RUN chown -R supervisord /var/log/supervisord
#RUN wget https://raw.githubusercontent.com/longthanhtran/tsuru/master/phalcon/supervisord.conf -O /tmp/supervisord.conf
#ADD /tmp/supervisord.conf /etc/supervisord.conf
RUN echo "[supervisord]" >> /etc/supervisord.conf
RUN echo "nodaemon=true" >> /etc/supervisord.conf
RUN echo "[program:httpd]" >> /etc/supervisord.conf
RUN echo "command=/bin/bash -c "exec /usr/sbin/apachectl start"" >> /etc/supervisord.conf
EXPOSE 22 80
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf" ]
