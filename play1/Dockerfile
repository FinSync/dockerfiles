FROM buildpack-deps:xenial-curl

ARG pkg=java-1.8.0-amazon-corretto-jdk_8.222.10-1_amd64.deb
ARG path=https://d3pxv6yz143wms.cloudfront.net/8.222.10.1

RUN apt-get -y update \
    && apt-get -y install java-common sudo python unzip \
    && wget $path/$pkg \
    && dpkg --install ./$pkg \
    && curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "/tmp/awscli-bundle.zip" \
    && unzip /tmp/awscli-bundle.zip -d /tmp \
    && /tmp/awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws \
    && rm -rf /tmp/awscli-bundle* \
    && rm $pkg \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto

WORKDIR /opt

ARG version=1.4.6

RUN wget -q https://downloads.typesafe.com/play/$version/play-$version.zip && \
    unzip -q play-$version.zip && rm play-$version.zip

ENV HOME /opt/play-$version
RUN groupadd -r play -g 1000 && \
    useradd -u 1000 -r -g play -m -d $HOME -s /usr/sbin/nologin -c "Play user" play && \
    chown -R play $HOME && \
    ln -sf $HOME/play /usr/local/bin

USER play

EXPOSE 9000
