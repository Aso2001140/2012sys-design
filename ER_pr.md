```startuml
@startuml

!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue

'グラデーションさせる場合 #xx-xx
!define MAIN_ENTITY #MintCream-MistyRose


skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}


package "ECサイト" as target_system {
entity "顧客テーブル" as user <t_user> <<T,TRANSACTION_MARK_COLOR>> {
        +ユーザID[PK]
        住所
        電話番号
        メール
        ログイン情報
        性別
        パスワード
        ポイント情報
    }

 entity "ガチャ" as lottery <lottery> <<M,MASTER_MARK_COLOR>>{
    +ユーザID[PK]
    --
    #景品ID[FK]
    }
    
  entity "ガチャ一覧" as all_prize <all_prize> <<M,MASTER_MARK_COLOR>>{
    +景品ID[PK]
    }
    
 entity "購入詳細テーブル" as order <t_order> <<T,TRANSACTION_MARK_COLOR>>{
    +ユーザID[PK][FK]
    --
    # 商品ID[FK]
    購入日
    }
    
 entity "定期便" as order_sub <t_order_sub> <<T,TRANSACTION_MARK_COLOR>>{
    +ユーザID[PK][FK]
    --
    # 商品ID[FK]
    お届け日
    }
    
 entity "商品テーブル" as items <t_items> <<T,TRANSACTION_MARK_COLOR>>{
    +商品ID[PK]
    --
    商品名
    商品画像
    商品値段
    商品内容
    在庫数
    カテゴリID
    }
    
    
    entity "カテゴリ" as category <category> <<M,MASTER_MARK_COLOR>> {
        + カテゴリID [PK]
        --
        # 商品ID[FK]
    }
    
    
    user          |o-ri-o{     lottery 
    
    lottery         }-ri-||      all_prize

    user          |o-ri-o{     order
    
    order         }-do-||      order_sub     
    
    order         }-do-||      items

    items         }-do-||      category 
    

@enduml
```
