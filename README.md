# rails7-mysql8-docker-template

Ruby on Rails 7 と MySQL 8 を Docker コンテナ上で実行するためのテンプレート

## 手順

1. 本リポジトリのクローン

   `git clone https://github.com/Mashpy/rails-7-docker-template-with-mysql`

2. rails app のインストール

   `docker compose run app rails new . --force --database=mysql --skip-bundle`

3. Docker イメージのビルド

   `docker-compose build`

4. `config/database.yml` を以下のように編集

   ```
   default: &default
     adapter: mysql2
     encoding: utf8
     pool: 5
     username: root
     password: "root"
     host: db

   development:
     <<: *default
     database: dev

   test:
     <<: *default
     database: dev
   ```

5. コンテナの起動

   `docker-compose up`

6. 起動確認

   `localhost:3000` にアクセスする
