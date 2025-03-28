# Challenge 06: Implement Monitoring and Logging of Azure OpenAI Using API Management Service

### Estimated Time: 90 minutes

## Introduction

Explore monitoring data collection, including activity logs and platform metrics. Configure Azure Monitor for log generation, customize data routing with diagnostic settings and initiate resource log collection. Discover Log Analytics Workspace limitations in logging user requests and model responses. Mitigate this by integrating the Azure API Management Service for comprehensive logging in the Azure OpenAI environment.

# Solution Guide

## Task 1: Monitoring the Azure OpenAI Service

When your crucial applications and business processes depend on Azure resources, it's essential to monitor their availability, performance, and operation. Azure OpenAI provides out-of-box dashboards for each of your Azure OpenAI resources. To access the monitoring dashboards, navigate to azure portal search and select the OpenAI and select one the OpenAI resource. On the overview Azure OpenAI resources you get  monitoring dashboards by clicking on **Monitor** tab.

   ![](../media/dashboard.png)

The dashboards are grouped into four categories: HTTP Requests, Tokens-Based Usage, PTU Utilization, and Fine-tuning.
- **HTTP Requests:** Dashboards that monitor OpenAI-powered services in Azure, displaying request volume, response times, errors, geographical distribution, and other metrics. They aid in understanding user interactions, pinpointing performance issues, and ensuring service reliability.
- **Tokens-Based Usage:** This category likely includes dashboards monitoring token usage in Azure OpenAI. Tokens are vital for authentication, authorization, and access control. They offer insights into creation rates, usage patterns, and lifetimes, and detect suspicious activities. Monitoring tokens is critical for AI resource security.
- **PTU Utilization:** PTU refers to Performance Tuning Units in Azure OpenAI. These dashboards monitor and optimize PTU use, showing allocation, trends, and efficiency metrics, and offering optimization suggestions. It's crucial for boosting performance and resource allocation.
- **Fine-tuning:** This category involves dashboards offering tools and insights for fine-tuning Azure OpenAI services. They include performance metrics, configurations, experiment results, and AI model optimization on Azure. They empower informed decisions for better AI performance and accuracy.

### Task 1.1: Configure Diagnostic Settings

Azure OpenAI collects the same kinds of monitoring data as other Azure resources. You can configure Azure Monitor to generate data in activity logs, resource logs, virtual machine logs, and platform metrics. Platform metrics and the Azure Monitor activity log are collected and stored automatically, which can be routed to other locations by using a diagnostic setting. Azure Monitor resource logs aren't collected and stored until you create a diagnostic setting and a Log Analytics workspace.

1. In the Azure Portal, search for and select Log Analytics.
Enter the Below details, then click **Review + Create**. Finally, select **Create** to complete the process.

   - Subscription : Select the default Subscription
   - Resource group : **ODL-GenAI-CL-XXXXXXX-01**
   - Name : **LogAnalytics-XXXXXXX**
   - Region : Select the Resourcegroup location

   ![](../media/loganalytics.png)

1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **Azure OpenAI (1)**, and then select **Azure OpenAI (2)** under services.

    ![](../media/solt1s1.png)

1. On **Azure AI Services | Azure OpenAI** blade, select **OpenAI Service** deployed previously.

   ![](../media/solt2s2.png)

1. From the Azure OpenAI resource page, under **Monitoring**, select **Diagnostic settings (1)** on the left pane. On the Diagnostic settings page, select **Add diagnostic setting (2)**.

   ![](../media/4-2.png)

1. To create a new Diagnostic Settings, on the **Diagnostic Settings** page, configure the following fields:
   
   - **Diagnostic settings name:** **OpenAI Diagnostic Setting (1)**
   - Select **Send to Log Analytics workspace (2)** - To be checked.
   - **Subscription**: Default - Pre-assigned subscription **(3)**
   - **Log Analytics Workspace:** Select the only pre-created log analytics workspace available in the subscription **(4)**.
   - Under **Logs** - Select **allLogs (5)**.
   - Under **Metrics**, select **allMetrics (6)**.
   - To save the configuration, click on **Save (7)**.

     ![](../media/Active-image225.png)

     > After the successful configuration of the diagnostic settings, you can work with metrics and log data for your Azure OpenAI resource in your Log Analytics workspace.

### Task 1.2: Use the Chat Playground to ingest additional logs

The *Chat* playground provides a chatbot interface for GPT 3.5 and higher models. It uses the *ChatCompletions* API rather than the older *Completions* API.

