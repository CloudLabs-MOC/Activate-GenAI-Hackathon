# Challenge 05: Serverless Document Batch Processing

## Introduction:

Welcome to a pivotal challenge where Contoso Ltd. aims to enhance its AI-powered chat app with a robust document processing system. This challenge focuses on creating a serverless solution for processing new documents, translating them as needed, and seamlessly storing them into Azure AI Search. This system will ensure that these documents are continuously available for consumption by Azure OpenAI, enhancing the chat app's knowledge base and response accuracy.

Building on your previous achievements in load-balancing Azure OpenAI resources, you will now embark on a journey to streamline document processing. This involves setting up a translation service, creating a serverless architecture for batch processing using Azure services, and leveraging technologies like Form Recognizer and Azure AI Search. Your task is to ensure that newly added documents are promptly processed, analyzed, and indexed, making them readily available for the chat app's AI to utilize.

This challenge unfolds in three main stages: language translation, serverless document batch processing using Azure services, and leveraging advanced features like Form Recognizer and AI search. We kick things off by translating files to meet language requirements. Next, you deploy a serverless architecture, utilizing Azure services, for efficient batch processing of documents. You train and test our model, establish a pipeline to convert documents into a Form Recognizer format, and bring in Azure's AI search service to verify the presence of specific documents in the processed dataset from where they can be used by Azure OpenAI. 

You will utilize the Form Recognizer Service and the Business Process Automation (BPA) Accelerator to build pipelines across various Azure services, creating a seamless document processing solution. This challenge is a step towards realizing an AI solution that can adapt and grow with Contoso's business needs.

# Solution Guide

### Task 1: Translate the documents using Translate

In this task, you'll set up Azure resources for Azure AI Services. It includes registering providers, creating a new Azure AI service, accepting Responsible AI terms, forking a GitHub repository, generating a Personal Access Token (PAT), and deploying resources to Azure via the GitHub repository using specified parameters and configurations. 

1. On Azure Portal page, in Search resources, services, and docs (G+/) box at the top of the portal, enter **Subscriptions (1)**, and then select **Subscriptions (2)** under services.

      ![](../media/Active-image121.png)

1. Select the existing **Subscription**.

    ![](../media/Active-image122.png)

1. From the left navigation pane expand **Settings (1)** then select **Resource Providers (2)** check **Microsoft DocumentDB** status is marked as **"Registered" (3)**. 
   If marked as **NotRegistered**, select **Microsoft DocumentDB** then click **Register** from the top menu.

   **Note**: *This process may take several seconds or minutes; be sure to refresh the entire browser periodically.*

      ![](../media/Active-image123.png)       

1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **Azure AI Foundry (1)**, and then select **Azure AI Foundry (2)** under services.
 
      ![](../media/c2.foundry.png)

1. On **Azure Al services multi service account (classic) (1)** blade, click on **Create (2)**.

   ![](../media/c5.task1.1.png)

