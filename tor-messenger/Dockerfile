# Run tor messenger in a container
#
# docker run -d \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	tor-messenger
#

FROM debian:sid
MAINTAINER Christian Koep <christian.koep@fom-net.de>

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /home/user
ENV LANG C.UTF-8
ENV TOR_VERSION 0.1.0b3
ENV TOR_FINGERPRINT 0x6887935AB297B391

RUN apt-get update && apt-get -y --no-install-recommends install \
	curl \
	tar \
	xz-utils \
	zenity \
	gxmessage \
	ca-certificates \
	libasound2 \
	libdbus-glib-1-2 \
	libxt6 && \
	rm -rf /var/lib/apt/lists/*

RUN useradd --create-home --home-dir $HOME user && chown -R user:user $HOME

RUN cd /tmp && \
	curl -sSOL https://dist.torproject.org/tormessenger/${TOR_VERSION}/tor-messenger-linux64-${TOR_VERSION}_en-US.tar.xz && \
	curl -sSOL https://dist.torproject.org/tormessenger/${TOR_VERSION}/sha256sums.txt && \
	curl -sSOL https://dist.torproject.org/tormessenger/${TOR_VERSION}/sha256sums.txt.asc && \
	mkdir ~/.gnupg && \
	gpg --keyserver x-hkp://keys.gnupg.net --recv-keys ${TOR_FINGERPRINT} || \
	gpg --fingerprint ${TOR_FINGERPRINT} | grep "Key fingerprint = 3A0B 3D84 3708 9613 6B84	5E82 6887 935A B297 B391" && \
	gpg --verify sha256sums.txt.asc && \
	grep $(sha256sum tor-messenger-linux64-${TOR_VERSION}_en-US.tar.xz) sha256sums.txt && \
	tar xfv tor-messenger-linux64-${TOR_VERSION}_en-US.tar.xz -C /usr/local/bin && \
	rm -rf tor-messenger*	&& \
	chown -R user.user /usr/local/bin/tor-messenger && \
	rm -rf ~/.gnupg

WORKDIR $HOME

USER user

CMD ["/usr/local/bin/tor-messenger/Messenger/start-tor-messenger", "--verbose"]