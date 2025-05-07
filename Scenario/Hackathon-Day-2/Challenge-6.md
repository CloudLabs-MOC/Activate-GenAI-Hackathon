# Challenge-06: Implement Monitoring and Logging of Azure OpenAI Using API Management Service

### Estimated Time: 90 minutes

## Introduction:

Building on the success of enhancing Contoso's AI-powered chat app with serverless document processing, your next objective is to operationalize these Azure OpenAI solutions with robust monitoring and logging mechanisms. In this challenge, you will delve into the intricacies of setting up and analyzing advanced monitoring systems using the Azure API Management Service and Log Analytics workspace. This is a crucial step in ensuring the smooth operation and maintenance of the AI solutions you've developed, providing valuable insights into system performance and user interactions.

Your task is to implement comprehensive monitoring for the Azure OpenAI service, leveraging diagnostic settings and Kusto queries for in-depth log analysis. Additionally, you'll be integrating the API Management Service to oversee the chat message completions and further analyze the prompts and outputs. This level of monitoring is essential for Contoso to maintain a high-quality, efficient, and user-friendly AI chat application.

## Challenge Objectives:

> **Important**: When deploying services in this challenge, please make sure to use the resource group named **rg-activategenai**

1. **Monitoring the Azure OpenAI Service:**
   - Set up diagnostic settings for the existing Azure OpenAI services.
   - Conduct log analysis utilizing Kusto Queries to monitor the service's performance and usage.
     
2. **Monitoring OpenAI prompts using Azure API Management:**
   - Utilize Kusto queries within API Management for comprehensive log analysis, focusing on chat message completions and prompt interactions.

     <validation step="6fd15003-a2d4-44d6-b213-91ca9dee3c47" />
  
## Success Criteria:

Participants will be evaluated based on the following criteria:

1. Successfully configure the Azure OpenAI service with appropriate diagnostic settings and analyze its logs using Kusto Queries.
2. Effectively create and configure Azure API Management, ensuring clear visibility of logs and OpenAI prompts through detailed Kusto Query analysis.

## Additional Resources:

- Refer to [How to Configure Azure API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md) for detailed information.
- Refer to this video about [Logging & Monitoring Everything in Azure OpenAI with API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md).
- Refer to the [Kusto Queries Tutorial](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial) for detailed information.
