<a id="ai.easymaker.console.guide"></a>

## Machine Learning > AI EasyMaker > Console Guide

<a id="dashboard"></a>

## Dashboard

You can check the usage status of all AI EasyMaker resources on the dashboard.

<a id="dashboard.service.usage.status"></a>

### Service Usage Status

Displays the number of resources in use by resource type.

- Notebook: Number of notebooks in ACTIVE(HEALTHY) status currently in use
- Training: Number of training jobs that have been completed (COMPLETE)
- Hyperparameter Tuning: Number of hyperparameter tuning jobs that have been completed (COMPLETE)
- Endpoint: Number of endpoints in ACTIVE status

<a id="dashboard.service.monitoring"></a>

### Service Monitoring

- Displays the top 3 endpoints with the highest API calls.
- When you select an endpoint, you can check the API success/failure total metrics for the sub-endpoint stages.

<a id="dashboard.resource.usage"></a>

### Resource Usage

- You can check the resources with the highest usage by CPU and GPU core types.
- Resource information is displayed when you hover the mouse pointer over the metrics.

<a id="notebook"></a>

## Notebook

Create and manage Jupyter notebooks with essential packages installed for machine learning development.

<a id="notebook.create"></a>

### Create Notebook

Create a Jupyter notebook.

- **Image**: Select the OS image to be installed on the notebook instance.
    - **Core Type**: The CPU and GPU core types of the image are displayed.
    - **Framework**: The framework installed on the image is displayed.
        - TENSORFLOW: Image with TensorFlow deep learning framework installed.
        - PYTORCH: Image with PyTorch deep learning framework installed.
        - PYTHON: Image with only Python language installed without deep learning frameworks.
    - **Framework Version**: The version of the framework installed on the image is displayed.
    - **Python Version**: The Python version installed on the image is displayed.

- **Notebook Information**
    - Enter the notebook name and description.
    - Select the instance type for the notebook. The instance specifications are selected according to the chosen type.

- **Storage**
    - Specify the boot storage and data storage size for the notebook.
        - Boot storage is where the Jupyter notebook and default virtual environment are installed. This storage is initialized when the notebook is restarted.
        - Data storage is block storage mounted to the `/root/easymaker` directory path. Data in this storage is preserved even when the notebook is restarted.
    - The storage size of a created notebook cannot be changed, so you must specify sufficient storage size during creation.
    - If needed, you can connect **NHN Cloud NAS** to the notebook.
        - Mount Directory Name: Enter the name of the directory to mount on the notebook.
        - NHN Cloud NAS Path: Enter the directory path in the format `nas://{NAS ID}:/{path}`.

!!! tip "Note"
    Creating a notebook may take several minutes.
    When creating resources for the first time, it may take additional minutes to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="notebook.list"></a>

### Notebook List

The notebook list is displayed. Selecting a notebook from the list allows you to view detailed information and modify information.

- **Name**: The notebook name is displayed. You can change the name by clicking **Change** on the detail screen.
- **Status**: The notebook status is displayed. Refer to the table below for key statuses.

    | Status             | Description                                                                                                                        |
    | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Notebook creation has been requested.                                                                                              |
    | CREATE IN PROGRESS | The notebook instance is being created.                                                                                           |
    | ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                     |
    | ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists after restarting the notebook, contact customer support. |
    | STOP IN PROGRESS   | The notebook is being stopped.                                                                                                    |
    | STOPPED            | The notebook has been stopped.                                                                                                    |
    | START IN PROGRESS  | The notebook is being started.                                                                                                    |
    | REBOOT IN PROGRESS | The notebook is being rebooted.                                                                                                   |
    | DELETE IN PROGRESS | The notebook is being deleted.                                                                                                    |
    | CREATE FAILED      | Notebook creation has failed. If creation continues to fail, contact customer support.                                           |
    | STOP FAILED        | Failed to stop the notebook. Please try again.                                                                                   |
    | START FAILED       | Failed to start the notebook. Please try again.                                                                                  |
    | REBOOT FAILED      | Failed to reboot the notebook. Please try again.                                                                                 |
    | DELETE FAILED      | Failed to delete the notebook. Please try again.                                                                                 |

- **Actions > Open Jupyter Notebook**: Clicking the **Open Jupyter Notebook** button opens the notebook in a new browser window. The notebook is only accessible to users logged into the console.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when selecting a notebook, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when the notebook is being created or when there are operations in progress.

<a id="notebook.user.virtual.run.environment.configuration"></a>

### User Virtual Runtime Environment Configuration

AI EasyMaker notebook instances provide a default Conda virtual environment with various libraries and kernels needed for machine learning installed.
The default Conda virtual environment is initialized and runs when the notebook is stopped and started, but virtual environments and external libraries installed by users in arbitrary paths are not automatically initialized and therefore are not preserved when the notebook is stopped and started.
To resolve this issue, you must create virtual environments in the `/root/easymaker/custom-conda-envs` directory path and install external libraries in the created virtual environments.
AI EasyMaker notebook instances support initialization and operation of virtual environments created in the `/root/easymaker/custom-conda-envs` directory path when the notebook is stopped and started.

Follow the guide below to configure user virtual environments.

1. Click **Open Jupyter Notebook** > **Jupyter Notebook > Launcher > Terminal** in the console notebook menu.
2. Navigate to the `/root/easymaker/custom-conda-envs` path.

        cd /root/easymaker/custom-conda-envs

3. To create a virtual environment named `easymaker_env` with Python 3.8, execute the `conda create` command as follows.

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

### User Scripts

You can register scripts that should be automatically executed when stopping and starting notebooks in the `/root/easymaker/cont-init.d` path.
They are executed in ascending order according to alphanumeric order.

- Script location and permissions
    - Only files located in the `/root/easymaker/cont-init.d` path are executed.
    - Only scripts with execute permissions are executed.
- Script content
    - The first line of the script must start with `#!`.
    - Scripts are executed with root privileges.
