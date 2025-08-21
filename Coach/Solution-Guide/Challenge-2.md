# Desafio 02: Implementar a pesquisa de documentos usando o Azure AI Search

### Tempo Estimado: 120 minutos

## Introdução:

Todas as organizações dependem de informações para tomar decisões, responder a perguntas e operar de forma eficiente. O maior desafio, na maioria dos casos, não está na falta de informação, mas sim em como localizar e extrair dados relevantes a partir do vasto conjunto de documentos, bancos de dados e outras fontes onde essas informações estão armazenadas.

Por exemplo, imagine a *Margie’s Travel*, uma agência de viagens especializada em organizar roteiros para cidades ao redor do mundo. Com o tempo, a empresa acumulou uma grande quantidade de informações em diferentes formatos, como folhetos e avaliações de hotéis enviadas por clientes. Esse material é uma fonte riquíssima de insights para agentes e viajantes durante o planejamento de viagens. No entanto, o grande volume de dados pode dificultar a busca por informações específicas — como responder rapidamente a uma dúvida de um cliente.

Para superar esse desafio, a *Margie’s Travel* pode adotar o Azure AI Search, que permite indexar documentos e enriquecê-los com habilidades de IA, tornando-os mais fáceis de pesquisar e transformando grandes volumes de dados em informações acessíveis e úteis.

## Guia da Solução

### Tarefa 1: Clonar o repositório para este curso

Se você ainda não clonou o repositório de código **mslearn-knowledge-mining** para o ambiente em que onde está trabalhando neste laboratório, siga estes passos para fazê-lo. Caso contrário, abra a pasta clonada no Visual Studio Code.

1. Abra o **Visual Studio Code** na área de trabalho da VM do laboratório, clicando duas vezes nele.

1. No **Visual Studio Code**, no menu superior esquerdo, selecione as reticências **(...) (1)** > **Terminal (2)** e, em seguida, escolha **Novo Terminal (3)**.

    ![](../media/Active-image42.png)

1. Execute o seguinte comando no terminal para clonar o repositório para uma pasta local (não importa qual pasta).

    ```
    git clone https://github.com/MicrosoftLearning/AI-102-AIEngineer
    ```

    ![](../media/Active-image43.png)

1. Quando o repositório for clonado, abra a pasta no Visual Studio Code seguindo estes passos:

    - No menu do canto superior esquerdo, selecione **Arquivo (1)** > **Abrir Pasta... (2)**.

        ![](../media/Active-image44.png)

    - No explorador de arquivos em **Acesso rápido**, selecione **mslearn-knowledge-mining (1)** e clique em **Selecionar pasta (2)**.

        ![](../media/1-11-24(39).png)

    - Se a mensagem **Você confia nos autores dos arquivos nesta pasta?** aparecer, clique em **Sim, eu confio nos autores.**.

        ![](../media/Active-image46.png) 

        > **Observação**: Se for solicitado que você adicione os ativos necessários para compilar e depurar, selecione **Agora Não**.

### Tarefa 2: Criar recursos do Azure

Para criar a solução para a Margie's Travel, você precisará dos seguintes recursos em sua assinatura do Azure:

- Um recurso do **Azure AI Search** que gerenciará a indexação e as consultas.
- Um recurso do **Serviços de IA do Azure** que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.
- Uma **Conta de armazenamento** com um contêiner de blob no qual os documentos a serem pesquisados ​​são armazenados.

  > **Importante**: Seus recursos do Azure AI Search e do Serviços de IA do Azure devem estar na mesma localização.

### Tarefa 2.1: Criar um recurso do Azure AI Search

Nesta tarefa, você aprenderá como criar um recurso do **Azure AI Search** no portal do Azure.

1. Em um navegador da Web, entre no portal do Azure usando `https://portal.azure.com`.

1. Retorne à página inicial do portal do Azure e clique no botão **&#65291;Criar um recurso**.

    ![](../media/1-11-24(19).png)

1. Pesquise e selecione **Azure AI Search** na lista na página Criar um recurso.

    ![](../media/1-11-24(21).png)

1. Na página **Marketplace**, selecione **Azure AI Search**.

    ![](../media/1-11-24(22).png)

1. Na página **Azure AI Search**, clique em **Criar**.

    ![](../media/1-11-24(23).png)

1. Especifique os seguintes dados para criar um serviço de **Pesquisa de IA do Azure** e clique na aba **Revisar + Criar (6)**.

    | **Opção** | **Valor** |
    | ------------------ | ----------------------------------------------------- |
    | Assinatura | Deixar padrão **(1)** |
    | Grupo de Recursos | **Activate-GenAI** **(2)** |
    | Nome | *Digite um nome exclusivo* para seu serviço de pesquisa ou use o formato **searchservice-xxxxxx** (substitua **xxxxxx** pelo **Deployment ID** registrado no **Challenge 01**) **(3)** |
    | Localização | Use o mesmo local que o grupo de recursos **(4)** |
    | Tipo de preço | Básico **(5)** |

    >**Observação**: aqui, xxxxxx se refere ao ID de implantação.
    
    > **Observação:** Se o tipo de preço estiver definido como **Standard**, altere-a para **Básico** clicando em **Alterar Tipo de Preço**.

    > **Observação**: Se você encontrar o erro **Não é possível obter os custos para a assinatura**, ignore-o e prossiga para a próxima etapa.

    > **Observação**: Se você enfrentar algum problema ao implantar o serviço de pesquisa na região selecionada, selecione uma região diferente para implantar o serviço de pesquisa.

    > **Observação**: Seus recursos do Azure AI Search e dos Serviços de IA do Azure devem estar na mesma localização.

