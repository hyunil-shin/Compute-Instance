I see you've provided a reference translation example, but I don't see the actual Korean document you want me to translate. You've only included:

```
<a id="ai.easymaker.console.guide"></a>
```

Could you please provide the Korean Markdown document that you'd like me to translate into English?

## Machine Learning > AI EasyMaker > Console Guide

<a id="dashboard"></a>

## Dashboard

You can check the usage status of all AI EasyMaker resources on the dashboard.

<a id="dashboard.service.usage.status"></a>

### Service Usage Status

Displays the number of resources in use by resource type.

- Notebook: Number of notebooks in ACTIVE (HEALTHY) status that are in use
- Training: Number of completed (COMPLETE) trainings
- Hyperparameter Tuning: Number of completed (COMPLETE) hyperparameter tunings
- Endpoint: Number of endpoints in ACTIVE status

<a id="dashboard.service.monitoring"></a>

### Service Monitoring

- Displays the top 3 endpoints with the most API calls.
- When you select an endpoint, you can check the total metrics of API success/failure for the sub-endpoint stages.

<a id="dashboard.resource.usage"></a>

### Resource Usage

- You can check the resources with the highest usage by CPU and GPU core type.
- Resource information is displayed when you hover the mouse pointer over the metrics.

<a id="notebook"></a>



## Experiments

Experiments group related training together for management.

<a id="experiment.create"></a>

### Create Experiments

1. Click **Create Experiment**.
2. Enter the experiment name and description, and click **Confirm**.

!!! tip "Note"
    Creating an experiment may take a few minutes.
    When creating resources for the first time, it may take a few additional minutes to configure the service environment.

<a id="experiment.list"></a>

### Experiment List

The experiment list is displayed. When you select an experiment from the list, you can view detailed information and modify the information.

- **Status**: The status of the experiment is displayed. See the table below for key statuses.

    | Status             | Description                                        |
    | ------------------ | -------------------------------------------------- |
    | CREATE REQUESTED   | Experiment creation has been requested.           |
    | CREATE IN PROGRESS | The experiment is being created.                  |
    | CREATE FAILED      | Experiment creation failed. Please try again.     |
    | ACTIVE             | The experiment has been created successfully.     |

- **Actions**
    - Click **Go to TensorBoard** to open TensorBoard in a new browser window where you can view statistics for the training included in the experiment. TensorBoard can only be accessed by users logged into the console.
    - **Retry**: If the experiment status is failed, you can click **Retry** to recover the experiment.
- **Training**: The **Training** tab in the detail screen that appears when you select training displays a list of training included in the experiment.

<a id="experiment.delete"></a>

### Delete Experiments

Delete an experiment.

1. Select the experiment to delete.
2. Click **Delete Experiment**. You cannot delete an experiment if it is in the process of being created.
3. The requested delete operation cannot be canceled. To proceed, click **Confirm**.

!!! tip "Note"
    You cannot delete an experiment if there are associated pipeline schedules or training, hyperparameter tuning, or pipeline executions being created.
    Delete the resources associated with the experiment before deleting the experiment.
    You can check associated resources in the detail screen at the bottom that appears when you click the experiment you want to delete.

<a id="training"></a>





## Training Template

By creating training templates in advance, you can retrieve the values entered in the template when creating training or hyperparameter tuning.

<a id="training.template.create"></a>

### Create Training Template

For information that can be configured in training templates, see [Create Training](#training.create).

<a id="training.template.list"></a>

### Training Template List

The training template list is displayed. When you select a training template from the list, you can check the details and modify the information.

- **Actions**
    - **Modify**: You can modify training template information.
- **Hyperparameters**: In the **Hyperparameters** tab of the details screen displayed when you select a training template, you can check the hyperparameter names configured in the training template.

<a id="training.template.copy"></a>

### Copy Training Template

Creates a new training template with the same settings as an existing training template.

1. Select the training template you want to copy.
2. Click **Copy Training Template**.
3. The training template creation screen is displayed with the same settings as the existing training template.
4. If there is information you want to modify, make the changes and then click **Create Training Template** to create the training template.

<a id="training.template.delete"></a>

### Delete Training Template

Deletes a training template.

1. Select the training template you want to delete.
2. Click **Delete Training Template**.
3. The requested delete operation cannot be canceled. To proceed, click **Confirm**.

<a id="model"></a>

## Models

You can manage models from AI EasyMaker training results or external models as artifacts.

<a id="model.create"></a>

### Create Models

- **Basic Information**: Enter basic information for the model.
    - **Name**: Enter the model name.
        - If the model framework type is PyTorch, you must enter the same model name as the PyTorch model name.
    - **Description**: Enter the model description.
- **Framework Information**: Enter framework information for the model.
    - **Framework**: Select the framework for the model.
    - **Framework Version**: Enter the version of the model framework.
- **Model Information**: Enter the repository where model artifacts are stored.
    - **Model Artifact**: Select the repository where model artifacts are stored.
        - **NHN Cloud Object Storage**: Enter the Object Storage path where model artifacts are stored.
            - Enter the directory path in the format `obs://{Object Storage API endpoint}/{containerName}/{path}`.
            - When using NHN Cloud Object Storage, set permissions by referring to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission). If permissions are not set, model creation will fail due to inability to access model artifacts.
        - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where model artifacts are stored.
            - Enter the directory path in the format `nas://{NAS ID}:/{path}`.
    - **Parameters**: Enter parameter information for the model.
        - **Parameter Name**: Enter the parameter name for the model.
        - **Parameter Value**: Enter the parameter value for the model.

!!! tip "Note"
    Values entered as model parameters are used when serving the model. Parameters can be used as arguments and environment variables.
    Arguments are used exactly as the entered parameter name, while environment variables are used with the parameter name converted to screaming snake case.

