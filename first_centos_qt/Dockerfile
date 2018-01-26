FROM centos:7
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum -y update && yum clean all
RUN yum install -y protobuf-compiler graphviz libxml2-devel libxslt-devel wget

#install qt
RUN mkdir /tmp/qt && \
cd /tmp/qt && \
wget -q http://download.qt.io/archive/qt/5.7/5.7.1/qt-opensource-linux-x64-5.7.1.run 

COPY resources /srv/resources
RUN chmod +x ./qt-opensource-linux-x64-5.7.1.run
RUN ./qt-opensource-linux-x64-5.7.1.run --script /srv/resources/qt-installer-noninteractive.qs -platform minimal

RUN /opt/Qt5.7.1/Tools/QtCreator/bin/qbs setup-toolchains --detect 
RUN /opt/Qt5.7.1/Tools/QtCreator/bin/qbs setup-qt '/opt/Qt5.7.1/5.7/gcc_64/bin/qmake' QtProfile
RUN /opt/Qt5.7.1/Tools/QtCreator/bin/qbs config profiles.QtProfile.baseProfile clang
RUN yes | cp /opt/Qt5.7.1/5.7/gcc_64/lib/*.* /usr/lib64/
RUN rm -rf /tmp/qt
