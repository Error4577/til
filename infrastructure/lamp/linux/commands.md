## `shutdown`コマンド

今すぐシャットダウン
```
$ shutdown -h now
```

時間を指定してシャットダウン
```
$ shutdown -h 13:00
```

10分後にシャットダウン
```
$ shutdown -h +10
```

ログインしている他のユーザーに、メッセージだけを表示する
```
$ shutdown -k "Please logout"
```

ログインしている他のユーザーに、メッセージを表示して、10分後にシャットダウン
```
$ shutdown -h +10 "Please logout within 10 minites"
```

## `history`コマンド
コマンド履歴を表示
```
$ history

```
