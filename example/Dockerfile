FROM registry.access.redhat.com/rhel7-atomic
MAINTAINER Greg Swallow (gswallow@ivytech.edu)

RUN microdnf install java-1.8.0-oracle-devel.x86_64 \
  java-1.8.0-oracle-jdbc.x86_64 \
  apr-devel \
  apr-util-devel \
  openssl-devel \
  gcc \
  gcc-c++ \
  autoconf \
  make \
  cmake \
  which \
  wget \
  ant \
  --enablerepo=rhel-7-server-thirdparty-oracle-java-rpms \
  --enablerepo=rhel-7-server-rpms

ENV TOMCAT_VERSION 8.5.23
ENV CATALINA_HOME /tomcat
ENV TOMCAT_NATIVE_VERSION 1.2.14
ENV TOMCAT_NATIVE_LIBDIR $CATALINA_HOME/native-jni-lib
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH:+$LD_LIBRARY_PATH:}$TOMCAT_NATIVE_LIBDIR
ENV PATH ${PATH}:${CATALINA_HOME}/bin

WORKDIR /tmp

RUN mkdir -p ${CATALINA_HOME} && \
 wget -q http://www-us.apache.org/dist/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 tar xzf apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 mv apache-tomcat-${TOMCAT_VERSION}/* /tomcat && \
 rm -rf /tomcat/webapps/examples && \
 rm -rf /tomcat/webapps/docs && \
 rm -rf apache-tomcat-${TOMCAT_VERSION}.tar.gz apache-tomcat-${TOMCAT_VERSION}

RUN JAVA_HOME=$(alternatives --display java_sdk_1.8.0 | tail -1 | awk '{print $NF}') && \
 export JAVA_HOME=${JAVA_HOME%.} && \
 wget -q http://www-us.apache.org/dist/tomcat/tomcat-connectors/native/${TOMCAT_NATIVE_VERSION}/source/tomcat-native-${TOMCAT_NATIVE_VERSION}-src.tar.gz && \
 tar xzf tomcat-native-${TOMCAT_NATIVE_VERSION}-src.tar.gz && \
 cd tomcat-native-${TOMCAT_NATIVE_VERSION}-src/native && \
 ./configure --libdir=${TOMCAT_NATIVE_LIBDIR} && \
 make && \
 make install && \
 cd /tmp && \
 rm -rf tomcat-native-* 

WORKDIR /tomcat
EXPOSE 8080
CMD ["catalina.sh", "run"]
