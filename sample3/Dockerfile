# 参照：https://docs.docker.com/engine/examples/postgresql_service/

FROM ubuntu:16.04

# 引数と初期値を設定
ARG user=docker
ARG password=docker
ARG dbname=docker

# PostgreSQL パッケージの検証に使うPGPキーを設定
# https://www.postgresql.org/media/keys/ACCC4CF8.asc と同じキーを使用
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# PostgreSQL リポジトリを追加
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

# python-software-properties、software-properties-common、PostgreSQL 9.3 パッケージをインストール
RUN apt-get update && apt-get install -y python-software-properties software-properties-common postgresql-9.3 postgresql-client-9.3 postgresql-contrib-9.3

# "apt-get clean" は各 apt-get で自動実行されるので不要

# 以降は postgres ユーザーで実行
# postgres ユーザーは postgres-9.3 パッケージのインストール時に作成される
USER postgres

# 1.PostgreSQL の Role を作成
#   Role名：${user}
#   パスワード：${password}
# 2.作成した Role がオーナーのデータベースを作成
#   データベース名：${dbname}
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER ${user} WITH SUPERUSER PASSWORD \'${password}\';" &&\
    createdb -O ${user} ${dbname}

# リモート接続を有効にする
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.3/main/pg_hba.conf

# postgresql.conf に listen_addresses を追加
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.3/main/postgresql.conf

# PostgreSQL のポートを公開
EXPOSE 5432

# config のバックアップ、ログ、データベース用のボリュームを設定
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# デフォルトの実行コマンド
CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.3/main", "-c", "config_file=/etc/postgresql/9.3/main/postgresql.conf"]