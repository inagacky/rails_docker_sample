FROM ruby:2.6.3

LABEL maintainer inagacky

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

RUN apt-get update \
  && apt-get install -y libpq-dev build-essential nodejs sudo default-libmysqlclient-dev mysql-client \
  && gem install bundler \
  && gem install rails

ENV APP_HOME /var/www/app
ENV USER    rails_dev

# User
RUN useradd -d /home/$USER -m -s /bin/bash $USER
RUN echo "$USER:$USER" | chpasswd
RUN echo "$USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USER
USER $USER
ENV HOME /home/$USER

ADD app $APP_HOME
RUN sudo chown -R $USER:$USER $APP_HOME
WORKDIR $APP_HOME

RUN sudo chown $USER:$USER Gemfile
RUN sudo chown $USER:$USER Gemfile.lock
RUN bundle install

EXPOSE 3000

CMD ["bundle", "exec", "rails", "s", "-p", "3000", "-b", "0.0.0.0"]