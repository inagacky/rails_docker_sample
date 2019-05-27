FROM mysql:8.0.13

LABEL maintainer inagacky

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

ADD ./conf/change_default_auth.cnf /etc/mysql/conf.d/.

RUN apt-get update && \
    apt-get install -y vim less
