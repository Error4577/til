# Day1対応
AWSアカウントの作成後に以下の4つの対応を実施する
- ルートアカウントの利用を停止する
- 他要素認証を有効にする
- AWS CloudTrailを有効化する
- AWSの請求レポートを有効化する

IAMのダッシュボード上で下図のように5つの項目について緑色のチェックマークが付いていればOK
[![Image from Gyazo](https://i.gyazo.com/455bf7f4670efd42a760c8a348609e15.png)](https://gyazo.com/455bf7f4670efd42a760c8a348609e15)

## AWS CloudTrail
デフォルトで有効になっている  
データ操作、データイベントについては無効になっている  

[証跡の作成]を押してログ取得の設定を行う  
[![Image from Gyazo](https://i.gyazo.com/e53129a8c7bd04c7a9320bc25a16cedf.png)](https://gyazo.com/e53129a8c7bd04c7a9320bc25a16cedf)

証跡名を入力する
[![Image from Gyazo](https://i.gyazo.com/8e307758ad89290dd2aff6299aa236dc.png)](https://gyazo.com/8e307758ad89290dd2aff6299aa236dc)

logを保管するS3バケットを作成する。  
S3バケット名はグローバルに一意でなければならない  
[![Image from Gyazo](https://i.gyazo.com/a35a3dd024fa4abd9c8262633d4456e8.png)](https://gyazo.com/a35a3dd024fa4abd9c8262633d4456e8)

ログの取得が開始される  
[![Image from Gyazo](https://i.gyazo.com/2be6f2d00d18d14ceef5ec0b23abd4d3.png)](https://gyazo.com/2be6f2d00d18d14ceef5ec0b23abd4d3)


## 請求状況
今後rootユーザーから請求額等は確認しないようにする。  
rootユーザーでログインし、右上から[マイアカウント]ページに移動  
[![Image from Gyazo](https://i.gyazo.com/6d4b56d7b3e7906c5b96e3f6336a6dda.png)](https://gyazo.com/6d4b56d7b3e7906c5b96e3f6336a6dda)

真ん中までスクロールすると[IAM ユーザー/ロールによる請求情報へのアクセス]という項目があるので、左上の[編集]をクリックする  
[![Image from Gyazo](https://i.gyazo.com/463515a8d88d003452dff8e93f8d081d.png)](https://gyazo.com/463515a8d88d003452dff8e93f8d081d)

[IAM アクセスのアクティブ化]にチェックを入れ、[更新]を押す  
[![Image from Gyazo](https://i.gyazo.com/970cb150897759dd12105ca06d1fd9a1.png)](https://gyazo.com/970cb150897759dd12105ca06d1fd9a1)

IAMユーザーで再度ログインし、請求ダッシュボードに移動すると、rootユーザーと同様に請求額が確認できる  

