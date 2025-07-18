# Challenge 03: Deploy an AI-Powered Chat App Using NIM

### Estimated Time: 45 minutes

## Introduction:

In this challenge, you'll deploy an AI-powered chat application specifically designed for Contoso Electronics. This app, built with React for the frontend and Python for the backend, showcases advanced features like chat and Q&A interfaces, all augmented by AI capabilities. It's an excellent opportunity for you to explore the integration of Azure OpenAI Service with the GPT-3.5 Turbo model and Azure Cognitive Search for efficient data indexing and retrieval.

This sample app is more than just a chat interface; it demonstrates the Retrieval-Augmented Generation pattern, offering a rich, ChatGPT-like experience over Contoso's own data. The app's features include trustworthiness evaluation of responses with citations, tracking of source content, data preparation, prompt construction, and orchestrating interaction between the ChatGPT model and Cognitive Search. You'll also find adjustable settings in the UX for experimentation and optional performance tracing and monitoring with Application Insights.

In this challenge, your task is to deploy this comprehensive chat solution for Contoso, allowing them to evaluate its capabilities and integrate it into their environment. The repository comes with sample data, representing a ready-to-use, end-to-end solution. This app is a valuable tool for Contoso's employees to inquire about company benefits, internal policies, job descriptions, and roles.

You will be using Bicep to deploy the chat app. 

The chat application integrates seamlessly with different Azure services to provide an intelligent user experience. Here's a simple overview of each service used by the app:

- **App Service:** This hosts the chat app, ensuring it can respond to the prompts sent by users from the uploaded relatable data.
- **Application Insights:** It proactively monitors the app's performance, taking care of issues before they become significant.
- **Document Intelligence:** Using AI, it understands the content in uploaded documents, making user information more insightful.
- **Azure OpenAI:** Enhances the app's capabilities with natural language understanding and responses.
- **Shared Dashboard:** Acts as a central hub for team collaboration and data sharing.
- **Smart Detector Alert Rule:** Monitors the app's health and notifies the team if any issues arise.
- **Search Service:** Empowers users with dynamic and efficient search functionality within the app.
- **Log Analytics Workspace:** Tracks and analyzes app activity, offering valuable insights and logs.
- **App Service Plan:** Optimizes resource allocation for optimal app performance.
- **Storage Account:** Securely stores the data that will be used by the Azure AI Search service to provide the inputs to the chat app.

Together, these services create a responsive chat application that combines AI features, monitoring capabilities, and efficient data management, providing Contoso with an exceptional user experience.

## Architecture diagram:

![](../media/Active-image258.png)

## Prerequisites

Make sure you have the following from the CloudLabs-provided integrated environment:

