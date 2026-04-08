<a id="ai.easymaker.console.guide"></a>

## Machine Learning > AI EasyMaker > Console Guide

<a id="dashboard"></a>

## Dashboard

You can check the usage status of all AI EasyMaker resources in the dashboard.

<a id="dashboard.service.usage.status"></a>

### Service Usage Status

Displays the number of resources in use by resource type.

- Notebook: Number of notebooks in ACTIVE(HEALTHY) status in use
- Training: Number of training sessions that are COMPLETE
- Hyperparameter Tuning: Number of hyperparameter tuning sessions that are COMPLETE
- Endpoint: Number of endpoints in ACTIVE status

<a id="dashboard.service.monitoring"></a>

### Service Monitoring

- Displays the top 3 endpoints with the most API calls.
- When you select an endpoint, you can check the API success/failure total metrics of the sub-endpoint stages.

<a id="dashboard.resource.usage"></a>

### Resource Usage

- You can check the resources with the highest usage by CPU and GPU core type.
- When you hover your mouse pointer over the metrics, resource information is displayed.

<a id="notebook"></a>

## Notebook

Create and manage Jupyter notebooks that come with essential packages installed for machine learning development.

<a id="notebook.create"></a>

### Create Notebook

Create a Jupyter notebook.

- **Image**: Select the OS image to be installed on the notebook instance.
    - **Core Type**: The CPU and GPU core type of the image is displayed.
    - **Framework**: The framework installed on the image is displayed.
        - TENSORFLOW: Image with TensorFlow deep learning framework installed.
        - PYTORCH: Image with PyTorch deep learning framework installed.
        - PYTHON: Image with only Python language installed without any deep learning framework.
    - **Framework Version**: The version of the framework installed on the image is displayed.
    - **Python Version**: The version of Python installed on the image is displayed.

- **Notebook Information**
    - Enter the name and description of the notebook.
    - Select the instance type for the notebook. The instance specifications are determined based on the selected type.

- **Storage**
    - Specify the boot storage and data storage size for the notebook.
        - Boot storage is where the Jupyter notebook and default virtual environment are installed. This storage is initialized when the notebook is restarted.
        - Data storage is block storage mounted to the `/root/easymaker` directory path. Data in this storage is maintained even when the notebook is restarted.
    - The storage size of created notebooks cannot be changed, so you must specify sufficient storage size at creation time.
    - If needed, you can connect **NHN Cloud NAS** to the notebook.
        - Mount Directory Name: Enter the name of the directory to mount on the notebook.
        - NHN Cloud NAS Path: Enter the directory path in the format `nas://{NAS ID}:/{path}`.

!!! tip "Note"
    Notebook creation may take several minutes.
    When creating resources for the first time, additional time is required to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="notebook.list"></a>

### Notebook List

The notebook list is displayed. Select a notebook from the list to view detailed information and modify settings.

- **Name**: The notebook name is displayed. You can change the name by clicking **Change** on the detail screen.
- **Status**: The status of the notebook is displayed. See the table below for main statuses.

    | Status               | Description                                                                                                                              |
    | ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Notebook creation has been requested.                                                                                                  |
    | CREATE IN PROGRESS | Notebook instance is being created.                                                                                           |
    | ACTIVE (HEALTHY)   | Notebook application is running normally.                                                                            |
    | ACTIVE (UNHEALTHY) | Notebook application is not running normally. If this status persists after restarting the notebook, please contact customer support. |
    | STOP IN PROGRESS   | Notebook is being stopped.                                                                                                    |
    | STOPPED            | Notebook has been stopped.                                                                                                       |
    | START IN PROGRESS  | Notebook is being started.                                                                                                    |
    | REBOOT IN PROGRESS | Notebook is being rebooted.                                                                                                  |
    | DELETE IN PROGRESS | Notebook is being deleted.                                                                                                    |
    | CREATE FAILED      | Failed while creating notebook. If creation continues to fail, please contact customer support.                                           |
    | STOP FAILED        | Failed to stop notebook. Please try again.                                                                              |
    | START FAILED       | Failed to start notebook. Please try again.                                                                              |
    | REBOOT FAILED      | Failed to reboot notebook. Please try again.                                                                            |
    | DELETE FAILED      | Failed to delete notebook. Please try again.                                                                              |

- **Actions > Open Jupyter Notebook**: Clicking the **Open Jupyter Notebook** button opens the notebook in a new browser window. The notebook can only be accessed by users logged into the console.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select a notebook, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when the notebook is being created or when there are ongoing operations.

<a id="notebook.user.virtual.run.environment.configuration"></a>

### Configure User Virtual Runtime Environment

AI EasyMaker notebook instances provide a default Conda virtual environment with various libraries and kernels required for machine learning installed.
The default Conda virtual environment is initialized and launched when the notebook is stopped and started, but virtual environments and external libraries installed by users in arbitrary paths are not automatically initialized, so they are not maintained when the notebook is stopped and started.
To solve this problem, you must create virtual environments in the `/root/easymaker/custom-conda-envs` directory path and install external libraries in the created virtual environments.
AI EasyMaker notebook instances support automatic initialization and launch of virtual environments created in the `/root/easymaker/custom-conda-envs` directory path when the notebook is stopped and started.

Follow the guide below to configure user virtual environments.

1. Click **Open Jupyter Notebook** > **Jupyter Notebook > Launcher > Terminal** in the console notebook menu.
2. Navigate to the `/root/easymaker/custom-conda-envs` path.

        cd /root/easymaker/custom-conda-envs

3. To create a virtual environment named `easymaker_env` with Python 3.8, execute the following `conda create` command.

        conda create --prefix ./easymaker_env python=3.8

4. The created virtual environment can be checked with the `conda env list` command.

        (base) root@nb-xxxxxx-0:~# conda env list
        # conda environments:
        #
                                /opt/intel/oneapi/intelpython/latest
                                /opt/intel/oneapi/intelpython/latest/envs/2022.2.1
        base                *   /opt/miniconda3
        easymaker_env           /root/easymaker/custom-conda-envs/easymaker_env

<a id="notebook.user.script"></a>

### User Script

Scripts that should be automatically executed when stopping and starting notebooks can be registered in the `/root/easymaker/cont-init.d` path.
They are executed in ascending alphanumeric order.

- Script location and permissions
    - Only files located in the `/root/easymaker/cont-init.d` path are executed.
    - Only scripts with execute permissions are executed.
- Script content
    - The first line of the script must start with `#!`.
    - Scripts are executed with root privileges.
- Script execution logs are saved in the following locations:
    - Script exit code: `/root/easymaker/cont-init.d/{SCRIPT}.exitcode`
    - Script standard output and standard error stream: `/root/easymaker/cont-init.d/{SCRIPT}.output`
    - Full execution log: `/root/easymaker/cont-init.output`

<a id="notebook.stop"></a>

### Stop Notebook

Stop a running notebook or start a stopped notebook.

