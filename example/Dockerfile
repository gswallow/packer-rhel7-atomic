FROM registry.access.redhat.com/rhel7-atomic
MAINTAINER Greg Swallow (gswallow@ivytech.edu)

RUN microdnf install java-1.8.0-oracle.x86_64 \
  java-1.8.0-oracle-jdbc.x86_64 \
  wget \
  --enablerepo=rhel-7-server-thirdparty-oracle-java-rpms \
  --enablerepo=rhel-7-server-rpms 

WORKDIR /tmp
ENV TOMCAT_VERSION 8.5.23

RUN mkdir /tomcat && \
 wget -q http://www-us.apache.org/dist/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 tar xzvf apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 mv apache-tomcat-${TOMCAT_VERSION}/* /tomcat && \
 rm -rf /tomcat/webapps/examples && \
 rm -rf /tomcat/webapps/docs && \
 cd .. && \
 rm -rf apache-tomcat-${TOMCAT_VERSION}.tar.gz apache-tomcat-${TOMCAT_VERSION}

WORKDIR /tomcat
