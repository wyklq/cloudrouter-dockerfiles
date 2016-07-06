FROM fedora:latest
MAINTAINER "Arun Neelicattu" <arun.neelicattu@gmail.com>

# configure osv vars
ENV OSV_REPO=https://github.com/cloudius-systems/osv.git
ENV OSV_VERSION=0.19
ENV OSV_DIR=/osv

# configure proxy
ENV http_proxy=http://10.10.10.10:8080
ENV https_proxy=http://10.10.10.10:8080

# install vbox repo
ENV VBOX_REPO=http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo
RUN curl -o /etc/yum.repos.d/$(basename ${VBOX_REPO}) ${VBOX_REPO}


# install CloudRouter repo
RUN dnf -y install \
    https://repo.cloudrouter.org/3/fedora/23/x86_64/cloudrouter-fedora-repo-latest.noarch.rpm

# do an update for sanity
RUN dnf clean packages; dnf -y update
# instal build dependencies
RUN dnf -y install \
    git wget zip unzip tar patch

# install VirtualBox
RUN dnf -y install \
    VirtualBox-5.0

# install Capstan
ENV CAPSTAN_ROOT=/capstan-repository
RUN dnf -y install \
    capstan

# fetch and setup OSV_REPO branch for master branch
RUN git clone ${OSV_REPO} ${OSV_DIR}
RUN cd ${OSV_DIR} && git submodule update --init --recursive

# add assets
ADD ./assets/osv /usr/bin/osv
ADD ./assets/patches ${OSV_DIR}/patches

WORKDIR ${OSV_DIR}

# apply patches
RUN find ${OSV_DIR}/patches -maxdepth 1 -type f -name "*.patch" \
    -exec bash -c "patch -p1 < {}" \;

# setup system
RUN cd ${OSV_DIR} && ./scripts/setup.py

# clean up
RUN dnf -y clean all

VOLUME ["/osv", "/osv/build/", "/osv/apps/", "/osv/images/", "/capstan-repository"]

CMD ["/usr/bin/bash"]
