@startuml

ユーザー -> webサーバー : ユーザー登録
webサーバー -> DBサーバー : ユーザー登録
DBサーバー -> DBサーバー : 登録処理
DBサーバー -> webサーバー : 登録結果

@enduml
