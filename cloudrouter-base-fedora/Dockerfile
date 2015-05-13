FROM fedora:20
MAINTAINER "Arun Neelicattu" <abn@iix.net>

RUN yum -y install deltarpm
RUN yum -y update
RUN yum -y swap -- remove fedora-release* -- install https://repo.cloudrouter.org/beta/x86_64/cloudrouter-release-fedora-latest.noarch.rpm
RUN find /etc/pki/rpm-gpg/ -maxdepth 1 -type f -name 'RPM-GPG-KEY-CLOUDROUTER*' \
    -exec rpm --import {} \;
RUN yum -y clean all

# Install any additional stuff required
RUN curl --silent \
    https://raw.githubusercontent.com/cloudrouter/cloudrouter/master/build/images/scripts/common.sh \
    | bash
RUN curl --silent \
    https://raw.githubusercontent.com/cloudrouter/cloudrouter/master/build/images/scripts/fedora.sh \
    | bash

ONBUILD RUN yum -y update && yum -y clean all
