# CakePHP4用テンプレート

## 概要

- CakePHP4用のDockerテンプレート
- php8+mysql8+Nginx

## 必要なソフトウェア

- [Docker](https://www.docker.com/)
   - [Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
   - [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
- [Docker Compose](https://docs.docker.jp/compose/toc.html)
- [Makefile](http://www.gnu.org/software/make/)

※各種DockerアプリとDocker ComposeはDocker Desktopに同梱

※MakefileはMacの場合はXcodeのコマンドラインツールに同梱
## 既存プロジェクトへの配置手順

1. ファイルを既存プロジェクトのルートディレクトリに配置
2. env.exampleの`MYSQL_USER`、`MYSQL_PASSWORD` 、`MYSQL_DATABASE`をアプリケーション側の設定と合わせる
3. CakePHPの`./config/app_local.php`の`Datasources.default.host`を`db`に書き換える
     
## 開発環境構築手順

0. Macの場合は以下のコマンドを実行 （他のプロジェクトで設定済みの場合は不要）

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

1. IPに127.0.0.1~127.0.0.255の値を設定して以下のコマンドを実行

    ```bash
    make init IP=127.0.0.*
    ```

2. ホストの/etc/hostsに設定したIPとドメインの対応を記載する

    ```bash
    sudo vi /etc/hosts
    ```
    ```hosts
    127.0.0.* myapp.local
    ```
   
## 参考

- [【超入門】20分でLaravel開発環境を爆速構築するDockerハンズオン](https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4)
- [最強のLaravel開発環境をDockerを使って構築する](https://qiita.com/ucan-lab/items/5fc1281cd8076c8ac9f4)
- [まだdocker-composeのホスト側portを考えるのに疲弊しているの？](https://wand-ta.hatenablog.com/entry/2020/05/23/011001)
- [MacのApacheで127.0.0.1以外のIPアドレスを使用する](https://qiita.com/HanaeKae/items/79d783521b83e350fa42)
- [Docker(PHP) 開発環境の Apache を mkcert を使って https で動かす](https://zenn.dev/oppara/articles/docker-php-apache-mkcert)
