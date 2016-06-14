FROM ubuntu:14.04

EXPOSE 8080
VOLUME /opt/my-app/data

# RUN locale-gen en_US.UTF-8
# ENV LANG en_US.UTF-8

RUN apt-get update
RUN apt-get -y upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install my-stuff

COPY my-app.sh /opt/my-app/


# For development only
RUN apt-get update && apt-get install -y openssh-server mc
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
EXPOSE 22

ENTRYPOINT ["/usr/sbin/sshd", "-D"]

# ENTRYPOINT ["/opt/my-app/my-app"]