# 支払い方法（PaymentMethod）
支払い方法（PaymentMethod）は、顧客と請求方法に紐づく代金清算に必要な情報を示します。<br>
請求方法の設定と請求方法IDの取得は、あらかじめ[コンソール画面](http://app.subscriptionbase.io/billing-methods/)で行います。

## 支払い方法を作成する

顧客の支払い方法を作成します。

> リクエスト

```shell
curl -X POST https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/\
  -H Authorization: Bearer <アクセストークン>\
  -d billing_method=blm_01da53n9f4c752cxsmp5kgyv4q\
  -d is_primary=true
  -d email_address[mail_to]=mailto@example.com
  -d email_address[name]=customer_name
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<顧客ID>);
$customer->payment_methods->create(array(
  "billing_method" => "blm_01da53n9f4c752cxsmp5kgyv4q",
  "is_primary"     => true,
  "email_address"  => array(
    "mail_to" => "mailto@example.com",
    "name"    => "customer_name",
  )
));
```

> レスポンス

```json
{
  "id"             : "pym_01daaj6g6kbbtd29g38wqyt4k6",
  "object_name"    : "paymentmethod",
  "customer"       : "cus_01daaj6g58fe7755ytqzetfd4g",
  "billing_method" : "blm_01daaj6g46zzfr9c56hfbgj73e",
  "is_primary"     : true,
  "email_address": {
    "mail_to"    : "mailto@example.com",
    "mail_cc"    : null,
    "mail_bcc"   : null,
    "company"    : null,
    "department" : null,
    "position"   : null,
    "name"       : "customer_name"
  },
  "archive_at" : null,
  "update_at"  : "2019-05-08T10:51:16+0900",
  "create_at"  : "2019-05-08T10:51:16+0900"
}
```

### HTTP Request

`POST https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/`

### リクエストデータ
リクエストデータは、請求方法の設定に応じた内容で指定します。
例えば、請求方法で請求書をEメール送信する設定をした場合には、「email_address」オブジェクトの指定が必須になります。

引数 | データ型（最大） | 必須 |詳細
---- | ---- | -- | -----------
billing_method | String(30) | ◯ | 請求方法ID
is_primary | Boolean | ◯ | 請求に使用する場合、Trueを指定。
email_address | Object | - | Eメール通知設定。請求方法でEメール通知を設定した場合は必須。

引数 | データ型（最大） | 必須 |詳細
---- | ---- | -- | -----------
email_address[mail_to] | String(254) | ◯ | 宛先メールアドレス
email_address[mail_cc] | String(1000) | - | CC送信メールアドレス。複数指定の場合、カンマ区切り文字列。
email_address[mail_bcc] | String(1000) | - | BCC送信メールアドレス。複数指定の場合、カンマ区切り文字列。
email_address[company] | String(35) | - | 会社名（本文差し込み項目）
email_address[department] | String(35) | - | 部署名（本文差し込み項目）
email_address[position] | String(35) | - | 肩書・役職（本文差し込み項目）
email_address[name] | String(30) | - | 氏名（本文差し込み項目）

* 「is_primary」... 支払い方法の登録が複数ある場合、更新時にis_primary=Trueを指定すると、他の支払い方法のis_primaryはFalseに上書きされます。また、支払い方法の登録が一つの場合、is_primaryは常にTrueになります。


## 支払い方法を取得する

顧客が保有する支払い方法を取得します。

> リクエスト

```shell
curl -X GET https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<顧客ID>);
$customer->payment_methods->retrieve(<支払い方法ID>);
```

> レスポンス

```json
{
  "id"             : "pym_01daaj6g6kbbtd29g38wqyt4k6",
  "object_name"    : "paymentmethod",
  "customer"       : "cus_01daaj6g58fe7755ytqzetfd4g",
  "billing_method" : "blm_01daaj6g46zzfr9c56hfbgj73e",
  "is_primary"     : true,
  "email_address": {
    "mail_to"    : "mailto@example.com",
    "mail_cc"    : null,
    "mail_bcc"   : null,
    "company"    : null,
    "department" : null,
    "position"   : null,
    "name"       : "customer_name"
  },
  "archive_at" : null,
  "update_at" : "2019-05-08T10:51:16+0900",
  "create_at" : "2019-05-08T10:51:16+0900"
}
```

### HTTP Request

`GET https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法ID>/`

### レスポンスデータ

引数 | データ型（最大）|詳細
---- | ---- | -- | -----------
id | String(30) | 支払い方法ID
object_name | String(255) | オブジェクト名称
customer | String(30) | 顧客ID
billing_method | String(30) | 請求方法ID
is_primary | Boolean | 請求で利用する支払い方法か
email_address | Object | Eメール通知設定。請求方法でEメール通知を設定した場合に発生。

引数 | データ型（最大) |詳細
---- | ---- | -- | -----------
email_address[mail_to] | String(254) | 宛先メールアドレス
email_address[mail_cc] | String(1000) | CC送信メールアドレス。複数指定の場合、カンマ区切り文字列。
email_address[mail_bcc] | String(1000) | BCC送信メールアドレス。複数指定の場合、カンマ区切り文字列。
email_address[company] | String(35) | 会社名（本文差し込み項目）
email_address[department] | String(35) | 部署名（本文差し込み項目）
email_address[position] | String(35) | 肩書・役職（本文差し込み項目）
email_address[name] | String(30) | 氏名（本文差し込み項目）


