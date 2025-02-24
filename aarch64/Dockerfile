FROM quay.io/pypa/manylinux_2_34_aarch64:latest

RUN yum install -y openblas*  && yum groupinstall -y 'Development Tools'
RUN yum install -y wget

RUN wget https://github.com/uxlfoundation/oneTBB/archive/refs/tags/v2022.0.0.tar.gz && \
tar -zvxf v2022.0.0.tar.gz && cd oneTBB-2022.0.0/ && mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local/tbb -DTBB_TEST=OFF .. && \
cmake --build . && cmake --install . && cd / && rm -rf /root/oneTBB-2022.0.0*