1. Navigate back to the Azure OpenAI service that was previously created.

1. In the Azure OpenAI resource pane, click on **Explore Azure AI Foundary portal**; it will navigate to **Azure AI Studio**.

1. Click on **Chat** under the **Playgrounds** tab in the left pane.

    ![](../media/aigen9.png)
   
1. In the **Playground** section, select the **Show setup** page, and ensure that the **text-turbo (1)** deployment is selected in the configuration pane. In the **Give the model instructions and context (2)** section, replace the current text with the following statement: `The system is an AI teacher that helps people learn about AI`. Click on **Apply changes (3)**.

   ![](../media/aigen10.png)

   

1. Scroll down, click on **+ Add Section (1)** and click on **Examples (2)**.

   ![](../media/aigen5.png)
   
1. Enter the following message and response in the designated boxes:
   
   - **User**: `What are different types of artificial intelligence?` **(1)**
          
   - **Assistant**: `There are three main types of artificial intelligence: Narrow or Weak AI (such as virtual assistants like Siri or Alexa, image recognition software, and spam filters), General or Strong AI (AI designed to be as intelligent as a human being. This type of AI does not currently exist and is purely theoretical), and Artificial Superintelligence (AI that is more intelligent than any human being and can perform tasks that are beyond human comprehension. This type of AI is also purely theoretical and has not yet been developed).`  **(2)**
          
   - Click on **Apply changes (3)** to start a new session and set the behavioral context of the chat system.

     ![](../media/aigen8.png)

     > **Note**: Few-shot examples are used to provide the model with examples of the types of responses that are expected. The model will attempt to reflect the tone and style of the examples in its own responses.
             
     > **Note**: Click on **Continue** when prompted with **Update system message?**.

       ![](../media/Active-image230.png)
          
1. Within the query box of the chat session pane, enter the text `What is artificial intelligence?`
   
1. Use the **Send** button to submit the message and view the response.

   > **Note**: You may receive a response that the API deployment is not yet ready. If so, wait for a few minutes and try again.

   > Any text that you enter in the **Completions playground** or the **Chat Completions playground** generates metrics and log data for your Azure OpenAI resource. In the Log Analytics workspace for your resource, you can query the monitoring data by using the Kusto query language.

### Task 1.3: Analyze logs using Kusto Queries

Data in Azure Monitor Logs is stored in tables, where each table has its own set of unique properties. The activity log is a type of platform log in Azure that provides insight into subscription-level events. You can view this log independently or route it to Azure Monitor Logs. In the Azure portal, you can use the activity log in Azure Monitor Logs to run complex queries with Log Analytics.

1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **Azure OpenAI (1)**, and then select **Azure OpenAI (2)** under services.

    ![](../media/solt1s1.png)

1. On **Azure AI Services | Azure OpenAI** blade, select **OpenAI Service** deployed previously.
   
1. From your Azure OpenAI resource page, under **Monitoring** on the left pane, select **Logs (1)**, and then click on the pre-created Log Analytics workspace **(2)** that was used to configure diagnostics for your Azure OpenAI resource.

    ![](../media/Active-image231.png)

1. Within the **Log Analytics workspace** page, under Overview on the left pane, select **Logs**.

   ![](../media/4-5.png)

   > The Azure portal displays a Queries window with sample queries and suggestions by default. You can close this window.

1. For the following examples, enter the Kusto query into the edit region at the top of the Query window, and then select Run. The query results are displayed below the query text.

    - This Kusto query is useful for an initial analysis of Azure Diagnostics (AzureDiagnostics) data about your resource:
      
    - This query returns a sample of 100 entries and displays a subset of the available columns of data in the logs.
      
        ```kusto
       AzureDiagnostics
       | take 100
       | project TimeGenerated, _ResourceId, Category, OperationName
        ```

1. In the query results, you can select the arrow next to the table name to view all available columns and associated data types.

   ![](../media/Active-image232.png)

1. To see all available columns of data, you can remove the scoping parameters line `| project ...` from the query:

   ```kusto
   AzureDiagnostics
   | take 100
   ```
   > **Note:** If the logs don't reflect immediately, please wait for 10–15 minutes for them to come up.

1. You can also expand the results and check for the details provided under each for more information.

   ![](../media/Active-image233.png)

## Task 2: Monitoring OpenAI prompts using Azure API Management

### Task 2.1: Configuring Azure API Management

