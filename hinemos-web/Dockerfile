# 1. Install and get files with CentOS 7
FROM centos:7.7.1908 AS install-env
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

# Install dependencies
RUN yum install -y unzip
# Install package
RUN rpm -ivh https://github.com/hinemos/hinemos/releases/download/v6.2.2/hinemos-6.2-web-6.2.2-1.el7.x86_64.rpm
RUN sed -iBAK 's/^\(export JAVA_[A-Z]*HOME=\)/#\1/' /opt/hinemos_web/conf/hinemos_web.cfg
# Turn Cataline to run mode
RUN sed -iBAK 's/catalina.sh start/catalina.sh run/' /opt/hinemos_web/bin/tomcat_start.sh

## Build runtime with OpenJDK 8
FROM openjdk:8-jdk
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

WORKDIR /opt
COPY --from=install-env /opt/hinemos_web hinemos_web

ENV JRE_HOME=/usr/local/openjdk-8
ENV JAVA_HOME=${JRE_HOME}
ENV JAVA_SDK_HOME=${JRE_HOME}

ENTRYPOINT ["/opt/hinemos_web/bin/tomcat_start.sh"]

