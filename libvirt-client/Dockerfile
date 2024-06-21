FROM alpine:3
MAINTAINER Jessica Frazelle <jess@docker.com>

RUN apk --no-cache add \
	libvirt-client

ENTRYPOINT [ "virsh", "-c", "qemu:///system" ]
