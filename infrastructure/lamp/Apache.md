# Apacheのインストール

yumを使ってインストールする
```
$ sudo yum install httpd
```

Apacheの2.4系がインストールされていればOK
```
$ httpd -v
Server version: Apache/2.4.6 (CentOS)
Server built:   Aug  8 2019 11:41:18
```

## OS再起動時に自動でApacheが起動するようにする

```
$ sudo systemctl enable httpd
```

再起動後にactive(running)になっていればOK

```
$ systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
   Active: active (running) since 火 2020-02-04 21:25:55 JST; 7h ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 1102 (httpd)
   Status: "Total requests: 0; Current requests/sec: 0; Current traffic:   0 B/sec"
   CGroup: /system.slice/httpd.service
           ├─1102 /usr/sbin/httpd -DFOREGROUND
           ├─1130 /usr/sbin/httpd -DFOREGROUND
           ├─1131 /usr/sbin/httpd -DFOREGROUND
           ├─1132 /usr/sbin/httpd -DFOREGROUND
           ├─1133 /usr/sbin/httpd -DFOREGROUND
           └─1134 /usr/sbin/httpd -DFOREGROUND

 2月 04 21:25:54 localhost.localdomain systemd[1]: Starting The Apache HTTP Server...
 2月 04 21:25:55 localhost.localdomain httpd[1102]: AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain. Set the 'ServerNam...this message
 2月 04 21:25:55 localhost.localdomain systemd[1]: Started The Apache HTTP Server.
Hint: Some lines were ellipsized, use -l to show in full.
```


## Apacheの設定
### ファイアウォールの設定
ファイアウォール・・・サーバーに対する不正なアクセスを防ぐ仕組み  

httpの通信に使うポート80を開ける
```
$ sudo firewall-cmd --permanent --zone=public --add-service=http
success
```

httpsの通信に使うポート443を開ける
```
$ sudo firewall-cmd --permanent --zone=public --add-service=https
success
```

firewallをリロードして設定を反映させる
```
$ sudo firewall-cmd --reload
success
```

SELinux関連の設定を行う  

SELinuxについて少し調べてみた
- 通常のパーミッションより細かくポリシーを定義できる(rootユーザーの権限を弱めることもできる)
- セキュリティが高いが故に余計な挙動が起こって、むしろ管理しにくいというケースがある。
- 無効化していてもサーバーとして問題無く動作する

以上の理由から実際の現場でもSELinuxを無効化するのはよくあることらしい。  

でも以下のような記事もあるから後々勉強したい  
[そろそろSELinux を有効にしてみませんか？](https://www.slideshare.net/atsushimitsu/selinux-87020074)

SELinuxが有効になっていることの確認  

```
$ getenforce
Enforcing
```

selinuxの設定ファイルをエディタで開く
```
$ sudo vi /etc/selinux/config
```

設定ファイルの`SELINUX=`の箇所を変更する
```
SELINUX=enforcing
↓
SELINUX=disabled
```

SELinuxの設定を反映させる為にOSを再起動する
```
$ sudo reboot
```

OS再起動、再ログインし、以下のコマンドを実行  
Disabledと返ってくれば、SELinuxが無効になっている
```
$ getenforce
Disabled
```

## Apacheの動作確認

VMに割り当てられているIPアドレスを確認する  

```
$ ip address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:45:49:af brd ff:ff:ff:ff:ff:ff
    inet 10.183.85.2/8 brd 10.255.255.255 scope global noprefixroute dynamic enp0s3
       valid_lft 85612sec preferred_lft 85612sec
    inet6 fe80::a00:27ff:fe45:49af/64 scope link 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:98:91:55 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.101/24 brd 192.168.56.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe98:9155/64 scope link 
       valid_lft forever preferred_lft forever
```

今回の環境では`10.183.85.2`がVMに割り当てられているIPアドレス。  
ブラウザにこのIPアドレスをコピペして開いてみる  
Apacheのテストページが表示されていれば、正常にApacheが動作していることが確認できる。  
[![Image from Gyazo](https://i.gyazo.com/1ae0b83e2e850410568c16c55e91813e.jpg)](https://gyazo.com/1ae0b83e2e850410568c16c55e91813e)


DocumentRootに当たるディレクトリを確認する  
```
$ less /etc/httpd/conf/httpd.conf
```

`/`で検索モードに移行、"DocumentRoot"と入力しエンターキーを押下。  
以下のようにDocumentRootに当たるディレクトリのパスが確認できる  
```
DocumentRoot "/var/www/html"
```

次にDocumentRootにindex.htmlを配置する  
```
$ vi /var/www/html/index.html
```

`Hello Apache`等と入力し、`:wq`で保存  
この時点ではindex.htmlの所有者はrootユーザーなので、所有者をApacheに変更する

```
$ sudo chown apache:apache /var/www/html/index.html 
```

ブラウザを開き、VMのIPアドレスを入力して開く  
[![Image from Gyazo](https://i.gyazo.com/2d2ba87baf869bc84b71cb561c3d90ae.png)](https://gyazo.com/2d2ba87baf869bc84b71cb561c3d90ae)

Hello Apacheと表示されていればOK  





