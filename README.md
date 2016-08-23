# rails-on-docker

参考
[http://docs.docker.jp/compose/rails.html](http://docs.docker.jp/compose/rails.html)

Gemfile作成
```
$ touch volumes/Gemfile
```
```
# Gemfile
source 'https://rubygems.org'
gem 'rails', '4.2.0'
```

Gemfile.lock作成
```
$ touch volumes/Gemfile.lock
```

ビルドしてbundle install
```
$ docker-compose build
```

Railsアプリを作る
```
$ docker-compose run web rails new . --force --database=postgresql --skip-bundle
```

権限を変える
```
$ sudo chown -R $USER:$USER volumes/
```

Gemfileからtherubyracerを読み込む行をアンコメント
```
gem 'therubyracer', platforms: :ruby
```

新しいGemfileでイメージ再構築
```
$ docker-compose build
```

config/database.ymlの編集してデータベースに接続
```
development: &default
  adapter: postgresql
  encoding: unicode
  database: postgres
  pool: 5
  username: postgres
  password:
  host: db

test:
  <<: *default
  database: myapp_test
```

アプリケーション起動
```
$ docker-compose up
```

別ターミナルでデータベース作成
```
$ docer-compose run web rake db:create
```
