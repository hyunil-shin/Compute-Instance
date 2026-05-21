## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter notebooks with essential packages pre-installed for machine learning development.

### Notebook List

The status of notebooks is displayed. Refer to the table below for major statuses.

| Status             | Description                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | Notebook creation has been requested.                                                                                             |
| CREATE IN PROGRESS | Notebook instance is being created.                                                                                               |
| ACTIVE (HEALTHY)   | Notebook application is running normally.                                                                                         |
| ACTIVE (UNHEALTHY) | Notebook application is not running normally. If this status persists after restarting the notebook, please contact customer support. |
| STOPPED            | Notebook has been stopped.                                                                                                        |

### Metric Log Storage for TensorBoard Usage

To view result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage path to the designated location (`EM_TENSORBOARD_LOG_DIR`) when writing the training script.

<details>
<summary><strong>Example</strong></summary>

```python
import tensorflow as tf

# Specify TensorBoard log path
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # Model implementation

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### Hyperparameter Input Screen

![Hyperparameter input screen](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/console-guide_appendix_hyperparameter_ko.png)