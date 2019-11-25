FROM circleci/ruby:2.4-node

########################################
ENV APP_HOME /myapp
ENV BUNDLE_PATH /cache
########################################

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
RUN apt-get update -qq && apt-get install -y build-essential

# for postgres
RUN apt-get install -y libpq-dev

# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev

# for pdftk
RUN apt-get install -y pdftk

RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD . $APP_HOME

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install nodejs
