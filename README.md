# e-match_docker

PHPおよびCakePHPの自己学習のために2019年頃に開発。<br />
現在はWeb公開はしていない。<br />
E-sportsで共に戦っていく仲間を探すことができるマッチングサイト。<br />

# 開発環境構築手順

1. 本リポジトリをcloneする
1. ターミナルで e-match_docker に cd する
1. e-match_docker配下で[e-match_app](https://github.com/koichirokudo/e-match_app)をcloneする
1. mv e-match_app src : cloneしたディレクトリ e-match_app から src にリネーム
1. docker-compose up -d
1. docker-compose exec app bash
1. composer install
1. bin/cake migrations migrate
1. localhost:8080 にブラウザでアクセスする