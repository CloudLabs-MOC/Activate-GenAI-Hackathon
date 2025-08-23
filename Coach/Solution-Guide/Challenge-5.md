# Desafio 05: Processamento em lote de documentos sem servidor

## Introdução:

Bem-vindo(a) a um desafio estratégico, onde a Contoso Ltda busca aprimorar sua aplicação de chat com IA por meio de um sistema robusto de processamento de documentos. O objetivo deste desafio é criar uma solução serverless para processar novos documentos, traduzi-los quando necessário e armazená-los de forma transparente no Azure AI Search. Dessa forma, os documentos estarão continuamente disponíveis para consumo pelo Azure OpenAI, fortalecendo a base de conhecimento e aumentando a precisão das respostas da aplicação de chat.

A partir das experiências anteriores com o balanceamento de carga de recursos do Azure OpenAI, você agora será responsável por otimizar o processamento de documentos. Isso inclui configurar serviços de tradução, construir uma arquitetura serverless para processamento em lote utilizando serviços do Azure e aproveitar tecnologias como o *Document Intelligence* (anteriormente Form Recognizer) e o Azure AI Search. Seu objetivo é garantir que documentos recém-adicionados sejam processados, analisados e indexados de forma eficiente, tornando-os imediatamente disponíveis para uso pela IA da aplicação de chat.

O desafio está estruturado em três etapas principais: tradução de idiomas, processamento serverless de documentos em lote usando serviços do Azure e utilização de recursos avançados como o *Document Intelligence* e o Azure AI Search. Primeiramente, você traduzirá arquivos para atender aos requisitos de idioma. Em seguida, implantará uma arquitetura serverless para processar documentos em lote de forma eficiente, treinando e testando modelos, estabelecendo pipelines para converter documentos para um formato compatível com o *Document Intelligence* e usando o serviço de pesquisa de IA do Azure para localizar e disponibilizar documentos no conjunto de dados processado.

Você também utilizará o *Document Intelligence* e o **Acelerador de Automação de Processos de Negócio** (*Business Process Automation* - BPA) para construir pipelines integrados entre diversos serviços do Azure, criando uma solução completa de processamento de documentos. Este desafio representa um passo fundamental rumo a uma aplicação de IA que se adapta e cresce conforme as necessidades de negócio da Contoso.

# Guia de soluções

### Tarefa 1: Traduzir os documentos usando o Translate

Nesta tarefa, você configurará os recursos do Azure para os Serviços de IA do Azure. Isso inclui registrar provedores, criar um novo serviço de IA do Azure, aceitar os termos de IA Responsável, fazer um "fork" de um repositório do GitHub, gerar um Token de Acesso Pessoal (PAT) e implantar recursos no Azure através do repositório do GitHub usando parâmetros e configurações especificadas.

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** na parte superior do portal, digite **Assinatura (1)** e, em seguida, selecione **Assinaturas (2)** em serviços.

    ![](../media/imag001.png)

1. Selecione a **Assinatura** existente.

    ![](../media/imag002.png)

1. No painel de navegação esquerdo, expanda **Configurações (1)**, selecione **Provedores de recurso (2)** e verifique se o status do **O status do Microsoft DocumentDB** está marcado como **Registered (3)**. Se estiver marcado como **Não Registrado**, selecione **Microsoft DocumentDB** e clique em **Registrar** no menu superior.

    **Observação**: *Este processo pode levar vários segundos ou minutos; certifique-se de atualizar todo o navegador periodicamente.*

    ![](../media/imag003.png)

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** na parte superior do portal, digite **Azure AI Foundry (1)** e selecione **Azure AI Foundry (2)** em serviços.

    ![](../media/imag004.png)

1. Na lâmina **Azure Al services | Azure Al services multi-service account (classic)**, clique em **+ Criar**.

    ![](../media/imag005.png)

