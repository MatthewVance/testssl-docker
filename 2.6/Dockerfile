FROM debian:jessie
MAINTAINER Matthew Vance

# Install the necessary tools
RUN set -x \
  && apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
  && rm -rf /var/lib/apt/lists/* \

# Build OpenSSL with additional ciphers and vulnerable protocols so testssl.sh
# can perform more comprehensive testing
ENV OPENSSL_VERSION 1.0.2-chacha
ENV OPENSSL_DOWNLOAD_URL https://github.com/PeterMosmans/openssl/archive/1.0.2-chacha.tar.gz
ENV OPENSSL_DOWNLOAD_SHA1 9bf6c245fcf97b3d2ea90a5cff5e771193c0d6cb

RUN buildDeps='gcc libc6-dev make perl zlib1g-dev' \
  && set -x \
  && apt-get update && apt-get install -y --no-install-recommends \
    $buildDeps \
  && rm -rf /var/lib/apt/lists/* \
	&& curl -sSL "$OPENSSL_DOWNLOAD_URL" -o  openssl.tar.gz \
	&& echo "$OPENSSL_DOWNLOAD_SHA1 *openssl.tar.gz" | sha1sum -c - \
	&& mkdir -p /usr/src/openssl \
	&& tar -xzf openssl.tar.gz -C /usr/src/openssl --strip-components=1 \
	&& rm openssl.tar.gz \
	&& cd /usr/src/openssl \
	&& ./config --openssldir=/usr/local/ssl enable-zlib enable-ssl2 \
	enable-rc5 enable-rc2 enable-GOST enable-cms enable-md2 enable-mdc2 enable-ec \
	enable-ec2m enable-ecdh enable-ecdsa enable-seed enable-camellia enable-idea \
	enable-rfc3779 enable-ec_nistp_64_gcc_128 -static experimental-jpake \
	-DOPENSSL_USE_BUILD_DATE \
	&& make -C /usr/src/openssl depend \
	&& make -C /usr/src/openssl \
	&& make -C /usr/src/openssl report \
	&& make -C /usr/src/openssl install \
	&& rm -r /usr/src/openssl \
	&& apt-get purge -y --auto-remove $buildDeps

# Install testssl.sh script
ENV TESTSSL_VERSION 2.6
ENV TESTSSL_DOWNLOAD_URL https://github.com/drwetter/testssl.sh/archive/v2.6.tar.gz
ENV TESTSSL_DOWNLOAD_SHA1 55fdfbd4321026e608cb5568ed27ac2f2832da8f

# Upstream tarball includes ./testssl.sh-{$TESTSSL_VERSION}/ so we end up with /usr/local/bin/testssl.sh-{$TESTSSL_VERSION}/
RUN set -x \
	&& curl -sSL "$TESTSSL_DOWNLOAD_URL" -o  testssl.tar.gz \
	&& echo "$TESTSSL_DOWNLOAD_SHA1 *testssl.tar.gz" | sha1sum -c - \
	&& mkdir -p /usr/local/bin/testssl \
	&& tar -xzf testssl.tar.gz -C /usr/local/bin/testssl --strip-components=1 \
	&& rm testssl.tar.gz \
	&& chmod +x /usr/local/bin/testssl/testssl.sh

ENV PATH /usr/local/bin/testssl:$PATH
ENTRYPOINT ["testssl.sh"]
CMD ["--help"]
