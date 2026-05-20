## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートブック

機械学習開発に必要なパッケージがインストールされているJupyterノートブックを作成および管理します。

### ノートブック一覧

ノートブックのステータスが表示されます。主なステータスについては以下の表を参考してください。

| ステータス         | 説明                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートブック作成が要求された状態です。                                                                                                  |
| CREATE IN PROGRESS | ノートブックインスタンスを作成中の状態です。                                                                                           |
| ACTIVE (HEALTHY)   | ノートブックアプリケーションが正常に稼働している状態です。                                                                            |
| ACTIVE (UNHEALTHY) | ノートブックアプリケーションが正常に稼働していない状態です。ノートブックを再起動した後もこのステータスが続く場合は、カスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートブックを停止した状態です。                                                                                                       |

### TensorBoardの活用のための指標ログ保存

学習後TensorBoardの画面で結果指標を確認するために、学習スクリプト作成時にTensorBoardログ保存スペースを指定された位置（`EM_TENSORBOARD_LOG_DIR`）に設定する必要があります。

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

![ハイパーパラメーター入力画面](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)