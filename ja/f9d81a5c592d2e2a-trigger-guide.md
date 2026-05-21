## Compute > Cloud Functions > トリガーガイド

このドキュメントは、Cloud Functionsで提供するトリガータイプと設定方法について説明します。

## トリガー概要

トリガーは関数を実行するイベントソースです。Cloud Functionsは様々なタイプのトリガーを提供し、複数の方法で関数を呼び出すことができます。

### サポートされるトリガータイプ

| トリガータイプ | 説明 | デフォルト提供 |
|-------------|------------------------|-------|
| HTTP | HTTP要求を通じて関数実行 | O |
| Timer | 指定された時間または周期に従って関数実行 | X |
| API Gateway | API Gatewayを通じて関数実行 | X |

## HTTPトリガー

HTTPトリガーは関数作成時にデフォルトで提供され、HTTP要求を通じて関数を実行できます。

### 特徴

- 関数作成時に自動的に作成されます。
- 削除できず、有効化/無効化のみが可能です。
- GET、POSTメソッドをサポートします。

### HTTPトリガーURL形式

```
https://{userdomain}/{関数名}
```

### 使用例

#### GET要求

```bash
curl -X GET "https://{userdomain}/{関数名}?param1=value1&param2=value2"
```

#### POST要求

```bash
curl -X POST "https://{userdomain}/{関数名}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### HTTPトリガーの有効化/無効化

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. HTTPトリガーの有効化/無効化トグルをクリックします。

> **[参考]**
> <br>無効化されたHTTPトリガーにリクエストを送信すると、関数は実行されません。

## Timerトリガー

Timerトリガーは、指定された時間または周期に従って自動的に関数を実行します。Cron表現式を使用して実行周期を設定できます。

### Timerトリガーの作成

![trigger-guide-05](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/ja/trigger-guide-01.png)

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. **トリガー作成**をクリックします。
4. トリガーのタイプを **Timer** に選択します。
5. **Value**にCron表現式を入力します。
6. **作成**をクリックします。

### Cron表現式形式

Cron表現式は次のような形式に従います。

```
* * * * * *
│ │ │ │ │ │
│ │ │ │ │ └─ 曜日 (0-6 または SUN-SAT、0: 日曜日)
│ │ │ │ └─── 月 (1-12 または JAN-DEC)
│ │ │ └───── 日 (1-31)
│ │ └─────── 時 (0-23)
│ └───────── 分 (0-59)
└─────────── 秒 (0-59)
```

#### Cron表現式フィールド

| フィールド | 必須 | 許可値 | 許可特殊文字 |
|-----------|-----|----------|-----------|
| 秒(Seconds) | Yes | 0-59 | * / , - |
| 分(Minutes) | Yes | 0-59 | * / , - |
| 時(Hours) | Yes | 0-23 | * / , - |
| 日(Day of month) | Yes | 1-31 | * / , - ? |
| 月(Month) | Yes | 1-12 または JAN-DEC | * / , - |
| 曜日(Day of week) | Yes | 0-6 または SUN-SAT | * / , - ? |

#### 特殊文字説明

`*`

該当フィールドのすべての値と一致することを表します。例えば、5番目のフィールド(月)に `*` を使用すると、すべての月を意味します。

`/`

範囲の増分を表す場合に使用します。例えば、2番目のフィールド(分)に `3-59/15` を使用すると、3分から始まり15分ごとに実行されることを意味します(3、18、33、48分)。`*/...` 形式は `first-last/...` 形式と同じであり、該当フィールドの最大範囲に対する増分を意味します。`N/...` 形式は `N-MAX/...` を意味し、Nから始まり該当範囲の終わりまで増分を使用します。範囲を超える場合、最初に戻りません。

`,`

リストの項目を区切る場合に使用します。例えば、6番目のフィールド(曜日)に `MON,WED,FRI` を使用すると、月曜日、水曜日、金曜日を意味します。

`-`

範囲を定義する場合に使用します。例えば、3番目のフィールド(時)に `9-17` を使用すると、午前9時から午後5時まで(含む)のすべての時間を意味します。

`?`

日(Day of month)または曜日(Day of week)フィールドを空にするために `*` の代わりに使用できます。

### Cron表現式例

| Cron表現式 | 説明 |
|-----------|------|
| `0 * * * * *` | 毎分実行(0秒に) |
| `0 0 * * * *` | 毎時間実行 |
| `0 0 0 * * *` | 毎日深夜に実行 |
| `0 0 9 * * MON` | 毎週月曜日午前9時に実行 |
| `0 0 0 1 * *` | 毎月1日深夜に実行 |
| `0 */5 * * * *` | 5分ごとに実行 |
| `0 0 9-18 * * MON-FRI` | 平日(月-金)午前9時から午後6時まで毎時間実行 |
| `30 0 12 * * *` | 毎日午後12時0分30秒に実行 |
| `0 0 0 1 JAN *` | 毎年1月1日深夜に実行 |

### Timerトリガーの修正

![trigger-guide-02](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/ja/trigger-guide-02.png)

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. 修正するTimerトリガーを選択します。
4. **トリガー修正**をクリックします。
5. **Value**のCron表現式を修正します。
6. **修正**をクリックします。

> **[参考]**
> <br>月(Month)と曜日(Day of week)フィールド値は大文字と小文字を区別しません。「SUN」、「Sun」、「sun」はすべて同じものとして認識されます。

## API Gatewayトリガー

API Gatewayトリガーは、同じプロジェクトのAPI Gatewayサービスを利用して関数を実行できます。API Gatewayを通じてより詳細なAPI管理と制御が可能です。

### 前提条件

- 同じプロジェクトでAPI Gatewayサービスが有効化されている必要があります。
  - 有効化されていない場合、トリガー作成時に有効化できます。

### API Gatewayトリガーの作成

![trigger-guide-04](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/ja/trigger-guide-04.png)

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. **トリガー作成**をクリックします。
4. トリガータイプからAPI Gatewayを選択します。
5. 使用するパスを入力します。
   * 重複するパスは使用できません。
6. **作成**をクリックします。

### API GatewayトリガーURL形式

```
https://{stageurl}/{パス}
```

### 使用例

#### GET要求

```bash
curl -X GET "https://{stageurl}/{パス}?param1=value1&param2=value2"
```

#### POST要求

```bash
curl -X POST "https://{stageurl}/{パス}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### API Gatewayトリガーの特徴