- Script execution records are saved at the following locations.
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
    To preserve virtual environments and external libraries when stopping and starting notebooks, configure user virtual environments by referring to [User Virtual Runtime Environment Configuration](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.instance.type.change"></a>

### Change Notebook Instance Type

Change the instance type of a created notebook.
The instance type to be changed can only be changed to an instance type with the same core type as the existing instance.

1. Select the notebook whose instance type you want to change.
2. If the notebook is in a running state (ACTIVE), click **Stop Notebook** to stop the notebook.
3. Click **Change Instance Type**.
4. Select the instance type you want to change to and click confirm.

!!! tip "Note"
    Changing instance type may take several minutes.

<a id="notebook.reboot"></a>

### Reboot Notebook

If problems occur while using the notebook, or if the status is normal (ACTIVE) but the notebook is not accessible,
you can reboot the notebook.

1. Select the notebook you want to reboot.
2. Click **Reboot Notebook**.
3. The requested delete operation cannot be canceled. Click **Confirm** to continue.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be initialized when rebooting notebooks.
    To preserve virtual environments and external libraries when rebooting notebooks, configure user virtual environments by referring to [User Virtual Runtime Environment Configuration](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.delete"></a>

### Delete Notebook

Delete a created notebook.

1. Select the notebook you want to delete from the list.
2. Click **Delete Notebook**.
3. The requested delete operation cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    When deleting a notebook, both boot storage and data storage are deleted.
    Connected NHN Cloud NAS is not deleted and must be individually deleted in **NHN Cloud NAS**.

<a id="experiment"></a>

## Experiments

Experiments manage related training by grouping them into experiments.

<a id="experiment.create"></a>

### Create Experiments

1. Click **Create Experiment**.
2. Enter the experiment name and description, then click **Confirm**.

!!! tip "Note"
    Creating an experiment may take a few minutes.
    When creating resources for the first time, it may take a few additional minutes to configure the service environment.

<a id="experiment.list"></a>

### Experiment List

The experiment list is displayed. Selecting an experiment from the list allows you to view detailed information and modify the information.

- **Status**: The status of the experiment is displayed. See the table below for key statuses.

    | Status             | Description                                               |
    | ------------------ | --------------------------------------------------------- |
    | CREATE REQUESTED   | The experiment creation has been requested.              |
    | CREATE IN PROGRESS | The experiment is being created.                         |
    | CREATE FAILED      | The experiment creation has failed. Please try again.    |
    | ACTIVE             | The experiment has been successfully created.            |

- **Actions**
    - Clicking **Go to TensorBoard** opens TensorBoard in a new browser window where you can view statistics for training included in the experiment. TensorBoard can only be accessed by users logged into the console.
    - **Retry**: If the experiment status is failed, you can click **Retry** to recover the experiment.
- **Training**: The **Training** tab in the detail screen that appears when selecting training displays a list of training included in the experiment.

<a id="experiment.delete"></a>

### Delete Experiments

Delete an experiment.

1. Select the experiment to delete.
2. Click **Delete Experiment**. You cannot delete an experiment if it is in the process of being created.
3. The requested deletion operation cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    You cannot delete an experiment if there are pipeline schedules associated with the experiment, or if there are training, hyperparameter tuning, or pipeline executions being created.
    Delete the resources associated with the experiment first, then delete the experiment.
    Associated resources can be viewed in the detailed screen at the bottom that appears when you click the experiment you want to delete.

<a id="training"></a>

## Training

Provides an environment where you can train machine learning algorithms and check training results through statistics.

<a id="training.create"></a>

### Create Training

Set up the environment where training will be performed by selecting the instance and OS image for training, and proceed with training by entering algorithm information and input/output data paths.

- **Training Template**: To set up training information by loading a training template, select 'Use' and then select the training template to load.
- **Basic Information**: Select basic information about the training and the experiment that will include the training.
    - **Training Name**: Enter the training name.
    - **Training Description**: Enter a description.
    - **Experiment**: Select the experiment that will include the training. Experiments group related trainings. If no experiment has been created, click **Add** to create an experiment.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information on provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select an algorithm.
            - **Hyperparameters**: Enter hyperparameter values required for training. For detailed information on hyperparameters for each algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use algorithms written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the NHN Cloud Object Storage path where the algorithm is stored.<br>
                    - Enter the directory path in the format obs://{Object Storage API endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, set permissions by referring to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission). Model creation will fail if the required permissions are not set.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is stored. <br>
                    Enter the directory path in the format nas://{NAS ID}:/{path}.

            - **Entry Point**
                - The entry point is the entry point for algorithm execution where training begins. Write the entry point filename.
                - The entry point file must exist in the algorithm path.
                - If you write **requirements.txt** in the same path, the Python packages required by the script will be installed.
            - **Hyperparameters**
                - To add parameters for training, click the **+ button** to enter parameters in Key-Value format. You can enter up to 100 parameters.
                - The entered hyperparameters are entered as execution arguments when the entry point is executed. For detailed usage methods, see [Appendix > 3. Hyperparameters](#appendix.3.hyperparameter).

- **Image**: Select the instance image according to the environment where training should be executed.

- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to execute training.
    - **Number of Distributed Nodes**: Enter the number of nodes to perform distributed training. Distributed training can be enabled through settings in the algorithm code. For details, see [Appendix > 6. Distributed Training Settings by Framework](#appendix.6.framework.training.settings).
    - **Use torchrun**: Select whether to use torchrun supported by the Pytorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. Using torchrun enables distributed training by running multiple processes on one node. The number of processes affects memory usage.
- **Input Data**
    - **Data Set**: Enter the data set to execute training. You can configure up to 10 data sets.
        - Data Set Name: Enter the data set name.
        - Data Path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to proceed with training from a saved checkpoint, enter the storage path of the checkpoint.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save the execution results of training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides checkpoints, enter the storage path of the checkpoint.
        - Generated checkpoints can be used when resuming training from previous training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance to execute training.
        - This is only used when using NHN Cloud Object Storage. It should be specified with sufficient size to store all data required for training.
    - **Maximum Training Time**: Specify the maximum wait time until training is completed. Training that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during training can be stored in the NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - If input data is deleted before training is completed, training may fail.

<a id="training.list"></a>

### Training List

The training list is displayed. Selecting a training from the list allows you to check detailed information and change information.

- **Training Time**: The time training has been in progress is displayed.
- **Status**: The status of training is displayed. For major statuses, see the table below.

    | Status                                       | Description                                                                                                                                         |
    | -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                             | The state where training creation has been requested.                                                                                               |
    | CREATE IN PROGRESS                           | The state where resources required for training are being created.                                                                                  |
    | RUNNING                                      | The state where training is in progress.                                                                                                           |
    | STOPPED                                      | The state where training has been stopped by user request.                                                                                         |
    | COMPLETE                                     | The state where training has completed normally.                                                                                                    |
    | STOP IN PROGRESS                             | The state where training is being stopped.                                                                                                         |
    | FAIL TRAIN                                   | The state where training failed during progress. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                | The state where training creation has failed. If creation continues to fail, please contact customer support.                                      |
    | FAIL TRAIN IN PROGRESS, COMPLETE IN PROGRESS | The state where resources used for training are being cleaned up.                                                                                  |

- **Actions**
    - **Go to TensorBoard**: TensorBoard, where you can check statistical information of training, opens in a new browser window.<br/>
        For how to leave TensorBoard logs, see [Appendix > 5. Storing Metric Logs for TensorBoard Utilization](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Training**: You can stop training in progress.

- **Hyperparameters**: You can check the hyperparameter values set for training in the **Hyperparameters** tab of the detail screen displayed when you select training.

- **Monitoring**: You can check the list of monitoring target instances and basic metric charts in the **Monitoring** tab of the detail screen displayed when you select training.
    - The **Monitoring** tab is disabled when training is in a creating state.

<a id="training.copy"></a>

### Copy Training

Create new training with the same settings as existing training.

1. Select the training you want to copy.
2. Click **Copy Training**.
3. The training creation screen is displayed with the same settings as existing training.
4. If there's information you want to change settings for, change it and then click **Create Training** to create the training.

<a id="training.model.create"></a>

### Create Model from Training

Create a model from training in a completed state.

1. Select the training you want to create as a model.
2. Click **Create Model**. Only training in COMPLETE state can be created as a model.
3. You are moved to the model creation page. After checking the content, click **Create Model** to create the model. For details on model creation, see the [Model](#model) document.

<a id="training.delete"></a>

### Delete Training

Delete training.

1. Select the training you want to delete.
2. Click **Delete Training**. Training in progress can be deleted after stopping.
3. The requested delete operation cannot be canceled. To continue, click **Confirm**.

!!! tip "Note"
    If there are models created from the training you want to delete, you cannot delete the training. Delete the models first, then delete the training.

<a id="hyperparameter.tuning"></a>

## Hyperparameter Tuning

Hyperparameter tuning is the process of optimizing hyperparameter values to maximize the prediction accuracy of models. If you don't use this feature, you would have to find optimal values by manually adjusting hyperparameters while directly running many training jobs.

<a id="hyperparameter.tuning.create"></a>

### Create Hyperparameter Tuning

This is how to configure a hyperparameter tuning job.

- **Training Template**
    - **Use**: Select whether to use a training template. Using a training template fills in some configuration values for hyperparameter tuning with predefined values.
    - **Training Template**: Select the training template to use for automatically entering some configuration values for hyperparameter tuning.
- **Basic Information**
    - **Hyperparameter Tuning Name**: Enter the name of the hyperparameter tuning job.
    - **Description**: Enter a description for the hyperparameter tuning job if needed.
    - **Experiment**: Select the experiment that will contain the hyperparameter tuning. Experiments group related hyperparameter tuning jobs. If no experiment has been created, click **Add** to create an experiment.
- **Tuning Strategy**
    - **Strategy Name**: Select which strategy to use to find optimal hyperparameters.
    - **Random Seed**: Determines random number generation. Specify a fixed value for reproducible results.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information about provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select an algorithm.
            - **Hyperparameter Spec**: Enter the hyperparameter value ranges to use for hyperparameter tuning. For detailed information about hyperparameters by algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
                - **Name**: Define which hyperparameter to tune. This is predefined for each algorithm.
                - **Type**: Select the data type of the hyperparameter. This is predefined for each algorithm.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determines the change size of hyperparameter values when using the "Grid" tuning strategy.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use an algorithm written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the NHN Cloud Object Storage path where the algorithm is stored.
                    - Enter the directory path in obs://{Object Storage API Endpoint}/{containerName}/{path} format.
                    - When using NHN Cloud Object Storage, set permissions by referring to [Appendix > 1. Add AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission). Model creation will fail if necessary permissions are not set.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is stored.
                    - Enter the directory path in nas://{NAS ID}:/{path} format.
            - **Entry Point**
                - The entry point is the entry point of algorithm execution where training starts. Write the entry point filename.
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
    - **Number of Parallel Trainings**: Enter the number of trainings to perform in parallel simultaneously.
    - **Use torchrun**: Select whether to use torchrun supported by the Pytorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. Using torchrun enables distributed training by running multiple processes on one node. The number of processes affects memory usage.
- **Input Data**
    - **Dataset**: Enter the dataset to execute training. Up to 10 datasets can be set.
        - Dataset Name: Enter the dataset name.
        - Data Path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to continue training from a saved checkpoint, enter the checkpoint storage path.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save training execution results.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides checkpoints, enter the checkpoint storage path.
        - Generated checkpoints can be used to resume training from previous training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Metrics**
    - **Metric Name**: Define which metrics to collect from the logs output by the training code.
    - **Metric Format**: Enter the regular expression to use for collecting metrics. The training algorithm must output metrics matching the regular expression.
- **Objective Metric**
    - **Metric Name**: Select which metric to optimize as the objective.
    - **Objective Metric Type**: Select the optimization type.
    - **Target Value**: The tuning job ends when the objective metric reaches this value.
- **Tuning Resource Configuration**
    - **Maximum Failed Training Count**: Define the maximum number of failed trainings. The tuning ends with failure when the number of failed trainings reaches this value.
    - **Maximum Training Count**: Define the maximum number of trainings. Tuning runs until the number of automatically executed trainings reaches this value.
- **Training Early Stopping**
    - **Name**: Stop training early if the model no longer improves even when training continues.
    - **Minimum Training Count**: Define from how many trainings to get objective metric values when calculating the median.
    - **Start Step**: Set from which training step to apply early stopping.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance to execute training.
        - Used only when using NHN Cloud Object Storage. Must be specified with sufficient size to store all data needed for training.
    - **Maximum Runtime**: Specify the maximum runtime until training completion. Trainings that exceed the maximum runtime are terminated.
    - **Log Management**: Logs generated during training can be stored in NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before training completion may cause training to fail.

<a id="hyperparameter.tuning.list"></a>

### Hyperparameter Tuning List

The hyperparameter tuning list is displayed. By selecting a hyperparameter tuning from the list, you can check detailed information and modify the information.

- **Duration**: Shows the time taken for hyperparameter tuning.
- **Completed Training**: Indicates the number of completed training sessions among those automatically generated by hyperparameter tuning.
- **Training in Progress**: Indicates the number of training sessions in progress.
- **Failed Training**: Indicates the number of failed training sessions.
- **Best Training**: Shows the target metric information of the training that recorded the best target metric value among the training sessions automatically generated by hyperparameter tuning.
- **Status**: The status of hyperparameter tuning is displayed. See the table below for major statuses.

    | Status                                                                           | Description                                                                                                                                              |
    | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                                                 | The status when hyperparameter tuning creation has been requested.                                                                                      |
    | CREATE IN PROGRESS                                                               | The status when resources required for hyperparameter tuning are being created.                                                                         |
    | RUNNING                                                                          | The status when hyperparameter tuning is in progress.                                                                                                   |
    | STOPPED                                                                          | The status when hyperparameter tuning has been stopped by user request.                                                                                 |
    | COMPLETE                                                                         | The status when hyperparameter tuning has completed normally.                                                                                           |
    | STOP IN PROGRESS                                                                 | The status when hyperparameter tuning is being stopped.                                                                                                 |
    | FAIL HYPERPARAMETER TUNING                                                       | The status when hyperparameter tuning has failed during progress. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                                                    | The status when hyperparameter tuning creation has failed. If creation continues to fail, please contact customer support.                            |
    | FAIL HYPERPARAMETER TUNING IN PROGRESS, COMPLETE IN PROGRESS, STOP IN PROGRESS  | The status when resources used for hyperparameter tuning are being cleaned up.                                                                          |

- **Detailed Status Information**: The content in parentheses for `COMPLETE` status is detailed status information. See the table below for major detailed information.

    | Detailed Information | Description                                                                                           |
    | -------------------- | ----------------------------------------------------------------------------------------------------- |
    | GoalReached          | Detailed information when hyperparameter tuning training has completed by reaching the target value. |
    | MaxTrialsReached     | Detailed information when hyperparameter tuning has completed by reaching the maximum number of training sessions. |
    | SuggestionEndReached | Detailed information when the search algorithm of hyperparameter tuning has explored all hyperparameters. |

- **Actions**
    - **Go to TensorBoard**: Opens TensorBoard in a new browser window where you can check training statistics.<br/>
        For how to save TensorBoard logs, see [Appendix > 5. Saving Metric Logs for TensorBoard Utilization](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Hyperparameter Tuning**: You can stop hyperparameter tuning in progress.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select hyperparameter tuning, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when hyperparameter tuning is in the creation state.

<a id="hyperparameter.tuning.training.list"></a>

### Hyperparameter Tuning Training List

The training list automatically generated by hyperparameter tuning is displayed. You can check detailed information by selecting a training from the list.

- **Target Metric Value**: Represents the target metric value.
- **Status**: Displays the status of training automatically generated by hyperparameter tuning. See the table below for key statuses.

    | Status              | Description                                                                                                                        |
    | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
    | CREATED             | Training has been created.                                                                                                         |
    | RUNNING             | Training is in progress.                                                                                                           |
    | SUCCEEDED           | Training has completed successfully.                                                                                               |
    | KILLED              | Training has been stopped by the system.                                                                                          |
    | FAILED              | Training failed during execution. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | METRICS_UNAVAILABLE | Target metrics cannot be collected.                                                                                               |
    | EARLY_STOPPED       | Training was stopped early because performance (target metric) did not improve further during execution.                          |

<a id="hyperparameter.tuning.copy"></a>

### Copy Hyperparameter Tuning

Create new hyperparameter tuning with the same settings as existing hyperparameter tuning.

1. Select the hyperparameter tuning you want to copy.
2. Click **Copy Hyperparameter Tuning**.
3. The hyperparameter tuning creation screen is displayed with the same settings as the existing hyperparameter tuning.
4. If there are settings you want to change, modify them and click **Create Hyperparameter Tuning** to create the hyperparameter tuning.

<a id="hyperparameter.tuning.model.create"></a>

### Creating Model from Hyperparameter Tuning

Create a model with the best training from completed hyperparameter tuning.

1. Select the hyperparameter tuning you want to create as a model.
2. Click **Create Model**. Only hyperparameter tuning in COMPLETE status can be created as a model.
3. You will be redirected to the model creation page. After reviewing the content, click **Create Model** to create the model.
   For more details on model creation, see the [Model](#model) document.

<a id="hyperparameter.tuning.delete"></a>

### Delete Hyperparameter Tuning

Delete hyperparameter tuning.

1. Select the hyperparameter tuning you want to delete.
2. Click **Delete Hyperparameter Tuning**. Hyperparameter tuning in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

!!! tip "Good to Know"
    If there are models created from the hyperparameter tuning you want to delete, you cannot delete the hyperparameter tuning. Delete the models first, then delete the hyperparameter tuning.

<a id="training.template"></a>

## Training Template

You can create training templates in advance and use the values entered in the template when creating training or hyperparameter tuning.

<a id="training.template.create"></a>

### Create Training Template

For information that can be configured in training templates, see [Create Training](#training.create).

<a id="training.template.list"></a>

### Training Template List

The training template list is displayed. Select a training template from the list to view details and modify information.

- **Actions**
    - **Modify**: You can modify training template information.
- **Hyperparameters**: You can check the hyperparameter names configured in the training template in the **Hyperparameters** tab of the detail screen displayed when you select a training template.

<a id="training.template.copy"></a>

### Copy Training Template

Creates a new training template with the same settings as an existing training template.

1. Select the training template you want to copy.
2. Click **Copy Training Template**.
3. The training template creation screen is displayed with the same settings as the existing training template.
4. If there is information you want to change, modify the settings and click **Create Training Template** to create the training template.

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

- **Basic Information**: Enter the basic information of the model.
    - **Name**: Enter the model name.
        - If the model framework type is PyTorch, you must enter a model name identical to the PyTorch model name.
    - **Description**: Enter the model description.
- **Framework Information**: Enter the framework information of the model.
    - **Framework**: Select the model framework.
    - **Framework Version**: Enter the version of the model framework.
- **Model Information**: Enter the storage where the model artifacts are stored.
    - **Model Artifact**: Select the storage where the model artifacts are stored.
        - **NHN Cloud Object Storage**: Enter the Object Storage path where the model artifacts are stored.
            - Enter the directory path in the format `obs://{Object Storage API Endpoint}/{containerName}/{path}`.
            - When using NHN Cloud Object Storage, refer to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to set permissions. If you do not set permissions, model creation will fail because access to the model artifacts is not possible.
        - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the model artifacts are stored.
            - Enter the directory path in the format `nas://{NAS ID}:/{path}`.
    - **Parameters**: Enter the parameter information of the model.
        - **Parameter Name**: Enter the model parameter name.
        - **Parameter Value**: Enter the model parameter value.

!!! tip "Note"
    Values entered as model parameters are used when serving the model. Parameters can be used as arguments and environment variables.
    Arguments are used as-is with the entered parameter name, and environment variables are used with the parameter name converted to screaming snake case.

!!! tip "Note"
    When creating HuggingFace models, you can create a model by entering the HuggingFace model ID as a parameter.
    The HuggingFace model ID can be found in the URL of the HuggingFace model page.
    For more details, see [Appendix > 11. Framework-specific Serving Notes](#appendix.11.framework.note).

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

!!! danger "Caution"
    HuggingFace model file types are limited to safetensors.
    safetensors is a safe and efficient machine learning model file format developed by HuggingFace.
    Other file formats are not supported.

!!! danger "Caution"
    When creating TensorFlow (Triton), PyTorch (Triton), ONNX (Triton) models, the model artifact path you enter must have model files and `config.pbtxt` file stored in a structure that allows the model to run with Triton.
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

The model list is displayed. You can check detailed information and modify information by selecting a model from the list.

- **Name**: The model name and description are displayed. You can change the model name and description by clicking **Modify**.
- **Model Artifact Path**: The storage where the model artifacts are stored is displayed.
- **Status**: The model status is displayed. Refer to the table below for main statuses.

    | Status             | Description                                                                                    |
    | ------------------ | ---------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Model creation has been requested.                                                             |
    | CREATE IN PROGRESS | Resources required for the model are being created.                                           |
    | DELETE IN PROGRESS | The model is being deleted.                                                                    |
    | ACTIVE             | The model has been created successfully.                                                       |
    | CREATE FAILED      | Model creation has failed. If creation continues to fail, please contact customer support.   |
    | DELETE FAILED      | Model deletion has failed. Please try again.                                                  |

- **Training Name**: For models created from training, the name of the underlying training is displayed.
- **Training ID**: For models created from training, the ID of the underlying training is displayed.
- **Framework**: The model framework information is displayed.
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

Create batch inference that can perform batch inference with the selected model and check inference results as statistics.

1. Select the model you want to create batch inference with from the list.
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

- **Basic Information**: Enter basic information for the model evaluation.
    - **Name**: Enter the model evaluation name.
    - **Description**: Enter the model evaluation description.
- **Model Information**: Enter information for the model to be evaluated.
    - **Model**: Select the model to evaluate. Only classification models and regression models are supported.
    - **Class Name**: Enter the class name of the model.
- **Model Evaluation Instance Information**
    - **Instance Type**: Select the instance type to run the model evaluation. Used for data preprocessing and evaluation calculation tasks.
- **Input Data**: Input data is used to compare predictions generated through batch inference with ground truth. Fields used for inference and the ground truth field are required.
    - **Data Path**: Enter the path where the input data is located.
        - **Input Data Format**: Select the format of the input data. CSV and JSONL formats are supported, and file extensions must be .csv and .jsonl respectively.
        - **Evaluation Target Field**: Enter the field name of the ground truth label.
- **Batch Inference Output Data**
    - **Data Path**: Enter the path where the batch inference results will be saved.
- **Batch Inference Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Number of Instances**: Enter the number of instances to perform batch inference.
    - **Number of Pods**: Enter the number of pods for batch inference.
    - **Batch Size**: Enter the number of data samples processed simultaneously in a single inference task.
    - **Inference Timeout (seconds)**: Enter the timeout for batch inference. Sets the maximum allowable time for a single inference request to be processed and return results.
- **Additional Settings**
    - **Maximum Progress Time**: Specify the maximum progress time until model evaluation is completed. Model evaluations that exceed the maximum progress time will be terminated.
    - **Log Management**: Logs generated during model evaluation progress can be saved to the NHN Cloud Log & Crash service.
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
- **Status**: The status of the model evaluation is displayed. Refer to the table below for main statuses.

    | Status                                                   | Description                                                                                |
    |----------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | CREATE REQUESTED                                         | Model evaluation creation has been requested.                                               |
    | CREATE IN PROGRESS                                       | Model evaluation is being created.                                                         |
    | CREATE FAILED                                            | Model evaluation creation has failed. Please try again.                                    |
    | RUNNING                                                  | Model evaluation is in progress.                                                           |
    | COMPLETE IN PROGRESS, FAIL MODEL EVALUATION IN PROGRESS  | Resources used for model evaluation are being cleaned up.                                  |
    | COMPLETE                                                 | Model evaluation has been completed normally.                                               |
    | STOP IN PROGRESS                                         | Model evaluation is being stopped.                                                         |
    | STOPPED                                                  | Model evaluation has been stopped by user request.                                         |
    | FAIL MODEL EVALUATION                                    | Model evaluation has failed. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | DELETE IN PROGRESS                                       | Model evaluation is being deleted.                                                         |

- **Actions**
    - **Stop**: You can stop model evaluation in progress.

<a id="model.evaluation.classification.metric"></a>

### Classification Model Evaluation Metrics

- **PR AUC**: Area under the precision-recall (PR) curve. Effective for measuring model classification performance on imbalanced datasets.
- **ROC AUC**: Area under the ROC curve (recall-false positive rate). The closer to 1, the better the performance.
- **Log Loss**: Loss value calculated using a log function for the difference between predicted probabilities and actual ground truth. Lower values mean the model's predictions are more reliable.
- **F1 Score**: Harmonic mean of precision and recall. Useful when there is class imbalance, and closer to 1 is better.
- **Precision**: Ratio of true positives among those predicted as positive. Focuses on reducing False Positives.
- **Recall**: Ratio of actual positives that the model correctly predicted as positive. Important for reducing False Negatives.
- **Precision-Recall Curve**: A curve that visualizes the relationship between precision and recall at various thresholds. Reference when adjusting model thresholds.
- **ROC Curve**: Shows the relationship between recall and false positive rate at various thresholds. Used for setting classification thresholds or comparing models.
- **Threshold-based Precision-Recall Curve**: Graph showing how precision and recall change at specific thresholds. Referenced when setting actual operational criteria.
- **Confusion Matrix**: A matrix that categorizes prediction results into four types: TP, FP, FN, TN. Makes it easy to identify error types by class.

<a id="model.evaluation.regression.metric"></a>

### Regression Model Evaluation Metrics

- **MAE (Mean Absolute Error)**: Average of absolute values of differences between actual values and predicted values. Intuitively shows the magnitude of prediction errors.
- **MAPE (Mean Absolute Percentage Error)**: Average of ratios of prediction errors divided by actual values. Since it's ratio-based, it may be unsuitable for data with values close to 0.
- **R-squared (Coefficient of Determination)**: Indicates how well the model explains actual data, with higher explanatory power closer to 1.
- **RMSE (Root Mean Squared Error)**: Square root of the mean squared error. More sensitive to large errors and can interpret results on the same scale as actual units.
- **RMSLE (Root Mean Squared Logarithmic Error)**: Calculated from the difference between log-transformed actual and predicted values. Not sensitive to magnitude differences, useful for evaluating exponential growth data.

<a id="model.evaluation.compare"></a>

### Compare Model Evaluations

Compares evaluation metrics of multiple models.

1. Select the model evaluations you want to compare from the list.
2. Click **Compare**.

<a id="model.evaluation.delete"></a>

### Delete Model Evaluation

Deletes a model evaluation.

1. Select the model evaluation you want to delete.
2. Click **Delete**. Model evaluations in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. Click **Confirm** to continue.

<a id="endpoint"></a>

## Endpoint

Create and manage endpoints for serving models.

<a id="endpoint.create"></a>

### Create Endpoint

- **Enable API Gateway Service**
    - AI EasyMaker endpoints create API endpoints and manage APIs through the NHN Cloud API Gateway service. To use the endpoint feature, you must enable the API Gateway service.
    - For more details and pricing on the API Gateway service, see the following:
        - [API Gateway Service Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/ko/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Endpoint**: Select whether to add a stage to a new or existing endpoint.
    - **Create New Endpoint**: Creates a new endpoint. An endpoint is created in API Gateway with a new service and default stage.
    - **Add New Stage to Existing Endpoint**: An endpoint is created as a new stage in the API Gateway service of an existing endpoint. Select an existing endpoint to add a stage to.
- **Endpoint Name**: Enter the endpoint name. Endpoint names cannot be duplicated.
- **Stage Name**: When adding a new stage to an existing endpoint, enter the new stage name. Stage names cannot be duplicated.
- **Description**: Enter the endpoint stage description.
- **Instance Information**: Enter the instance information where the model will be served.
    - **Instance Type**: Select the instance type.
    - **Number of Instances**: Enter the number of running instances.
    - **Autoscaler**: The autoscaler automatically adjusts the number of nodes according to resource usage policies. Autoscaler is configured per stage.
        - **Use/Don't Use**: Select whether to use the autoscaler. When enabled, the number of instances scales in or out based on instance load.
        - **Minimum Nodes**: Minimum number of nodes that can be scaled down
        - **Maximum Nodes**: Maximum number of nodes that can be scaled up
        - **Scale-in**: Set whether to enable node scale-in
        - **Resource Usage Threshold**: Reference value for the resource usage threshold area that serves as the criterion for scale-in
        - **Threshold Area Maintenance Time (minutes)**: Resource usage maintenance time below the threshold for nodes to be scaled down
        - **Scale-in Delay Time After Scale-out (minutes)**: Delay time from node scale-out until monitoring begins for scale-in target nodes
- **Stage Information**: Enter information about the model artifacts to deploy to the endpoint. When the same model is deployed to multiple stage resources, requests are distributed for processing.
    - **Model**: Select the model you want to deploy to the endpoint. If no model has been created, create a model first. For serving considerations by model framework, see [Appendix > 11. Framework-Specific Serving Considerations](#appendix.11.framework.note).
    - **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance at a fixed ratio.
        - **cpu**: Enter the CPU allocation. Enter when directly allocating without using allocation ratio (%).
        - **memory**: Enter the Memory allocation. Enter when directly allocating without using allocation ratio (%).
        - **gpu**: Enter the GPU allocation. Enter when directly allocating without using allocation ratio (%).
    - **Description**: Enter the stage resource description.
    - **Pod Autoscaler**: A feature that automatically adjusts the number of pods based on the model's request volume. Autoscaler is configured per model.
        - **Use/Don't Use**: Select whether to use the autoscaler. When enabled, the number of pods scales in or out based on model load.
        - **Scale-out Unit**: Enter the pod scale-out unit.
            - **CPU**: The number of pods is adjusted based on CPU usage.
            - **Memory**: The number of pods is adjusted based on Memory usage.
        - **Threshold Value**: The threshold value per scale-out unit at which pods will be scaled out.
    - **Resource Information**: You can check the actual resources being used. Actual resource usage is allocated to each model based on the entered model allocation. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).

!!! tip "Note"
    The AI EasyMaker service provides endpoints based on the OIP (open inference protocol) specification. For endpoint API specification details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
    To use a separate endpoint, refer to the resources created in the API Gateway service to create and use new resources.
    For more details on the OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

!!! tip "Note"
    Creating an endpoint may take several minutes.
    When creating resources for the first time, additional minutes may be required for service environment configuration.

!!! tip "Note"
    Creating a new endpoint creates a new API Gateway service.
    Adding a new stage to an existing endpoint creates a new stage in the API Gateway service.
    If the default quota of the [API Gateway Service Resource Provision Policy](https://docs.nhncloud.com/en/nhncloud/ko/resource-policy/#api-gateway) is exceeded, endpoint creation in AI EasyMaker may not be possible. In this case, you can resolve this by adjusting the API Gateway service resource quota.

<a id="endpoint.list"></a>

### Endpoint List

The endpoint list is displayed. Selecting an endpoint from the list allows you to check detailed information and modify the information.

- **Default Stage URL**: The URL of the default stage among the endpoint's stages is displayed.
- **Status**: The status of the endpoint. See the table below for major statuses.

    | Status             | Description                                                                                                                                       |
    | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | The endpoint creation has been requested.                                                                                                         |
    | CREATE IN PROGRESS | The endpoint is being created.                                                                                                                    |
    | UPDATE IN PROGRESS | Some stages of the endpoint have tasks in progress.<br/>You can check the task status for each stage in the endpoint stage list.               |
    | DELETE IN PROGRESS | The endpoint is being deleted.                                                                                                                    |
    | ACTIVE             | The endpoint is running normally.                                                                                                                 |
    | CREATE FAILED      | The endpoint creation has failed.<br/>You must delete the endpoint and create it again. If the creation failed status repeats, contact customer support. |
    | UPDATE FAILED      | Some stages of the endpoint are not serving normally. You must delete the problematic stage and create it again.                                |

- **API Gateway Status**: The API Gateway status information of the endpoint's default stage is displayed. See the table below for major statuses.

    | Status                         | Description                                                                                                                                                                                                                                      |
    | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | CREATE IN PROGRESS             | API Gateway resources are being created.                                                                                                                                                                                                        |
    | STAGE DEPLOYING                | The API Gateway default stage is being deployed.                                                                                                                                                                                                |
    | ACTIVE                         | The API Gateway default stage has been successfully deployed and is active.                                                                                                                                                                     |
    | NOT FOUND: STAGE               | The default stage of the endpoint cannot be found.<br/>Check if the stage exists in the API Gateway console.<br/>If the stage has been deleted, the deleted API Gateway stage cannot be recovered, and you must delete the endpoint and create it again. |
    | NOT FOUND: STAGE DEPLOY RESULT | The deployment status of the endpoint's default stage cannot be found.<br/>Check if the default stage is deployed in the API Gateway console.                                                                                                  |
    | STAGE DEPLOY FAIL              | The API Gateway default stage has failed to deploy.                                                                                                                                                                                             |

<a id="endpoint.stage.create"></a>

### Create Endpoint Stage

Add a new stage to an existing endpoint. By creating a new stage, you can test the new stage without affecting the default stage.

1. Click **Endpoint Name** in the endpoint list.
2. Click **+ Create Stage**.
3. Adding a new stage to an existing endpoint is automatically selected, and the configuration method is the same as creating an endpoint.
4. The requested delete operation cannot be canceled. To proceed, click **Confirm**.

<a id="endpoint.stage.list"></a>

### Endpoint Stage List

A list of stages created under the endpoint is displayed. You can view detailed information by selecting a stage from the list.

- **Status**: The status of the endpoint stage is displayed. See the table below for key statuses.

    | Status             | Description                                                                     |
    | ------------------ | ------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Endpoint stage creation has been requested.                                     |
    | CREATE IN PROGRESS | Endpoint stage is being created.                                                |
    | DEPLOY IN PROGRESS | Model is being deployed to the endpoint stage.                                 |
    | DELETE IN PROGRESS | Endpoint stage is being deleted.                                                |
    | ACTIVE             | Endpoint stage is running normally.                                             |
    | CREATE FAILED      | Endpoint stage creation failed. Please try again.                              |
    | DEPLOY FAILED      | Endpoint stage deployment failed. Please try creating again.                   |

- **API Gateway Status**: The stage status of the API Gateway where the endpoint stage is deployed is displayed.
- **Default Stage**: Whether it is the default stage is displayed.
- **Stage URL**: The stage URL of the API Gateway where the model is served is displayed.
- **View API Gateway Settings**: To check the settings that AI EasyMaker deployed to the API Gateway stage, click **View Settings**.
- **View API Gateway Statistics**: To view API statistics for the endpoint, click **View Statistics**.
- **Instance Type**: The endpoint instance type where the model is served is displayed.
- **Running Work Nodes/Pods**: The number of nodes and pods in use by the endpoint is displayed.
- **Stage Resources**: Information about model artifacts deployed to the stage is displayed.
- **Monitoring**: In the **Monitoring** tab of the detail screen that appears when you select an endpoint stage, you can view the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when the endpoint stage is being created.
- **API Statistics**: In the **API Statistics** tab of the detail screen that appears when you select an endpoint stage, you can view API statistics information for the endpoint stage.
    - The **API Statistics** tab is disabled when the endpoint stage is being created.

!!! danger "Caution"
    When AI EasyMaker creates an endpoint or endpoint stage, it creates API Gateway services and stages for the endpoint.
    If you make changes directly to the API Gateway services and stages created by AI EasyMaker through the API Gateway service console, be sure to note the following precautions:

    1. Do not delete the API Gateway services and stages created by AI EasyMaker. If deleted, API Gateway information may not display properly for the endpoint, and endpoint changes may not be applied to the API Gateway.
    2. Do not modify or delete the resource at the API Gateway resource path entered when creating the endpoint. If deleted, inference API calls to the endpoint may fail.
    3. Do not add resources under the API Gateway resource path entered when creating the endpoint. Added resources may be deleted during endpoint stage addition/modification operations.
    4. Do not disable or change the **Backend Endpoint URL Override** set for the API Gateway resource path in the API Gateway stage settings. Changes may cause inference API calls to the endpoint to fail.
       Other settings besides the above precautions can utilize features provided by API Gateway as needed.
       For detailed information on using API Gateway, see [API Gateway Console Guide](https://docs.nhncloud.com/ko/Application%20Service/API%20Gateway/ko/console-guide/).

!!! tip "Note"
    If AI EasyMaker endpoint stage settings are not deployed to the API Gateway stage due to temporary issues, it will be displayed as 'deployment failed' status.
    In this case, you can manually deploy the API Gateway stage by selecting the stage from the stage list > **View API Gateway Settings** in the detail screen at the bottom > clicking **Deploy Stage**.
    If the deployment status is not restored with the above guide, please contact customer support.

<a id="endpoint.stage.resource.create"></a>

### Create Stage Resource

Add a new resource to an existing endpoint stage.

- **Model**: Select the model to deploy to the endpoint. If you have not created a model, create a model first.
- **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance at a fixed ratio.
    - **CPU**: Enter the CPU allocation. Enter this if you want to allocate directly without using the allocation ratio (%).
    - **Memory**: Enter the Memory allocation. Enter this if you want to allocate directly without using the allocation ratio (%).
- **Number of Pods**: Enter the number of pods for the stage resource.
- **Description**: Enter a description for the stage resource.
- **Pod Autoscaler**: A feature that automatically adjusts the number of pods based on the model's request volume. Autoscaler is configured on a per-model basis.
    - **Use/Do Not Use**: Select whether to use the autoscaler. When enabled, the number of pods scales in or out based on model load.
    - **Scale-out Unit**: Enter the pod scale-out unit.
        - **CPU**: The number of pods is adjusted based on CPU usage.
        - **Memory**: The number of pods is adjusted based on Memory usage.
    - **Threshold Value**: The threshold value for each scale-out unit at which pods will be scaled out.

<a id="endpoint.stage.resource.list"></a>

### Stage Resource List

Displays the list of resources created under an endpoint stage.

- **Status**: Shows the status of the stage resource. Refer to the table below for main statuses.

    | Status             | Description                                                   |
    | ------------------ | ------------------------------------------------------------- |
    | CREATE REQUESTED   | The stage resource creation has been requested.              |
    | CREATE IN PROGRESS | The stage resource is being created.                         |
    | DELETE IN PROGRESS | The stage resource is being deleted.                         |
    | ACTIVE             | The stage resource has been successfully deployed.           |
    | CREATE FAILED      | The stage resource creation has failed. Please try again.    |

- **Model Name**: The name of the model deployed to the stage.
- **API Gateway Resource Path**: The inference URL of the model deployed to the stage. You can request inference using the displayed URL. For more details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
- **Pod Count**: Shows the number of healthy pods and total pods in use by the resource.

<a id="endpoint.inference.call"></a>

### Endpoint Inference Calls

1. In **Endpoints** > **Endpoint Stages**, click a stage to display the stage details screen at the bottom.
2. Check the API Gateway resource path in the stage resource tab of the details screen.
3. Call the API Gateway resource path with the HTTP POST method to invoke the inference API.
    - The request and response specifications of the inference API vary depending on the algorithm you created.

            // Inference API example: Request
            curl --location --request POST '{API Gateway Resource Path}' \
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

1. Click **Endpoint Name** in the endpoint list to go to the endpoint stage list.
2. In the endpoint stage list, click the endpoint stage where the stage resource to be deleted is deployed. When clicked, the stage details screen is displayed at the bottom.
3. In the **Stage Resource** tab of the details screen, select the stage resource to delete.
4. Click **Delete Stage Resource**.
5. The requested deletion operation cannot be canceled. Click **Confirm** to continue.

<a id="endpoint.default.stage.change"></a>

### Change Endpoint Default Stage

Change the default stage of an endpoint to another stage.
To change the model of an endpoint without service interruption, AI EasyMaker recommends deploying models using the stage feature.

1. The stage actually running in service operates as the default stage.
2. When replacing with a new model, add a new stage to the existing endpoint.
3. Confirm that there are no issues with the endpoint service using the replaced model in the new stage.
4. Click **Change Default Stage**.
5. Select the new stage to change to the default stage from the stage to change.
6. The change request operation cannot be canceled. Click **Confirm** to continue.
7. The stage to change becomes the default stage, and the resources of the existing default stage are automatically deleted.

<a id="endpoint.stage.delete"></a>

### Delete Endpoint Stage

1. Click **Endpoint Name** in the endpoint list to go to the endpoint stage list.
2. In the endpoint stage list, select the endpoint stage to delete. The default stage cannot be deleted.
3. Click **Delete Stage**.
4. The requested deletion operation cannot be canceled. Click **Confirm** to continue.

!!! danger "Caution"
    When you delete an endpoint stage in AI EasyMaker, the stage of the API Gateway service where the endpoint's stage is deployed is also deleted.
    If there are APIs in operation on the API Gateway stage being deleted, API calls will not be possible, so please be careful.

<a id="endpoint.delete"></a>

### Delete Endpoint

Delete an endpoint.

1. Select the endpoint you want to delete from the endpoint list.
2. If there are stages other than the default stage under the endpoint, the endpoint cannot be deleted. Delete other stages first, then delete the endpoint.
3. Click **Delete Endpoint**.
4. The requested deletion operation cannot be canceled. Click **Confirm** to continue.

!!! danger "Caution"
    When you delete an endpoint in AI EasyMaker, the API Gateway service where the endpoint is deployed is also deleted.
    If there are APIs in operation on the API Gateway service being deleted, API calls will not be possible, so please be careful.

<a id="batch.inference"></a>

## Batch Inference

Provides an environment where you can perform batch inference with AI EasyMaker models and check inference results through statistics.

<a id="batch.inference.create"></a>

### Create Batch Inference

Configure the environment where batch inference will be performed by selecting instances and OS images, and proceed with batch inference by entering the paths for input/output data to be inferred.

- **Basic Information**: Enter basic information for batch inference.
    - **Batch Inference Name**: Enter the batch inference name.
    - **Batch Inference Description**: Enter a description.
- **Instance Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Number of Instances**: The number of instances to perform batch inference.
- **Model Information**
    - **Model**: Select the model for batch inference. If you haven't created a model, create one first.
    - **Number of Pods**: Enter the number of pods for the model.
    - **Resource Information**: You can check the actual resources used by the model. The actual usage is divided according to the number of pods entered and allocated to each pod. For details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).
- **Input Data**
    - **Data Path**: Enter the path of data to run batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Input Data Type**: Select the type of data to run batch inference.
        - **JSON**: Uses valid JSON data in files as input values.
        - **JSONL**: Uses JSON Lines files where each line consists of valid JSON as input values.
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
        - **Inference Timeout (seconds)**: Enter the timeout for batch inference. You can set the maximum allowed time for a single inference request to be processed and results returned.
    - **Data Storage Size**: Enter the data storage size of the instance to run batch inference.
        - Used only when using NHN Cloud Object Storage. You must specify a sufficient size to store all data required for batch inference.
    - **Maximum Batch Inference Time**: Specify the maximum wait time until batch inference is completed. Batch inference that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during batch inference can be saved to the NHN Cloud Log & Crash Search service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Good to Know"
    - When using Glob patterns, **exclude Glob patterns** are applied with priority.
    - **Batch size** and **inference timeout** should be set appropriately according to the performance of the model performing batch inference. If the entered settings are incorrect, batch inference may not achieve sufficient performance.

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before batch inference is completed may cause batch inference to fail.
    - When using Glob patterns, if values are not entered appropriately, input data may not be found and batch inference may not operate normally.

!!! danger "Caution"
    Batch inference using GPU instances allocates GPU instances according to the number of pods.
    If `number of pods / number of GPUs` is not divisible by an integer, unallocated GPUs may occur.
    Since unallocated GPUs are not used for batch inference, set the number of pods appropriately to use GPU instances efficiently.

<a id="batch.inference.list"></a>

### Batch Inference List

The batch inference list is displayed. Select a batch inference from the list to check detailed information and modify information.

- **Inference Duration**: The time batch inference has been running is displayed.
- **Status**: The status of batch inference is displayed. Refer to the table below for main statuses.

    | Status                                                   | Description                                                                                                                                   |
    | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                       | Batch inference creation has been requested.                                                                                                    |
    | CREATE IN PROGRESS                                     | Resources required for batch inference are being created.                                                                                        |
    | RUNNING                                                | Batch inference is in progress.                                                                                                      |
    | STOPPED                                                | Batch inference has been stopped by user request.                                                                                       |
    | COMPLETE                                               | Batch inference has been completed normally.                                                                                              |
    | STOP IN PROGRESS                                       | Batch inference is being stopped.                                                                                                      |
    | FAIL BATCH INFERENCE                                   | Batch inference failed during execution. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | CREATE FAILED                                          | Batch inference creation has failed. If creation continues to fail, contact customer support.                                              |
    | FAIL BATCH INFERENCE IN PROGRESS, COMPLETE IN PROGRESS | Resources used for batch inference are being cleaned up.                                                                                      |

- **Actions**
    - **Stop**: You can stop batch inference in progress.
- **Monitoring**: In the **Monitoring** tab of the detailed screen displayed when you select batch inference, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when batch inference is being created.

<a id="batch.inference.copy"></a>

### Copy Batch Inference

Create new batch inference with the same settings as existing batch inference.

1. Select the batch inference you want to copy.
2. Click **Copy Batch Inference**.
3. The batch inference creation screen is displayed with the same settings as the existing batch inference.
4. If there are settings you want to change, modify them and click **Create Batch Inference** to create batch inference.

<a id="batch.inference.delete"></a>

### Delete Batch Inference

Delete batch inference.

1. Select the batch inference you want to delete.
2. Click **Delete Batch Inference**. Batch inference in progress can be deleted after stopping.
3. The requested delete operation cannot be canceled. Click **Confirm** to continue.

<a id="personal.image"></a>

## Personal Images

You can run notebooks, training, and hyperparameter tuning using personalized container images.
Only personal images derived from the notebook/deep learning images provided by AI EasyMaker can be used when creating resources in AI EasyMaker.
See the table below for AI EasyMaker base images.

<a id="personal.image.notebook.image"></a>

#### Notebook Images

| Image Name                           | Core Type | Framework  | Framework Version | Python Version | Image Address                                                                                          |
| ------------------------------------ | --------- | ---------- | ----------------- | -------------- | ------------------------------------------------------------------------------------------------------ |
| Ubuntu 22.04 CPU Python Notebook     | CPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204    |
| Ubuntu 22.04 GPU Python Notebook     | GPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-gpu-py310-ubuntu2204    |
| Ubuntu 22.04 CPU PyTorch Notebook    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Notebook    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Notebook | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Notebook | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-gpu-py310-ubuntu2204 |

<a id="personal.image.deep.learning.image"></a>

#### Deep Learning Images

| Image Name                           | Core Type | Framework  | Framework Version | Python Version | Image Address                                                                                       |
| ------------------------------------ | --------- | ---------- | ----------------- | -------------- | --------------------------------------------------------------------------------------------------- |
| Ubuntu 22.04 CPU PyTorch Training    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Training    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Training | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Training | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-gpu-py310-ubuntu2204 |

!!! tip "Note"
    Only NHN Container Registry (NCR) can be integrated as the container registry service where personal images are stored (as of December 2023).

!!! danger "Caution"
    You can only use personal images derived from the base images provided by AI EasyMaker.

<a id="personal.image.create"></a>

### Create Personal Images

The following document guides you on how to create container images using Docker with AI EasyMaker base images and use personal images for notebooks in AI EasyMaker.

1. Write the DockerFile for your personal image.

        FROM fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204 as easymaker-notebook
        RUN conda create -n example python=3.10
        RUN conda activate example
        RUN pip install torch torchvision

2. Build personal image and push to container registry
    Build the image with Dockerfile and push the image to NCR registry.

        docker build -t {image name}:{tag} .
        docker tag {image name}:{tag} {NCR registry address}/{image name}:{tag}
        docker push {NCR registry address}/{image name}:{tag}

        (Example)
        docker build -t custom-training:v1 .
        docker tag custom-training:v1 example-kr1-registry.container.nhncloud.com/registry/custom-training:v1
        docker push example-kr1-registry.container.nhncloud.com/registry/custom-training:v1

3. Create the image pushed to NCR as a personal image in AI EasyMaker.

    1. Go to the **Images** menu in the AI EasyMaker console.
    2. Click the **Create Image** button to enter the information for the created image.
        - Name, Description: Enter the name and description for the image.
        - Address: Enter the registry image address.
        - Type: Enter the type of container image. Select **Notebook** or **Training**.
        - Account: Select an account for AI EasyMaker notebook/training nodes to access your registry repository.
            - Use New: Register a new registry account.
                - Name, Description: Enter the name and description for the registry account.
                - Category: Select the container registry service.
                - ID: Enter the ID of the registry repository.
                - Password: Enter the password of the registry repository.
            - Use Existing Account: Select an already registered registry account.

4. Create a notebook with the created personal image.
    1. Go to the **Notebooks** menu. Click the **Create Notebook** button to go to the notebook creation page.
    2. In the image information, click the **Personal Images** tab.
    3. Select the personal image to use as the notebook container image.
    4. After entering other notebook information and creating it, the notebook will run with the personal image.

!!! tip "Note"
    Personal images can be used to create resources for notebooks, training, and hyperparameter tuning.

!!! tip "Note"
    Only NHN Container Registry (NCR) service can be integrated as the container registry service (as of December 2023).
    For the NCR service account ID and password, enter the following values:
    ID: User Access Key of NHN Cloud user account
    Password: User Secret Key of NHN Cloud user account

<a id="registry.account"></a>

## Registry Account

For AI EasyMaker to pull images from a user's registry containing private images and run containers, it needs to log in to the user's registry.
By storing login information as a registry account, it can be reused for images linked to that registry account.
To manage registry accounts, navigate to the **Images** menu in the AI EasyMaker console and select the **Registry Account** tab.

<a id="registry.account.create"></a>

### Create Registry Account

Creates a new registry account.

- Name: Enter the name of the registry account.
- Description: Enter the description of the registry account.
- Category: Select a container registry service.
- ID: Enter the ID of the registry account.
- Password: Enter the password of the registry account.

<a id="registry.account.modify"></a>

### Modify Registry Account

<a id="registry.account.modify.account.modify"></a>

#### Modify Registry ID and Password

- Click the **Modify Registry Account** button.
- Enter the new ID and password, then click the **Confirm** button.

!!! tip "Note"
    When you change a registry account, the modified ID and password will be used when utilizing images linked to that account.
    If you enter incorrect registry ID or password, authentication will fail during private image pull and resource creation will fail.

!!! danger "Caution"
    Modifying ID and password when there are resources being created with private images linked to the registry account or when there are ongoing training and hyperparameter tuning may cause issues.
    Be careful when modifying ID and password.

<a id="registry.account.modify.account.info.modify"></a>

#### Registry Account > Change Name and Description

1. Select the account to change from the registry account list.
2. Click the **Change** button at the bottom of the screen.
3. Change the name and description, then click the **Confirm** button.

<a id="registry.account.delete"></a>

### Delete Registry Account

Select the registry account to delete from the list and click the **Delete Registry Account** button.

!!! tip "Note"
    Registry accounts linked to images cannot be deleted. To delete them, you must first delete the linked images and then delete the registry account.

<a id="pipeline"></a>

## Pipeline

ML pipelines are a feature for managing and executing portable and scalable machine learning workflows.
You can use the Kubeflow Pipelines (KFP) Python SDK to write components and pipelines, compile pipelines to intermediate representation YAML, and execute them in AI EasyMaker.
Most pipelines aim to produce one or more ML artifacts such as datasets, models, evaluation metrics, etc.

!!! tip "Note"
    A **pipeline** is a workflow definition that combines one or more components to form a directed acyclic graph (DAG).
    - Each component runs a single container during execution, which can produce ML artifacts.
    - Components can take inputs and produce outputs. There are two types of I/O types: parameters and artifacts.
    - Parameters are useful for passing small amounts of data between components.
    - Artifact types are for ML artifact outputs such as datasets, models, metrics, etc. They provide a convenient mechanism for storage in object storage.

!!! tip "Note"
    The ability to view console output generated during pipeline execution is not provided.
    Send pipeline code logs to Log & Crash Search using the [SDK's log sending feature](./sdk-guide/#feature.lncs.log.send) to check them.

!!! tip "Note"
    Kubeflow Pipelines (KFP) official documentation
    - [KFP User Guide](https://www.kubeflow.org/docs/components/pipelines/user-guides/)
    - [KFP SDK Reference](https://kubeflow-pipelines.readthedocs.io/ko/stable/)

<a id="pipeline.upload"></a>

### Pipeline Upload

Upload a pipeline.

- **Name**: Enter the pipeline name.
- **Description**: Enter a description.
- **File Registration**: Select the YAML file to upload.

!!! tip "Note"
    Pipeline upload may take several minutes.
    When creating resources for the first time, it may take additional minutes to configure the service environment.

<a id="pipeline.list"></a>

### Pipeline List

The pipeline list is displayed. Select a pipeline from the list to view detailed information and modify information.

- **Status**: The status of the pipeline is displayed. Refer to the table below for major statuses.

    | Status             | Description                                     |
    |--------------------|-----------------------------------------------|
    | CREATE REQUESTED   | Pipeline creation has been requested.          |
    | CREATE IN PROGRESS | Pipeline creation is in progress.              |
    | CREATE FAILED      | Pipeline creation has failed. Please try again. |
    | ACTIVE             | Pipeline has been created successfully.         |

<a id="pipeline.graph"></a>

### Pipeline Graph

The pipeline graph is displayed. Select a node in the graph to view detailed information.

A graph is a visual representation of a pipeline. Each node in the graph represents a step in the pipeline, and arrows show the parent/child relationships between pipeline components represented by each step.

<a id="pipeline.delete"></a>

### Delete Pipeline

Delete a pipeline.

1. Select the pipeline to delete.
2. Click **Delete Pipeline**. Pipelines that are being created cannot be deleted.
3. The requested deletion operation cannot be canceled. Click **Delete** to continue.

!!! tip "Note"
    If there are schedules created with the pipeline you want to delete, the pipeline cannot be deleted. Delete the pipeline schedule first, then delete the pipeline.

<a id="pipeline.run"></a>

## Pipeline Execution

You can run and manage uploaded pipelines in AI EasyMaker.

<a id="pipeline.run.create"></a>

### Create Pipeline Execution

Execute a pipeline.

- **Basic Information**
    - **Name**: Enter the pipeline execution name.
    - **Description**: Enter a description.
    - **Pipeline**: Select the pipeline to execute.
    - **Experiment**: Select the experiment that will include the pipeline execution. Experiments group related pipeline executions. If no experiment exists, click **Add** to create one.
- **Execution Information**
    - **Execution Parameters**: Enter values if there are input parameters defined in the pipeline.
    - **Execution Type**: Select the pipeline execution type. If you select **One-time**, the pipeline will run only once. To run the pipeline periodically, select **Schedule Settings** and configure the schedule by referring to [Create Pipeline Schedule](#pipeline.recurring.run.create).
- **Instance Information**
    - **Instance Type**: Select the instance type to run the pipeline.
    - **Number of Instances**: Enter the number of instances to use for pipeline execution.
- **Additional Settings**
    - **Boot Storage Size**: Enter the boot storage size for the instance that will run the pipeline.
    - **NHN Cloud NAS**: You can connect **NHN Cloud NAS** to the instance that will run the pipeline.
        - **Mount Directory Name**: Enter the directory name to mount on the instance.
        - **NAS Path**: Enter the path in the format `nas://{NAS ID}:/{path}`.
    - **Log Management**: You can save logs generated during pipeline execution to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    Creating a pipeline execution may take several minutes.
    When creating resources for the first time, additional time is required to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="pipeline.run.list"></a>

### Pipeline Execution List

The pipeline execution list is displayed. Selecting a pipeline execution from the list allows you to view detailed information and modify settings.

- **Status**: The status of the pipeline execution is displayed. Refer to the table below for key statuses.

    | Status                        | Description                                                                                    |
    |-------------------------------|------------------------------------------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline execution creation has been requested.                                                |
    | CREATE IN PROGRESS            | Pipeline execution creation is in progress.                                                    |
    | CREATE FAILED                 | Pipeline execution creation has failed. Please try again.                                     |
    | RUNNING                       | Pipeline execution is in progress.                                                             |
    | COMPLETE IN PROGRESS          | Resources used for pipeline execution are being cleaned up.                                   |
    | COMPLETE                      | Pipeline execution has completed successfully.                                                 |
    | STOP IN PROGRESS              | Pipeline execution is being stopped.                                                          |
    | STOPPED                       | Pipeline execution has been stopped by user request.                                          |
    | FAIL PIPELINE RUN IN PROGRESS| Resources used for pipeline execution are being cleaned up.                                   |
    | FAIL PIPELINE RUN             | Pipeline execution has failed. Detailed failure information can be viewed through Log & Crash Search logs if log management is enabled. |

- **Actions**
    - **Stop**: You can stop a running pipeline execution.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when selecting a pipeline execution from the list, you can view the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when pipeline execution is being created.

<a id="pipeline.run.graph"></a>

### Pipeline Execution Graph

The pipeline execution graph is displayed. Selecting a node in the graph allows you to view detailed information.

The graph is a visual representation of pipeline execution. This graph shows the steps that have already been executed and the currently running steps during pipeline execution, and represents parent/child relationships between pipeline components shown as each step with arrows. Each node in the graph represents a step in the pipeline.

Through detailed information for each node, you can download generated artifacts.

!!! danger "Caution"
    Pipeline artifacts are stored for 120 days. Artifacts older than 120 days are automatically deleted.

<a id="pipeline.run.stop"></a>

### Stop Pipeline Execution

Stop a running pipeline execution.

1. Select the pipeline execution you want to stop from the list.
2. Click **Stop Execution**.
3. The requested action cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    Stopping a pipeline execution may take several minutes.

<a id="pipeline.run.copy"></a>

### Copy Pipeline Execution

Create a new pipeline execution with the same settings as an existing pipeline execution.

1. Select the pipeline execution you want to copy.
2. Click **Copy Pipeline Execution**.
3. The pipeline execution creation screen is displayed with the same settings as the existing pipeline execution.
4. If there are settings you want to change, modify them and click **Create Pipeline Execution**.

<a id="pipeline.run.delete"></a>

### Delete Pipeline Execution

Delete a pipeline execution.

1. Select the pipeline execution to delete.
2. Click **Delete Pipeline Execution**. Running pipeline executions cannot be deleted.
3. The requested deletion cannot be canceled. Click **Delete** to proceed.

<a id="pipeline.schedule"></a>

## Pipeline Schedule

You can create and manage schedules to periodically run uploaded pipelines in AI EasyMaker.

<a id="pipeline.recurring.run.create"></a>

### Create Pipeline Schedule

Create a schedule to periodically run a pipeline.

For information that can be configured when creating a pipeline schedule other than the items below, see [Create Pipeline Run](#pipeline.run.create).

- **Run Information**
    - **Run Type**: Select the pipeline run type. When **Schedule Setting** is selected, the pipeline runs periodically. To run the pipeline only once, select **One-time**.
    - **Trigger Type**: Select the pipeline run trigger type. You can select **Time Interval** or **Cron Expression**.
        - To run the pipeline repeatedly through time interval settings, select **Time Interval** and enter a number and time unit.
        - To run the pipeline repeatedly through cron expression settings, select **Cron Expression** and enter a cron expression.
    - **Concurrent Execution Settings**: According to the trigger cycle (**Time Interval** or **Cron Expression**), a new pipeline run may be created before the previously created pipeline run is terminated. You can limit the number of runs executed in parallel by specifying the maximum number of concurrent executions.
    - **Start Time**: You can set the start time for the pipeline schedule. If not entered, pipeline runs are created according to the configured cycle.
    - **End Time**: You can set the end time for the pipeline schedule. If not entered, pipeline runs are created until stopped.
    - **Missed Run Catchup**: Determines whether to catch up when pipeline runs fall behind schedule.
        - For example, assuming a pipeline schedule is temporarily stopped and then restarted later, setting it to **Enable** will catch up on missed pipeline runs.
        - If the pipeline internally handles backfill, it should be set to **Disable** to prevent duplicate backfill operations.

!!! tip "Note"
    Creating a pipeline schedule may take a few minutes.
    When creating resources for the first time, it may take a few additional minutes to configure the service environment.

!!! tip "Note"
    Cron expressions use 6 space-separated fields to represent time.
    For more details, see the [Cron Expression Format](https://pkg.go.dev/github.com/robfig/cron#hdr-CRON_Expression_Format) documentation.

<a id="pipeline.recurring.run.list"></a>

### Pipeline Schedule List

The pipeline schedule list is displayed. By selecting a pipeline schedule from the list, you can check detailed information and change the information.

- **Status**: The status of the pipeline schedule is displayed. See the table below for major statuses.

    | Status                        | Description                                                    |
    |-------------------------------|----------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline schedule creation has been requested.                  |
    | CREATE FAILED                 | Pipeline schedule creation has failed. Please try again.       |
    | ENABLED                       | Pipeline schedule has started normally.                        |
    | ENABLED(EXPIRED)              | Pipeline schedule has started normally but has passed the configured end time. |
    | DISABLED                      | Pipeline schedule has been stopped by user request.            |

- **Run Management**: In the **Run Management** tab of the detail screen displayed when selecting a pipeline schedule from the list, you can check the list of runs created by the pipeline schedule.

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
4. If there is information you want to change in the settings, change it and then click **Create Pipeline Schedule**.

<a id="pipeline.recurring.run.delete"></a>

### Delete Pipeline Schedule

Delete a pipeline schedule.

1. Select the pipeline schedule to delete.
2. Click **Delete Pipeline Schedule**.
3. The requested deletion cannot be canceled. To proceed, click **Delete**.

!!! tip "Note"
    If a run created by the pipeline schedule you want to delete is in progress, it cannot be deleted. Delete the pipeline schedule after the pipeline run is completed.

<a id="rag"></a>

## RAG

RAG (Retrieval-Augmented Generation) is a technology that vectorizes and stores user documents, then searches for relevant content to improve the accuracy of LLM (Large Language Model) responses. AI EasyMaker can create and manage RAG systems by integrating vector stores, embedding models, and LLMs.

<a id="rag.create"></a>

### Create RAG

Create a new RAG.

- **Enable API Gateway Service**
    - AI EasyMaker RAG uses the NHN Cloud API Gateway service to create and manage API endpoints. To use RAG functionality, you must enable the API Gateway service.
    - For more details and pricing information about the API Gateway service, see:
        - [API Gateway Service Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/ko/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Basic Settings**
    - **Name**: Enter the RAG name. RAG names cannot be duplicated.
    - **Description**: Enter a description for the RAG.
    - **Instance Type**: Select the instance type to run the RAG endpoint.
    - **Number of Instances**: Enter the number of instances to run the RAG endpoint.
    - **Prompt**: The prompt to be used by the RAG endpoint. Click **View Content** to see the full content of the prompt.
- **Vector Store Settings**
    - **Vector Store Type**: Select the vector store type.
        - **RDS for PostgreSQL**
            - **Enable RDS for PostgreSQL**
                - AI EasyMaker RAG uses NHN Cloud RDS for PostgreSQL to create and manage vector stores. If you select this option, you must enable RDS for PostgreSQL.
                - For more details and pricing information about RDS for PostgreSQL, see:
                    - [RDS for PostgreSQL Guide](https://docs.nhncloud.com/en/Database/RDS%20for%20PostgreSQL/ko/overview/)
                    - [RDS for PostgreSQL Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Database&s=RDS%20for%20PostgreSQL)
            - **Instance Type**: Select the instance type to use for RDS for PostgreSQL.
            - **Storage Type**: Select the storage type to use for RDS for PostgreSQL.
            - **Storage Size**: The storage size to use for RDS for PostgreSQL.
            - **User ID**: Enter the user ID to use for PostgreSQL access.
            - **Password**: Enter the password to use for PostgreSQL access.
            - **Password Confirmation**: Re-enter the password to confirm.
            - **VPC ID**: Enter the VPC ID to use for RDS for PostgreSQL.
            - **Subnet ID**: Enter the subnet ID to use for RDS for PostgreSQL.
        - **PostgreSQL Instance**: Use a user-created NHN Cloud PostgreSQL Instance as a vector store.
            - **User ID**: Enter the user ID that can access the PostgreSQL Instance.
            - **Password**: Enter the password that can access the PostgreSQL Instance.
            - **VPC ID**: Enter the VPC ID of the PostgreSQL Instance.
            - **Subnet ID**: Enter the subnet ID of the PostgreSQL Instance.
            - **PostgreSQL Instance IP**: Enter the IP address of the PostgreSQL Instance.
    - **Ingestion Settings**
        - **Data Path**: Enter the data path where documents to be ingested into the vector store are stored.
    - **Embedding Model**
        - **Model**: Select the embedding model to use when vectorizing documents and queries.
        - **Instance Type**: The instance type to run the embedding model.
        - **Number of Instances**: Enter the number of instances to run the embedding model.
- **LLM Settings**
    - **Model**: Select the LLM to use when generating responses.
    - **Instance Type**: The instance type to run the LLM.
    - **Number of Instances**: The number of instances to run the LLM.
- **Additional Settings**
    - **Log Management**: Logs generated during RAG execution can be saved to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    The format, size, and number of files that can be used for ingestion may be limited. For more details, see [Ingestion Sync](#rag.ingestion.sync).

!!! danger "Caution"
    When using PostgreSQL Instance, set the port to `15432`.
    For how to create an instance, see [PostgreSQL Instance](https://docs.nhncloud.com/en/Compute/Instance/ko/component-guide/#postgresql-instance).
    Configure the security group to allow access to port `15432` from the instance's subnet range.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="rag.list"></a>

### RAG List

View and manage the list of created RAGs. Select a RAG from the list to view detailed information.

- **Status**: RAG status. See the table below for major statuses.

| Status | Description |
| --- | --- |
| CREATE REQUESTED | RAG creation has been requested. |
| CREATE IN PROGRESS | RAG creation is in progress. |
| ACTIVE | RAG is operating normally. |
| UPDATE IN PROGRESS | RAG ingestion is in progress. |
| DELETE IN PROGRESS | RAG deletion is in progress. |
| CREATE FAILED | RAG creation failed.<br/>Delete the RAG and create it again. If creation failures persist, contact customer support. |
| UPDATE FAILED | RAG ingestion failed.<br/>Try **Ingestion Sync** again. If update failures persist, contact customer support. |
| DELETE FAILED | RAG deletion failed.<br/>Try deletion again. If deletion failures persist, contact customer support. |

- **API Gateway Status**: Deployment status information for the API Gateway default stage.

| Status | Description |
| --- | --- |
| DEPLOYING | API Gateway default stage is being deployed. |
| COMPLETE | API Gateway default stage has been successfully deployed and activated. |
| FAILURE | API Gateway default stage deployment failed. |

- **Ingestion History**: In the **Ingestion History** tab of the detail screen displayed when selecting a RAG, you can check the execution history of document ingestion tasks.
- **API Statistics**: In the **API Statistics** tab of the detail screen displayed when selecting a RAG, you can check API statistics information.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when selecting a RAG, you can check the list of monitoring target instances and basic metrics charts.

<a id="rag.ingestion.sync"></a>

### Ingestion Sync

- The ingestion sync function is available in the **Vector Store** tab of the detail screen displayed when selecting a RAG.
- When documents are added, deleted, or modified in the ingestion data path, you can execute **Ingestion Sync** to reflect the changes.
- The format, size, and number of files that can be used for ingestion may be limited. See the table below for details.

| Item | Limit |
|-----|------|
| Total file size | 100GB |
| Maximum number of files | 1,000,000 files |

| Category | Supported Formats | Maximum File Size |
|--------|---------|------------|
| Text documents | `.txt`, `.text`, `.md` | 3MB |
| Documents | `.doc`, `.docx`, `.pdf` | 50MB |
| Spreadsheets | `.csv`, `.xls`, `.xlsx` | 3MB |
| Presentations | `.ppt`, `.pptx` | 50MB |

<a id="rag.delete"></a>

### Delete RAG

- RAGs that are in the process of creation or deletion cannot be deleted.
- Requested deletion tasks cannot be canceled.

<a id="rag.query.request.guide"></a>

### RAG Query Request Guide

- When requesting a query, include `model` and `messages` in the request body like the OpenAI Chat Completion API. Use the RAG name as the `model` value.
- See the examples below for detailed request examples.

<details>
<summary><strong>Call Example (cURL)</strong></summary>

```bash
curl -X POST https://{API endpoint address}/rag/v1/query \
  -H "Content-Type: application/json" \
  -d '{
    "model": "{RAG name}",
    "messages": [
      {
        "role": "user",
        "content": "{query_text}"
      }
    ]
  }'
```

</details>

<details>
<summary><strong>Streaming Call Example (cURL)</strong></summary>

```bash
#!/bin/bash
set -euo pipefail

DEFAULT_URL="https://{API endpoint address}/rag/v1/query"
DEFAULT_MODEL="{RAG name}"
DEFAULT_PROMPT="Please describe the AI EasyMaker service."

usage() {
  cat <<'EOF'
Usage:
  <file name> -k <API_KEY> [-u URL] [-m MODEL] [-p PROMPT]

Options:
  -k   API key (sent as x-nhn-apikey: <API_KEY> header)
  -u   Call URL
  -m   Model name
  -p   User prompt
  -h   Help

Description:
  - Performs stream=true call with OpenAI compatible specification,
    and sequentially records only choices[].delta.content of each
    chunk delivered via streaming to standard output.

Required tools:
  - curl, jq
EOF
}

API_KEY=""
URL="$DEFAULT_URL"
MODEL="$DEFAULT_MODEL"
PROMPT="$DEFAULT_PROMPT"

while getopts ":k:u:m:p:h" opt; do
  case "$opt" in
    k) API_KEY="$OPTARG" ;;
    u) URL="$OPTARG" ;;
    m) MODEL="$OPTARG" ;;
    p) PROMPT="$OPTARG" ;;
    h) usage; exit 0 ;;
    \?) echo "Unknown option: -$OPTARG" >&2; usage; exit 2 ;;
    :) echo "Option -$OPTARG requires a value." >&2; usage; exit 2 ;;
  esac
done

if ! command -v curl >/dev/null 2>&1; then
  echo "Error: curl is required." >&2
  exit 1
fi
if ! command -v jq >/dev/null 2>&1; then
  echo "Error: jq is required." >&2
  exit 1
fi

# Create JSON Payload (OpenAI Chat Completions compatible format)
payload="$(jq -n \
  --arg model "$MODEL" \
  --arg prompt "$PROMPT" \
  '{
    model: $model,
    messages: [ { role: "user", content: $prompt } ],
    stream: true
  }'
)"

headers=( -H "Content-Type: application/json" )
if [[ -n "$API_KEY" ]]; then
  headers+=( -H "x-nhn-apikey: $API_KEY" )
fi

echo "Request URL: $URL" >&2
echo "Model: $MODEL" >&2
echo "---------------- Streaming Start ----------------" >&2

# Streaming processing: Extract only delta.content from data: {json} lines
curl -sS -N -X POST "$URL" "${headers[@]}" --data-raw "$payload" \
| while IFS= read -r line; do
    [[ -z "$line" ]] && continue
    if [[ "$line" == "data: [DONE]"* ]]; then
      break
    fi
    if [[ "$line" == data:* ]]; then
      json="${line#data: }"
      # There may be multiple choices, so output all
      # delta.content may not exist, so handle as empty
      while IFS= read -r piece; do
        printf "%s" "$piece"
      done < <(printf '%s\n' "$json" | jq -r '.choices[]?.delta?.content // empty')
    fi
  done

echo
echo "---------------- Streaming End ----------------" >&2
```

</details>

<a id="appendix"></a>

## Appendix

<a id="appendix.1.object.storage.account.permission"></a>

### 1. Add AI EasyMaker System Account Permissions to NHN Cloud Object Storage

When using the user's NHN Cloud Object Storage as input/output storage in some functions of AI EasyMaker,
you must allow read or write permissions for the AI EasyMaker system account in your NHN Cloud Object Storage container for normal function operation.

Allowing the AI EasyMaker system account read/write permissions in your NHN Cloud Object Storage container means that the AI EasyMaker system account can read or write files according to the granted permissions for all files in your NHN Cloud Object Storage container.

You must confirm this content and set access policies for your Object Storage with only the necessary accounts and permissions.

The 'user' is responsible for all consequences arising from allowing access to the user's Object Storage for accounts other than the AI EasyMaker system account during the access policy setting process, and AI EasyMaker is not responsible for this.

!!! tip "Note"
    The files that AI EasyMaker accesses to read or write in Object Storage according to function are as follows:

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

To add read/write permissions for the AI EasyMaker system account to NHN Cloud Object Storage, refer to the following:

1. Click **[Training]** or **[Model]** tab > **AI EasyMaker System Account Information**.
2. Save the AI EasyMaker system account information: **AI EasyMaker Tenant ID** and **AI EasyMaker API User ID**.
3. Go to the NHN Cloud Object Storage console.
4. Refer to the [Allow read/write access to specific projects or specific users](https://docs.nhncloud.com/en/Storage/Object%20Storage/ko/acl-guide/#role-based-access-allow-rw-project-or-user) document to add the necessary read and write permissions for the AI EasyMaker system account in the NHN Cloud Object Storage console.

<a id="appendix.2.lncs.service.usage.guide.and.log.inquiry.guide"></a>

### 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Query Methods

<a id="appendix.2.lncs.service.usage.guide"></a>

#### NHN Cloud Log & Crash Search Service Usage Guide

Logs and events generated from the AI EasyMaker service can be stored in the NHN Cloud Log & Crash Search service.
To store logs in the Log & Crash Search service, you must enable the Log & Crash service, and separate usage fees will be charged.

- **Log & Crash Search Service Usage and Pricing Information**
    - For more details and pricing on the Log & Crash Search service, see the following:
        - [Log & Crash Search Service Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/Overview/)
        - [Log & Crash Search Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Data%20%26%20Analytics&s=Log%20%26%20Crash%20Search)

<a id="appendix.2.lncs.service.log.inquiry.guide"></a>

#### Log Query

1. Navigate to the Log & Crash Search service console page.
2. Enter search conditions in the Log & Crash Search service to query logs.
    - AI EasyMaker training log query: Query logs where the category field is "easymaker.training".
        - Query: category:"easymaker.training"
    - AI EasyMaker endpoint log query: Query logs where the category field is "easymaker.inference".
        - Query: category:"easymaker.inference"
    - AI EasyMaker complete log query: Query logs where the logType field is "NHNCloud-AIEasyMaker".
        - Query: logType:"NHNCloud\-AIEasyMaker"
3. For detailed usage methods of the Log & Crash Search service, see [Log & Crash Search Service Console Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/console-guide/).

The AI EasyMaker service sends logs to the Log & Crash Search service with fields defined as follows:

- **Common Log Fields**

    | Name            | Description                      | Valid Range                             |
    | --------------- | -------------------------------- | --------------------------------------- |
    | easymakerAppKey | AI EasyMaker Appkey              | -                                       |
    | category        | Log category                     | easymaker.training, easymaker.inference |
    | logLevel        | Log level                        | INFO, WARNING, ERROR                    |
    | body            | Log content                      | -                                       |
    | logType         | Log providing service name       | NHNCloud-AIEasyMaker                    |
    | time            | Log occurrence time (UTC time)   | -                                       |

- **Training Log Fields**

    | Name       | Description              |
    | ---------- | ------------------------ |
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
    | modelName       | Inference target model name     |

- **Batch Inference Log Fields**

    | Name             | Description                   |
    | ---------------- | ----------------------------- |
    | batchInferenceId | AI EasyMaker batch inference ID |

<a id="appendix.3.hyperparameter"></a>

### 3. Hyperparameters

- Key-Value format values entered through the console.
- When executing the entry point, they are passed as execution arguments (--{Key}).
- They are also stored as environment variable values (EM*HP*{Key converted to uppercase}) and can be utilized.

As shown in the example below, you can utilize the hyperparameter values entered when creating training.<br>
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

- Information required for training is passed to the training container as **environment variables**, and the **training script** can utilize the passed environment variables.
- Environment variable names created from user input are converted to uppercase.
- In the code, the trained model must be saved to the EM_MODEL_DIR path.
- **Key Environment Variables**

    | Environment Variable Name                      | Description                                                                        |
    |-----------------------------| --------------------------------------------------------------------------- |
    | EM_SOURCE_DIR               | Absolute path of the folder where the algorithm script entered during training creation is downloaded  |
    | EM_ENTRY_POINT              | Name of the algorithm entry point entered during training creation                             |
    | EM_DATASET_${Dataset Name}     | Absolute path of the folder where each dataset entered during training creation is downloaded |
    | EM_DATASETS                 | Complete dataset list (JSON format)                                            |
    | EM_MODEL_DIR                | Model save path                                                              |
    | EM_CHECKPOINT_INPUT_DIR     | Input checkpoint save path                                                  |
    | EM_CHECKPOINT_DIR           | Output checkpoint save path                                                  |
    | EM_HP_${Hyperparameter Key Converted to Uppercase} | Hyperparameter value corresponding to the hyperparameter key                              |
    | EM_HPS                      | Complete hyperparameter list (JSON format)                                         |
    | EM_TENSORBOARD_LOG_DIR      | TensorBoard log path for checking training results                                    |
    | EM_REGION                   | Current region information                                                              |
    | EM_APPKEY                   | Appkey of the AI EasyMaker service currently in use                                   |

- **Example Code Using Environment Variables**

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

### 5. Saving Metric Logs for TensorBoard Usage

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
    TensorBoard metric logs are stored for 120 days. Metric logs older than 120 days are automatically deleted.

<a id="appendix.6.framework.training.settings"></a>

### 6. Distributed Training Settings by Framework

- **Tensorflow**
    - The environment variable `TF_CONFIG` required for distributed training is automatically set. For more details, see the [Tensorflow official guide documentation](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy).
- **Pytorch**
    - `Backends` configuration is required for distributed training. Set it to gloo for CPU-based distributed training or nccl for GPU-based distributed training. For more details, see the [Pytorch official guide documentation](https://pytorch.org/docs/stable/distributed.html).

<a id="appendix.7.cluster.upgrade"></a>

### 7. Cluster Version Upgrade

AI EasyMaker service periodically upgrades cluster versions to provide stable services and new features.
When a new cluster version is deployed, notebooks and endpoints running on the old version cluster must be migrated to the new cluster.
This section provides migration methods for each resource type to the new cluster.

<a id="appendix.7.cluster.upgrade.notebook"></a>

#### Notebook Cluster Version Upgrade

In the **Notebook** list screen, notebooks that need to be migrated to the new cluster display a **Restart** button to the left of their name.
When you hover the mouse pointer over the **Restart** button, restart guidance and expiration date/time are displayed.

- Before expiration, make sure to check the following precautions before clicking the **Restart** button:
    - When restarting, data stored in data storage (/root/easymaker directory path) is preserved as-is.
    - When executing a restart, data stored in boot storage is initialized and may be lost. Move data to data storage before restarting.

The restart takes approximately 25 minutes on first execution, and approximately 10 minutes thereafter.
If the restart fails, it is automatically reported to the administrator.

<a id="appendix.7.cluster.upgrade.endpoint"></a>

#### Endpoint Cluster Version Upgrade

In the **Endpoint List** screen, endpoints that need to be migrated to the new cluster display a **! Notice** message to the left of their name.
When you hover the mouse pointer over the **! Notice** message, version upgrade guidance and expiration date/time are displayed.
Before expiration, stages operating on the old version cluster must be migrated to the new version cluster according to the following guidance.

<a id="appendix.7.cluster.upgrade.endpoint.stage"></a>

##### Cluster Version Upgrade for General Stages

1. Delete general stages that are not default stages. Before deletion, first check if the stage is in service.
2. Create the stage again.
3. When the new stage becomes ACTIVE, verify that API calls and inference responses are received normally through the stage endpoint.

!!! danger "Caution"
    When a stage is deleted, the endpoint terminates and API calls are not possible. Before deletion, verify that the stage is not in service.

<a id="appendix.7.cluster.upgrade.endpoint.default.stage"></a>

##### Cluster Version Upgrade for Default Stage

The default stage is the stage where actual services operate.
To migrate the default stage's cluster version without service interruption, follow the guide below.

1. Create a new stage to replace the default stage of the old version cluster.
2. Verify that API calls and inference responses are received normally from the new stage endpoint.
3. Click the **Change Default Stage** button. Select the new stage and change it to the default stage.
4. When the change is complete, the new stage is set as the default stage, and the existing default stage is deleted.

<a id="appendix.8.torchrun.usage"></a>

### 8. How to use torchrun

- The code is written to enable distributed training in PyTorch. When you input the number of distributed nodes and the number of processes per node, distributed training using distributed nodes and multi-processes with torchrun will be performed.
- Training and hyperparameter tuning may fail due to memory shortage caused by factors such as the total number of processes, model size, input data size, and batch size. When failing due to memory shortage, the following error message may appear. However, not all instances of this message indicate memory shortage failures. Set an appropriate instance type according to memory usage.

```plaintext
exit code : -9 (pid: {pid})
```

- For more details on torchrun, see the [PyTorch official guide documentation](https://pytorch.org/docs/stable/elastic/run.html).

<a id="appendix.9.resource.info"></a>

### 9. Resource Information

When creating batch inference and endpoints in AI EasyMaker, resources are allocated excluding the default usage from the selected instance type.
Since the required resources vary depending on the request volume and complexity of the model, carefully set the number of pods and resource allocation along with an appropriate instance type.

Batch inference divides the actual usage by the number of pods to allocate resources to each pod. For endpoints, the input allocation cannot exceed the actual usage of the instance, so check resource usage in advance.
Note that both batch inference and endpoints may fail to be created if the allocated resources are less than the minimum usage required for inference.

<a id="appendix.10.endpoint.api.specification"></a>

### 10. Endpoint API Specification

The AI EasyMaker service provides endpoints based on the OIP (Open Inference Protocol) specification.
For detailed information on the OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

| Name                          | Method | API Path                                                                |
| ----------------------------- | ------ | ----------------------------------------------------------------------- |
| Model List                    | GET    | /{model_name}/v1/models                                                 |
| Model Ready                   | GET    | /{model_name}/v1/models/{model_name}                                    |
| Inference                     | POST   | /{model_name}/v1/models/{model_name}/predict                            |
| Explain                       | POST   | /{model_name}/v1/models/{model_name}/explain                            |
| Server Information            | GET    | /{model_name}/v2                                                        |
| Server Live                   | GET    | /{model_name}/v2/health/live                                            |
| Server Ready                  | GET    | /{model_name}/v2/health/ready                                           |
| Model Information             | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]       |
| Model Ready                   | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/ready |
| Inference                     | POST   | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/infer |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/completions                                     |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/chat/completions                                |

!!! tip "Note"
    OpenAI generative model inference is used when using generative models such as OpenAI's GPT-4o.
    Input values required for inference must be entered according to OpenAI's API specification. For more details, see [OpenAI API Documentation](https://platform.openai.com/docs/api-reference/chat).
    For models that support the Completion and Chat Completion APIs provided by AI EasyMaker, check [Model endpoint compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility).

<a id="appendix.11.framework.note"></a>

### 11. Framework-specific Serving Notes

<a id="appendix.11.framework.note.tensorflow.framework"></a>

#### TensorFlow Framework

TensorFlow model serving provided by AI EasyMaker uses SavedModel(.pb), which is recommended by TensorFlow.
To use checkpoints, save the checkpoint variables directory stored as SavedModel in the model directory, and it will be used for model serving.
Reference: [https://www.tensorflow.org/guide/saved_model](https://www.tensorflow.org/guide/saved_model)

<a id="appendix.11.framework.note.pytorch.framework"></a>

#### PyTorch Framework

AI EasyMaker serves PyTorch models(.mar) with TorchServe.
It is recommended to use MAR files created using model-archiver, and serving with weight files is also possible but requires additional files along with the weight files.
Check the table below and the [model-archiver documentation](https://github.com/pytorch/serve/blob/master/model-archiver/README.md) for required files and detailed descriptions.

| File Name                    | Required | Description                                                              |
| ---------------------------- | -------- | ------------------------------------------------------------------------ |
| model.py                     | Required | Model structure file passed as model-file parameter.                    |
| handler.py                   | Required | File passed as handler parameter to process inference logic.             |
| weight file(.pt, .pth, .bin) | Required | File that stores the model's weights and structure.                      |
| requirements.txt             | Optional | File for installing Python packages required for serving.               |
| extra/                       | Optional | Files in the directory are passed as extra-files parameter.             |

!!! danger "Caution"
    There are differences in request format between using TorchServe directly and using AI EasyMaker serving, so be careful when writing handler.py.
    Check the values passed in the handler.py example below and write your handler accordingly.

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

AI EasyMaker serves Scikit-learn models(.joblib) with mlserver.
The `model-settings.json` required when using mlserver directly is not needed when using AI EasyMaker serving.

<a id="appendix.11.framework.note.hugging.face.framework"></a>

#### Hugging Face Framework

Hugging Face models can be served using the runtime provided by AI EasyMaker, or through TensorFlow Serving and TorchServe.

<a id="appendix.11.framework.note.hugging.face.framework.runtime"></a>

##### Hugging Face Runtime

This is a convenient way to serve Hugging Face models.
Hugging Face runtime serving does not support fine-tuning. To serve fine-tuned models, use the TensorFlow/PyTorch serving method.

1. Check the model to serve on Hugging Face.
2. Copy the Hugging Face model ID.
3. Select the Hugging Face framework on the AI EasyMaker model creation page and enter the Hugging Face model ID.
4. Enter the required input values according to the model to create the model.
5. Check the created model and create an endpoint.

!!! tip "Note"
    Currently, Hugging Face runtime does not support all Tasks from Hugging Face.
    Supported Tasks are `sequence_classification`, `token_classification`, `fill_mask`, `text_generation`, `text2text_generation`.
    To use unsupported Tasks, use the TensorFlow/PyTorch serving method.

!!! tip "Note"
    To serve a Gated Model, you must enter a token from an account with allowed access as a model parameter.
    If you don't enter a token or enter a token from an unauthorized account, model deployment will fail.

<a id="appendix.11.framework.note.hugging.face.framework.tensorflow.pytorch.serving"></a>

##### TensorFlow/PyTorch Serving

This is a method to serve Hugging Face models trained with TensorFlow and PyTorch.

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
    - If fine-tuning is required, you can write your own code for training following the [Hugging Face Fine-tuning Guide](https://huggingface.co/docs/transformers/main/ko/training).
        - For more details on AI EasyMaker training, see [Training](#training).

2. Check the Hugging Face model information and create files required for serving.
    - Save the model in the format required for serving by each framework.
    - For details, check the reference notes for TensorFlow and PyTorch frameworks.
3. Upload the model files to OBS or NAS.
4. For subsequent processes, see the [Create Model](#model.create) and [Create Endpoint](#endpoint.create) guides.