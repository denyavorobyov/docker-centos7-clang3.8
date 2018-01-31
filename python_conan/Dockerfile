FROM apriorit/docker-centos7-clang3.8:qt5.10
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum install -y perl
RUN yum install -y libtool
RUN yum install -y python-testtools python-pip
RUN yes | pip install checksumdir
RUN yes | pip install conan==0.28.1

#bzip2 need for bulding of boost iostream library
RUN yum -y install bzip2 bzip2-devel
