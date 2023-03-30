# Laravel Docker Base
**プロジェクト毎に新規リポジトリにコピーして利用してください。**

## 前提
* Docker Desktop または Lima + Docker 環境構築済み

## コンテナ構造
```
docker
├── app
├── nginx
└── mysql
```
### app container
php + composer + Laravel 導入済みのアプリケーションサーバ

### nginx container
nginx導入済みのwebサーバ

* リクエストを受け取り、アプリケーションサーバに流してます。
* .php 以外の静的ファイルはwebサーバから返しているため、このコンテナにもソースコードを同期してます。

### mysql container
mysql導入済みのdbサーバ

## 使い方
### コンテナ起動の設定調整
※ 変更が必要ない場合はデフォルト値で起動します
1. env作成
    ```
    $ cp .env .env.example
    ```
1. 変更したい項目を変更

### コンテナ起動
```
$ docker compose up -d
```

### バージョン変更方法
PHP
* docker/app/Dockerfile 1行目でベースイメージを変更

Composer
* docker/app/Dockerfile 5行目の `composer:2.5` を変更

Laravel
1. コンテナを起動
1. app コンテナに接続
    ```
    $ docker compose exec app bash
    ```
1. `/var/www` に移動
    ```
    # cd /var/www
    ```
1. `src` ディレクトリ内を空に
    ```
    # rm -rf src/*
    ```
1. バージョンを指定して新しくプロジェクトを作成
    ```:ex. バージョン10.x
    # composer create-project laravel/laravel=10  src
    ```
Nginx
* docker/nginx/Dockerfile の1行目でベースイメージを変更

MySQL
* docker/mysql/Dockerfile の1行目でベースイメージを変更
