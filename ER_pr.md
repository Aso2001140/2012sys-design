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
entity "トップページ" as customer <m_customers> <<M,MASTER_MARK_COLOR>> {
        ログイン
        新規登録
        商品一覧
        カテゴリ一覧
        順番指定
    }

 entity "顧客テーブル" as order <d_purchase> <<T,TRANSACTION_MARK_COLOR>>{
    +登録者名[PK]
    +パスワード[PK]
    --
    カート情報
    ポイント情報
    ガチャ
    }
    
  entity "ガチャ" as lottery <d_purchase> <<T,TRANSACTION_MARK_COLOR>>{
    +登録者名[PK]
    +パスワード[PK]
    --
    ポイント情報
    }
    
 entity "購入詳細テーブル" as order_detail <d_purchase_detail> <<T,TRANSACTION_MARK_COLOR>>{
    +登録者情報[PK]
    +カート情報[PK]
    --
    # 商品情報[FK]
    商品金額
    商品合計金額
    }
    
 entity "受注" as order_main <d_purchase_detail> <<T,TRANSACTION_MARK_COLOR>>{
    +登録者情報[PK]
    +受注番号[PK]
    --
    受注情報
    }
    
 entity "受注明細" as order_sub <d_purchase_detail> <<T,TRANSACTION_MARK_COLOR>>{
    +登録者情報[PK]
    +受注番号[PK]
    --
    受注情報明細
    }
    
    
    entity "商品詳細" as items <m_items> <<M,MASTER_MARK_COLOR>> {
        + 商品番号 [PK]
        --
        商品名
        金額
        +カテゴリー番号[FK]
        イメージ写真
        商品説明
    }

    entity "カテゴリー" as category <m_category> <<M,MASTER_MARK_COLOR>> {
        + カテゴリー番号[PK]
        --
        カテゴリー名
    }
    
    
    customer       |o-ri-o{     order 
    
    order         　||-ri-||      lottery

    order          ||-ri-|{     order_detail 

    order_detail    }-do-||     items 

    items          }o-le-||     category 
    

@enduml
```