![](../media/searchservice-1504.png)
    ![](../media/1-11-24(24).png)

1. Assim que a validação for bem-sucedida na guia **Revisar + criar**, clique em **Criar** e aguarde a conclusão da implantação, depois clique em **Ir para o recurso**.

    ![](../media/1-11-24(25).png)

    ![](../media/1-11-24(26).png)

1. Revise a página **Visão geral** o painel do seu recurso Azure AI Search no portal do Azure. Aqui, você pode usar uma interface visual para criar, testar, gerenciar e monitorar os vários componentes de uma solução de pesquisa, incluindo fontes de dados, índices, indexadores e conjuntos de habilidades.
   
#### Tarefa 2.2: Criar um recurso dos Serviços de IA do Azure

Nesta tarefa, você aprenderá como criar um recurso dos Serviços de IA do Azure no portal do Azure. Sua solução de pesquisa usará este recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

1. Retorne à página inicial do portal do Azure e clique no botão **&#65291;Criar um recurso**.

    ![](../media/1-11-24(19).png)

1. Pesquise e selecione **Serviços de IA do Azure (1) (2)** na lista e, na página **Marketplace**, selecione **Serviços de IA do Azure (3)**.

    ![](../media/imag01.png)
    
    ![](../media/imag02.png)

1. Na página **Serviços de IA do Azure**, clique em **Criar**.

1. Especifique os seguintes dados para criar um **Serviço de IA do Azure** e clique na aba **Examinar + Criar (7)**.

    | **Opção** | **Valor** |
    | ------------------ | ----------------------------------------------------- |
    | Assinatura | Deixar padrão **(1)** |
    | Grupo de Recursos | **Activate-GenAI** **(2)** |
    | Localização | Usar a mesma localização do Azure AI Search **(3)** |
    | Nome | *Insira um nome único para seus Serviços de IA do Azure ou use o formato **challengeservice-xxxxxx** (substitua **xxxxxx** pelo **Deployment ID** registrado no **Challenge 01**) **(4)** |
    | Tipo de Preço | Standard S0 **(5)** |
    | Ao marcar esta caixa, reconheço que li e entendi todos os termos abaixo | Selecione a **Checkbox** **(6)**|
    
    >**Observação**: aqui, xxxxxx se refere à ID de implantação

    ![](../media/imag9.png)

1. Assim que a validação for bem-sucedida na guia **Examinar + Criar**, clique em **Criar** e aguarde a conclusão da implantação, depois clique em **Ir para o recurso**.

    >**Observação**: Seus recursos do Azure AI Search e dos Serviços de IA do Azure devem estar na mesma localização.

### Tarefa 2.3: Criar uma conta de armazenamento

Nesta tarefa, você aprenderá a criar um recurso de **Conta de armazenamento** no portal do Azure e, nas próximas etapas, criará um contêiner de blobs onde os documentos a serem pesquisados ​​serão armazenados.

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** na parte superior do portal, digite **Contas de armazenamento** **(1)** e selecione **Conta de armazenamento** **(2)**.

    ![](../media/1-11-24(32).png)

1. Clique em **+ Criar**.

    ![](../media/1-11-24(33).png)

1. Especifique os seguintes dados para criar uma conta de armazenamento do Azure e clique na guia **Próximo (7)**.

    | **Opção** | **Valor** |
    | ------------------ | ----------------------------------------------------- |
    | Assinatura | Deixe o padrão **(1)** |
    | Grupo de recursos | **Activate-GenAI** **(2)** |
    | Nome da conta de armazenamento | *Digite um nome exclusivo* para seus Serviços de IA do Azure ou use o formato **storagexxxxxx** (substitua **xxxxxx** pelo **ID de implantação** registrado no **Desafio 01**) **(3)** |
    | Região | Use o mesmo local do grupo de recursos **(4)** |
    | Desempenho | Standard **(5)** |
    | Redundância | **LRS (armazenamento com redundância local)** **(6)**|

    >**Observação**: aqui, xxxxxx se refere ao ID de implantação

    ![](../media/1-11-24(34).png)

1. Na aba **Avançado**, marque a caixa ao lado de **Permitir a hablitacao do acesso anônimo em contêineres individuais (1)** e clique em **Revisar + criar (2)**

    ![](../media/1-11-24(35).png)

1. Assim que a validação for bem-sucedida em **Revisar + criar**, clique em **Criar** e aguarde a conclusão da implantação, clique em **Ir para o recurso**.

    ![](../media/1-11-24(36).png)

    ![](../media/1-11-24(37).png)

1. Na página **Visão geral**, observe o **ID da Assinatura**; ele identifica a assinatura para a qual a conta de armazenamento é provisionada.

    ![](../media/1-11-24(38).png)

    > **Dica**: Mantenha o painel da **Conta de armazenamento** aberto; você precisará do ID da assinatura e de uma das chaves no próximo procedimento.

### Tarefa 3 e Tarefa 4: Fazer upload de documentos para o Armazenamento do Azure e executar o script

Nesta tarefa, você navegará entre o Visual Studio Code e o portal do Azure para obter as credenciais necessárias, atualizar um arquivo de lote e usar a CLI do Azure para fazer upload de documentos para um contêiner de blob em sua conta de armazenamento.

>**Importante**: Agora que você tem os recursos necessários, pode fazer o upload de alguns documentos para sua conta de Armazenamento do Azure.

1. Navegue de volta para o Visual Studio Code, no painel **Explorador**, expanda a pasta **22-create-a-search-solution (1)** e selecione **UploadDocs.cmd (2)**.

    ![](../media/Active-image47.png)


