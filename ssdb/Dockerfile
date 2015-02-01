FROM ubuntu

# Set the env variable DEBIAN_FRONTEND to noninteractive
ENV DEBIAN_FRONTEND noninteractive

ENV SSDB_TAG stable-1.8.0

RUN mkdir -p /ssdb/bin /ssdb/data/var && \
  apt-get update && \
  apt-get install -y --force-yes git make gcc g++ && apt-get clean && \
  git clone --depth 1 --branch $SSDB_TAG https://github.com/ideawu/ssdb.git src && \
  cd src && make && make install && cp ssdb-server /ssdb/bin && \
  apt-get remove -y --force-yes git make gcc g++ && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* src

EXPOSE 8888

ENTRYPOINT /ssdb/bin/ssdb-server /ssdb/data/ssdb.conf