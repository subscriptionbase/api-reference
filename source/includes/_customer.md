# 顧客（Customer）

「顧客(Customer)」は、貴社サービスを購読する契約者を示します。<br>

顧客モデルの契約者情報は、請求書や利用明細書を発行する際などに請求宛先として記載されます。

## 顧客を作成する

> リクエスト

```shell
curl -X POST https://api.subscriptionbase.io/v1/customers/\
  -H Authorization: Bearer <アクセストークン>\
  -d udid=customer_id_in_your_service\
  -d email=email@example.com
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Customer::create(array(
    'udid'  => 'customer_id_in_your_service',
    'email' => 'email@example.com',
));
```

> レスポンス

```json
{
  "id"               : "cus_01da62ff7mx3brkprjrjfve597",
  "object_name"      : "customer",
  "udid"             : "customer_id_in_your_service",
  "email"            : "email@example.com",
  "company"          : null,
  "department"       : null,
  "position"         : null,
  "name"             : null,
  "postal_code3"     : null,
  "postal_code4"     : null,
  "prefecture"       : null,
  "address_city"     : null,
  "address_town"     : null,
  "address_number"   : null,
  "address_building" : null,
  "archive_at"       : null,
  "update_at"        : "2019-05-06T16:59:35+0900",
  "create_at"        : "2019-05-06T16:59:35+0900"
}
```

udid（ユーザー定義ID）または、メールアドレスを指定すると、該当項目で検索が可能になります。

### HTTP Request

`POST https://api.subscriptionbase.io/v1/customers/`

### リクエストデータ
引数 | データ型（最大） | 必須 |詳細
---- | ---- | -- | -----------
udid | String（255） | - | 任意の顧客ID。複数の顧客に同一のudidを指定することはできません。
email | String(254) | - | メールアドレス。複数の顧客に同一のメールアドレスを指定することはできません。
company | String(35) | - | 会社名
department | String(35) | - | 部署名
position | String(35) | - | 肩書・役職
name | String(30) | - | 契約者氏名
postal_code3 | Integer(3) | - | 郵便番号の前半３桁
postal_code4 | Integer(4) | - | 郵便番号の後半4桁
prefecture | String(4) | - | 都道府県
address_city | String(20) | - | 市町村名
address_town | String(30) | - | 町域名
address_number | String(30) | - | 丁目・番地
address_building | String(35) | - | 建物名・階数・部屋番号


## 顧客を取得する

> リクエスト

```shell
curl https://api.subscriptionbase.io/v1/customers/<ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Customer::retrieve(<ID>);
```

> レスポンス

```json
{
  "id"               : "cus_01da62ff7mx3brkprjrjfve597",
  "object_name"      : "customer",
  "udid"             : "customer_id_in_your_service",
  "email"            : "email@example.com",
  "company"          : null,
  "department"       : null,
  "position"         : null,
  "name"             : null,
  "postal_code3"     : null,
  "postal_code4"     : null,
  "prefecture"       : null,
  "address_city"     : null,
  "address_town"     : null,
  "address_number"   : null,
  "address_building" : null,
  "archive_at"       : null,
  "update_at"        : "2019-05-06T16:59:35+0900",
  "create_at"        : "2019-05-06T16:59:35+0900"
}
```

顧客IDから顧客情報を取得します。

### HTTP Request

`GET https://api.subscriptionbase.io/v1/customers/<ID>/`

### レスポンスデータ
引数 | データ型（最大）| 詳細
---- | ---- | -----------
id | String（30) | 顧客ID
object_name | String(255) | オブジェクト名称
udid | String（255) | ユーザー定義ID
email | String(254) | メールアドレス
company | String(35) | 会社名
department | String(35) | 部署名
position | String(35) | 肩書・役職
name | String(30) | 契約者氏名
postal_code3 | Integer(3) | 郵便番号の前半３桁
postal_code4 | Integer(4) | 郵便番号の後半4桁
prefecture | String(4) | 都道府県
address_city | String(20) | 市町村名
address_town | String(30) | 町域名
address_number | String(30) | 丁目・番地
address_building | String(35) | 建物名・階数・部屋番号


## 顧客リストを取得する

> リクエスト

```shell
curl https://api.subscriptionbase.io/v1/customers/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Customer::all(array(
  'page' => 1,
));
```

> レスポンス

```json
{
  "object_name" : "list",
  "url"         : "https://api.subscriptionbase.io/v1/customers/",
  "has_more"    : false,
  "count"       : 1,
  "data"        : [
    {
      "id"               : "cus_01da62ff7mx3brkprjrjfve597",
      "object_name"      : "customer",
      "udid"             : "customer_id_in_your_service",
      "email"            : "email@example.com",
      "company"          : null,
      "department"       : null,
      "position"         : null,
      "name"             : null,
      "postal_code3"     : null,
      "postal_code4"     : null,
      "prefecture"       : null,
      "address_city"     : null,
      "address_town"     : null,
      "address_number"   : null,
      "address_building" : null,
      "archive_at"       : null,
      "update_at"        : "2019-05-06T16:59:35+0900",
      "create_at"        : "2019-05-06T16:59:35+0900"
    }
  ]
}
```

顧客のリストを取得します。

### HTTP Request

`GET https://api.subscriptionbase.io/v1/customers/`


## 顧客を削除する

> リクエスト

```shell
curl -X DELETE https://api.subscriptionbase.io/v1/customers/<ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Customer;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$customer = Customer::retrieve(<ID>);
$customer->delete();
```

> レスポンス

```json
{
  "id"         : "cus_01da62ff7mx3brkprjrjfve597",
  "archive_at" : "2019-05-06T16:59:35+0900",
}
```

### HTTP Request

`DELETE https://api.subscriptionbase.io/v1/customers/<ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | 顧客ID