Creating a diagnostic setting and linking Azure OpenAI to a log analytics workspace does help in capturing native logs; however, the Log Analytics workspace is incapable of logging the user request and OpenAI model response prompts. In such scenarios, the Azure API Management Service comes in handy.

1. Within the global search bar, search for and select the **API Management services**, and select it

    ![](../media/Active-image234.png)

1. Click on **+ Create**.

   ![](../media/Active-image235.png)

1. Add the following details in the **Create API Management Service** page and click on **Review + Create (9)**:

      - Subscription: **Select the default subscription (1)**

      - Resource Group: Select **ODL-GenAI-CL-XXXXXXX-01 (2)**

      - Region: **(US) East US (3)**

      - Resource Name: **apim-XXXXXXX (4)**

      - Organization Name: **Windows (5)**

      - Administrator email: **Email/Username**: <inject key="AzureAdUserEmail"></inject> (6)

      - Pricing Tier: Select **Standard (99.95% SLA) (7)**

      - Unit(s): **1 (8)**
    
        ![](../media/Active-image257.png)
      
        ![](../media/aigen7.png)

1. On **Review + Create** tab once validation passed click on **Create**.

   > **Note**: Before proceeding with next step make sure **API Management Service** deployed successfully.

   > **Note**: The deployment of API Management service resource could take approximately 20 minutes. 

1. Once **API Management Service** deployed successfully, click on **Go to resource**.

1. On **API Management service** blade, from left navigation pane under **Security** select **Managed identities** then on **System assigned** tab set the status to **On** and click on **Save**.

    ![](../media/ai5.png)

1. Click on **Yes** when **Enable system assigned managed identity** when prompted.

   ![](../media/Active-image241.png)
   
1. Please sign out and then sign back in to the Azure portal before proceeding with the next steps.
        
1. On Azure Portal page, in Search resources, services and docs (G+/) box at the top of the portal, enter **Azure OpenAI (1)**, and then select **Azure OpenAI (2)** under services.

    ![](../media/solt1s1.png)

1. Select the **OpenAI Service** deployed in the previous challenge.

1. To capture the values of Azure OpenAI's key and endpoint, execute the following steps:
   
    - Select **Keys and Endpoints (1)** under the **Resource Management** section from the left navigation pane.
    - Click on **Show Keys (2)**.
    - Copy **Key 1 (3)** and ensure to paste it into a text editor such as Notepad for future reference.
    - Finally, copy the **Endpoint (4)** API URL by clicking on **Copy to clipboard**. Paste it in a text editor such as Notepad for later use.

      ![](../media/k&e.png "Create Azure OpenAI resource")
   
1. In the **OpenAI**, select **Access control (IAM)** **(1)**, click on **+ Add** **(2)**, and select **Add role assignment** **(3)**.

   ![](../media/apinew2.png)   

1. In **Add role assignment** tab in the search bar search and select **Cognitive Services User** and click on **Next**.

   ![](../media/apinew3.png)

1. In the **Members** tab, select **Managed identity** **(1)**, click on **+ Select Members** **(2)** in the select managed identity pop-up under Managed identity the drop-down select **API Management service** **(3)**, select the **apim-<inject key="Deployment ID" enableCopy="false"/>** **(4)**, then click-on **Select** **(5)** and click on **Next** **(6)**.

   ![](../media/apim-role.png)

1. In the **Review + assign** tab click on **Review + assign**.

1. In the API Management service, click on **APIs** **(1)** under APIs from the left menu and select **HTTP** **(2)** under Define a new API to create an HTTP API.

    ![](../media/lab3-t1-s2.png)

1. Enter the following values in the Create an HTTP API pane:
   
      | **Parameter**           | **Values**           | 
      | ----------------------- | -------------------- | 
      | API Type **(1)**        | **Basic**            | 
      | Display name **(2)**    | **miyagi-api**       |
      | Name **(3)**            | **miyagi-api**       |
      | Web service URL **(4)** | Enter the Endpoint of Azure OpenAI Endpoint |
      | API URL suffix **(5)**  | **openai** |
      | Click on  **(6)**       | **Create** |

      ![](../media/apim1.png)

1. In the API Management service, click on **APIs** **(1)**, click on the **three dots** **(2)** next to miyagi-api, select **Import** **(3)**, and click on **OpenAPI** **(4)**.

   ![](../media/api-openi-import.png)

