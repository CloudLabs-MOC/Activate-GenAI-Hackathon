# Challenge 02: Implement Document Search with Azure AI Search

### Estimated Time: 120 minutes

## Introduction:

Contoso is leveraging Azure AI Search and Azure OpenAI (GPT-3.5-Turbo) to create a document search solution that not only makes support documents easily searchable but also uses OpenAI's powerful language model to understand and process customer queries effectively. This integration will enable Contoso to provide accurate and relevant responses, thereby streamlining its support services.

Azure AI Search will be used to organize and index Contoso's large volumes of support documents, while Azure OpenAI will interpret customer queries for semantic search, improving the search results' relevance. This fusion of technologies will assist in making informed decisions and extracting vital information from unstructured data, ultimately providing a seamless information retrieval system that enhances Contoso's customer support experience.

In this challenge, you'll clone a provided repository to lay the groundwork for Azure AI Search, integrate it with Azure AI Services, and create a powerful indexer for advanced search capabilities. Finally, you'll work on refining search queries and kickstart the development of a search application that leverages both Azure AI Search and OpenAI's language model.

## Challenge Objectives:

> **Important:** When deploying services in this challenge, please make sure to use the resource group named **<inject key="Resource Group Name"/>** 

1. **Clone the Repository:**
   - Clone the repository within Visual Studio Code: `https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git`.
     > **Hint:** You can utilize the following repository: [mslearn-knowledge-mining](https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git) to explore and perform the scenarios listed below.

2. **Setup Azure Resources:**
   - Create an Azure AI Search resource with basic pricing.
   - Create an Azure AI services multi-service account with the Standard S0 SKU.
      > **Note:** Ensure to use both the Azure AI services multi-service account and the Azure AI Search resource in the same region.     
   - Create an Azure Storage Account with the Standard Tier.

3. **Prepare Document Upload:**
   - In Visual Studio Code, within the cloned repository, navigate to the 01-azure-search folder.
   - Edit the UploadDocs.cmd batch file with the required values.

4. **Execute the Upload Script:**
   - Open and examine the UploadDocs.cmd batch file using VS Code.
   - Execute the batch file to ensure that the necessary resources and files are created in Azure.
     > **Hint:** Begin by ensuring you have the proper credentials. This command will guide you through logging into your Azure account using the Azure CLI.

5. **Data Import and Indexing:**
   - Import data for AI Search using Blob Storage.
   - Configure the data source in AI Search.
      > **Hint:** Provide the existing storage account and select the container.
   - Link with Azure AI Services and customize the index.
      > **Note:** Select **Azure AI services multi-service account** resource only.
      - Skillset name: margies-skillset
      - Enable OCR → Merge into merged_content
      - Import data by selecting multiple cognitive skills, which include Extract.
   
        | Cognitive Skill | Parameter | Field name |
        | --------------- | ---------- | ---------- |
        | Extract location names | | locations |
        | Extract key phrases | | keyphrases |
        | Detect language | | language |
        | Generate tags from images | | imageTags |
        | Generate captions from images | | imageCaption |
   -  Link with Azure AI Services and customize the target index. Configure field properties according to the requirements.
      - The index as margies-index  
      - Set Key to metadata_storage_path
      - Keep Search mode at its default
      - Update only these fields—leave all others at their default settings: (Scroll right in the UI to view full table if needed).
     
          | Field name | Retrievable | Filterable | Sortable | Facetable | Searchable |
          | ---------- | ----------- | ---------- | -------- | --------- | ---------- |
          | metadata_storage_size | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_last_modified | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_name | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | metadata_author | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | locations | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | keyphrases | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | language | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |

   -  Indexer name: margies-indexer, Schedule: Once, Enable Base-64 encoding of keys.

       > **Note:** If Base-64 encoding for keys is not available during indexer setup, once the index is created, follow the steps.
         
   - Navigate to **Indexers** in the Azure AI Search resource.
   - Edit JSON and replace the fieldMappings section.

     ```json
     "fieldMappings": [
        {
         "sourceFieldName": "metadata_storage_path",
         "targetFieldName": "metadata_storage_path",
          "mappingFunction": {
              "name": "base64Encode",
              "parameters": null
         }
        }
     ]
     ```
                 
7. **Query Indexed Documents:**
   - Tweak queries to include counts and specific fields.
   - Update **modify-search.cmd** and **skillset.json** file with appropriate values.
      > **Note:** Select **Azure AI Search** and **Azure AI services multi-service account** resource only.
   - Create search components by executing **modify-search.cmd** file.
   - Query the modified index to retrieve refined and targeted information.
      > **Hint:** Refine your queries to count results, choose specific fields, configure search components, and use the updated index for detailed and focused information retrieval.

8. **Deploy & Test a Search Client Application:**
   - Install the Azure AI Search SDK package depending on your language preference.
      > **Note:** Please ensure the necessary extensions are already installed in VS Code.
   - Update the configuration files, which are the **appsettings.json** file for the C# language and the **.env** file for the Python language, with appropriate values.  
   - Update application settings and configure the web app.
   - Run the application locally to test the search functionality.
   - Verify that the search results display correctly in the application.
      > **Hint:** The application supports multiple languages; choose the one that suits your project's requirements. Adjust your application settings and configure the web application as needed. Then, run the application locally to test the search functionality before proceeding with deployment. 

     <validation step="e5e712e9-b444-4d98-b535-330d56d7e714" />
   
## Success criteria:

To successfully complete this challenge, you must:

   - Deploy the Azure Search Service and Azure Storage Account.
   - Add data to the storage account.
   - Index the documents in Azure AI Search using the Azure portal.
   - Customize the index and configure the indexer in Azure AI Search.
   - Modify and explore search components using JSON definitions.
   - Utilize the Azure AI Search SDK to create a client application for search.
   - Run the web application locally, perform searches, and refine search results effectively.

## Additional Resources:

- Refer to [What is Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) for reference.
- [What are Indexes in Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
- [Searching document text at scale using Azure Cognitive Search](https://benalexkeen.com/searching-document-text-at-scale-using-azure-cognitive-search/)
