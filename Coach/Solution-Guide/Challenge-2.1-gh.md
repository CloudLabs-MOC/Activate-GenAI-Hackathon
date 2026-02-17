# Challenge 03: Deploy NVIDIA NIM on Azure

### Estimated Time: 120 Minutes

## Introduction

This lab guides participants through deploying NVIDIA NeMo Inference Manager (NIM) on Azure, which facilitates rapid development and deployment of sophisticated AI models for various applications. NVIDIA NIM is a model deployment and management solution that enables efficient utilization of NVIDIA GPUs for AI model inference. This deployment involves using Azure's powerful cloud infrastructure to host NIM containers, which simplifies the integration of AI models into production environments by managing model lifecycle, deployment, and scaling in Azure Machine Learning (AML) services.

Participants will begin by creating an NVIDIA account to generate an API key, essential for accessing NVIDIA’s NGC resources, such as container images for NeMo models. Then, the lab covers setting up Azure Container Registry (ACR) for storing these images, configuring Git Bash to interact with Azure, and updating relevant configuration files within Visual Studio Code. After this setup, participants will deploy the NIM container through Azure Machine Learning, which will handle the GPU-based model deployment and expose it through a managed online endpoint.

## Solution Guide

### Task 1: Generate API Key

The NVIDIA API key is a unique identifier used to authenticate requests to NVIDIA's APIs, such as the NGC (NVIDIA GPU Cloud) services. This key allows developers to access various resources, including pre-trained models, GPU-accelerated software, and container images. Obtaining an API key typically involves creating an account on NVIDIA's developer portal and generating the key within the account settings. It is important to keep this key secure, as it grants access to your NVIDIA resources and can be used for billing purposes.