1. Within the **Import from OpenAPI specification** pop-up window, enter and configure the following details:
   
    - **OpenAPI specification:** `https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json` **(1)**
    - **Import method:** Select **Update (2)**
    - Click on **Import (3)** to update the existing API with the above OpenAPI specification.

      ![](../media/import-api-2.png)

      > **Note:**  The OpenAPI specification is a JSON file that contains the API specifications of Azure OpenAI. You can have a detailed look at the specifications by accessing the above-provided link for a deeper understanding and clarity.

1. Click on the newly added API and observe the presence of multiple POST operations based on the OpenAPI specification that was provided earlier.

    ![](../media/post-operations.png)

1. In the **Azure OpenAI Service API** API navigate to the **Settings** **(1)** tab and update the subscription key **Header Name** to **api-key** **(2)** and click on **Save** **(3)**.

    ![](../media/azure-open-api-setting.png)

1. In the API Management service, click on **Products** **(1)** under APIs from the left menu and click on **+ Add** **(2)**.

    ![](../media/api-product1.png) 

1. In the **Add product** display name as **OpenAi** **(1)**, description as **OpenAI** **(2)**. Under the APIs menu click the **plus sign** **(3)** select the **Azure OpenAI Service API** **(4)** hit Enter and click on **Create** **(5)**.

     ![](../media/api-product2.png)

1. In the API Management service, click on **Subscriptions** **(1)** under APIs from the left menu and click on **+ Add subscription** **(2)**.

    ![](../media/api-product3.png)

1. In the **Add subscription**, enter the Name as **aoai-test** **(1)**, enter Display name as **AOAI Test** **(2)**, and click on **Create** **(3)**.

    ![](../media/api-product4.png)

1. To create a new policy with specific parameters, follow the below instructions:
    
    - Select **All Operations (1)**.
    - Within the Inbound processing tile, click on the ellipses **(2)** adjacent to the **base** policy.
    - Click on **Code editor (3)**.
   
      ![](../media/allop.png)

1. In the code editor copy the below policy to overwrite the **inbound** **(1)** tags only, replace **&lt;&lt;Azure_OpenAI_Endpoint&gt;&gt;** **(2)** of API manager which you copy in Task 1 Step 4 and click on **Save** **(3)**.

      ```
      <inbound>
         <base />
         <set-header name="api-key" exists-action="delete" />
         <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
         <set-header name="Authorization" exists-action="override">
            <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
         </set-header>
         <set-backend-service base-url="https://<<Azure_OpenAI_Endpoint>>/openai" />
      </inbound>
      ```

      ![](../media/gen28.png)
   
      ![](../media/gen29.png)

      > **Note**: Please ensure to paste the **OpenAIEndpoint** values and eliminate any duplication of **https://**.
    
1. Click on **Save**. Notice that a new policy named **set-backend-service** has been added within the inbound processing tile.
    
1. Navigate to **Diagnostic settings** in the left pane of the API management service. Click on **+ Add Diagnostic setting**.

    ![](../media/diag3.png)

    - **Diagnostic setting name** :  Provide any Unquie name **(1)**
    - **Category groups** : Select check box for both **Audit** and **allLogs** **(2)**.
    - **Metrics** : Select check box for **AllMetrics** **(3)**
    - **Destination details** : Select check box **Send to Log Analytics workspace** **(4)**
    - **Subscription** : Select existing **Subscription** **(5)** make sure to select log Analytics workspace
    - **Log analytics workspace** : make sure to select **log Analytics workspace** **(6)**
    - Click on **Save (7)**.

      ![](../media/Active-image256.png)
    
1. Now that the API has been successfully added, it requires configuration to call the OpenAI API through the API Management Service, which can be done by following the below steps:

    - Select the newly added API **(1)**.
    - Click on the **Settings (2)** tab.
    - Click on the **Azure Monitor (3)** tab under the **Diagnostics Logs** section. Check the box for **Override-global**.
    - Set the **Number of payload bytes to log (up to 8192)** to **8192 (4)**.
    - Click on **Save (5)**.

      >**Note:** It might take 15-20 minutes for the **Override global** option to appear under **Azure Monitor**.
      
      ![](../media/diag-logs-configs-1.png)
      
### Task 2.2: Test the API to create completions for chat message

