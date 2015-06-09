FROM fedora:latest
MAINTAINER "David Jorm" <djorm@iix.net>

RUN yum -y update
RUN yum -y install https://cloudrouter.org/repo/1/x86_64/onos-1.2.0-1.noarch.rpm
RUN yum clean all

# expose ports as listed at http://sdnhub.org/tutorials/onos/
EXPOSE 8181 6633 6635

ENV JAVA_HOME /usr/lib/jvm/java
ENV KARAF_DIR=/opt/onos/apache-karaf-3.0.3
WORKDIR ${KARAF_DIR}
CMD ["./bin/karaf" , "clean"]
