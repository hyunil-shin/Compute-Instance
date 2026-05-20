## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートブック

機械学習開発に必要なパッケージがインストールされているJupyter（ジュピター）ノートブックを作成・管理します。

### ノートブック一覧

ノートブックのステータスが表示されます。主なステータスは以下の表を参照してください。

| ステータス         | 説明                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートブック作成がリクエストされた状態です。                                                                                                  |
| CREATE IN PROGRESS | ノートブックインスタンスを作成中の状態です。                                                                                           |
| ACTIVE (HEALTHY)   | ノートブックアプリケーションが正常に稼働中の状態です。                                                                            |
| ACTIVE (UNHEALTHY) | ノートブックアプリケーションが正常に稼働していない状態です。ノートブックを再起動した後もこの状態が続く場合は、カスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートブックを停止した状態です。                                                                                                       |

### TensorBoardの活用のための指標ログ保存

学習後、TensorBoard画面で結果指標を確認するため、学習スクリプト作成時にTensorBoardログ保存領域を指定された位置（`EM_TENSORBOARD_LOG_DIR`）に設定してください。

<details>
<summary><strong>例</strong></summary>

```python
import tensorflow as tf

# TensorBoardログパス指定
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # モデル実装

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### ハイパーパラメーター入力画面

![ハイパーパラメーター入力画面](images/console-guide_appendix_hyperparameter_ko.png)