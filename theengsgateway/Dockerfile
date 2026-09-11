ARG BUILD_FROM
FROM $BUILD_FROM
LABEL io.hass.version="1.11.5" io.hass.type="addon" io.hass.arch="armv7|armhf|aarch64|i386|amd64"
RUN echo -e "Acquire::Check-Valid-Time \"false\";\nAcquire::Check-Date \"false\";" > /etc/apt/apt.conf.d/99no-check-valid-time && \
    sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
    sed -i 's|security.debian.org/debian-security|archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    sed -i '/debian-security/s/bullseye\/updates/bullseye-security/g' /etc/apt/sources.list || true && \
    apt-get update && \
    apt-get install --no-install-recommends -y build-essential bluez python3-pip python3-dev && \
    pip3 install --extra-index-url=https://www.piwheels.org/simple TheengsGateway==1.7.5
ENV current /root
ENV HOME $current
WORKDIR $current
COPY run.sh /root
COPY entrypoint.sh /root
RUN chmod a+x /root/run.sh
RUN chmod a+x /root/entrypoint.sh
ENTRYPOINT ["/root/entrypoint.sh"]
CMD [ "/root/run.sh" ]
