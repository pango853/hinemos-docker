# 1. Install and get files with CentOS 7
FROM centos:7.7.1908 AS install-env
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

ARG LANGUAGE=en

# Install dependencies
RUN yum install -y vim-common
# Install package
RUN LANGUAGE=${LANGUAGE} rpm -ivh https://github.com/hinemos/hinemos/releases/download/v6.2.2/hinemos-6.2-manager-6.2.2-1.el7.x86_64.rpm


## Build runtime with CentOS 7
FROM centos:7.7.1908
LABEL maintainer="Pango Chan <Pango853@gmail.com>"

RUN groupadd -g 1000 hinemos && useradd -m -u 1000 -g hinemos hinemos
USER hinemos

WORKDIR /opt
COPY --from=install-env /opt/hinemos hinemos

ENTRYPOINT ["/opt/hinemos/postgresql/bin/postgres", "-D", "/opt/hinemos/var/data"]

