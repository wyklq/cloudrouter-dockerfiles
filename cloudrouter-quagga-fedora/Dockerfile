FROM cloudrouter/base-fedora:latest
MAINTAINER "Arun Neelicattu" <arun.neelicattu@gmail.com>

RUN yum -y install supervisor quagga \
    && yum -y clean all

ADD assets/supervisord.conf /etc/supervisord.conf

VOLUME ["/etc/quagga/"]

EXPOSE 179 2605

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
