docker-compose up -d

mysql -h db -u dbuser -p
dbpass

```
ec2-user@7d7d499bdfd2:~/environment$ whoami
ec2-user

$ php -v
PHP 7.4.33 (cli) (built: Nov 15 2022 06:03:30) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
#PHP 7.2.24 (cli) (built: Oct 31 2019 18:27:08) ( NTS )


$ mysql --version
mysql  Ver 15.1 Distrib 10.5.18-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper
# mysql  Ver 15.1 Distrib 10.2.38-MariaDB, for Linux (x86_64) using  EditLine wrapper

$ composer -V
Composer version 2.5.1 2022-12-22 15:33:54

$ date
Mon Jan 30 13:12:11 UTC 2023

$ git --version
git version 2.30.2
```

$ git clone https://github.com/TakanoriShima/todolist.git
$ cd todolist/
$ composer install
$ cp .env.example .env
$ php artisan key:generate
.env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=todolist
DB_USERNAME=dbuser
DB_PASSWORD=dbpass

$ php artisan migrate
$ php artisan db:seed --class=FrontAuthUser
$ php artisan db:seed --class=AdminAuthUser
$ php artisan serve --port=$PORT

$ mysql -h db -u root -p
root
MySQL [todolist]> exit