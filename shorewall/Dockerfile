# shorewall in a container
#
# docker run --rm -it \
# 	--net host \
# 	--cap-add NET_ADMIN \
#	--privileged \
# 	jess/shorewall
#
FROM alpine:3.18.3
MAINTAINER Jessica Frazelle <jess@docker.com>

RUN apk --no-cache add \
	shorewall \
	&& touch /var/log/messages

COPY ./etc /etc/shorewall

ENTRYPOINT [ "/usr/sbin/shorewall" ]
