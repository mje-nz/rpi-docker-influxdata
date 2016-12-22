FROM resin/raspberrypi3-buildpack-deps:jessie-curl

RUN gpg \
    --keyserver hkp://ha.pool.sks-keyservers.net \
    --recv-keys 05CE15085FC09D18E99EFB22684A14CF2582E0C5

ENV TELEGRAF_VERSION 1.1.2
RUN wget -q https://dl.influxdata.com/telegraf/releases/telegraf_${TELEGRAF_VERSION}_armhf.deb.asc && \
    wget -q https://dl.influxdata.com/telegraf/releases/telegraf_${TELEGRAF_VERSION}_armhf.deb && \
    gpg --batch --verify telegraf_${TELEGRAF_VERSION}_armhf.deb.asc telegraf_${TELEGRAF_VERSION}_armhf.deb && \
    dpkg -i telegraf_${TELEGRAF_VERSION}_armhf.deb && \
    rm -f telegraf_${TELEGRAF_VERSION}_armhf.deb*

EXPOSE 8125/udp 8092/udp 8094

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["telegraf"]
