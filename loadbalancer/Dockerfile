FROM centos:7
MAINTAINER Jean Lejeune <jlejeune@immunit.ch>

RUN yum -y update
RUN yum install -y httpd httpd-devel gcc libtool wget ea-apache24-devel make

RUN wget https://archive.apache.org/dist/tomcat/tomcat-connectors/jk/tomcat-connectors-1.2.44-src.tar.gz -O /tmp/jk.tar.gz
RUN tar xvf /tmp/jk.tar.gz -C /tmp/

WORKDIR /tmp/tomcat-connectors-1.2.44-src/native

RUN ./configure -with-apxs=/usr/bin/apxs
RUN make
RUN mv apache-2.0/mod_jk.so /etc/httpd/modules/mod_jk.so

ADD cnf/httpd.conf /etc/httpd/conf/httpd.conf
ADD cnf/00-base.conf /etc/httpd/conf.modules.d/00-base.conf
ADD cnf/mod-jk.conf /etc/httpd/conf.d/mod-jk.conf
ADD cnf/workers.properties /etc/httpd/conf/workers.properties

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
