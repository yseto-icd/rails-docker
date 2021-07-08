# README
## Docker説明用リポジトリ

### お断り
- 説明用にアンチパターンをいくつか使ってます
  - postgresにPASSWORDなしでログインできる設定
  - DBの永続データをGit管理内に入れる

### イメージビルド
`docker-compose build`
rails-docker_web

### コンテナ起動(compose)
`docker-compose up -d [--build]`
- localhost:3000でEXPOSE

### コンテナ起動(isolate)
`docker run -it -p 3030:3000 rails-docker_web bash`
- bashで`bundle exec rails s`
- localhost:3030でEXPOSE(エラーになるはず)

`docker run --name db -p 5431:5432 -e POSTGRES_HOST_AUTH_METHOD=trust postgres`

`docker run --link=db -it -p 3030:3000 rails-docker_web bash`
- bashで`bundle exec rails db:create`
- bashで`bundle exec rails s -p 3000 -b '0.0.0.0'`
- localhost:3030でEXPOSE
