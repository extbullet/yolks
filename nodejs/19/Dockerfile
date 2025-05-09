FROM        --platform=$TARGETOS/$TARGETARCH node:19-bullseye-slim

LABEL       author="Michael Parker" maintainer="parker@pterodactyl.io"

# add container user and set stop signal
RUN         useradd -m -d /home/container container
STOPSIGNAL  SIGINT

RUN         apt update \
            && apt -y install \
                ffmpeg \
                iproute2 \
                git \
                sqlite3 \
                libsqlite3-dev \
                python3 \
                python3-dev \
                ca-certificates \
                dnsutils \
                tzdata \
                zip \
                tar \
                curl \
                build-essential \
                libtool \
                iputils-ping \
                libnss3 \
                tini \
				libatk-bridge2.0-0 \
				libatk1.0-0 \
				libxcb1 \
				libxcomposite1 \
				libxdamage1 \
				libxfixes3 \
				libxrandr2 \
				libgbm1 \
				libasound2 \
				libpangocairo-1.0-0 \
				libpango-1.0-0 \
				libcairo2 \
				libx11-xcb1 \
				libnss3 \
				libxss1 \
				libxtst6 \
				fonts-liberation \
				libappindicator3-1 \
				libdrm2 \
				libnspr4 \
				libxext6 \
				lsb-release \
				wget \
				xdg-utils

RUN         npm install --global npm@9.x.x typescript ts-node @types/node

# install pnpm
RUN         npm install -g corepack
RUN         corepack enable
RUN         corepack prepare pnpm@latest --activate

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
