# Challenge 01: Deploy Azure OpenAI Service and LLM Models

### Estimated Time: 30 minutes

## Introduction

**Azure OpenAI Service** provides REST API access to OpenAI's powerful language models, including the GPT-4, GPT-4 Turbo with Vision, `gpt-35-turbo`, and Embeddings model series. In addition, the new `GPT-4` and `gpt-35-turbo` model series have now reached general availability.


A **Large Language Model (LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models use transformer models and are trained using massive datasets hence, large. This enables them to recognize, translate, predict, or generate text or other content.

A **Large Language Model (LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models utilize transformer models and are trained on massive datasets—hence, the term "large." This enables them to recognize, translate, predict, or generate text or other content.


**Contoso Ltd.**, a leading technological firm, is seeking to enhance its product support operations. They receive a vast number of queries daily, which results in longer waiting times and decreased customer satisfaction. To address this, Contoso is planning to implement an AI-powered solution that can handle customer inquiries effectively and efficiently.

They have chosen to deploy Azure OpenAI Service, along with its Large Language Models (LLMs), such as `gpt-35-turbo` and `text-embedding-ada-002`. These models are renowned for their ability to process and generate human-like text, making them well-suited for this application.

As a part of this challenge, your task is to create an Azure OpenAI service and deploy Large Language Models (LLM). The LLMs include **gpt-35-turbo** and **text-embedding-ada-002**.

### Accessing the Azure portal

1. To access the Azure portal, open a private/incognito window in your browser and navigate to the Azure Portal.

1. On the **Sign in to Microsoft Azure tab**, you will see a login screen. Enter the following email/username, and then click on **Next**.

   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

1. Now enter the following password and click on **Sign in**.

   - **Password:** <inject key="AzureAdUserPassword"></inject>

1. If you see the pop-up **Stay Signed in?**, click No.

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue with the challenge.

1. If a **Welcome to Microsoft Azure** pop-up window appears, click **Maybe Later** to skip the tour.

## Prerequisites

Make sure you have the following from the CloudLabs-provided integrated environment:

> Note: Prerequisites are already set up in the CloudLabs-provided environment. If you're using your personal computer or laptop, please make sure that all necessary prerequisites are installed to complete this hackathon.

  - [Azure Subscription](https://azure.microsoft.com/en-us/free/)
  - [Azure OpenAI](https://aka.ms/oai/access) access is available with the following models:
    - gpt-35-turbo
    - text-embedding-ada-002

## Challenge Objectives:

1. **Azure OpenAI Service Deployment:**
   - Set up an Azure OpenAI Service instance with SKU size Standard `S0`.
   - Deploy it in the existing resource group named - **<inject key="Resource Group Name"/>**
   - Deploy the resource in the **East US** region.
   - Obtain the necessary Azure OpenAI Key and Endpoint.
   - Please ensure the Azure OpenAI Service name follows this format: **OpenAI-xxxxxx**, where xxxxxx should be replaced with your specific **Deployment ID**.

     <validation step="a98f394c-9dd0-4b36-85a5-85d307c3f778" />

2. **Deploy Large Language Models (LLM):**
   - Azure OpenAI provides a web-based portal named **Azure AI Foundry Portal** that you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using the Azure AI Foundry Portal to deploy a model.
   - Launch Azure AI Foundry Portal from the overview pane and deploy two OpenAI models, i.e., `gpt-35-turbo` and `text-embedding-ada-002`, with a TPM capacity of 20k.

     > **Note:** Ensure you deploy **gpt-35-turbo** model with **version : 0125**.


## Success Criteria:

- Verify that the Azure OpenAI Service is successfully deployed in the existing resource group - <inject key="Resource Group Name"/>.
- Verify that the Large Language Models (LLM), `gpt-35-turbo` and `text-embedding-ada-002`, are successfully deployed with the Azure OpenAI Service.

## Additional Resources:

- Refer to the [Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/) for guidance on deploying the service.

## Conclusion

In this challenge, you successfully deployed the Azure OpenAI service and provisioned LLM models. In the next challenge, you will connect unstructured documents to Azure AI Search and enrich them with cognitive skills for intelligent retrieval.

### Now, click on Next from the lower right corner to move on to the next page.

![](../media/nextpage(2).png)
