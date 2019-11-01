# ベースイメージ
FROM centos:7.5.1804

# httpd、iprouteパッケージをインストール
# その後キャッシュを削除
RUN yum install -y httpd iproute && yum clean all

# ホストからindex.htmlを/var/www/html/にコピー
COPY index.html /var/www/html/

# httpdを有効にする
RUN systemctl enable httpd

# systemdの起動
CMD ["/sbin/init"]