> Note: Prerequisites are already set up in the CloudLabs-provided environment. If you're using your personal computer or laptop, please make sure that all necessary prerequisites are installed to complete this hackathon.

  - [Azure Subscription](https://azure.microsoft.com/en-us/free/)
  - [Azure OpenAI](https://aka.ms/oai/access) access is available with the following models:
    - gpt-35-turbo
    - text-embedding-ada-002
   - Bicep 
   - Azd 
   - Poweshell 7 

## Challenge Objectives:

> **Note**: When deploying services in this challenge, please make sure to use the resource group named rg-activategenai.

> **Important** : Start Powershell 7 +.

1. **Clone the Repository:**
   - Clone the Active Gen AI repository: `https://github.com/CloudLabsAI-Azure/azure-search-openai-demo-nvidia`.
   - Verify if Bicep is installed on your machine. If not, follow the [Bicep installation guide](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/install)).

2. **Deploy the AI-Powered Chat App:**

    - Deploy an AI-powered chat application on Azure, integrating Azure AI services and Azure Search, and ensuring it's accessible and functional post-deployment.

   - Provide the name of the environment as **activategenai** when prompted.
    
      > Hint : Begin by ensuring you have the proper credentials. This command will guide you through logging into your Azure account using the Azure Developer CLI. Once authenticated, you'll have access to your Azure resources.
    
      > Hint : Initialize your project with a specific template. This command will help you set up your project environment

      > Hint : Launch your project into action. This command will deploy your application to Azure, setting up all necessary resources and configurations automatically.

      > Note : Ensure to re-run in case of any deployment failure with Storage Account.

        <validation step="d170a2ad-32d3-4149-ba77-caf4264a4373" />

3. **Deploying with NVIDIA NIM**

    - Along with OpenAI Large Language Models (LLMs), NVIDIA NIM along with Meta Llama 3.1 8B can be used for ChatCompletion requests.This document outlines the steps to configure the app to use NVIDIA NIM.
    - Follow the given instructions here: `https://github.com/CloudLabsAI-Azure/azure-search-openai-demo-nvidia/blob/main/docs/deploy_nvidia_nim.md`

4. **Interact with the Chat App**

Access Web Application and Query Construction and Response:
   
   - In the Azure Portal, search for **`App Services`** and select the web app you deployed in the previous challenge.
   - Click on **"Browse"** to open your web application.
 You will be prompted with the **Northwind Health chat application** as below. 

     ![](../media/lab03-04.png)

- In the chat application, provide the below prompt and check how responses are given by the ChatGPT and Azure cognitive search services by interacting to construct search queries and retrieve candidate information from the knowledge base.

   ```
   What does a Product Manager do?
   ```

- The response not only answered the question based on the content found in these documents, but it also included **citations (1)** to that content to validate the accuracy of the information. When you click on an annotation, the app jumps right to the page of the **document (2)** that goes into the comparison of the plans, so that we can read more or do additional validation on the accuracy of the answer under the **citation** section. 


- See how when we click on an annotation, the app jumps right to the page of the document that goes into the comparison of the plans, so that we can read more or do additional validation on the accuracy of the answer. 

   ```
   Does the project manager manage the human resources team?
   ```

- As per our constructed app, we can pass context from previous parts of the chat into the prompt behind the scenes, which enables ChatGPT to answer the question if the project manager manages the human resources team. Click on the citation, and you'll see the part of the plan that covers the related information.


2. Multilingual Query Capability:
   
- Let us make a slight change to the prompt to ask open AI to take any question that is not asked in English and respond in the language it was asked in. Go to **Developer Settings** and add the below message in the **Override prompt template** section. Click on **Close**.

  ```
   convert prompts to English and respond when asked questions in different language
   ```

- In this override, when we ask a question in a different language, behind the scenes, the prompt gets converted to English to perform the search, and then the model will respond in the same language it was asked in. Enter the below prompt in the chat section and observe that it's taking the question, detecting that it's in French, converting it to English, executing it as before, and then returning the expected response like before.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

3. Advanced Settings Impact:
- Go to **Developer Settings**, and in the **Exclude category** section, enable the check box for **Use query-contextual summaries instead of whole documents** and **Suggest follow-up questions**. Click on **Close** and observe how the responses to the prompt will change in the chat by giving the below prompt.

   ```
   What happens in a performance review?
   ```
   
4. OpenAI and AI Search Capabilities Exploration:
  - Conduct your own tests using various prompts to assess the range and depth of the app's conversational and search capabilities.
  - Focus on understanding how the app integrates OpenAI's model and AI Search for seamless user interactions.

5. **Interact with the Chat App with NVIDIA NIM LLM**

- In the **Developer settings** pop-up, check the box for **Use NVIDIA NIM LLM**, then click the **Close** button.

- Enter the prompt: **What does a Product Manager do?** and press Enter. You’ll notice that the Chat UI updates in green and is generated from NVIDIA LLM. Next, click on the **Show Thought Process** icon to get more details of the model used.

- Below in the **Thought Process**, you will see that the **llama-3.1-8b-instruct** model is utilized coming from the AML endpoint that you have deployed in the previous challenge.


## Success Criteria:

- Successful deployment of the Chat App.
- validate if the following services are successfully deployed in the RG (Resource Group).
  - App Service
  - Document Intelligence
  - Azure OpenAI
  - Shared Dashboard
  - Smart Detector Alert Rule
  - Search Service
  - Log Analytics Workspace
  - App Service Plan
  - Storage Account
- Validate if the data is populated into the storage container named `content`.
- The Chat app should be accessible using the Azure App service.

## Additional Resources:

-  Refer to the  [Azure Search OpenAI demo GitHub repository](https://github.com/cmendible/azure-search-openai-demo) for detailed information on the architecture.
-  [Azure copilot](https://learn.microsoft.com/en-us/azure/copilot/overview)