## 支払い方法リストを取得する

顧客が保有する全ての支払い方法を取得します。

> リクエスト

```shell
curl -X GET https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<顧客ID>);
$customer->payment_methods->all();
```

> レスポンス

```json
{
  "object_name" : "list",
  "url"         : "https://api.subscriptionbase.io/v1/customers/cus_01daaj6g58fe7755ytqzetfd4g/payment-methods/",
  "has_more"    : false,
  "count"       : 1,
  "data"        : [
    {
      "id"             : "pym_01daaj6g6kbbtd29g38wqyt4k6",
      "object_name"    : "paymentmethod",
      "customer"       : "cus_01daaj6g58fe7755ytqzetfd4g",
      "billing_method" : "blm_01daaj6g46zzfr9c56hfbgj73e",
      "is_primary"     : true,
      "email_address": {
        "mail_to"    : "mailto@example.com",
        "mail_cc"    : null,
        "mail_bcc"   : null,
        "company"    : null,
        "department" : null,
        "position"   : null,
        "name"       : "customer_name"
      },
      "archive_at" : null,
      "update_at"  :"2019-05-08T10:51:16+0900",
      "create_at"  : "2019-05-08T10:51:16+0900"
    }
  ]
}
```

### HTTP Request

`GET https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/`


## 支払い方法を選択する

顧客が料金精算に使用する支払い方法を選択します。<br>
支払いIDを指定してこの操作を実行すると、is_primary=trueが設定され、その他の支払い方法はis_primary=falseに変更されます。

> リクエスト

```shell
curl -X GET https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法ID>/primary/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<顧客ID>);
$paymentMethod = $customer->payment_methods->retrieve(<支払い方法ID>);
$paymentMethod->primary();
```

> レスポンス

```json
{
  "id"             : "pym_01daaj6g6kbbtd29g38wqyt4k6",
  "object_name"    : "paymentmethod",
  "customer"       : "cus_01daaj6g58fe7755ytqzetfd4g",
  "billing_method" : "blm_01daaj6g46zzfr9c56hfbgj73e",
  "is_primary"     : true,
  "email_address": {
    "mail_to"    : "mailto@example.com",
    "mail_cc"    : null,
    "mail_bcc"   : null,
    "company"    : null,
    "department" : null,
    "position"   : null,
    "name"       : "customer_name"
  },
  "archive_at" : null,
  "update_at" : "2019-05-08T10:51:16+0900",
  "create_at" : "2019-05-08T10:51:16+0900"
}
```

### HTTP Request

`POST https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法>/primary/`


## 支払い方法を削除する

顧客が保有する支払い方法を削除します。<br>
支払い方法が使用設定（is_primary=true）されている場合、削除リクエストはエラーになります。

> リクエスト

```shell
curl -X DELETE https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<顧客ID>);
$paymentMethod = $customer->payment_methods->retrieve(<支払い方法ID>);
$paymentMethod->delete();
```

> レスポンス

```json
{
  "id"         : "pym_01daaj6g6kbbtd29g38wqyt4k6",
  "archive_at" : "2019-05-06T16:59:35+0900",
}
```

### HTTP Request

`DELETE https://api.subscriptionbase.io/v1/customers/<顧客ID>/payment-methods/<支払い方法ID>/`