1. Navegue de volta para a aba do navegador exibindo o **portal do Azure**, obtenha o **nome da conta de armazenamento do Azure (1)**, o **ID da Assinatura (2)** e a **chave da conta de armazenamento do Azure** clicando em **Chaves de acesso** em **Segurança + rede** no menu à esquerda e, em seguida, clique na opção **Mostrar** > **Área de transferência (3)** da conta de armazenamento criada recentemente e registre os valores no bloco de notas.

    ![](../media/imag1.png)

    ![](../media/imag2.png)

1. Retorne ao código do VS e edite o arquivo em lote para substituir os espaços reservados **YOUR_SUBSCRIPTION_ID**, **YOUR_AZURE_STORAGE_ACCOUNT_NAME** e **YOUR_AZURE_STORAGE_KEY** com os valores correspondentes que você anotou no passo anterior.

    ![](../media/Active-image85.png)

1. Salve suas alterações e, em seguida, clique com o botão direito na pasta **01-azure-search (1)** > **Abrir em um terminal integrado (2)**.

    ![](../media/Active-image51.png)

1. Digite o seguinte comando para fazer login na sua assinatura do Azure usando o Azure CLI:

    >**Observação**: Certifique-se de ter instalado a CLI do Azure e a extensão Azure CLI Tools no Visual Studio Code.

    >**Observação**: Certifique-se de substituir `<your-username>` e `<your-password>` pelo nome de usuário e senha do Azure que você está usando desde o desafio 1.

    ```
    az login --username <your-username> --password <your-password>
    ```

    ![](../media/Active-image52.png)

    > **Observação**: Se uma aba do navegador abrir e solicitar que você faça login no Azure, faça o login, feche a aba do navegador e retorne ao Visual Studio Code.

1. Digite o seguinte comando para executar o arquivo de lote. Isso criará um contêiner de blob em sua conta de armazenamento e fará o upload dos documentos da pasta **data** para ele.

    ```
    .\UploadDocs
    ```

    ![](../media/Active-image53.png)

### Tarefa 5: Importação e indexação de dados:

#### Tarefa 5.1: Indexar os documentos

Nesta tarefa, você aprenderá a criar uma solução de pesquisa indexando documentos que já estão no lugar. Navegando até seu recurso do Azure AI Search no portal do Azure, configure a fonte de dados para utilizar o Armazenamento de Blobs do Azure, integre habilidades cognitivas para enriquecimento, personalize o índice de destino e configure um indexador para processar e indexar os documentos de forma eficaz.

>**Observação**: Agora que os documentos estão no lugar, você pode criar uma solução de pesquisa indexando-os.

1. No portal do Azure, navegue até seu recurso **Azure AI Search**. Em seguida, na página **Visão geral**, selecione **Importar dados**.

    ![](../media/imag3.png)

1. Na página **Conectar aos seus dados**, na lista **Fonte de Dados**, selecione **Armazenamento de Blob do Azure**. Em seguida, preencha os dados do armazenamento de dados com os seguintes valores:

    - **Fonte de Dados (1)**: Armazenamento de Blob do Azure
    - **Nome da fonte de dados (2)**: margies-data
    - **Dados para extrair (3)**: Conteúdo e metadados
    - **Modo de análise (4)**: Padrão
    - **Assinatura (5)**: Deixe o padrão
    - **Cadeia de conexão**: Selecione **Escolher uma conexão existente (6)**. Em seguida, selecione sua **Conta de armazenamento (7)** e, finalmente, selecione o contêiner **margies (8)** que foi criado pelo script UploadDocs.cmd. Em seguida, clique em **Selecionar (9)**.

      ![](../media/imag4.png)
        
      ![](../media/imag5.png)
        
      ![](../media/imagn1.png)

    - **Autenticação de identidade gerenciada (10)**: Nenhum 
    - **Nome do contêiner (11)**: margies
    - **Pasta de blobs (12)**: Deixe em branco
    - **Descrição (13)**: Brochuras e avaliações no site da Margie's Travel.
    - Clique em **Próximo : Adicionar habilidades cognitivas (opcional) (14)**

      ![](../media/imag7.png)

1. Na aba **Adicionar habilidades cognitivas (Opcional)**, expanda **Anexar Serviços de IA (1)**. Na seção, selecione seu recurso **Serviços de IA do Azure (2)**.

   ![](../media/imag10.png)

1. Role para baixo e expanda a seção **Adicionar enriquecimentos (1)** e especifique o seguinte:

    - Altere o **Nome do conjunto de habilidades** para **margies-skillset (2)**.
    - Marque a caixa de seleção para **Habilitar OCR e mesclar todo o texto no campo merged_content (3)**.
    - Certifique-se de que o **Campo de dados de origem** esteja definido como **merged_content (4)**.
    - Deixe o **Nível de granularidade do enriquecimento** como o **Campo de origem(padrão) (5)**, que define todo o conteúdo do documento que está sendo indexado, mas observe que você pode alterar isso para extrair informações em níveis mais granulares, como páginas ou frases.
    
        ![](../media/imag11.png)

    - Selecione os seguintes campos enriquecidos:
    
        | Habilidades Cognitivas de Texto | Parâmetro | Nome do campo |
        | --------------- | ---------- | ---------- |
        | Extrair nomes de localização | | locations |
        | Extrair frases-chave | | keyphrases |
        | Detectar idioma | | language |
        | Gerar marcações de imagens | | imageTags |
        | Gerar legendas de imagens | | imageCaption |
        
        ![](../media/imag12.png)

1. Verifique novamente suas seleções (pode ser difícil alterá-las mais tarde). Em seguida, prossiga para a próxima etapa (*Personalizar índice de destino*).

    ![](../media/imag13.png)

