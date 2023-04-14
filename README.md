# Docker-PNMAMHES
Is reusable docker dev-box for multiple frameworks in PHP Tehnology.

![My Remote Image](https://i.ibb.co/tsJjFfJ/Screenshot-at-Apr-14-13-23-50.png)

# Dev-box tehnology stack
- `PHP 8.1`
- `MySql`
- `Redis`
- `ElasticSearch`
- `Kibana`
- `Adminer`
- `Nginx`
- `MailPit`


# Supported frameworks
*Note: Cureenlty all frameworks support `PHP8.1`

- [Laravel](https://laravel.com/)
- [Symfony](https://symfony.com/)
- [Slim](https://www.slimframework.com/)
- [Codeigniter](https://codeigniter.com/)
- [Yii](https://www.yiiframework.com/)


# Extensibility and Reusabillity

It's totally up to you to make replasements
- for example `MySQL` -> `PgSql` or `MongoDB` 
- for example `MailPit` -> `MailHog`
- even to make a clean up to suttesfly your needs.

# PHP version upgrade

The change is trivial and is located [here](https://github.com/sports-match-maker/docker-pnmamhes/blob/main/docker/php/Dockerfile)

`FROM php:8.1-fpm` to `FROM php:8.2-fpm` or `FROM php:7.4-fpm`

# Clean up 

 - Go to the default configuration for `Nginx` [here](https://github.com/sports-match-maker/docker-pnmamhes/blob/main/docker/nginx/conf.d/default.conf)
and configure the servers as many projects as with you have in your repo.
 - Go to the `init.sql` configuration for databases [here](https://github.com/sports-match-maker/docker-pnmamhes/blob/main/docker/db/init.sql) and make the changes
 - Register the projects as following [here](https://github.com/sports-match-maker/docker-pnmamhes/blob/main/docker-compose.yaml)
 
For example  

```
php-fpm:
    container_name: php
    build:
      context: .
      dockerfile: docker/php/Dockerfile
    volumes:
      - ./src/laravel:/var/www/html/laravel
      - ./src/symfony:/var/www/html/symfony
      - ./src/codeigniter:/var/www/html/codeigniter
      - ./src/slim:/var/www/html/slim
      - ./src/yii:/var/www/html/yii
    networks:
      - docker-pnmamhes

  nginx:
    container_name: nginx
    image: nginx:stable
    ports:
      - '80:80'
      - '81:81'
      - '82:82'
      - '83:83'
      - '84:84'
    volumes:
      - ./src/laravel:/var/www/html/laravel 
      - ./src/symfony:/var/www/html/symfony
      - ./src/codeigniter:/var/www/html/codeigniter
      - ./src/slim:/var/www/html/slim
      - ./src/yii:/var/www/html/yii
      - ./docker/nginx/conf.d/default.conf:/etc/nginx/conf.d/default.conf
    networks:
      - docker-pnmamhes

```
