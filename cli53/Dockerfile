FROM alpine:3.18.5

RUN apk --no-cache add \
	ca-certificates \
	python \
	py-pip \
	&& pip install cli53

ENTRYPOINT [ "cli53" ]
