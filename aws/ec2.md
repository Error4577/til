

ダウンロードしたpemファイルを~/.sshに移動する
```
$ mv ~/Downloads/***.pem ~/.ssh/
```

所有しているユーザーのみ読み取り可能にする
```
$ chmod 400 ~/.ssh/***.pem
```

EC2インスタンスにssh接続する
```
$ ssh -i ~/.ssh/***.pem ec2-user@***.***.***.***
```

