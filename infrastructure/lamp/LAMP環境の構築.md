# LAMP環境の構築
ローカルPC上に作成した仮想マシン上にLAMP環境を構築する

## LAMPとは
- L : Linux ・・・ OS
- A : Apache ・・・ Webサーバ
- M : MySQL ・・・ リレーショナルデータベース
- P : PHP ・・・ プログラミング言語


```
使用するバージョン
CentOS 7
Apache 2.4
MySQL 5.7
PHP 7
```

## yum(ヤム, Yellowdog Updater Modified)
- パッケージ管理システム
- 各種ソフトウェアをインストール、アップデート、削除
- RPM(RedHat Package Manager)と互換性がある。Fedora CoreやCentOSなどRPMを利用するディストリビューションで使われる

## リポジトリ
- リポジトリ追加で最新のソフトをyumでインストールできるようになる。
- リポジトリとは、ソフトウェアが格納されているデータベースのようなもの

### EPEL(Extra Package for Enterprise Linux)リポジトリ
- RedHat Enterprise Linux向けの追加パッケージ
- Fedoraプロジェクトで有志によって作成されている

### Remiリポジトリ
- mysqlやPHPの新しいバージョンなどを集めているリポジトリ

### リポジトリの追加
インストールされているソフトウェアのアップデート
```
$ sudo yum update
```

epelリポジトリをインストールする
```
$ sudo yum install epel-release
```

remiリポジトリをインストールする
```
$ sudo yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

有効なリポジトリを確認する
```
$ yum repolist
```


