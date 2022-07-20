# Dockerとは
https://www.tohoho-web.com/docker/about.html  

## Docker
--- 

- Dockerとは
- インストール >> 環境　Windows:docker desktop
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

## Dockerのチュートリアル
- イメージを管理する
- コンテナを管理する
- コンテナに接続する
- ホストのディレクトリをマウントする
- ホストの8080ポートをコンテナの80にマッピングする

```shell:イメージを管理する
# DockerHub からイメージを検索する
docker search centos

# イメージをダウンロードする
docker pull centos:7

# ダウンロード済みのイメージ一覧を表示する
docker images

# イメージを削除する
docker rmi centos:7
```

```shell:コンテナを管理する
# コンテナを起動する
docker run -d -it --name cont1 centos:7

# コンテナの一覧を表示する (-a は停止中もすべて)
docker ps -a

# コンテナを開始・停止・再起動・削除・リネームする
docker start cont1
docker stop cont1
docker restart cont1
docker rm cont1
docker rename cont1 cont2
```

コンテナ起動(run)時には下記などのオプションを指定することができます。  


|オプション	|説明|
|---|---|
|-d	|コンテナのメインプロセスを端末からデタッチします。|
|-i	|コンテナの標準入力を開いたままにします。|
|-t	|端末を割り当てたままにします。|
|--name 名前	|コンテナ名を指定します。|
|-p hPort:cPort	|ホストOSのポート番号(hPort)を、コンテナ内のポート番号(cPort)にバインドします。(例: -p 8080:80)|
|-v hVolume:cVolume	|ホストのボリューム(hVolume)を、コンテナ内のボリューム(cVolume)にバインドします。(例: -v /var/cont1/app:/opt/app)|
|--rm	|コンテナのメインプロセス終了時にコンテナを自動的に削除します。|
  

- centos イメージなど、起動時に -it オプションをつけ、メインプロセスが /bin/bash 等であるコンテナに対しては、メインプロセスに直接アタッチすることができます。この場合、exit や Ctrl-D 等でぬけると、メインプロセス(＝コンテナ)自体が終了してしまします。
```shell:コンテナに接続する
# コンテナのメインプロセスにアタッチする
docker attach cont1
[root@db80ea8860ff /]# Ctrl-P Ctrl-Q   デタッチするには Ctrl-P Ctrl-Q を押す
```
  
- httpd イメージなど、メインプロセスが httpd 等のコンテナの場合、メインプロセスとは別に、もう一つ別の /bin/bash 等を起動して、それにアタッチすることも可能です。この場合、exit や Ctrl-D で抜けても /bin/bash が終了するのみで、メインプロセス(＝コンテナ)は終了しません。
```shell:
# コンテナにもうひとつ別の /bin/bash を起動して接続する
docker exec -it cont1 /bin/bash
[root@db80ea8860ff /]# exit
```


```shell:ホストのディレクトリをマウントする
# SELinuxを無効化する
vi /etc/selinux/config
SELINUX=disabled

```shell:ホストの8080ポートをコンテナの80にマッピングする
docker run -d -it --name cont1 -p 8080:80 centos:centos6
```


# setenforce 0

-vオプションでホストの /mnt/cont1 をコンテナの /mnt にマウントする
# docker run -d -it --name cont1 -v /mnt/cont1:/mnt centos:centos6
```

## dockerコマンド

```console
# コンテナ作成
run image - コンテナを作成する(起動状態で)
create image - コンテナを作成する(停止状態で)

# コンテナ一覧
ps - コンテナの一覧を表示する
stats - コンテナのリソース使用状況一覧を表示する

# コンテナ操作(1)
rm container - コンテナを削除する
start container - コンテナを開始する
stop container - コンテナを停止する
kill container - コンテナを強制停止する
restart container - コンテナを再起動する
pause container - コンテナ上のプロセスを一時停止する
unpause container - コンテナ上のプロセスを再開始する

# コンテナ操作(2)
exec container - コンテナ内でプロセスを起動する
attach container - コンテナに標準入出力をアタッチする

# コンテナ操作(3)
cp srcfile dstfile - コンテナに(から)ファイルをコピーする
rename container newname - コンテナ名を変更する
update container - コンテナの設定(CPU数等)を変更する

# コンテナ詳細
logs container - コンテナのログを表示する
port container - コンテナのポートマッピングを表示する
top container - コンテナ内のプロセスの一覧を表示する

# Dockerレジストリ関連
pull name - レジストリからイメージをダウンロードする
push name - レジストリにイメージをアップロードする
search term - Dockerレジストリからイメージを検索する
login - Dockerレジストリにログインする
logout - Dockerレジストリからログアウトする

# イメージ管理
images - イメージの一覧を表示する
rmi images - イメージを削除する
history image - イメージのヒストリを表示する
commit container - コンテナからイメージを作成する
tag image NEWimage - イメージにタグをつける
build dockerfile - イメージをビルドする
trust - イメージに署名する

# ボリューム管理
volume - Dockerボリュームを管理する

# ネットワーク管理
network - Dockerネットワークを管理する

# インポート／エクスポート／セーブ／ロード
export container - コンテナをファイルにエクスポートする
import file - エクスポートファイルをイメージとしてインポートする
save image - イメージをファイルにセーブする
load file - セーブファイルをイメージとしてロードする

# Docker Swarm(クラスタリング)関連
swarm - Swarmを管理する
node - Swarmノードを管理する
stack - Swarmスタックを管理する
secret - Swarmシークレットを管理する
service - Swarmサービスを管理する

# その他
version - バージョンを表示する
help - ヘルプを表示する
info - Dockerに関するシステム情報を表示する
inspect - 様々なDockerオブジェクトの詳細情報を表示する
diff container - コンテナ生成後の更新ファイルを表示する
wait container - コンテナの停止を待ち合わせる
events - Dockerエンジンのイベントを監視・表示する
image - イメージ管理系コマンドを実行する
container - コンテナ管理系コマンドを実行する
builder - イメージビルド系コマンドを実行する
system - システム管理系コマンドを実行する
config - コンフィグを管理する
context - ビルド時のコンテキストを管理する
engine - Dockerエンジンを管理する
plugin - プラグインを管理する
```

### オプション(OPTIONS)
```console
--config string
-c, --context string
-D, --debug
-H, --host list
-l, --log-level string
-v, --version
--tls
--tlscacert string
--tlscert string
--tlskey string
--tlsverify
```

### docker run/create


### docker ps/stats


### docker rm/start/stop...


### docker exec/attach


### docker cp/rename/update


### docker logs/port/top


### docker pull/push/search/login/logout


### docker images/rmi/history/commit/tag/build/trust


### docker volume


### docker network


### docker export/import/save/load
