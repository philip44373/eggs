/bin/bash -c #(nop) CMD ["/bin/bash" "/entrypoint.sh"]
/bin/bash -c #(nop) COPY file:e66b09c047c4b6b6625f3480964eb434bb9cf4b17f659d3e8363dea2a48f32d6 in /entrypoint.sh
/bin/bash -c #(nop) WORKDIR /home/container
/bin/bash -c #(nop) ENV HOME=/home/container
/bin/bash -c #(nop) ENV USER=container
/bin/bash -c #(nop) USER container
/bin/bash -c apt clean && rm -rf /var/cache/apt/archives && rm -rf /var/lib/apt/lists/*
/bin/bash -c chmod +x /start.sh
/bin/bash -c #(nop) COPY file:ea436d3d3b792cc4f9d36b14833c2398b1b9b443a38bc883fca01613a3b9d6fd in /start.sh
/bin/bash -c apt-get update && apt-get -y install dnsutils python3 build-essential
/bin/bash -c npm install -g coffeescript typescript node-gyp
/bin/bash -c npm install -g nodemon && nodemon -v
/bin/bash -c ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
/bin/bash -c #(nop) ENV TZ=UTC
/bin/bash -c #(nop) ENV LANG=en_US.UTF-8
/bin/bash -c locale-gen en_US.UTF-8
/bin/bash -c apt-get update && apt-get upgrade -y && apt-get -y install iptables apt-utils curl ffmpeg software-properties-common apt-transport-https ca-certificates wget dirmngr gnupg iproute2 youtube-dl sqlite3 libopus0 make g++ locales git cmake zip unzip libtool-bin autoconf automake curl jq && useradd -d /home/container -m container
/bin/bash -c #(nop) SHELL [/bin/bash -c]
ENV DEBIAN_FRONTEND=noninteractive
CMD ["node"]
ENTRYPOINT ["docker-entrypoint.sh"]
COPY file:4d192565a7220e135cab6c77fbc1c73211b69f3d9fb37e62857b2c6eb9363d51 in /usr/local/bin/
RUN set -ex && savedAptMark="$(apt-mark showmanual)" && apt-get update && apt-get install -y ca-certificates curl wget gnupg dirmngr --no-install-recommends && rm -rf /var/lib/apt/lists/* && for key in 6A010C5166006599AA17F08146C2130DFD2497F5 ; do gpg --batch --keyserver hkps://keys.openpgp.org --recv-keys "$key" || gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "$key" ; done && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz.asc" && gpg --batch --verify yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz && mkdir -p /opt && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg && rm yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz && apt-mark auto '.*' > /dev/null && { [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark > /dev/null; } && find /usr/local -type f -executable -exec ldd '{}' ';' | awk '/=>/ { print $(NF-1) }' | sort -u | xargs -r dpkg-query --search | cut -d: -f1 | sort -u | xargs -r apt-mark manual && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false && yarn --version
ENV YARN_VERSION=1.22.19
RUN ARCH= && dpkgArch="$(dpkg --print-architecture)" && case "${dpkgArch##*-}" in amd64) ARCH='x64';; ppc64el) ARCH='ppc64le';; s390x) ARCH='s390x';; arm64) ARCH='arm64';; armhf) ARCH='armv7l';; i386) ARCH='x86';; *) echo "unsupported architecture"; exit 1 ;; esac && set -ex && apt-get update && apt-get install -y ca-certificates curl wget gnupg dirmngr xz-utils libatomic1 --no-install-recommends && rm -rf /var/lib/apt/lists/* && for key in 4ED778F539E3634C779C87C6D7062848A1AB005C 141F07595B7B3FFE74309A937405533BE57C7D57 74F12602B6F1C4E913FAA37AD3A89613643B6201 61FC681DFB92A079F1685E77973F295594EC4689 8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 890C08DB8579162FEE0DF9DB8BEAB4DFCF555EF4 C82FA3AE1CBEDC6BE46B9360C43CEC45C17AB93C 108F52B48DB57BB0CC439B2997B01419BD92F80A ; do gpg --batch --keyserver hkps://keys.openpgp.org --recv-keys "$key" || gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "$key" ; done && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc && grep " node-v$NODE_VERSION-linux-$ARCH.tar.xz\$" SHASUMS256.txt | sha256sum -c - && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt && apt-mark auto '.*' > /dev/null && find /usr/local -type f -executable -exec ldd '{}' ';' | awk '/=>/ { print $(NF-1) }' | sort -u | xargs -r dpkg-query --search | cut -d: -f1 | sort -u | xargs -r apt-mark manual && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false && ln -s /usr/local/bin/node /usr/local/bin/nodejs && node --version && npm --version
ENV NODE_VERSION=16.18.0
RUN groupadd --gid 1000 node && useradd --uid 1000 --gid node --shell /bin/bash --create-home node
CMD ["bash"]
ADD file:14c4aa7a136ce9eb1fae0ba0f394509990d44126be801a2713cf8722fbb2e6b9 in /