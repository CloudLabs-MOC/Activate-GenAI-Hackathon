# Desafio 05: Processamento em Lote de Documentos com Serverless

### Duração Estimada: 90 minutos

## Introdução:

Bem-vindo(a) a um desafio estratégico, onde a Contoso Ltda busca aprimorar sua aplicação de chat com IA por meio de um sistema robusto de processamento de documentos. O objetivo deste desafio é criar uma solução serverless para processar novos documentos, traduzi-los quando necessário e armazená-los de forma transparente no Azure AI Search. Dessa forma, os documentos estarão continuamente disponíveis para consumo pelo Azure OpenAI, fortalecendo a base de conhecimento e aumentando a precisão das respostas da aplicação de chat.

A partir das experiências anteriores com o balanceamento de carga de recursos do Azure OpenAI, você agora será responsável por otimizar o processamento de documentos. Isso inclui configurar serviços de tradução, construir uma arquitetura serverless para processamento em lote utilizando serviços do Azure e aproveitar tecnologias como o *Document Intelligence* (anteriormente Form Recognizer) e o Azure AI Search. Seu objetivo é garantir que documentos recém-adicionados sejam processados, analisados e indexados de forma eficiente, tornando-os imediatamente disponíveis para uso pela IA da aplicação de chat.

O desafio está estruturado em três etapas principais: tradução de idiomas, processamento serverless de documentos em lote usando serviços do Azure e utilização de recursos avançados como o *Document Intelligence* e o Azure AI Search. Primeiramente, você traduzirá arquivos para atender aos requisitos de idioma. Em seguida, implantará uma arquitetura serverless para processar documentos em lote de forma eficiente, treinando e testando modelos, estabelecendo pipelines para converter documentos para um formato compatível com o *Document Intelligence* e usando o serviço de pesquisa de IA do Azure para localizar e disponibilizar documentos no conjunto de dados processado.

Você também utilizará o *Document Intelligence* e o **Acelerador de Automação de Processos de Negócio** (*Business Process Automation* - BPA) para construir pipelines integrados entre diversos serviços do Azure, criando uma solução completa de processamento de documentos. Este desafio representa um passo fundamental rumo a uma aplicação de IA que se adapta e cresce conforme as necessidades de negócio da Contoso.

## Objetivos do Desafio:

> **Important**: Ao provisionar os serviços neste desafio, certifique-se de usar o grupo de recursos com o nome **<inject key="Resource Group Name"/>**  !

1. **Faça um fork do repositório e gere um Token de Acesso Pessoal (PAT) do GitHub.**

   - Faça um fork do repositório de Automação de Processos de Negócio para o seu GitHub: `https://github.com/CloudLabs-MOC/business-process-automation`.
   - Gere um **Token de Acesso Pessoal (PAT) do GitHub** com Nível de Token para Workflow.

2. **Implante a Infraestrutura do Azure no Portal Azure**:

   - Clique no botão "Implantar no Azure" (Deploy to Azure):

      [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FCloudLabs-MOC%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoai.json)

   - Atualize o token do repositório e a URL do repositório Git que você forkou, deixando todas as outras configurações inalteradas.

>**Observação:** Garanta que a região Principal esteja definida como EASTUS2.

3. **Configure o Armazenamento de Blobs do Azure:**
   
   - Crie contêineres obrigatórios de origem e de destino no Armazenamento de Blobs do Azure para o processamento de documentos, concedendo acesso a blobs.

5. **Inicialize o Ambiente C#/.NET para Processamento de Documentos:**
   
   - Configure um projeto C#/.NET no Visual Studio para tradução de documentos  usando a versão 7 do .NET.
   - Instale os pacotes necessários, incluindo o `Newtonsoft.Json`.

7. **Traduza Documentos e Execute o Aplicativo:**
   
   - Implemente o código para a tradução de documentos no projeto C#/.NET..
   - Execute a aplicação para traduzir todos os documentos no contêiner de armazenamento
     
   > **Observação:** Você pode encontrar os documentos em `C:\LabFiles\Documents`.

   <validation step="6936c21b-ffd6-4778-904b-25346932940b" />

**Usando a Inteligência de Documentos (Doc Intelligence):**

> **Importante**: Ao implantar serviços neste desafio, certifique-se de usar o grupo de recursos chamado  **<inject key="Resource Group Name"/>**  !

1. **Usando um recurso de Azure Document Intelligence (Form Recognizer):**
   
    - Navegue até os serviços de IA do Azure e utilize o recurso do Azure Document Intelligence (Form Recognizer).
    - Faça o upload e rotule os documentos de treinamento para treinar o modelo do Azure Document Intelligence.
      
    > **Observação:** Você pode encontrar os documentos em  C:\LabFiles\Documents.

1. **Crie um Novo Pipeline com um Módulo de Modelo Personalizado no BPA:**
   
    - Utilize o modelo treinado do Azure Document Intelligence para criar um novo pipeline no BPA.
    - Configure o pipeline para um processamento eficiente de documentos e integração com o Azure Cognitive Search.
      
    > **Dica:** Utilize um aplicativo web estático.

1. **Configure o Azure AI Search:**
   
    - Conecte-se ao Armazenamento de Blobs do Azure e configure a importação e indexação de dados.
    - Configure um indexador para a recuperação organizada de dados.

1. **Atualize o Modelo de Azure OpenAI para usar o Azure AI Search**
    - Atualize a implantação do seu modelo existente do Azure OpenAI para se conectar ao índice recém-criado do AI Search e teste usando o Playground do Azure OpenAI.
      
## Critérios de Sucesso:

- Tradução bem-sucedida de documentos e armazenamento no contêiner de destino do Armazenamento de Blobs do Azure.
- Configuração e utilização eficazes do recurso Form Recognizer e do pipeline do BPA.
- Configuração adequada do Azure Cognitive Search para os documentos processados.
- Validação do processamento de documentos e da funcionalidade de pesquisa usando a Aplicação de Pesquisa de Amostra no BPA.

## Recursos Adicionais:

- Consulte [tradução de documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample) para um código de exemplo que será usado para a tradução de documentos usando C#.
- Consulte [operações de Tradução de Documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/reference/rest-api-guide) para entender as APIs REST que utilizamos para a tradução de documentos.
