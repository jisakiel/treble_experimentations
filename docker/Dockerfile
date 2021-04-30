FROM ubuntu:20.04
MAINTAINER Pierre-Hugues Husson <phh@phh.me>

ENV DEBIAN_FRONTEND noninteractive
ENV USER root
ENV CCACHE_MAXSIZE 50g
ENV CCACHE_COMPRESS 1
ENV CCACHE_PATH /usr/bin/ccache
# /bin/sh points to Dash by default, reconfigure to use bash until Android
# build becomes POSIX compliant
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    dpkg-reconfigure -p critical dash
RUN dpkg --add-architecture i386 && apt update && apt install -y apt dpkg && apt install -y \
	build-essential \
    bsdmainutils \
    pngcrush schedtool xsltproc zip zlib1g-dev graphviz \
    flex gnupg \
        imagemagick \
	xorriso \
	openjdk-8-jdk \
	openjdk-11-jdk \
	python \
	python3 \
	git \
	m4 \
	unzip \
	bison \
	zip \
	gperf \
	libxml2-utils \
    xmlstarlet \
	zlib1g:i386 \
	libstdc++6:i386 \
	bc \
	curl \
	lzop \
	lzip \
	ccache \
	lunzip \
	jq \
	wget \
	squashfs-tools \
	sudo && \
	apt clean autoremove && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN ln -s /usr/bin/xorrisofs /usr/bin/mkisofs

# Download and install repo
RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo && chmod a+x /usr/local/bin/repo

RUN git config --global user.name "buildbot"
RUN git config --global user.email "buildbot@phh.me"

USER root
