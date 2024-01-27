FROM base_image:1.0

ARG CHROMIUM_VERSION=120.0.6099.224-1~deb11u1_arm64

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    gconf-service \
    libasound2 \
    libatomic1 \
    libdouble-conversion3 \
    libevent-2.1-7 \
    libgcc-s1 \
    libgbm1 \
    libatk1.0-0 \
    libxslt1.1 \
    libre2-9 \
    libminizip1 \
    libopenjp2-7 \
    libsnappy1v5 \
    libstdc++6 \
    libwebpdemux2 \
    libwebpmux3 \
    libwoff1 \
    libxnvctrl0 \
    libxslt1.1 \
    libc6 \
    libcairo2 \
    libcups2 \
    libdbus-1-3 \
    libexpat1 \
    libfontconfig1 \
    libfreetype6 \
    libgcc1 \
    libgconf-2-4 \
    libgdk-pixbuf2.0-0 \
    libglib2.0-0 \
    libgtk2.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libnss3 \
    libpango1.0-0 \
    libstdc++6 \
    libx11-6 \
    zlib1g \
    libx11-xcb1 \
    libxcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    ca-certificates \
    fonts-liberation \
    libappindicator3-1 \
    libnss3 \
    lsb-base \
    x11-utils \
    xdg-utils \
    libcurl4 \
    iproute2 \
    chromium-chromedriver && \
    curl -o libjsoncpp.deb http://ftp.de.debian.org/debian/pool/main/libj/libjsoncpp/libjsoncpp24_1.9.4-4_arm64.deb && \
    curl -o libwebp6.deb http://security.debian.org/debian-security/pool/updates/main/libw/libwebp/libwebp6_0.6.1-2.1+deb11u2_arm64.deb && \
    curl -o libjpeg.deb http://ftp.de.debian.org/debian/pool/main/libj/libjpeg-turbo/libjpeg62-turbo_1.5.2-2+deb10u1_arm64.deb && \
    curl -o chromiumcommon.deb http://security.debian.org/debian-security/pool/updates/main/c/chromium/chromium-common_${CHROMIUM_VERSION}.deb && \
    curl -o chromium-browser.deb http://security.debian.org/debian-security/pool/updates/main/c/chromium/chromium_${CHROMIUM_VERSION}.deb && \
    dpkg -i libjpeg.deb && \
    dpkg -i libjsoncpp.deb && \
    dpkg -i chromiumcommon.deb && \
    dpkg -i libwebp6.deb && \
    dpkg -i chromium-browser.deb && \
    rm -rf /tmp/* && rm -rf /var/lib/apt/lists/* && \
    apt-get clean && apt-get autoremove -y && \
    rm -f libjsoncpp.deb libwebp6.deb libjpeg.deb chromiumcommon.deb chromium-browser.deb

ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

COPY chromedriver /usr/bin/
COPY entrypoint.sh /

RUN chmod +x /usr/bin/chromedriver && \
    chmod +x /entrypoint.sh && \
    echo "cookie-file = ~/.config/pulse/cookie" >> /etc/pulse/client.conf

USER selenium

EXPOSE 4444 5900

ENTRYPOINT ["/entrypoint.sh"]