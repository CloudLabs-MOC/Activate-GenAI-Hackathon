# Challenge 01: Deploy Foundry Service and LLM Models

### Estimated Time: 30 Minutes

## Introduction

Welcome to the Deploy Microsoft Foundry Service Challenge! This challenge is designed to test your skills in deploying the Foundry Service and its Large Language Models (LLMs). The goal is to set up the Foundry Service and deploy LLM models.

**Microsoft Foundry Service** provides REST API access to OpenAI's powerful language models, including the GPT-4, GPT-4 Turbo with Vision, and Embeddings model series. In addition, the new `GPT-4` model series has now reached general availability.

A **Large Language Model** **(LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models use transformer models and are trained using massive datasets—hence, large. This enables them to recognize, translate, predict, or generate text or other content.

**Contoso Ltd.**, a leading technological firm, is seeking to enhance its product support operations. They receive a vast number of queries daily, which results in longer waiting times and decreased customer satisfaction. To address this, Contoso is planning to implement an AI-powered solution that can handle customer inquiries effectively and efficiently.

They have chosen to deploy Foundry Service along with its Large Language Models (LLMs), like `gpt-4.1-mini` and `text-embedding-ada-002`. These models are known for their capability of processing and generating human-like text, making them ideal for this application.

As a part of this challenge, your task is to create a Microsoft Foundry service and deploy Large Language Models (LLMs). The Large Language Models include **gpt-4.1-mini** and **text-embedding-ada-002**.

### Accessing the Azure portal

1. To access the Azure portal, open a private/incognito window in your browser and navigate to the Azure Portal.

1. On the **Sign in to Microsoft Azure tab**, you will see a login screen. Enter the following email/username, and then click on **Next**.

   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

1. Now enter the following password and click on **Sign in**.

   - **Password:** <inject key="AzureAdUserPassword"></inject>

1. If you see the pop-up **Stay Signed in?**, click No.

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue with the challenge.

1. If a **Welcome to Microsoft Azure** pop-up window appears, click **Cancel** to skip the tour.

## Prerequisites

Make sure you have the following from the CloudLabs-provided integrated environment:

> Note: Prerequisites are already set up in the CloudLabs-provided environment. If you're using your personal computer or laptop, please make sure that all necessary prerequisites are installed to complete this hackathon.

  - [Azure Subscription](https://azure.microsoft.com/en-us/free/)
  - [Foundry](https://aka.ms/oai/access) access is available with the following models:
    - gpt-4.1-mini
    - text-embedding-ada-002

## Challenge Objectives:

1. **Foundry Service Deployment:**
   - Set up a Foundry Service instance.
   - Deploy it in the existing resource group named - **<inject key="Resource Group Name"/>**
   - Deploy the resource in the **East US** region.
   - Please ensure the Foundry Service name follows this format: **Foundry-xxxxxx**, where xxxxxx should be replaced with your specific **Deployment ID**.

     <validation step="a98f394c-9dd0-4b36-85a5-85d307c3f778" />

2. **Deploy Large Language Models (LLM):**
   - Foundry provides a web-based portal named **Microsoft Foundry Portal** that you can use to deploy, manage, and explore models. You'll start your exploration of Foundry by using the Azure Microsoft Foundry Portal to deploy a model.
   - Launch Azure AI Foundry Portal from the overview pane and deploy two models, i.e., `gpt-4.1-mini` and `text-embedding-ada-002`, with a TPM capacity of 20k.

     > **Note:** Ensure you deploy **gpt-4.1-mini** model with **version : 2024-08-06 (Default)**.

## Success Criteria:

- Verify that the Foundry Service is successfully deployed in the existing resource group - <inject key="Resource Group Name"/>.
- Verify that the Large Language Models (LLM), `gpt-4.1-mini` and `text-embedding-ada-002`, are successfully deployed with the Azure OpenAI Service.

## Additional Resources:

- Refer to the [Microsoft Foundry Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/) for guidance on deploying the service.

## Conclusion

In this challenge, you successfully deployed the Foundry service and provisioned LLM models. In the next challenge, you will connect unstructured documents to Azure AI Search and enrich them with cognitive skills for intelligent retrieval.

### Now, click on Next from the lower right corner to move on to the next page.

![](../media/nextpage(2).png)