1. Na guia **Personalizar índice de destino**, altere o **Nome do índice** para **margies-index (1)**.

1. Certifique-se de que a **Chave** esteja definida como **metadata_storage_path (2)** e deixe o **Nome do sugeridor** em branco e o **Modo de busca (3)** em seu valor padrão.

    ![](../media/imag14.png)
   
1. Faça as seguintes alterações nos campos de índice, deixando todos os outros campos com suas configurações padrão (**IMPORTANTE**: pode ser necessário rolar para a direita para ver a tabela inteira):

    | Nome do campo | Recuperável | Filtrável | Classificável | Com faceta | Pesquisável |
    | ------------- | ----------- | --------- | ------------- | ---------- | ----------- |
    | metadata_storage_size | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
    | metadata_storage_last_modified | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
    | metadata_storage_name | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
    | metadata_author | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
    | locations | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
    | keyphrases | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
    | language | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | |
    
    Use a imagem abaixo para verificar a opção.
    
    ![](../media/Active-image64.png)

1. Verifique novamente suas seleções, prestando atenção especial para garantir que as opções corretas **Recuperável**, **Filtrável**, **Classificável**, **Com faceta** e **Pesquisável** estejam selecionadas para cada campo (pode ser difícil alterá-las mais tarde). Em seguida, prossiga para a próxima etapa clicando em **Próximo: Criar um indexador**.

1. Na guia **Criar um indexador**, especifique o seguinte
    - Altere o **Nome do indexador** para **margies-indexer (1)**.
    - Deixe o **Agenda** definido como **Uma vez (2)**.
    - Expanda as **Opções avançadas (3)** e certifique-se de que a opção **Chaves de codificação Base-64 (4)** esteja selecionada (geralmente, as chaves de codificação tornam o índice mais eficiente).

    - Selecione **Enviar (5)** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:

        1. Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
        2. Executa o conjunto de habilidades cognitivas para gerar campos enriquecidos adicionais.
        3. Mapeia os campos extraídos para o índice.

           ![](../media/imag15.png)

1. Na página de recursos do **Serviço de Pesquisa**, expanda **Gerenciamento de pesquisa (1)** selecione **Indexadores (2)** que deve mostrar o **margies-indexer (3)** recém-criado.

    ![](../media/imag16.png)

1. Selecione **margies-indexer** . Aguarde alguns minutos e clique em **&orarr; Atualizar** até que o **Status** indique **Exito**.

    ![](../media/imag17.png)
   
### Tarefa 5.2: Pesquisar o índice

Nesta tarefa, você aprenderá a pesquisar e consultar o índice criado anteriormente:

1. Na parte superior da página **Visão geral** do seu recurso de pesquisa do Azure AI, selecione **Explorador de pesquisa**.

    ![](../media/imag18.png)

1. No Explorador de pesquisa, na caixa **Sequência de caracteres de consulta**, insira `*` **(1)** (um único asterisco) e selecione **Pesquisar (2)**.

    ![](../media/imag19.png)
    
    >**Observação**: Esta consulta retorna todos os documentos do índice em formato JSON. Analise os resultados e observe que cada documento inclui o conteúdo, os metadados e os dados enriquecidos gerados pelas habilidades cognitivas configuradas.

1. No menu **Exibir**, selecione **Exibição JSON**.

    ![](../media/imag20.png)

1. Observe que a solicitação JSON para a pesquisa é mostrada, assim:

    ```json
    {
    "search": "*"
    }
    ```
    ![](../media/imag21.png)

>**Observação:** Vá para o passo 6 se o parâmetro count estiver presente na solicitação JSON.

1. Modifique a solicitação JSON para incluir o parâmetro **count**, conforme mostrado aqui:

    ```json
    {
    "search": "*",
    "count": true
    }
    ```

1. Envie a pesquisa modificada. Desta vez, os resultados incluem um campo **@odata.count** no topo, que indica o número de documentos retornados pela pesquisa.

1. Tente a seguinte consulta:
    
    ```json
    {
    "search": "*",
    "count": true,
    "select": "metadata_storage_name,metadata_author,locations"
    }
    ```

    >**Observação**: Desta vez, os resultados incluem apenas o nome do arquivo, o autor e quaisquer locais mencionados. O nome do arquivo e o autor estão nos campos  **metadata_storage_name** e **metadata_author**, que foram extraídos do documento de origem. O campo **locations** foi gerado por uma habilidade cognitiva.

1. Agora, tente a seguinte cadeia de caracteres de consulta:

    ```json
    {
    "search": "New York",
    "count": true,
    "select": "metadata_storage_name,keyphrases"
    }
    ```
    
    >**Observação**: Esta pesquisa encontra documentos que mencionam "New York" e retorna o nome do arquivo e as frases-chave.

1. Vamos tentar mais uma consulta:

    ```json
    {
    "search": "New York",
    "count": true,
    "select": "metadata_storage_name",
    "filter": "metadata_author eq 'Reviewer'"
    }
    ```

    >**Observação**: Esta consulta retorna o nome do arquivo de quaisquer documentos de autoria de *Reviewer* que mencionem "New York".
  
## Tarefa 6: Explorar e modificar definições de componentes de pesquisa

Os componentes de uma solução de pesquisa são definidos em JSON, e essas definições podem ser visualizadas e editadas diretamente no portal do Azure.

Embora o portal ofereça uma interface prática para criar e gerenciar soluções de pesquisa, em muitos cenários é mais eficiente trabalhar diretamente com os objetos de pesquisa em JSON, utilizando a API REST do Azure AI Search para criar e modificar esses componentes de forma automatizada e reproduzível.

