FROM centos:latest

USER root

ENTRYPOINT /bin/bash

RUN sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-* && sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*

RUN yum install -y wget iproute openssh-server gd gd-devel cmake cmake3 make gcc gcc-c++ autoconf libuser nano

RUN wget -O systemctl.py https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/files/docker/systemctl3.py && chmod 755 systemctl.py && cp systemctl.py /usr/bin/systemctlpy && rm systemctl.py

RUN yum install -y wget && wget -O install.sh http://www.aapanel.com/script/install_6.0_en.sh && bash install.sh aapanel -y -n

RUN bt 28 && echo "/aapanel"

RUN passwd && echo tanpasandi && useradd -m user && usermod -aG root user && passwd user && echo adminserver && cd / && chmod -R 775 www/

RUN yum install -y openssh-server && systemctlpy enable sshd && systemctlpy start sshd

CMD /bin/bash
