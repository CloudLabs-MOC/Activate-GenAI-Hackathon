# Challenge 01: Deploy Azure OpenAI Service and LLM Models

### Estimated Time: 30 Minutes

## Introduction

**Azure OpenAI Service** provides REST API access to OpenAI's powerful language models, including the GPT-4, GPT-4 Turbo with Vision, `gpt-35-turbo`, and Embeddings model series. In addition, the new `GPT-4` and `gpt-35-turbo` model series have now reached general availability.

A **Large Language Model (LLM)** is a deep learning algorithm that can perform a variety of natural language processing (NLP) tasks. Large language models use transformer models and are trained using massive datasets—hence, large. This enables them to recognize, translate, predict, or generate text or other content.

**Contoso Ltd.**, a leading technological firm, is seeking to enhance its product support operations. They receive a vast number of queries daily, which results in longer waiting times and decreased customer satisfaction. To address this, Contoso is planning to implement an AI-powered solution that can handle customer inquiries effectively and efficiently.

They have chosen to deploy Azure OpenAI Service along with its Large Language Models (LLM), like `gpt-4o` and `text-embedding-ada-002`. These models are known for their capability in processing and generating human-like text, making them ideal for this application.

As a part of this challenge, your task is to create an Azure OpenAI service and deploy Large Language Models (LLM). The LLMs include **gpt-4o** and **text-embedding-ada-002**.

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
  - [Azure OpenAI](https://aka.ms/oai/access) access is available with the following models:
    - gpt-4o
    - text-embedding-ada-002

## Challenge Objectives:

1. **Azure OpenAI Service Deployment:**
   - Set up an Azure OpenAI Service instance with SKU size Standard `S0`.
   - Deploy it in the existing resource group named - **<inject key="Resource Group Name"/>**
   - Once the Azure OpenAI is deployed, obtain the necessary Azure OpenAI Key and Endpoint.
   - Please ensure the Azure OpenAI Service name follows this format: **OpenAI-xxxxxx**, where xxxxxx should be replaced with your specific **Deployment ID**.

     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
    - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task.
      
    - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
      
    - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
      
     <validation step="9ba9cc02-3197-449e-a583-feee9f3df4a6" />

2. **Deploy Large Language Models (LLM):**
   - Azure OpenAI provides a web-based portal named **Azure OpenAI Studio** that you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using Azure 
    OpenAI Studio to deploy a model.
   - Launch Azure OpenAI Studio from the overview pane and deploy two OpenAI models, i.e., `gpt-4o` and `text-embedding-ada-002`, with a TPM capacity of 20k.

     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
    - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task.
      
    - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
      
    - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

     <validation step="a4ef7586-7347-499d-8f5d-67e71ed0aea0" />

## Success Criteria:

- Verify that the Azure OpenAI Service is successfully deployed in the existing resource group - <inject key="Resource Group Name"/>.
- Verify that the Large Language Models (LLM), `gpt-4o` and `text-embedding-ada-002`, are successfully deployed with the Azure OpenAI Service.

## Additional Resources:

- Refer to the [Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/) for guidance on deploying the service.
