# htop in a container
#
# docker run --rm -it \
# 	--pid host \
# 	jess/htop
#
FROM alpine:3.18.3
MAINTAINER Jessica Frazelle <jess@docker.com>

RUN apk --no-cache add \
	htop

CMD [ "htop" ]
