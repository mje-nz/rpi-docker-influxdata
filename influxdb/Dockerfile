FROM resin/raspberrypi3-buildpack-deps:jessie-curl

RUN gpg \
    --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

ENV INFLUXDB_VERSION 1.2.4
RUN wget -q https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_armhf.deb.asc && \
    wget -q https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_armhf.deb && \
    gpg --batch --verify influxdb_${INFLUXDB_VERSION}_armhf.deb.asc influxdb_${INFLUXDB_VERSION}_armhf.deb && \
    dpkg -i influxdb_${INFLUXDB_VERSION}_armhf.deb && \
    rm -f influxdb_${INFLUXDB_VERSION}_armhf.deb*
COPY influxdb.conf /etc/influxdb/influxdb.conf

EXPOSE 8086

VOLUME /var/lib/influxdb

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["influxd"]
