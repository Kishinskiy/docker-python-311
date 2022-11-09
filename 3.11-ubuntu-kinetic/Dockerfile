FROM ubuntu:kinetic as build
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gzip \
    libbz2-1.0 \
    libc6 \
    libcom-err2 \
    libcrypt1 \
    libgssapi-krb5-2 \
    libk5crypto3 \
    libkeyutils1 \
    libkrb5-3 \
    libkrb5support0 \
    liblzma5 \
    libncursesw6 \
    libnsl2 \
    libreadline8 \
    libsqlite3-0 \
    libsqlite3-dev \
    libssl-dev \
    libtinfo6 \
    libtirpc3 \
    zlib1g-dev\
    openssl \
    tar \
    unzip \
    wget \
    zlib1g
WORKDIR /build
RUN wget --no-check-certificate https://www.python.org/ftp/python/3.11.0/Python-3.11.0.tgz && tar -xvf Python-3.11.0.tgz
RUN cd Python-3.11.0 && ./configure \
    --prefix=/opt/python311 \
    --enable-optimizations \
    && make -j$(nproc --all) && make install

FROM ubuntu:kinetic
COPY --from=build /opt/python311 /opt/python311
ENV PATH=/opt/python311/bin:$PATH
RUN apt-get update && apt-get install openssl -y
CMD python3 --version
