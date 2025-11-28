# Microsoft Azure Hackathon: Activate Generative AI with Azure Trainer Guide

<p align="right">Last updated November 24, 2025</p>

## Challenge 01: Deploy Azure OpenAI Service and LLM Models

### Estimated Time: 30 Minutes
## Introduction

Welcome to the Deploy Azure OpenAI Service Challenge! This challenge is designed to test your skills in deploying the Azure OpenAI Service and its Large Language Models (LLMs). The goal is to set up the OpenAI Service and deploy LLM models.

**Azure OpenAI Service** provides REST API access to OpenAI's powerful language models, including the GPT-4, GPT-4 Turbo with Vision, and Embeddings model series. In addition, the new `GPT-4` model series have now reached general availability.

A **Large Language Model** **(LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models use transformer models and are trained using massive datasets—hence, large. This enables them to recognize, translate, predict, or generate text or other content.

**Contoso Ltd.**, a leading technological firm, is seeking to enhance its product support operations. They receive a vast number of queries daily, which results in longer waiting times and decreased customer satisfaction. To address this, Contoso is planning to implement an AI-powered solution that can handle customer inquiries effectively and efficiently.

They have chosen to deploy Azure OpenAI Service along with its Large Language Models (LLM), like `gpt-4o` and `text-embedding-ada-002`. These models are known for their capability of processing and generating human-like text, making them ideal for this application.

As a part of this challenge, your task is to create an Azure OpenAI service and deploy Large Language Models (LLMs). The Large Language Models include **gpt-4o** and **text-embedding-ada-002**.

## Description

Your task is to deploy the Azure OpenAI Service and deploy Large Language Models (LLM).

### Accessing the Azure portal

>**Important:** You can find the Username and Password within the environment by navigating to the **Environment** tab in the left pane then copy the **Azure Username** and **Azure Password**, which will be required for signing into the Azure portal in later steps and you can record the **Deployment Id**, which can be used to provide a unique name to the resources during deployment.

>**Note:** Numbers and ID values may vary. Kindly ignore values in screenshots and copy values from the **Environment** tab.

 ![](../media1/Active-image19updnew.png)

1. To access the Azure portal, within labvm open **Microsoft Edge** and browse to the [Azure Portal](https://portal.azure.com/).

1. In the **Sign in to Microsoft Azure** window, enter the following **Email/Username** **(1)**, and then click on **Next** **(2)**.
   
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

     ![](../media/Active-image1.png)

1. Now enter the following **Password** **(1)** and click on **Sign in** **(2)**.

   - **Password:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/password(1).png)

1. When **Action Required** window pop up, click on **Ask Later**.

    ![](../media/Active-image3.png)
   
1. If you see the pop-up **Stay Signed in?**, click **No**.

    ![](../media/Active-image4.png)

1. If a **Welcome to Microsoft Azure** pop-up window appears, click **Cancel** to skip the tour.

    ![](../media/Active-image5.png)

## Prerequisites

- [Azure Subscription](https://azure.microsoft.com/en-us/free/)
- [Azure OpenAI](https://aka.ms/oai/access) access is available with the following models:
  - gpt-4o
  - text-embedding-ada-002

## Solution Guide

## Task 1: Deploy an Azure Open AI Service

In this task, you'll learn the process of setting up and deploying the Azure OpenAI service within the Azure Portal.

1. On the Azure Portal page, in Search resources, **services and docs (G+/) box** at the top of the portal, enter **Azure OpenAI** **(1)**, and then select **Azure OpenAI** **(2)** under Services.

   ![](../media/searchopai(1).png)

1. On the **Microsoft Foundry | Azure OpenAI** **(1)** blade, click on **+ Create** **(2)**, and from the drop down select **Azure OpenAI** **(3)**.

   ![](../media/c1.step2new.png)

1. Specify the following details to deploy the Azure Open AI service and click **Next** **(6)** thrice.

   | **Option**         | **Value**                                              |
   | ------------------ | -----------------------------------------------------  |
   | Subscription       | Leave default **(1)**                                         |
   | Resource Group     | **ODL-GenAI-CL-XXXXXXX-01** **(2)**                 |
   | Region             | Use the same location as the resource group **(3)**           |
   | Name               | Use the format **OpenAI-xxxxxx** **(4)**  (replace **xxxxxx** with the **Deployment ID**) |
   | Pricing tier       | **Standard S0** **(5)**                                        | 

   > **Note:** Here, xxxxxx refers to the **deployment ID** which you recorded in last task.

     ![](../media/act1.png)

1. Once validation is successful on the **Review + submit** tab, click **Create** and wait for the deployment to complete.

   ![](../media/act2.png)

## Task 2: Deploy a model

Azure OpenAI provides a web-based portal named Azure AI Foundry, which you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using Azure AI Foundry to deploy a model.

1. On the Azure Portal page, in the Search resources, services and docs** **(G+/) box at the top of the portal, enter **Azure OpenAI** **(1)**, and then select **Azure OpenAI** **(2)** under services.

   ![](../media/searchopai(1).png)

1. From the left navigation pane, click **Azure OpenAI** **(1)**. On the **Microsoft Foundry | Azure OpenAI** blade, select **OpenAI-<inject key="Deployment-id" enableCopy="false"></inject>** **(2)**.

   ![](../media/c1.task2,step2new.png)

1. In the Azure OpenAI resource pane, from the Overview section, click on **Go to Foundry portal** to navigate to the **AI Foundry portal**. 

   ![](../media/a19new.png)

   > **Note:** If the pop-up Discover an even better Azure AI Studio experience appears, click Close to dismiss it.

1. From the left pane, click on **Deployments** **(1)** under **Shared resources**, then select **+ Deploy model** **(2)**. Next, choose **Deploy base model** **(3)**.

    ![](../media/a20new.png)

1. Search for **`gpt-4o`**, then select **gpt-4o** **(1)** and click on **Confirm** **(2)**.

    ![](../media/c1-task2.1new.png)

1. Within the Deploy model pop-up interface, click on **Customize** and enter the following details:
  
   - Deployment name: **text-turbo** **(1)**
   - Deployment type: **Standard** **(2)**
   - Model version upgrade policy: **Upgrade once new default version becomes available** **(3)**
   - Model version: **2024-08-06 (Default)** **(4)**
   - Tokens per Minute Rate Limit (thousands): **20K** **(5)**
   - Enable dynamic quota: **Enabled** **(6)**
   - Click on **Deploy** **(7)**.
        
     ![](../media/c1.task2.step6new.png)

     ![](../media/c1.task2.step6.1new.png)

     > **Note:** If the **Customize** option doesn't appear, you can enter the model deployment details directly. 

1. Again click on **Deployments** **(1)** under **Shared resources**, then select **+ Deploy model** **(2)**. Next, choose **Deploy base model** **(3)**.

   ![](../media/a201new.png)

1. Search for **text-embedding-ada-002**, select **text-embedding-ada-002** **(1)** and click on **Confirm** **(2)**.

   ![](../media/c1-task2.2new.png)

1. Within the Deploy model pop-up interface, click on **Customize** and enter the following details:

   - Deployment name: **text-ada-002** **(1)**
   - Deployment type: **Standard** **(2)**
   - Model version: Use the default version **2** **(Default)** **(3)**
   - Tokens per Minute Rate Limit (thousands): **20K** **(4)**
   - Enable dynamic quota: **Enabled** **(5)**
   - Click on **Deploy** **(6)**
        
     ![](../media/c1.task2.step9.png)
        
     ![](../media/solimage7.png)

     > **Note:** If the **Customize** option doesn't appear, you can enter the model deployment details directly. 

1. Back on the **Deployments** **(1)** page, you should see the deployment models **text-turbo** and **text-ada-002** created **(2)**.

   ![](../media/act3new.png)

## Success Criteria:

- Successful deployment of the Azure OpenAI Service.

- Deploying Large Language Models (LLM) with the OpenAI Service.

## Additional Resources:

- Refer to the [Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/) for guidance on deploying the service.

### Now, click on Next from the lower right corner to move on to the next page.

![](../media/nextpage(1).png)

