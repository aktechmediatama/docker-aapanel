FROM centos:latest

USER root

ENTRYPOINT /bin/bash

RUN sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-* && sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*

RUN yum install -y wget iproute openssh-server gd gd-devel cmake cmake3 make gcc gcc-c++ autoconf libuser passwd nano

RUN rm /usr/bin/systemctl

COPY files/ /tmp/files

RUN chmod -R 755 /tmp/files && cp /tmp/files/systemctl3.py /usr/bin/systemctl

RUN /tmp/files/install.sh aapanel

RUN echo 'tanpasandi' | passwd --stdin root

RUN useradd -m user && usermod -aG root user

RUN echo "adminserver" | passwd --stdin user


RUN yum install -y openssh-server && systemctlpy enable sshd && systemctlpy start sshd

RUN rm -rf /tmp/files

CMD /bin/bash
