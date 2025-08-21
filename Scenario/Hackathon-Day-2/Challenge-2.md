# Desafio 02: Implementar Busca de Documentos com Azure AI Search

### Duração Estimada: 120 minutos

## Introdução:

A Contoso está utilizando o Azure AI Search e o Azure OpenAI (GPT-3.5-Turbo) para criar uma solução de busca de documentos que não apenas torna os documentos de suporte facilmente pesquisáveis, mas também usa o poderoso modelo de linguagem da OpenAI para entender e processar as consultas dos clientes de forma eficaz. Esta integração permitirá que a Contoso forneça respostas precisas e relevantes, otimizando assim seus serviços de suporte.

O Azure AI Search será usado para organizar e indexar os grandes volumes de documentos de suporte da Contoso, enquanto o Azure OpenAI interpretará as consultas dos clientes para a busca semântica, melhorando a relevância dos resultados. A integração dessas tecnologias possibilita decisões baseadas em dados e a extração de insights críticos a partir de informações não estruturadas. Isso resulta em um sistema de recuperação de informações robusto e integrado, capaz de otimizar processos e aumentar a eficiência no suporte ao cliente da Contoso

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
   - Forneça o nome `margies-data`.
   - Configure a fonte de dados (data source) no AI Search.
      >**Dica:** Forneça a conta de armazenamento existente e selecione o contêiner.
   - Vincule com os Serviços de IA do Azure e personalize o índice.
   >**Dica:** Selecione apenas o recurso de conta multisserviço dos Serviços de IA do Azure.
   - Nome do skillset: `margies-skillset`.
   - Habilitar OCR → Mesclar em `merged_content`.
   - Importe dados selecionando múltiplas habilidades cognitivas, que incluem "Extrair".
   
        | Habilidade Cognitiva | Parâmetro | Nome do Campo |
        | --------------- | ---------- | ---------- |
        | Extrair nomes de locais | | locations |
        | Extrair frases-chave | | keyphrases |
        | Detectar idioma | | language |
        | Gerar tags de imagens | | imageTags |
        | Gerar legendas de imagens | | imageCaption |
   -  Vincule com os Serviços de IA do Azure e personalize o índice de destino (*target index*). Configure as propriedades dos campos de acordo com os requisitos.
      - O índice como `margies-index`.
      - Defina a Chave para `metadata_storage_path`.
      - Mantenha o Modo de Busca (*Search mode*) em seu valor padrão.
      - Atualize apenas estes campos — deixe todos os outros com suas configurações padrão:
     
          | Nome do Campo | Recuperável | Filtrável | Classificável | Facetável | Pesquisável |
          | ---------- | ----------- | ---------- | -------- | --------- | ---------- |
          | metadata_storage_size | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_last_modified | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_name | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | metadata_author | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | locations | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | keyphrases | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | language | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |

   -  Nome do indexador: `margies-indexer`, Agendamento: **Uma vez**, Habilitar codificação Base-64 das chaves.

       > **Observação:** Se a opção de codificação Base-64 para chaves não estiver disponível durante a configuração do indexador, uma vez que o índice for criado, siga os passos abaixo.
         
   - Navegue até **Indexadores** no recurso do Azure AI Search.
   - Edite o JSON e substitua a seção `fieldMappings`:

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
   - Ajuste as consultas para incluir contagens e campos específicos.
   - Atualize os arquivos `modify-search.cmd` e `skillset.json` com os valores apropriados.
     >**Observação:** Selecione apenas os recursos do Azure AI Search e da conta multisserviço dos Serviços de IA do Azure.
   - Crie componentes de busca executando o arquivo `modify-search.cmd`.
   - Consulte o índice modificado para recuperar informações refinadas e direcionadas.
     >**Observação:** Refine suas consultas para contar resultados, escolher campos específicos, configurar componentes de busca e usar o índice atualizado para uma recuperação de informações detalhada e focada.

7. **Implantar e Testar uma Aplicação Cliente de Busca:**
   - Instale o pacote SDK do Azure AI Search de acordo com sua preferência de linguagem.
   >**Observação:** Por favor, garanta que as extensões necessárias já estejam instaladas no VS Code.
   - Atualize os arquivos de configuração, que são o arquivo `appsettings.json` para a linguagem C# e o arquivo `.env` para a linguagem Python, com os valores apropriados.
   - Atualize as configurações da aplicação e configure o aplicativo web.
   - Execute a aplicação localmente para testar a funcionalidade de busca.
   - Verifique se os resultados da busca são exibidos corretamente na aplicação.
   > **Observação:** A aplicação suporta múltiplos idiomas; escolha o que melhor se adapta aos requisitos do seu projeto. Ajuste as configurações da sua aplicação e configure o aplicativo web conforme necessário. Em seguida, execute a aplicação localmente para testar a funcionalidade de busca antes de prosseguir com a implantação.

   <validation step="00185b3f-b0cd-4db1-87bf-d782f730cf95" />
   
## Critérios de Sucesso:

Para completar este desafio com sucesso, você deve:

   - Provisionar o serviço Azure Search e a Conta de Armazenamento em Azure.
   - Adicionar dados à conta de armazenamento.
   - Indexar os documentos no Azure AI Search usando o portal do Azure.
   - Personalizar o índice e configurar o indexador no Azure AI Search.
   - Modificar e explorar os componentes de busca usando definições JSON.
   - Utilizar o SDK do Azure AI Search para criar uma aplicação cliente para a busca.
   - Executar a aplicação web localmente, realizar buscas e refinar os resultados de forma eficaz.

## Recursos Adicionais:

- Consulte [O que é Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) para referência.
- [O que são Índices no Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
- [Pesquisando texto de documentos em escala usando o Azure Cognitive Search](https://benalexkeen.com/searching-document-text-at-scale-using-azure-cognitive-search/)