- API Gatewayの様々な機能を活用できます。
  - 認証と権限管理
  - リクエスト/レスポンス変換
  - 使用量プランとAPIキー管理
  - リクエスト制限
- API GatewayコンソールでAPI設定を管理できます。
- 自動作成された1つのサービスでのみ関数連動が可能です。
- HTTPトリガーと同じくGET、POSTメソッドをサポートします。

### API Gatewayトリガーの修正

![trigger-guide-05](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/ja/trigger-guide-05.png)

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. 修正するAPI Gatewayトリガーを選択します。
4. **トリガー修正**をクリックします。
5. パスを変更します。
6. **修正**をクリックします。

> **[参考]**
> <br>API Gatewayトリガー修正は、API Gatewayサービス内で既存トリガーを削除した後に新たに作成する方法で進行します。
> <br>これにより、該当リソースに適用されたプラグインがすべて削除されます。
> <br>プラグインが適用されたリソースパスを変更するには、修正の代わりに新しいトリガーを追加することをお勧めします。

### API Gatewayと一緒に使用する

API Gatewayトリガーを作成すると、API Gatewayコンソールで追加設定ができます。

詳細については、[API Gatewayガイド](https://docs.nhncloud.com/ko/Application%20Service/API%20Gateway/ko/overview/)を参照してください。

## トリガー削除

### トリガー削除方法

![trigger-guide-03](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/ja/trigger-guide-03.png)

1. Cloud Functionsコンソールで関数を選択します。
2. **トリガー** タブに移動します。
3. 削除するトリガーを選択します。(複数選択可)
4. **トリガー削除**をクリックします。
5. **トリガー削除** モーダルウィンドウで **削除** をクリックします。

### 注意事項

- HTTPトリガーは削除できません。HTTPトリガーはデフォルトトリガーとして提供され、有効化/無効化のみが可能です。
- トリガーを削除すると、該当イベントを通じて関数を実行できません。
- 削除されたトリガーは復構できません。

## トリガー制限事項

### API Gatewayトリガー制限事項

- 同じプロジェクト内のAPI Gatewayのみ接続できます。
- 1つのAPI Gateway Resourceは1つの関数のみ接続できます。
- 1つの関数に複数のAPI Gatewayトリガーを登録できます。
- API Gatewayサービスが無効化されたり、接続されたリソースが削除または変更されたりすると、トリガーも動作しません。
  - この場合、トリガーを修正できないため、削除した後に再度登録する必要があります。