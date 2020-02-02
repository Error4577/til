# ディレクトリ構造
Linuxのディレクト構造  

```
/
┣━etc
┣━boot
┣━var
┃ ┗━log
┣━bin
┣━dev
┣━usr
┃ ┗━bin
┗━home
```

/ ルートディレクトリ
ファイルシステムの頂点に当たるディレクトリ

/etc
システム管理用・各種ソフトウェアの設定ファイルを保存

/boot
rootユーザーのホームディレクトリ

/var
システム運用中にファイルサイズが変化するファイルを保存

/var/log
システムやアプリケーションのログファイルを保存

/bin
一般ユーザー、管理者が使用するコマンドが配置

/dev
デバイスファイルを保存

/usr
ユーザーが共有するファイルを保存。
ユーティリティ、ライブラリ、コマンド等を配置

/home
ユーザーのホームディレクトリが配置
