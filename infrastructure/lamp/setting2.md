
# システム管理者用のユーザーを作成する
必要な時だけ、root権限を使えるユーザーの作成


```
# ユーザーを作成
$ useradd username
```

```
# ユーザーのパスワードを設定
$ passwd username
```

```
# ユーザーをroot権限を取得できるwheelグループに追加する
$ usermod -aG wheel username
```

```
# ユーザーにsudo権限を付与する
$ visudo

# /で検索モード、"Allow root"で検索
# root  ALL=(ALL) ALLの下の行に
username ALL=(ALL) ALL
# を追加する
```
