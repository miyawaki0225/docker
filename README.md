# Dockerとは
https://www.tohoho-web.com/docker/about.html  

## Docker
--- 
- Dockerとは
- インストール
- チュートリアル
- Dockerコマンド
  - docker run/create
  - docker ps/stats
  - docker rm/start/stop...
  - docker exec/attach
  - docker cp/rename/update
  - docker logs/port/top
  - docker pull/push/search/login/logout
  - docker images/rmi/history/commit/tag/build/trust
  - docker volume
  - docker network
  - docker export/import/save/load
- Dockerfileによるビルド
- Docker Compose
- Podman
- 小技・ノウハウ集


## Dockerとは
― Docker社が開発している、Linux をターゲットとするコンテナ管理基盤です。
- CentOS や Ubuntu などの Linux(ホストOS)上で、CentOS や Ubuntu などをゲストOSの様に稼働させることができます。
- VirtualBox, VMware, Hyper-V などのハイパーバイザ型仮想化がホストOS上でゲストOSを仮想的に起動させるのに対し、コンテナ型仮想化では、ホストOSとゲストコンテナでOSを共有し、ファイルシステムやプロセス空間、ネットワーク空間等のみを仮想化し、プロセスのみを起動します。
- ハイパーバイザ型に対して、起動が早い、サイズが小さいなどの利点を持ちます。
- コンテナ内では、複数のプロセスを動かすことも可能ですが、通常、ひとつのコンテナでひとつのプロセスのみを起動します。
- ハイパーバイザ型は仮想OSを動かすもの、コンテナ型はプロセス固有のファイルシステム等をまとったプロセスを動かすものだと考えれば理解が早いと思います。
- 最近では Mac や Windows でも Docker を動かせるようになってきました。
- コンテナ内部のボリューム(ファイルシステム/ディレクトリ/ファイル)は基本的に揮発性です。コンテナが削除された時点で、コンテナ内のプロセスが書き込んだログファイルなどもすべて消えてしまいます。永続ボリュームを使用するには、ホスト側のファイルシステムをアタッチし、ホスト側に書き込みます。

## Docker-docs-ja
https://docs.docker.jp/  


