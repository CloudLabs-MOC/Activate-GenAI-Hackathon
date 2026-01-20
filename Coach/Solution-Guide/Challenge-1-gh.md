# Microsoft Azure Hackathon: Activate Generative AI with Azure Trainer Guide

<p align="right">Last updated January 20, 2026</p>

## Challenge 01: Deploy Azure OpenAI Service and LLM Models

### Estimated Time: 30 Minutes
## Introduction

Welcome to the Deploy Azure OpenAI Service Challenge! This challenge is designed to test your skills in deploying the Azure OpenAI Service and its Large Language Models (LLMs). The goal is to set up the OpenAI Service and deploy LLM models.

**Azure OpenAI Service** provides REST API access to OpenAI's powerful language models, including the GPT-4, GPT-4 Turbo with Vision, and Embeddings model series. In addition, the new `GPT-4` model series have now reached general availability.

A **Large Language Model** **(LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models use transformer models and are trained using massive datasets—hence, large. This enables them to recognize, translate, predict, or generate text or other content.

**Contoso Ltd.**, a leading technological firm, is seeking to enhance its product support operations. They receive a vast number of queries daily, which results in longer waiting times and decreased customer satisfaction. To address this, Contoso is planning to implement an AI-powered solution that can handle customer inquiries effectively and efficiently.

They have chosen to deploy Azure OpenAI Service along with its Large Language Models (LLM), like `gpt-4.1-mini` and `text-embedding-ada-002`. These models are known for their capability of processing and generating human-like text, making them ideal for this application.

As a part of this challenge, your task is to create an Azure OpenAI service and deploy Large Language Models (LLMs). The Large Language Models include **gpt-4.1-mini** and **text-embedding-ada-002**.

## Description

Your task is to deploy the Azure OpenAI Service and deploy Large Language Models (LLM).

### Accessing the Azure portal

>**Important:** You can find the Username and Password within the environment by navigating to the **Environment** tab in the left pane then copy the **Azure Username** and **Azure Password**, which will be required for signing into the Azure portal in later steps and you can record the **Deployment Id**, which can be used to provide a unique name to the resources during deployment.

>**Note:** Numbers and ID values may vary. Kindly ignore values in screenshots and copy values from the **Environment** tab.

 ![](../media/Update-10.png)

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
- [Microsoft Foundry](https://aka.ms/oai/access) access is available with the following models:
  - gpt-4.1-mini
  - text-embedding-ada-002

## Solution Guide

## Task 1: Deploy Microsoft Foundry Service

In this task, you'll learn the process of setting up and deploying the Azure OpenAI service within the Azure Portal.

1. On the Azure Portal page, in Search resources, **services and docs (G+/) box** at the top of the portal, enter **Microsoft Foundry** **(1)**, and then select **Microsoft Foundry** **(2)** under Services.

   ![](../media/image-5.png)

1. From the left navigation pane, expand **Use with Foundry (1)**, click on **Foundry (2)** and then select **+ Create (3)** from the menu bar.

   ![](../media/image-4.png)

1. Specify the following details to deploy the Foundry service and click **Review + create** **(6)** thrice.

   | **Option**         | **Value**                                              |
   | ------------------ | -----------------------------------------------------  |
   | Subscription       | Leave default **(1)**                                         |
   | Resource Group     | **Activate-GenAI** **(2)**                 |
   |Name                | Use the format **Foundry-xxxxxx** **(3)**  (replace **xxxxxx** with the **Deployment ID**) |
   | Region             | Use the same location as the resource group **(4)**           |
   | Default project name | **proj-xxxxxx** **(5)** (replace **xxxxxx** with the **Deployment ID**) | 

   > **Note:** Here, xxxxxx refers to the **deployment ID** which you recorded in last task.

     ![](../media/image-1.png)

1. Once validation is successful on the **Review + create** tab, click on **Create**.

   ![](../media/image-2.png)

1. Wait for the deployment to be completed, and then **click on Go to resource**. 

1. On the Overview pane, click on Go to Foundry portal to navigate to the Microsoft Foundry portal.

1. Once you are in the Microsoft Foundry portal, locate the New Foundry option and switch the toggle to Enabled.

## Task 2: Deploy a model

Azure OpenAI provides a web-based portal named Azure AI Foundry, which you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using Azure AI Foundry to deploy a model.

1. On the Azure Portal page, in Search resources, **services and docs (G+/) box** at the top of the portal, enter **Microsoft Foundry** **(1)**, and then select **Microsoft Foundry** **(2)** under Services.

   ![](../media/image-5.png)

1. From the left navigation pane, click **Foundry** **(1)**. On the **Microsoft Foundry | Foundry** blade, select **Foundry-<inject key="Deployment-id" enableCopy="false"></inject>** **(2)**.

   ![](../media/image-6.png)

1. In the Foundry resource pane, from the Overview section, click on **Go to Foundry portal** to navigate to the **Microsoft Foundry portal**. 

   ![](../media/image-3.png)

   > **Note:** If the pop-up Discover an even better Azure AI Studio experience appears, click Close to dismiss it.

1. Once you are in the **Microsoft Foundry** portal, locate the **New Foundry** option and switch the toggle to **Enabled**.

   ![](../media/image-7.png)

1. In the **Microsoft Foundry** portal, select **Discover (1)** from the top left corner, click **Models (2)** from left pane. In the search bar, search for **gpt-4.1-mini (3)** and select **gpt-4.1-mini (4)**.

    ![](../media/image-8.png)

1. On the **gpt-4.1-mini** page, click on **Deploy (1)** and select **Custom Settings (2)** from the dropdown.

    ![](../media/image-9.png)

1. Within the Deploy model pop-up interface, click on **Customize** and enter the following details:
  
   - Deployment name: **text-turbo** **(1)**
   - Deployment type: **Standard** **(2)**
   - Model version: **2024-08-06 (Default)** **(3)**   
   - Model version upgrade policy: **Upgrade once new default version becomes available** **(4)**
   - Enable dynamic quota: **Enabled** **(5)**   
   - Tokens per Minute Rate Limit (thousands): **20K** **(6)**
   - Click on **Deploy** **(7)**.

     ![](../media/image-10.png)

1. In the **Microsoft Foundry** portal, select **Discover (1)** from the top left corner, click **Models (2)** from left pane. In the search bar, search for **text-embedding-ada-002 (3)** and select **text-embedding-ada-002 (4)**.

   ![](../media/image-11.png)

1. On the **text-embedding-ada-002** page, click on **Deploy (1)** and select **Custom Settings (2)** from the dropdown.

   ![](../media/image-13.png)   

1. Within the Deploy model pop-up interface, click on **Customize** and enter the following details:

   - Deployment name: **text-ada-002** **(1)**
   - Deployment type: **Standard** **(2)**
   - Model version: Use the default version **2** **(Default)** **(3)**
   - Enable dynamic quota: **Enabled** **(4)**   
   - Tokens per Minute Rate Limit (thousands): **20K** **(5)**
   - Click on **Deploy** **(6)**
        
     ![](../media/image-12.png)

1. Back on the **Deployments** **(1)** page, you should see the deployment models **text-turbo** and **text-ada-002** created **(2)**.

1. In the **Microsoft Foundry** portal, select **Build (1)** from the top left corner, click **Models (2)** from left pane and you should see the deployment models **text-turbo** and **text-ada-002** created **(3)**.

   ![](../media/image-14.png)

## Success Criteria:

- Successful deployment of the Foundry Service.

- Deploying Large Language Models (LLM) with the OpenAI Service.

## Additional Resources:

- Refer to the [Microsoft Foundry Service documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-foundry?view=foundry) for guidance on deploying the service.

### Now, click on Next from the lower right corner to move on to the next page.

![](../media/nextpage(1).png)

