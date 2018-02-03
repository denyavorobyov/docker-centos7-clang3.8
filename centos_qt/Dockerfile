FROM apriorit/docker-centos7-clang3.8:clang3.8
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum -y update && yum clean all
# add custom repo
RUN yum -y install p7zip
RUN yum -y install epel-release yum-plugin-copr python-requests
RUN yum install -y protobuf-compiler graphviz libxml2-devel libxslt-devel aria2

#install qt
RUN mkdir /tmp/qt && \
cd /tmp/qt && \
qtbase=5.7.1-0qtbase-Linux-RHEL_6_6-GCC-Linux-RHEL_6_6-X86_64.7z && \
qtcreator=4.5.0-0qtcreator.7z && \
wget http://download.qt.io/online/qtsdkrepository/linux_x64/desktop/qt5_57/qt.57.gcc_64/$qtbase && \
wget http://download.qt.io/online/qtsdkrepository/linux_x64/desktop/tools_qtcreator/qt.tools.qtcreator/$qtcreator && \
7za x -y $qtbase && \
7za x -y $qtcreator && \
mkdir /opt/Qt && \
cp -r ./5.7 /opt/Qt && \
cp -r ./Tools /opt/Qt && \
cd /tmp && \
rm -rf /tmp/qt

RUN export PATH=$PATH:/opt/llvm-3.8.0/bin/ && \
qtBinPath=/opt/Qt/5.7/gcc_64/bin && \
cd $qtBinPath && \
printf "[Paths]\nPrefix=.." >> ./qt.conf && \
creatorBinPath=/opt/Qt/Tools/QtCreator/bin && \
$creatorBinPath/qbs setup-toolchains --detect && \
$creatorBinPath/qbs setup-qt $qtBinPath/qmake QtProfile && \
$creatorBinPath/qbs config profiles.QtProfile.baseProfile clang

RUN yes | cp /opt/Qt/Tools/QtCreator/lib/Qt/lib/*.* /usr/lib64/
