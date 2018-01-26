FROM centos:7
MAINTAINER kotik <obrbkru@apriorit.com>

RUN yum install -y cmake3 cmake wget

#build install clang 3.8.0
RUN yum -y install epel-release yum-plugin-copr python-requests &&\
yum copr enable -y alonid/llvm-3.8.0 && \
yum install -y clang-3.8.0 && \
yum install -y clang-3.8.0-devel.x86_64 && \
export PATH=$PATH:/opt/llvm-3.8.0/bin/

#building and installing of clang c++ library for better c++11 support
# http://stackoverflow.com/questions/25840088/how-to-build-libcxx-and-libcxxabi-by-clang-on-centos-7/25840107#25840107
# use "one command" style because of Docker copypaste convenience
#*******************************************
RUN libcxx="libcxx-3.8.1.src" && \
libcxxabi="libcxxabi-3.8.1.src" && \
tmp="tmpDirectory" && \
pwd && \
wget "http://llvm.org/releases/3.8.1/$libcxx.tar.xz" && \
tar xf "$libcxx.tar.xz" && \
cd $libcxx && \
pwd && \
mkdir $tmp && \
cd $tmp && \
pwd && \
ls -l && \
cmake3 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_C_COMPILER=/usr/bin/clang -DCMAKE_CXX_COMPILER=/usr/bin/clang++ .. && \
make install && \
ln -s /usr/lib/libc++.so.1 /lib64 && \
cd .. && \
rm $tmp -rf && \
cd .. && \
wget "http://llvm.org/releases/3.8.1/$libcxxabi.tar.xz" && \
tar xf "$libcxxabi.tar.xz" && \
cd $libcxxabi && \
mkdir $tmp && \
cd $tmp && \
cmake3 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_C_COMPILER=/usr/bin/clang -DCMAKE_CXX_COMPILER=/usr/bin/clang++ -DCMAKE_CXX_FLAGS="-std=c++11" -DLIBCXXABI_LIBCXX_INCLUDES=../../$libcxx/include .. && \
make install && \
ln -s /usr/lib/libc++abi.so.1 /lib64 && \
cd ../.. && \
cd $libcxx && \
mkdir $tmp && \
cd $tmp && \
cmake3 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_C_COMPILER=/usr/bin/clang -DCMAKE_CXX_COMPILER=/usr/bin/clang++ -DLIBCXX_CXX_ABI=libcxxabi -DLIBCXX_CXX_ABI_INCLUDE_PATHS=../../$libcxxabi/include .. && \
make install && \
cd ../.. && \
rm -rf $libcxx $libcxxabi
#*******************************************