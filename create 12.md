```uml
@startuml
[*] -> トップページ
会員情報 --> 会員登録済みトップページ : トップページをクリック/商品検索
ログイン --> トップページ : トップページをクリック/商品検索
ログイン : entry/id,passwordを入力
ログイン : do/ログイン認証
トップページ --> 買い物終了 : ログアウトをクリック
トップページ -> トップページ : 商品検索
トップページ -> 商品詳細 : 商品をクリック
ログイン -left-> 会員情報 : 会員登録をクリック
トップページ -left-> ログイン : ログインをクリック
トップページ --> カート内 : カートの中をクリック
トップページ : do/商品一覧を表示
商品詳細 --> カート内 : カートに入れるをクリック
商品詳細 --> トップページ : 前の画面に戻るをクリック
商品詳細 : do/商品説明を表示
カート内 -up-> トップページ : トップページをクリック/商品検索
カート内 -up-> 買い物終了 : ログアウトをクリック
カート内 -> 商品詳細 : 詳細へをクリック

state カート内{
[*] --> カート
カート -> 注文 : 注文をクリック
カート -> カート : 数量を変更/商品を削除
注文 --> カート : カートをクリック
state 注文{
[*] --> お届け先入力
お届け先入力 -> お届け先入力内容確認 : 入力内容確認をクリック
お届け先入力内容確認 -> お届け先入力 : 修正をクリック
お届け先入力内容確認 -> 購入完了 : 注文確定をクリック
}
}
state 会員登録済みカート内{
[*] --> 会員カート
会員カート -> 注文 : 注文をクリック
会員カート -> 会員カート : 数量を変更/商品を削除
注文 --> 会員カート : カートをクリック
state 注文{
[*] --> 購入
購入商品情報 -> 購入商品内容確認 : 内容確認をクリック
購入商品内容確認 -> 購入完了 : 注文確定をクリック
}
}
@enduml
```