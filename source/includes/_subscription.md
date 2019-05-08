# 購読契約（Subscription）

「購読契約（Subscription）」は、顧客が購読する各種プランの契約情報を示します。<br>
各種プランの設定・ID取得は、[コンソール画面](http://app.subscriptionbase.io/products/)で行います。


## 購読契約を作成する

> リクエスト

```shell
curl -X POST https://api.subscriptionbase.io/v1/subscriptions/\
  -H Authorization: Bearer <アクセストークン>\
  -d customer=<顧客ID>\
  -d plan=<プランID>\
  -d start_at=2019-06-01T00:00:00+0900
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Subscription;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Subscription::create(array(
    'customer'  => <顧客ID>,
    'plan'      => <プランID>,
    'start_at'  => '2019-06-01T00:00:00+0900',
));
```

> レスポンス

```json
{
  "id"                : "sub_01daaym81nk191jk81rcra91hq",
  "object_name"       : "subscription",
  "trial_begin_at"    : "2019-06-01T00:00:00+0900",
  "contract_begin_at" : "2019-06-08T00:00:00+0900",
  "contract_end_at"   : "2019-07-08T00:00:00+0900",
  "last_payment_at"   : null,
  "next_payment_at"   : "2019-07-08T00:00:00+0900",
  "state"             : "active",
  "churn_at"          : null,
  "update_at"         : "2019-05-08T14:28:30+0900",
  "create_at"         : "2019-05-08T14:28:30+0900",
  "customer": {
    "id"               : "cus_01daaym803gvhdycjcky0hmx6t",
    "object_name"      : "customer",
    "udid"             : "90e342e0-bc4d-48cb-baf4-f93e139f4858",
    "email"            : "claytonsanders@banks.com",
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
    "update_at"        : "2019-05-08T14:28:29+0900",
    "create_at"        : "2019-05-08T14:28:29+0900"
  },
  "plan": {
    "id"              : "pln_01daaym808vm16e5eyar0pezdg",
    "object_name"     : "plan",
    "product"         : "prd_01daaym8051ej4z6rd54jckgtp",
    "name"            : "\u30d7\u30e9\u30f3\u540d",
    "public_name"     : "\u30d7\u30e9\u30f3\u516c\u958b\u540d",
    "contract_period" : "m1",
    "update_method"   : "repeat",
    "payment_term"    : "m1",
    "start_method"    : "trial",
    "trial_days"      : 7,
    "charge": {
      "charge_type" : "volume",
      "meter": {
        "id"               : "mtr_01daaym806bak37h7xrjmrrrqb",
        "object_name"      : "meter",
        "name"             : "meter name",
        "public_name"      : "",
        "is_active"        : false,
        "last_counting_at" : "2019-05-08T14:28:29+0900",
        "update_at"        : "2019-05-08T14:28:29+0900",
        "create_at"        : "2019-05-08T14:28:29+0900"
      },
      "volume": {
        "unit"   : 1,
        "amount" : 10
      }
    },
    "archive_at" : null,
    "update_at"  : "2019-05-08T14:28:29+0900",
    "create_at" : "2019-05-08T14:28:29+0900"
  }
}
```

契約の開始時期を独自に指定したい場合には、start_atを指定します。

### HTTP Request

`POST https://api.subscriptionbase.io/v1/subscriptions/`

### リクエストデータ
引数 | データ型（最大） | 必須 |詳細
---- | ---- | -- | -----------
customer | String（30） | ◯ | 顧客ID
plan | String(30) | ◯ | プランID
start_at | String | - | 契約（課金）開始時刻をUTCで指定。デフォルトは現在時刻。


## 購読契約を取得する

購読IDから契約情報を取得します。

> リクエスト

```shell
curl https://api.subscriptionbase.io/v1/subscriptions/<ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Subscription;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Subscription::retrieve(<ID>);
```

> レスポンス

```json
{
  "id"                : "sub_01daaym81nk191jk81rcra91hq",
  "object_name"       : "subscription",
  "trial_begin_at"    : "2019-06-01T00:00:00+0900",
  "contract_begin_at" : "2019-06-08T00:00:00+0900",
  "contract_end_at"   : "2019-07-08T00:00:00+0900",
  "last_payment_at"   : null,
  "next_payment_at"   : "2019-07-08T00:00:00+0900",
  "state"             : "active",
  "churn_at"          : null,
  "customer": {
    "id"               : "cus_01daaym803gvhdycjcky0hmx6t",
    "object_name"      : "customer",
    "udid"             : "90e342e0-bc4d-48cb-baf4-f93e139f4858",
    "email"            : "claytonsanders@banks.com",
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
    "update_at"        : "2019-05-08T14:28:29+0900",
    "create_at"        : "2019-05-08T14:28:29+0900"
  },
  "plan": {
    "id"              : "pln_01daaym808vm16e5eyar0pezdg",
    "object_name"     : "plan",
    "product"         : "prd_01daaym8051ej4z6rd54jckgtp",
    "name"            : "\u30d7\u30e9\u30f3\u540d",
    "public_name"     : "\u30d7\u30e9\u30f3\u516c\u958b\u540d",
    "contract_period" : "m1",
    "update_method"   : "repeat",
    "payment_term"    : "m1",
    "start_method"    : "trial",
    "trial_days"      : 7,
    "charge": {
      "charge_type" : "volume",
      "meter": {
        "id"               : "mtr_01daaym806bak37h7xrjmrrrqb",
        "object_name"      : "meter",
        "name"             : "meter name",
        "public_name"      : "",
        "is_active"        : false,
        "last_counting_at" : "2019-05-08T14:28:29+0900",
        "update_at"        : "2019-05-08T14:28:29+0900",
        "create_at"        : "2019-05-08T14:28:29+0900"
      },
      "volume": {
        "unit"   : 1,
        "amount" : 10
      }
    },
    "archive_at" : null,
    "update_at"  : "2019-05-08T14:28:29+0900",
    "create_at" : "2019-05-08T14:28:29+0900"
  },
  "update_at" : "2019-05-08T14:28:30+0900",
  "create_at" : "2019-05-08T14:28:30+0900"
}
```

### HTTP Request

`GET https://api.subscriptionbase.io/v1/subscriptions/<ID>/`

### レスポンスデータ
引数 | データ型（最大）| 詳細
---- | ---- | -----------
id | String（30) | 購読ID
object_name | String(255) | オブジェクト名称
trial_begin_at | Datetime | トライアル開始日時
contract_begin_at | Datetime | 契約開始日時
contract_end_at | Datetime | 契約終了日時
last_payment_at | Datetime | 前回清算日時
next_payment_at | Datetime | 次回清算日時
state | String(255) | 契約の状態値
churn_at | Datetime | 解約日時
customer | Object | 顧客情報のオブジェクト
plan | Object | プラン情報のオブジェクト


