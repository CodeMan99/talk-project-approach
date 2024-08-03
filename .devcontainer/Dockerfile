ARG VARIANT=20-bookworm
FROM mcr.microsoft.com/devcontainers/javascript-node:1-${VARIANT}

RUN apt-get -y update \
 && DEBIAN_FRONTEND=noninteractive apt-get -y install \
      aspell \
      inetutils-ping \
      moreutils \
 && rm -rf /var/lib/apt/lists/*

RUN su node -c "npm install -g imagemin-cli imagemin-pngquant"
