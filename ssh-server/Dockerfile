FROM ubuntu:16.04
MAINTAINER buktsa@hotmail.com

# Installing required software
FROM ubuntu:16.04
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y openssh-server
RUN apt-get install -y vim

RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# Making a folder that we will map from outside
RUN mkdir -p /data
RUN chown -R root:root /data

VOLUME /data
                      
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]