1. To run a POST operation to test the functionality of the added API:

    - Select the Azure OpenAI Service API **(1)**.
    - Click on the **Test (2)** tab.
    - Click on the POST operation that **Creates a completion for the chat message (3)**.
    - Under the **Template parameters** section, enter the following details:
        - **deployment-id:** Provide the name you had provided earlier for **gpt-35-turbo** model **(4)**
        - **api-version:** 2023-03-15-preview **(5)**
    - Within the **Request body** section, edit the content **(6)** of the sample with the following prompt:
      
        ```
        {"model":"gpt-35-turbo","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
        ```
    - Click on **Send (7)**.

      ![](../media/test-api-1.png)
   
      ![](../media/test-api-2.png)

3. Notice the **HTTP response** that is generated with the reply under the **message** tab:

   ![](../media/http-response.png)

### Task 2.3: Analyze OpenAI logs using Kusto Queries within the API Management Service

> **DISCLAIMER:** Please note that it might take an hour or two for the Log Analytics Workspace to display results after a query. To ensure smooth execution and to save time, we've included screenshots of the results for better clarity and understanding. 

1. Once OpenAI requests begin to log to the Azure Monitor service, you can begin to analyze the service usage using Log Analytics queries.

2. Navigate back to the API Management Service and click on **Logs** under the **Monitoring** section.

   ![](../media/apim-logs.png)

3. Within the **New Query 1** tab, draft a new query such that:
   
    - The table should be named **ApiManagementGatewayLogs**.
    - The **BackendResponseBody** field contains the JSON response from the OpenAI service, which includes the text completion as well as the token and model information.
    - Paste the below query within the query editor to identify token usage by IP model:
      
    ```
    ApiManagementGatewayLogs
    | where tolower(OperationId) in ('completions_create','chatcompletions_create')
    | where ResponseCode  == '200'
    | extend modelkey = substring(parse_json(BackendResponseBody)['model'], 0, indexof(parse_json(BackendResponseBody)['model'], 
    '-', 0, -1, 2))
    | extend model = tostring(parse_json(BackendResponseBody)['model'])
    | extend prompttokens = parse_json(parse_json(BackendResponseBody)['usage'])['prompt_tokens']
    | extend completiontokens = parse_json(parse_json(BackendResponseBody)['usage'])['completion_tokens']
    | extend totaltokens = parse_json(parse_json(BackendResponseBody)['usage'])['total_tokens']
    | extend ip = CallerIpAddress
    | where model !=  ''
    | summarize
        sum(todecimal(prompttokens)),
        sum(todecimal(completiontokens)),
        sum(todecimal(totaltokens)),
        avg(todecimal(totaltokens))
        by ip, model
    ```

      ![](../media/apim-query.png)

5. Click on **Run** and notice the result, which defines the token usage based on the given prompt and response.

   ![](../media/apim-result.png)

6. Let's run another query to monitor prompt completions.
   
    - Replace the contents of the query editor with the following KQL to log the prompts **(1)**.
      
    ```
    ApiManagementGatewayLogs
    | where tolower(OperationId) in ('completions_create','chatcompletions_create')
    | where ResponseCode  == '200'
    | extend model = tostring(parse_json(BackendResponseBody)['model'])
    | extend prompttokens = parse_json(parse_json(BackendResponseBody)['usage'])['prompt_tokens']
    | extend prompttext = substring(parse_json(parse_json(BackendResponseBody)['choices'])[0], 0, 100)
    ```
    - Click on **Run (2)**.
    - Observe the intricacies of the generated result under the **Results** tab **(3)**.
  
      ![](../media/apim-result-2.png)

8. To view the logged prompts, <br>

- Under the **Results** tab, click on the arrow adjacent to the result that was generated using the above query to log prompts.<br>
- Scroll down and observe the Key-Value pairs of **RequestBody** and **ResponseBody**.

   ![](../media/apim-result-3.png)
   
   ![](../media/apim-result-4.png)

   >**Note:** If you get the following error, It will take some time to reflect.

   ![](../media/image.png)

## Success Criteria:

Participants will be evaluated based on the following criteria:

1. Successfully configure the Azure OpenAI service with appropriate diagnostic settings and analyze its logs using Kusto Queries.
2. Effectively create and configure Azure API Management, ensuring clear visibility of logs and OpenAI prompts through detailed Kusto Query analysis.

## Additional Resources:

- Refer to [How to Configure Azure API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md) for detailed information.
- Refer to this video about [Logging & Monitoring Everything in Azure OpenAI with API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md).
- Refer to the [Kusto Queries Tutorial](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial) for detailed information.

## Proceed with the next Challenge by clicking on **Next**>>.
