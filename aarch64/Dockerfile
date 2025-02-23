FROM quay.io/pypa/manylinux_2_34_aarch64:latest

RUN yum install -y wget && \
yum install -y gmp  gmp-devel  mpfr  mpfr-devel  libmpc  libmpc-devel  && yum install -y kernel-devel kernel-headers
RUN wget https://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-14.2.0/gcc-14.2.0.tar.gz &&  \
tar -zvxf gcc-14.2.0.tar.gz && cd gcc-14.2.0 && mkdir build && cd build && \
../configure --enable-languages=c,c++ --prefix=/usr/local/gcc-14.2.0 --enable-checking=release --disable-bootstrap --disable-multilib && \
make -j$(nproc) && make install &&  cd ../../ && rm -rf gcc-14.2.0
RUN yum install -y openblas* lapack* libomp* && yum groupinstall -y 'Development Tools'
RUN wget https://github.com/uxlfoundation/oneTBB/archive/refs/tags/v2022.0.0.tar.gz && \
tar -zvxf v2022.0.0.tar.gz && cd oneTBB-2022.0.0/ && mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local/tbb -DTBB_TEST=OFF .. && \
cmake --build . && cmake --install . && cd / && rm -rf /root/oneTBB-2022.0.0*
RUN cd /root/ && VERSIONS=("3.9.21" "3.10.16" "3.11.11" "3.12.9" "3.13.2"); BASE_URL="https://www.python.org/ftp/python"; for V in "${VERSIONS[@]}"; do wget "${BASE_URL}/${V}/Python-${V}.tgz" && tar -zxf "Python-${V}.tgz" && cd "Python-${V}" && ./configure --prefix="/opt/_internal/cpython-${V}" --enable-optimizations --enable-shared && make -j$(nproc) && make install && cd ..; done && rm -rf /root/Python*
RUN for V in "3.9.21 3.9" "3.10.16 3.10" "3.11.11 3.11" "3.12.9 3.12" "3.13.2 3.13"; do set -- $V; ln -s "/opt/_internal/cpython-$1/lib/libpython$2.so.1.0" "/lib64/libpython$2.so.1.0"; done
