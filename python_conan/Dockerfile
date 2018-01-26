FROM apriorit/docker-centos7-clang3.8:qt
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum install -y  python-testtools python-pip
RUN yes | pip install checksumdir
RUN yes | pip install conan

#bzip2 need for bulding of boost iostream library
RUN yum -y install bzip2 bzip2-devel