1. Select the notebook you want to start or stop from the notebook list.
2. Click **Start Notebook** or **Stop Notebook**.
3. The requested operation cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    Starting and stopping notebooks may take several minutes.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be initialized when stopping and starting notebooks.
    To maintain virtual environments and external libraries when stopping and starting notebooks, configure user virtual environments by referring to [Configure User Virtual Runtime Environment](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.instance.type.change"></a>

### Change Notebook Instance Type

Change the instance type of a created notebook.
The instance type you want to change to can only be changed to an instance type with the same core type as the existing instance.

1. Select the notebook whose instance type you want to change.
2. If the notebook is in a running state (ACTIVE), click **Stop Notebook** to stop the notebook.
3. Click **Change Instance Type**.
4. Select the instance type you want to change to and click Confirm.

!!! tip "Note"
    Changing instance type may take several minutes.

<a id="notebook.reboot"></a>

### Reboot Notebook

If problems occur while using the notebook, or if the status is normal (ACTIVE) but the notebook is not accessible, you can reboot the notebook.

1. Select the notebook you want to reboot.
2. Click **Reboot Notebook**.
3. The requested operation cannot be canceled. Click **Confirm** to continue.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be initialized when rebooting notebooks.
    To maintain virtual environments and external libraries when rebooting notebooks, configure user virtual environments by referring to [Configure User Virtual Runtime Environment](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.delete"></a>

### Delete Notebook

Delete a created notebook.

1. Select the notebook you want to delete from the list.
2. Click **Delete Notebook**.
3. The requested delete operation cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    When deleting a notebook, boot storage and data storage are deleted.
    Connected NHN Cloud NAS is not deleted and must be deleted individually in **NHN Cloud NAS**.

<a id="experiment"></a>

## Experiment

Experiments group related training into experiments for management.

<a id="experiment.create"></a>

### Create Experiment

1. Click **Create Experiment**.
2. Enter the experiment name and description, then click **Confirm**.

!!! tip "Note"
    Creating an experiment may take a few minutes.
    When creating resources for the first time, it may take additional minutes to configure the service environment.

<a id="experiment.list"></a>

### Experiment List

The experiment list is displayed. Select an experiment from the list to view details and modify information.

- **Status**: The status of the experiment is displayed. See the table below for main statuses.

    | Status             | Description                                               |
    | ------------------ | --------------------------------------------------------- |
    | CREATE REQUESTED   | The experiment creation has been requested.              |
    | CREATE IN PROGRESS | The experiment is being created.                         |
    | CREATE FAILED      | The experiment creation failed. Please try again.        |
    | ACTIVE             | The experiment has been successfully created.            |

- **Tasks**
    - Click **TensorBoard Shortcut** to open TensorBoard in a new browser window where you can view statistical information of training included in the experiment. TensorBoard can only be accessed by users logged into the console.
    - **Retry**: When the experiment status is failed, you can click **Retry** to recover the experiment.
- **Training**: The **Training** tab in the detail screen displayed when selecting training shows the list of training included in the experiment.

<a id="experiment.delete"></a>

### Delete Experiment

Delete an experiment.

1. Select the experiment to delete.
2. Click **Delete Experiment**. You cannot delete an experiment if it is currently being created.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    You cannot delete an experiment if there are associated pipeline schedules or training, hyperparameter tuning, or pipeline executions being created.
    Delete the resources associated with the experiment before deleting the experiment.
    You can view the associated resources in the detail screen at the bottom that appears when you click the experiment you want to delete.

<a id="training"></a>



### Create Hyperparameter Tuning

This is how to configure hyperparameter tuning tasks.

- **Training Template**
    - **Use**: Select whether to use a training template. When using a training template, some configuration values for hyperparameter tuning are filled with predefined values.
    - **Training Template**: Select the training template to use for automatically entering some configuration values for hyperparameter tuning.
- **Basic Information**
    - **Hyperparameter Tuning Name**: Enter the name of the hyperparameter tuning task.
    - **Description**: Enter a description for the hyperparameter tuning task if needed.
    - **Experiment**: Select the experiment that will include the hyperparameter tuning. Experiments group related hyperparameter tunings. If no experiment has been created, click **Add** to create an experiment.
- **Tuning Strategy**
    - **Strategy Name**: Select which strategy to use to find optimal hyperparameters.
    - **Random Seed**: Determines random number generation. Specify a fixed value for reproducible results.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information about provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select the algorithm.
            - **Hyperparameter Spec**: Enter the hyperparameter value ranges to use for hyperparameter tuning. For detailed information about hyperparameters for each algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
                - **Name**: Define which hyperparameter to tune. This is predetermined for each algorithm.
                - **Type**: Select the data type of the hyperparameter. This is predetermined for each algorithm.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determines the change size of hyperparameter values when using the "Grid" tuning strategy.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use an algorithm written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the NHN Cloud Object Storage path where the algorithm is stored.
                    - Enter the directory path in the format obs://{Object Storage API Endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, refer to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to set permissions. Model creation will fail if necessary permissions are not set.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is stored.
                    - Enter the directory path in the format nas://{NAS ID}:/{path}.
            - **Entry Point**
                - The entry point is the entry point for algorithm execution where training begins. Write the entry point file name.
                - The entry point file must exist in the algorithm path.
                - If you write **requirements.txt** in the same path, the Python packages required by the script will be installed.
            - **Hyperparameter Spec**
                - **Name**: Define which hyperparameter to tune.
                - **Type**: Select the data type of the hyperparameter.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determines the change size of hyperparameter values when using the "Grid" tuning strategy.
                    - **Comma-separated values**: Tune hyperparameters using static values (e.g., sgd, adam).
- **Image**: Select the instance image suitable for the environment where training should be executed.
- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to execute training.
    - **Number of Training Instances**: The number of instances to perform training. The number of training instances is 'number of distributed nodes × number of parallel trainings'.
    - **Number of Distributed Nodes**: Enter the number of nodes to perform distributed training. Distributed training can be enabled through settings in the algorithm code. For details, see [Appendix > 6. Distributed Training Settings by Framework](#appendix.6.framework.training.settings).
    - **Number of Parallel Trainings**: Enter the number of trainings to perform simultaneously in parallel.
    - **Use torchrun**: Select whether to use torchrun supported by the PyTorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. Using torchrun enables distributed training by running multiple processes on one node. The number of processes affects memory usage.
- **Input Data**
    - **Data Set**: Enter the data set to execute training. Up to 10 data sets can be configured.
        - Data Set Name: Enter the data set name.
        - Data Path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to proceed with training from a saved checkpoint, enter the storage path of the checkpoint.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save training execution results.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides checkpoints, enter the storage path for checkpoints.
        - Generated checkpoints can be used to resume training from previous training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Metrics**
    - **Metric Name**: Define which metrics to collect from the logs output by the training code.
    - **Metric Format**: Enter the regular expression to use for collecting metrics. The training algorithm must output metrics according to the regular expression.
- **Target Metrics**
    - **Metric Name**: Select which metric to optimize as the target.
    - **Target Metric Type**: Select the optimization type.
    - **Target Value**: The tuning task terminates when the target metric reaches this value.
- **Tuning Resource Configuration**
    - **Maximum Number of Failed Trainings**: Define the maximum number of failed trainings. When the number of failed trainings reaches this value, tuning terminates with failure.
    - **Maximum Number of Trainings**: Define the maximum number of trainings. Tuning executes until the number of automatically executed trainings reaches this value.
- **Early Stopping**
    - **Name**: Terminates training early if the model does not improve further even if training continues.
    - **Minimum Number of Trainings**: Define from how many trainings to obtain target metric values when calculating the median.
    - **Starting Step**: Set from which training step to apply early stopping.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance to execute training.
        - Used only when using NHN Cloud Object Storage. Must be specified with sufficient size to store all data required for training.
    - **Maximum Duration**: Specify the maximum duration until training is completed. Trainings that exceed the maximum duration are terminated.
    - **Log Management**: Logs generated during training can be saved to the NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before training is completed may cause training to fail.

<a id="hyperparameter.tuning.list"></a>

### Hyperparameter Tuning List

The hyperparameter tuning list is displayed. You can select hyperparameter tuning from the list to check details and modify information.

- **Duration**: Displays the time taken for hyperparameter tuning.
- **Completed Training**: Indicates the number of training sessions completed among those automatically generated by hyperparameter tuning.
- **Training in Progress**: Indicates the number of training sessions in progress.
- **Failed Training**: Indicates the number of failed training sessions.
- **Best Training**: Indicates the target metric information of the training that achieved the best target metric value among those automatically generated by hyperparameter tuning.
- **Status**: The status of hyperparameter tuning is displayed. See the table below for key statuses.

    | Status                                                                           | Description                                                                                                                                              |
    | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                                               | The state where hyperparameter tuning creation has been requested.                                                                                                     |
    | CREATE IN PROGRESS                                                             | The state where resources required for hyperparameter tuning are being created.                                                                                         |
    | RUNNING                                                                        | The state where hyperparameter tuning is in progress.                                                                                                       |
    | STOPPED                                                                        | The state where hyperparameter tuning has been stopped by user request.                                                                                        |
    | COMPLETE                                                                       | The state where hyperparameter tuning has been completed normally.                                                                                               |
    | STOP IN PROGRESS                                                               | The state where hyperparameter tuning is being stopped.                                                                                                       |
    | FAIL HYPERPARAMETER TUNING                                                     | The state where hyperparameter tuning has failed during progress. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | CREATE FAILED                                                                  | The state where hyperparameter tuning creation has failed. If creation continues to fail, please contact customer support.                                               |
    | FAIL HYPERPARAMETER TUNING IN PROGRESS, COMPLETE IN PROGRESS, STOP IN PROGRESS | The state where resources used for hyperparameter tuning are being cleaned up.                                                                                       |

- **Status Details**: The content in parentheses for `COMPLETE` status is detailed status information. See the table below for key details.

    | Details            | Description                                                                                         |
    | -------------------- | -------------------------------------------------------------------------------------------- |
    | GoalReached          | Detailed information when hyperparameter tuning training is completed by reaching the target value.             |
    | MaxTrialsReached     | Detailed information when hyperparameter tuning is completed by reaching the maximum number of training sessions.               |
    | SuggestionEndReached | Detailed information when the hyperparameter tuning search algorithm has explored all hyperparameters. |

- **Actions**
    - **TensorBoard Shortcut**: Opens TensorBoard in a new browser window where you can check training statistics.<br/>
        For how to save TensorBoard logs, see [Appendix > 5. Saving Metric Logs for TensorBoard Usage](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Hyperparameter Tuning**: You can stop hyperparameter tuning in progress.

- **Monitoring**: In the **Monitoring** tab of the details screen that appears when you select hyperparameter tuning, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when hyperparameter tuning is in the creation state.

<a id="hyperparameter.tuning.training.list"></a>

### Training List for Hyperparameter Tuning

Displays the training list automatically generated by hyperparameter tuning. Select a training from the list to view detailed information.

- **Target Metric Value**: Represents the target metric value.
- **Status**: Displays the status of training automatically generated by hyperparameter tuning. See the table below for main statuses.

    | Status              | Description                                                                                                                   |
    | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
    | CREATED             | Training has been created.                                                                                                    |
    | RUNNING             | Training is in progress.                                                                                                      |
    | SUCCEEDED           | Training has completed normally.                                                                                              |
    | KILLED              | Training has been stopped by the system.                                                                                     |
    | FAILED              | Training failed during progress. For detailed failure information, if log management is enabled, you can check through Log & Crash Search logs. |
    | METRICS_UNAVAILABLE | Target metrics cannot be collected.                                                                                          |
    | EARLY_STOPPED       | Training was stopped early during progress because performance (target metrics) did not improve further.                    |

<a id="hyperparameter.tuning.copy"></a>

### Copy Hyperparameter Tuning

Creates new hyperparameter tuning with the same settings as existing hyperparameter tuning.

1. Select the hyperparameter tuning you want to copy.
2. Click **Copy Hyperparameter Tuning**.
3. The hyperparameter tuning creation screen appears with the same settings as the existing hyperparameter tuning.
4. If there is information you want to change in the settings, make the changes and then click **Create Hyperparameter Tuning** to create the hyperparameter tuning.

<a id="hyperparameter.tuning.model.create"></a>

### Create Model from Hyperparameter Tuning

Creates a model with the best training from completed hyperparameter tuning.

1. Select the hyperparameter tuning you want to create as a model.
2. Click **Create Model**. Only hyperparameter tuning in completed (COMPLETE) status can be created as a model.
3. You will be redirected to the model creation page. After reviewing the content, click **Create Model** to create the model.
   For more details on model creation, see the [Model](#model) document.

<a id="hyperparameter.tuning.delete"></a>

### Delete Hyperparameter Tuning

Deletes hyperparameter tuning.

1. Select the hyperparameter tuning you want to delete.
2. Click **Delete Hyperparameter Tuning**. Hyperparameter tuning in progress can be deleted after stopping.
3. The requested deletion operation cannot be canceled. To proceed, click **Confirm**.

!!! tip "Note"
    If there is a model created from the hyperparameter tuning you want to delete, you cannot delete the hyperparameter tuning. Delete the model first, then delete the hyperparameter tuning.

<a id="training.template"></a>

## Training Template

By creating training templates in advance, you can use the values entered in the template when creating training or hyperparameter tuning.

<a id="training.template.create"></a>

### Create Training Template

For information that can be set in training templates, see [Create Training](#training.create).

<a id="training.template.list"></a>

### Training Template List

The training template list is displayed. When you select a training template from the list, you can check detailed information and modify the information.

- **Task**
    - **Modify**: You can modify training template information.
- **Hyperparameters**: In the **Hyperparameters** tab of the details screen displayed when you select a training template, you can check the hyperparameter names set in the training template.

<a id="training.template.copy"></a>

### Copy Training Template

Creates a new training template with the same settings as an existing training template.

1. Select the training template you want to copy.
2. Click **Copy Training Template**.
3. The training template creation screen is displayed with the same settings as the existing training template.
4. If there is any information you want to modify, change it and then click **Create Training Template** to create the training template.

<a id="training.template.delete"></a>

### Delete Training Template

Deletes a training template.

1. Select the training template you want to delete.
2. Click **Delete Training Template**.
3. The requested delete operation cannot be canceled. To continue, click **Confirm**.

<a id="model"></a>

## Models

You can manage models from AI EasyMaker training results or external models as artifacts.

<a id="model.create"></a>

### Create Model

- **Basic Information**: Enter the basic information for the model.
    - **Name**: Enter the model name.
        - If the model framework type is PyTorch, you must enter a model name identical to the PyTorch model name.
    - **Description**: Enter the model description.
- **Framework Information**: Enter the framework information for the model.
    - **Framework**: Select the model framework.
    - **Framework Version**: Enter the version of the model framework.
- **Model Information**: Enter the storage where the model artifacts are stored.
    - **Model Artifact**: Select the storage where the model artifacts are stored.
        - **NHN Cloud Object Storage**: Enter the Object Storage path where the model artifacts are stored.
            - Enter the directory path in the format `obs://{Object Storage API Endpoint}/{containerName}/{path}`.
            - When using NHN Cloud Object Storage, refer to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to configure permissions. If permissions are not configured, model creation will fail due to inability to access the model artifacts.
        - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the model artifacts are stored.
            - Enter the directory path in the format `nas://{NAS ID}:/{path}`.
    - **Parameters**: Enter the parameter information for the model.
        - **Parameter Name**: Enter the model parameter name.
        - **Parameter Value**: Enter the model parameter value.

!!! tip "Note"
    Values entered as model parameters are used when serving the model. Parameters can be used as arguments and environment variables.
    Arguments are used exactly as the entered parameter name, and environment variables are used with the parameter name converted to screaming snake case.

!!! tip "Note"
    When creating a HuggingFace model, you can create the model by entering the HuggingFace model ID as a parameter.
    The HuggingFace model ID can be found in the URL of the HuggingFace model page.
    For more details, see [Appendix > 11. Framework-specific Serving Notes](#appendix.11.framework.note).

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

!!! danger "Caution"
    HuggingFace model file types are restricted to safetensors.
    Safetensors is a safe and efficient machine learning model file format developed by HuggingFace.
    Other file formats are not supported.

!!! danger "Caution"
    When creating TensorFlow (Triton), PyTorch (Triton), or ONNX (Triton) models, the model artifact path you enter must contain model files and `config.pbtxt` files stored in a structure that allows running the model with Triton.
    Refer to the example below.
    <details>
    <summary><strong>Example</strong></summary>

        model_name/
        ├── config.pbtxt                              # Model configuration file
        └── 1/                                        # Version 1 directory
            └── model.savedmodel/                     # TensorFlow SavedModel directory
                ├── saved_model.pb                    # Metagraph and checkpoint data
                └── variables/                        # Model weights directory
                    ├── variables.data-00000-of-00001
                    └── variables.index

    </details>

<a id="model.list"></a>

### Model List

The model list is displayed. Selecting a model from the list allows you to view detailed information and modify the information.

- **Name**: The model name and description are displayed. You can change the model name and description by clicking **Modify**.
- **Model Artifact Path**: The storage where the model artifacts are stored is displayed.
- **Status**: The model status is displayed. Refer to the table below for key statuses.

    | Status             | Description                                                                              |
    | ------------------ | ---------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | The model creation has been requested.                                                   |
    | CREATE IN PROGRESS | Resources required for the model are being created.                                     |
    | DELETE IN PROGRESS | The model is being deleted.                                                             |
    | ACTIVE             | The model has been created successfully.                                                |
    | CREATE FAILED      | Model creation has failed. If creation continues to fail, please contact customer support. |
    | DELETE FAILED      | Model deletion has failed. Please try again.                                           |

- **Training Name**: For models created from training, the name of the base training is displayed.
- **Training ID**: For models created from training, the ID of the base training is displayed.
- **Framework**: The model's framework information is displayed.
- **Parameters**: The model parameters are displayed. Parameters are used for inference.

<a id="model.endpoint.create"></a>

### Create Endpoint from Model

Create an endpoint that can serve the selected model.

1. Select the model you want to create as an endpoint from the list.
2. Click **Create Endpoint**.
3. You will be redirected to the **Create Endpoint** page. After reviewing the content, click **Create Endpoint**.
   For more details on endpoint creation, see the [Endpoint](#endpoint) documentation.

<a id="model.batch.inference.create"></a>

### Create Batch Inference from Model

Create batch inference that can perform batch inference with the selected model and view inference results as statistics.

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

Batch inference is automatically created during the model evaluation process.

- **Basic Information**: Enter the basic information for the model evaluation.
    - **Name**: Enter the model evaluation name.
    - **Description**: Enter the model evaluation description.
- **Model Information**: Enter information about the model to be evaluated.
    - **Model**: Select the model to evaluate. Only classification models and regression models are supported.
    - **Class Name**: Enter the class name of the model.
- **Model Evaluation Instance Information**
    - **Instance Type**: Select the instance type to run the model evaluation. Used for data preprocessing and evaluation calculation tasks.
- **Input Data**: Input data is used to compare predictions generated through batch inference with ground truth. Fields used for inference and ground truth fields are required.
    - **Data Path**: Enter the path where the input data is located.
        - **Input Data Type**: Select the format of the input data. CSV and JSONL formats are supported, and file extensions must be .csv and .jsonl respectively.
        - **Evaluation Target Field**: Enter the field name of the ground truth label.
- **Batch Inference Output Data**
    - **Data Path**: Enter the path where batch inference results will be saved.
- **Batch Inference Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Number of Instances**: Enter the number of instances to perform batch inference.
    - **Number of Pods**: Enter the number of pods for batch inference.
    - **Batch Size**: Enter the number of data samples processed simultaneously in a single inference task.
    - **Inference Timeout (seconds)**: Enter the timeout for batch inference. Sets the maximum allowed time for a single inference request to be processed and return results.
- **Additional Settings**
    - **Maximum Progress Time**: Specify the maximum progress time until model evaluation is completed. Model evaluations that exceed the maximum progress time are terminated.
    - **Log Management**: Logs generated during model evaluation progress can be saved to NHN Cloud Log & Crash service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Check](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - The size of input data used for model evaluation must be 20GB or less.
    - The number of classes for classification model evaluation must be 50 or less.

<a id="model.evaluation.list"></a>

### Model Evaluation List

The model evaluation list is displayed. Selecting a model evaluation from the list allows you to check detailed information and modify information.

- **Name**: The name of the model evaluation is displayed.
- **Model**: The name of the model used for model evaluation is displayed.
- **Status**: The status of the model evaluation is displayed. Refer to the table below for major statuses.

    | Status                                                   | Description                                                                                 |
    |----------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | CREATE REQUESTED                                         | Model evaluation creation has been requested.                                               |
    | CREATE IN PROGRESS                                       | Model evaluation is being created.                                                        |
    | CREATE FAILED                                            | Model evaluation creation failed. Please try again.                                       |
    | RUNNING                                                  | Model evaluation is in progress.                                                          |
    | COMPLETE IN PROGRESS, FAIL MODEL EVALUATION IN PROGRESS  | Resources used for model evaluation are being cleaned up.                                 |
    | COMPLETE                                                 | Model evaluation has been completed normally.                                             |
    | STOP IN PROGRESS                                         | Model evaluation is being stopped.                                                        |
    | STOPPED                                                  | Model evaluation has been stopped by user request.                                        |
    | FAIL MODEL EVALUATION                                    | Model evaluation failed. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | DELETE IN PROGRESS                                       | Model evaluation is being deleted.                                                        |

- **Actions**
    - **Stop**: You can stop a model evaluation in progress.

<a id="model.evaluation.classification.metric"></a>

### Classification Model Evaluation Metrics

- **PR AUC**: Area under the precision-recall (PR) curve. Effective for measuring classification performance of models on imbalanced datasets.
- **ROC AUC**: Area under the ROC curve (recall-false positive rate). The closer to 1, the better the performance.
- **Log Loss**: Loss value calculated using a log function for the difference between predicted probability and actual ground truth. Lower values mean the model's predictions are more reliable.
- **F1 Score**: Harmonic mean of precision and recall. Useful when there is class imbalance, and the closer to 1, the better.
- **Precision**: Ratio of actual positives among those predicted as positive. Focuses on reducing false positives.
- **Recall**: Ratio of correctly predicted positives among actual positives. Important for reducing false negatives.
- **Precision-Recall Curve**: Curve visualizing the relationship between precision and recall at various thresholds. Reference when adjusting model thresholds.
- **ROC Curve**: Shows the relationship between recall and false positive rate at various thresholds. Used for setting classification thresholds or comparing models.
- **Precision-Recall by Threshold Curve**: Graph showing how precision and recall change at specific thresholds. Reference when setting actual operation criteria.
- **Confusion Matrix**: Matrix categorizing prediction results into four types: TP, FP, FN, TN. Easily identifies error types by class.

<a id="model.evaluation.regression.metric"></a>

### Regression Model Evaluation Metrics

- **MAE (mean absolute error)**: Average of absolute values of differences between actual and predicted values. Intuitively shows the magnitude of prediction errors.
- **MAPE (mean absolute percentage error)**: Average of ratios of prediction errors divided by actual values. Being ratio-based, it may be unsuitable for data with values close to 0.
- **R-squared (coefficient of determination)**: Indicates how well the model explains actual data, with higher explanatory power as it approaches 1.
- **RMSE (root mean squared error)**: Square root of the mean squared error. More sensitive to large errors and results can be interpreted in the same units as actual values.
- **RMSLE (root mean squared logarithmic error)**: Calculated from differences between log-transformed actual and predicted values. Not sensitive to magnitude differences, useful for evaluating exponentially growing data.

<a id="model.evaluation.compare"></a>

### Model Evaluation Comparison

Compares evaluation metrics of multiple models.

1. Select the model evaluations you want to compare from the list.
2. Click **Compare**.

<a id="model.evaluation.delete"></a>

### Delete Model Evaluation

Deletes a model evaluation.

1. Select the model evaluation you want to delete.
2. Click **Delete**. Model evaluations in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

<a id="endpoint"></a>

## Endpoint

Create and manage endpoints for serving models.

<a id="endpoint.create"></a>

### Create Endpoint

- **API Gateway Service Activation**
    - AI EasyMaker endpoints create API endpoints and manage APIs through the NHN Cloud API Gateway service. To use the endpoint features, you must enable the API Gateway service.
    - For detailed information and pricing on the API Gateway service, see the following:
        - [API Gateway Service Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/ko/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Endpoint**: Choose whether to add a stage to a new or existing endpoint.
    - **Create as New Endpoint**: Creates a new endpoint. An endpoint is created in API Gateway as a new service with a default stage.
    - **Add New Stage to Existing Endpoint**: An endpoint is created as a new stage in the API Gateway service of an existing endpoint. Select the existing endpoint to which you want to add a stage.
- **Endpoint Name**: Enter the endpoint name. Endpoint names must be unique.
- **Stage Name**: When adding a new stage to an existing endpoint, enter the new stage name. Stage names must be unique.
- **Description**: Enter the endpoint stage description.
- **Instance Information**: Enter the instance information where the model will be served.
    - **Instance Type**: Select the instance type.
    - **Number of Instances**: Enter the number of running instances.
    - **Autoscaler**: The autoscaler is a feature that automatically adjusts the number of nodes according to resource usage policies. Autoscaler is configured per stage.
        - **Use/Disable**: Choose whether to use the autoscaler. When enabled, the number of instances scales in or out based on instance load.
        - **Minimum Number of Nodes**: Minimum number of nodes that can be scaled in
        - **Maximum Number of Nodes**: Maximum number of nodes that can be scaled out
        - **Scale-in**: Set whether node scale-in is enabled
        - **Resource Usage Threshold**: Reference value for the resource usage threshold range that is the basis for scale-in
        - **Threshold Range Duration (minutes)**: Duration of resource usage below the threshold for nodes to become scale-in targets
        - **Scale-in Delay Time After Scale-out (minutes)**: Delay time from node scale-out to starting monitoring as scale-in target nodes
- **Stage Information**: Enter the information of model artifacts to be deployed to the endpoint. When the same model is deployed with multiple stage resources, requests are distributed and processed.
    - **Model**: Select the model you want to deploy to the endpoint. If you haven't created a model, create the model first. For serving considerations by model framework, see [Appendix > 11. Framework-specific Serving Considerations](#appendix.11.framework.note).
    - **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance at a fixed ratio.
        - **cpu**: Enter the CPU allocation. Enter this when allocating directly without using the allocation ratio (%).
        - **memory**: Enter the Memory allocation. Enter this when allocating directly without using the allocation ratio (%).
        - **gpu**: Enter the GPU allocation. Enter this when allocating directly without using the allocation ratio (%).
    - **Description**: Enter the stage resource description.
    - **Pod Autoscaler**: A feature that automatically adjusts the number of pods according to the model's request volume. Autoscaler is configured per model.
        - **Use/Disable**: Choose whether to use the autoscaler. When enabled, the number of pods scales in or out based on model load.
        - **Scale-out Unit**: Enter the pod scale-out unit.
            - **CPU**: The number of pods is adjusted according to CPU usage.
            - **Memory**: The number of pods is adjusted according to Memory usage.
        - **Threshold Value**: The threshold value per scale-out unit at which pods will be scaled out.
    - **Resource Information**: You can check the actual resources being used. Allocates actual resource usage to each model according to the entered model's allocation. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).

!!! tip "Note"
    The AI EasyMaker service provides endpoints based on the OIP (open inference protocol) specification. For endpoint API specification details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
    To use a separate endpoint, create new resources by referring to the resources created in the API Gateway service.
    For more details on the OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

!!! tip "Note"
    Creating an endpoint may take several minutes.
    When creating resources for the first time, it may take additional minutes to configure the service environment.

!!! tip "Note"
    Creating a new endpoint creates a new API Gateway service.
    Adding a new stage to an existing endpoint creates a new stage in the API Gateway service.
    If the basic allocation amount of the [API Gateway Service Resource Provision Policy](https://docs.nhncloud.com/en/nhncloud/ko/resource-policy/#api-gateway) is exceeded, endpoint creation may not be possible in AI EasyMaker. In this case, you can resolve this by adjusting the API Gateway service resource quota.

<a id="endpoint.list"></a>

### Endpoint List

The endpoint list is displayed. Select an endpoint from the list to view details and modify information.

- **Default Stage URL**: The URL of the default stage among the endpoint stages is displayed.
- **Status**: The endpoint status. See the table below for key statuses.

    | Status             | Description                                                                                                                                                           |
    | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Endpoint creation has been requested.                                                                                                                                 |
    | CREATE IN PROGRESS | The endpoint is being created.                                                                                                                                        |
    | UPDATE IN PROGRESS | Some stages of the endpoint have tasks in progress.<br/>You can check the task status for each stage in the endpoint stage list.                                   |
    | DELETE IN PROGRESS | The endpoint is being deleted.                                                                                                                                        |
    | ACTIVE             | The endpoint is running normally.                                                                                                                                     |
    | CREATE FAILED      | Endpoint creation has failed.<br/>The endpoint must be deleted and recreated. If the creation failure status persists, please contact customer support.           |
    | UPDATE FAILED      | Some stages of the endpoint are not serving properly. The problematic stage must be deleted and recreated.                                                          |

- **API Gateway Status**: API Gateway status information for the endpoint's default stage is displayed. See the table below for key statuses.

    | Status                         | Description                                                                                                                                                                                                                                 |
    | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE IN PROGRESS             | API Gateway resources are being created.                                                                                                                                                                                                   |
    | STAGE DEPLOYING                | The API Gateway default stage is being deployed.                                                                                                                                                                                           |
    | ACTIVE                         | The API Gateway default stage has been deployed and activated normally.                                                                                                                                                                    |
    | NOT FOUND: STAGE               | The endpoint's default stage cannot be found.<br/>Check if the stage exists in the API Gateway console.<br/>If the stage has been deleted, the deleted API Gateway stage cannot be recovered and the endpoint must be deleted and recreated. |
    | NOT FOUND: STAGE DEPLOY RESULT | The deployment status of the endpoint's default stage cannot be found.<br/>Check if the default stage is deployed in the API Gateway console.                                                                                           |
    | STAGE DEPLOY FAIL              | The API Gateway default stage deployment has failed.                                                                                                                                                                                       |

<a id="endpoint.stage.create"></a>

### Create Endpoint Stage

Add a new stage to an existing endpoint. You can create a new stage to test it without affecting the default stage.

1. Click **Endpoint Name** in the endpoint list.
2. Click **+ Create Stage**.
3. Adding a new stage to an existing endpoint is automatically selected, and the configuration method is the same as endpoint creation.
4. The requested deletion operation cannot be canceled. To proceed, click **Confirm**.

<a id="endpoint.stage.list"></a>

### Endpoint Stage List

The list of stages created under the endpoint is displayed. You can check detailed information by selecting a stage from the list.

- **Status**: The status of the endpoint stage is displayed. Refer to the table below for key statuses.

    | Status             | Description                                                                     |
    | ------------------ | ------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | The endpoint stage creation has been requested.                                 |
    | CREATE IN PROGRESS | The endpoint stage is being created.                                           |
    | DEPLOY IN PROGRESS | A model is being deployed to the endpoint stage.                               |
    | DELETE IN PROGRESS | The endpoint stage is being deleted.                                           |
    | ACTIVE             | The endpoint stage is running normally.                                        |
    | CREATE FAILED      | Endpoint stage creation has failed. Please try again.                          |
    | DEPLOY FAILED      | Endpoint stage deployment has failed. Please try creating again.               |

- **API Gateway Status**: The stage status of the API Gateway where the endpoint stage is deployed is displayed.
- **Default Stage**: Whether it is the default stage is displayed.
- **Stage URL**: The stage URL of the API Gateway where the model is served is displayed.
- **View API Gateway Settings**: To check the settings deployed by AI EasyMaker to the API Gateway stage, click **View Settings**.
- **View API Gateway Statistics**: To view API statistics of the endpoint, click **View Statistics**.
- **Instance Type**: The endpoint instance type where the model is served is displayed.
- **Running Work Nodes/Pods**: The number of nodes and pods in use by the endpoint is displayed.
- **Stage Resource**: Information about the model artifacts deployed to the stage is displayed.
- **Monitoring**: In the **Monitoring** tab of the details screen displayed when you select an endpoint stage, you can check the list of monitoring target instances and basic metrics charts.
    - The **Monitoring** tab is disabled when the endpoint stage is in a creating state.
- **API Statistics**: In the **API Statistics** tab of the details screen displayed when you select an endpoint stage, you can check API statistics information for the endpoint stage.
    - The **API Statistics** tab is disabled when the endpoint stage is in a creating state.

!!! danger "Caution"
    When AI EasyMaker creates an endpoint or endpoint stage, it creates API Gateway services and stages for the endpoint.
    If you directly make changes to API Gateway services and stages created by AI EasyMaker through the API Gateway service console, please be sure to refer to the following cautions.

    1. Do not delete the API Gateway services and stages created by AI EasyMaker. If deleted, API Gateway information may not display properly in the endpoint, and endpoint changes may not be applied to API Gateway.
    2. Do not change or delete the resources of the API Gateway resource path entered when creating the endpoint. If deleted, the endpoint's inference API calls may fail.
    3. Do not add resources under the API Gateway resource path entered when creating the endpoint. Added resources may be deleted when adding/changing endpoint stages.
    4. Do not disable **Backend Endpoint URL Override** set in the API Gateway resource path or change the URL in the API Gateway stage settings. If changed, the endpoint's inference API calls may fail.
       Other settings besides the above cautions can use the features provided by API Gateway as needed.
       For detailed API Gateway usage, see [API Gateway Console Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/ko/console-guide/).

!!! tip "Note"
    If AI EasyMaker endpoint stage settings are not deployed to the API Gateway stage due to temporary issues, it will be displayed as 'deployment failed' status.
    In this case, you can manually deploy the API Gateway stage by selecting a stage from the stage list > **View API Gateway Settings** in the bottom details screen > clicking **Deploy Stage**.
    If the deployment status is not recovered with the above guide, please contact customer support.

<a id="endpoint.stage.resource.create"></a>

### Create Stage Resource

Add new resources to an existing endpoint stage.

- **Model**: Select the model you want to deploy to the endpoint. If you have not created a model, create a model first.
- **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance at a fixed ratio.
    - **CPU**: Enter the CPU allocation. Enter this if you want to allocate directly without using allocation percentage (%).
    - **Memory**: Enter the memory allocation. Enter this if you want to allocate directly without using allocation percentage (%).
- **Number of Pods**: Enter the number of pods for the stage resource.
- **Description**: Enter the stage resource description.
- **Pod Autoscaler**: A feature that automatically adjusts the number of pods according to model request volume. The autoscaler is configured on a per-model basis.
    - **Enable/Disable**: Select whether to use the autoscaler. When enabled, the number of pods scales in or out according to model load.
    - **Scale-out Unit**: Enter the pod scale-out unit.
        - **CPU**: The number of pods is adjusted according to CPU usage.
        - **Memory**: The number of pods is adjusted according to memory usage.
    - **Threshold Value**: The threshold value per scale-out unit at which pods will be scaled out.

<a id="endpoint.stage.resource.list"></a>

### Stage Resource List

Displays the list of resources created under the endpoint stage.

- **Status**: Displays the status of the stage resource. See the table below for key statuses.

    | Status             | Description                                                   |
    | ------------------ | ------------------------------------------------------------- |
    | CREATE REQUESTED   | Stage resource creation has been requested.                  |
    | CREATE IN PROGRESS | Stage resource is being created.                            |
    | DELETE IN PROGRESS | Stage resource is being deleted.                            |
    | ACTIVE             | Stage resource has been deployed successfully.              |
    | CREATE FAILED      | Stage resource creation has failed. Please try again.       |

- **Model Name**: Name of the model deployed to the stage.
- **API Gateway Resource Path**: Inference URL of the model deployed to the stage. You can request inference using the displayed URL. For more details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
- **Number of Pods**: Displays the number of healthy pods and total pods in use by the resource.

<a id="endpoint.inference.call"></a>

### Endpoint Inference Call

1. Click a stage in **Endpoint** > **Endpoint Stage** to display the stage detail screen at the bottom.
2. Check the API Gateway resource path in the Stage Resource tab of the detail screen.
3. Call the inference API by calling the API Gateway resource path with HTTP POST Method.
    - The request and response specifications of the inference API differ according to the algorithm written by the user.

            // Inference API example: Request
            curl --location --request POST '{API Gateway resource path}' \
            --header 'Content-Type: application/json' \
            --data-raw '{
                "instances": [
                    [6.8,  2.8,  4.8,  1.4],
                    [6.0,  3.4,  4.5,  1.6]
                ]
            }'

            // Inference API example: Response
            {
                "predictions" : [
                    [
                        0.337502569,
                        0.332836747,
                        0.329660654
                    ],
                    [
                        0.337530434,
                        0.332806051,
                        0.329663515
                    ]
                ]
            }

<a id="endpoint.stage.resource.delete"></a>

### Delete Stage Resource

1. Click **Endpoint Name** in the endpoint list to move to the endpoint stage list.
2. Click the endpoint stage where the stage resource to be deleted is deployed in the endpoint stage list. When clicked, the stage detail screen is displayed at the bottom.
3. Select the stage resource to delete in the **Stage Resource** tab of the detail screen.
4. Click **Delete Stage Resource**.
5. The requested delete operation cannot be canceled. To continue, click **Confirm**.

<a id="endpoint.default.stage.change"></a>

### Change Endpoint Default Stage

Change the default stage of the endpoint to another stage.
To change the model of an endpoint without service interruption, AI EasyMaker recommends deploying models using the stage feature.

1. The stage currently in operation as an actual service operates on the default stage.
2. When replacing with a new model, add a new stage to the existing endpoint.
3. Check whether there are any problems with the endpoint service with the replaced model in the new stage.
4. Click **Change Default Stage**.
5. Select the new stage to change to the default stage from Change to Stage.
6. The change request operation cannot be canceled. To continue, click **Confirm**.
7. The stage to be changed becomes the default stage, and the resources of the existing default stage are automatically deleted.

<a id="endpoint.stage.delete"></a>

### Delete Endpoint Stage

1. Click **Endpoint Name** in the endpoint list to move to the endpoint stage list.
2. Select the endpoint stage to delete in the endpoint stage list. The default stage cannot be deleted.
3. Click **Delete Stage**.
4. The requested delete operation cannot be canceled. To continue, click **Confirm**.

!!! danger "Caution"
    When you delete an endpoint stage in AI EasyMaker, the stage of the API Gateway service where the endpoint stage is deployed is also deleted.
    If there are APIs in operation in the API Gateway stage to be deleted, API calls will not be possible, so be careful.

<a id="endpoint.delete"></a>

### Delete Endpoint

Delete an endpoint.

1. Select the endpoint you want to delete from the endpoint list.
2. If there are stages other than the default stage under the endpoint, you cannot delete the endpoint. Delete other stages first and then delete the endpoint.
3. Click **Delete Endpoint**.
4. The requested delete operation cannot be canceled. To continue, click **Confirm**.

!!! danger "Caution"
    When you delete an endpoint in AI EasyMaker, the API Gateway service where the endpoint is deployed is also deleted.
    If there are APIs in operation in the API Gateway service to be deleted, API calls will not be possible, so be careful.

<a id="batch.inference"></a>

## Batch Inference

Provides an environment where you can perform batch inference with AI EasyMaker models and check inference results through statistics.

<a id="batch.inference.create"></a>

### Create Batch Inference

Set up the environment where batch inference will be performed by selecting instances and OS images, and proceed with batch inference by entering the paths of input/output data to be inferred.

- **Basic Information**: Enter basic information about batch inference.
    - **Batch Inference Name**: Enter the batch inference name.
    - **Batch Inference Description**: Enter a description.
- **Instance Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Number of Instances**: Number of instances to perform batch inference.
- **Model Information**
    - **Model**: Select the model for batch inference. If you haven't created a model, create a model first.
    - **Number of Pods**: Enter the number of pods for the model.
    - **Resource Information**: You can check the resources actually used by the model. According to the number of pods entered, the actual usage is divided and allocated to each pod. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).
- **Input Data**
    - **Data Path**: Enter the path of data to execute batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Input Data Type**: Select the type of data to execute batch inference.
        - **JSON**: Use valid JSON data in the file as input values.
        - **JSONL**: Use JSON Lines files where each line consists of valid JSON as input values.
            - Reference: [https://jsonlines.org/](https://jsonlines.org/)
    - **Glob Pattern**
        - **Include File Specification**: Enter the file set to include in input data as a Glob pattern.
        - **Exclude File Specification**: Enter the file set to exclude from input data as a Glob pattern.
- **Output Data**
    - **Output Data**: Enter the data storage path to save the execution results of batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Batch Options**
        - **Batch Size**: Enter the number of data samples processed simultaneously in one inference task.
        - **Inference Timeout (seconds)**: Enter the timeout for batch inference. You can set the maximum allowed time for a single inference request to be processed and results to be returned.
    - **Data Storage Size**: Enter the data storage size of the instance to execute batch inference.
        - Used only when using NHN Cloud Object Storage. You must specify sufficient size to store all data required for batch inference.
    - **Maximum Batch Inference Time**: Specify the maximum wait time until batch inference is completed. Batch inference that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during batch inference can be saved to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Good to Know"
    - When using Glob patterns, **exclude Glob patterns** are applied with priority.
    - You must appropriately set **batch size** and **inference timeout** according to the performance of the model performing batch inference. If the entered setting values are incorrect, batch inference may not achieve sufficient performance.

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before batch inference is completed may cause batch inference to fail.
    - When using Glob patterns, if values are not entered appropriately, input data cannot be found and batch inference may not work normally.

!!! danger "Caution"
    Batch inference using GPU instances allocates GPU instances according to the number of pods.
    If `number of pods / number of GPUs` is not divisible by an integer, unallocated GPUs may occur.
    Since unallocated GPUs are not used for batch inference, set the number of pods appropriately to use GPU instances efficiently.

<a id="batch.inference.list"></a>

### Batch Inference List

The batch inference list is displayed. When you select batch inference from the list, you can check detailed information and change information.

- **Inference Duration**: The time batch inference has been running is displayed.
- **Status**: The status of batch inference is displayed. Refer to the table below for major statuses.

    | Status                                                   | Description                                                                                                                                   |
    | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                       | Status where batch inference creation has been requested.                                                                                                    |
    | CREATE IN PROGRESS                                     | Status where resources required for batch inference are being created.                                                                                        |
    | RUNNING                                                | Status where batch inference is in progress.                                                                                                      |
    | STOPPED                                                | Status where batch inference has been stopped by user request.                                                                                       |
    | COMPLETE                                               | Status where batch inference has been completed normally.                                                                                              |
    | STOP IN PROGRESS                                       | Status where batch inference is being stopped.                                                                                                      |
    | FAIL BATCH INFERENCE                                   | Status where failure occurred during batch inference. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                          | Status where batch inference creation has failed. If creation continues to fail, please contact customer support.                                              |
    | FAIL BATCH INFERENCE IN PROGRESS, COMPLETE IN PROGRESS | Status where resources used for batch inference are being cleaned up.                                                                                      |

- **Actions**
    - **Stop**: You can stop batch inference in progress.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select batch inference, you can check the list of monitoring target instances and basic indicator charts.
    - The **Monitoring** tab is disabled when batch inference is in creation status.

<a id="batch.inference.copy"></a>

### Copy Batch Inference

Creates new batch inference with the same settings as existing batch inference.

1. Select the batch inference you want to copy.
2. Click **Copy Batch Inference**.
3. The batch inference creation screen is displayed with the same settings as the existing batch inference.
4. If there is information you want to change settings for, change it and click **Create Batch Inference** to create batch inference.

<a id="batch.inference.delete"></a>

### Delete Batch Inference

Deletes batch inference.

1. Select the batch inference you want to delete.
2. Click **Delete Batch Inference**. Batch inference in progress can be deleted after stopping.
3. The requested delete operation cannot be canceled. To continue, click **Confirm**.

<a id="personal.image"></a>

## Personal Images

Users can run notebooks, training, and hyperparameter tuning using personalized container images.
Only personal images derived from the notebook/deep learning images provided by AI EasyMaker can be used when creating resources in AI EasyMaker.
Check the table below for AI EasyMaker's base images.

<a id="personal.image.notebook.image"></a>

#### Notebook Images

| Image Name                          | Core Type | Framework | Framework Version | Python Version | Image URL                                                                                            |
| ------------------------------------ | -------- | ---------- | --------------- | ----------- | ------------------------------------------------------------------------------------------------------ |
| Ubuntu 22.04 CPU Python Notebook     | CPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204    |
| Ubuntu 22.04 GPU Python Notebook     | GPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-gpu-py310-ubuntu2204    |
| Ubuntu 22.04 CPU PyTorch Notebook    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Notebook    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Notebook | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Notebook | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-gpu-py310-ubuntu2204 |

<a id="personal.image.deep.learning.image"></a>

#### Deep Learning Images

| Image Name                          | Core Type | Framework | Framework Version | Python Version | Image URL                                                                                         |
| ------------------------------------ | -------- | ---------- | --------------- | ----------- | --------------------------------------------------------------------------------------------------- |
| Ubuntu 22.04 CPU PyTorch Training    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Training    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Training | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Training | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-gpu-py310-ubuntu2204 |

!!! tip "Note"
    Only NHN Container Registry (NCR) can be integrated as the Container Registry service where personal images are stored (as of December 2023).

!!! danger "Caution"
    Only personal images derived from base images provided by AI EasyMaker can be used.

<a id="personal.image.create"></a>

### Create Personal Images

The following document guides you on how to create container images using AI EasyMaker base images with Docker and use personal images for notebooks in AI EasyMaker.

1. Write the DockerFile for your personal image.

        FROM fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204 as easymaker-notebook
        RUN conda create -n example python=3.10
        RUN conda activate example
        RUN pip install torch torchvision

2. Build personal image and push to Container Registry
    Build the image from the Dockerfile and push the image to the NCR registry.

        docker build -t {Image Name}:{Tag} .
        docker tag {Image Name}:{Tag} {NCR Registry Address}/{Image Name}:{Tag}
        docker push {NCR Registry Address}/{Image Name}:{Tag}

        # Example
        docker build -t custom-training:v1 .
        docker tag custom-training:v1 example-kr1-registry.container.nhncloud.com/registry/custom-training:v1
        docker push example-kr1-registry.container.nhncloud.com/registry/custom-training:v1

3. Create the image pushed to NCR as a personal image in AI EasyMaker.

    1. Go to the **Image** menu in the AI EasyMaker console.
    2. Click the **Create Image** button and enter information about the created image.
        - Name, Description: Enter the name and description for the image.
        - Address: Enter the registry image address.
        - Type: Enter the type of container image. Select **Notebook** or **Training**.
        - Account: Select an account for AI EasyMaker notebook/training nodes to access your registry repository.
            - Create New: Register a new registry account.
                - Name, Description: Enter the name and description for the registry account.
                - Category: Select the Container Registry service.
                - ID: Enter the ID of the registry repository.
                - Password: Enter the password of the registry repository.
            - Use Existing Account: Select an already registered registry account.

4. Create a notebook using the created personal image.
    1. Go to the **Notebook** menu. Click the **Create Notebook** button to go to the notebook creation page.
    2. Click the **Personal Image** tab in the image information.
    3. Select the personal image to use as the notebook container image.
    4. After entering other notebook information and creating it, the notebook will run with the personal image.

!!! tip "Note"
    Personal images can be used to create resources for notebooks, training, and hyperparameter tuning.

!!! tip "Note"
    Only NHN Container Registry (NCR) service can be integrated as the Container Registry service (as of December 2023).
    For NCR service account ID and password, enter the following values:
    ID: User Access Key of NHN Cloud user account
    Password: User Secret Key of NHN Cloud user account

<a id="registry.account"></a>

## Registry Accounts

For AI EasyMaker to pull images from a user's registry where private images are stored and run containers, it must log in to the user's registry.
By storing login information as registry accounts, you can reuse them for images linked to that registry account.
To manage registry accounts, go to the **Image** menu in the AI EasyMaker console and select the **Registry Accounts** tab.

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
    When you change a registry account, the registry service will use the changed ID and password when using images linked to that account.
    If you enter an incorrect registry ID or password, authentication will fail during private image pull, causing resource creation to fail.

!!! danger "Caution"
    If there are resources being created with private images linked to the registry account, or if there are training and hyperparameter tuning tasks in progress, modifying the ID and password may cause problems.
    Be careful when modifying IDs and passwords.

<a id="registry.account.modify.account.info.modify"></a>

#### Registry Account > Change Name and Description

1. Select the account to change from the registry account list.
2. Click the **Change** button in the bottom screen.
3. Change the name and description, then click the **Confirm** button.

<a id="registry.account.delete"></a>

### Delete Registry Account

Select the registry account to delete from the list and click the **Delete Registry Account** button.

!!! tip "Note"
    Registry accounts linked to images cannot be deleted. To delete them, you must first delete the linked images, then delete the registry account.

<a id="pipeline"></a>

## Pipeline

ML Pipeline is a feature for managing and executing portable and scalable machine learning workflows.
You can use the Kubeflow Pipelines (KFP) Python SDK to write components and pipelines, compile pipelines into intermediate representation YAML, and execute them in AI EasyMaker.
Most pipelines aim to produce one or more ML artifacts such as datasets, models, evaluation metrics, etc.

!!! tip "Note"
    A **pipeline** is a definition of a workflow that combines one or more components to form a directed acyclic graph (DAG).
    - Each component runs a single container during execution, which can generate ML artifacts.
    - Components can receive inputs and generate outputs. There are two types of I/O types: parameters and artifacts.
    - Parameters are useful for passing small amounts of data between components.
    - Artifact types are for ML artifact outputs such as datasets, models, metrics, etc. They provide a convenient mechanism for storing in Object Storage.

!!! tip "Note"
    The ability to view console output that occurs while running pipelines is not provided.
    Send pipeline code logs to Log & Crash Search using the [SDK's Log transmission feature](./sdk-guide/#feature.lncs.log.send) to check them.

!!! tip "Note"
    Kubeflow Pipelines (KFP) official documentation
    - [KFP User Guide](https://www.kubeflow.org/docs/components/pipelines/user-guides/)
    - [KFP SDK Reference](https://kubeflow-pipelines.readthedocs.io/ko/stable/)

<a id="pipeline.upload"></a>

### Upload Pipeline

Upload a pipeline.

- **Name**: Enter the pipeline name.
- **Description**: Enter a description.
- **Register File**: Select the YAML file to upload.

!!! tip "Note"
    Pipeline upload may take several minutes.
    When creating a resource for the first time, it takes additional minutes to configure the service environment.

<a id="pipeline.list"></a>

### Pipeline List

The pipeline list is displayed. Select a pipeline from the list to view detailed information and modify information.

- **Status**: The status of the pipeline is displayed. See the table below for major statuses.

    | Status             | Description                                    |
    |--------------------|-----------------------------------------------|
    | CREATE REQUESTED   | Pipeline creation has been requested.          |
    | CREATE IN PROGRESS | Pipeline creation is in progress.              |
    | CREATE FAILED      | Pipeline creation failed. Please try again.    |
    | ACTIVE             | Pipeline has been created successfully.        |

<a id="pipeline.graph"></a>

### Pipeline Graph

The pipeline graph is displayed. Select a node in the graph to view detailed information.

The graph is a pictorial representation of the pipeline. Each node in the graph represents a step in the pipeline, and arrows indicate the parent/child relationships between pipeline components shown as each step.

<a id="pipeline.delete"></a>

### Delete Pipeline

Delete a pipeline.

1. Select the pipeline to delete.
2. Click **Delete Pipeline**. Pipelines being created cannot be deleted.
3. The requested delete operation cannot be canceled. Click **Delete** to proceed.

!!! tip "Note"
    If there is a schedule created with the pipeline you want to delete, the pipeline cannot be deleted. Delete the pipeline schedule first, then delete the pipeline.

<a id="pipeline.run"></a>

## Pipeline Execution

You can execute and manage uploaded pipelines in AI EasyMaker.

<a id="pipeline.run.create"></a>

### Create Pipeline Execution

Execute a pipeline.

- **Basic Information**
    - **Name**: Enter the pipeline execution name.
    - **Description**: Enter a description.
    - **Pipeline**: Select the pipeline to execute.
    - **Experiment**: Select the experiment that will contain the pipeline execution. Experiments group related pipeline executions. If there are no created experiments, click **Add** to create an experiment.
- **Execution Information**
    - **Execution Parameters**: Enter values if there are input parameters defined in the pipeline.
    - **Execution Type**: Select the pipeline execution type. If you select **One-time**, the pipeline will be executed only once. To run the pipeline periodically, select **Schedule** and configure the schedule by referring to [Create Pipeline Schedule](#pipeline.recurring.run.create).
- **Instance Information**
    - **Instance Type**: Select the instance type to execute the pipeline.
    - **Number of Instances**: Enter the number of instances to use for pipeline execution.
- **Additional Settings**
    - **Boot Storage Size**: Enter the boot storage size of the instance to execute the pipeline.
    - **NHN Cloud NAS**: You can connect **NHN Cloud NAS** to the instance that will execute the pipeline.
        - **Mount Directory Name**: Enter the directory name to mount on the instance.
        - **NAS Path**: Enter the path in `nas://{NAS ID}:/{path}` format.
    - **Log Management**: You can save logs generated during pipeline execution to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    Creating pipeline execution may take several minutes.
    When creating resources for the first time, it may take a few additional minutes to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="pipeline.run.list"></a>

### Pipeline Execution List

The pipeline execution list is displayed. Select a pipeline execution from the list to check detailed information and modify information.

- **Status**: The status of the pipeline execution is displayed. Refer to the table below for main statuses.

    | Status                        | Description                                                                                    |
    |-------------------------------|------------------------------------------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline execution creation has been requested.                                                |
    | CREATE IN PROGRESS            | Pipeline execution creation is in progress.                                                    |
    | CREATE FAILED                 | Pipeline execution creation has failed. Please try again.                                     |
    | RUNNING                       | Pipeline execution is in progress.                                                            |
    | COMPLETE IN PROGRESS          | Resources used for pipeline execution are being cleaned up.                                   |
    | COMPLETE                      | Pipeline execution has been completed successfully.                                            |
    | STOP IN PROGRESS              | Pipeline execution is being stopped.                                                          |
    | STOPPED                       | Pipeline execution has been stopped by user request.                                          |
    | FAIL PIPELINE RUN IN PROGRESS | Resources used for pipeline execution are being cleaned up.                                   |
    | FAIL PIPELINE RUN             | Pipeline execution has failed. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |

- **Tasks**
    - **Stop**: You can stop pipeline execution in progress.
- **Monitoring**: When you select a pipeline execution from the list, you can check the monitoring target instance list and basic metric charts in the **Monitoring** tab of the detailed screen that appears.
    - The **Monitoring** tab is disabled when pipeline execution is in the creating state.

<a id="pipeline.run.graph"></a>

### Pipeline Execution Graph

The pipeline execution graph is displayed. Select a node in the graph to check detailed information.

The graph is a visual representation of pipeline execution. This graph shows the steps that have already been executed and the currently executing steps during pipeline execution, and indicates the parent/child relationships between pipeline components represented as each step with arrows. Each node in the graph represents a step in the pipeline.

Through detailed information for each node, you can download generated artifacts.

!!! danger "Caution"
    Pipeline artifacts are retained for 120 days. Artifacts older than 120 days are automatically deleted.

<a id="pipeline.run.stop"></a>

### Stop Pipeline Execution

Stop pipeline execution in progress.

1. Select the pipeline execution you want to stop from the list.
2. Click **Stop Execution**.
3. The requested operation cannot be cancelled. To continue, click **Confirm**.

!!! tip "Note"
    Stopping pipeline execution may take several minutes.

<a id="pipeline.run.copy"></a>

### Copy Pipeline Execution

Create a new pipeline execution with the same settings as an existing pipeline execution.

1. Select the pipeline execution you want to copy.
2. Click **Copy Pipeline Execution**.
3. The pipeline execution creation screen is displayed with the same settings as the existing pipeline execution.
4. If there is information you want to change, modify the settings and click **Create Pipeline Execution**.

<a id="pipeline.run.delete"></a>

### Delete Pipeline Execution

Delete pipeline execution.

1. Select the pipeline execution to delete.
2. Click **Delete Pipeline Execution**. Pipeline execution in progress cannot be deleted.
3. The requested deletion operation cannot be cancelled. To continue, click **Delete**.

<a id="pipeline.schedule"></a>

## Pipeline Schedule

You can create and manage schedules to periodically and repeatedly execute uploaded pipelines in AI EasyMaker.

<a id="pipeline.recurring.run.create"></a>

### Create Pipeline Schedule

Create a schedule to periodically and repeatedly execute a pipeline.

For information other than the items below that can be configured when creating a pipeline schedule, see [Create Pipeline Execution](#pipeline.run.create).

- **Execution Information**
    - **Execution Type**: Select the pipeline execution type. When **Schedule Settings** is selected, the pipeline is executed periodically and repeatedly. To execute the pipeline only once, select **One-time**.
    - **Trigger Type**: Select the pipeline execution trigger type. You can choose **Time Cycle** or **Cron Expression**.
        - To repeatedly execute a pipeline through time cycle settings, select **Time Cycle** and then enter a number and time unit.
        - To repeatedly execute a pipeline through Cron expression settings, select **Cron Expression** and then enter a Cron expression.
    - **Concurrent Execution Settings**: New pipeline executions may be created before previously created pipeline executions terminate, depending on the trigger cycle (**Time Cycle** or **Cron Expression**). You can limit the number of executions running in parallel by specifying the maximum number of concurrent executions.
    - **Start Time**: You can set the start time for the pipeline schedule. If not entered, pipeline executions are created according to the configured cycle.
    - **End Time**: You can set the end time for the pipeline schedule. If not entered, pipeline executions are created until stopped.
    - **Missed Execution Catchup**: Determines whether to catch up when pipeline executions fall behind schedule.
        - For example, assuming a pipeline schedule is temporarily stopped and then restarted later, setting it to **Enable** will catch up on missed pipeline executions.
        - If the pipeline internally handles backfill, it should be set to **Disable** to prevent duplicate backfill tasks.

!!! tip "Note"
    Creating a pipeline schedule may take a few minutes.
    When creating resources for the first time, it takes a few additional minutes to configure the service environment.

!!! tip "Note"
    Cron expressions use six space-separated fields to represent time.
    For more details, see the [Cron Expression Format](https://pkg.go.dev/github.com/robfig/cron#hdr-CRON_Expression_Format) documentation.

<a id="pipeline.recurring.run.list"></a>

### Pipeline Schedule List

The pipeline schedule list is displayed. Selecting a pipeline schedule from the list allows you to check detailed information and modify information.

- **Status**: The status of the pipeline schedule is displayed. See the table below for major statuses.

    | Status                        | Description                                                    |
    |-------------------------------|---------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline schedule creation has been requested.                |
    | CREATE FAILED                 | Pipeline schedule creation has failed. Please try again.     |
    | ENABLED                       | Pipeline schedule has started normally.                      |
    | ENABLED(EXPIRED)              | Pipeline schedule has started normally but has passed the configured end time. |
    | DISABLED                      | Pipeline schedule has been stopped by user request.          |

- **Execution Management**: In the **Execution Management** tab of the detail screen displayed when selecting a pipeline schedule from the list, you can check the list of executions created by the pipeline schedule.

<a id="pipeline.recurring.run.start.stop"></a>

### Start and Stop Pipeline Schedule

Start a stopped pipeline schedule or stop a started pipeline schedule.

1. Select the pipeline schedule you want to start or stop from the list.
2. Click **Start Schedule** or **Stop Schedule**.

<a id="pipeline.recurring.run.copy"></a>

### Copy Pipeline Schedule

Create a new pipeline schedule with the same settings as an existing pipeline schedule.

1. Select the pipeline schedule you want to copy.
2. Click **Copy Pipeline Schedule**.
3. The pipeline schedule creation screen is displayed with the same settings as the existing pipeline schedule.
4. If there is information you want to change in the settings, modify it and then click **Create Pipeline Schedule**.

<a id="pipeline.recurring.run.delete"></a>

### Delete Pipeline Schedule

Delete a pipeline schedule.

1. Select the pipeline schedule to delete.
2. Click **Delete Pipeline Schedule**.
3. The requested delete operation cannot be canceled. To continue, click **Delete**.

!!! tip "Note"
    If executions created by the pipeline schedule you want to delete are in progress, it cannot be deleted. Delete the pipeline schedule after the pipeline executions are completed.

<a id="rag"></a>



### 1. Add AI EasyMaker System Account Permissions to NHN Cloud Object Storage

When some AI EasyMaker features use the user's NHN Cloud Object Storage as input/output storage,
you must allow read or write permissions for the AI EasyMaker system account in the user's NHN Cloud Object Storage container for normal feature operation.

Allowing read/write permissions for the AI EasyMaker system account in the user's NHN Cloud Object Storage container means that the AI EasyMaker system account can read or write files in the user's NHN Cloud Object Storage container according to the granted permissions for all files.

You must confirm this content and set access policies for your Object Storage with only the necessary accounts and permissions.

The user is responsible for all consequences arising from allowing access to the user's Object Storage for accounts other than the AI EasyMaker system account during the access policy configuration process, and AI EasyMaker does not take responsibility for such consequences.

!!! tip "Good to know"
    Depending on the function, the files that AI EasyMaker accesses to read or write in Object Storage are as follows.

| Function       | Permission | Access Target                                            |
| ---------- | ---- | ---------------------------------------------------- |
| Training, Hyperparameter tuning       | Read | Algorithm path and training input data path entered by user |
| Training, Hyperparameter tuning       | Write | Training output data and checkpoint path entered by user   |
| Model       | Read | Model artifact path entered by user                   |
| Model evaluation | Read | Input data path entered by user                   |
| Model evaluation | Write | Output data path entered by user                   |
| Batch inference | Read | Input data path entered by user                   |
| Batch inference | Write | Output data path entered by user                   |
| RAG | Read | Collection data path entered by user                   |

To add read/write permissions for the AI EasyMaker system account to NHN Cloud Object Storage, refer to the following:

1. Click **[Training]** or **[Model]** tab > **AI EasyMaker System Account Information**.
2. Save the AI EasyMaker system account information: **AI EasyMaker Tenant ID** and **AI EasyMaker API User ID**.
3. Go to the NHN Cloud Object Storage console.
4. Refer to the [Allow read/write access to specific projects or specific users](https://docs.nhncloud.com/en/Storage/Object%20Storage/ko/acl-guide/#role-based-access-allow-rw-project-or-user) document to add the necessary read and write permissions for the AI EasyMaker system account in the NHN Cloud Object Storage console.

<a id="appendix.2.lncs.service.usage.guide.and.log.inquiry.guide"></a>

### 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Methods

<a id="appendix.2.lncs.service.usage.guide"></a>

#### NHN Cloud Log & Crash Search Service Usage Guide

Logs and events generated from AI EasyMaker service can be stored in the NHN Cloud Log & Crash Search service.
To store logs in the Log & Crash Search service, you need to enable the Log & Crash service, and separate usage fees will be charged.

- **Log & Crash Search Service Usage and Pricing Information**
    - For detailed information and pricing of the Log & Crash Search service, please refer to:
        - [Log & Crash Search Service Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/Overview/)
        - [Log & Crash Search Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Data%20%26%20Analytics&s=Log%20%26%20Crash%20Search)

<a id="appendix.2.lncs.service.log.inquiry.guide"></a>

#### Log Search

1. Navigate to the Log & Crash Search service console page.
2. Query logs by entering search conditions in the Log & Crash Search service.
    - AI EasyMaker training log query: Query logs where the category field is "easymaker.training".
        - Query: category:"easymaker.training"
    - AI EasyMaker endpoint log query: Query logs where the category field is "easymaker.inference".
        - Query: category:"easymaker.inference"
    - AI EasyMaker full log query: Query logs where the logType field is "NNHCloud-AIEasyMaker".
        - Query: logType:"NHNCloud\-AIEasyMaker"
3. For detailed usage of the Log & Crash Search service, see the [Log & Crash Search Service Console Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/console-guide/).

AI EasyMaker service sends logs to the Log & Crash Search service with fields defined as follows.

- **Common Log Fields**

    | Name            | Description                   | Valid Range                             |
    | --------------- | ----------------------------- | --------------------------------------- |
    | easymakerAppKey | AI EasyMaker Appkey           | -                                       |
    | category        | Log category                  | easymaker.training, easymaker.inference |
    | logLevel        | Log level                     | INFO, WARNING, ERROR                    |
    | body            | Log content                   | -                                       |
    | logType         | Log providing service name    | NHNCloud-AIEasyMaker                    |
    | time            | Log occurrence time (UTC)     | -                                       |

- **Training Log Fields**

    | Name       | Description          |
    | ---------- | -------------------- |
    | trainingId | AI EasyMaker training ID |

- **Hyperparameter Tuning Log Fields**

    | Name                   | Description                         |
    | ---------------------- | ----------------------------------- |
    | hyperparameterTuningId | AI EasyMaker hyperparameter tuning ID |

- **Endpoint Log Fields**

    | Name            | Description                     |
    | --------------- | ------------------------------- |
    | endpointId      | AI EasyMaker endpoint ID        |
    | endpointStageId | Endpoint stage ID               |
    | inferenceId     | Inference request unique ID     |
    | action          | Action classification (Endpoint.Model) |
    | modelName       | Target model name for inference |

- **Batch Inference Log Fields**

    | Name             | Description                   |
    | ---------------- | ----------------------------- |
    | batchInferenceId | AI EasyMaker batch inference ID |

<a id="appendix.3.hyperparameter"></a>

### 3. Hyperparameters

- Values in Key-Value format entered through the console.
- When executing the entry point, they are passed as execution arguments (--{Key}).
- They can also be stored and used as environment variable values (EM_HP_{Key converted to uppercase}).

You can use the hyperparameter values entered when creating training, as shown in the example below.<br>
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

- Information required for training is passed to the training container through **environment variables**, and the passed environment variables can be utilized in the **training script**.
- Environment variable names created from user input are converted to uppercase.
- In the code, the trained model must be saved to the EM_MODEL_DIR path.
- **Key Environment Variables**

    | Environment Variable Name                      | Description                                                                        |
    |-----------------------------| --------------------------------------------------------------------------- |
    | EM_SOURCE_DIR               | Absolute path of the folder where the algorithm script entered during training creation is downloaded  |
    | EM_ENTRY_POINT              | Algorithm entry point name entered during training creation                             |
    | EM_DATASET_${data set name}     | Absolute path of the folder where each data set entered during training creation is downloaded |
    | EM_DATASETS                 | Complete data set list (JSON format)                                            |
    | EM_MODEL_DIR                | Model storage path                                                              |
    | EM_CHECKPOINT_INPUT_DIR     | Input checkpoint storage path                                                  |
    | EM_CHECKPOINT_DIR           | Output checkpoint storage path                                                  |
    | EM_HP_${uppercase converted hyperparameter key} | Hyperparameter value corresponding to the hyperparameter key                              |
    | EM_HPS                      | Complete hyperparameter list (JSON format)                                         |
    | EM_TENSORBOARD_LOG_DIR      | TensorBoard log path for checking training results                                    |
    | EM_REGION                   | Current region information                                                              |
    | EM_APPKEY                   | Appkey of the currently used AI EasyMaker service                                   |

- **Environment Variable Usage Example Code**

```python
import os
import tensorflow

dataset_dir = os.environ.get("EM_DATASET_TRAIN")
train_data = read_data(dataset_dir, "train.csv")

model = ... # 입력한 데이터를 이용해 모델 구현
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

### 5. Storing Metric Logs for TensorBoard Usage

- To check result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage location to the designated location (`EM_TENSORBOARD_LOG_DIR`) when writing your training script.

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

<img src="images/console-guide_appendix_tensorboard.png" alt="Check TensorBoard Logs">

</details>

!!! danger "Caution"
    TensorBoard metric logs are retained for 120 days. Metric logs older than 120 days are automatically deleted.

<a id="appendix.6.framework.training.settings"></a>

### 6. Distributed Training Settings by Framework

- **Tensorflow**
    - The environment variable `TF_CONFIG` required for distributed training is automatically configured. For more details, see the [Tensorflow official guide documentation](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy).
- **Pytorch**
    - `Backends` configuration is required for distributed training. Set it to gloo when performing distributed training with CPU, and nccl when using GPU. For more details, see the [Pytorch official guide documentation](https://pytorch.org/docs/stable/distributed.html).

<a id="appendix.7.cluster.upgrade"></a>

### 7. Cluster Version Upgrade

AI EasyMaker service periodically upgrades cluster versions to provide stable service and new features.
When a new cluster version is deployed, notebooks and endpoints running on the old version cluster must be migrated to the new cluster.
This guide explains how to migrate resources to the new cluster by resource type.

<a id="appendix.7.cluster.upgrade.notebook"></a>

#### Notebook Cluster Version Upgrade

In the **Notebook** list screen, notebooks that need to be migrated to the new cluster display a **Restart** button to the left of their name.
When you hover the mouse pointer over the **Restart** button, restart guidance text and expiration date are displayed.

- Before expiration, be sure to check the following precautions and then click the **Restart** button.
    - When restarting, data stored in data storage (/root/easymaker directory path) will be preserved as-is.
    - When restart is executed, data stored in boot storage may be initialized and lost. Move data to data storage before restarting.

Restart takes about 25 minutes for the first execution, and about 10 minutes thereafter.
If restart fails, it is automatically reported to the administrator.

<a id="appendix.7.cluster.upgrade.endpoint"></a>

#### Endpoint Cluster Version Upgrade

In the **Endpoint List** screen, endpoints that need to be migrated to the new cluster display **! Notice** text to the left of their name.
When you hover the mouse pointer over the **! Notice** text, version upgrade guidance text and expiration date are displayed.
Before expiration, you must migrate stages running on the old version cluster to the new version cluster according to the following guidance.

<a id="appendix.7.cluster.upgrade.endpoint.stage"></a>

##### General Stage Cluster Version Upgrade

1. Delete general stages that are not default stages. Before deletion, first check whether the stage is in service.
2. Create the stage again.
3. When the new stage becomes ACTIVE, verify that API calls and inference responses are coming normally through the stage endpoint.

!!! danger "Caution"
    When a stage is deleted, the endpoint terminates and API calls become impossible. Before deletion, verify that it is a stage not in service.

<a id="appendix.7.cluster.upgrade.endpoint.default.stage"></a>

##### Default Stage Cluster Version Upgrade

The default stage is the stage where actual service is operated.
To migrate the cluster version of the default stage without service interruption, follow the guide below.

1. Create a new stage to replace the default stage of the old version cluster.
2. Verify that API calls and inference responses are coming normally from the new stage endpoint.
3. Click the **Change Default Stage** button. Select the new stage to change it to the default stage.
4. When the change is complete, the new stage is set as the default stage, and the existing default stage is deleted.

<a id="appendix.8.torchrun.usage"></a>

### 8. How to Use torchrun

- The code has been written to enable distributed training in PyTorch, and when you input the number of distributed nodes and the number of processes per node, distributed training using distributed nodes and multi-processes via torchrun is performed.
- Training and hyperparameter tuning may fail due to memory shortage caused by factors such as total number of processes, model size, input data size, and batch size. When failing due to memory shortage, the following error message may appear. However, not all cases where this message appears are failures due to memory shortage. Set an appropriate instance type according to memory usage.

```plaintext
exit code : -9 (pid: {pid})
```

- For more detailed information about torchrun, see the [PyTorch official guide documentation](https://pytorch.org/docs/stable/elastic/run.html).

<a id="appendix.9.resource.info"></a>

### 9. Resource Information

When creating batch inference and endpoints in AI EasyMaker, resources are allocated excluding basic usage from the selected instance type.
Since the required resources vary depending on the model's request volume and complexity, carefully set the number of pods and resource allocation along with an appropriate instance type.

Batch inference allocates resources to each pod by dividing actual usage by the number of pods. For endpoints, the input allocation cannot exceed the instance's actual usage, so check resource usage in advance.
Note that both batch inference and endpoints may fail to be created if the allocated resources are less than the minimum usage required for inference.

<a id="appendix.10.endpoint.api.specification"></a>

### 10. Endpoint API Specification

AI EasyMaker service provides endpoints based on the OIP (open inference protocol) specification.
For detailed information about the OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

| Name                           | Method | API Path                                                                |
| ------------------------------ | ------ | ----------------------------------------------------------------------- |
| Model List                     | GET    | /{model_name}/v1/models                                                 |
| Model Ready                    | GET    | /{model_name}/v1/models/{model_name}                                    |
| Inference                      | POST   | /{model_name}/v1/models/{model_name}/predict                            |
| Explanation                    | POST   | /{model_name}/v1/models/{model_name}/explain                            |
| Server Information             | GET    | /{model_name}/v2                                                        |
| Server Live                    | GET    | /{model_name}/v2/health/live                                            |
| Server Ready                   | GET    | /{model_name}/v2/health/ready                                           |
| Model Information              | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]       |
| Model Ready                    | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/ready |
| Inference                      | POST   | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/infer |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/completions                                     |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/chat/completions                                |

!!! tip "Note"
    OpenAI generative model inference is used when using generative models such as OpenAI's GPT-4o.
    Input values required for inference must be entered according to OpenAI's API specification. For more details, see [OpenAI API Documentation](https://platform.openai.com/docs/api-reference/chat).
    For models that support Completion and Chat Completion APIs provided by AI EasyMaker, check [Model endpoint compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility).

<a id="appendix.11.framework.note"></a>

### 11. Framework-Specific Serving Notes

<a id="appendix.11.framework.note.tensorflow.framework"></a>

#### TensorFlow Framework

The TensorFlow model serving provided by AI EasyMaker uses SavedModel (.pb), which is recommended by TensorFlow.
To use checkpoints, save the checkpoint variables directory saved as SavedModel together with the model directory, and it will be used for model serving.
Reference: [https://www.tensorflow.org/guide/saved_model](https://www.tensorflow.org/guide/saved_model)

<a id="appendix.11.framework.note.pytorch.framework"></a>

#### PyTorch Framework

AI EasyMaker serves PyTorch models (.mar) with TorchServe.
It is recommended to use MAR files created with model-archiver, and serving with weight files is also possible, but weight files require additional files.
Check the table below and the [model-archiver documentation](https://github.com/pytorch/serve/blob/master/model-archiver/README.md) for required files and detailed instructions.

| File Name                    | Required | Description                                                              |
| ---------------------------- | -------- | ------------------------------------------------------------------------ |
| model.py                     | Required | Model structure file passed as model-file parameter.                    |
| handler.py                   | Required | File passed as handler parameter to handle inference logic.             |
| weight file (.pt, .pth, .bin) | Required | File that stores the model's weights and structure.                     |
| requirements.txt             | Optional | File for installing Python packages required for serving.               |
| extra/                       | Optional | Files in the directory are passed as extra-files parameter.             |

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
The `model-settings.json` required when using mlserver directly is not required when using AI EasyMaker serving.

<a id="appendix.11.framework.note.hugging.face.framework"></a>

#### Hugging Face Framework

Hugging Face models can be served using the runtime provided by AI EasyMaker or TensorFlow Serving, TorchServe.

<a id="appendix.11.framework.note.hugging.face.framework.runtime"></a>

##### Hugging Face Runtime

This is an easy way to serve Hugging Face models.
Hugging Face runtime serving does not support fine-tuning. To serve fine-tuned models, use the TensorFlow/PyTorch Serving method.

1. Check the model to be served on Hugging Face.
2. Copy the Hugging Face model ID.
3. On the AI EasyMaker model creation page, select Hugging Face framework and enter the Hugging Face model ID.
4. Enter the required input values according to the model to create the model.
5. Check the created model and create an endpoint.

!!! tip "Note"
    Currently, Hugging Face runtime does not support all Tasks of Hugging Face.
    Supported Tasks are `sequence_classification`, `token_classification`, `fill_mask`, `text_generation`, `text2text_generation`.
    To use unsupported Tasks, use the TensorFlow/PyTorch Serving method.

!!! tip "Note"
    To serve a Gated Model, you must enter a token from an account with access permission as a model parameter.
    If you don't enter a token or enter a token from an unauthorized account, model deployment will fail.

<a id="appendix.11.framework.note.hugging.face.framework.tensorflow.pytorch.serving"></a>

##### TensorFlow/PyTorch Serving

This is a method for serving Hugging Face models trained with TensorFlow and PyTorch.

1. Download the Hugging Face model.
    - You can download using AutoTokenizer, AutoConfig, and AutoModel from the transformers library as shown in the example code below.

            from transformers import AutoTokenizer, AutoConfig, AutoModel

            model_id = "<model_id>"
            revision = "main"

            model_dir = f"./models/{model_id}/{revision}"

            tokenizer = AutoTokenizer.from_pretrained(model_id, revision=revision)
            model_config = AutoConfig.from_pretrained(model_id, revision=revision)
            model = AutoModel.from_config(model_config)

            tokenizer.save_pretrained(model_dir)
            model.save_pretrained(model_dir)

    - If model download fails, try importing the appropriate class for the model instead of AutoModel and attempt the download.
    - If fine-tuning is needed, you can write your own code for training according to the [Hugging Face fine-tuning guide](https://huggingface.co/docs/transformers/main/ko/training).
        - For more details on AI EasyMaker training, see [Training](#training).

2. Check the Hugging Face model information and create files required for serving.
    - Save the model in the format required for serving by each framework.
    - For details, check the notes for TensorFlow and PyTorch frameworks.
3. Upload model files to OBS or NAS.
4. For the subsequent process, see the [Create Model](#model.create) and [Create Endpoint](#endpoint.create) guides.