1. Please [Click Here](https://nvdam.widen.net/s/tvgjgxrspd/create-build-account-and-api-key) and follow the instructions to generate an NVIDIA API Key.

### Success!

You have successfully created your NVIDIA Account.

   ![](../../Scenario/media/nvaie-creditsa.png)

### Explore NIMs:

- Now you can explore all available NIMs! Use the search bar at the top to search for any model or LLM task (e.g., search for "Llama").

  ![](../../Coach/media/llamasearch.png)

- Explore the search results, open the NIM of interest, and experiment with it.
- You are now provided with a free usage limit of up to **40 requests per minute (RPM)**, giving you more flexibility to try out the NIMs..

   ![](../../Coach/media/nvaie-7-1.png)
  
- You can also call these NIMs in your Python application using the OpenAI library (refer to the Python code on the right) or using [NVIDIA LangChain endpoints](https://python.langchain.com/docs/integrations/chat/nvidia_ai_endpoints/).

   ![](../../Coach/media/nvaie-8.png)

### Generate API Key

1. Please [Click Here](https://nvdam.widen.net/s/tvgjgxrspd/create-build-account-and-api-key) and follow the instructions to generate an NVIDIA API Key.

### Accessing the Azure portal

>**Important:** You can find the Username and Password by navigating to the **Environment** **(1)** tab, then copy the **Azure Username** **(2)** and **Azure Password** **(3)**, which will be required for signing into the Azure portal in later steps. You can also record the **Deployment Id** **(4)**, which can be used to provide a unique name to the resources during deployment.

   >**Note:** Numbers and ID values may vary. Kindly ignore values in screenshots and copy values from the **Environment** tab.

 ![](../media/Active-image19upd.png)

1. To access the Azure portal, from the **LabVM** open **Microsoft Edge** and browser to the [Azure Portal](https://portal.azure.com/).

1. On the **Sign into Microsoft Azure tab**, you will see a login screen. Enter the following email/username, and then click on **Next**.
   
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

     ![](../media/Active-image1.png)

1. Now enter the following **Password (1)** and click on **Sign in (2)**.

   - **Password:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/password(1).png)

1. If a **Welcome to Microsoft Azure** pop-up window appears, click **Cancel** to skip the tour.

    ![](../media/Active-image5.png)

### Docker Start

1. In the lab VM, from the Start bar, search for **Docker** **(1)** and select **Docker Desktop** **(2)** from the results.

   ![](../media/h71.png)

1. Click on **Accept.**

   ![](../media/h28.png)

1. Click **Skip** on the **Welcome to Docker** page. 

   ![](../media/h30.png)

1. Click on **Skip** on the **Tell us about yourself** page.   

   ![](../media/h31-new.png)

1. Wait for the app to start. After the app starts, wait for the app to start Docker Engine.

   ![](../media/Ch3-11.png)

   > **Note:** If you see a message that Docker needs upgrade then run the below mentioned command in PowerShell and then click on Restart button

      ```
      wsl --update
      ```

1. After the Docker Engine starts, the Docker UI should resemble the following screenshot. Docker will display any running containers.

   ![](../media/h33.png)

   > **Note**: Minimize the Docker Desktop, but don’t close the app.

1. Minimize Docker Desktop and continue with the next steps.

   ![](../../Coach/media/nvdocker6.png)

   >**Note:** If you encounter an error such as **"Docker Desktop - Unexpected WSL error"**, click **Quit** to close Docker and follow below steps:

   ![](../../Coach/media/nvdocker7.png)

   - Search for the **PowerShell (1)** from the taskbar in your lab-VM, right-click on the **PowerShell (2)**, and select **Run as administrator (3)**.
     
     ![](../../Coach/media/powershell.png)
     
   - Run the below command:
     
      ```
      #Check if 'docker-users' group exists before adding to 'Administrators'
       $dockerUsersGroupExists = Get-LocalGroup -Name 'docker-users' -ErrorAction SilentlyContinue
       $CurrentUser = "demouser"
       if ($dockerUsersGroupExists -ne $null) {
           Add-LocalGroupMember -Group 'docker-users' -Member $CurrentUser -Verbose
           Write-Host "User '$CurrentUser' added to the 'docker-users' group."
       } else {
           Write-Host "'docker-users' group does not exist. Skipping adding the user to 'docker-users'."
     
        }
       ```

      >**Note:** If you get an error `demouser is already a member of group docker-users`, ignore and proceed further
  
   - Once the command is executed, from the **Resources** tab, **restart** the Virtual machine.

     ![](../../Coach/media/resupd.png)
  
   - Once the VM is restarted, reopen the **Docker Desktop**.

## Task 2: Create Container Registry

Azure Container Registry (ACR) is a managed Docker container registry service that allows you to store and manage private Docker container images and artifacts in Azure. It provides a secure and scalable solution for building, deploying, and managing containerized applications, enabling seamless integration with Azure services.

1. In the search bar of the Azure portal, type **Container registries** **(1)**. From the search results, select **Container registries** **(2)** to access the container registry management section.

   ![](../../Coach/media/cr1.png)

1. From the **Container registries** blade, click on **+ Create**.

1. On the **Basics** tab of Create **Container Registry**, provide details as mentioned in the table below and select **Review + create** **(6)** at the bottom of the page and subsequently click on **Create**.

    | Setting | Action |
    | -- | -- |
    | **Subscription** | Default |
    | **Resource Group** | **ODL-GenAI-CL-XXXXXX-01** **(1)** |
    | **Registry name** | **amlregistryxxxxxxx** **(2)** |
    | **Location** | **UK South** (Choose the same location where the resource group) **(3)** |
    | **Domain name label scope** | **Unsecure** **(4)** |    
    | **Pricing plan** | **Standard** **(5)** |

   > **Note:** Unique ID (XXXXXX) refers to DeploymentID.

   ![](../../Coach/media/create-amlregistryupd(1).png)

   ![](../../Coach/media/validate-amlregistryupd(2).png)

1. Once the deployment is completed, click on **Go to resource**.

1. From the Overview page, copy the **Subscription ID** and paste the  subscription ID into Notepad, as you will need it later.

   ![](../../Coach/media/aml3(1).png)

## Task 3: Setup Git Bash Environment

1. In the **LabVM**, from the **Taskbar**, search for **git bash** **(1)**. Once you find it, right-click on **Git Bash** **(2)** and select **Run as administrator** **(3)** to launch Git Bash with elevated privileges.

   ![](../media/git-bash-run.png)

1. Run the following command. This command downloads the latest version of jq, a lightweight and flexible command-line JSON processor, and saves it as an executable file named `jq.exe` in the `/usr/bin/` directory, making it accessible for command-line use.

   ```
   curl -L -o /usr/bin/jq.exe https://github.com/stedolan/jq/releases/latest/download/jq-win64.exe
   ```
   >**Note:** If `jq` is not found or fails to download, open PowerShell and run `choco install jq` to install it.

1. Install the **az CLI** by navigating to the link below:

      ```
      $ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://azcliprod.blob.core.windows.net/msi/azure-cli-2.51.0.msi -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; Remove-Item .\AzureCLI.msi
      ```

      >**Note:** Ensure to run the command in Windows PowerShell.

1. Now, install the ml extension.

   ```
   az extension add -n ml
   ```

   ```
   az extension update -n ml
   ```

1. Run the help command to verify your installation and see available subcommands:

   ```
   az ml -h
   ```

1. Clone the GitHub repository to your Desktop 

   ```
   cd Desktop
   ```

   ```
   git clone https://github.com/CloudLabsAI-Azure/nim-deploy.git
   ```

1. Use the command below to navigate to the directory:

   ```
   cd nim-deploy/cloud-service-providers/azure/azureml/cli
   ```

Detailed instructions can be found [here](https://github.com/NVIDIA/nim-deploy/tree/main/cloud-service-providers/azure/azureml/cli).

## Task 4: Visual Studio config.sh file update

1. Start **Visual Studio Code** by launching it from your desktop.

   ![](../../Coach/media/vscode(1).png)

1. Go to the **Explorer** panel in the upper left corner, click on **Open Folder**,  select **cli folder** from the location where you have cloned the repo in previous step `Desktop/cloud-service-providers/azure/azureml/cli`, and then click on **Select Folder** to open it in Visual Studio Code.

   ```
   Desktop\nim-deploy\cloud-service-providers\azure\azureml\cli
   ```

   ![](../../Coach/media/vscode2.png)

1. Select **Yes, I trust the authors**.

   ![](../../Coach/media/vscode3.png)

1. Open the `config.sh` file and update the values as needed. You can refer to the `example_config.sh` file for guidance on the appropriate configurations and settings.

    | Setting | Action |
    | -- | -- |
    | **subscription_id** | **<inject key="SubscriptionID" enableCopy="false"/>** |
    | **resource_group** | **ODL-GenAI-CL-XXXXXXX-01**  |
    | **workspace** | **ml-workspace{suffix}** (Provide the name of the workspace you want to create) |
    | **location** | Kindly refer to Challenge 3 on page 6 of the integrated lab guide (Attendee Guide). Under step 5 in the "Note" section, you’ll find the region selection details. Please select any one region from the list of provided options. |
    | **ngc_api_key** | Provide the NGC key  |
    | **email_address** | Enter the email from the Environmental Details tab  |
    | **acr_registry_name** | **amlregistry{suffix}** |
    | **image_name** | **llama3-8b-instruct:latest**|
    | **endpoint_name** | **llama3-8b-nim-endpoint{suffix}** |
    | **deployment_name** | **llama3-8b-nim-dep{suffix}** |

   ![](../../Coach/media/vmnew.png)
   
   ![](../../Coach/media/vscode4.png)

   ![](../../Coach/media/up2upd.png)

   > **Note** : Replace `{suffix}` with the Deployment ID. Navigate to **Environment** **(1)**, and copy the **Deployment ID** from the **User Name** field.

   ![](../media/a26upd.png)

1. Press **Ctrl + S** to save the changes you made to the file.

## Task 5: Create AzureML Deployment of the NIM Container

### Log in to Azure with Your Credentials

1. Switch back to the Git Bash terminal.

1. Update your login credentials (**Username** and **Password**) and set the **subscription_id** for your subscription.
   
   - **Subscription Id:** - <inject key="SubscriptionID"></inject>
   - **Username:** <inject key="AzureAdUserEmail"></inject>
   - **Password:** <inject key="AzureAdUserPassword"></inject>
   
      ```
      az login 
      az account set --subscription <subscription_id>
      ```

      > **Note:** If you encounter an error mentioned below, run `az login` and select your account for logging in to Azure.
      
       ![](../media/CH2T3S5.png)
      
      > **Note:** If you encounter any issues during login, you can execute the following command.
   
      ```
      az account clear
      az config set core.enable_broker_on_windows=false
      az login 
      az account set --subscription <subscription_id>
      ```

1. This will prompt an Azure login window; please select your credentials to log in.

##  Task 6: Set up Azure ML Workspace

1. Navigate to the deployment directory by using the following command:

    ```cmd
    cd ./Desktop/nim-deploy/cloud-service-providers/azure/azureml/cli

    ```

1. Execute the following command to create a new AzureML workspace with the "Azure ML Secrets Reader" role assignment.

   ```cmd
    ./1_set_credentials.sh --create_new_workspace
   ```
   > **Note:** The above command creates a new workspace with the workspace name provided in the config.sh file.

1. You can find the newly created workspace in Azure

   ![](../../Coach/media/u1.png)

##  Task 7: Store NGC API Key for Use in the AzureML Deployment

1. To Store the NGC API Key for Use in the AzureML Deployment. You have two options for storing the NGC API Key:

   >**Note:** The NGC API Key needs to be stored within Azure so the AzureML workspace can access it during deployment. The API key is required to pull the correct model from the NGC model  catalog. The key can be provided as a workspace connection to the AzureML workspace.
   
   **Store the Key as a Workspace Connection:**
   Store the NGC API Key as a custom credential using a workspace connection.

   This script stores the NGC API Key as a workspace connection credential and verifies if the provided workspace can access it.

   Run the following script to configure this and verify the connection

   ```cmd
   ./2_provide_ngc_connection.sh
   ```
   >**Note:** If you see a `jq: command not found` error while running the script, open PowerShell as Administrator, run `choco install jq`, and then re-run the `2_provide_ngc_connection.sh` script.

##  Task 8: Save NIM Container in Your Container Registry

Pull the NIM Docker container for the model specified in the `config.sh` file. Create another Docker container wrapped around the NIM container for deployment in AzureML and push this new container to an Azure container registry that can be accessed by your AzureML endpoint. All required commands are provided in the `3_save_nim_container.sh` script.

1. Run the following command to **save the NIM container in your container registry**.

   ```cmd
   ./3_save_nim_container.sh
   ```
   >**Note:** This action will approximately take around 20-25 Minutes.
   
   >**Note:** Ensure that the Docker engine is running.

1. Navigate to your container registry (**amlregistry**), under **Services**, click on the **Repositories**, select your **llama-3-8b-instruct** repository, here you will find your image is pushed with the tag name **latest**.

   ![](../../Coach/media/bash2-1upd1.png)

##  Task 9: Create Managed Online Endpoint

1. Run the following command to **create a managed online endpoint**.

   ```cmd
   ./4_create_endpoint.sh
   ```

   >**Note:** This command creates an endpoint with the name provided in the config.sh file.

   > **Note:** If you see an `ERROR: 'ml' is misspelled or not recognized by the system.` Run the below commands to remove, install, and verify the ML extension.

   ```
   az extension remove -n ml
   ```

   ```
   az extension add -n ml
   ```

   ```
   az ml -h
   ```

   >**Note:** Rerun the command to create the endpoint.

## Task 10: Role Assignment

1. Go to **amlregistry** container regiestry first. Navigate to **Access control (IAM) (1)**. Click on **+ Add (2)** and choose **Add role assignment (3)**. This allows you to assign specific roles to users, groups, or applications, controlling their permissions to manage resources associated with the app service.

   ![](../../Coach/media/bash3.png)

1. In the **Add role assignment** page, under the Role tab, choose **Job function roles (1)**. Search for **AcrPull (2)** and then select **AcrPull (3)** within this category, and then click **Next (4)** to proceed.

   ![](../../Coach/media/bash4.png)

1. From the **Members** tab, follow the steps below:

   * Under **Assign access to**, select **Managed identity (1)**.
   * Click on **+ Select members (2)**.
   * On the right, under **Select managed identities**, choose **Machine learning online endpoint (3)** for **Managed identity**.
   * Under **Selected members**, select **llama3-1-8b-nim-endpointDID (4)**.
   * Click **Select (5)**.
   * Click **Next (6)** to continue.

      ![](../../Coach/media/bash5.png)

1. Click on **Review + assign**.

## Task 11: Create AzureML Deployment of the NIM Container

Create an AzureML deployment with the NIM container obtained from the provided Azure container registry.

1. Run the following command to **create an AzureML deployment of the NIM container**.

   ```cmd
   ./5_create_deployment.sh
   ```

   >**Note:** This action will approximately take around 20-25 Minutes.

## Task 12: Verify Your Connection

1. Return to the **Azure Portal**.

2. Open the **ml-workspace** and click on **Launch studio**.

   ![](../../Coach/media/nvverify1.png)

3. This will take you to **AML Studio**. From the left-hand menu, select **Endpoints** and choose your endpoint.

   ![](../../Coach/media/nvverify2.png)

4. Go to the **Consume** tab, then copy the **REST endpoint** and the **Primary key**.

   ![](../../Coach/media/nvverify3upd.png)

5. In VS Code, open the **`test_chat_completions.sh`** file. Replace the following headers `<your-azureml-endpoint>`, `<your-azureml-endpoint-token>`, and `<deployment-name>` with the appropriate values. Ensure the **deployment-name** matches the one in your `config.sh` file and save the file.

   >**Note:** Ensure to add **/v1/chat/completions** towards the end of the endpoint.

   >**Note:** Ensure that the model name is **meta/llama3-8b-instruct**

6. Once you have updated all the headers, the code should look similar to the following:

   ```
   #!/bin/bash
   curl -X 'POST' \
     'https://llama-3-8b-nim-endpoint<SUFFIX>.eastus2.inference.ml.azure.com/v1/chat/completions' \
     -H 'accept: application/json' \
     -H 'azureml-model-deployment: llama3-8b-nim-dep<SUFFIX>' \
     -H 'Authorization: Bearer 3L3s8qb6dCQq7TTgorFnwDVZT8qsvId5' \
     -H 'Content-Type: application/json' \
     -d '{
     "messages": [
       {
         "content": "You are a polite and respectful chatbot helping people plan a vacation.",
         "role": "system"
       },
       {
         "content": "What should I do for a 4 day vacation in Spain?",
         "role": "user"
       }
     ],
     "model": "meta/llama3-8b-instruct",
     "max_tokens": 500,
     "top_p": 1,
     "n": 1,
     "stream": false,
     "stop": "\n",
     "frequency_penalty": 0.0
   }'
   
   ```

1. Run the following command to verify the Connection.

   ```
   ./test_chat_completions.sh
   ```

1. You will see the output similar to the screenshot below.

   ![](../media/llama-output.png)  

### Now, click on Next from the lower right corner to move on to the next page.

![](../media/nextpage(1).png) 
