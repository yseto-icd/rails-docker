# README
## Docker説明用リポジトリ

### お断り
- 説明用にアンチパターンをいくつか使ってます
  - postgresにPASSWORDなしでログインできる設定

### イメージビルド
`docker-compose build`
rails-docker_web

### コンテナ起動(compose)
`docker-compose up -d [--build]`  
`docker-compose run web rails db:create`
- localhost:3000でEXPOSE
  - レスポンス遅かったりしたらwebコンテナの再起動とか必要かも

### コンテナ起動(isolate)
`docker run -it -p 3030:3000 rails-docker_web bash`
- bashで`bundle exec rails s`
- localhost:3030でEXPOSE(エラーになるはず)

`docker run --name db -p 5431:5432 -e POSTGRES_HOST_AUTH_METHOD=trust postgres`

`docker run --link=db -it -p 3030:3000 rails-docker_web bash`
- bashで`bundle exec rails db:create`
- bashで`bundle exec rails s -p 3000 -b '0.0.0.0'`
- localhost:3030でEXPOSE
