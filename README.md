# Dockerテンプレート(php8+MySQL8+Nginx)

- CakePHP4用での使用を想定

## 必要なソフトウェア

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.jp/compose/toc.html)
- [Makefile](http://www.gnu.org/software/make/)

## 開発環境構築手順

0. Macの場合は次に設定するIPに対して以下のコマンドを実行

    ```bash
    sudo ifconfig lo0 alias 127.*.*.* up
    ```


1. IPに127.0.0.1~127.255.255.254の値を設定して以下のコマンドを実行

    ```bash
    make init IP=127.*.*.*
    ```

## 参考

- [【超入門】20分でLaravel開発環境を爆速構築するDockerハンズオン](https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4)
- [最強のLaravel開発環境をDockerを使って構築する](https://qiita.com/ucan-lab/items/5fc1281cd8076c8ac9f4)
- [まだdocker-composeのホスト側portを考えるのに疲弊しているの？](https://wand-ta.hatenablog.com/entry/2020/05/23/011001)
- [MacのApacheで127.0.0.1以外のIPアドレスを使用する](https://qiita.com/HanaeKae/items/79d783521b83e350fa42)
- [Docker(PHP) 開発環境の Apache を mkcert を使って https で動かす](https://zenn.dev/oppara/articles/docker-php-apache-mkcert)