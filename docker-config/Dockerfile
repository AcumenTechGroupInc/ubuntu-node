FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Raj Rajen <raj.rajen.acumen@gmail.com>

# References from 
## https://github.com/ryanfb/tesseract_latinocr_docker/blob/master/Dockerfile
## https://github.com/docker-library/golang/blob/1a422afd7db928a821e97906ed27ed606e2f072a/1.3/Dockerfile
## https://github.com/ironSource/docker-config/blob/master/Dockerfile-nodejs-cluster
# 


# Security updates plus handy stuff
RUN	apt-get update \
	&& apt-get -y install unattended-upgrades curl wget vim \
	&& unattended-upgrades -v

################## BEGIN INSTALLATION ######################

# verify gpg and sha256: http://nodejs.org/dist/v0.12.7/SHASUMS256.txt.asc
# gpg: aka "Timothy J Fontaine (Work) <tj.fontaine@joyent.com>"
# gpg: aka "Julien Gilli <jgilli@fastmail.fm>"
RUN set -xe \
	&& for key in \
		7937DFD2AB06298B2293C3187D33FF9D0246406D \
		114F43EE0176B71C7BC219DD50A3051F888C628D \
	; do \
		gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	done

# Print "Hello docker2!"
RUN echo "Hello docker2!"

ENV NODE_VERSION 0.12.7
ENV NPM_VERSION 2.14.1

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
	&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
	&& gpg --verify SHASUMS256.txt.asc \
	&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
	&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
	&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc \
	&& npm install -g npm@"$NPM_VERSION" \
	&& npm cache clear

##################### INSTALLATION END #####################

RUN     useradd ubuntu -b /home/ubuntu \
        && mkdir /var/log/sails \
        && mkdir /home/ubuntu \
        && chown -R ubuntu:ubuntu /home/ubuntu \
        && chown -R ubuntu:ubuntu /var/log/sails

# COPY    code /home/ubuntu

USER    ubuntu

WORKDIR /home/ubuntu

# RUN     npm install

# CMD     node src/ /home/ubuntu

CMD [ "node" ]