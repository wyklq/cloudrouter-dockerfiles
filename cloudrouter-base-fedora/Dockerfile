FROM fedora:20
MAINTAINER "Arun Neelicattu" <abn@iix.net>

RUN yum -y install deltarpm
RUN yum -y update
RUN yum -y install \
    https://repo.cloudrouter.org/beta/x86_64/cloudrouter-release-latest.noarch.rpm
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CLOUDROUTER
RUN yum -y clean all

# Install any additional stuff required
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/common.sh \
    | bash
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/fedora.sh \
    | bash

ONBUILD RUN yum -y update && yum -y clean all
