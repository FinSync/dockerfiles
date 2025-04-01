FROM node:18.20-alpine AS node_base

FROM cimg/ruby:3.0.5

# get node/npm binaries
COPY --from=node_base /usr/local/bin /usr/local/bin
COPY --from=node_base /usr/local/lib/node_modules/npm /usr/local/lib/node_modules/npm

# Create symbolic link for the nodejs path expected by rails, matches the path where CircleCI puts the binary: https://github.com/CircleCI-Public/cimg-ruby/blob/2cb03f2a4f02107a7994973c56c99978d925d779/3.0/node/Dockerfile
RUN sudo ln -s /usr/local/bin/node /usr/local/bin/nodejs

########################################
ENV APP_HOME /myapp
ENV BUNDLE_PATH /cache
########################################
#RUN sudo su -c "printf \"deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main\" > /etc/apt/sources.list"
#RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8B48AD6246925553 7638D0442B90D010 CBF8D6FD518E17E1
#RUN sudo apt-get install debian-archive-keyring
RUN sudo apt-get update -qq && sudo apt-get install -y build-essential

# for postgres
RUN sudo apt-get install -y libpq-dev

# for nokogiri
RUN sudo apt-get install -y libxml2-dev libxslt1-dev

# for pdftk
RUN sudo apt-get install -y pdftk
USER root

RUN sudo mkdir $APP_HOME

WORKDIR $APP_HOME

ADD . $APP_HOME
