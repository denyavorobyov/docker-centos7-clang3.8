FROM centos:7
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum -y update && yum clean all
# add custom repo
RUN yum -y install epel-release yum-plugin-copr python-requests
RUN yum install -y protobuf-compiler graphviz libxml2-devel libxslt-devel aria2

#install qt
COPY resources /srv/resources
RUN mkdir /tmp/qt && \
cd /tmp/qt && \
aria2c http://download.qt.io/official_releases/qt/5.7/5.7.1/qt-opensource-linux-x64-5.7.1.run.meta4 && \
chmod +x ./qt-opensource-linux-x64-5.7.1.run && \
./qt-opensource-linux-x64-5.7.1.run --script /srv/resources/qt-installer-noninteractive.qs -platform minimal && \
rm -rf /tmp/qt

RUN /opt/Qt5.7.1/Tools/QtCreator/bin/qbs setup-toolchains --detect && \
/opt/Qt5.7.1/Tools/QtCreator/bin/qbs setup-qt '/opt/Qt5.7.1/5.7/gcc_64/bin/qmake' QtProfile && \
/opt/Qt5.7.1/Tools/QtCreator/bin/qbs config profiles.QtProfile.baseProfile clang

RUN yes | cp /opt/Qt5.7.1/5.7/gcc_64/lib/*.* /usr/lib64/
