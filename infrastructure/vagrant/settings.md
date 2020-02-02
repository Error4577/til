# 環境設定

## VirtualBoxのインストール
[VirtualBoxのダウンロードページ](https://www.virtualbox.org/wiki/Downloads)


## Vagrantのインストール
以下のリンクからVagrantのパッケージをダウンロードしてインストール  
[Vagrantのダウンロードページ](https://www.vagrantup.com/downloads.html)

インストールが完了するとvagrantコマンドが使用出来るようになる。

```
$ vagrant -v
Vagrant 2.2.7
```

# 設定フィアルの準備
## Boxes(Boxファイル)のインストール

Boxファイルは`vagrant box add`コマンドで追加する
```
$ vagrant box add NAME URL
```

NAMEはBoxファイル名。  
ホストPC内でBoxファイルを識別する名前。  
ホストPC内で一意であれば任意の名前を付けることができる。  

URLはBoxファイルが配置されているURL、またはファイルパスを指定する。  
Boxファイルは自分で作成することもできるし、公開されている物を使用することもできる。  

[vagrantbox.es](https://www.vagrantbox.es/)に様々なOS、プロバイダのBoxファイルが公開されている。  
利用したいOS、プロバイダのBoxファイルのURLをコピーして利用できる。  
ただし殆どのBoxファイルはVagrant公式ではなく、有志が作成したものであることは注意。  

## Boxファイルの追加
VirtualBox用CentOS6.4のBoxファイルを追加する  
以下のコマンドを実行する。(通信環境によっては結構時間掛かるので注意)  

```
$ vagrant box add centos64_gihyo https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box

==> box: Successfully added box 'centos64_gihyo' (v0) for 'virtualbox'!
```

## Boxファイルの確認
`vagrant box list`コマンドを実行するとBoxファイルの一覧が表示される。

```
$ vagrant box list
```

## Boxファイルの削除
Boxファイルを削除するには、`vagrant box remove`コマンドを実行する

```
$ vagrant box remove centos64_gihyo
```

# Vagrantfileの作成
Vagrantfileには、起動する仮想マシンのスペック、プロビジョニング内容などを記述する。  
Vagrantはこのファイルを読み込み、仮想マシンを起動する。  
VagrantfileはRubyで記述する。  

## Vagrantfileの生成
Vagrantfileを生成するには`vagrant init`コマンドを実行する。  
`vagrant init`コマンドにBoxファイル名を指定するとそのBoxファイルを利用するVagrantfileが生成される。  

```
$ vagrant init centos64_gihyo
```