1. Especifique os seguintes dados para criar um serviço de IA do Azure e clique na aba **Examinar + criar (7)**.

    | **Opção** | **Valor** |
    | ------------------ | ----------------------------------------------------- |
    | Assinatura | Deixe o padrão **(1)** |
    | Grupo de recursos | **ODL-GenAI-CL-xxxxxx-Activate-GenAI** **(2)** |
      | Região | Use o mesmo local que o grupo de recursos **(3)** |
    | Nome | *Digite um nome exclusivo* para seu serviço de pesquisa ou use o formato **AI-Service-xxxxxx** (substitua **xxxxxx** por ID de implantação **(4)** |
    | Tipo de preço | Standard S0 **(5)** |
    | Ao marcar essa caixa, confirmo que li e compreendi todos os termos abaixo | Selecione a **Caixa de seleção** **(6)**|
    
    >**Observação**: aqui, xxxxxx se refere à ID de implantação.

    ![](../media/imag006.png)

1. Assim que a validação for bem-sucedida na aba **Examinar + criar**, clique em **Criar** e aguarde a conclusão da implantação.

1. Para garantir que **Aceitamos os termos e condições para a IA responsável**: devemos iniciar a criação de uma **conta multisserviço dos Serviços de IA do Azure** a partir do portal do Azure para revisar e reconhecer os termos e condições.

    >**Observação**: Documento de referência: [Início rápido: Criar um recurso de Serviços Cognitivos usando o portal do Azure](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account?tabs=multiservice%2Cwindows). Uma vez aceito, você pode criar recursos subsequentes usando qualquer ferramenta de implantação (SDK, CLI ou modelo ARM, etc.) sob a mesma assinatura do Azure.

1. Navegue até `https://github.com/CloudLabs-MOC/business-process-automation` e clique em **Sign in**, clique em **GitHub username (1)** e **Password (2)** pessoais e clique em **Sign in (3)**.

    ![](../media/Active-image128.png)
    
    ![](../media/Active-image129.png)

1. Depois de entrar, selecione **Fork (1)** para bifurcar o repositório e, em **Create a new fork**, clique em **Create fork (2)**.

    ![](../media/Active-image130.png)
    
    ![](../media/Active-image131.png)

1. Clique no seu **profile** no canto superior direito e selecione **Settings**.

    ![](../media/Active-image132.png)

1. Role até o final e selecione **Developer settings**.

    ![](../media/Active-image133.png)

1. No painel de navegação esquerdo, expanda **Personal access tokens (1)** e selecione **Tokens (classic) (2)**. Na página **Personal access tokens**, clique em **Generate new token (3)** e escolha **Generate new token (classic) (4)**.

    ![](../media/Active-image134.png)

    >**Observação:** Se for solicitado suas credenciais do GitHub ao criar o PAT (Personal access tokens), insira a senha da sua conta do GitHub.

1. Forneça os seguintes dados:

    - Note: **PAT (1)**
    - Expiration: **7 days (2)**
    
       ![](../media/Active-image135.png)

    - Selecione os escopos: Selecione todos os escopos **repo, workflow, write:packages, delete:packages, admin:org, admin:public_key, admin:repo_hook, admin:org_hook, gist,notifications, user, delete_repo, write:discussion, admin:enterprise, audit_log, codespace, copilot, project, admin:gpg_key, admin:ssh_signing_key** e clique em **Generate token**.

       ![](../media/Active-image138.png)
    
       ![](../media/Active-image139.png)
    
       ![](../media/Active-image140.png)

       >**Link de referência**: [Obtenha um token de nível de fluxo de trabalho (clássico)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1. Copie o **PAT token** e cole-o em um bloco de notas.

    ![](../media/gen37.png)

1. Clique no botão "Deploy to Azure" que corresponde ao seu ambiente.

    ### Com OpenAI
      [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FCloudLabs-MOC%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoai.json)

1. No painel de implantação personalizada, especifique o seguinte:

    - Grupo de recursos: **ODL-GenAI-CL-xxxxxx-Activate-GenAI**.
    - Repository Token : cole o token PAT que você criou e registrou na etapa anterior.
    - Repository Url : cole a URL da **conta bifurcada do Github**.
    
      ![](../media/gen39.png)

      >**Observação**: certifique-se de que a região primária esteja definida como `EASTUS2`.
    
      ![](../media/gen47.png)

      >**Observação**: (Você pode obter a URL clicando no perfil no canto direito e, em seguida, selecionar **Seus repositórios**, clicar em **business-process-automation** e, na barra superior, copiar a URL da **conta do Github**).
    
      ![](../media/Active-image141.png)

1. Clique em **Examinar + criar** e **Criar**.

1. Aguarde a conclusão da implantação e clique em **Ir para o grupo de recursos**.

1. Verifique se todos os recursos foram implantados sem problemas.

    ![](../media/d005.png)
   
#### Tarefa 1.2 - Criar contêineres do Azure Blob Storage

Nesta tarefa, você aprenderá a criar um contêiner em uma conta de armazenamento existente onde os documentos que precisam ser pesquisados ​​são armazenados.

1. No portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** na parte superior do portal, digite **Contas de armazenamento** e selecione **Contas de armazenamento**.

1. Selecione a conta de armazenamento criada a partir dos recursos que foram implantados na tarefa anterior.

1. No painel de Visão geral da conta de armazenamento, expanda **Configurações (1)** selecione **Configuração (2)**, clique em **Habilitado** na opção **Permitir acesso anônimo ao blob (3)** e, em seguida, clique em **Salvar (4)**.

    ![](../media/imag007.png)

1. Expanda **Armazenamento de dados (1)**, selecione **Contêineres (2)** no painel de navegação esquerdo, selecione **+ Contêiner (3)**.

    ![](../media/imag008.png)

1. Na página **Novo contêiner**, forneça o nome como **Source (1)** e, em **Nível de acesso anônimo**, selecione **Blob (acesso de leitura anônimo somente para blobs) (2)** e clique em **Criar (3)**.

    ![](../media/imag009.png)

1. Clique no contêiner **source**.

    ![](../media/imag0010.png)

1. No painel de navegação esquerdo, expanda **Configurações (1)** e selecione **Tokens de acesso compartilhado (2)**. No menu suspenso **Permissões**, selecione **Ler (3)** e **Lista (4)** e clique em **Gerar token SAS e URL (5)**.

    ![](../media/imag0011.png)

1. Após clicar em **Gerar token SAS e URL** role para baixo e copie o **URL de SAS do blob**.

    ![](../media/imag0012.png)

1. Repita os mesmos passos de 1 a 8 criando outro contêiner com o nome **target** dando permissões **Gravar** e **Lista**.

1. Navegue até o contêiner de `source` e clique em **Carregar**.

   ![](../media/imagn3.png)

1. Clique em **Procurar arquivos**.

    ![](../media/imagn4.png)

1. No **Explorador de Arquivos** navegue até `C:\LabFiles\Documents` e selecione o arquivo **document-translation-sample (1)**. Clique em **Abrir (2)** para carregar o arquivo.

   ![](../media/imagn5.png)

1. De volta à página **Carregar blob**, certifique-se de que o arquivo **document-translation-sample (1)** esteja selecionado e clique em **Carregar (2)**.

    ![](../media/imagn6.png)

#### Tarefa 1.3 - Configure seu ambiente C#/.NET e instale Newtonsoft.Json

Nesta tarefa, configuraremos um ambiente C#/.NET no Visual Studio 2022. Criaremos um novo aplicativo de console chamado "document-translation-qs" usando o .NET 7.0 e instalaremos o pacote Newtonsoft.Json via NuGet para gerenciar operações JSON em nosso projeto.
   
1. Na **LabVM**, na barra de pesquisa do Windows, digite Visual e selecione **Visual Studio 2022**.

   > **Observação**: quando solicitado a entrar, selecione **Ignorar por enquanto** e, em **Configurações de desenvolvimento**, clique em **Iniciar o Visual Studio**.

1. Clique em **Conta de trabalho ou escola** para fazer login.

    > **Observação**: navegue até a aba Detalhes do Ambiente para obter as credenciais.
      
1. Na página **Introdução** do Visual Studio, selecione **Criar um projeto**.

   ![](../media/imagn8.png)

1. Na página **Criar um novo projeto**, digite **console (1)** na caixa de pesquisa. Escolha o modelo **Aplicativo do Console (2)** e, em seguida, escolha **Próximo (3)**.

    ![](../media/imagn9.png)

1. Na página **Configurar seu novo projeto**, digite **document-translation-qs (1)** na caixa do nome do Projeto. Em seguida, escolha **Próximo (2)**.

   ![](../media/imagn010.png)

1. Na página **Informações adicionais**, selecione **.NET 9.0 (1)** e, em seguida, selecione **Criar (2)**.

     ![](../media/imagn11.png)
    
1. Clique com o botão direito no seu projeto **document-translation-qs (1)** e selecione **Gerenciar pacotes do NuGet... (2)**.

    ![](../media/imagn12.png)

1. Selecione a aba **Procurar (1)** e digite **NewtonsoftJson (2)**. Selecione a versão estável mais recente no menu suspenso.

    ![](../media/imagn13.png)
   
1. Clique em **Instalar** para instalar o pacote no seu projeto.

    ![](../media/imagn14.png)

1. Clique em **Aplicar**.

    ![](../media/imagn15.png)
   
#### Tarefa 1.4 - Traduza todos os documentos para um contêiner de armazenamento e execute seu aplicativo

Nesta tarefa, você configurará um recurso do Translator no Portal do Azure, obterá suas chaves e ponto de extremidade e os integrará a um aplicativo de console C# no Visual Studio 2022. Este aplicativo será configurado para traduzir em lote documentos armazenados em um contêiner do Azure Storage usando APIs do serviço Translator.

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** na parte superior do portal, digite **Translator** e selecione **Translators** em serviços.

   ![](../media/imagn16.png)

1. Vá para o recurso Translator que foi criado e obtenha as chaves do recurso seguindo o próximo passo.
   
      ![](../media/imagn17.png)
   
1. No painel de navegação esquerdo, na seção **Gerenciamento de Recursos (1)**, selecione **Chaves e Ponto de extremidade (2)**. Copie e cole seu endpoint **Chave (3)** e **Document Translation (4)** em um local conveniente, como o Microsoft Notepad. Apenas uma chave é necessária para fazer uma chamada de API.

     ![](../media/imagn18.png)
   
1. Navegue de volta para o Visual Studio 2022 e abra o arquivo **Program.cs (1)**. Exclua o código pré-existente, incluindo a linha **Console.WriteLine("Hello World!") (2)**.

   ![](../media/imagn19.png)

1. Abra outra aba no Edge, procure pelo [código de exemplo](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample), e navegue até a seção **Start asynchronous batch translation** e copie o código.

    ![](../media/Active-image170.png)

1. Cole o código copiado no arquivo **Program.cs**.
   
    ![](../media/Active-image173.png)

1. Dentro do arquivo **Program.cs**, faça as seguintes atualizações:

    - Atualize **?api-version={date}** para **?api-version=2024-05-01**.
    - Atualize **{your-document-translation-endpoint}** e **{your-api-key}** com valores da instância do Translator que você registrou no bloco de notas.
    - Além disso, atualize **"https://YOUR-SOURCE-URL-WITH-READ-LIST-ACCESS-SAS\"** e **"https://YOUR-TARGET-URL-WITH-WRITE-LIST-ACCESS-SAS\"** com os valores da instância do contêiner da sua Conta de Armazenamento que você anotou no bloco de notas.
      
      ![](../media/Active-image171.png)
      
1. Depois de adicionar o exemplo de código ao seu aplicativo, escolha o botão verde **Iniciar** ao lado de `document-translation-qs` para criar e executar seu programa ou pressione F5.
   
    ![](../media/Active-image172.png)
   
### Tarefa 2: Criando um Recurso de Reconhecimento de Formulário

Nesta tarefa, você criará um recurso do Form Recognizer no Portal do Azure configurando um novo projeto no Document Intelligence Studio. Isso envolve configurar detalhes do projeto, conectar-se a uma fonte de dados de treinamento armazenada em uma conta do Azure Storage e validar suas configurações antes de criar o projeto.

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)**, digite **Azure AI Foundry (1)** e selecione **Azure AI Foundry (2)** em serviços.
   
   ![](../media/imagn20.png)

1. Na página **Azure AI services multi-service account**,  selecione o serviço que foi implantado usando o modelo personalizado.

     ![](../media/imagn21.png)
   
1. Na página **Azure AI services multi-service account**, clique na aba **Document Intelligence (1)** e selecione **Go to studio (2)**.

    ![](../media/imagn23.png)

1. No Document Intelligence Studio, role para baixo até **Custom extraction models** e selecione **Get started**.

   ![](../media/Active-image176.png)

1. Em **My Projects**, clique em **+ Create a project**.

    ![](../media/Active-image177.png)

      > **Observação**: Por favor, faça login se for solicitado.

1. Insira os seguintes detalhes e clique em **Continue**  **(3)**.
    
   - Project name: **testproject** **(1)**.
   - Description: **Custom model project** **(2)**.

      ![](../media/Active-image178.png)

1. Insira os seguintes dados em **Configure service resource** e clique em **Continue** **(5)**.

   - Subscription: Selecione sua **Assinatura Padrão** **(1)**.
   - Resource group: **ODL-GenAI-CL-xxxxxx-Activate-GenAI**.
   - Document Intelligence or Cognitive Service Resource: Selecione os disponíveis Cognitive Service nome semelhante a **cogservicesbpass{suffix}** **(3)**.
   - API version: **2022-08-31 (3.0 General Availability)** **(4)**.

     ![](../media/Active-image179.png)

1. Insira os seguintes dados em **Connect training data source**. e clique em **Continue** **(8)**.

   - Subscription: Selecione o seu **Assinatura Padrão** **(1)**.
   - Resource group: **ODL-GenAI-CL-xxxxxx-Activate-GenAI** **(2)**.
   - Storage account: **Selecione a conta de armazenamento existente (3)**.
   - Blob container: Clique em **Create new (4)** e forneça o nome como **custommoduletext** **(5)** e clique em **OK** **(6)**.
   - Revise as configurações e clique em **Continue** **(7)**.
   
       ![](../media/Active-image180.png)
       ![](../media/Active-image181.png)
       ![](../media/Active-image182.png)

1. Valide as informações e escolha **Create project**.

      ![](../media/Active-image183.png)

### Tarefa 3: Treinar e rotular dados

Nesta tarefa, você treinará um modelo do Form Recognizer carregando, rotulando, treinando e testando com dados de amostra compreendendo 6 documentos de treinamento.

1. Clique em **Browse for files**.

      ![](../media/Active-image184.png)

1.  No explorador de arquivos, navegue até o caminho `C:\LabFiles\Documents\Custom Model Sample` **(1)**, selecione todos os arquivos JPEG de trem **train1 a train6 (2)** e clique em **Abrir** **(3)**.

      ![](../media/imagn24.png)

1. Após o upload, escolha **Run now** na janela pop-up em Run Layout.

     ![](../media/Active-image186.png)

1. Clique em **+ Add a field** **(1)**, selecionar **Field** **(2)**, digite o nome field como **Organization_sample** **(3)**, e pressione **enter**.

      ![](../media/Active-image187.png)

      ![](../media/Active-image188.png)

1. Rotule o novo campo adicionado selecionando **CONTOSO LTD** no canto superior esquerdo de cada documento carregado. Faça isso para todos os seis documentos.

    ![](../media/Active-image189.png)
   
1. Depois que todos os documentos estiverem etiquetados, clique em **Train** no canto superior direito.

     ![](../media/Active-image190.png)

1. Especifique o model ID como **customfrs** **(1)**, model description como **custom model** **(2)**, e no menu suspenso, selecione **Template** **(3)** como Build Mode e clique em **Train** **(4)**.

    ![](../media/Active-image191.png)

1. Clique em **Go to Models**. 

   ![](../media/Active-image192.png)

1. Aguarde até que o status do modelo seja exibido **succeeded**. Uma vez que o status seja alcançado, selecione o modelo **customfrs** **(2)** que você criou e escolha **Test (3)**.

     ![](../media/Active-image193.png)

1. Selecione o modelo **customfrs** **(1)** que você criou e escolha **Test** **(2)**.

      ![](../media/Active-image194.png)
   
1. Na janela **Test model**, clique em **Browse for files**.

      ![](../media/Active-image195.png)

1. No explorador de arquivos, navegue até `C:\LabFiles\Document\Custom Model Sample` **(1)**, selecione todos os arquivos JPEG de teste **test1 and test2** **(2)**, e clique em **Abrir** **(3)**.

     ![](../media/imagn25.png)

1. Após o upload, selecione **um modelo de teste (1)** e clique em **Run analysis** **(2)**.

     ![](../media/Active-image197.png)

1. Agora você pode ver no lado direito que o modelo foi capaz de detectar o campo **Organization_sample** que criamos na última etapa, junto com sua pontuação de confiança.

    ![](../media/Active-image198.png)

### Tarefa 4: Construir um novo pipeline com o módulo de modelo personalizado no BPA

Nesta tarefa, você configurará um novo pipeline no Business Process Automation Accelerator (BPA) para utilizar um modelo personalizado do Form Recognizer. Isso envolve configurar o ID do modelo dentro dos estágios do pipeline e configurar a ingestão de documentos de caminhos de arquivo especificados.

Depois de ficar satisfeito com o desempenho do modelo personalizado, você pode recuperar o ID do modelo e usá-lo em um novo pipeline BPA com o módulo Modelo Personalizado no próximo passo.

1. Retorne para os Grupos de Recursos e selecione o grupo de recursos **ODL-GenAI-CL-xxxxxx-Activate-GenAI**.    

1. Vá para o Grupo recursos, pesquise e selecione o tipo de recurso **Aplicativo Web Estático** com um nome semelhante a **webappbpa{sufixo}**.

    ![](../media/imagn26.png)

1. Na página **Aplicativo Web Estático**, clique em **Exibir aplicativo no navegador**.

     ![](../media/imagn27.png)

1. Depois que a página **Business Process Automation Accelerator** for carregada com sucesso, clique em **Create/Update/Delete Pipelines**.

   ![](../media/Active-image201.png)

1. Na página **Create Or Select A Pipeline**, insira o nome do novo pipeline como **workshop** **(1)** e clique em **Create Custom Pipeline** **(2)**.

    ![](../media/Active-image202.png)

1. Na página **Select a document type to get started**, selecione **PDF Document**.

    ![](../media/Active-image203.png)

1. Na página **Select a stage to add it to your pipeline configuration**, pesquise e selecione **Form Recognizer Custom Model (Batch)**.

    ![](../media/Active-image204.png)
   
1. No pop-up, insira o ID do modelo como **customfrs** **(1)** e clique em **Submit** **(2)**. 

    ![](../media/Active-image205.png)

1. Na página **Select a stage to add it to your pipeline configuration**, role para baixo para revisar a **Pipeline Preview** e clique em **Done**.

    ![](../media/Active-image206.png)

1. Na página **Workshop Pipelines**, clique em **Home**. 

      ![](../media/Active-image207.png)

1. Na página **Business Process Automation Accelerator**, clique em **Ingest Documents**.

     ![](../media/Active-image208.png)

1. Na página **Upload a document to Blob Storage**, no menu suspenso, selecione um pipeline com o nome **workshop** **(1)** e clique em **Upload or drop a file right here**.

      ![](../media/Active-image209.png)

1. Para documentos, insira o seguinte caminho `C:\LabFiles\Document\Lab 1 Step 3.7` e pressione enter. Você pode carregar várias faturas, uma por uma.

      ![](../media/imagn28.png)

### Tarefa 5: Configurar a Pesquisa Cognitiva do Azure

Nesta tarefa, você configurará o Azure Cognitive Search para se conectar ao Azure Blob Storage. Isso inclui configurar uma fonte de dados, definir opções de análise para arquivos JSON, personalizar um índice de pesquisa para campos de dados e criar um indexador para automatizar processos de ingestão e indexação de dados.

1. Retorne para a janela do Grupo de recursos, pesquise e selecione **Serviço de pesquisa** com um nome semelhante a **bpa{sufixo}**.

   ![](../media/bpa4-1.png)

1. Na página **Serviço de pesquisa**, clique em **Importar dados**.

   ![](../media/imagn30.png)

1. Insira os seguintes detalhes para **Conectar a seus dados**.

    - Fonte de Dados: Selecione **Armazenamento de Blobs do Azure** **(1)**
    - Nome da fonte de dados: Insira **workshop** **(2)**.
    - Modo de análise: Selecione **JSON** **(3)**.
    - Assinatura: Selecione a **existente (4)**
    - Clique em **Escolher uma conexão existente** **(5)** na sequência de conexão.
  
      ![](../media/imagn31.png)

1. Na página **Contas de armazenamento**, selecione a conta de armazenamento com nome semelhante a **bpa{sufixo} (6)**. 

    ![](../media/imagn33.png)

1. Selecione **results** **(7)** na página **Contêineres** e clique em **Selecionar** **(8)**. Ele redirecionará de volta para a página **Conectar a seus dados**.

     ![](../media/imagn35.png)
  
1. Na página **Conectar a seus dados**, para **Pasta de blobs** digite **workshop** **(9)** clique em **Próximo: Adicionar habilidades cognitivas (Opcional) (10)**.

    ![](../media/imagn37.png)

1. Em **Adicionar habilidades cognitivas (Opcional)**, clique em **Ir para: Personalizar índice de destino**.

1. Em **Personalizar índice de destino**, insira o nome do índice como **azureblob-index** **(1)**, torne todos os campos **Recuperával** **(2)** e **Pesquisável** **(3)**.

      ![](../media/imagn38.png)

1. Expanda **aggregatedResults** **(1)** > **customFormRec (2)** > **documents** **(3)** > **fields** **(4)**. Abaixo dele, expanda **Organization_sample (5)**. Torne os três camp Faceta **(type, valueString, & content)** **(6)**.

   ![](../media/imagn39.png)

1.  clique em **Próximo: Criar um indexador**.

1. Na página **Criar um indexador**, insira o nome como **azureblob-indexer** **(1)** e clique em **Enviar** **(2)**.
   
    ![](../media/imagn40.png)

## Critérios de Sucesso:

- Tradução bem-sucedida de documentos e armazenamento no contêiner de destino do Armazenamento de Blobs do Azure.
- Configuração e utilização eficazes do recurso Form Recognizer e do pipeline do BPA.
- Configuração adequada do Azure Cognitive Search para os documentos processados.
- Validação do processamento de documentos e da funcionalidade de pesquisa usando a Aplicação de Pesquisa de Amostra no BPA.

## Recursos Adicionais:

- Consulte [tradução de documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample) para um código de exemplo que será usado para a tradução de documentos usando C#.
- Consulte [operações de Tradução de Documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/reference/rest-api-guide) para entender as APIs REST que utilizamos para a tradução de documentos.

## Prossiga para o próximo Desafio clicando em **próximo**>>.