1. Specify the following details to create an **Azure AI service** then click on **Review + create (7)** tab.
   
     | **Option**         | **Value**                                              |
     | ------------------ | -----------------------------------------------------  |
     | Subscription       | Leave default  **(1)**                                 |
     | Resource Group     | **Activate-GenAI**  **(2)**        |
     | Name               | *Enter a unique name* for your search service or use the format **AI-Service-xxxxxx** (replace **xxxxxx** with Deployment ID **(3)** |
     | Location           | Use the same location as the resource group  **(4)**    |
     | Pricing tier       | Standard S0     **(5)**                                 |
     | By checking this box I acknowledge that I have read and understood all the terms below | Select the **Checkbox** **(6)**| 

   >**Note**: Here, xxxxxx refers to the deployment ID

   ![](../media/Active-image126.png)

1. Once validation is successful on the **Review + create** tab, click **Create** and wait for the deployment to complete.

    ![](../media/Active-image127.png)

1. To make sure that we have **Accepted the terms and conditions for Responsible AI**:  We must initiate the creation of a **Azure AI Services multi-service account** from the Azure portal to review and acknowledge the terms and conditions. 

    >**Note**: Reference doc: [Quickstart: Create a Cognitive Services resource using the Azure portal](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account?tabs=multiservice%2Cwindows). Once accepted, you can create subsequent resources using any deployment tool (SDK, CLI, or ARM template, etc.) under the same Azure subscription.

1. Navigate to `https://github.com/CloudLabs-MOC/business-process-automation` and click on **Sign in** then provide your personal **GitHub Username** and **Password** then click **Sign in**.

    ![](../media/Active-image128.png)

    ![](../media/Active-image129.png)
    
1. Once signed in, select **fork (1)** to fork the repository then on **Create a new fork** click **Create fork (2)**.
   
    ![](../media/Active-image130.png)

   ![](../media/Active-image131.png)

1. Click on your **profile** which is at the top of your right hand, and then select **Settings**.

    ![](../media/Active-image132.png)
   
1. Scroll down to the complete bottom and select **Developer settings**.

    ![](../media/Active-image133.png)

1. From the left navigation pane, expand **Personal access tokens (1)** and select **Tokens (classic) (2)**. On the **Personal access tokens** page, click **Generate new token (3)** and then choose **Generate new token (classic) (4)**.

      ![](../media/c5.task1.2.png)

      >**Note:** If a prompt appears asking for your GitHub credentials while creating the PAT (Personal Access Token), enter your GitHub account password when prompted.

1. Provide the following details:

   - Note: **PAT (1)**
   - Expiration: **7 days (2)**
     
     ![](../media/Active-image135.png)

   - Select scopes: Select all the scopes **repo, workflow, write:packages, delete:packages, admin:org, admin:public_key, admin:repo_hook, admin:org_hook, gist,notifications, user, delete_repo, write:discussion, admin:enterprise, audit_log, codespace, copilot, project, admin:gpg_key, admin:ssh_signing_key** and click on **Genearte token**.

      ![](../media/Active-image138.png)

      ![](../media/Active-image139.png)

      ![](../media/Active-image140.png)

   >**Reference link**: [Get a Workflow Level Token (Classic)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1. Copy the **PAT token** and paste it in a notepad.

      ![](../media/gen37.png)
   
1. Click on the "Deploy to Azure" button that corresponds to your environment.

     ### With OpenAI
      [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FCloudLabs-MOC%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoai.json)

1. Custom deployment blade, specify the following and others parameters can keep default values.

   - Resource Group : **Activate-GenAI**
   - Repository Token : Paste the PAT token which you created and recorded in previous step.
   - Repository Url : Paste the **Forked Github account** url

      ![](../media/gen39.png)
  
      >**Note**: Ensure the primary region is set to EASTUS2
      
       ![](../media/gen47.png)
     
     >**Note**: (you can get URL by click on profile from right corner then select **Your repositories** click on **business-process-automation** and from top bar copy the **Github account** url)
     
     ![](../media/Active-image141.png)

1. Click on **Review + Create**, followed by **Create**.

1. Wait for the deployment to get complete and click on **Go to resource group**.    

1. Verify that all the resources are deployed without any issues.
   
   ![](../media/d005-1.png)
   
#### Task 1.2 - Create Azure Blob Storage containers

In this task, you'll learn how to create a container in an existing storage account where the documents that need to be searched are stored.

1. On Azure Portal page, in **Search resources, services and docs (G+/)** box at the top of the portal, enter **Storage account**, and then select **Storage account** under services.

1. Select the storage account that is created from the resources that were deployed in the previous task.

1. In the storage account overview blade, expand **Settings(1)** select **Configuration (2)**, **Enabled** the **Allow the blob anonymous access (3)** and click on **Save (4)**.

      ![](../media/Active-image146.png)

1. Expand **Data Storage (1)** select on **Containers (2)** from the left navigation pane, select **+ Container (3)**.

    ![](../media/Active-image147.png)
  
1. On the **New container** blade provide the name as **source (1)** then for **Anonymous access level** select **Blob (anonymous read access for blobs only) (2)** and click on **Create (3)**.

     ![](../media/Active-image148.png)

1. Click on the **source** container.

     ![](../media/Active-image149.png)
   
1. From the left navigation pane expand **Settings(1)** then select **Shared Access Tokens(2)**. From the **Permission** drop down select **Read(3)** and **List(4)** then click on **Generate SAS token and URL(5)**.

      ![](../media/Active-image150.png)

1. After clicking **Generate SAS token and URL** scroll down then copy the **Blob SAS URL**.

    ![](../media/Active-image151.png)
   
1. Repeat the same steps number from 1 - 8 by creating another container with name **target** by giving **Write** and **List** permissions.

1. Navigate to the source container and click on **Upload**.

   ![](../media/c5.task1-2.1.png)

1. Click on **Browse for files**.

    ![](../media/Active-image154.png)

1. Within in **File Explorer** navigate to `C:\LabFiles\Documents` and select **document-translation-sample** file click on **Open** to upload the file.

    ![](../media/Active-image155.png)

1. Back on **Upload blob** blade make sure **document-translation-sample** file is selected then click on **Upload**.

    ![](../media/Active-image156.png)

#### Task 1.3 - Set up your C#/.NET environment and install Newtonsoft.Json

In this task, we will set up a C#/.NET environment in Visual Studio 2022. We'll create a new console application named "document-translation-qs" using .NET 7.0 and install the Newtonsoft.Json package via NuGet for managing JSON operations within our project.
   
1. In the **LabVM**, in the Windows Search bar type Visual and select **Visual Studio 2022**.

   ![](../media/Active-image165.png)

   > **Note**: When prompted to sign in, select **Skip for now** then on the **Developement settings** click **Start Visual Studio**.

1. Please click on **Work or school Account** to sign in.

      ![](../media/ai3.png)   

      > **Note**: Navigate to the Environment Details tab to get the credentials.
      
1. On the Visual studio **Get Started** page, select **Create a New Project**.

   ![](../media/Active-image157.png)

1. On the **Create a new project** page, enter **console** in the search box. Choose the **Console Application** template, then choose **Next**.

    ![](../media/Active-image158.png)

1. In the **Configure your new project** dialog window, enter **document-translation-qs** in the Project name box. Then, choose **Next**.

    ![](../media/Active-image159.png)

1. In the **Additional information** dialog window, select **.NET 9.0**, and then select **Create**.

     ![](../media/net9.0.png)
    
1. Right-click on your **document-translation-qs (1)** project and select **Manage NuGet Packages (2)**.

    ![](../media/Active-image161.png)

1. Select the **Browse (1)** tab and type **NewtonsoftJson (2) (3)**.  Select the latest stable version from the drop-down menu

    ![](../media/Active-image162.png)
   
1. Click on **install** to install the package in your project.

    ![](../media/Active-image163.png)

1. Click on **Apply**.

    ![](../media/Active-image164.png)
   
#### Task 1.4 -Translate all documents into a storage container and run your application

In this task, you'll set up a Translator resource in Azure Portal, obtain its keys and endpoint, and integrate them into a C# console application in Visual Studio 2022. This application will be configured to batch-translate documents stored in an Azure Storage container using Translator service APIs.

1. On Azure Portal page, in **Search resources, services and docs (G+/)** box at the top of the portal, enter **Translator**, and then select **Translator** under services.

   ![](../media/Active-image166.png)

1. Go to the Translator resource that is created, please get the resource keys by following the next step.
   
      ![](../media/c5.task1-4.1.png)
   
1. On the left navigation pane, under **Resource Management** section, select **Keys and Endpoint (1)**. Copy and paste your **Key 1 (2)** in a convenient location, such as Microsoft Notepad. Only one key is necessary to make an API call.

     ![](../media/c5.trans.png)
   
1. Navigate back to Visual Studio 2022 and open the **Program.cs (1)** file. Delete the pre-existing code, including the line **Console.WriteLine("Hello World!") (2)**.

   ![](../media/Active-image169.png)

1. Open another tab in edge browse for [code sample](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample) then navigate to **Start asynchronous batch translation** section copy the code.

    ![](../media/Active-image170.png)

1. Paste the copied code into the Program.cs file.
    ![](../media/Active-image173.png)

1. Within Program.cs file. make the following update  

    - Update **?api-version={date}** with **?api-version=2024-05-01**.
    - Update **{your-document-translation-endpoint}** with the below value 
        ```
        https://api.cognitive.microsofttranslator.com
        ```
    - Update **{your-api-key}** with values of Translator instance which you recorded in the notepad.    
    - Also, update **"https://YOUR-SOURCE-URL-WITH-READ-LIST-ACCESS-SAS\"** and **"https://YOUR-TARGET-URL-WITH-WRITE-LIST-ACCESS-SAS\"** with values from your Storage account container instance which you recorded in notepad.
      
      ![](../media/Active-image171.png)
      
1. Once you've added the code sample to your application, choose the green Start button next to document-translation-qs to build and run your program, or press F5.
   
    ![](../media/Active-image172.png)
   
### Task 2: Creating a Form Recognizer Resource

In this task, you'll create a Form Recognizer resource in Azure Portal by setting up a new project in Document Intelligence Studio. This involves configuring project details, connecting to a training data source stored in an Azure Storage account, and validating your settings before creating the project.

1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **Azure AI Foundry (1)**, and then select **Azure AI Foundry (2)** under services.
 
      ![](../media/c2.foundry.png)


1. On the **Azure AI services multi-service account** blade, select the service that was deployed using the custom template.

     ![](../media/c5.task2.1.png)
   
1. On **Azure AI services multi-service account** blade, click on the **Document Intelligence (1)** tab and select **Go to studio (2)**.

    ![](../media/Active-image175.png)

1. In Document Intelligence Studio, scroll down to **Custom extraction models** and select **Get started**.

   ![](../media/Active-image176.png)

   >**Note:** If you're prompted to sign in to your Azure account, authenticate using the Azure account credentials.

1. Under My Project, click on **+ Create a project**.

    ![](../media/Active-image177.png)

      > **Note**: Please sign in if prompted.

1. Enter the following details and click on **Continue**  **(3)**.
    
   - Project name: **testproject** **(1)**.
   - Description: **Custom model project** **(2)**.

      ![](../media/Active-image178.png)

1. Enter the following details under **Configure service resource** and click on **Continue** **(5)**.

   - Subscription: Select your **Default Subscription** **(1)**.
   - Resource group: **Activate-GenAI**.
   - Form Recognizer or Cognitive Service Resource: Select the available Cognitive Service Form Recognizer name similar to **cogservicesbpass{suffix}** **(3)**.
   - API version: **2022-08-31 (3.0 General Availability)** **(4)**.

     ![](../media/c5.task2.2.png)

1. Enter the following details under **Connect training data source**. and click on **Continue** **(8)**.

   - Subscription: Select your **Default Subscription** **(1)**.
   - Resource group: **Activate-GenAI** **(2)**.
   - Storage account name: **Select the existing storage account (3)**.
   - Blob container name: Click on **Create new (4)** and provide the name as **custommoduletext** **(5)** then click on **OK** **(6)**.
   - Review the settings then click on **Continue** **(7)**.
   
       ![](../media/Active-image180.png)
       ![](../media/Active-image181.png)
       ![](../media/Active-image182.png)

1. Validate the information and choose **Create project**.

      ![](../media/Active-image183.png)

### Task 3: Train and label data

In this task, you'll train a Form Recognizer model by uploading, labeling, training, and testing with sample data comprising 6 training documents.

1. Click on **Browse for files**.

      ![](../media/Active-image184.png)

1.  On the file explorer, navigate to `C:\LabFiles\Documents\Custom Model Sample` (1) path, select all train JPEG files **train1 to train6 (2)**, and hit **Open** **(3)**.

      ![](../media/Active-image185.png)

1. Once uploaded, choose **Run now** in the pop-up window under Run Layout.

     ![](../media/Active-image186.png)

1. Click on **+ Add a field** **(1)**, select **Field** **(2)**, enter the field name as **Organization_sample** **(3)**, and hit **enter**.

      ![](../media/Active-image187.png)

      ![](../media/Active-image188.png)

1. Label the new field added by selecting **CONTOSO LTD** in the top left of each document uploaded. Do this for all six documents.

    ![](../media/Active-image189.png)
   
1. Once all the documents are labeled, click on **Train** in the top-right corner.

     ![](../media/Active-image190.png)

1. Specify the model ID as **customfrs** **(1)**, the model description as **custom model** **(2)**, and from the drop-down, select **Template** **(3)** as Build Mode and click on **Train** **(4)**.

    ![](../media/Active-image191.png)

1. Click on **Go to Models**. 

   ![](../media/Active-image192.png)

1. Wait until the model status shows **succeeded**. Once the status is achieved, select the model **customfrs** **(2)** you created and choose **Test** **(3)**.

     ![](../media/Active-image193.png)

1. Select the model **customfrs** **(1)** you created and choose **Test** **(2)**.

      ![](../media/Active-image194.png)
   
1. On the **Test model** window, click on **Browse for files**. 

      ![](../media/Active-image195.png)

1. On the file explorer, navigate to `C:\LabFiles\Document\Custom Model Sample` **(1)** path, select all test JPEG files **test1 and test2** **(2)**, and hit **Open** **(3)**.

     ![](../media/Active-image196.png)

1. Once uploaded, select **one test model (1)** and click on **Run analysis** **(2)**. 

     ![](../media/Active-image197.png)

1. Now you can see on the right-hand side that the model was able to detect the field **Organization_sample** we created in the last step, along with its confidence score.

    ![](../media/Active-image198.png)

### Task 4 : Build a new pipeline with the custom model module in BPA

In this task, you'll configure a new pipeline in the Business Process Automation Accelerator (BPA) to utilize a custom Form Recognizer model. This involves setting up the model ID within the pipeline stages and configuring document ingestion from specified file paths.

After you are satisfied with the custom model performance, you can retrieve the model ID and use it in a new BPA pipeline with the Custom Model module in the next step.

1. Navigate back to the Resource groups and select the resource group **Activate-GenAI**.    

1. Go to the Resource group, search, and select the **Static Web App** resource type with a name similar to **webappbpa{suffix}**.

    ![](../media/activategenai-rg-1.png)

1. On the **Static Web App** page, click on **View app in browser**.

     ![](../media/Active-image200.png)

1. Once the **Business Process Automation Accelerator** page is loaded successfully, click on **Create/Update/Delete Pipelines**. 

   ![](../media/Active-image201.png)

1. On the **Create Or Select A Pipeline** page, enter the New Pipeline Name as **workshop** **(1)**, and click on the **Create Custom Pipeline** **(2)**. 

    ![](../media/Active-image202.png)

1. On the **Select a document type to get started** page, select **PDF Document**.

    ![](../media/Active-image203.png)

1. On the **Select a stage to add it to your pipeline configuration** page, search for and select **Form Recognizer Custom Model (Batch)**.

    ![](../media/Active-image204.png)
   
1. On the pop-up, enter the model ID as **customfrs** **(1)** and click on **Submit** **(2)**. 

    ![](../media/Active-image205.png)

1. On the **Select a stage to add it to your pipeline configuration** page, scroll down to review the **Pipeline Preview** and click on **Done**.

    ![](../media/Active-image206.png)

1. On the **Pipelines workshop** page, click on **Home**. 

      ![](../media/Active-image207.png)

1. On the **Business Process Automation Accelerator** page, click on **Ingest Documents**.

     ![](../media/Active-image208.png)

1. On the **Upload a document to Blob Storage** page, from the drop-down, select a pipeline with the name **workshop** **(1)** and click on **Upload or drop a file right here**.

      ![](../media/Active-image209.png)

1. For documents, enter the following `C:\LabFiles\Document\Lab 1 Step 3.7` **(1)** path and hit enter. You can upload multiple invoices one by one.

      ![](../media/Active-image215.png)

### Task 5: Configure Azure Cognitive Search 

In this task, you'll configure Azure Cognitive Search to connect with Azure Blob Storage. This includes setting up a data source, defining parsing options for JSON files, customizing a search index for data fields, and creating an indexer to automate data ingestion and indexing processes.

1. Navigate back to the resource group window, search, and select **Search Service** with a name similar to **bpa{suffix}**.

   ![](../media/bpa4-1.png)

1. On the **Search service** page, click on **Import data**.

   ![](../media/Active-image216.png)

1. Enter the following details for **Connect to your data**.

   - Data Source: Select **Azure Blob Storage** **(1)**
   - Data Source Name: Enter **workshop** **(2)**.
   - Parsing mode: Select **JSON** **(3)**.
   - Subscription: Select the **existing one (4)**
   - Click on **Choose an existing connection** **(5)** under the Connection string.
  
     ![](../media/Active-image210.png)

1. On the **Storage accounts** page, select the storage account named similar to **bpass{suffix} (6)**. 

    ![](../media/Active-image211.png)

1. Select **results** **(7)** from the **Containers** page and click on **Select** **(8)**. It will redirect back to **Connect to your data** page.

     ![](../media/Active-image212.png)
  
1. On the **Connect to your data** page, for **Blob folder** enter  **workshop** **(9)** click on **Next : Add cognitive skills (Optional) (10)**.

    ![](../media/Active-image217.png)

1. On the **Add cognitive skills (Optional)**, click on **Skip to : Customize target index**.

1. On the **Customize target index**, enter the index name as **azureblob-index** **(1)**, make all fields **Retrievable** **(2)**, and **Searchable** **(3)**.

      ![](../media/Active-image214.png)

1. Expand the **aggregatedResults** **(1)** > **customFormRec (2)** > **documents** **(3)** > **fields** **(4)**. Under it, expand **Organization_sample (5)**. Make the three fields Facetable **(type, valueString, & content)** **(6)** and click on **Next: Create an indexer** **(7)**.

   ![](../media/Active-image218.png)

1. On the **Create an indexer** page, enter the name as **azureblob-indexer** **(1)** and click on **Submit** **(2)**.
   
    ![](../media/bpa4-10.png)

## Success Criteria:

- Successful translation of documents and storage in the Azure Blob Storage target container.
- Effective setup and utilization of the Form Recognizer resource and BPA pipeline.
- Proper configuration of Azure Cognitive Search for processed documents.
- Validation of document processing and search functionality using the Sample Search Application in BPA.

## Additional Resources:

- Refer to [document translation](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample) for sample code that will be used for document translation using C#.
- Refer to [Document Translation operations](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/reference/rest-api-guide) to understand the REST APIs that we utilize for document translation.

## Proceed with the next Challenge by clicking on **Next**>>.
