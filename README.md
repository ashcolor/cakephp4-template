# CakePHP4 用テンプレート

## 概要

-   CakePHP4 用の Docker テンプレート
-   php8+mysql8+Nginx

## 必要なソフトウェア

-   [Docker](https://www.docker.com/)
    -   [Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
    -   [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
-   [Docker Compose](https://docs.docker.jp/compose/toc.html)
-   [Makefile](http://www.gnu.org/software/make/)

※各種 Docker アプリと Docker Compose は Docker Desktop に同梱

※Makefile は Mac の場合は Xcode のコマンドラインツールに同梱

## 既存プロジェクトへの配置手順

1. ファイルを既存プロジェクトのルートディレクトリに配置
2. env.example の`MYSQL_USER`、`MYSQL_PASSWORD` 、`MYSQL_DATABASE`をアプリケーション側の設定と合わせる
3. CakePHP の`./config/app_local.php`の`Datasources.default.host`を`db`に書き換える

## 開発環境構築手順

0. Mac の場合は以下のコマンドを実行 （他のプロジェクトで設定済みの場合は不要）

    ```bash
    cat <<EOL > /usr/local/etc/set_loopback_address
    #!/bin/bash
    for ((i=1;i<255;i++))
    do
    sudo ifconfig lo0 alias 127.0.0.\$i up
    done
    EOL
    chmod 777 /usr/local/etc/set_loopback_address
    sudo /usr/local/etc/set_loopback_address
    sudo defaults write com.apple.loginwindow LoginHook /usr/local/etc/set_loopback_address
    ```

1. IP に 127.0.0.1~127.0.0.255 の値を設定して以下のコマンドを実行

    ```bash
    make init IP=127.0.0.*
    ```

2. ホストの/etc/hosts に設定した IP とドメインの対応を記載する

    ```bash
    sudo vi /etc/hosts
    ```

    ```hosts
    127.0.0.* myapp.local
    ```

3. CakePHP の取得

    ```
    make php
    composer create-project --prefer-dist cakephp/app:4.* app
    mv app/* app/.[^\.]* .
    rm -r app
    ```

4. DB 設定を書き換える

    `config\app_local.php`

    ```bash:
        'host' => 'db',
    ```

## 参考

-   [【超入門】20 分で Laravel 開発環境を爆速構築する Docker ハンズオン](https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4)
-   [最強の Laravel 開発環境を Docker を使って構築する](https://qiita.com/ucan-lab/items/5fc1281cd8076c8ac9f4)
-   [まだ docker-compose のホスト側 port を考えるのに疲弊しているの？](https://wand-ta.hatenablog.com/entry/2020/05/23/011001)
-   [Mac の Apache で 127.0.0.1 以外の IP アドレスを使用する](https://qiita.com/HanaeKae/items/79d783521b83e350fa42)
-   [Docker(PHP) 開発環境の Apache を mkcert を使って https で動かす](https://zenn.dev/oppara/articles/docker-php-apache-mkcert)
