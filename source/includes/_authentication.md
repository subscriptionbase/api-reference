# 認証

クライアントIDとシークレットキーを使用してトークンリクエストを行い、レスポンスとしてアクセストークンを取得します。

## トークンリクエスト

> リクエスト

```shell
curl -X POST "https://api.subscriptionbase.io/oauth2/token/" \
  -d client_id=<クライアントID>\
  -d client_secret=<シークレットキー>\
  -d grant_type=client_credentials\
  -d scope=tenant_application
```

```php
use SubscriptionBase\SubscriptionBase;

SubscriptionBase::setApiKeys(<クライアントID>, <シークレットキー>);
```

> レスポンス

```json
{
  "access_token" : "IlpS2sonJrXLXWJnxKV2QjpsAR76NK",
  "expires_in"   : 36000,
  "token_type"   : "Bearer",
  "scope"        : "tenant_application",
}
```

クライアントIDとシークレットキーは [コンソール画面](http://app.subscriptionbase.io/setting/oauth2/)で発行します。

### HTTP リクエスト

`POST https://api.subscriptionbase.io/oauth2/token/`

### リクエストデータ
引数 | データ型(最大) | 必須 | 詳細
---- | ---- | ---- |-----------
client_id | String | ◯ | クライアントID
client_secret | String | ◯ | シークレットキー
grant_type | String | ◯ | "client_credentials"を指定
scope | String | ◯ | "tenant_application"を指定

トークンリクエストは、content_typeに「application/x-www-form-urlencoded」が指定されている必要があります。
それ以外が指定されている場合には、リクエストエラーになります。

## アクセストークンの利用
全てのAPIリクエストは、以下の通りAuthorizationヘッダーにアクセストークンをセットしてリクエストします。<br>
SDKを利用している場合には、自動的にヘッダーが付与されます。

`Authorization: Bearer <AccessToken>`
