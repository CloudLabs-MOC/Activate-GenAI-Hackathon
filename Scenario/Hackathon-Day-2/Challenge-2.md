# Desafio 02: Implementar Busca de Documentos com Azure AI Search

### Duração Estimada: 120 minutos

## Introdução:

A Contoso está utilizando o Azure AI Search e o OpenAI do Azure (GPT-3.5-Turbo) para criar uma solução de busca de documentos que não apenas torna os documentos de suporte facilmente pesquisáveis, mas também usa o poderoso modelo de linguagem da OpenAI para entender e processar as consultas dos clientes de forma eficaz. Esta integração permitirá que a Contoso forneça respostas precisas e relevantes, otimizando assim seus serviços de suporte.

O Azure AI Search será usado para organizar e indexar os grandes volumes de documentos de suporte da Contoso, enquanto o OpenAI do Azure interpretará as consultas dos clientes para a busca semântica, melhorando a relevância dos resultados. A integração dessas tecnologias possibilita decisões baseadas em dados e a extração de insights críticos a partir de informações não estruturadas. Isso resulta em um sistema de recuperação de informações robusto e integrado, capaz de otimizar processos e aumentar a eficiência no suporte ao cliente da Contoso

Este desafio consiste em clonar um repositório pré-configurado, estabelecer a infraestrutura do Azure AI Search e integrá-la aos Azure AI Services. Em seguida, será desenvolvido um indexador robusto para viabilizar buscas avançadas, além do refinamento de consultas, culminando na implementação de uma aplicação de busca integrada ao Azure AI Search e ao modelo de linguagem da OpenAI.

## Objetivos do Desafio:

> **Importante**: Ao implantar serviços neste desafio, certifique-se de usar o grupo de recursos  **<inject key="Resource Group Name"/>**!

1. **Clonar o Repositório:**
   - Clone o repositório dentro do Visual Studio Code: `https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git`.
     > **Dica:** Você pode utilizar o seguinte repositório, [https://github.com/MicrosoftLearning/AI-102-AIEngineer](https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git), para explorar e executar os cenários listados abaixo.

2. **Configurar os Recursos do Azure:**
   - Crie um recurso do Azure AI Search com o plano de preços Básico.
   - Crie uma conta multissserviço nos Serviços de IA do Azure utilizando a SKU Standard S0
      >**Observação:** Garanta que tanto a conta multisserviço dos Serviços de IA do Azure quanto o recurso do Azure AI Search estejam na mesma região.
   - Crie uma Conta de Armazenamento no Azure com a camada Padrão.

3. **Preparar o Upload de Documentos:**
   - No Visual Studio Code, dentro do repositório clonado, navegue até a pasta 22-create-a-search-solution.
   - Edite o arquivo de lote `UploadDocs.cmd` com os valores necessários.

4. **Executar o Script de Upload:**
   - Abra e examine o arquivo de lote `UploadDocs.cmd`usando o VS Code.
   - Execute o arquivo de lote para garantir que os recursos e arquivos necessários sejam criados no Azure.
     > **Observação:** Comece garantindo que você tenha as credenciais corretas. Este comando o guiará para fazer login na sua conta do Azure usando a CLI do Azure.

5. **Importar e Indexar Dados:**
   - Importe dados para o AI Search usando o Blob Storage.
   - Provide the name as **margies-data**.
   - Configure the data source in AI Search.
      > Hint: Provide the existing storage account and select the container.
   - Link with Azure AI Services and customize the index.
      > Note: Select **Azure AI services multi-service account** resource only.
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

       > Note: If Base-64 encoding for keys is not available during indexer setup, once the index is created fallow steps.
         
   - Navigate to **Indexers** in the Azure AI Search resource
   - Edit JSON and replace the fieldMappings section

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

6. **Consultar Documentos Indexados:**
   - Ajuste as consultas para incluir contagens e campos específicos..
   - Defina os componentes de busca.
   - Consulte o índice modificado para recuperar informações refinadas e direcionadas.
     > Dica: Refine as suas consultas para contar resultados, escolha campos específicos, configure componentes de busca e use o índice atualizado para obtenção de informações detalhadas e focadas.

7. **Provisionar e Testar uma Aplicação de Cliente de Busca:**
   - Atualize as configurações do aplicativo e configure o aplicativo web.
   - Execute o aplicativo localmente para testar a funcionalidade de busca.
   > Dica: A aplicação suporta múltiplos idiomas; escolha o que melhor atende aos requisitos do seu projeto. Ajuste as configurações da aplicação e configure a aplicação web conforme necessário. Em seguida, execute a aplicação localmente para testar a funcionalidade de busca antes de prosseguir com a implementação.

   <validation step="00185b3f-b0cd-4db1-87bf-d782f730cf95" />
   
## Critério de Sucesso:

Para concluir este desafio com sucesso, você deve:

   - Provisionar o serviço Azure Search e a Conta de Armazenamento em Azure.
   - Adicionar dados à conta de armazenamento.
   - Indexar os documentos no Azure AI Search usando o portal de Azure.
   - Personalizar o índice e configurar o indexador no Azure AI Search.
   - Modificar e explorar componentes de busca usando definições em JSON.
   - Utilizar o SDK do Azure AI Search para criar uma aplicação cliente de busca.
   - Executar o aplicativo web localmente, realizar buscas e refinar os resultados de busca de forma eficaz.

## Recursos Adicionais:

- Consulte [O que é Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) para referência.
- [O que são Índices no Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
- [Busca de texto em documentos em grande escala usando o Azure Cognitive Search](https://benalexkeen.com/searching-document-text-at-scale-using-azure-cognitive-search/)
