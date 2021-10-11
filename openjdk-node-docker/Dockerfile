FROM adoptopenjdk/openjdk11:x86_64-ubuntu-jdk-11.0.11_9

ARG WORKDIR=/apps
ARG UNAME=user
ARG UID=1000
ARG GID=1000

RUN apt-get update -qq && apt-get install -y \
    curl \
    gzip \
    git \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get clean

ENV JAVA_HOME=/opt/java/openjdk

RUN rm /opt/java/openjdk/lib/src.zip 

RUN groupadd -g $GID -o $UNAME && useradd -m -u $UID -g $GID -s /bin/bash $UNAME

ENV NODE_VERSION=14.18.0 \
    NPM_VERSION=6.14.14

# Install basics
RUN echo "Installing node v${NODE_VERSION}..." && \
    curl --retry 3 -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
    tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
    rm "node-v$NODE_VERSION-linux-x64.tar.gz" && \
    npm install -g npm@"$NPM_VERSION" && \
    npm cache clear --force

RUN mkdir -p $WORKDIR && \
    chown -R $UID:$GID $WORKDIR

WORKDIR $WORKDIR


