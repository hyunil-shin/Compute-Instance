## Compute > Image > API v2ガイド

APIを使用するにはAPIエンドポイントとトークンなどが必要です。[API使用準備](/Compute/Compute/ja/identity-api/)を参照してAPI使用に必要な情報を準備します。

イメージAPIは`image`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| image | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>日本リージョン<br>米国(カリフォルニア)リージョン | https://kr1-api-image-infrastructure.nhncloudservice.com<br>https://kr2-api-image-infrastructure.nhncloudservice.com<br>https://jp1-api-image-infrastructure.nhncloudservice.com<br>https://us1-api-image-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに明示されていないフィールドが表示される場合があります。これらのフィールドはNHN Cloud内部用途で使用され、事前通知なしに変更される可能性があるため使用しません。