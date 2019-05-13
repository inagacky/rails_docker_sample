FROM ruby:2.6.3

MAINTAINER inagacky 

ARG USER="rails"
ARG UID="1000"
ARG GROUP="rails"
ARG GID="1000"
ARG WORKSPACE=/usr/src/app
ARG START_ENV=development

ENV LANG C.UTF-8
ENV RAILS_ENV $START_ENV

RUN apt-get update && \
    apt-get install -y vim less sudo

RUN mkdir -p $WORKSPACE
WORKDIR $WORKSPACE

COPY app/Gemfile $WORKSPACE
COPY app/Gemfile.lock $WORKSPACE

RUN apt-get install -y build-essential libpq-dev imagemagick libmagickcore-dev libmagickwand-dev nodejs && \
    gem install bundler

COPY app $WORKSPACE

RUN bundle install

RUN groupadd -r --gid $GID $GROUP && \
    useradd -r --uid $UID --gid $GID $USER && \
    chown -R $USER:$GROUP $WORKSPACE
RUN echo "${USER} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${USER}

ENV SECRET_KEY_BASE "`bundle exec rake secret`"

USER $USER

EXPOSE 3000
CMD ["bundle", "exec", "rails", "s", "-p", "3000", "-b", "0.0.0.0"]

