## AI Service > AI EasyMaker > Console Guide

This document explains the usage of the console for AI EasyMaker.

## Algorithm

You can check, create, modify, and delete algorithms. 

### Algorithm List

You can check the registered algorithms and their details. Each algorithm provides basic information, input schema, and output schema.

![algorithm_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/algorithm/algorithm_list.png)

### Create Algorithm

You can create an algorithm by entering the following information:

![create_algorithm.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/algorithm/create_algorithm.png)

**Basic Information**

* **Algorithm Name**: Enter the algorithm name.
* **Algorithm Description**: Enter the algorithm description.
* **Stage**: Select the stage to register the algorithm. You can select from training, preprocessing, and inference.

**Algorithm Information**

* **Framework**: Select the framework. You can select from TensorFlow, PyTorch, etc.
* **Framework Version**: Enter the framework version.
* **Python Version**: Enter the Python version.
* **Algorithm Image**: Enter the algorithm image URI. You must enter the full path of the container registry URL.
* **Dockerfile URI**: Enter the Dockerfile URI. If not entered, the default Dockerfile provided by AI EasyMaker is used.
* **Source Code URI**: Enter the source code URI. You must enter the full path including the source code file name.
* **Entry Point**: Enter the entry point. It is the command to be executed when the algorithm is run.
* **Instance Type**: Select the instance type to be used when running the algorithm.

**Schema Information**

