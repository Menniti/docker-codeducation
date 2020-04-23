FROM php:7.3.6-fpm-alpine3.9


RUN apk add sudo
#apk add sudo
RUN apk add bash mysql-client
RUN docker-php-ext-install pdo pdo_mysql
RUN apk add --no-cache openssl


## assumir que estamos trabalhando nessa pasta dentro do container
WORKDIR /var/www
COPY . .
RUN rm -rf /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# RUN php artisan migrate
# RUN php artisan serve --host=0.0.0.0
# RUN php artisan key:generate
# RUN php artisan config:cache

#RUN usermod -u 1000 www-data

# RUN whoami && \
#     groups $(whoami)

RUN composer install && \
            cp .env.example .env && \
            php artisan key:generate && \
            php artisan config:cache
            #php artisan serve --host=0.0.0.0

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

#RUN sudo usermod -u 1000 www-data

#USER root
#RUN chown -R www-data:www-data /var/www
#RUN chmod -R 777 /var/www
#RUN chmod 755 /var/www

#RUN chown -R www-data:www-data * /var/www
#COPY --chown=www-data:www-data . /var/www
#RUN chmod -R 755 /var/www/storage
#RUN chown -R www-data:www-data /var/www*
#RUN chown -R nginx /var/www/storage
RUN chmod -R u=rw,go=r /var/www

#RUN php artisan serve --host=0.0.0.0

#RUN sudo chgrp -R www-data storage bootstrap/cache; sudo chmod -R ug+rwx storage bootstrap/cache
#COPY . /var/www


#ln - comando do linux para associar (link simbólico) a pasta public (laravel computador) para pasta html no container
RUN ln -s public html

EXPOSE 9000

ENTRYPOINT ["php-fpm"]