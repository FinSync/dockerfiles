FROM cimg/ruby:3.0.5-node

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

RUN sudo mkdir $APP_HOME
RUN sudo chown -R $USER:$USER $APP_HOME
WORKDIR $APP_HOME

ADD . $APP_HOME
