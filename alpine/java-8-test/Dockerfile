# Java 8 testing docker image.
#
# Building the image: 'docker image build --squash -t java-8-test .'.
#
# Using the image:
# - For debugging, install the gdb and strace packages.
#   Start docker with '--cap-add=SYS_PTRACE --security-opt seccomp=unconfined'.
# - For exposing all ports, add '--network="host'.
#
# The image is available on Dockerhub: https://hub.docker.com/r/shaharv/alpine-java-8-builds
#

FROM alpine:3.11

# Install useful packages
RUN apk --no-cache add \
	bash binutils coreutils file grep nano procps sudo tar unzip

# Install packaged OpenJDK 8 (8.242.08-r0)
RUN apk --no-cache add openjdk8

# Install gradle
RUN apk --no-cache add gradle

# Download zipped OpenJDK 8 versions
RUN set -ex && \
	cd /usr/lib/jvm && \
        for JAVA_VER in 8.131.11-r2 8.151.12-r0 8.171.11-r0 8.181.13-r0 8.191.12-r0 8.201.08-r0 8.201.08-r1 8.212.04-r0 8.222.10-r1 8.232.09-r0; \
	do \
		ZIP_NAME=java-1.8-openjdk-$JAVA_VER.tar.gz && \
		wget https://github.com/shaharv/alpine-openjdk-builds/releases/download/1.8/$ZIP_NAME && \
		tar -xf $ZIP_NAME && \
		rm $ZIP_NAME; \
	done

CMD ["/bin/bash"]