#### Tarefa 6.1: Obter o ponto de extremidade e a chave para seu recurso do Azure AI Search

Nesta tarefa, você está se preparando para executar comandos CURL no Visual Studio Code para interagir com a interface REST do Serviço de IA do Azure:

1. No portal do Azure, retorne à página **Visão geral** do seu recurso **Serviço de pesquisa** e, na seção superior da página, encontre o **Url** do seu recurso (algo como **https://resource_name.search.windows.net**) e copie-a.

    ![](../media/imag22.png)

1. No Visual Studio Code, no painel Explorador, expanda a pasta **01-azure-search (1)** e sua subpasta **modify-search (2)** e selecione **modify-search.cmd (3)** para abri-la. Você usará este arquivo de script para executar comandos *CURL* que enviam JSON para a interface REST do Serviço de IA do Azure.

    ![](../media/Active-image73.png)

1. Em **modify-search.cmd**, substitua o espaço reservado **YOUR_SEARCH_URL** pela URL que você copiou.

    ![](../media/Active-image76.png)

1. No portal do Azure, volte para a página **Visão geral** do seu recurso **Serviço de pesquisa**, expanda **Configurações (1)** e selecione **Chaves (2)** e copie a **Chave de administração primária (3)** para a área de transferência.

    ![](../media/imag23.png)

1. Volte para o **Visual Studio Code**, substitua o espaço reservado **YOUR_ADMIN_KEY** pela chave que você copiou.

    ![](../media/Active-image77.png)

1. Salve as alterações em **modify-search.cmd** (mas não o execute ainda!)

    ![](../media/Active-image75.png)
    
### Tarefa 6.2: Revisar e modificar o conjunto de habilidades

Nesta tarefa, você configurará um conjunto de habilidades (skillset.json) no Visual Studio Code para integrar os Serviços de IA do Azure com o Azure AI Search:

1. No Visual Studio Code, na pasta **modify-search**, abra **skillset.json**.

    ![](../media/Active-image78.png)

1. Na parte superior da definição do skillset, você encontrará o objeto **cognitiveServices**, responsável por conectar o seu recurso dos Serviços de IA do Azure ao skillset.

1. No portal do Azure, na caixa de pesquisa, digite **Azure AI Foundry (1)** e selecione **Azure AI Foundry (2)**.

1. Na navegação à esquerda, vá para **Conta multisserviço dos serviços de IA do Azure (clássico) (1)** e selecione o **challengeservice (2)**.

1. Na página de visão geral da **Conta Multisserviços de IA do Azure**, no painel de navegação esquerdo, expanda **Gerenciamento de Recursos (1)**, selecione **Chaves e Ponto de Extremidade (2)**. Em seguida, copie a **Chave 1 (3)**.

    ![](../media/imag24.png)

1. No Visual Studio Code, em **skillset.json**, substitua o espaço reservado **YOUR_COGNITIVE_SERVICES_KEY** do Serviço de IA do Azure que você copiou.

    ![](../media/Active-image80.png)

1. Role pelo arquivo JSON. Na parte inferior da lista de habilidades, uma habilidade adicional foi adicionada com a seguinte definição:

    ```
    {
    "@odata.type": "#Microsoft.Skills.Text.V3.SentimentSkill",
    "defaultLanguageCode": "en",
    "name": "get-sentiment",
    "description": "Nova habilidade para avaliar o sentimento",
    "context": "/document",
    "inputs": [
    {
    "name": "text",
    "source": "/document/merged_content"
    },
    {
    "name": "languageCode",
    "source": "/document/language"
    }
    ],
    "outputs": [
    {
    "name": "sentiment",
    "targetName": "sentimentLabel"
    }
    ]
    }
    ```

    >**Observação**: A nova habilidade é chamada **get-sentiment** e irá avaliar o texto encontrado no campo **merged_content** do documento. A etiqueta de sentimento ("positivo", "negativo", "neutro" ou "misto") é então emitida como um novo campo chamado **sentimentLabel**.

1. Salve as alterações que você fez em **skillset.json**.

### Tarefa 6.3: Revise e modifique o índice

Nesta tarefa, você revisará o arquivo index.json no Visual Studio Code, que mostra uma definição JSON para **margies-index**

1. No Visual Studio Code, na pasta **modify-search**, abra **index.json**. Isso mostra uma definição JSON para **margies-index**.

    ![](../media/Active-image81.png)

1. Role pelo índice e visualize as definições de campo. Alguns campos são baseados em metadados e conteúdo no documento de origem, e outros são resultados de habilidades no conjunto de habilidades.
   
1. No final da lista de campos que você definiu no portal do Azure, observe que dois campos adicionais foram adicionados:

    ```
    {
    "name": "sentiment",
    "type": "Edm.String",
    "facetable": false,
    "filterable": true,
    "retrievable": true,
    "sortable": true
    },
    {
    "name": "url",
    "type": "Edm.String",
    "facetable": false,
    "filterable": true,
    "retrievable": true,
    "searchable": false,
    "sortable": false
    }
    ```

1. O campo **sentiment** será usado para adicionar a saída da habilidade **get-sentiment** que foi adicionada ao conjunto de habilidades. O campo **url** será usado para adicionar a URL de cada documento indexado ao índice, com base no valor **metadata_storage_path** extraído da fonte de dados. Observe que o índice já inclui o campo **metadata_storage_path**, mas ele é usado como a chave de índice e codificado em Base-64, tornando-o eficiente como uma chave, mas exigindo que os aplicativos clientes o decodifiquem se quiserem usar o valor real da URL como um campo. Adicionar um segundo campo para o valor não codificado resolve esse problema.
   
### Tarefa 6.4: Revisar e modificar o indexador

Nesta tarefa, você revisará o arquivo **indexer.json** no Visual Studio Code, que mostra uma definição JSON para **margies-index**

1. No Visual Studio Code, na pasta **modify-search**, abra **indexer.json**. Isso mostra uma definição JSON para **margies-indexer**, que mapeia campos extraídos do conteúdo do documento e metadados (na seção **fieldMappings**) e valores extraídos por habilidades no skillset (na seção **outputFieldMappings**) para campos no índice.

    ![](../media/Active-image82.png)

1. Na lista **fieldMappings**, observe o mapeamento do valor **metadata_storage_path** para o campo de chave codificado em base 64. Isso foi criado quando você atribuiu **metadata_storage_path** como a chave e selecionou a opção para codificar a chave no portal do Azure. Além disso, um novo mapeamento mapeia explicitamente o mesmo valor para o campo **url**, mas sem a codificação Base-64:

    ```
    {
    "sourceFieldName" : "metadata_storage_path",
    "targetFieldName" : "url"
    }
    ```

    > **Observação**: Todos os outros metadados e campos de conteúdo no documento de origem são mapeados implicitamente para campos do mesmo nome no índice.

1. Revise a seção **ouputFieldMappings**, que mapeia saídas das habilidades no skillset para campos de índice. A maioria delas reflete as escolhas que você fez na interface do usuário, mas o mapeamento a seguir foi adicionado para mapear o valor **sentimentLabel** extraído pela sua habilidade de sentimento para o campo **sentiment** que você adicionou ao índice:

    ```
    {
    "sourceFieldName": "/document/sentimentLabel",
    "targetFieldName": "sentiment"
    }
    ```

### Tarefa 6.5: Use uma API REST para atualizar a solução de pesquisa

Nesta tarefa, você atualizará as definições JSON no Visual Studio Code para Azure AI Search para incluir novos campos, como resultados de análise de sentimento e URLs de documentos. Execute modify-search.cmd para aplicar as alterações e iniciar a indexação. Monitore o progresso na seção Indexadores do portal do Azure para avisos de conclusão e tamanho do documento durante a análise de sentimento.

1. Clique com o botão direito na pasta **modify-search (1)** e selecione **Abrir em um Terminal Integrado (2)**.

    ![](../media/Active-image83.png)

1. No painel do terminal, digite o seguinte comando para executar o script **modify-search.cmd**, que envia as definições JSON para a interface REST e inicia a indexação.

    ```
    .\modify-search
    ```

1. Quando o script terminar, retorne à página **Visão geral** do seu **Serviço de pesquisa** no painel de navegação esquerdo, expanda **Gerenciamento de pesquisa** e selecione **Indexadores**. Em seguida, selecione periodicamente **Atualizar** periodicamente para acompanhar o progresso da operação de indexação. Pode levar cerca de um minuto para ser concluído.

    ![](../media/imag25.png)

    >**Observação**: Pode haver alguns avisos para documentos que sejam grandes demais para a avaliação de sentimento. Normalmente, a análise de sentimento é realizada em nível de página ou de frase, em vez de no documento completo. No entanto, neste cenário, a maioria dos documentos — especialmente as avaliações de hotéis — é curta o suficiente para que seja possível calcular pontuações úteis de sentimento em nível de documento.

### Tarefa 6.6: Consultar o índice modificado

Nesta tarefa, você executará uma consulta no Azure AI Search para recuperar URLs, sentimentos e frases-chave para documentos que mencionam "Londres" com sentimentos positivos, de autoria de "Reviewer".

1. Na parte superior da lâmina do seu recurso do Azure AI Search, selecione **Explorador de pesquisa**.
   
1. No Explorador de pesquisa, na caixa **Cadeia de caracteres de consulta**, envie a seguinte consulta JSON:

    ```json
    {
    "search": "London",
    "select": "url,sentiment,keyphrases",
    "filter": "metadata_author eq 'Reviewer' and sentiment eq 'positive'"
    }
    ```

    Esta consulta recupera a **url**, **sentiment** e **keyphrases** para todos os documentos que mencionam *London* de autoria de *Reviewer* que têm um rótulo de **sentiment** positivo (em outras palavras, avaliações positivas que mencionam London).

1. Feche a página **Explorador de pesquisa** para retornar à página **Visão geral**.

### Tarefa 7: Criar um aplicativo cliente de pesquisa

Agora que você tem um índice útil, pode usá-lo em um aplicativo cliente. Você pode fazer isso consumindo a interface REST, enviando solicitações e recebendo respostas no formato JSON por HTTP, ou pode usar o kit de desenvolvimento de software (SDK) para sua linguagem de programação preferida. Neste exercício, usaremos o SDK.

> **Observação**: Você pode escolher usar o SDK para **C#** ou **Python**. Nas etapas abaixo, execute as ações apropriadas para sua linguagem preferida.

### Tarefa 7.1: Obter o ponto de extremidade e as chaves para seu recurso de pesquisa

Nesta tarefa, você recuperará a URL e as chaves do ponto de extremidade para seu recurso de Pesquisa de IA do Azure do portal do Azure, essencial para gerenciar e consultar seus recursos de pesquisa em tarefas futuras.

1. No portal do Azure, navegue de volta para **Serviço de pesquisa**. Na página Visão geral do recurso **Serviço de pesquisa**, observe o valor da URL, que deve ser semelhante a **https://your_resource_name.search.windows.net**. Registre esse valor no Bloco de notas, pois ele será necessário em tarefas futuras.

    ![](../media/imag22.png)

1. Na navegação à esquerda, expanda **Configurações (1)**, selecione **Chaves (2)**, observe que há duas chaves **administrador** e uma única chave **Gerenciar chaves de administrador**.

    >**Observação**: uma chave *admin* é usada para criar e gerenciar recursos de pesquisa

    >**Observação**: uma chave *Gerenciar chaves de consulta* é usada por aplicativos clientes que precisam apenas executar consultas de pesquisa.
    
    ![](../media/imag23.png)

1. Copie as **Gerenciar chaves de consulta** para a área de transferência e registre-as no Bloco de notas, pois elas serão necessárias para tarefas futuras.

    ![](../media/imag26.png)

### Tarefa 7.2: Prepare-se para usar o SDK de pesquisa do Azure AI

Nesta tarefa, você preparará seu ambiente de desenvolvimento no Visual Studio Code para integrar-se ao Azure AI Search SDK instalando os pacotes necessários (Azure.Search.Documents para C# ou azure-search-documents para Python) e configurando a URL do ponto de extremidade e a chave de consulta nos respectivos arquivos de configuração.

1. No Visual Studio Code, no painel **Explorer**, navegue até a pasta **22-create-a-search-solution** e expanda a pasta **C-Sharp** ou **Python** dependendo da sua preferência de idioma.
1. Clique com o botão direito do mouse na pasta **margies-travel** e abra um terminal integrado. Em seguida, instale o pacote Azure AI Search SDK executando o comando apropriado para sua preferência de idioma:
    > **Observação**: certifique-se de que as extensões necessárias já estejam instaladas no VS Code.

    **C#**

    ```
    dotnet add package Azure.Search.Documents --version 11.1.1
    ```
    **Python**

    ```
    pip install azure-search-documents==11.0.0
    ```

1. Veja o conteúdo da pasta **margies-travel** e observe que ela contém um arquivo para definições de configuração:
    - **C#**: appsettings.json
    - **Python**: .env

1. Abra o arquivo de configuração e atualize o **YOUR_SEARCH_ENDPOINT** com o link **Azure AI Search** *Endpoint URL* e os valores **YOUR_SEARCH_QUERY_KEY** com **Manage query keys** que você registrou em tarefas anteriores e salve as alterações.

    - **C#**: appsettings.json
    
        ![](../media/Active-image93.png)
    
    - **Python**: .env
    
        ![](../media/Active-image94.png)

### Tarefa 7.3: Explorar código para pesquisar um índice

Nesta tarefa, você explorará o código para um aplicativo da Web (C# ASP.NET Razor ou Python Flask) dentro da pasta margies-travel. Você revisará como ele interage com o Azure AI Search SDK para executar consultas de pesquisa, configurar clientes de pesquisa e gerenciar resultados de pesquisa, incluindo filtragem, classificação e destaque de campos de conteúdo.

A pasta **margies-travel** contém arquivos de código para um aplicativo da Web (um aplicativo da Web Microsoft C# *ASP.NET Razor* ou um aplicativo Python *Flask*), que inclui funcionalidade de pesquisa.

1. Abra o seguinte arquivo de código no aplicativo da Web, dependendo da sua escolha de linguagem de programação:
    - **C#**: Pages/Index.cshtml.cs
    - **Python**: app.py

1. Próximo ao topo do arquivo de código, encontre o comentário **Import search namespaces** e observe os namespaces que foram importados para funcionar com o Azure AI Search SDK:

1. Na função **search_query**, encontre o comentário **Create a search client** e observe que o código cria um objeto **SearchClient** usando o ponto de extremidade e a chave de consulta para seu recurso do Azure AI Search:

1. Na função **search_query**, encontre o comentário **Submit search query** e revise o código para enviar uma pesquisa para o texto especificado com as seguintes opções:
    - Um *modo de pesquisa* que requer que **todas** as palavras individuais no texto de pesquisa sejam encontradas.
    - O número total de documentos encontrados pela pesquisa é incluído nos resultados.
    - Os resultados são filtrados para incluir apenas documentos que correspondem à expressão de filtro fornecida.
    - Os resultados são classificados na ordem de classificação especificada.
    - Cada valor discreto do campo **metadata_author** é retornado como uma *faceta* que pode ser usada para exibir valores predefinidos para filtragem.
    - Até três extratos dos campos **merged_content** e **imageCaption** com os termos de pesquisa destacados são incluídos nos resultados.
    - Os resultados incluem apenas os campos especificados.

### Tarefa 7.4: Explorar código para renderizar resultados de pesquisa

Nesta tarefa, você se aprofundará no código do aplicativo da web (C# ASP.NET Razor ou Python Flask) para entender como ele apresenta os resultados da pesquisa:

O aplicativo da web já inclui código para processar e renderizar os resultados da pesquisa.

1. Abra o seguinte arquivo de código no aplicativo da web, dependendo da sua escolha de linguagem de programação:
    - **C#**: Pages/Index.cshtml
    - **Python**: templates/search.html
1. Examine o código, que renderiza a página na qual os resultados da pesquisa são exibidos. Observe que:
    - A página começa com um formulário de pesquisa que o usuário pode usar para enviar uma nova pesquisa (na versão Python do aplicativo, esse formulário é definido no modelo **base.html**), que é referenciado no início da página.
    - Um segundo formulário é então renderizado, permitindo que o usuário refine os resultados da pesquisa. O código para este formulário:
        - Recupera e exibe a contagem de documentos dos resultados da pesquisa.
        - Recupera os valores de faceta para o campo **metadata_author** e os exibe como uma lista de opções para filtragem.
        - Cria uma lista suspensa de opções de classificação para os resultados.
        - O código então itera pelos resultados da pesquisa, renderizando cada resultado da seguinte forma:
        - Exibe o campo **metadata_storage_name** (nome do arquivo) como um link para o endereço no campo **url**.
        - Exibe *destaques* para termos de pesquisa encontrados nos campos **merged_content** e **imageCaption** para ajudar a mostrar os termos de pesquisa em contexto.
        - Exibe os campos **metadata_author**, **metadata_storage_size**, **metadata_storage_last_modified** e **language**.
        - Exibe o rótulo **sentiment** para o documento. Pode ser positivo, negativo, neutro ou misto.
        - Exibe as cinco primeiras **keyphrases** (se houver).
        - Exibe os cinco primeiros **locations** (se houver).
        - Exibe as cinco primeiras **imageTags** (se houver).
          
### Tarefa 7.5: Executar o aplicativo da web

Nesta tarefa, você executará o aplicativo da web Margie's Travel localmente, pesquisando termos específicos como "hotel em Londres" e "hotel tranquilo em Nova York", refinando os resultados da pesquisa usando filtros e opções de classificação com base no sentimento, observando a identificação de palavras-chave e localização em documentos.

1. Retorne ao terminal integrado para a pasta **margies-travel** e insira o seguinte comando para executar o programa:

    **C#**

    ```
    dotnet run
    ```
    > **Observação:** Se o comando falhar, clique no link fornecido na mensagem de erro para baixar a versão mais recente do Microsoft ASP.NET Core Shared Framework. Depois disso, baixe e instale o .NET Core e execute o comando novamente.

   **Python**

    ```
    flask run
    ```
    > **Observação:** se o comando falhar, execute os comandos **pip install flask** e **pip install python-dotenv** e, em seguida, execute o comando novamente.

1. Abra outra aba no Edge Browse seguindo o link (*http://localhost:5000/* ou *http://127.0.0.1:5000/*) para abrir o site **Margie's Travel** em um navegador da web.

    ![](../media/Active-image101.png)

1. No site **Margie's Travel**, digite **London hotel (1)** na caixa de pesquisa e clique em **Search (2)**.

    ![](../media/Active-image95.png)

1. Revise os resultados da pesquisa. Eles incluem o nome do arquivo (com um hiperlink para a URL do arquivo), um extrato do conteúdo do arquivo com os termos de pesquisa (*London* e *hotel*) enfatizados e outros atributos do arquivo dos campos de índice.

    ![](../media/Active-image96.png)
    
1. Observe que a página de resultados inclui alguns elementos da interface do usuário que permitem refinar os resultados. Eles incluem:
    
    - Um *Filtro por autor* com base em um valor de faceta para o campo **metadata_author**. Isso demonstra como você pode usar campos *facetable* para retornar uma lista de *facetas* - campos com um pequeno conjunto de valores discretos que podem ser exibidos como valores de filtro potenciais na interface do usuário.
    
    - Uma capacidade de **Classificar por** para *ordenar* os resultados com base em um campo especificado e na direção da classificação (crescente ou decrescente). A ordem padrão é baseada na *relevância*, que é calculada como um valor **search.score()** com base em um *perfil de pontuação* que avalia a frequência e a importância dos termos de pesquisa nos campos de índice.

1. Selecione o filtro **Reviewer (1)** e a opção de classificação **Positive to negative (2)** e, em seguida, selecione **Refine Results (3)**.

    ![](../media/Active-image97.png)

1. Observe que os resultados são filtrados para incluir apenas avaliações e classificados com base no rótulo de sentimento.

    ![](../media/Active-image98.png)

1. No site **Margie's Travel**, digite **quiet hotel in New York (1)** na caixa de pesquisa e clique em **Search (2)**.

    ![](../media/Active-image99.png)

1. Tente os seguintes termos de pesquisa:
    - **Torre de Londres** (observe que este termo é identificado como uma *frase-chave* em alguns documentos).
    - **arranha-céu** (observe que esta palavra não aparece no conteúdo real de nenhum documento, mas é encontrada nas *legendas de imagem* e *etiquetas de imagem* que foram geradas para imagens em alguns documentos).
    - **deserto de Mojave** (observe que este termo é identificado como um *local* em alguns documentos).

1. Feche a aba do navegador que contém o site Margie's Travel e retorne ao Visual Studio Code. Então, no terminal Python para a pasta **margies-travel** (onde o aplicativo dotnet ou flask está sendo executado), digite Ctrl+C para parar o aplicativo.
   
## Critério de Sucesso:

Para concluir este desafio com sucesso, você deve:

- Implantar o Serviço de Pesquisa do Azure e a Conta de Armazenamento do Azure.
- Adicionar dados à conta de armazenamento.
- Indexar os documentos no Azure AI Search usando o portal do Azure.
- Personalizar o índice e configurar o indexador no Azure AI Search.
- Modificar e explorar componentes de pesquisa usando definições JSON.
- Utilizar o Azure AI Search SDK para criar um aplicativo cliente para pesquisa.
- Executar o aplicativo da Web localmente, realizar pesquisas e refinar os resultados da pesquisa de forma eficaz.

## Recursos Adicionais:

- Consulte [O que é o Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) para referência.
- [O que são índices no Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
- [Pesquisando texto de documento em escala usando o Azure Cognitive Search](https://benalexkeen.com/searching-document-text-at-scale-using-azure-cognitive-search/)

Para saber mais sobre o Azure AI Search, consulte a [documentação do Azure AI Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search).

## Prossiga para o próximo Desafio clicando em **Próximo**>>.
