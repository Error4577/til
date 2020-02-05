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
