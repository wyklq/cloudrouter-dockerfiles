FROM centos:latest
MAINTAINER "Arun Neelicattu" <arun.neelicattu@gmail.com>

RUN yum -y install \
    deltarpm \
    epel-release curl
RUN yum -y update
RUN yum -y swap -- remove centos-release* -- install https://repo.cloudrouter.org/1/x86_64/cloudrouter-release-centos-latest.noarch.rpm
RUN find /etc/pki/rpm-gpg/ -maxdepth 1 -type f -name 'RPM-GPG-KEY-cloudrouter*' \
    -exec rpm --import {} \;
RUN yum -y clean all

# Install any additional stuff required
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/common.sh \
    | bash
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/centos.sh \
    | bash

ONBUILD RUN yum -y update && yum -y clean all
