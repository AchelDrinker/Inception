# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: humartin <humartin@student.42.fr>          +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2023/02/13 11:57:44 by humartin          #+#    #+#              #
#    Updated: 2023/02/13 11:57:55 by humartin         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM alpine:3.16

LABEL maintainer="humartin@student.42mulhouse.fr"

RUN apk update && apk upgrade && \
    apk add --no-cache mariadb mariadb-client
RUN mkdir -p /run/mysqld && \
	chown -R mysql:mysql /run/mysqld

COPY ./tools/start.sh /
EXPOSE	3306

ENTRYPOINT ["sh", "/start.sh"]