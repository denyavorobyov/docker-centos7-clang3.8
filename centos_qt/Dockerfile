FROM apriorit/docker-centos7-clang3.8:clang3.8
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum -y update && yum clean all
# add custom repo
RUN yum -y install epel-release yum-plugin-copr python-requests
RUN yum install -y protobuf-compiler graphviz libxml2-devel libxslt-devel aria2

#install qt
COPY resources /srv/resources
RUN mkdir /tmp/qt && \
cd /tmp/qt && \
aria2c http://download.qt.io/official_releases/qt/5.10/5.10.0/qt-opensource-linux-x64-5.10.0.run.meta4 && \
chmod +x ./qt-opensource-linux-x64-5.10.0.run && \
./qt-opensource-linux-x64-5.10.0.run --script /srv/resources/qt-installer-noninteractive.qs -platform minimal && \
rm -rf /tmp/qt

RUN export PATH=$PATH:/opt/llvm-3.8.0/bin/ && \
/opt/Qt5.10.0/Tools/QtCreator/bin/qbs setup-toolchains --detect && \
/opt/Qt5.10.0/Tools/QtCreator/bin/qbs setup-qt '/opt/Qt5.10.0/5.5.10.0/gcc_64/bin/qmake' QtProfile && \
/opt/Qt5.10.0/Tools/QtCreator/bin/qbs config profiles.QtProfile.baseProfile clang

RUN yes | cp /opt/Qt5.10.0/5.10.0/gcc_64/lib/*.* /usr/lib64/
