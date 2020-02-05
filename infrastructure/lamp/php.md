# PHP7のインストール

今回はPHP 7.1系の最新をインストールする。  
```
$ sudo yum --enablerepo=remi-php71 install php php-devel php-mysql php-gd php-mbstring
```

インストールが完了したら、Apacheを再起動する
```
$ sudo systemctl restart httpd
```

## PHPの動作確認

```
$ sudo vi /var/www/html/index.php
```

index.phpに以下のように記述する
```
<?php
phpinfo();
```

ブラウザを開き、IPアドレスの末尾に/index.phpと入力し開くと、下図のようにPHPの設定情報やバージョンなどが確認できる
[![Image from Gyazo](https://i.gyazo.com/308649174c04707b0ad12762f496f75a.png)](https://gyazo.com/308649174c04707b0ad12762f496f75a)

これらの情報はWeb上に公開するとセキュリティホールに成りかねない為、本番環境でphpinfo()関数を使う場合はアクセス制限を設ける必要がある。  

## PHPでHello World

index.phpから`phpinfo()`関数を削除し、下記を追記する

```
echo 'Hello World';
```

ブラウザから再びIPアドレスの末尾に/index.phpと入力して開き、Hello Worldと表示されていればOK
[![Image from Gyazo](https://i.gyazo.com/acd44aa5b867f36e3ace460fcd3ab968.png)](https://gyazo.com/acd44aa5b867f36e3ace460fcd3ab968)

