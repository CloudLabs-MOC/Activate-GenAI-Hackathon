# Challenge 04: Interact with the Chat App

### Estimated Time: 30 Minutes

## Introduction:

After successfully deploying the AI-enhanced chat app in the previous challenge, it's time to assess its capabilities. This challenge is centered around interacting with the app to understand its potential for real-world applications at Contoso Ltd. You will explore the efficiency of query responses, multilingual capabilities, and the impact of advanced settings, making a compelling business case for the integration of these technologies at Contoso.

## Challenge Objectives

**1. Access Web Application and Query Construction and Response:**
   
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

**2. Multilingual Query Capability:**
   
- Let us make a slight change to the prompt to ask OpenAI to take any question that is not asked in English and respond in the language it was asked in. Go to **Developer Settings** and add the below message in the **Override prompt template** section. Click on **Close**.

   ```
   Convert prompts to English and respond when asked questions in a different language
   ```

- In this override, when we ask a question in a different language, behind the scenes, the prompt gets converted to English to perform the search, and then the model will respond in the same language it was asked in. Enter the below prompt in the chat section and observe that it's taking the question, detecting that it's in French, converting it to English, executing it as before, and then returning the expected response like before.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

**3. Advanced Settings Impact:** 
- Go to **Developer Settings**, and in the **Exclude category** section, enable the check box for **Use query-contextual summaries instead of whole documents** and **Suggest follow-up questions**. Click on **Close** and observe how the responses to the prompt will change in the chat by giving the prompt below.

   ```
   What happens in a performance review?
   ```
4. OpenAI and AI Search Capabilities Exploration:
  - Conduct your own tests using various prompts to assess the range and depth of the app's conversational and search capabilities.
  - Focus on understanding how the app integrates OpenAI's model and AI Search for seamless user interactions.
## Success Criteria:
  - Successful interaction with the chat application, exploring a variety of conversational use cases.
  - Comprehensive understanding of the app's capabilities in handling multilingual queries, advanced settings, and its overall potential for Contoso's environment.
     
> **Important**: There is no specific validation for this challenge, but your exploration and understanding are crucial.

## Additional Resources:

- Refer to the  [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) for detailed information.
