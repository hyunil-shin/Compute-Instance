## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter notebooks with essential packages for machine learning development pre-installed.

### Notebook List

The status of the notebook is displayed. Refer to the table below for major statuses.

| Status             | Description                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | The notebook creation has been requested.                                                                                         |
| CREATE IN PROGRESS | The notebook instance is being created.                                                                                           |
| ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                     |
| ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists after restarting the notebook, please contact Customer Support. |
| STOPPED            | The notebook has been stopped.                                                                                                    |

### Saving Metric Logs for TensorBoard Usage

To check the training results in the TensorBoard screen after training, you must set the TensorBoard log storage path to the specified location (`EM_TENSORBOARD_LOG_DIR`) when writing the training script.

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

![Hyperparameter input screen](images/console-guide_appendix_hyperparameter_ko.png)