# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: humartin <humartin@student.42.fr>          +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2023/02/13 12:01:57 by humartin          #+#    #+#              #
#    Updated: 2023/02/13 12:02:08 by humartin         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM debian:buster
LABEL maintainer="humartin@student.42mulhouse.fr"

ARG PHP_VERSION

RUN apt-get -y update && \
	apt-get -y upgrade && \
	apt-get install -y \
		php${PHP_VERSION} \
		php${PHP_VERSION}-mysql \
		php${PHP_VERSION}-fpm \
		php${PHP_VERSION}-gd \
		php${PHP_VERSION}-mbstring \
		php${PHP_VERSION}-zip \
		mariadb-client \
		wget


# user:group in debian is www-data
RUN mkdir -p /var/www/html
RUN chown -R www-data:www-data /var/www/html
RUN userdel -f www-data && useradd -u 82 www-data

COPY ./tools/start.sh /start.sh
COPY ./conf/www.conf /etc/php/${PHP_VERSION}/fpm/pool.d/
COPY ./conf/php-fpm.conf /etc/php/${PHP_VERSION}/fpm/
#COPY ./conf/wp-config.php /var/www/html/wordpress/wp-config.php

# ! Install wp-cli, using it to build, configure wordpress
RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
	chmod +x wp-cli.phar && \
	mv wp-cli.phar /usr/local/bin/wp

WORKDIR /var/www/html/wordpress

EXPOSE	9000

ENTRYPOINT ["sh", "/start.sh"]