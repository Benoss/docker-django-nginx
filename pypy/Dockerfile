FROM pypy:2

MAINTAINER Benoit Chabord <>

RUN ln -s /usr/local/bin/pypy /usr/local/bin/python

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
	&& echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list \
	&& echo "deb http://ftp.debian.org/debian jessie-backports main " >> /etc/apt/sources.list.d/backports.list \
	&& apt-get update \
	&& apt-get install -y -t jessie-backports openssl libssl-dev \
	&& apt-get install -y ca-certificates nginx gettext-base \
        && apt-get install -y libev-dev \
        && apt-get install -y python-dev libmysqlclient-dev \
	&& rm -rf /var/lib/apt/lists/*
# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log
EXPOSE 80 443
# Finished setting up Nginx
RUN rm /etc/nginx/conf.d/default.conf

RUN python --version && nginx -v && pip --version
