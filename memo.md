# Dockerメモ

- Linux(ubuntu最新版でいい)
- PHP 7.3.3
- Apache 2.4.38
- WordPress
- MySQL 10.1.38-MariaDB

## とりあえず成功したコマンドメモ

- docker pull debian:stretch-slim
- docker run -it debian:stretch-slim
- apt-get update && apt-get install tree
- docker pull mysql:5.6.42
- apt-get -y install apt-transport-https lsb-release ca-certificates wget
- wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
- sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
- apt-get update
- apt-get -y install php7.3 php7.3-fpm php7.3-mysql php7.3-mbstring php7.3-xml php7.3-gd php7.3-curl php7.3-mysqli
- apt-get install vim
- apt-get install apache2
- service php7.3-fpm start
- service apache2 start
- mkdir html
- 

# Apache

## その他メモ
- dpkg -L パッケージ名 -> パッケージに関連するファイルがどこにあるか確認できる
- apt系はdebianのパッケージ管理ツール
- treeコマンドでディレクトリ配下の構造を見れるのでほしい
- treeをインストールするには apt-get update が必要だった
- apt-cache policy [query(正規表現)]でインストール可能なパッケージが確認可能
- dpkg -l でインストールされたパッケージが一覧表示
- docker tag a1e05daa2311 hoge/ubuntu-mongodb:latest
- 滅びの呪文(コンテナイメージネットワークを全部消す)
    - docker-compose down --rmi all --volumes
- /etc/php/7.3/fpm/pool.d/www.conf
- php.iniを探す
    - php -i | grep php.ini
- Apache2は2.4.25までの対応だったのでとりあえずそれで。
- service --status-allでwebサーバー内のすべてのサービスの状態を見れる


## ファイル構成
sample
|- mysql
|  |- Dockerfile
|- debian
|  |- Dockerfile
|- docker-compose.yml

## Dockerfile 起動コマンド
``` terminal
docker build ./mysql
docker tag 2bd6bd1f900e mysql:5.6.42-custom
docker build ./debian
docker tag 4c9d9a415138 debian:stretch-slim-custom
```

## コンテナ構成
|- mysql
|- apache
|  |- debian(php)