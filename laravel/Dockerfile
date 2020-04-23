FROM php:7.3.6-fpm-alpine3.9

## assumir que estamos trabalhando nessa pasta dentro do container
WORKDIR /var/www

RUN rm -rf /var/www/html

COPY . /var/www

#ln - comando do linux para associar (link simbólico) a pasta public (laravel computador) para pasta html no container
RUN ln -s public html

EXPOSE 9000

ENTRYPOINT ["php-fpm"]