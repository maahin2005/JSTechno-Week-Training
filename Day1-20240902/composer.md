# composer

- [Download Composer](https://getcomposer.org/download/)

- steps for setting cmd like php8.2

  - go to php.ini file
  - copy and paste it there
  - rename it according to it version ( ex. if version is 7.4 so rename it as php7.4 )

- [Refer it for initial setup](https://getcomposer.org/download/)

# steps for setup/ creating composer.phar:

- php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

- php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

- php composer-setup.php

- php -r "unlink('composer-setup.php');"

## difference:

- exe => only will run at default php version and the cmd is `php -v`
- composer.phar => we can use any version of php using cmd `ex. php8.2`