* **Input Schema**: Enter the input schema as JSON format. It defines the algorithm input. (Refer to [Input/Output Schema Guide](./algorithm-guide/#_2))
* **Output Schema**: Enter the output schema as JSON format. It defines the algorithm output. (Refer to [Input/Output Schema Guide](./algorithm-guide/#_2))
* **Hyperparameter Schema**: Enter the hyperparameter schema as JSON format. It defines the hyperparameters of the algorithm. (Refer to [Hyperparameter Schema Guide](./algorithm-guide/#_3))

> [Caution]
> When creating an algorithm, the following conditions must be met:
> * Algorithm name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.
> * Source code URI must be Object Storage URI or a publicly accessible URL.
> * Dockerfile URI must be Object Storage URI or a publicly accessible URL.
> * All schemas must be entered in JSON format.

### Modify Algorithm

You can modify algorithm information by clicking the **Modify** button from the algorithm list.

![modify_algorithm.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/algorithm/modify_algorithm.png)

> [Note]
> When modifying an algorithm, you cannot change the algorithm name and stage.

### Delete Algorithm

You can delete an algorithm by clicking the **Delete** button from the algorithm list.

> [Caution]
> Algorithms that are being used by experiments cannot be deleted.

## Experiment

You can create, modify, delete, copy, and run training experiments.

### Experiment List

You can check the registered experiments and their details.

![experiment_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/experiment_list.png)

### Create Experiment

You can create an experiment by entering the following information:

![create_experiment.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/create_experiment.png)

**Basic Information**

* **Experiment Name**: Enter the experiment name.
* **Experiment Description**: Enter the experiment description.

**Algorithm Information**

* **Algorithm**: Select the algorithm to be used for the experiment.
* **Entry Point**: It is automatically filled in based on the selected algorithm. You can modify it if necessary.
* **Hyperparameters**: Enter hyperparameters in JSON format. The hyperparameter schema defined in the algorithm is displayed as a guide.

**Data Information**

* **Input Data**: Select the data to be used for training. Select from the created datasets.
* **Data Path**: Select the path of the data to be used. You can select file or directory.

**Training Information**

* **Instance Type**: Select the instance type to be used for training.
* **Instance Count**: Enter the number of instances to be used for training.
* **Maximum Runtime**: Enter the maximum runtime for training (minutes).
* **Storage Size**: Enter the storage size required for training (GB).

**Output Information**

* **Training Output**: Enter the path where training results will be saved. The results are saved in NHN Cloud Object Storage.

> [Caution]
> When creating an experiment, the following conditions must be met:
> * Experiment name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.
> * Training output path must be Object Storage URI format.
> * Maximum runtime must be between 1 and 259200 minutes (180 days).

### Run Experiment

You can run an experiment by clicking the **Run** button from the experiment list.

![run_experiment.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/run_experiment.png)

### Experiment Details

You can check experiment details by clicking an experiment from the experiment list.

![experiment_detail.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/experiment_detail.png)

The experiment details page provides the following information:

* **Basic Information**: Experiment name, description, creation date, status, etc.
* **Algorithm Information**: Algorithm name, entry point, hyperparameters, etc.
* **Data Information**: Input data, data path, etc.
* **Training Information**: Instance type, instance count, maximum runtime, storage size, etc.
* **Output Information**: Training output path, etc.
* **Log**: Training logs are displayed in real-time.

### Modify Experiment

You can modify experiment information by clicking the **Modify** button from the experiment details page.

![modify_experiment.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/modify_experiment.png)

> [Note]
> Running experiments cannot be modified.

### Copy Experiment

You can copy an experiment by clicking the **Copy** button from the experiment list.

![copy_experiment.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/experiment/copy_experiment.png)

### Delete Experiment

You can delete an experiment by clicking the **Delete** button from the experiment list.

> [Caution]
> Running experiments cannot be deleted.

## Training

You can check training logs and status.

### Training List

You can check the training list and their status.

![training_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/training/training_list.png)

### Training Details

You can check training details by clicking a training from the training list.

![training_detail.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/training/training_detail.png)

The training details page provides the following information:

* **Basic Information**: Training name, status, creation date, start date, end date, etc.
* **Algorithm Information**: Algorithm name, entry point, hyperparameters, etc.
* **Data Information**: Input data, data path, etc.
* **Training Information**: Instance type, instance count, maximum runtime, storage size, etc.
* **Output Information**: Training output path, etc.
* **Log**: Training logs are displayed.

### Stop Training

You can stop running training by clicking the **Stop** button from the training details page.

## Model

You can check, create, modify, and delete models.

### Model List

You can check the registered models and their details.

![model_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/model/model_list.png)

### Create Model

You can create a model by entering the following information:

![create_model.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/model/create_model.png)

**Basic Information**

* **Model Name**: Enter the model name.
* **Model Description**: Enter the model description.

**Algorithm Information**

* **Algorithm**: Select the algorithm to be used for the model.
* **Entry Point**: It is automatically filled in based on the selected algorithm. You can modify it if necessary.

**Model Information**

* **Model Path**: Enter the path where the model is saved. You must enter Object Storage URI.
* **Instance Type**: Select the instance type to be used when the model is deployed.

> [Caution]
> When creating a model, the following conditions must be met:
> * Model name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.
> * Model path must be Object Storage URI format.

### Modify Model

You can modify model information by clicking the **Modify** button from the model list.

![modify_model.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/model/modify_model.png)

> [Note]
> When modifying a model, you cannot change the model name.

### Delete Model

You can delete a model by clicking the **Delete** button from the model list.

> [Caution]
> Models that are being used by endpoints cannot be deleted.

## Endpoint

You can create, modify, delete, and deploy endpoints.

### Endpoint List

You can check the registered endpoints and their details.

![endpoint_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/endpoint_list.png)

### Create Endpoint

You can create an endpoint by entering the following information:

![create_endpoint.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/create_endpoint.png)

**Basic Information**

* **Endpoint Name**: Enter the endpoint name.
* **Endpoint Description**: Enter the endpoint description.

**Stage Information**

* **Stage Name**: Enter the stage name.
* **Model**: Select the model to be used for the endpoint.
* **Resource Information**: Enter the resource information required for deployment.
  * **Instance Type**: Select the instance type to be used for deployment.
  * **Instance Count**: Enter the number of instances to be used for deployment.
  * **Node Connection Information**: Select the node connection information. You can select public or private.

> [Caution]
> When creating an endpoint, the following conditions must be met:
> * Endpoint name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.
> * Stage name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.

### Deploy Endpoint

You can deploy an endpoint by clicking the **Deploy** button from the endpoint list.

![deploy_endpoint.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/deploy_endpoint.png)

### Endpoint Details

You can check endpoint details by clicking an endpoint from the endpoint list.

![endpoint_detail.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/endpoint_detail.png)

The endpoint details page provides the following information:

* **Basic Information**: Endpoint name, description, creation date, status, etc.
* **Stage Information**: Stage name, model name, resource information, endpoint URI, etc.
* **Monitoring**: Various metrics for the deployed endpoint are displayed.

### Add Stage

You can add a stage by clicking the **Add Stage** button from the endpoint details page.

![add_stage.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/add_stage.png)

### Modify Endpoint

You can modify endpoint information by clicking the **Modify** button from the endpoint details page.

![modify_endpoint.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/endpoint/modify_endpoint.png)

> [Note]
> When modifying an endpoint, you cannot change the endpoint name.

### Delete Endpoint

You can delete an endpoint by clicking the **Delete** button from the endpoint list.

> [Caution]
> Deployed endpoints cannot be deleted. You must undeploy them first.

## Notebook

You can create, start, stop, and delete notebooks.

### Notebook List

You can check the created notebooks and their details.

![notebook_list.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/notebook/notebook_list.png)

### Create Notebook

You can create a notebook by entering the following information:

![create_notebook.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/notebook/create_notebook.png)

**Basic Information**

* **Notebook Name**: Enter the notebook name.
* **Notebook Description**: Enter the notebook description.

**Notebook Information**

* **Notebook Image**: Select the notebook image. Various images such as TensorFlow, PyTorch, etc. are provided.
* **Instance Type**: Select the instance type to be used for the notebook.
* **Storage Size**: Enter the storage size required for the notebook (GB).
* **Storage Type**: Select the storage type. You can select HDD or SSD.

> [Caution]
> When creating a notebook, the following conditions must be met:
> * Notebook name: Can contain only English letters, numbers, and hyphens (-), and must be 1-50 characters long.
> * Storage size must be between 10 and 1024 GB.

### Start Notebook

You can start a notebook by clicking the **Start** button from the notebook list.

![start_notebook.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/notebook/start_notebook.png)

### Stop Notebook

You can stop a running notebook by clicking the **Stop** button from the notebook list.

### Access Notebook

You can access a running notebook by clicking the **Open** button from the notebook list.

![access_notebook.png](https://static.toastoven.net/prod_ai_easymaker/console_guide/en/notebook/access_notebook.png)

### Delete Notebook

You can delete a notebook by clicking the **Delete** button from the notebook list.

> [Caution]
> Running notebooks cannot be deleted. You must stop them first.

## Machine Learning > AI EasyMaker > Console User Guide

<a id="dashboard"></a>

## Dashboard

You can check the usage status of all AI EasyMaker resources on the dashboard.

<a id="dashboard.service.usage.status"></a>

### Service Usage Status

Displays the number of resources in use by resource type.

- Notebook: Number of notebooks in ACTIVE (HEALTHY) status in use
- Training: Number of training jobs that are COMPLETE
- Hyperparameter Tuning: Number of hyperparameter tuning jobs that are COMPLETE
- Endpoint: Number of endpoints in ACTIVE status

<a id="dashboard.service.monitoring"></a>

### Service Monitoring

- Displays the top 3 endpoints with the highest API calls.
- When you select an endpoint, you can check the API success/failure total metrics for the sub-endpoint stages.

<a id="dashboard.resource.usage"></a>

### Resource Usage

- You can check the resources with the highest usage by CPU and GPU core type.
- When you hover over the metrics, resource information is displayed.

<a id="notebook"></a>

## Notebook

Create and manage Jupyter notebooks with essential packages installed for machine learning development.

<a id="notebook.create"></a>

### Create Notebook

Create a Jupyter notebook.

- **Image**: Select the OS image to be installed on the notebook instance.
    - **Core Type**: The CPU and GPU core type of the image is displayed.
    - **Framework**: The framework installed on the image is displayed.
        - TENSORFLOW: Image with TensorFlow deep learning framework installed.
        - PYTORCH: Image with PyTorch deep learning framework installed.
        - PYTHON: Image with only Python language installed without deep learning framework.
    - **Framework Version**: The version of the framework installed on the image is displayed.
    - **Python Version**: The Python version installed on the image is displayed.

- **Notebook Information**
    - Enter the name and description of the notebook.
    - Select the instance type for the notebook. The instance specifications are selected according to the chosen type.

- **Storage**
    - Specify the boot storage and data storage size for the notebook.
        - Boot storage is where the Jupyter notebook and default virtual environment are installed. This storage is initialized when the notebook is restarted.
        - Data storage is block storage mounted to the `/root/easymaker` directory path. Data in this storage is preserved even when the notebook is restarted.
    - The storage size of a created notebook cannot be changed, so you must specify sufficient storage size when creating it.
    - If needed, you can connect **NHN Cloud NAS** to the notebook.
        - Mount Directory Name: Enter the name of the directory to mount on the notebook.
        - NHN Cloud NAS Path: Enter the directory path in the format `nas://{NAS ID}:/{path}`.

!!! tip "Note"
    Notebook creation may take several minutes.
    When creating resources for the first time, it takes additional minutes to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="notebook.list"></a>

### Notebook List

The notebook list is displayed. Select a notebook from the list to view details and modify information.

- **Name**: The notebook name is displayed. You can change the name by clicking **Change** on the detail screen.
- **Status**: The status of the notebook is displayed. See the table below for key statuses.

    | Status             | Description                                                                                                                                           |
    | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Notebook creation has been requested.                                                                                                                 |
    | CREATE IN PROGRESS | The notebook instance is being created.                                                                                                               |
    | ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                                         |
    | ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists after restarting the notebook, contact customer support.                |
    | STOP IN PROGRESS   | The notebook is being stopped.                                                                                                                        |
    | STOPPED            | The notebook has been stopped.                                                                                                                        |
    | START IN PROGRESS  | The notebook is being started.                                                                                                                        |
    | REBOOT IN PROGRESS | The notebook is being rebooted.                                                                                                                       |
    | DELETE IN PROGRESS | The notebook is being deleted.                                                                                                                        |
    | CREATE FAILED      | Notebook creation has failed. If creation continues to fail, contact customer support.                                                              |
    | STOP FAILED        | Notebook stop has failed. Please try again.                                                                                                          |
    | START FAILED       | Notebook start has failed. Please try again.                                                                                                         |
    | REBOOT FAILED      | Notebook reboot has failed. Please try again.                                                                                                        |
    | DELETE FAILED      | Notebook deletion has failed. Please try again.                                                                                                      |

- **Actions > Open Jupyter Notebook**: Clicking the **Open Jupyter Notebook** button opens the notebook in a new browser window. The notebook is only accessible to users logged into the console.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select a notebook, you can check the list of monitoring target instances and basic metrics charts.
    - The **Monitoring** tab is disabled when the notebook is being created or when there are ongoing tasks.

<a id="notebook.user.virtual.run.environment.configuration"></a>

### User Virtual Runtime Environment Configuration

AI EasyMaker notebook instances provide a default Conda virtual environment with various libraries and kernels required for machine learning.
The default Conda virtual environment is initialized and runs when the notebook is stopped and started, but virtual environments and external libraries installed by users in arbitrary paths are not automatically initialized and will not be preserved when the notebook is stopped and started.
To solve this problem, you must create a virtual environment in the `/root/easymaker/custom-conda-envs` directory path and install external libraries in the created virtual environment.
AI EasyMaker notebook instances support initialization and operation of virtual environments created in the `/root/easymaker/custom-conda-envs` directory path when notebooks are stopped and started.

Follow the guide below to configure your user virtual environment.

1. Click **Open Jupyter Notebook** > **Jupyter Notebook > Launcher > Terminal** from the console notebook menu.
2. Navigate to the `/root/easymaker/custom-conda-envs` path.

        cd /root/easymaker/custom-conda-envs

3. To create a virtual environment named `easymaker_env` with Python 3.8, execute the `conda create` command as follows.

        conda create --prefix ./easymaker_env python=3.8

4. The created virtual environment can be verified with the `conda env list` command.

        (base) root@nb-xxxxxx-0:~# conda env list
        # conda environments:
        #
                                /opt/intel/oneapi/intelpython/latest
                                /opt/intel/oneapi/intelpython/latest/envs/2022.2.1
        base                *   /opt/miniconda3
        easymaker_env           /root/easymaker/custom-conda-envs/easymaker_env

<a id="notebook.user.script"></a>

### User Scripts

Scripts that need to be executed automatically when the notebook is stopped and started can be registered in the `/root/easymaker/cont-init.d` path.
They are executed in ascending order according to alphanumeric order.

- Script location and permissions
    - Only files located in the `/root/easymaker/cont-init.d` path are executed.
    - Only scripts with execution permissions are executed.
- Script content
    - The first line of the script must start with `#!`.
    - Scripts are executed with root privileges.
- Script execution records are stored in the following locations.
    - Script exit code: `/root/easymaker/cont-init.d/{SCRIPT}.exitcode`
    - Script standard output and standard error stream: `/root/easymaker/cont-init.d/{SCRIPT}.output`
    - Full execution log: `/root/easymaker/cont-init.output`

<a id="notebook.stop"></a>

### Stop Notebook

Stop a running notebook or start a stopped notebook.

1. Select the notebook you want to start or stop from the notebook list.
2. Click **Start Notebook** or **Stop Notebook**.
3. The requested action cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    Starting and stopping notebooks may take several minutes.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be initialized when stopping and starting notebooks.
    To maintain virtual environments and external libraries when stopping and starting notebooks, configure user virtual environments by referring to [User Virtual Runtime Environment Configuration](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.instance.type.change"></a>

### Change Notebook Instance Type

Change the instance type of a created notebook.
The instance type you want to change can only be changed to an instance type with the same core type as the existing instance.

1. Select the notebook whose instance type you want to change.
2. If the notebook is in a running state (ACTIVE), click **Stop Notebook** to stop the notebook.
3. Click **Change Instance Type**.
4. Select the instance type you want to change to and click Confirm.

!!! tip "Note"
    Changing instance type may take several minutes.

<a id="notebook.reboot"></a>

### Reboot Notebook

If problems occur while using the notebook, or if the status is normal (ACTIVE) but the notebook is not accessible,
you can reboot the notebook.

1. Select the notebook you want to reboot.
2. Click **Reboot Notebook**.
3. The requested deletion action cannot be canceled. Click **Confirm** to continue.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be initialized when rebooting notebooks.
    To maintain virtual environments and external libraries when rebooting notebooks, configure user virtual environments by referring to [User Virtual Runtime Environment Configuration](#notebook.user.virtual.run.environment.configuration).

<a id="notebook.delete"></a>

### Delete Notebook

Delete a created notebook.

1. Select the notebook you want to delete from the list.
2. Click **Delete Notebook**.
3. The requested deletion action cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    When deleting a notebook, both boot storage and data storage are deleted.
    Connected NHN Cloud NAS is not deleted and must be individually deleted in **NHN Cloud NAS**.

<a id="experiment"></a>

## Experiment

Experiments manage related training by grouping them into experiments.

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

- **Status**: The experiment status is displayed. See the table below for key statuses.

    | Status             | Description                                               |
    | ------------------ | --------------------------------------------------------- |
    | CREATE REQUESTED   | The experiment creation has been requested.              |
    | CREATE IN PROGRESS | The experiment is being created.                         |
    | CREATE FAILED      | The experiment creation has failed. Please try again.    |
    | ACTIVE             | The experiment has been created successfully.            |

- **Actions**
    - Clicking **Go to TensorBoard** opens TensorBoard in a new browser window, where you can view statistical information for training included in the experiment. TensorBoard can only be accessed by users logged into the console.
    - **Retry**: If the experiment status is failed, click **Retry** to recover the experiment.
- **Training**: When you select training, the **Training** tab in the detail screen that appears displays a list of training included in the experiment.

<a id="experiment.delete"></a>

### Delete Experiment

Delete an experiment.

1. Select the experiment to delete.
2. Click **Delete Experiment**. You cannot delete an experiment if it is in the process of being created.
3. The requested deletion operation cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    You cannot delete an experiment if there are associated pipeline schedules, or if there are training, hyperparameter tuning, or pipeline executions being created.
    Delete the resources associated with the experiment before deleting the experiment.
    Associated resources can be viewed in the bottom detail screen that appears when you click the experiment you want to delete.

<a id="training"></a>

## Training

Provides an environment to train machine learning algorithms and check training results through statistics.

<a id="training.create"></a>

### Create Training

Set up the environment where training will be performed by selecting the instance and OS image for training, and proceed with training by entering algorithm information and input/output data paths.

- **Training Template**: To set up training information by loading a training template, select 'Use' and then select the training template to load.
- **Basic Information**: Select basic information about training and the experiment that will include the training.
    - **Training Name**: Enter the training name.
    - **Training Description**: Enter a description.
    - **Experiment**: Select the experiment that will include the training. Experiments group related trainings. If no experiments have been created, click **Add** to create an experiment.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information about the provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select an algorithm.
            - **Hyperparameters**: Enter hyperparameter values required for training. For detailed information about hyperparameters for each algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use algorithms written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the NHN Cloud Object Storage path where the algorithm is stored.<br>
                    - Enter the directory path in the format obs://{Object Storage API Endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, set permissions by referring to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission). Model creation will fail if the necessary permissions are not set.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is stored. <br>
                    Enter the directory path in the format nas://{NAS ID}:/{path}.

            - **Entry Point**
                - The entry point is the entry point of algorithm execution where training starts. Write the entry point filename.
                - The entry point file must exist in the algorithm path.
                - If you write **requirements.txt** in the same path, Python packages required by the script will be installed.
            - **Hyperparameters**
                - To add parameters for training, click the **+ button** to enter parameters in Key-Value format. You can enter up to 100 parameters.
                - The entered hyperparameters are input as execution arguments when the entry point is executed. For detailed usage methods, see [Appendix > 3. Hyperparameters](#appendix.3.hyperparameter).

- **Image**: Select the instance image according to the environment where training should be executed.

- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to execute training.
    - **Number of Distributed Nodes**: Enter the number of nodes to perform distributed training. Distributed training can be enabled through settings in the algorithm code. For details, see [Appendix > 6. Distributed Training Settings by Framework](#appendix.6.framework.training.settings).
    - **Use torchrun**: Select whether to use torchrun supported by the Pytorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. Using torchrun enables distributed training by running multiple processes on one node. The number of processes affects memory usage.
- **Input Data**
    - **Data Set**: Enter the data set to execute training. Up to 10 data sets can be configured.
        - Data Set Name: Enter the data set name.
        - Data Path: Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to proceed with training from a saved checkpoint, enter the storage path of the checkpoint.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save training execution results.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides checkpoints, enter the storage path for checkpoints.
        - Created checkpoints can be used when resuming training from previous training.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance to execute training.
        - Used only when using NHN Cloud Object Storage. It should be specified with sufficient size to store all data required for training.
    - **Maximum Training Time**: Specify the maximum waiting time until training is completed. Training that exceeds the maximum waiting time will be terminated.
    - **Log Management**: Logs generated during training can be stored in the NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - If input data is deleted before training is completed, training may fail.

<a id="training.list"></a>

### Training List

The training list is displayed. When you select a training from the list, you can check detailed information and change information.

- **Training Time**: The time training has progressed is displayed.
- **Status**: The status of training is displayed. See the table below for major statuses.

    | Status                                       | Description                                                                                                                      |
    | -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                             | Training creation has been requested.                                                                                            |
    | CREATE IN PROGRESS                           | Resources required for training are being created.                                                                               |
    | RUNNING                                      | Training is in progress.                                                                                                         |
    | STOPPED                                      | Training has been stopped by user request.                                                                                      |
    | COMPLETE                                     | Training has been completed normally.                                                                                            |
    | STOP IN PROGRESS                             | Training is being stopped.                                                                                                       |
    | FAIL TRAIN                                   | Training failed during progress. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                | Training creation failed. If creation continues to fail, contact customer support.                                              |
    | FAIL TRAIN IN PROGRESS, COMPLETE IN PROGRESS | Resources used for training are being cleaned up.                                                                               |

- **Actions**
    - **Go to TensorBoard**: TensorBoard where you can check statistical information of training opens in a new browser window.<br/>
        For how to create TensorBoard logs, see [Appendix > 5. Storing Metric Logs for TensorBoard Usage](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Training**: You can stop training in progress.

- **Hyperparameters**: In the **Hyperparameters** tab of the detail screen displayed when you select training, you can check the hyperparameter values set for training.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select training, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when training is in creation status.

<a id="training.copy"></a>

### Copy Training

Create new training with the same settings as existing training.

1. Select the training you want to copy.
2. Click **Copy Training**.
3. The training creation screen is displayed with the same settings as the existing training.
4. If there is information you want to change, modify it and then click **Create Training** to create the training.

<a id="training.model.create"></a>

### Create Model from Training

Create a model from training in completed status.

1. Select the training you want to create as a model.
2. Click **Create Model**. Only training in COMPLETE status can be created as a model.
3. You will be moved to the model creation page. After checking the content, click **Create Model** to create the model. For detailed information about model creation, see the [Model](#model) document.

<a id="training.delete"></a>

### Delete Training

Delete training.

1. Select the training you want to delete.
2. Click **Delete Training**. Training in progress can be deleted after stopping.
3. The requested deletion operation cannot be canceled. Click **Confirm** to proceed.

!!! tip "Good to Know"
    If there is a model created from the training you want to delete, the training cannot be deleted. Delete the model first, then delete the training.

<a id="hyperparameter.tuning"></a>

## Hyperparameter Tuning

Hyperparameter tuning is the process of optimizing hyperparameter values to maximize the predictive accuracy of a model. If this feature is not used, you would need to manually adjust hyperparameters by running many training jobs yourself to find optimal values.

<a id="hyperparameter.tuning.create"></a>

### Create Hyperparameter Tuning

How to configure a hyperparameter tuning job.

- **Training Template**
    - **Use**: Select whether to use a training template. Using a training template automatically fills in some configuration values for hyperparameter tuning with predefined values.
    - **Training Template**: Select the training template to use for automatically entering some configuration values for hyperparameter tuning.
- **Basic Information**
    - **Hyperparameter Tuning Name**: Enter the name of the hyperparameter tuning job.
    - **Description**: Enter a description for the hyperparameter tuning job if needed.
    - **Experiment**: Select the experiment that will contain the hyperparameter tuning. Experiments group related hyperparameter tuning. If no experiments have been created, click **Add** to create an experiment.
- **Tuning Strategy**
    - **Strategy Name**: Select which strategy to use to find optimal hyperparameters.
    - **Random Seed**: Determines random number generation. Specify a fixed value for reproducible results.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information about the provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select an algorithm.
            - **Hyperparameter Spec**: Enter the range of hyperparameter values to use for hyperparameter tuning. For detailed information about hyperparameters for each algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
                - **Name**: Define which hyperparameter to tune. This is predetermined for each algorithm.
                - **Type**: Select the data type of the hyperparameter. This is predetermined for each algorithm.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determine the step size for hyperparameter value changes when using the "Grid" tuning strategy.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use an algorithm written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the NHN Cloud Object Storage path where the algorithm is stored.
                    - Enter the directory path in the format obs://{Object Storage API Endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, set permissions by referring to [Appendix > 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission). If you don't set the required permissions, model creation will fail.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is stored.
                    - Enter the directory path in the format nas://{NAS ID}:/{path}.
            - **Entry Point**
                - The entry point is the entry point for algorithm execution where training begins. Write the entry point file name.
                - The entry point file must exist in the algorithm path.
                - If you create **requirements.txt** in the same path, the Python packages required by the script will be installed.
            - **Hyperparameter Spec**
                - **Name**: Define which hyperparameter to tune.
                - **Type**: Select the data type of the hyperparameter.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determine the step size for hyperparameter value changes when using the "Grid" tuning strategy.
                    - **Comma-separated values**: Tune hyperparameters using static values (e.g., sgd, adam).
- **Image**: Select the instance image according to the environment where training should be executed.
- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to run training on.
    - **Number of Training Instances**: The number of instances to perform training on. Number of training instances = 'number of distributed nodes x number of parallel training'.
    - **Number of Distributed Nodes**: Enter the number of nodes to perform distributed training on. Distributed training can be enabled through configuration in the algorithm code. For details, see [Appendix > 6. Distributed Training Settings by Framework](#appendix.6.framework.training.settings).
    - **Number of Parallel Training**: Enter the number of training sessions to run simultaneously in parallel.
    - **Use torchrun**: Select whether to use torchrun supported by the PyTorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. Using torchrun enables distributed training by running multiple processes on one node. The number of processes affects memory usage.
- **Input Data**
    - **Dataset**: Enter the dataset to run training on. Up to 10 datasets can be configured.
        - Dataset Name: Enter the dataset name.
        - Data Path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to continue training from a saved checkpoint, enter the checkpoint's storage path.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save training execution results.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides checkpoints, enter the checkpoint storage path.
        - Generated checkpoints can be used to resume training from previous training sessions.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Metrics**
    - **Metric Name**: Define which metrics to collect from the logs output by the training code.
    - **Metric Format**: Enter the regular expression to use for collecting metrics. The training algorithm must output metrics matching the regular expression.
- **Objective Metric**
    - **Metric Name**: Select which metric is the target for optimization.
    - **Objective Metric Type**: Select the optimization type.
    - **Target Value**: The tuning job ends when the objective metric reaches this value.
- **Tuning Resource Configuration**
    - **Maximum Number of Failed Training**: Define the maximum number of failed training sessions. When the number of failed training sessions reaches this value, tuning ends with failure.
    - **Maximum Number of Training**: Define the maximum number of training sessions. Tuning runs until the number of automatically executed training sessions reaches this value.
- **Early Stopping**
    - **Name**: End training early if the model no longer improves even if training continues.
    - **Minimum Number of Training**: Define from how many training sessions to get objective metric values when calculating the median.
    - **Start Step**: Set from which training step to apply early stopping.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size for instances that will run training.
        - Only used when using NHN Cloud Object Storage. Must be specified with sufficient size to store all data required for training.
    - **Maximum Progress Time**: Specify the maximum progress time until training is completed. Training that exceeds the maximum progress time will be terminated.
    - **Log Management**: Logs generated during training progress can be stored in the NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before training is completed may cause training to fail.

<a id="hyperparameter.tuning.list"></a>

### Hyperparameter Tuning List

The list of hyperparameter tuning is displayed. Selecting a hyperparameter tuning from the list allows you to view detailed information and modify information.

- **Duration**: Displays the time taken for hyperparameter tuning.
- **Completed Training**: Indicates the number of completed training sessions among the training sessions automatically generated by hyperparameter tuning.
- **Training in Progress**: Indicates the number of training sessions in progress.
- **Failed Training**: Indicates the number of failed training sessions.
- **Best Training**: Indicates the objective metric information of the training with the best objective metric value among the training sessions automatically generated by hyperparameter tuning.
- **Status**: The status of hyperparameter tuning is displayed. Refer to the table below for key statuses.

    | Status                                                                           | Description                                                                                                                                              |
    | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                                                 | The state where hyperparameter tuning creation has been requested.                                                                                      |
    | CREATE IN PROGRESS                                                               | The state where resources needed for hyperparameter tuning are being created.                                                                           |
    | RUNNING                                                                          | The state where hyperparameter tuning is in progress.                                                                                                   |
    | STOPPED                                                                          | The state where hyperparameter tuning has been stopped by user request.                                                                                 |
    | COMPLETE                                                                         | The state where hyperparameter tuning has completed normally.                                                                                           |
    | STOP IN PROGRESS                                                                 | The state where hyperparameter tuning is being stopped.                                                                                                 |
    | FAIL HYPERPARAMETER TUNING                                                       | The state where hyperparameter tuning failed during progress. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                                                    | The state where hyperparameter tuning creation failed. If creation continues to fail, please contact customer support.                                |
    | FAIL HYPERPARAMETER TUNING IN PROGRESS, COMPLETE IN PROGRESS, STOP IN PROGRESS | The state where resources used for hyperparameter tuning are being cleaned up.                                                                          |

- **Status Details**: The content in parentheses for `COMPLETE` status is detailed status information. Refer to the table below for key detailed information.

    | Detailed Information | Description                                                                                                    |
    | -------------------- | -------------------------------------------------------------------------------------------------------------- |
    | GoalReached          | Detailed information when hyperparameter tuning training has completed after reaching the target value.       |
    | MaxTrialsReached     | Detailed information when hyperparameter tuning has completed after reaching the maximum number of training.  |
    | SuggestionEndReached | Detailed information when the hyperparameter tuning search algorithm has explored all hyperparameters.        |

- **Actions**
    - **TensorBoard Shortcut**: TensorBoard for checking training statistics information opens in a new browser window.<br/>
        For how to log TensorBoard logs, see [Appendix > 5. Storing Metric Logs for TensorBoard Utilization](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Hyperparameter Tuning**: You can stop hyperparameter tuning in progress.

- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when you select hyperparameter tuning, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled while hyperparameter tuning is being created.

<a id="hyperparameter.tuning.training.list"></a>

### Training List from Hyperparameter Tuning

The list of training sessions automatically generated by hyperparameter tuning is displayed. Selecting a training session from the list allows you to view detailed information.

- **Objective Metric Value**: Indicates the objective metric value.
- **Status**: The status of training automatically generated by hyperparameter tuning is displayed. Refer to the table below for key statuses.

    | Status              | Description                                                                                                                                    |
    | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATED             | The state where training has been created.                                                                                                    |
    | RUNNING             | The state where training is in progress.                                                                                                      |
    | SUCCEEDED           | The state where training has completed normally.                                                                                              |
    | KILLED              | The state where training has been stopped by the system.                                                                                      |
    | FAILED              | The state where training failed during progress. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | METRICS_UNAVAILABLE | The state where objective metrics cannot be collected.                                                                                        |
    | EARLY_STOPPED       | The state where training was stopped early because performance (objective metrics) did not improve during progress.                          |

<a id="hyperparameter.tuning.copy"></a>

### Copy Hyperparameter Tuning

Create new hyperparameter tuning with the same settings as existing hyperparameter tuning.

1. Select the hyperparameter tuning you want to copy.
2. Click **Copy Hyperparameter Tuning**.
3. The hyperparameter tuning creation screen is displayed with the same settings as the existing hyperparameter tuning.
4. If there is information you want to change, modify it and click **Create Hyperparameter Tuning** to create the hyperparameter tuning.

<a id="hyperparameter.tuning.model.create"></a>

### Create Model from Hyperparameter Tuning

Create a model from the best training of completed hyperparameter tuning.

1. Select the hyperparameter tuning you want to create as a model.
2. Click **Create Model**. Only hyperparameter tuning in COMPLETE status can be created as a model.
3. You are moved to the model creation page. After reviewing the content, click **Create Model** to create the model.
   For details about model creation, see the [Model](#model) document.

<a id="hyperparameter.tuning.delete"></a>

### Delete Hyperparameter Tuning

Delete hyperparameter tuning.

1. Select the hyperparameter tuning you want to delete.
2. Click **Delete Hyperparameter Tuning**. Hyperparameter tuning in progress can be deleted after stopping.
3. The requested delete operation cannot be canceled. Click **Confirm** to continue.

!!! tip "Note"
    If models created from the hyperparameter tuning you want to delete exist, you cannot delete the hyperparameter tuning. Delete the models first, then delete the hyperparameter tuning.

<a id="training.template"></a>

## Training Template

By creating training templates in advance, you can retrieve the values entered in the template when creating training or hyperparameter tuning.

<a id="training.template.create"></a>

### Create Training Template

For information that can be set in training templates, see [Create Training](#training.create).

<a id="training.template.list"></a>

### Training Template List

The training template list is displayed. Select a training template from the list to view details and modify information.

- **Actions**
    - **Modify**: You can modify training template information.
- **Hyperparameters**: On the **Hyperparameters** tab of the detail screen displayed when you select a training template, you can check the hyperparameter names set in the training template.

<a id="training.template.copy"></a>

### Copy Training Template

Creates a new training template with the same settings as an existing training template.

1. Select the training template you want to copy.
2. Click **Copy Training Template**.
3. The training template creation screen is displayed with the same settings as the existing training template.
4. If there is any information you want to change, modify the settings and click **Create Training Template** to create the training template.

<a id="training.template.delete"></a>

### Delete Training Template

Deletes a training template.

1. Select the training template you want to delete.
2. Click **Delete Training Template**.
3. The requested deletion operation cannot be canceled. To continue, click **Confirm**.

<a id="model"></a>

## Model

Models from AI EasyMaker training results or external models can be managed as artifacts.

<a id="model.create"></a>

### Create Model

- **Basic Information**: Enter the basic information of the model.
    - **Name**: Enter the model name.
        - If the model framework type is PyTorch, you must enter a model name that is identical to the PyTorch model name.
    - **Description**: Enter the model description.
- **Framework Information**: Enter the framework information of the model.
    - **Framework**: Select the framework of the model.
    - **Framework Version**: Enter the version of the model framework.
- **Model Information**: Enter the storage where the model artifacts are stored.
    - **Model Artifact**: Select the storage where the model artifacts are stored.
        - **NHN Cloud Object Storage**: Enter the Object Storage path where the model artifacts are stored.
            - Enter the directory path in the format `obs://{Object Storage API Endpoint}/{containerName}/{path}`.
            - When using NHN Cloud Object Storage, refer to [Appendix > 1. Add AI EasyMaker System Account Permission to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to set permissions. If permissions are not set, model creation will fail due to inability to access model artifacts.
        - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the model artifacts are stored.
            - Enter the directory path in the format `nas://{NAS ID}:/{path}`.
    - **Parameters**: Enter the parameter information of the model.
        - **Parameter Name**: Enter the parameter name of the model.
        - **Parameter Value**: Enter the parameter value of the model.

!!! tip "Note"
    Values entered as model parameters are used when serving the model. Parameters can be used as arguments and environment variables.
    Arguments are used exactly as entered parameter names, while environment variables are used with parameter names converted to screaming snake case.

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
    When creating TensorFlow (Triton), PyTorch (Triton), ONNX (Triton) models, the model artifact path you enter must contain model files and `config.pbtxt` files stored in a structure that allows the model to be executed with Triton.
    Please refer to the example below.
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

The model list is displayed. Selecting a model from the list allows you to view detailed information and modify the information.

- **Name**: The model name and description are displayed. The model name and description can be changed by clicking **Change**.
- **Model Artifact Path**: The storage where the model artifacts are stored is displayed.
- **Status**: The status of the model is displayed. Please refer to the table below for key statuses.

    | Status             | Description                                                                                      |
    | ------------------ | ------------------------------------------------------------------------------------------------ |
    | CREATE REQUESTED   | The model creation has been requested.                                                           |
    | CREATE IN PROGRESS | Resources required for the model are being created.                                             |
    | DELETE IN PROGRESS | The model is being deleted.                                                                      |
    | ACTIVE             | The model has been created successfully.                                                         |
    | CREATE FAILED      | Model creation has failed. If creation continues to fail, please contact customer support.     |
    | DELETE FAILED      | Model deletion has failed. Please try again.                                                    |

- **Training Name**: For models created from training, the name of the underlying training is displayed.
- **Training ID**: For models created from training, the ID of the underlying training is displayed.
- **Framework**: The framework information of the model is displayed.
- **Parameters**: The parameters of the model are displayed. Parameters are used for inference.

<a id="model.endpoint.create"></a>

### Create Endpoint from Model

Creates an endpoint that can serve the selected model.

1. Select the model you want to create as an endpoint from the list.
2. Click **Create Endpoint**.
3. You will be redirected to the **Create Endpoint** page. After reviewing the content, click **Create Endpoint**.
   For more details on endpoint creation, see the [Endpoint](#endpoint) documentation.

<a id="model.batch.inference.create"></a>

### Create Batch Inference from Model

Creates batch inference that can perform batch inference with the selected model and view inference results as statistics.

1. Select the model you want to create for batch inference from the list.
2. Click **Create Batch Inference**.
3. You will be redirected to the **Create Batch Inference** page. After reviewing the content, click **Create Batch Inference**.
   For more details on batch inference creation, see the [Batch Inference](#batch.inference) documentation.

<a id="model.delete"></a>

### Delete Model

Deletes the model.

1. Select the model you want to delete from the list.
2. Click **Delete Model**.
3. The requested deletion operation cannot be canceled. To proceed, click **Confirm**.

!!! tip "Note"
    If there are endpoints created from the model you want to delete, the model cannot be deleted.
    To delete it, first delete the endpoints created from that model, then delete the model.

<a id="model.evaluation"></a>

## Model Evaluation

Measure model performance and compare performance between multiple models.

<a id="model.evaluation.create"></a>

### Create Model Evaluation

Batch inference is automatically generated during the model evaluation process.

- **Basic Information**: Enter basic information for the model evaluation.
    - **Name**: Enter the model evaluation name.
    - **Description**: Enter the model evaluation description.
- **Model Information**: Enter information for the model to be evaluated.
    - **Model**: Select the model to evaluate. Only classification and regression models are supported.
    - **Class Name**: Enter the class name of the model.
- **Model Evaluation Instance Information**
    - **Instance Type**: Select the instance type to run the model evaluation. Used for data preprocessing and evaluation computation tasks.
- **Input Data**: Input data is used to compare predictions generated through batch inference with ground truth. Fields used for inference and ground truth fields are required.
    - **Data Path**: Enter the path where input data is located.
        - **Input Data Format**: Select the format of the input data. CSV and JSONL formats are supported, with file extensions .csv and .jsonl respectively.
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
    - **Maximum Progress Time**: Specify the maximum progress time until model evaluation is completed. Model evaluations exceeding the maximum progress time will be terminated.
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
- **Model**: The name of the model used in the model evaluation is displayed.
- **Status**: The status of the model evaluation is displayed. Refer to the table below for key statuses.

    | Status                                                   | Description                                                                          |
    |----------------------------------------------------------|------------------------------------------------------------------------------------|
    | CREATE REQUESTED                                         | Model evaluation creation has been requested.                                       |
    | CREATE IN PROGRESS                                       | Model evaluation is being created.                                                  |
    | CREATE FAILED                                            | Model evaluation creation has failed. Please try again.                             |
    | RUNNING                                                  | Model evaluation is in progress.                                                    |
    | COMPLETE IN PROGRESS, FAIL MODEL EVALUATION IN PROGRESS | Resources used for model evaluation are being cleaned up.                           |
    | COMPLETE                                                 | Model evaluation has completed successfully.                                         |
    | STOP IN PROGRESS                                         | Model evaluation is being stopped.                                                  |
    | STOPPED                                                  | Model evaluation has been stopped by user request.                                  |
    | FAIL MODEL EVALUATION                                    | Model evaluation has failed. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | DELETE IN PROGRESS                                       | Model evaluation is being deleted.                                                  |

- **Actions**
    - **Stop**: You can stop an ongoing model evaluation.

<a id="model.evaluation.classification.metric"></a>

### Classification Model Evaluation Metrics

- **PR AUC**: Area under the Precision-Recall (PR) curve. Effective for measuring classification performance on imbalanced datasets.
- **ROC AUC**: Area under the ROC curve (Recall-False Positive Rate). The closer to 1, the better the performance.
- **Log Loss**: Loss value calculated using logarithmic function for the difference between predicted probabilities and actual answers. Lower values mean the model's predictions are more reliable.
- **F1 Score**: Harmonic mean of precision and recall. Useful when there is class imbalance, and closer to 1 is better.
- **Precision**: Ratio of actual positives among predictions made as positive. Focuses on reducing False Positives.
- **Recall**: Ratio of actual positives that the model correctly predicted as positive. Important for reducing False Negatives.
- **Precision-Recall Curve**: A curve visualizing the relationship between precision and recall at various thresholds. Refer to this when adjusting model thresholds.
- **ROC Curve**: Shows the relationship between recall and false positive rate at various thresholds. Used for setting classification thresholds or comparing models.
- **Precision-Recall Curve by Threshold**: A graph showing how precision and recall change at specific thresholds. Referred to when setting actual operational criteria.
- **Confusion Matrix**: A matrix that categorizes prediction results into four types: TP, FP, FN, TN. Makes it easy to identify error types by class.

<a id="model.evaluation.regression.metric"></a>

### Regression Model Evaluation Metrics

- **MAE (Mean Absolute Error)**: Average of absolute differences between actual and predicted values. Intuitively shows the magnitude of prediction errors.
- **MAPE (Mean Absolute Percentage Error)**: Average of ratios obtained by dividing prediction errors by actual values. Being ratio-based, it may be inappropriate for data with values close to 0.
- **R-squared (Coefficient of Determination)**: Indicates how well the model explains actual data, with values closer to 1 showing higher explanatory power.
- **RMSE (Root Mean Squared Error)**: Square root of the mean squared error. More sensitive to large errors and allows interpretation of results on the same scale as actual units.
- **RMSLE (Root Mean Squared Logarithmic Error)**: Calculated from the difference between log-transformed actual and predicted values. Not sensitive to magnitude differences, useful for evaluating exponentially growing data.

<a id="model.evaluation.compare"></a>

### Model Evaluation Comparison

Compare evaluation metrics of multiple models.

1. Select the model evaluations you want to compare from the list.
2. Click **Compare**.

<a id="model.evaluation.delete"></a>

### Delete Model Evaluation

Delete a model evaluation.

1. Select the model evaluation you want to delete.
2. Click **Delete**. Ongoing model evaluations can be deleted after stopping.
3. The requested deletion operation cannot be canceled. Click **Confirm** to proceed.

<a id="endpoint"></a>

## Endpoint

Create and manage endpoints for model serving.

<a id="endpoint.create"></a>

### Create Endpoint

- **Enable API Gateway Service**
    - AI EasyMaker endpoints create API endpoints and manage APIs through the NHN Cloud API Gateway service. To use endpoint features, you must enable the API Gateway service.
    - For more details on the API Gateway service and pricing, see the following:
        - [API Gateway Service Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/en/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Endpoint**: Select whether to add a stage to a new or existing endpoint.
    - **Create New Endpoint**: Creates a new endpoint. The endpoint is created as a new service and default stage in API Gateway.
    - **Add New Stage to Existing Endpoint**: The endpoint is created as a new stage in the API Gateway service of an existing endpoint. Select an existing endpoint to add a stage to.
- **Endpoint Name**: Enter the endpoint name. Endpoint names must be unique.
- **Stage Name**: When adding a new stage to an existing endpoint, enter the new stage name. Stage names must be unique.
- **Description**: Enter the endpoint stage description.
- **Instance Information**: Enter the instance information where the model will be served.
    - **Instance Type**: Select the instance type.
    - **Number of Instances**: Enter the number of running instances.
    - **Autoscaler**: The autoscaler automatically adjusts the number of nodes based on resource usage policies. Autoscaler is configured per stage.
        - **Use/Don't Use**: Select whether to use the autoscaler. When enabled, the number of instances will scale in or out based on instance load.
        - **Minimum Number of Nodes**: Minimum number of nodes that can be scaled in
        - **Maximum Number of Nodes**: Maximum number of nodes that can be scaled out
        - **Scale-in**: Configure whether to enable node scale-in
        - **Resource Usage Threshold**: Reference value for the resource usage threshold range that serves as the criterion for scale-in
        - **Threshold Range Maintenance Time (minutes)**: Time to maintain resource usage below the threshold for nodes to become scale-in targets
        - **Scale-in Delay Time After Scale-out (minutes)**: Delay time from node scale-out until monitoring begins for scale-in target nodes
- **Stage Information**: Enter information about the model artifact to deploy to the endpoint. Deploying the same model to multiple stage resources distributes and processes requests.
    - **Model**: Select the model to deploy to the endpoint. If no model has been created, create a model first. For serving considerations by model framework, see [Appendix > 11. Framework-specific Serving Considerations](#appendix.11.framework.note).
    - **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance as a fixed ratio.
        - **CPU**: Enter CPU allocation. Enter this if you want to allocate directly without using allocation ratio (%).
        - **Memory**: Enter memory allocation. Enter this if you want to allocate directly without using allocation ratio (%).
        - **GPU**: Enter GPU allocation. Enter this if you want to allocate directly without using allocation ratio (%).
    - **Description**: Enter the stage resource description.
    - **Pod Autoscaler**: A feature that automatically adjusts the number of pods based on model request volume. Autoscaler is configured per model.
        - **Use/Don't Use**: Select whether to use the autoscaler. When enabled, the number of pods will scale in or out based on model load.
        - **Scale-out Unit**: Enter the pod scale-out unit.
            - **CPU**: The number of pods is adjusted based on CPU usage.
            - **Memory**: The number of pods is adjusted based on memory usage.
        - **Threshold Value**: The threshold value for each scale-out unit at which pods will be scaled out.
    - **Resource Information**: You can check the actual resources used. Allocates actual resource usage to each model based on the model's allocation. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).

!!! tip "Note"
    The AI EasyMaker service provides endpoints based on OIP (open inference protocol) specifications. For endpoint API specification details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
    To use a separate endpoint, refer to the resources created in the API Gateway service to create and use new resources.
    For more details on OIP specifications, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

!!! tip "Note"
    Endpoint creation may take several minutes.
    When creating resources for the first time, additional time may be required to configure the service environment.

!!! tip "Note"
    Creating a new endpoint creates a new API Gateway service.
    Adding a new stage to an existing endpoint creates a new stage in the API Gateway service.
    If the default quota of [API Gateway Service Resource Provision Policy](https://docs.nhncloud.com/en/nhncloud/en/resource-policy/#api-gateway) is exceeded, endpoint creation may not be possible in AI EasyMaker. This can be resolved by adjusting the API Gateway service resource quota.

<a id="endpoint.list"></a>

### Endpoint List

The endpoint list is displayed. Select an endpoint from the list to view detailed information and modify settings.

- **Default Stage URL**: Displays the URL of the default stage among the endpoint's stages.
- **Status**: The status of the endpoint. Refer to the table below for major statuses.

    | Status             | Description                                                                                                                               |
    | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Endpoint creation has been requested.                                                                                                     |
    | CREATE IN PROGRESS | Endpoint is being created.                                                                                                                |
    | UPDATE IN PROGRESS | Some stages of the endpoint have work in progress.<br/>You can check the work status of each stage in the endpoint stage list.         |
    | DELETE IN PROGRESS | Endpoint is being deleted.                                                                                                                |
    | ACTIVE             | Endpoint is running normally.                                                                                                             |
    | CREATE FAILED      | Endpoint creation has failed.<br/>You must delete the endpoint and create it again. If creation failure persists, contact customer support. |
    | UPDATE FAILED      | Some stages of the endpoint are not serving normally. You must delete the problematic stage and create it again.                        |

- **API Gateway Status**: Displays API Gateway status information for the endpoint's default stage. Refer to the table below for major statuses.

    | Status                         | Description                                                                                                                                                                                                                           |
    | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE IN PROGRESS             | API Gateway resources are being created.                                                                                                                                                                                             |
    | STAGE DEPLOYING                | API Gateway default stage is being deployed.                                                                                                                                                                                         |
    | ACTIVE                         | API Gateway default stage has been deployed normally and is active.                                                                                                                                                                  |
    | NOT FOUND: STAGE               | The default stage of the endpoint cannot be found.<br/>Check if the stage exists in the API Gateway console.<br/>If the stage has been deleted, the deleted API Gateway stage cannot be recovered, and you must delete the endpoint and create it again. |
    | NOT FOUND: STAGE DEPLOY RESULT | The deployment status of the endpoint's default stage cannot be found.<br/>Check if the default stage has been deployed in the API Gateway console.                                                                               |
    | STAGE DEPLOY FAIL              | API Gateway default stage deployment has failed.                                                                                                                                                                                     |

<a id="endpoint.stage.create"></a>

### Create Endpoint Stage

Add a new stage to an existing endpoint. Create a new stage to test it without affecting the default stage.

1. Click **Endpoint Name** in the endpoint list.
2. Click **+ Create Stage**.
3. Adding a new stage to an existing endpoint is automatically selected, and the configuration method is the same as endpoint creation.
4. The requested delete operation cannot be cancelled. To proceed, click **Confirm**.

<a id="endpoint.stage.list"></a>

### Endpoint Stage List

The list of stages created under the endpoint is displayed. Select a stage from the list to view detailed information.

- **Status**: Displays the status of the endpoint stage. Refer to the table below for major statuses.

    | Status             | Description                                                              |
    | ------------------ | ------------------------------------------------------------------------ |
    | CREATE REQUESTED   | Endpoint stage creation has been requested.                              |
    | CREATE IN PROGRESS | Endpoint stage is being created.                                         |
    | DEPLOY IN PROGRESS | Model is being deployed to the endpoint stage.                          |
    | DELETE IN PROGRESS | Endpoint stage is being deleted.                                         |
    | ACTIVE             | Endpoint stage is running normally.                                      |
    | CREATE FAILED      | Endpoint stage creation has failed. Try again.                          |
    | DEPLOY FAILED      | Endpoint stage deployment has failed. Try creating again.               |

- **API Gateway Status**: Displays the stage status of the API Gateway where the endpoint stage is deployed.
- **Stage Default Stage Status**: Shows whether it is the default stage.
- **Stage URL**: Displays the stage URL of the API Gateway where the model is served.
- **View API Gateway Settings**: To check the settings deployed by AI EasyMaker to the API Gateway stage, click **View Settings**.
- **View API Gateway Statistics**: To view API statistics for the endpoint, click **View Statistics**.
- **Instance Type**: Displays the endpoint instance type where the model is served.
- **Running Worker Nodes/Pods**: Displays the number of nodes and pods in use by the endpoint.
- **Stage Resources**: Displays information about model artifacts deployed to the stage.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when selecting an endpoint stage, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when the endpoint stage is being created.
- **API Statistics**: In the **API Statistics** tab of the detail screen displayed when selecting an endpoint stage, you can check API statistics information for the endpoint stage.
    - The **API Statistics** tab is disabled when the endpoint stage is being created.

!!! danger "Caution"
    When AI EasyMaker creates an endpoint or endpoint stage, it creates API Gateway services and stages for the endpoint.
    If you directly make changes to API Gateway services and stages created by AI EasyMaker in the API Gateway service console, please refer to the following precautions:

    1. Do not delete API Gateway services and stages created by AI EasyMaker. Deleting them may cause API Gateway information to not display properly in endpoints, and endpoint changes may not be applied to API Gateway.
    2. Do not change or delete resources in the API Gateway resource path entered during endpoint creation. Deleting them may cause endpoint inference API calls to fail.
    3. Do not add resources under the API Gateway resource path entered during endpoint creation. Added resources may be deleted during endpoint stage addition/modification operations.
    4. Do not disable **Backend Endpoint URL Override** set in the API Gateway resource path in the API Gateway stage settings, or change the URL. Changing it may cause endpoint inference API calls to fail.
       Other settings besides the above precautions can use features provided by API Gateway as needed.
       For detailed API Gateway usage, see [API Gateway Console Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/en/console-guide/).

!!! tip "Note"
    If AI EasyMaker endpoint stage settings are not deployed to the API Gateway stage due to temporary issues, it will be displayed as 'deployment failed' status.
    In this case, you can manually deploy the API Gateway stage by clicking Stage List > Select Stage > **View API Gateway Settings** in the bottom detail screen > **Deploy Stage**.
    If the deployment status is not recovered with the above guide, contact customer support.

<a id="endpoint.stage.resource.create"></a>

### Create Stage Resource

Add a new resource to an existing endpoint stage.

- **Model**: Select the model to deploy to the endpoint. If no model has been created, create a model first.
- **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the actual resource usage of the instance as a fixed ratio.
    - **CPU**: Enter CPU allocation. Enter this if you want to allocate directly without using allocation ratio (%).
    - **Memory**: Enter memory allocation. Enter this if you want to allocate directly without using allocation ratio (%).
- **Number of Pods**: Enter the number of pods for the stage resource.
- **Description**: Enter the stage resource description.
- **Pod Autoscaler**: A feature that automatically adjusts the number of pods based on model request volume. Autoscaler is configured per model.
    - **Use/Don't Use**: Select whether to use the autoscaler. When enabled, the number of pods will scale in or out based on model load.
    - **Scale-out Unit**: Enter the pod scale-out unit.
        - **CPU**: The number of pods is adjusted based on CPU usage.
        - **Memory**: The number of pods is adjusted based on memory usage.
    - **Threshold Value**: The threshold value for each scale-out unit at which pods will be scaled out.

<a id="endpoint.stage.resource.list"></a>

### Stage Resource List

The list of resources created under the endpoint stage is displayed.

- **Status**: Displays the status of the stage resource. Refer to the table below for major statuses.

    | Status             | Description                                               |
    | ------------------ | --------------------------------------------------------- |
    | CREATE REQUESTED   | Stage resource creation has been requested.              |
    | CREATE IN PROGRESS | Stage resource is being created.                         |
    | DELETE IN PROGRESS | Stage resource is being deleted.                         |
    | ACTIVE             | Stage resource has been deployed normally.               |
    | CREATE FAILED      | Stage resource creation has failed. Try again.          |

- **Model Name**: The name of the model deployed to the stage.
- **API Gateway Resource Path**: The inference URL of the model deployed to the stage. You can request inference to the displayed URL. For more details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
- **Number of Pods**: Displays the number of healthy pods and total pods in use by the resource.

<a id="endpoint.inference.call"></a>

### Endpoint Inference Call

1. Click a stage in **Endpoint** > **Endpoint Stage** to display the stage detail screen at the bottom.
2. Check the API Gateway resource path in the stage resource tab of the detail screen.
3. Call the API Gateway resource path with HTTP POST Method to invoke the inference API.
    - The request and response specifications of the inference API vary depending on the algorithm you wrote.

            // Inference API Example: Request
            curl --location --request POST '{API Gateway Resource Path}' \
            --header 'Content-Type: application/json' \
            --data-raw '{
                "instances": [
                    [6.8,  2.8,  4.8,  1.4],
                    [6.0,  3.4,  4.5,  1.6]
                ]
            }'

            // Inference API Example: Response
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
2. Click the endpoint stage where the stage resource to delete is deployed in the endpoint stage list. Clicking will display the stage detail screen at the bottom.
3. Select the stage resource to delete in the **Stage Resources** tab of the detail screen.
4. Click **Delete Stage Resource**.
5. The requested delete operation cannot be cancelled. To proceed, click **Confirm**.

<a id="endpoint.default.stage.change"></a>

### Change Endpoint Default Stage

Change the default stage of the endpoint to another stage.
To change the endpoint model without service interruption, AI EasyMaker recommends using stage functionality to deploy models.

1. Operate the stage actually running the service as the default stage.
2. When replacing with a new model, add a new stage to the existing endpoint.
3. Verify that there are no issues with the endpoint service using the replaced model in the new stage.
4. Click **Change Default Stage**.
5. Select the new stage to change to the default stage in Change Stage.
6. The change request operation cannot be cancelled. To proceed, click **Confirm**.
7. The stage to change becomes the default stage, and the resources of the existing default stage are automatically deleted.

<a id="endpoint.stage.delete"></a>

### Delete Endpoint Stage

1. Click **Endpoint Name** in the endpoint list to go to the endpoint stage list.
2. Select the endpoint stage to delete in the endpoint stage list. The default stage cannot be deleted.
3. Click **Delete Stage**.
4. The requested delete operation cannot be cancelled. To proceed, click **Confirm**.

!!! danger "Caution"
    When you delete an AI EasyMaker endpoint stage, the stage of the API Gateway service where the endpoint stage is deployed is also deleted.
    If there are APIs in operation in the API Gateway stage being deleted, API calls will fail, so be careful.

<a id="endpoint.delete"></a>

### Delete Endpoint

Delete the endpoint.

1. Select the endpoint to delete in the endpoint list.
2. If there are stages other than the default stage under the endpoint, you cannot delete the endpoint. First delete other stages, then delete the endpoint.
3. Click **Delete Endpoint**.
4. The requested delete operation cannot be cancelled. To proceed, click **Confirm**.

!!! danger "Caution"
    When you delete an AI EasyMaker endpoint, the API Gateway service where the endpoint is deployed is also deleted.
    If there are APIs in operation in the API Gateway service being deleted, API calls will fail, so be careful.

<a id="batch.inference"></a>

## Batch Inference

AI EasyMaker provides an environment where you can perform batch inference using models and check inference results through statistics.

<a id="batch.inference.create"></a>

### Create Batch Inference

Select instances and OS images to set up the environment where batch inference will be performed, and enter input/output data paths to proceed with batch inference.

- **Basic Information**: Enter basic information for batch inference.
    - **Batch Inference Name**: Enter the batch inference name.
    - **Batch Inference Description**: Enter the description.
- **Instance Information**
    - **Instance Type**: Select the instance type to run batch inference.
    - **Instance Count**: The number of instances to perform batch inference.
- **Model Information**
    - **Model**: Select the model for batch inference. If no model has been created, create a model first.
    - **Pod Count**: Enter the number of pods for the model.
    - **Resource Information**: You can check the resources actually used by the model. According to the entered pod count, the actual usage is divided and allocated to each pod. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).
- **Input Data**
    - **Data Path**: Enter the path of data to run batch inference.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Input Data Type**: Select the type of data to run batch inference.
        - **JSON**: Uses valid JSON data from files as input values.
        - **JSONL**: Uses JSON Lines files where each line consists of valid JSON as input values.
            - Reference: [https://jsonlines.org/](https://jsonlines.org/)
    - **Glob Pattern**
        - **Include File Specification**: Enter the file set to include in input data as a Glob pattern.
        - **Exclude File Specification**: Enter the file set to exclude from input data as a Glob pattern.
- **Output Data**
    - **Output Data**: Enter the data storage path to save batch inference execution results.
        - Enter NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Batch Options**
        - **Batch Size**: Enter the number of data samples processed simultaneously in one inference task.
        - **Inference Timeout (seconds)**: Enter the timeout for batch inference. You can set the maximum allowed time for a single inference request to be processed and results to be returned.
    - **Data Storage Size**: Enter the data storage size of the instance to run batch inference.
        - Used only when using NHN Cloud Object Storage. You must specify a sufficient size to store all data required for batch inference.
    - **Maximum Batch Inference Time**: Specify the maximum wait time until batch inference is completed. Batch inference that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during batch inference can be stored in NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    - When using Glob patterns, **exclude Glob patterns** are applied with priority.
    - **Batch size** and **inference timeout** must be set appropriately according to the performance of the model performing batch inference. If the entered configuration values are incorrect, batch inference may not achieve sufficient performance.

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - Deleting input data before batch inference is completed may cause batch inference to fail.
    - When using Glob patterns, if values are not entered appropriately, input data cannot be found and batch inference may not operate normally.

!!! danger "Caution"
    Batch inference using GPU instances allocates GPU instances according to the number of pods.
    If `pod count / GPU count` is not divisible as an integer, unallocated GPUs may occur.
    Since unallocated GPUs are not used for batch inference, set the pod count appropriately to use GPU instances efficiently.

<a id="batch.inference.list"></a>

### Batch Inference List

The batch inference list is displayed. Select a batch inference from the list to check detailed information and modify information.

- **Inference Duration**: The time batch inference has been running is displayed.
- **Status**: The status of batch inference is displayed. See the table below for key statuses.

    | Status                                                   | Description                                                                                                                                   |
    | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                       | Batch inference creation has been requested.                                                                                                    |
    | CREATE IN PROGRESS                                     | Resources required for batch inference are being created.                                                                                        |
    | RUNNING                                                | Batch inference is in progress.                                                                                                      |
    | STOPPED                                                | Batch inference has been stopped by user request.                                                                                       |
    | COMPLETE                                               | Batch inference has been completed normally.                                                                                              |
    | STOP IN PROGRESS                                       | Batch inference is being stopped.                                                                                                      |
    | FAIL BATCH INFERENCE                                   | Batch inference failed during processing. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | CREATE FAILED                                          | Batch inference creation failed. If creation continues to fail, contact customer support.                                              |
    | FAIL BATCH INFERENCE IN PROGRESS, COMPLETE IN PROGRESS | Resources used for batch inference are being cleaned up.                                                                                      |

- **Actions**
    - **Stop**: You can stop batch inference in progress.
- **Monitoring**: In the **Monitoring** tab of the detailed screen displayed when selecting batch inference, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when batch inference is in a creating state.

<a id="batch.inference.copy"></a>

### Copy Batch Inference

Create new batch inference with the same settings as existing batch inference.

1. Select the batch inference you want to copy.
2. Click **Copy Batch Inference**.
3. The batch inference creation screen appears with the same settings as the existing batch inference.
4. If there is information you want to change settings for, modify it and then click **Create Batch Inference** to create batch inference.

<a id="batch.inference.delete"></a>

### Delete Batch Inference

Delete batch inference.

1. Select the batch inference you want to delete.
2. Click **Delete Batch Inference**. Batch inference in progress can be deleted after stopping.
3. The requested deletion cannot be canceled. To continue, click **Confirm**.

<a id="personal.image"></a>

## Personal Images

You can run notebooks, training, and hyperparameter tuning using container images personalized by users.
Only personal images derived from the notebook/deep learning images provided by AI EasyMaker can be used when creating resources in AI EasyMaker.
Check the table below for AI EasyMaker base images.

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
    Only NHN Container Registry (NCR) can be integrated as the container registry service for storing personal images (as of December 2023).

!!! danger "Caution"
    Only personal images derived from the base images provided by AI EasyMaker can be used.

<a id="personal.image.create"></a>

### Creating Personal Images

This document guides you on how to create container images using AI EasyMaker base images with Docker and use personal images for notebooks in AI EasyMaker.

1. Create a DockerFile for the personal image.

        FROM fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204 as easymaker-notebook
        RUN conda create -n example python=3.10
        RUN conda activate example
        RUN pip install torch torchvision

2. Build personal image and push to container registry
    Build an image from the Dockerfile and store (push) the image to the NCR registry.

        docker build -t {image name}:{tag} .
        docker tag {image name}:{tag} {NCR registry address}/{image name}:{tag}
        docker push {NCR registry address}/{image name}:{tag}

        (Example)
        docker build -t custom-training:v1 .
        docker tag custom-training:v1 example-kr1-registry.container.nhncloud.com/registry/custom-training:v1
        docker push example-kr1-registry.container.nhncloud.com/registry/custom-training:v1

3. Create the image stored (pushed) to NCR as a personal image in AI EasyMaker.

    1. Go to the **Images** menu in the AI EasyMaker console.
    2. Click the **Create Image** button and enter information for the created image.
        - Name, Description: Enter the name and description for the image.
        - URL: Enter the registry image address.
        - Type: Enter the type of container image. Select **Notebook** or **Training**.
        - Account: Select an account for AI EasyMaker notebook/training nodes to access your registry repository.
            - Create new: Register a new registry account.
                - Name, Description: Enter the name and description for the registry account.
                - Category: Select the container registry service.
                - ID: Enter the ID for the registry repository.
                - Password: Enter the password for the registry repository.
            - Use existing account: Select an already registered registry account.

4. Create a notebook with the created personal image.
    1. Go to the **Notebooks** menu. Click the **Create Notebook** button to go to the notebook creation page.
    2. Click the **Personal Images** tab in the image information.
    3. Select the personal image to use as the notebook container image.
    4. After entering other notebook information and creating it, the notebook will run with the personal image.

!!! tip "Note"
    Personal images can be used for notebooks, training, and hyperparameter tuning to create resources.

!!! tip "Note"
    Only NHN Container Registry (NCR) service can be integrated as the container registry service (as of December 2023).
    For the NCR service account ID and password, enter the following values:
    ID: User Access Key of the NHN Cloud user account
    Password: User Secret Key of the NHN Cloud user account

<a id="registry.account"></a>

## Registry Account

AI EasyMaker needs to log in to your registry to pull images from your personal registry where private images are stored and run containers.
By storing login information as a registry account, you can reuse it with images linked to that registry account.
To manage registry accounts, go to the **Images** menu in the AI EasyMaker console and select the **Registry Account** tab.

<a id="registry.account.create"></a>

### Create Registry Account

Create a new registry account.

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
    When you change a registry account, the registry service will use the changed ID and password when using images linked to that account.
    If you enter an incorrect registry ID or password, authentication will fail during private image pull, causing resource creation to fail.

!!! danger "Caution"
    Problems may occur if you modify the ID and password when there are resources being created with private images linked to the registry account, or when training and hyperparameter tuning are in progress.
    Be careful when modifying the ID and password.

<a id="registry.account.modify.account.info.modify"></a>

#### Registry Account > Change Name and Description

1. Select the account to change from the registry account list.
2. Click the **Change** button at the bottom of the screen.
3. Change the name and description, then click the **Confirm** button.

<a id="registry.account.delete"></a>

### Delete Registry Account

Select the registry account to delete from the list and click the **Delete Registry Account** button.

!!! tip "Note"
    Registry accounts linked to images cannot be deleted. To delete one, you must first delete the linked images, then delete the registry account.

<a id="pipeline"></a>

## Pipelines

ML Pipelines are features for managing and executing portable and scalable machine learning workflows.
You can use the Kubeflow Pipelines (KFP) Python SDK to create components and pipelines, compile pipelines into intermediate representation YAML, and run them in AI EasyMaker.
Most pipelines aim to produce one or more ML artifacts such as datasets, models, evaluation metrics, and more.

!!! tip "Note"
    A **pipeline** is a definition of a workflow that combines one or more components to form a directed acyclic graph (DAG).
    - Each component runs a single container during execution, which can produce ML artifacts.
    - Components can receive inputs and generate outputs. There are two types of I/O: parameters and artifacts.
    - Parameters are useful for passing small amounts of data between components.
    - Artifact types are for ML artifact outputs such as datasets, models, metrics, etc. They provide a convenient mechanism for storage in Object Storage.

!!! tip "Note"
    The ability to view console output generated during pipeline execution is not provided.
    Pipeline code logs should be sent to Log & Crash Search using the [SDK's Log transmission feature](./sdk-guide/#feature.lncs.log.send) for verification.

!!! tip "Note"
    Kubeflow Pipelines (KFP) official documentation
    - [KFP User Guide](https://www.kubeflow.org/docs/components/pipelines/user-guides/)
    - [KFP SDK Reference](https://kubeflow-pipelines.readthedocs.io/en/stable/)

<a id="pipeline.upload"></a>

### Upload Pipeline

Upload a pipeline.

- **Name**: Enter the pipeline name.
- **Description**: Enter a description.
- **File Registration**: Select the YAML file to upload.

!!! tip "Note"
    Pipeline upload may take several minutes.
    When creating a resource for the first time, it may take several additional minutes to configure the service environment.

<a id="pipeline.list"></a>

### Pipeline List

The pipeline list is displayed. Select a pipeline from the list to view detailed information and modify information.

- **Status**: The status of the pipeline is displayed. For major statuses, see the table below.

    | Status             | Description                                    |
    |--------------------|-----------------------------------------------|
    | CREATE REQUESTED   | Pipeline creation has been requested.         |
    | CREATE IN PROGRESS | Pipeline creation is in progress.             |
    | CREATE FAILED      | Pipeline creation failed. Please try again.   |
    | ACTIVE             | Pipeline has been created successfully.       |

<a id="pipeline.graph"></a>

### Pipeline Graph

The pipeline graph is displayed. Select a node in the graph to view detailed information.

The graph is a visual representation of the pipeline. Each node in the graph represents a step in the pipeline, and arrows indicate the parent/child relationships between pipeline components represented by each step.

<a id="pipeline.delete"></a>

### Delete Pipeline

Delete a pipeline.

1. Select the pipeline to delete.
2. Click **Delete Pipeline**. Pipelines being created cannot be deleted.
3. The requested deletion operation cannot be canceled. To proceed, click **Delete**.

!!! tip "Note"
    If there is a schedule created with the pipeline you want to delete, you cannot delete the pipeline. Delete the pipeline schedule first, then delete the pipeline.

<a id="pipeline.run"></a>

## Pipeline Run

You can run and manage uploaded pipelines in AI EasyMaker.

<a id="pipeline.run.create"></a>

### Create Pipeline Run

Run a pipeline.

- **Basic Information**
    - **Name**: Enter the pipeline run name.
    - **Description**: Enter a description.
    - **Pipeline**: Select the pipeline to run.
    - **Experiment**: Select an experiment to include the pipeline run. Experiments group related pipeline runs. If no experiment has been created, click **Add** to create an experiment.
- **Run Information**
    - **Run Parameters**: If there are input parameters defined in the pipeline, enter values.
    - **Run Type**: Select the pipeline run type. If you select **One-time**, the pipeline runs only once. To run the pipeline periodically and repeatedly, select **Schedule** and configure the schedule by referring to [Create Pipeline Schedule](#pipeline.recurring.run.create).
- **Instance Information**
    - **Instance Type**: Select the instance type to run the pipeline.
    - **Number of Instances**: Enter the number of instances to use for the pipeline run.
- **Additional Settings**
    - **Boot Storage Size**: Enter the boot storage size of the instance to run the pipeline.
    - **NHN Cloud NAS**: You can connect **NHN Cloud NAS** to the instance that will run the pipeline.
        - **Mount Directory Name**: Enter the name of the directory to mount on the instance.
        - **NAS Path**: Enter a path in the format `nas://{NAS ID}:/{path}`.
    - **Log Management**: You can save logs generated during pipeline run progress to the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    Creating a pipeline run may take several minutes.
    When creating resources for the first time, it takes a few additional minutes to configure the service environment.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="pipeline.run.list"></a>

### Pipeline Run List

The pipeline run list is displayed. Selecting a pipeline run from the list allows you to check detailed information and change information.

- **Status**: The status of the pipeline run is displayed. Refer to the table below for main statuses.

    | Status                        | Description                                                                                    |
    |-------------------------------|------------------------------------------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline run creation has been requested.                                                      |
    | CREATE IN PROGRESS            | Pipeline run creation is in progress.                                                          |
    | CREATE FAILED                 | Pipeline run creation failed. Please try again.                                                |
    | RUNNING                       | Pipeline run is in progress.                                                                   |
    | COMPLETE IN PROGRESS          | Resources used for pipeline run are being cleaned up.                                          |
    | COMPLETE                      | Pipeline run completed successfully.                                                            |
    | STOP IN PROGRESS              | Pipeline run is being stopped.                                                                 |
    | STOPPED                       | Pipeline run was stopped by user request.                                                      |
    | FAIL PIPELINE RUN IN PROGRESS | Resources used for pipeline run are being cleaned up.                                          |
    | FAIL PIPELINE RUN             | Pipeline run failed. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |

- **Actions**
    - **Stop**: You can stop a pipeline run in progress.
- **Monitoring**: In the **Monitoring** tab of the detail screen displayed when selecting a pipeline run from the list, you can check the list of monitoring target instances and basic metric charts.
    - The **Monitoring** tab is disabled when the pipeline run is in the creation state.

<a id="pipeline.run.graph"></a>

### Pipeline Run Graph

The pipeline run graph is displayed. Selecting a node in the graph allows you to check detailed information.

The graph is a visual representation of the pipeline run. This graph shows the steps already executed during pipeline run and the currently executing step, and represents parent/child relationships between pipeline components shown as each step with arrows. Each node in the graph represents a step of the pipeline.

Through detailed information for each node, you can download generated artifacts.

!!! danger "Caution"
    Pipeline artifacts are stored for 120 days. Artifacts older than 120 days are automatically deleted.

<a id="pipeline.run.stop"></a>

### Stop Pipeline Run

Stop a pipeline run in progress.

1. Select the pipeline run you want to stop from the list.
2. Click **Stop Run**.
3. The requested action cannot be canceled. To continue, click **Confirm**.

!!! tip "Note"
    Stopping a pipeline run may take several minutes.

<a id="pipeline.run.copy"></a>

### Copy Pipeline Run

Create a new pipeline run with the same settings as an existing pipeline run.

1. Select the pipeline run you want to copy.
2. Click **Copy Pipeline Run**.
3. The pipeline run creation screen is displayed with the same settings as the existing pipeline run.
4. If there is information you want to change, modify it and click **Create Pipeline Run**.

<a id="pipeline.run.delete"></a>

### Delete Pipeline Run

Delete a pipeline run.

1. Select the pipeline run to delete.
2. Click **Delete Pipeline Run**. Pipeline runs in progress cannot be deleted.
3. The requested deletion cannot be canceled. To continue, click **Delete**.

<a id="pipeline.schedule"></a>

## Pipeline Schedule

You can create and manage schedules for periodically and repeatedly executing uploaded pipelines in AI EasyMaker.

<a id="pipeline.recurring.run.create"></a>

### Create Pipeline Schedule

Create a schedule for periodically and repeatedly executing a pipeline.

For information other than the items below that can be configured when creating a pipeline schedule, see [Create Pipeline Execution](#pipeline.run.create).

- **Execution Information**
    - **Execution Type**: Select the pipeline execution type. When **Schedule Setting** is selected, the pipeline is executed periodically and repeatedly. To execute the pipeline only once, select **One-time**.
    - **Trigger Type**: Select the pipeline execution trigger type. You can select **Time Period** or **Cron Expression**.
        - To repeatedly execute the pipeline through time period settings, select **Time Period** and then enter a number and time unit.
        - To repeatedly execute the pipeline through Cron expression settings, select **Cron Expression** and then enter a Cron expression.
    - **Concurrent Execution Setting**: Depending on the trigger cycle (**Time Period** or **Cron Expression**), a new pipeline execution may be created before a previously created pipeline execution ends. You can limit the number of parallel executions by specifying the maximum number of concurrent executions.
    - **Start Time**: You can set the start time of the pipeline schedule. If not entered, pipeline executions are created according to the configured cycle.
    - **End Time**: You can set the end time of the pipeline schedule. If not entered, pipeline executions are created until stopped.
    - **Missed Execution Catchup**: Determines whether to catch up if pipeline execution falls behind schedule.
        - For example, assuming the pipeline schedule is temporarily stopped and then restarted later, setting this to **Enable** will catch up on missed pipeline executions.
        - If the pipeline handles backfill internally, this should be set to **Disable** to prevent duplicate backfill operations.

!!! tip "Note"
    Creating a pipeline schedule may take several minutes.
    When creating resources for the first time, it may take several additional minutes to configure the service environment.

!!! tip "Note"
    Cron expressions use 6 space-separated fields to represent time.
    For more details, see the [Cron Expression Format](https://pkg.go.dev/github.com/robfig/cron#hdr-CRON_Expression_Format) documentation.

<a id="pipeline.recurring.run.list"></a>

### Pipeline Schedule List

The pipeline schedule list is displayed. Selecting a pipeline schedule from the list allows you to check detailed information and modify the information.

- **Status**: The status of the pipeline schedule is displayed. For key statuses, see the table below.

    | Status                        | Description                                                      |
    |-------------------------------|------------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline schedule creation has been requested.                   |
    | CREATE FAILED                 | Pipeline schedule creation has failed. Please try again.        |
    | ENABLED                       | Pipeline schedule has started normally.                         |
    | ENABLED(EXPIRED)              | Pipeline schedule has started normally but has passed the configured end time. |
    | DISABLED                      | Pipeline schedule has been stopped at the user's request.       |

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
    If executions created by the pipeline schedule to be deleted are in progress, it cannot be deleted. Delete the pipeline schedule after the pipeline execution is completed.

<a id="rag"></a>

## RAG

RAG (Retrieval-Augmented Generation) is a technology that vectorizes and stores user documents, then searches for content related to questions to improve the accuracy of LLM (Large Language Model) responses. AI EasyMaker can create and manage RAG systems by integrating vector stores, embedding models, and LLMs.

<a id="rag.create"></a>

### Create RAG

Create a new RAG.

- **API Gateway Service Activation**
    - AI EasyMaker RAG uses the NHN Cloud API Gateway service to create and manage API endpoints. To use RAG functionality, you must activate the API Gateway service.
    - For more details on the API Gateway service and pricing, see:
        - [API Gateway Service Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/en/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Basic Settings**
    - **Name**: Enter a RAG name. RAG names must be unique.
    - **Description**: Enter a description of the RAG.
    - **Instance Type**: Select the instance type to run the RAG endpoint.
    - **Number of Instances**: Enter the number of instances to run the RAG endpoint.
    - **Prompt**: The prompt to be used by the RAG endpoint. Click **View Content** to see the full content of the prompt.
- **Vector Store Settings**
    - **Vector Store Type**: Select the vector store type.
        - **RDS for PostgreSQL**
            - **RDS for PostgreSQL Activation**
                - AI EasyMaker RAG uses NHN Cloud RDS for PostgreSQL to create and manage vector stores. If you select this option, you must activate RDS for PostgreSQL.
                - For more details on RDS for PostgreSQL and pricing, see:
                    - [RDS for PostgreSQL Guide](https://docs.nhncloud.com/en/Database/RDS%20for%20PostgreSQL/en/overview/)
                    - [RDS for PostgreSQL Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Database&s=RDS%20for%20PostgreSQL)
            - **Instance Type**: Select the instance type to use in RDS for PostgreSQL.
            - **Storage Type**: Select the storage type to use in RDS for PostgreSQL.
            - **Storage Size**: The storage size to use in RDS for PostgreSQL.
            - **User ID**: Enter the user ID for PostgreSQL access.
            - **Password**: Enter the password for PostgreSQL access.
            - **Confirm Password**: Re-enter the password for confirmation.
            - **VPC ID**: Enter the VPC ID to use in RDS for PostgreSQL.
            - **Subnet ID**: Enter the subnet ID to use in RDS for PostgreSQL.
        - **PostgreSQL Instance**: Use a user-created NHN Cloud PostgreSQL Instance as the vector store.
            - **User ID**: Enter the user ID that can access the PostgreSQL Instance.
            - **Password**: Enter the password that can access the PostgreSQL Instance.
            - **VPC ID**: Enter the VPC ID of the PostgreSQL Instance.
            - **Subnet ID**: Enter the subnet ID of the PostgreSQL Instance.
            - **PostgreSQL Instance IP**: Enter the IP address of the PostgreSQL Instance.
    - **Collection Settings**
        - **Data Path**: Enter the data path where documents to be collected into the vector store are stored.
    - **Embedding Model**
        - **Model**: Select the embedding model to use when vectorizing documents and queries.
        - **Instance Type**: The instance type to run the embedding model.
        - **Number of Instances**: Enter the number of instances to run the embedding model.
- **LLM Settings**
    - **Model**: Select the LLM to use when generating responses.
    - **Instance Type**: The instance type to run the LLM.
    - **Number of Instances**: The number of instances to run the LLM.
- **Additional Settings**
    - **Log Management**: Logs generated during RAG execution can be stored in the NHN Cloud Log & Crash Search service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    The format, size, and number of files that can be used for collection may be limited. For more details, see [Ingestion Sync](#rag.ingestion.sync).

!!! danger "Caution"
    When using PostgreSQL Instance, set the port to `15432`.
    For instructions on creating instances, see [PostgreSQL Instance](https://docs.nhncloud.com/en/Compute/Instance/en/component-guide/#postgresql-instance).
    Configure the security group to allow access to port `15432` from the instance's subnet range.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="rag.list"></a>

### RAG List

View and manage the list of created RAGs. Select a RAG from the list to view detailed information.

- **Status**: The RAG status. See the table below for major statuses.

| Status | Description |
| --- | --- |
| CREATE REQUESTED | RAG creation has been requested. |
| CREATE IN PROGRESS | RAG creation is in progress. |
| ACTIVE | RAG is operating normally. |
| UPDATE IN PROGRESS | Collection is in progress in the RAG. |
| DELETE IN PROGRESS | RAG deletion is in progress. |
| CREATE FAILED | RAG creation has failed.<br/>Delete the RAG and create it again. If creation failures persist, contact customer support. |
| UPDATE FAILED | Collection has failed in the RAG.<br/>Try **Ingestion Sync** again. If update failures persist, contact customer support. |
| DELETE FAILED | RAG deletion has failed.<br/>Try deletion again. If deletion failures persist, contact customer support. |

- **API Gateway Status**: Deployment status information for the API Gateway default stage.

| Status | Description |
| --- | --- |
| DEPLOYING | API Gateway default stage is being deployed. |
| COMPLETE | API Gateway default stage has been successfully deployed and is active. |
| FAILURE | API Gateway default stage deployment has failed. |

- **Ingestion History**: On the **Ingestion History** tab of the detailed screen displayed when you select a RAG, you can view the execution history of document collection tasks.
- **API Statistics**: On the **API Statistics** tab of the detailed screen displayed when you select a RAG, you can view API statistics information.
- **Monitoring**: On the **Monitoring** tab of the detailed screen displayed when you select a RAG, you can view the list of monitoring target instances and basic metric charts.

<a id="rag.ingestion.sync"></a>

### Ingestion Sync

- The ingestion sync feature is available on the **Vector Store** tab of the detailed screen displayed when you select a RAG.
- When documents are added, deleted, or modified in the collection data path, you can run **Ingestion Sync** to reflect the changes.
- The format, size, and number of files that can be used for collection may be limited. See the table below for details.

| Item | Limit |
|-----|------|
| Total file size | 100GB |
| Maximum number of files | 1,000,000 |

| Category | Supported formats | Maximum file size |
|--------|---------|------------|
| Text documents | `.txt`, `.text`, `.md` | 3MB |
| Documents | `.doc`, `.docx`, `.pdf` | 50MB |
| Spreadsheets | `.csv`, `.xls`, `.xlsx` | 3MB |
| Presentations | `.ppt`, `.pptx` | 50MB |

<a id="rag.delete"></a>

### Delete RAG

- RAGs that are being created or deleted cannot be deleted.
- Requested deletion tasks cannot be canceled.

<a id="rag.query.request.guide"></a>

### RAG Query Request Guide

- When requesting queries, include `model` and `messages` in the request body like the OpenAI Chat Completion API. Use the RAG name for the `model`.
- For detailed request examples, see the content below.

<details>
<summary><strong>Call Example (cURL)</strong></summary>

```bash
curl -X POST https://{API 엔드포인트 주소}/rag/v1/query \
  -H "Content-Type: application/json" \
  -d '{
    "model": "{RAG 이름}",
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

DEFAULT_URL="https://{API 엔드포인트 주소}/rag/v1/query"
DEFAULT_MODEL="{RAG 이름}"
DEFAULT_PROMPT="AI EasyMaker 서비스에 대해 설명하세요."

usage() {
  cat <<'EOF'
사용법:
  <파일 이름> -k <API_KEY> [-u URL] [-m MODEL] [-p PROMPT]

옵션:
  -k   API 키 (x-nhn-apikey: <API_KEY> 헤더로 전송)
  -u   호출 URL
  -m   모델명
  -p   사용자 프롬프트
  -h   도움말

설명:
  - OpenAI 호환 스펙으로 stream=true 호출을 수행하고,
    스트리밍으로 전달되는 각 chunk의 choices[].delta.content만을
    표준 출력에 순차적으로 기록합니다.

필수 도구:
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
    \?) echo "알 수 없는 옵션: -$OPTARG" >&2; usage; exit 2 ;;
    :) echo "옵션 -$OPTARG 에 값이 필요합니다." >&2; usage; exit 2 ;;
  esac
done

if ! command -v curl >/dev/null 2>&1; then
  echo "에러: curl 이 필요합니다." >&2
  exit 1
fi
if ! command -v jq >/dev/null 2>&1; then
  echo "에러: jq 가 필요합니다." >&2
  exit 1
fi

# JSON Payload 생성 (OpenAI Chat Completions 호환 형태)
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

echo "요청 URL: $URL" >&2
echo "모델: $MODEL" >&2
echo "---------------- 스트리밍 시작 ----------------" >&2

# 스트리밍 처리: data: {json} 라인에서 delta.content 만 추출
curl -sS -N -X POST "$URL" "${headers[@]}" --data-raw "$payload" \
| while IFS= read -r line; do
    [[ -z "$line" ]] && continue
    if [[ "$line" == "data: [DONE]"* ]]; then
      break
    fi
    if [[ "$line" == data:* ]]; then
      json="${line#data: }"
      # 여러 choice가 있을 수 있으므로 모두 출력
      # delta.content가 없을 수도 있어 empty로 처리
      while IFS= read -r piece; do
        printf "%s" "$piece"
      done < <(printf '%s\n' "$json" | jq -r '.choices[]?.delta?.content // empty')
    fi
  done

echo
echo "---------------- 스트리밍 종료 ----------------" >&2
```

</details>

<a id="appendix"></a>

## Appendix

<a id="appendix.1.object.storage.account.permission"></a>

### 1. Adding AI EasyMaker System Account Permissions to NHN Cloud Object Storage

When using your NHN Cloud Object Storage as input/output storage for some AI EasyMaker features, you must grant read or write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container for proper feature operation.

Granting read/write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container means that the AI EasyMaker system account can read or write files in your NHN Cloud Object Storage container according to the granted permissions for all files.

Please make sure to check this information and set access policies for your Object Storage with only the necessary accounts and permissions.

The user is responsible for all consequences that may arise from allowing access to your Object Storage by accounts other than the AI EasyMaker system account during the access policy setting process, and AI EasyMaker does not take responsibility for such consequences.

!!! tip "Note"
    The files that AI EasyMaker accesses to read or write in Object Storage depending on the feature are as follows.

| Feature       | Permission | Access Target                                            |
| ---------- | ---- | ---------------------------------------------------- |
| Training, Hyperparameter Tuning       | Read | Algorithm path and training input data path entered by the user |
| Training, Hyperparameter Tuning       | Write | Training output data and checkpoint path entered by the user   |
| Model       | Read | Model artifact path entered by the user                   |
| Model Evaluation | Read | Input data path entered by the user                   |
| Model Evaluation | Write | Output data path entered by the user                   |
| Batch Inference | Read | Input data path entered by the user                   |
| Batch Inference | Write | Output data path entered by the user                   |
| RAG | Read | Collection data path entered by the user                   |

To add read/write permissions for the AI EasyMaker system account to NHN Cloud Object Storage, refer to the following:

1. Click **[Training]** or **[Model]** tab > **AI EasyMaker System Account Information**.
2. Save the AI EasyMaker system account information: **AI EasyMaker Tenant ID** and **AI EasyMaker API User ID**.
3. Go to the NHN Cloud Object Storage console.
4. Refer to the [Allow Read/Write to Specific Projects or Users](https://docs.nhncloud.com/en/Storage/Object%20Storage/en/acl-guide/#role-based-access-allow-rw-project-or-user) document and add the necessary read and write permissions for the AI EasyMaker system account in the NHN Cloud Object Storage console.

<a id="appendix.2.lncs.service.usage.guide.and.log.inquiry.guide"></a>

### 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Method

<a id="appendix.2.lncs.service.usage.guide"></a>

#### NHN Cloud Log & Crash Search Service Usage Guide

Logs and events from the AI EasyMaker service can be stored in the NHN Cloud Log & Crash Search service.
To store logs in the Log & Crash Search service, you must enable the Log & Crash service, and separate usage fees will be charged.

- **Log & Crash Search Service Usage and Pricing Information**
    - For detailed information and pricing of the Log & Crash Search service, see:
        - [Log & Crash Search Service Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/en/Overview/)
        - [Log & Crash Search Usage Fees](https://www.nhncloud.com/kr/pricing/by-service?c=Data%20%26%20Analytics&s=Log%20%26%20Crash%20Search)

<a id="appendix.2.lncs.service.log.inquiry.guide"></a>

#### Log Inquiry

1. Go to the Log & Crash Search service console page.
2. Enter search conditions in the Log & Crash Search service to query logs.
    - AI EasyMaker training log query: Query logs where the category field is "easymaker.training".
        - Query: category:"easymaker.training"
    - AI EasyMaker endpoint log query: Query logs where the category field is "easymaker.inference".
        - Query: category:"easymaker.inference"
    - AI EasyMaker all log query: Query logs where the logType field is "NHNCloud-AIEasyMaker".
        - Query: logType:"NHNCloud\-AIEasyMaker"
3. For detailed usage of the Log & Crash Search service, see the [Log & Crash Search Service Console Guide](https://docs.nhncloud.com/en/Data%20&%20Analytics/Log%20&%20Crash%20Search/en/console-guide/).

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
    | trainingId | AI EasyMaker training ID |

- **Hyperparameter Tuning Log Fields**

    | Name                   | Description                                |
    | ---------------------- | ----------------------------------- |
    | hyperparameterTuningId | AI EasyMaker hyperparameter tuning ID |

- **Endpoint Log Fields**

    | Name            | Description                        |
    | --------------- | --------------------------- |
    | endpointId      | AI EasyMaker endpoint ID  |
    | endpointStageId | Endpoint stage ID      |
    | inferenceId     | Inference request unique ID           |
    | action          | Action classification (Endpoint.Model) |
    | modelName       | Inference target model name         |

- **Batch Inference Log Fields**

    | Name             | Description                      |
    | ---------------- | ------------------------- |
    | batchInferenceId | AI EasyMaker batch inference ID |

<a id="appendix.3.hyperparameter"></a>

### 3. Hyperparameters

- Key-Value format values received through the console.
- When executing entry points, they are passed as execution arguments (--{Key}).
- They can also be used as environment variable values (EM*HP*{Key converted to uppercase}).

As shown in the example below, you can use hyperparameter values entered when creating training.<br>
![Hyperparameter input screen](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)

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

- Information needed for training is passed to the training container as **environment variables**, and the passed environment variables can be used in the **training script**.
- Environment variable names created from user input are converted to uppercase.
- In the code, the completed trained model must be saved in the EM_MODEL_DIR path.
- **Key Environment Variables**

    | Environment Variable Name                      | Description                                                                        |
    |-----------------------------| --------------------------------------------------------------------------- |
    | EM_SOURCE_DIR               | Absolute path of the folder where the algorithm script entered when creating training is downloaded  |
    | EM_ENTRY_POINT              | Name of the algorithm entry point entered when creating training                             |
    | EM_DATASET_${Dataset Name}     | Absolute path of the folder where each dataset entered when creating training is downloaded |
    | EM_DATASETS                 | Complete dataset list (JSON format)                                            |
    | EM_MODEL_DIR                | Model save path                                                              |
    | EM_CHECKPOINT_INPUT_DIR     | Input checkpoint save path                                                  |
    | EM_CHECKPOINT_DIR           | Output checkpoint save path                                                  |
    | EM_HP_${Hyperparameter Key Converted to Uppercase} | Hyperparameter value corresponding to hyperparameter key                              |
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

### 5. Storing Metric Logs for TensorBoard Usage

- To check result metrics on the TensorBoard screen after training, when writing training scripts, you must set the TensorBoard log storage space to the specified location (`EM_TENSORBOARD_LOG_DIR`).

<details>
<summary><strong>Example</strong></summary>

```python
import tensorflow as tf

# Specify TensorBoard log path
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # Implement model

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

<details>
<summary><strong>Check TensorBoard Logs</strong></summary>

<img src="http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_tensorboard.png" alt="Check TensorBoard Logs">

</details>

!!! danger "Caution"
    TensorBoard metric logs are stored for 120 days. Metric logs older than 120 days are automatically deleted.

<a id="appendix.6.framework.training.settings"></a>

### 6. Distributed Training Settings by Framework

- **Tensorflow**
    - The environment variable `TF_CONFIG` required for distributed training is automatically set. For details, see the [Tensorflow Official Guide](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy).
- **Pytorch**
    - `Backends` setting is required for distributed training. Set to gloo for CPU distributed training and nccl for GPU distributed training. For details, see the [Pytorch Official Guide](https://pytorch.org/docs/stable/distributed.html).

<a id="appendix.7.cluster.upgrade"></a>

### 7. Cluster Version Upgrade

The AI EasyMaker service periodically upgrades cluster versions to provide stable service and new features.
When a new cluster version is deployed, notebooks and endpoints running on the old version cluster must be migrated to the new cluster.
Here's the migration method for each resource to the new cluster.

<a id="appendix.7.cluster.upgrade.notebook"></a>

#### Notebook Cluster Version Upgrade

In the **Notebook** list screen, notebooks that need to be migrated to the new cluster display a **Restart** button to the left of the name.
When you hover your mouse pointer over the **Restart** button, a restart guide message and expiration date are displayed.

- Before expiration, please check the following precautions and click the **Restart** button.
    - When restarting, data stored in data storage (/root/easymaker directory path) is retained as is.
    - When executing restart, data stored in boot storage is initialized and may be lost. Move data to data storage before restarting.

Restart takes approximately 25 minutes for the first execution and approximately 10 minutes thereafter.
If restart fails, it is automatically reported to the administrator.

<a id="appendix.7.cluster.upgrade.endpoint"></a>

#### Endpoint Cluster Version Upgrade

In the **Endpoint List** screen, endpoints that need to be migrated to the new cluster display **! Notice** text to the left of the name.
When you hover your mouse pointer over the **! Notice** text, a version upgrade guide message and expiration date are displayed.
Before expiration, you must migrate stages operating on the old version cluster to the new version cluster according to the following guide.

<a id="appendix.7.cluster.upgrade.endpoint.stage"></a>

##### General Stage Cluster Version Upgrade

1. Delete general stages that are not default stages. Before deletion, first check if the stage is in service.
2. Create the stage again.
3. When the new stage becomes ACTIVE, check that API calls to the stage endpoint and inference responses are returned normally.

!!! danger "Caution"
    When a stage is deleted, the endpoint is terminated and API calls become impossible. Before deletion, check that it is not a stage in service.

<a id="appendix.7.cluster.upgrade.endpoint.default.stage"></a>

##### Default Stage Cluster Version Upgrade

The default stage is the stage where actual services operate.
To migrate the cluster version of the default stage without service interruption, follow this guide:

1. Create a new stage to replace the default stage of the old version cluster.
2. Check that API calls and inference responses are returned normally from the new stage endpoint.
3. Click the **Change Default Stage** button. Select the new stage to change to the default stage.
4. When the change is complete, the new stage is set as the default stage, and the existing default stage is deleted.

<a id="appendix.8.torchrun.usage"></a>

### 8. How to Use torchrun

- When code is written to enable distributed training in Pytorch and the number of distributed nodes and processes per node are entered, distributed training using distributed nodes and multi-processes with torchrun is performed.
- Training and hyperparameter tuning may fail due to memory shortage caused by factors such as total number of processes, model size, input data size, and batch size. When failing due to memory shortage, the following error message may appear. However, not all failures with the following message are due to memory shortage. Set an appropriate instance type according to memory usage.

```plaintext
exit code : -9 (pid: {pid})
```

- For more details on torchrun, see the [Pytorch Official Guide](https://pytorch.org/docs/stable/elastic/run.html).

<a id="appendix.9.resource.info"></a>

### 9. Resource Information

When creating batch inference and endpoints in AI EasyMaker, resources are allocated excluding basic usage from the selected instance type.
Since required resources vary depending on model request volume and complexity, carefully set appropriate instance types along with pod count and resource allocation.

Batch inference divides actual usage by pod count to allocate resources to each pod. For endpoints, the entered allocation cannot exceed the instance's actual usage, so check resource usage in advance.
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
    OpenAI generative model inference is used when using generative models like OpenAI's GPT-4o.
    Input values required for inference must be entered according to OpenAI's API specifications. For details, see [OpenAI API Documentation](https://platform.openai.com/docs/api-reference/chat).
    For models that support Completion and Chat Completion APIs provided by AI EasyMaker, check [Model endpoint compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility).

<a id="appendix.11.framework.note"></a>

### 11. Framework-specific Serving Notes

<a id="appendix.11.framework.note.tensorflow.framework"></a>

#### TensorFlow Framework

TensorFlow model serving provided by AI EasyMaker uses SavedModel (.pb) recommended by TensorFlow.
To use checkpoints, save the checkpoint variables directory as SavedModel together in the model directory, and it will be used for model serving.
Reference: [https://www.tensorflow.org/guide/saved_model](https://www.tensorflow.org/guide/saved_model)

<a id="appendix.11.framework.note.pytorch.framework"></a>

#### PyTorch Framework

AI EasyMaker serves PyTorch models (.mar) with TorchServe.
It is recommended to use MAR files created with model-archiver, and serving with weight files is also possible, but weight files require additional files.
Check the table below and [model-archiver documentation](https://github.com/pytorch/serve/blob/master/model-archiver/README.md) for required files and detailed descriptions.

| File Name                    | Required | Description                                                              |
| ---------------------------- | --------- | ----------------------------------------------------------------- |
| model.py                     | Required      | Model structure file passed as model-file parameter.              |
| handler.py                   | Required      | File passed as handler parameter to handle inference logic. |
| Weight file(.pt, .pth, .bin) | Required      | File storing model weights and structure.                         |
| requirements.txt             | Optional      | File to install Python packages needed for serving.        |
| extra/                       | Optional      | Files in directory are passed as extra-files parameter.         |

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
    def preprocess(self, data): # Example : data = [[1.0, 2.0], [3.0, 4.0]]
        features = []
        for row in data:
            content = row # Example : row = [1.0, 2.0]
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

Hugging Face models can be served using the runtime provided by AI EasyMaker or TensorFlow Serving and TorchServe.

<a id="appendix.11.framework.note.hugging.face.framework.runtime"></a>

##### Hugging Face Runtime

This is a simple way to serve Hugging Face models.
Hugging Face runtime serving does not support fine-tuning. To serve fine-tuned models, use TensorFlow/Pytorch Serving methods.

1. Check the model to serve on Hugging Face.
2. Copy the Hugging Face model ID.
3. Select Hugging Face framework on the AI EasyMaker model creation page and enter the Hugging Face model ID.
4. Enter input values required for the model to create the model.
5. Check the created model and create an endpoint.

!!! tip "Note"
    Currently, Hugging Face runtime does not support all Tasks of Hugging Face.
    Supported Tasks are `sequence_classification`, `token_classification`, `fill_mask`, `text_generation`, `text2text_generation`.
    To use unsupported Tasks, use TensorFlow/Pytorch Serving methods.

!!! tip "Note"
    To serve Gated Models, you must enter a token from an account with allowed access as a model parameter.
    If no token is entered or a token from an unauthorized account is entered, model deployment will fail.

<a id="appendix.11.framework.note.hugging.face.framework.tensorflow.pytorch.serving"></a>

##### TensorFlow/PyTorch Serving

This is a method to serve Hugging Face models trained with TensorFlow and PyTorch.

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
    - If fine-tuning is needed, you can write your own code to train according to the [Hugging Face Fine-tuning Guide](https://huggingface.co/docs/transformers/main/en/training).
        - For details on AI EasyMaker training, see [Training](#training).

2. Check Hugging Face model information and create files needed for serving.
    - Save the model in the format required for serving by framework.
    - For details, check the notes for TensorFlow and PyTorch frameworks.
3. Upload model files to OBS or NAS.
4. For subsequent processes, see the [Create Model](#model.create) and [Create Endpoint](#endpoint.create) guides.