## 購読契約リストを取得する

購読契約のリストを取得します。

> リクエスト

```shell
curl https://api.subscriptionbase.io/v1/subscriptions/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Subscription;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

Subscription::all(array(
  'page' => 1,
));
```

> レスポンス

```json
{
  "object_name" : "list",
  "url"         : "https://api.subscriptionbase.io/v1/subscriptions/",
  "has_more"    : false,
  "count"       : 1,
  "data"        : [
    {
      "id"                : "sub_01daaym81nk191jk81rcra91hq",
      "object_name"       : "subscription",
      "trial_begin_at"    : "2019-06-01T00:00:00+0900",
      "contract_begin_at" : "2019-06-08T00:00:00+0900",
      "contract_end_at"   : "2019-07-08T00:00:00+0900",
      "last_payment_at"   : null,
      "next_payment_at"   : "2019-07-08T00:00:00+0900",
      "state"             : "active",
      "churn_at"          : null,
      "customer": {
        "id"               : "cus_01daaym803gvhdycjcky0hmx6t",
        "object_name"      : "customer",
        "udid"             : "90e342e0-bc4d-48cb-baf4-f93e139f4858",
        "email"            : "claytonsanders@banks.com",
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
        "update_at"        : "2019-05-08T14:28:29+0900",
        "create_at"        : "2019-05-08T14:28:29+0900"
      },
      "plan": {
        "id"              : "pln_01daaym808vm16e5eyar0pezdg",
        "object_name"     : "plan",
        "product"         : "prd_01daaym8051ej4z6rd54jckgtp",
        "name"            : "\u30d7\u30e9\u30f3\u540d",
        "public_name"     : "\u30d7\u30e9\u30f3\u516c\u958b\u540d",
        "contract_period" : "m1",
        "update_method"   : "repeat",
        "payment_term"    : "m1",
        "start_method"    : "trial",
        "trial_days"      : 7,
        "charge": {
          "charge_type" : "volume",
          "meter": {
            "id"               : "mtr_01daaym806bak37h7xrjmrrrqb",
            "object_name"      : "meter",
            "name"             : "meter name",
            "public_name"      : "",
            "is_active"        : false,
            "last_counting_at" : "2019-05-08T14:28:29+0900",
            "update_at"        : "2019-05-08T14:28:29+0900",
            "create_at"        : "2019-05-08T14:28:29+0900"
          },
          "volume": {
            "unit"   : 1,
            "amount" : 10
          }
        },
        "archive_at" : null,
        "update_at"  : "2019-05-08T14:28:29+0900",
        "create_at" : "2019-05-08T14:28:29+0900"
      },
      "update_at" : "2019-05-08T14:28:30+0900",
      "create_at" : "2019-05-08T14:28:30+0900"
    }
  ]
}
```

### HTTP Request

`GET https://api.subscriptionbase.io/v1/subscriptions/`


## 購読契約を削除する

購読契約の削除は、即時解約を示します。<br>
<aside class="warning">
この操作を行うと、該当の購読契約は契約期間の残存を無視して即座に解約済み状態となり、料金清算も行われません。
</aside>

> リクエスト

```shell
curl -X DELETE https://api.subscriptionbase.io/v1/subscriptions/<ID>/\
  -H Authorization: Bearer <アクセストークン>
```

```php
use SubscriptionBase\SubscriptionBase;
use SubscriptionBase\Subscription;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);

$subscription = Subscription::retrieve(<ID>);
$subscription->delete();
```

> レスポンス

```json
{
  "id"         : "sub_01daaym81nk191jk81rcra91hq",
  "archive_at" : "2019-05-06T16:59:35+0900",
}
```

### HTTP Request

`DELETE https://api.subscriptionbase.io/v1/subscriptions/<ID>/`
