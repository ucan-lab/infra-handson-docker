# Docker handson

## Require for mac

- Install [Homebrew](https://brew.sh/index_ja)
- Install [Docker for mac](https://docs.docker.com/docker-for-mac)

```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
$ brew cask install docker
```

## Build

```
$ git clone https://github.com/ucan-lab/infra-handson-docker.git
$ git clone https://github.com/ucan-lab/infra-handson-docker.git infra-handson-docker/shop

$ docker build -t php_image ./php
$ docker build -t mysql_image ./mysql
$ docker volume create --name shop_db_storage
$ docker network create shop_network
$ docker run -d --name shop_web --network shop_network -p 8100:80 -v $(pwd)/shop:/var/www/html php_image
$ docker run -d --name shop_db -v shop_db_storage:/var/lib/mysql --network shop_network mysql_image
```

### SQL

```
$ docker exec -it shop_db bash
$ mysql -u root -p$MYSQL_PASSWORD $MYSQL_DATABASE

create table shop.items (
  id int primary key auto_increment,
  name varchar(30) comment '商品名',
  stock int default 0 comment '在庫数'
) comment='商品テーブル';

INSERT INTO items (name, stock) VALUE ("Apple", 10);
INSERT INTO items (name, stock) VALUE ("Bad Apple", 1);
```

http://127.0.0.1:8100

## Clear

```
$ docker rm -f shop_web shop_db
$ docker rmi php_image mysql_image
$ docker volume rm shop_db_storage
$ docker network rm shop_network
```
