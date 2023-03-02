ARG BUILD_FROM
FROM $BUILD_FROM

MAINTAINER Matt Longman <git@mattlongman.com>

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV LANG C.UTF-8

RUN apk update && \
apk add --no-cache bash jq iw networkmanager networkmanager-cli net-tools sudo dnsmasq git build-essential && \
rm -rf /var/cache/apk/* && \
git clone https://github.com/jenssegers/RTL8188-hostapd && \
cd RTL8188-hostapd/hostapd && \
make && \
make install && \
cd ../wpa_supplicant && \
make && \
make install

COPY hostapd.conf /
COPY dnsmasq.conf /

COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