!!! tip "Note"
    When creating a HuggingFace model, you can create the model by entering the HuggingFace model ID as a parameter.
    The HuggingFace model ID can be found in the URL of the HuggingFace model page.
    For more details, see [Appendix > 11. Framework-specific Serving Notes](#appendix.11.framework.note).

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

!!! danger "Caution"
    HuggingFace model file types are limited to safetensors.
    Safetensors is a safe and efficient machine learning model file format developed by HuggingFace.
    Other file formats are not supported.

!!! danger "Caution"
    When creating TensorFlow (Triton), PyTorch (Triton), or ONNX (Triton) models, the model artifact path you enter must contain model files and `config.pbtxt` files stored in a structure that allows the model to run with Triton.
    Refer to the example below.
    <details>
    <summary><strong>Example</strong></summary>

        model_name/
        ├── config.pbtxt                              # Model configuration file
        └── 1/                                        # Version 1 directory
            └── model.savedmodel/                     # TensorFlow SavedModel directory
                ├── saved_model.pb                    # MetaGraph and checkpoint data
                └── variables/                        # Model weights directory
                    ├── variables.data-00000-of-00001
                    └── variables.index

    </details>

<a id="model.list"></a>

### Model List

A list of models is displayed. When you select a model from the list, you can check detailed information and modify information.

- **Name**: Model name and description are displayed. You can modify the model name and description by clicking **Modify**.
- **Model Artifact Path**: The repository where the model artifacts are stored is displayed.
- **Status**: The status of the model is displayed. Refer to the table below for major statuses.

    | Status             | Description                                                                                    |
    | ------------------ | ---------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Model creation has been requested.                                                             |
    | CREATE IN PROGRESS | Resources required for the model are being created.                                           |
    | DELETE IN PROGRESS | The model is being deleted.                                                                    |
    | ACTIVE             | The model has been created successfully.                                                       |
    | CREATE FAILED      | Model creation has failed. If creation continues to fail, please contact Customer Center.     |
    | DELETE FAILED      | Model deletion has failed. Please try again.                                                  |

- **Training Name**: For models created from training, the name of the underlying training is displayed.
- **Training ID**: For models created from training, the ID of the underlying training is displayed.
- **Framework**: Framework information for the model is displayed.
- **Parameters**: Model parameters are displayed. Parameters are used for inference.

<a id="model.endpoint.create"></a>

### Create Endpoint from Model

Create an endpoint to serve the selected model.

1. Select the model you want to create as an endpoint from the list.
2. Click **Create Endpoint**.
3. You will be redirected to the **Create Endpoint** page. After reviewing the content, click **Create Endpoint**.
   For more details on endpoint creation, see the [Endpoint](#endpoint) documentation.

<a id="model.batch.inference.create"></a>

### Create Batch Inference from Model

Create batch inference that performs batch inference with the selected model and allows you to check inference results as statistics.

1. Select the model you want to create for batch inference from the list.
2. Click **Create Batch Inference**.
3. You will be redirected to the **Create Batch Inference** page. After reviewing the content, click **Create Batch Inference**.
   For more details on batch inference creation, see the [Batch Inference](#batch.inference) documentation.

<a id="model.delete"></a>

### Delete Model

Delete a model.

1. Select the model you want to delete from the list.
2. Click **Delete Model**.
3. The requested deletion operation cannot be canceled. To continue, click **Confirm**.

!!! tip "Note"
    If there are endpoints created with the model you want to delete, you cannot delete the model.
    To delete it, first delete the endpoints created with that model, then delete the model.

<a id="model.evaluation"></a>

## Model Evaluation

Measures model performance and compares performance between multiple models.

<a id="model.evaluation.create"></a>

### Create Model Evaluation

Batch inference is automatically generated during the model evaluation process.

- **Basic Information**: Enter the basic information for model evaluation.
    - **Name**: Enter the model evaluation name.
    - **Description**: Enter the model evaluation description.
- **Model Information**: Enter the information for the model to be evaluated.
    - **Model**: Select the model to evaluate. Only classification and regression models are supported.
    - **Class Name**: Enter the class name of the model.
- **Model Evaluation Instance Information**
    - **Instance Type**: Select the instance type to run model evaluation. Used for data preprocessing and evaluation calculation tasks.
- **Input Data**: Input data is used to compare predictions generated through batch inference with ground truth. Fields used for inference and ground truth fields are required.
    - **Data Path**: Enter the path where input data is located.
        - **Input Data Classification**: Select the format of input data. CSV and JSONL formats are supported, with file extensions .csv and .jsonl respectively.
        - **Target Field for Evaluation**: Enter the field name of the ground truth label.
- **Batch Inference Output Data**
    - **Data Path**: Enter the path where batch inference results will be saved.
- **Batch Inference Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Number of Instances**: Enter the number of instances to perform batch inference.
    - **Number of Pods**: Enter the number of pods for batch inference.
    - **Batch Size**: Enter the number of data samples processed simultaneously in one inference task.
    - **Inference Timeout (seconds)**: Enter the timeout for batch inference. Sets the maximum allowed time for a single inference request to be processed and return results.
- **Additional Settings**
    - **Maximum Execution Time**: Specify the maximum execution time until model evaluation is completed. Model evaluations that exceed the maximum execution time will be terminated.
    - **Log Management**: Logs generated during model evaluation can be saved to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - The size of input data used for model evaluation must be 20GB or less.
    - The number of classes for classification model evaluation must be 50 or less.

<a id="model.evaluation.list"></a>

### Model Evaluation List

The model evaluation list is displayed. Select a model evaluation from the list to check detailed information and modify information.

- **Name**: The name of the model evaluation is displayed.
- **Model**: The name of the model used for model evaluation is displayed.
- **Status**: The status of the model evaluation is displayed. See the table below for major statuses.

    | Status                                                   | Description                                                                                 |
    |----------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | CREATE REQUESTED                                         | Model evaluation creation has been requested.                                                               |
    | CREATE IN PROGRESS                                       | Model evaluation is being created.                                                                |
    | CREATE FAILED                                            | Model evaluation creation failed. Please try again.                                                     |
    | RUNNING                                                  | Model evaluation is in progress.                                                                |
    | COMPLETE IN PROGRESS, FAIL MODEL EVALUATION IN PROGRESS  | Resources used for model evaluation are being cleaned up.                                                       |
    | COMPLETE                                                 | Model evaluation completed successfully.                                                            |
    | STOP IN PROGRESS                                         | Model evaluation is being stopped.                                                                |
    | STOPPED                                                  | Model evaluation was stopped by user request.                                                        |
    | FAIL MODEL EVALUATION                                    | Model evaluation failed. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | DELETE IN PROGRESS                                       | Model evaluation is being deleted.                                                                |

- **Actions**
    - **Stop**: You can stop model evaluation in progress.

<a id="model.evaluation.classification.metric"></a>

### Classification Model Evaluation Metrics

- **PR AUC**: The area under the precision-recall (PR) curve. Effective for measuring model classification performance on imbalanced datasets.
- **ROC AUC**: The area under the ROC curve (recall-false positive rate). The closer to 1, the better the performance.
- **Log Loss**: The loss value calculated using a log function for the difference between predicted probabilities and actual answers. Lower values indicate more reliable model predictions.
- **F1 Score**: The harmonic mean of precision and recall. Useful when there is class imbalance, and closer to 1 is better.
- **Precision**: The ratio of actual positives among those predicted as positive. Focuses on reducing false positives.
- **Recall**: The ratio of correctly predicted positives among actual positives. Important for reducing false negatives.
- **Precision-Recall Curve**: A curve that visualizes the relationship between precision and recall at various thresholds. Reference when adjusting model thresholds.
- **ROC Curve**: Represents the relationship between recall and false positive rate at various thresholds. Used for setting classification thresholds or comparing models.
- **Threshold-based Precision-Recall Curve**: A graph showing how precision and recall change at specific thresholds. Referenced when setting actual operational criteria.
- **Confusion Matrix**: A matrix that categorizes prediction results into four types: TP, FP, FN, TN. Makes it easy to identify error types by class.

<a id="model.evaluation.regression.metric"></a>

### Regression Model Evaluation Metrics

- **MAE (Mean Absolute Error)**: The average of absolute differences between actual and predicted values. Intuitively shows the magnitude of prediction errors.
- **MAPE (Mean Absolute Percentage Error)**: The average of ratios of prediction errors divided by actual values. Being ratio-based, it may be unsuitable for data with values close to 0.
- **R-squared (Coefficient of Determination)**: Indicates how well the model explains actual data, with closer to 1 indicating higher explanatory power.
- **RMSE (Root Mean Squared Error)**: The square root of the mean squared error. More sensitive to large errors and allows interpretation of results on the same scale as actual units.
- **RMSLE (Root Mean Squared Logarithmic Error)**: Calculated from the difference between log-transformed actual and predicted values. Not sensitive to differences in value magnitude, useful for evaluating exponential growth data.

<a id="model.evaluation.compare"></a>

### Compare Model Evaluations

Compares evaluation metrics of multiple models.

1. Select the model evaluations you want to compare from the list.
2. Click **Compare**.

<a id="model.evaluation.delete"></a>

### Delete Model Evaluation

Deletes model evaluation.

1. Select the model evaluation to delete.
2. Click **Delete**. Model evaluations in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

<a id="endpoint"></a>



## Batch Inference

Provides an environment for batch inference with AI EasyMaker models and checking inference results with statistics.

<a id="batch.inference.create"></a>

### Create Batch Inference

Select instances and OS images to set up the environment for batch inference, and enter the paths for input/output data to proceed with batch inference.

- **Basic Information**: Enter basic information for batch inference.
    - **Batch Inference Name**: Enter the batch inference name.
    - **Batch Inference Description**: Enter a description.
- **Instance Information**
    - **Instance Type**: Select the instance type to execute batch inference.
    - **Number of Instances**: Number of instances to perform batch inference.
- **Model Information**
    - **Model**: Select a model for batch inference. If you have not created a model, create a model first.
    - **Number of Pods**: Enter the number of pods for the model.
    - **Resource Information**: You can check the actual resources used by the model. The actual usage is divided according to the number of pods entered and allocated to each pod. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).
- **Input Data**
    - **Data Path**: Enter the path of the data to execute batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Input Data Type**: Select the type of data to execute batch inference.
        - **JSON**: Uses valid JSON data in the file as input values.
        - **JSONL**: Uses JSON Lines files consisting of valid JSON on each line as input values.
            - Reference: [https://jsonlines.org/](https://jsonlines.org/)
    - **Glob Pattern**
        - **Include Files**: Enter the file set to include in input data as a Glob pattern.
        - **Exclude Files**: Enter the file set to exclude from input data as a Glob pattern.
- **Output Data**
    - **Output Data**: Enter the data storage path to save the execution results of batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Batch Options**
        - **Batch Size**: Enter the number of data samples processed simultaneously in one inference task.
        - **Inference Timeout (seconds)**: Enter the timeout for batch inference. You can set the maximum allowed time for a single inference request to be processed and return results.
    - **Data Storage Size**: Enter the data storage size of the instance to execute batch inference.
        - Used only when using NHN Cloud Object Storage. You must specify sufficient size to store all data required for batch inference.
    - **Maximum Batch Inference Time**: Specify the maximum wait time until batch inference is completed. Batch inference that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during batch inference can be stored in the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    - When using Glob patterns, **exclude Glob patterns** are applied with priority.
    - You must properly set **batch size** and **inference timeout** according to the performance of the model for batch inference. If the entered settings are incorrect, batch inference may not achieve sufficient performance.

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before batch inference is completed may cause batch inference to fail.
    - When using Glob patterns, if values are not entered properly, input data may not be found and batch inference may not work normally.

!!! danger "Caution"
    Batch inference using GPU instances allocates GPU instances according to the number of pods.
    If `Number of pods / Number of GPUs` is not divisible by an integer, unallocated GPUs may occur.
    Unallocated GPUs are not used for batch inference, so set the number of pods appropriately to use GPU instances efficiently.

<a id="batch.inference.list"></a>

### Batch Inference List

The batch inference list is displayed. Selecting a batch inference from the list allows you to check detailed information and change settings.

- **Inference Duration**: The time taken for batch inference is displayed.
- **Status**: The status of batch inference is displayed. Refer to the table below for major statuses.

    | Status                                                 | Description                                                                                                                                          |
    | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                       | Requested to create batch inference.                                                                                                                 |
    | CREATE IN PROGRESS                                     | Creating resources required for batch inference.                                                                                                     |
    | RUNNING                                                | Batch inference is in progress.                                                                                                                      |
    | STOPPED                                                | Batch inference has been stopped by user request.                                                                                                   |
    | COMPLETE                                               | Batch inference has completed normally.                                                                                                              |
    | STOP IN PROGRESS                                       | Batch inference is being stopped.                                                                                                                   |
    | FAIL BATCH INFERENCE                                   | Failed during batch inference. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled.          |
    | CREATE FAILED                                          | Failed to create batch inference. If creation continues to fail, please contact customer support.                                                  |
    | FAIL BATCH INFERENCE IN PROGRESS, COMPLETE IN PROGRESS | Cleaning up resources used for batch inference.                                                                                                     |

- **Actions**
    - **Stop**: You can stop batch inference in progress.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select batch inference, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when batch inference is in the creating state.

<a id="batch.inference.copy"></a>

### Copy Batch Inference

Create a new batch inference with the same settings as an existing batch inference.

1. Select the batch inference you want to copy.
2. Click **Copy Batch Inference**.
3. The batch inference creation screen is displayed with the same settings as the existing batch inference.
4. If there is information you want to change, modify it and click **Create Batch Inference** to create the batch inference.

<a id="batch.inference.delete"></a>

### Delete Batch Inference

Delete batch inference.

1. Select the batch inference you want to delete.
2. Click **Delete Batch Inference**. Batch inference in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. To continue, click **Confirm**.

<a id="personal.image"></a>

## Personal Images

You can run notebooks, training, and hyperparameter tuning using personalized container images.
Only personal images derived from notebook/deep learning images provided by AI EasyMaker can be used when creating resources in AI EasyMaker.
See the table below for AI EasyMaker base images.

<a id="personal.image.notebook.image"></a>

#### Notebook Images

| Image Name                           | Core Type | Framework  | Framework Version | Python Version | Image Address                                                                                          |
| ------------------------------------ | --------- | ---------- | ----------------- | -------------- | ------------------------------------------------------------------------------------------------------ |
| Ubuntu 22.04 CPU Python Notebook     | CPU       | Python     | 3.10.12           | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204    |
| Ubuntu 22.04 GPU Python Notebook     | GPU       | Python     | 3.10.12           | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-gpu-py310-ubuntu2204    |
| Ubuntu 22.04 CPU PyTorch Notebook    | CPU       | PyTorch    | 2.0.1             | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Notebook    | GPU       | PyTorch    | 2.0.1             | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Notebook | CPU       | TensorFlow | 2.12.0            | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Notebook | GPU       | TensorFlow | 2.12.0            | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-gpu-py310-ubuntu2204 |

<a id="personal.image.deep.learning.image"></a>

#### Deep Learning Images

| Image Name                           | Core Type | Framework  | Framework Version | Python Version | Image Address                                                                                       |
| ------------------------------------ | --------- | ---------- | ----------------- | -------------- | --------------------------------------------------------------------------------------------------- |
| Ubuntu 22.04 CPU PyTorch Training    | CPU       | PyTorch    | 2.0.1             | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Training    | GPU       | PyTorch    | 2.0.1             | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Training | CPU       | TensorFlow | 2.12.0            | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Training | GPU       | TensorFlow | 2.12.0            | 3.10           | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-gpu-py310-ubuntu2204 |

!!! tip "Note"
    Only NHN Container Registry (NCR) can be integrated as a container registry service where personal images are stored (as of December 2023).

!!! danger "Caution"
    Only personal images derived from base images provided by AI EasyMaker can be used.

<a id="personal.image.create"></a>

### Create Personal Images

The following document guides you through creating container images using Docker with AI EasyMaker base images and using personal images for notebooks in AI EasyMaker.

1. Write a Dockerfile for your personal image.

        FROM fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204 as easymaker-notebook
        RUN conda create -n example python=3.10
        RUN conda activate example
        RUN pip install torch torchvision

2. Build personal image and push to Container Registry
    Build an image with Dockerfile and save (push) the image to NCR registry.

        docker build -t {이미지 이름}:{태그} .
        docker tag {이미지 이름}:{태그} {NCR 레지스트리 주소}/{이미지 이름}:{태그}
        docker push {NCR 레지스트리 주소}/{이미지 이름}:{태그}

        (예시)
        docker build -t custom-training:v1 .
        docker tag custom-training:v1 example-kr1-registry.container.nhncloud.com/registry/custom-training:v1
        docker push example-kr1-registry.container.nhncloud.com/registry/custom-training:v1

3. Create the image saved (pushed) to NCR as a personal image in AI EasyMaker.

    1. Go to the **Images** menu in the AI EasyMaker console.
    2. Click the **Create Image** button to enter information about the created image.
        - Name, Description: Enter a name and description for the image.
        - Address: Enter the registry image address.
        - Type: Enter the type of container image. Select **Notebook** or **Training**.
        - Account: Select an account for AI EasyMaker notebook/training nodes to access your registry repository.
            - Use New: Register a new registry account.
                - Name, Description: Enter a name and description for the registry account.
                - Category: Select the container registry service.
                - ID: Enter the ID of the registry repository.
                - Password: Enter the password of the registry repository.
            - Use Existing Account: Select an already registered registry account.

4. Create a notebook with the created personal image.
    1. Go to the **Notebook** menu. Click the **Create Notebook** button to go to the notebook creation page.
    2. Click the **Personal Images** tab in the image information.
    3. Select the personal image to use as the notebook container image.
    4. After entering other notebook information and creating it, the notebook will run with the personal image.

!!! tip "Note"
    Personal images can be used to create resources for notebooks, training, and hyperparameter tuning.

!!! tip "Note"
    Only NHN Container Registry (NCR) service can be integrated as a container registry service (as of December 2023).
    For the NCR service account ID and password, enter the following values:
    ID: User Access Key of NHN Cloud user account
    Password: User Secret Key of NHN Cloud user account

<a id="registry.account"></a>

## Registry Account

AI EasyMaker must log in to the user's registry to pull images from the user's registry where personal images are stored and run containers.
If you save login information as a registry account, it can be reused for images linked to that registry account.
To manage registry accounts, go to the **Image** menu in the AI EasyMaker console and select the **Registry Account** tab.

<a id="registry.account.create"></a>

### Create Registry Account

Create a new registry account.

- Name: Enter the name of the registry account.
- Description: Enter the description of the registry account.
- Category: Select the container registry service.
- ID: Enter the ID of the registry account.
- Password: Enter the password of the registry account.

<a id="registry.account.modify"></a>

### Modify Registry Account

<a id="registry.account.modify.account.modify"></a>

#### Modify Registry ID and Password

- Click the **Modify Registry Account** button.
- Enter the new ID and password, then click the **Confirm** button.

!!! tip "Note"
    When you change a registry account, the changed ID and password will be used for the registry service when using images linked to that account.
    If you enter an incorrect registry ID or password, authentication will fail during personal image pull, resulting in resource creation failure.

!!! danger "Caution"
    Problems may occur if you modify the ID and password when there are resources being created with personal images linked to the registry account, or when there are training and hyperparameter tuning in progress.
    Be careful when modifying the ID and password.

<a id="registry.account.modify.account.info.modify"></a>

#### Registry Account > Change Name and Description

1. Select the account to change from the registry account list.
2. Click the **Change** button in the bottom screen.
3. Change the name and description, then click the **Confirm** button.

<a id="registry.account.delete"></a>

### Delete Registry Account

Select the registry account to delete from the list and click the **Delete Registry Account** button.

!!! tip "Note"
    Registry accounts linked to images cannot be deleted. To delete them, you must first delete the linked images and then delete the registry account.

<a id="pipeline"></a>

## Pipeline

ML Pipeline is a feature for managing and executing portable and scalable machine learning workflows.
You can use the Kubeflow Pipelines (KFP) Python SDK to write components and pipelines, compile pipelines into intermediate representation YAML, and execute them in AI EasyMaker.
Most pipelines aim to produce one or more ML artifacts such as datasets, models, evaluation metrics, and so on.

!!! tip "Note"
    **Pipeline** is a definition of a workflow that combines one or more components to form a directed acyclic graph (DAG).
    - Each component runs a single container during execution, which can produce ML artifacts.
    - Components can receive inputs and generate outputs. There are two types of I/O types: parameters and artifacts.
    - Parameters are useful for passing small amounts of data between components.
    - Artifact types are for ML artifact outputs such as datasets, models, metrics, etc. They provide a convenient mechanism for storing in Object Storage.

!!! tip "Note"
    The feature to view console output generated while executing pipelines is not provided.
    Send logs from pipeline code to Log & Crash Search using [SDK's Log Send Feature](./sdk-guide/#feature.lncs.log.send) to check them.

!!! tip "Note"
    Kubeflow Pipelines (KFP) official documentation
    - [KFP User Guide](https://www.kubeflow.org/docs/components/pipelines/user-guides/)
    - [KFP SDK Reference](https://kubeflow-pipelines.readthedocs.io/ko/stable/)

<a id="pipeline.upload"></a>

### Pipeline Upload

Upload a pipeline.

- **Name**: Enter the pipeline name.
- **Description**: Enter the description.
- **File Register**: Select the YAML file to upload.

!!! tip "Note"
    Pipeline upload may take several minutes.
    When creating resources for the first time, it may take several additional minutes to configure the service environment.

<a id="pipeline.list"></a>

### Pipeline List

The pipeline list is displayed. When you select a pipeline from the list, you can view detailed information and modify the information.

- **Status**: The status of the pipeline is displayed. See the table below for major statuses.

    | Status             | Description                                       |
    |--------------------|---------------------------------------------------|
    | CREATE REQUESTED   | Pipeline creation has been requested.             |
    | CREATE IN PROGRESS | Pipeline creation is in progress.                 |
    | CREATE FAILED      | Pipeline creation has failed. Please try again.   |
    | ACTIVE             | Pipeline has been created successfully.           |

<a id="pipeline.graph"></a>

### Pipeline Graph

The pipeline graph is displayed. When you select a node in the graph, you can view detailed information.

A graph is a visual representation of a pipeline. Each node in the graph represents a step in the pipeline, and arrows show the parent/child relationships between pipeline components represented by each step.

<a id="pipeline.delete"></a>

### Pipeline Delete

Delete a pipeline.

1. Select the pipeline to delete.
2. Click **Delete Pipeline**. Pipelines that are being created cannot be deleted.
3. The requested delete operation cannot be canceled. To continue, click **Delete**.

!!! tip "Note"
    If there are schedules created with the pipeline you want to delete, you cannot delete the pipeline. Delete the pipeline schedule first, then delete the pipeline.

<a id="pipeline.run"></a>



## Pipeline Schedule

You can create and manage schedules to repeatedly run uploaded pipelines periodically in AI EasyMaker.

<a id="pipeline.recurring.run.create"></a>

### Create Pipeline Schedule

Create a schedule to repeatedly run pipelines periodically.

For information other than the items below that can be configured when creating a pipeline schedule, see [Create Pipeline Run](#pipeline.run.create).

- **Execution Information**
    - **Execution Type**: Select the pipeline execution type. When **Schedule Setting** is selected, the pipeline is repeatedly run periodically. To run the pipeline only once, select **One-time**.
    - **Trigger Type**: Select the pipeline execution trigger type. You can choose **Time Period** or **Cron Expression**.
        - To repeatedly run pipelines through time period settings, select **Time Period** and enter a number and time unit.
        - To repeatedly run pipelines through Cron expression settings, select **Cron Expression** and enter a Cron expression.
    - **Concurrent Execution Setting**: Depending on the trigger cycle (**Time Period** or **Cron Expression**), new pipeline executions may be created before previously created pipeline executions are terminated. You can limit the number of executions running in parallel by specifying the maximum number of concurrent executions.
    - **Start Time**: You can set the start time of the pipeline schedule. If not entered, pipeline executions are created according to the configured cycle.
    - **End Time**: You can set the end time of the pipeline schedule. If not entered, pipeline executions are created until stopped.
    - **Missed Run Catchup**: Determines whether to catch up when pipeline executions fall behind schedule.
        - For example, assuming a case where a pipeline schedule is temporarily stopped and then restarted later, setting it to **Enable** will catch up on missed pipeline executions.
        - If the pipeline internally handles backfill, it should be set to **Disable** to prevent duplicate backfill operations.

!!! tip "Note"
    Creating a pipeline schedule may take a few minutes.
    When creating resources for the first time, it may take an additional few minutes to configure the service environment.

!!! tip "Note"
    Cron expressions use 6 space-separated fields to represent time.
    For more details, see the [Cron Expression Format](https://pkg.go.dev/github.com/robfig/cron#hdr-CRON_Expression_Format) documentation.

<a id="pipeline.recurring.run.list"></a>

### Pipeline Schedule List

A list of pipeline schedules is displayed. Selecting a pipeline schedule from the list allows you to check detailed information and modify settings.

- **Status**: The status of the pipeline schedule is displayed. See the table below for major statuses.

    | Status                        | Description                                          |
    |-------------------------------|-----------------------------------------------------|
    | CREATE REQUESTED              | Pipeline schedule creation has been requested.       |
    | CREATE FAILED                 | Pipeline schedule creation has failed. Please try again. |
    | ENABLED                       | Pipeline schedule has started normally.             |
    | ENABLED(EXPIRED)              | Pipeline schedule has started normally but has passed the configured end time. |
    | DISABLED                      | Pipeline schedule has been stopped by user request.  |

- **Execution Management**: In the **Execution Management** tab of the detail screen displayed when selecting a pipeline schedule from the list, you can check the list of executions created by the pipeline schedule.

<a id="pipeline.recurring.run.start.stop"></a>

### Start and Stop Pipeline Schedule

Stop a started pipeline schedule or start a stopped pipeline schedule.

1. Select the pipeline schedule you want to start or stop from the list.
2. Click **Start Schedule** or **Stop Schedule**.

<a id="pipeline.recurring.run.copy"></a>

### Copy Pipeline Schedule

Create a new pipeline schedule with the same settings as an existing pipeline schedule.

1. Select the pipeline schedule you want to copy.
2. Click **Copy Pipeline Schedule**.
3. The pipeline schedule creation screen is displayed with the same settings as the existing pipeline schedule.
4. If there are settings you want to change, modify them and then click **Create Pipeline Schedule**.

<a id="pipeline.recurring.run.delete"></a>

### Delete Pipeline Schedule

Delete a pipeline schedule.

1. Select the pipeline schedule to delete.
2. Click **Delete Pipeline Schedule**.
3. The requested deletion operation cannot be canceled. To proceed, click **Delete**.

!!! tip "Note"
    If executions created by the pipeline schedule you want to delete are in progress, it cannot be deleted. Delete the pipeline schedule after the pipeline executions are completed.

<a id="rag"></a>



## Appendix

<a id="appendix.1.object.storage.account.permission"></a>

### 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage

When AI EasyMaker functions use your NHN Cloud Object Storage as input/output storage,
you must grant read or write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container for normal operation.

Granting read/write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container means that the AI EasyMaker system account can read or write files in your NHN Cloud Object Storage container according to the granted permissions.

You must verify this information and configure access policies for your Object Storage with only the necessary accounts and permissions.

All responsibility for any consequences arising from allowing accounts other than the AI EasyMaker system account to access your Object Storage during the access policy configuration process lies with the 'user', and AI EasyMaker bears no responsibility for such consequences.

!!! tip "Note"
    The files that AI EasyMaker accesses to read or write in Object Storage according to each function are as follows:

| Function       | Permission | Access Target                                            |
| ---------- | ---- | ---------------------------------------------------- |
| Training, Hyperparameter Tuning       | Read | Algorithm path and training input data path entered by user |
| Training, Hyperparameter Tuning       | Write | Training output data and checkpoint path entered by user   |
| Model       | Read | Model artifact path entered by user                   |
| Model Evaluation | Read | Input data path entered by user                   |
| Model Evaluation | Write | Output data path entered by user                   |
| Batch Inference | Read | Input data path entered by user                   |
| Batch Inference | Write | Output data path entered by user                   |
| RAG | Read | Collection data path entered by user                   |

To add AI EasyMaker system account read/write permissions to NHN Cloud Object Storage, see the following:

1. Click **AI EasyMaker System Account Information** in the **[Training]** or **[Model]** tab.
2. Save the AI EasyMaker system account information: **AI EasyMaker Tenant ID** and **AI EasyMaker API User ID**.
3. Go to the NHN Cloud Object Storage console.
4. Refer to the [Allow read/write access to specific projects or specific users](https://docs.nhncloud.com/en/Storage/Object%20Storage/ko/acl-guide/#role-based-access-allow-rw-project-or-user) document to add the necessary read and write permissions for the AI EasyMaker system account in the NHN Cloud Object Storage console.

<a id="appendix.2.lncs.service.usage.guide.and.log.inquiry.guide"></a>

### 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Query Method

<a id="appendix.2.lncs.service.usage.guide"></a>

#### NHN Cloud Log & Crash Search Service Usage Guide

Logs and events generated from the AI EasyMaker service can be stored in the NHN Cloud Log & Crash Search service.
To store logs in the Log & Crash Search service, you must enable the Log & Crash service, and separate usage fees will be charged.

- **Log & Crash Search Service Usage and Pricing Guide**
    - For detailed information and pricing on the Log & Crash Search service, see the following:
        - [Log & Crash Search Service Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/Overview/)
        - [Log & Crash Search Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Data%20%26%20Analytics&s=Log%20%26%20Crash%20Search)

<a id="appendix.2.lncs.service.log.inquiry.guide"></a>

#### Log Query

1. Go to the Log & Crash Search service console page.
2. Query logs by entering search conditions in the Log & Crash Search service.
    - AI EasyMaker training log query: Query logs where the category field is "easymaker.training".
        - Query: category:"easymaker.training"
    - AI EasyMaker endpoint log query: Query logs where the category field is "easymaker.inference".
        - Query: category:"easymaker.inference"
    - AI EasyMaker complete log query: Query logs where the logType field is "NHNCloud-AIEasyMaker".
        - Query: logType:"NHNCloud\-AIEasyMaker"
3. For detailed usage of the Log & Crash Search service, see the [Log & Crash Search Service Console Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/console-guide/).

The AI EasyMaker service sends logs to the Log & Crash Search service with fields defined as follows:

- **Common Log Fields**

    | Name            | Description                      | Valid Range                               |
    | --------------- | ------------------------- | --------------------------------------- |
    | easymakerAppKey | AI EasyMaker Appkey | -                                       |
    | category        | Log category             | easymaker.training, easymaker.inference |
    | logLevel        | Log level                 | INFO, WARNING, ERROR                    |
    | body            | Log content                 | -                                       |
    | logType         | Log providing service name     | NHNCloud-AIEasyMaker                    |
    | time            | Log occurrence time (UTC time)  | -                                       |

- **Training Log Fields**

    | Name       | Description                 |
    | ---------- | -------------------- |
    | trainingId | AI EasyMaker Training ID |

- **Hyperparameter Tuning Log Fields**

    | Name                   | Description                                |
    | ---------------------- | ----------------------------------- |
    | hyperparameterTuningId | AI EasyMaker Hyperparameter Tuning ID |

- **Endpoint Log Fields**

    | Name            | Description                        |
    | --------------- | --------------------------- |
    | endpointId      | AI EasyMaker Endpoint ID  |
    | endpointStageId | Endpoint stage ID      |
    | inferenceId     | Inference request unique ID           |
    | action          | Action classification(Endpoint.Model) |
    | modelName       | Inference target model name         |

- **Batch Inference Log Fields**

    | Name             | Description                      |
    | ---------------- | ------------------------- |
    | batchInferenceId | AI EasyMaker Batch Inference ID |

<a id="appendix.3.hyperparameter"></a>

### 3. Hyperparameters

- Key-Value format values entered through the console.
- When executing entry points, they are passed as execution arguments (--{Key}).
- They can also be used as environment variable values (EM*HP*{Key converted to uppercase}).

You can utilize hyperparameter values entered during training creation as shown in the example below.<br>
![Hyperparameter input screen](images/console-guide_appendix_hyperparameter_ko.png)

```python
import argparse

model_version = os.environ.get("EM_HP_MODEL_VERSION")

def parse_hyperparameters():
    parser = argparse.ArgumentParser()

    # Parse entered hyperparameters
    parser.add_argument("--epochs", type=int, default=500)
    parser.add_argument("--batch_size", type=int, default=32)
    ...

    return parser.parse_known_args()
```

<a id="appendix.4.environment"></a>

### 4. Environment Variables

- Information required for training is passed to the training container as **environment variables**, and the passed environment variables can be utilized in **training scripts**.
- Environment variable names created from user input are converted to uppercase.
- Models completed in the code must be saved to the EM_MODEL_DIR path.
- **Key Environment Variables**

    | Environment Variable Name                      | Description                                                                        |
    |-----------------------------| --------------------------------------------------------------------------- |
    | EM_SOURCE_DIR               | Absolute path of the folder where algorithm scripts entered during training creation are downloaded  |
    | EM_ENTRY_POINT              | Algorithm entry point name entered during training creation                             |
    | EM_DATASET_${Dataset Name}     | Absolute path of the folder where each dataset entered during training creation is downloaded |
    | EM_DATASETS                 | Complete dataset list (json format)                                            |
    | EM_MODEL_DIR                | Model save path                                                              |
    | EM_CHECKPOINT_INPUT_DIR     | Input checkpoint save path                                                  |
    | EM_CHECKPOINT_DIR           | Output checkpoint save path                                                  |
    | EM_HP_${Hyperparameter Key Converted to Uppercase} | Hyperparameter value corresponding to hyperparameter key                              |
    | EM_HPS                      | Complete hyperparameter list (json format)                                         |
    | EM_TENSORBOARD_LOG_DIR      | TensorBoard log path for checking training results                                    |
    | EM_REGION                   | Current region information                                                              |
    | EM_APPKEY                   | Appkey of the AI EasyMaker service currently in use                                   |

- **Environment Variable Usage Example Code**

```python
import os
import tensorflow

dataset_dir = os.environ.get("EM_DATASET_TRAIN")
train_data = read_data(dataset_dir, "train.csv")

model = ... # Implement model using input data
model.load_weights(os.environ.get('EM_CHECKPOINT_INPUT_DIR', None))
callbacks = [
    tensorflow.keras.callbacks.ModelCheckpoint(filepath=f'{os.environ.get("EM_CHECKPOINT_DIR")}/cp-{{epoch:04d}}.ckpt', save_freq='epoch', period=50),
    tensorflow.keras.callbacks.TensorBoard(log_dir=f'{os.environ.get("EM_TENSORBOARD_LOG_DIR")}'),
]
model.fit(..., callbacks)

model_dir = os.environ.get("EM_MODEL_DIR")
model.save(model_dir)
```

<a id="appendix.5.tensorboard.store.metric.log"></a>

### 5. Saving Metric Logs for TensorBoard

- To view result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage location to the designated location (`EM_TENSORBOARD_LOG_DIR`) when writing training scripts.

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

<details>
<summary><strong>Check TensorBoard Logs</strong></summary>

<img src="images/console-guide_appendix_tensorboard.png" alt="Check TensorBoard logs">

</details>

!!! danger "Caution"
    TensorBoard metric logs are retained for 120 days. Metric logs older than 120 days are automatically deleted.

<a id="appendix.6.framework.training.settings"></a>

### 6. Distributed Training Settings by Framework

- **Tensorflow**
    - The environment variable `TF_CONFIG` required for distributed training is automatically configured. For details, see the [Tensorflow official guide document](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy).
- **Pytorch**
    - `Backends` configuration is required for distributed training. Set to gloo for CPU distributed training and nccl for GPU distributed training. For details, see the [Pytorch official guide document](https://pytorch.org/docs/stable/distributed.html).

<a id="appendix.7.cluster.upgrade"></a>

### 7. Cluster Version Upgrade

The AI EasyMaker service periodically upgrades cluster versions to provide stable service and new features.
When a new cluster version is deployed, notebooks and endpoints running on old version clusters must be migrated to the new cluster.
This guide explains how to migrate to new clusters for each resource type.

<a id="appendix.7.cluster.upgrade.notebook"></a>

#### Notebook Cluster Version Upgrade

In the **Notebook** list screen, notebooks that need to be migrated to a new cluster display a **Restart** button to the left of the name.
Hovering the mouse pointer over the **Restart** button displays restart guidance and expiration date.

- Before expiration, be sure to check the following precautions and then click the **Restart** button.
    - Data stored in data storage (/root/easymaker directory path) will be preserved during restart.
    - When restart is executed, data stored in boot storage is initialized and may be lost. Move data to data storage before restarting.

Restart takes about 25 minutes for the first execution, and about 10 minutes thereafter.
If restart fails, it is automatically reported to administrators.

<a id="appendix.7.cluster.upgrade.endpoint"></a>

#### Endpoint Cluster Version Upgrade

In the **Endpoint List** screen, endpoints that need to be migrated to a new cluster display **! Notice** text to the left of the name.
Hovering the mouse pointer over the **! Notice** text displays version upgrade guidance and expiration date.
Before expiration, you must migrate stages operating on old version clusters to new version clusters according to the following guidance.

<a id="appendix.7.cluster.upgrade.endpoint.stage"></a>

##### General Stage Cluster Version Upgrade

1. Delete general stages that are not default stages. Before deletion, first check if the stage is in service.
2. Create the stage again.
3. When the new stage becomes ACTIVE, verify that API calls and inference responses come normally to the stage endpoint.

!!! danger "Caution"
    Deleting a stage terminates the endpoint, making API calls impossible. Before deletion, verify that the stage is not in service.

<a id="appendix.7.cluster.upgrade.endpoint.default.stage"></a>

##### Default Stage Cluster Version Upgrade

The default stage is where actual services operate.
To migrate the cluster version of the default stage without service interruption, follow this guide:

1. Create a new stage to replace the default stage of the old version cluster.
2. Verify that API calls and inference responses come normally from the new stage endpoint.
3. Click the **Change Default Stage** button. Select the new stage to change it to the default stage.
4. When the change is complete, the new stage is set as the default stage and the existing default stage is deleted.

<a id="appendix.8.torchrun.usage"></a>

### 8. How to Use torchrun

- If you write code to enable distributed training in Pytorch and enter the number of distributed nodes and number of processes per node, distributed training using distributed nodes and multi-processes with torchrun will be performed.
- Training and hyperparameter tuning may fail due to memory shortage caused by factors such as total number of processes, model size, input data size, and batch size. When failing due to memory shortage, the following error message may appear. However, not all occurrences of the message below indicate memory shortage failures. Set an appropriate instance type according to memory usage.

```plaintext
exit code : -9 (pid: {pid})
```

- For more details on torchrun, see the [Pytorch official guide document](https://pytorch.org/docs/stable/elastic/run.html).

<a id="appendix.9.resource.info"></a>

### 9. Resource Information

When creating batch inference and endpoints in AI EasyMaker, resources are allocated excluding basic usage from the selected instance type.
Since required resources vary depending on model request volume and complexity, carefully set appropriate instance types along with the number of pods and resource allocation.

Batch inference allocates resources to each pod by dividing actual usage by the number of pods. For endpoints, the entered allocation cannot exceed the actual usage of the instance, so check resource usage beforehand.
For both batch inference and endpoints, creation may fail if allocated resources are less than the minimum usage required for inference, so be careful.

<a id="appendix.10.endpoint.api.specification"></a>

### 10. Endpoint API Specification

The AI EasyMaker service provides endpoints based on the OIP (open inference protocol) specification.
For detailed information on the OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

| Name                    | Method | API Path                                                                |
| ----------------------- | ------ | ----------------------------------------------------------------------- |
| Model List               | GET    | /{model_name}/v1/models                                                 |
| Model Ready              | GET    | /{model_name}/v1/models/{model_name}                                    |
| Inference                    | POST   | /{model_name}/v1/models/{model_name}/predict                            |
| Explanation                    | POST   | /{model_name}/v1/models/{model_name}/explain                            |
| Server Information               | GET    | /{model_name}/v2                                                        |
| Server Live               | GET    | /{model_name}/v2/health/live                                            |
| Server Ready              | GET    | /{model_name}/v2/health/ready                                           |
| Model Information               | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]       |
| Model Ready              | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/ready |
| Inference                    | POST   | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/infer |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/completions                                     |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/chat/completions                                |

!!! tip "Note"
    OpenAI generative model inference is used when using generative models such as OpenAI's GPT-4o.
    Input values required for inference must be entered according to OpenAI's API specification. For details, see the [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat).
    For models supporting Completion and Chat Completion APIs provided by AI EasyMaker, check [Model endpoint compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility).

<a id="appendix.11.framework.note"></a>

### 11. Framework-Specific Serving Notes

<a id="appendix.11.framework.note.tensorflow.framework"></a>

#### TensorFlow Framework

TensorFlow model serving provided by AI EasyMaker uses SavedModel (.pb) recommended by TensorFlow.
To use checkpoints, save the checkpoint variables directory stored as SavedModel in the model directory together for use in model serving.
Reference: [https://www.tensorflow.org/guide/saved_model](https://www.tensorflow.org/guide/saved_model)

<a id="appendix.11.framework.note.pytorch.framework"></a>

#### PyTorch Framework

AI EasyMaker serves PyTorch models (.mar) with TorchServe.
It is recommended to use MAR files created with model-archiver, and serving is also possible with weight files, but additional files are needed along with weight files.
Check the table below and the [model-archiver documentation](https://github.com/pytorch/serve/blob/master/model-archiver/README.md) for required files and detailed explanations.

| File Name                    | Required | Description                                                              |
| ---------------------------- | --------- | ----------------------------------------------------------------- |
| model.py                     | Required      | Model structure file passed as model-file parameter.              |
| handler.py                   | Required      | File passed as handler parameter for processing inference logic. |
| Weight file (.pt, .pth, .bin) | Required      | File storing model weights and structure.                         |
| requirements.txt             | Optional      | File for installing Python packages needed for serving.        |
| extra/                       | Optional      | Files in the directory are passed as extra-files parameter.         |

!!! danger "Caution"
    There are differences in request format between using TorchServe directly and using AI EasyMaker serving, so be careful when writing handler.py.
    Check the values passed in the handler.py example below and write the handler accordingly.

<details>
<summary><strong>Request Example (cURL)</strong></summary>

```bash
curl --location --request POST '{API Gateway Resource Path}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "instances": [
        [1.0, 2.0],
        [3.0, 4.0]
    ]
}'
```

</details>

<details>
<summary><strong>Example (handler.py)</strong></summary>

```python
class TestHandler(BaseHandler):
    # ...
    def preprocess(self, data): # Example: data = [[1.0, 2.0], [3.0, 4.0]]
        features = []
        for row in data:
            content = row # Example: row = [1.0, 2.0]
            features.append(content)
        tensor = torch.tensor(features, dtype=torch.float32).to(self.device)
        return tensor
    # ...
```

</details>

<a id="appendix.11.framework.note.scikitlearn.framework"></a>

#### Scikit-learn Framework

AI EasyMaker serves Scikit-learn models (.joblib) with mlserver.
The `model-settings.json` required when using mlserver directly is not needed when using AI EasyMaker serving.

<a id="appendix.11.framework.note.hugging.face.framework"></a>

#### Hugging Face Framework

Hugging Face models can be served using AI EasyMaker's provided runtime or TensorFlow Serving, TorchServe.

<a id="appendix.11.framework.note.hugging.face.framework.runtime"></a>

##### Hugging Face Runtime

This is a convenient way to serve Hugging Face models.
Hugging Face runtime serving does not support fine-tuning. To serve fine-tuned models, use TensorFlow/Pytorch Serving methods.

1. Check the model to be served on Hugging Face.
2. Copy the Hugging Face model ID.
3. In the AI EasyMaker model creation page, select the Hugging Face framework and enter the Hugging Face model ID.
4. Enter the required input values according to the model to create the model.
5. Check the created model and create an endpoint.

!!! tip "Note"
    Currently, Hugging Face runtime does not support all Tasks from Hugging Face.
    Supported Tasks are `sequence_classification`, `token_classification`, `fill_mask`, `text_generation`, `text2text_generation`.
    To use unsupported Tasks, use TensorFlow/Pytorch Serving methods.

!!! tip "Note"
    To serve Gated Models, you must enter a token from an account with allowed access as a model parameter.
    If you do not enter a token or enter a token from an unauthorized account, model deployment will fail.

<a id="appendix.11.framework.note.hugging.face.framework.tensorflow.pytorch.serving"></a>

##### TensorFlow/PyTorch Serving

This is a method for serving Hugging Face models trained with TensorFlow and PyTorch.

1. Download the Hugging Face model.
    - You can download using AutoTokenizer, AutoConfig, AutoModel from the transformers library as shown in the example code below.

            from transformers import AutoTokenizer, AutoConfig, AutoModel

            model_id = "<model_id>"
            revision = "main"

            model_dir = f"./models/{model_id}/{revision}"

            tokenizer = AutoTokenizer.from_pretrained(model_id, revision=revision)
            model_config = AutoConfig.from_pretrained(model_id, revision=revision)
            model = AutoModel.from_config(model_config)

            tokenizer.save_pretrained(model_dir)
            model.save_pretrained(model_dir)

    - If model download fails, try downloading by importing the appropriate class for the model instead of AutoModel.
    - If fine-tuning is needed, you can write your own code for training according to the [Hugging Face fine-tuning guide](https://huggingface.co/docs/transformers/main/ko/training).
        - For detailed information on AI EasyMaker training, see [Training](#training).

2. Check the Hugging Face model information and create the files required for serving.
    - Save the model in the format required for serving by framework.
    - For details, check the notes for TensorFlow and PyTorch frameworks.
3. Upload the model files to OBS or NAS.
4. For subsequent processes, see the [Create Model](#model.create) and [Create Endpoint](#endpoint.create) guides.