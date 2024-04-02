## LaravelのDocker開発環境

## 構造

```
  ├── ...
  ├── docker
  │   ├── mysql
  │        ├── Dockerfile           # MySQL 8.0.28
  │        └── my.cnf               # MySQL config file
  │   ├── nginx
  │        └── my.cnf               # nginx config file
  │   ├── php
  │        ├── Dockerfile           # PHP8.1-fpm and php Composer
  │        └── php.ini              # PHP config file
  ├── src                           # PHP Laravel source file folder
  ├── .env                          # Using docker-compose.yml
  ├── .gitignore                    # gitingore file
  └── docker-compose.yml            # docker comose file
```

## 起動
docker-compose up -d

## 環境変数 .env
自分に合った環境変数名に合わせてもOKです.
```
DB_NAME=database
DB_USER=root
DB_PASS=password
DB_ROOT_PASS=password
DB_PORT=3306
TZ=Asia/Tokyo
```

### PHPMyAdminが入っています.
```
http://localhsot:8080
```

## Laravel Projectの作成
project1 は適当に変えてください。  
変更した場合は、nginx/default.conf 4行目の部分も変更してください。
```
    root /var/www/project1/public;
                  ^^^^^^^^
```

```
docker-compose exec php /bin/bash
root@127294f359d1:/var/www# composer create-project --prefer-dist laravel/laravel project1
root@127294f359d1:/var/www# cd project1
root@127294f359d1:/var/www/project1# chmod -R 777 storage bootstrap/cache
root@127294f359d1:/var/www/project1# php artisan ui vue
root@127294f359d1:/var/www/project1# npm install
root@127294f359d1:/var/www/project1# npm install --save vue-router
```

### ブラウザーで確認
```
http://localhost
```

### Laravel開発環境のDockerファイルになります.
毎回、ネットで探すのも面倒なので.

2023/11/24時点では動作確認済み.
Windows11 wsl2 Ubuntu20.04 Docker

ご自由にどうぞ.
