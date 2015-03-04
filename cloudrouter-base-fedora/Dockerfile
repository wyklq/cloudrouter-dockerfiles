FROM fedora:20
MAINTAINER "Arun Neelicattu" <abn@iix.net>

# Install any additional stuff required
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/common.sh \
    | bash
RUN curl --silent \
    https://raw.githubusercontent.com/iixlabs/cloudrouter/master/build/images/scripts/fedora.sh \
    | bash

RUN yum -y install \
    deltarpm \
    https://cloudrouter.org/repo/beta/x86_64/cloudrouter-release-latest.noarch.rpm
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CLOUDROUTER
RUN yum -y clean all

ONBUILD RUN yum -y update && yum -y clean all
