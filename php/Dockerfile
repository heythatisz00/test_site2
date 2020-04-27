FROM bitnami/php-fpm:7.2 as builder
RUN install_packages git autoconf build-essential
WORKDIR /app
RUN wget https://github.com/xdebug/xdebug/archive/2.6.0.tar.gz && \
    tar xzf 2.6.0.tar.gz && \
    cd xdebug-2.6.0 && \
    phpize && \
    ./configure --enable-xdebug && \
    make && make install


FROM bitnami/php-fpm:7.2
COPY --from=builder /opt/bitnami/php/lib/php/extensions/xdebug.so /opt/bitnami/php/lib/php/extensions/
RUN echo 'zend_extension="/opt/bitnami/php/lib/php/extensions/xdebug.so"' >> /opt/bitnami/php/etc/php.ini

RUN echo "xdebug.remote_port=9000" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.remote_enable=1" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.remote_connect_back=0" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.remote_host=192.168.1.4" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.idekey=docker" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.remote_autostart=1" >> /opt/bitnami/php/etc/php.ini \
    && echo "xdebug.remote_log=/tmp/xdebug.log" >> /opt/bitnami/php/etc/php.ini