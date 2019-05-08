# イントロダクション

サブスクリプションベースのAPIドキュメントです。

APIを利用するには、最初に[コンソール画面](http://app.subscriptionbase.io/setting/oauth2/)からクライアントIDとシークレットキーの発行が必要です。

<aside class="notice">
<strong>クライアントIDとシークレットキーは秘密情報として取り扱いください。</strong><br><br>
クライアントIDとシークレットキーを利用すると顧客情報の取得が可能になりますので、外部に漏洩すると情報流出につながる可能性があります。<br>
また、git等のバージョン管理ツールの管理下にも含めないようご注意ください。
</aside>

## SDK

各言語に対応したSDKを提供しています。<br>
本ページのソースコード例は、各言語のSDKを利用した記述になっています。<br>
* [PHP] (https://github.com/subscriptionbase/subscriptionbase-php)

## リクエストとレスポンス

リクエストを送信する際には、セキュリティのためhttps通信をご利用ください。<br>
レスポンスは全てJSON形式で返却されます。
