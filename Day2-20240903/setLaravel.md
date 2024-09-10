# How to Install Laravel - The process for installing Laravel

1. php.ini file
    - if php.ini file is not present so copy the php.ini - development file and past
    - then rename it as php.ini

2. inside php.ini file most of smp imp extensions are commented so uncomment the require extensions.

3. ext folder extension for windows.

4. Install the composer.phar file.
    - for installation we have to paste 4 lines in cmd
    - [Get those Lines](https://getcomposer.org/download/)

5. disable the token -> git command
    - git config --global credential.helper store

6. download the cacert.pem from google or stackover flow

7. increase the memory of post, upload, etc in php.ini.

8. also use this and disable the certificate => composer config -g -- disable-tls false

9. create project
    - using specific version
        - ex command => php8.2 composer.phar create-project laravel/laravel hello-world
    - with default version
        - ex command => composer create-project laravel/laravel example-app

10. after installation and before serve must set the db config and apply it using this cmd: php artisan migrate

# Enjoy............................!