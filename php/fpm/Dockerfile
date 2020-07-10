ARG PHP_VERSION=7.4
FROM php:${PHP_VERSION}-fpm-alpine

ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone