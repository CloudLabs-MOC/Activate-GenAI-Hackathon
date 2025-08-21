# Desafio 01: Implantar o Serviço Azure OpenAI e Modelos LLM

### Duração Estimada: 30 minutos

## Introdução

Bem-vindo(a) ao Desafio de Implantação do Serviço Azure OpenAI! Este desafio foi projetado para testar suas habilidades na implantação do Serviço Azure OpenAI e de seus Modelos de Linguagem Grandes (LLM). O objetivo é configurar o Serviço Azure OpenAI e implantar os modelos LLM.

O **Serviço Azure OpenAI** fornece acesso via API REST aos poderosos modelos de linguagem da OpenAI, incluindo as séries de modelos GPT-4, GPT-4 Turbo with Vision, gpt-35-turbo e Embeddings. Além disso, as novas séries de modelos `GPT-4` e `gpt-35-turbo` estão agora disponíveis para uso geral.

Um **Modelo de Linguagem Grande(Large Language Model-LLM)** é um algoritmo de *deep learning* que pode realizar uma variedade de tarefas de processamento de linguagem natural (PLN). Os modelos de linguagem grandes usam modelos transformer e são treinados com conjuntos de dados massivos — daí o nome "grande". Isso lhes permite reconhecer, traduzir, prever ou gerar texto e outros conteúdos.

A **Contoso Ltda**, uma empresa líder em tecnologia, busca aprimorar suas operações de suporte ao produto. Eles recebem um grande número de consultas diariamente, o que resulta em maiores tempos de espera e menor satisfação do cliente. Para resolver isso, a Contoso está planejando implementar uma solução potencializada por IA que possa lidar com as perguntas dos clientes de forma eficaz e eficiente.

Eles escolheram implantar o serviço Azure OpenAI juntamente com seus Modelos de Linguagem Grandes (LLM), como o `gpt-35-turbo` e o `text-embedding-ada-002`. Esses modelos são conhecidos por sua capacidade de processar e gerar texto semelhante ao humano, tornando-os ideais para esta aplicação.

Como parte deste desafio, sua tarefa é criar um serviço Azure OpenAI e implantar Modelos de Linguagem Grandes (LLM). Os LLMs incluem o **gpt-35-turbo** e **text-embedding-ada-002**.

## Descrição

Sua tarefa é implantar o Serviço Azure OpenAI e Large Language Models (LLM).

### Acessando o portal do Azure

>**Importante**: Você pode encontrar o nome de usuário e a senha no ambiente navegando até a aba **Ambiente** no painel esquerdo e, em seguida, copiar o **Nome de Usuário do Azure** e a **Senha do Azure**, que serão necessários para entrar no portal do Azure em etapas posteriores. também pode anotar **Deployment ID**, que pode ser usado para fornecer um nome exclusivo aos recursos durante a implantação.

>**Observação**: Os valores de números e IDs podem variar; por favor,ignore os valores nas capturas de tela e copie os valores da aba **Ambiente**.

![](../media/1-11-24(18).png)

1. Para acessar o portal do Azure, dentro VM do laboratório, abra o **Microsoft Edge** e navegue até o [Portal do Azure](https://portal.azure.com/).

1. Na aba **Entrar no Microsoft Azure**, você verá uma tela de login. Insira o seguinte e-mail/usuário e clique em **Avançar** **(2)**.

    - **E-mail/Usuário:** **(1)** <inject key="AzureAdUserEmail"></inject>

        ![](../media/1-11-24(1).png)

1. Agora insira a seguinte senha e clique em **Entrar** **(2)**.

    - **Senha:** **(1)** <inject key="AzureAdUserPassword"></inject>

        ![](../media/1-11-24(2).png)

1. Quando a janela **Ação necessária** aparecer, clique em **Perguntar depois**.

1. Se aparecer o pop-up **Continuar conectado?**, clique em **Não**.

    ![](../media/1-11-24(3).png)

1. Se uma janela pop-up **Bem-vindo ao Microsoft Azure** aparecer, clique em **Cancelar** para ignorar o tour.

    ![](../media/1-11-24(4).png)

## Pré-requisitos

- [Assinatura de Azure](https://azure.microsoft.com/en-us/free/)
  - Acesso ao [Azure OpenAI](https://aka.ms/oai/access) com os seguintes modelos:
    - gpt-35-turbo
    - text-embedding-ada-002
    - gpt-4

## Guia de solução

### Tarefa 1: Implantar um Serviço Azure OpenAI

Nesta tarefa, você aprenderá o processo de configurar e implantar o serviço Azure OpenAI dentro do Portal do Azure.

1. Na página do Portal do Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** no topo do portal, digite **Azure OpenAI (1)** e selecione **Azure OpenAI (2)** em serviços.

    ![](../media/1-11-24(5).png)

1. No painel **AI foundry | OpenAI**, clique em **+ Criar**.

    ![](../media/1-11-24(6).png)

1. Especifique os seguintes dados para implantar o serviço Azure OpenAI e clique em **Avançar (6)** três vezes.

    | **Opção** | **Valor** |
    | ------------------ | ----------------------------------------------------- |
    | Assinatura | Deixar padrão **(1)** |
    | Grupo de recursos | **Activate-GenAI (2)** |
    | Região | Use o mesmo local do grupo de recursos **(3)** |
    | Nome | Use o formato **OpenAI-xxxxxx** (substitua **xxxxxx** pelo **Deployment ID**) **(4)** |
    | Faixas de preço | **Standard S0 (5)** |

    >**Observação**: aqui, xxxxxx se refere ao **Deployment ID** que você registrou na última tarefa.

    ![](../media/1-11-24(7).png)

1. Uma vez que a validação for bem-sucedida no **Examinar + enviar**, clique em **Criar** e aguarde a conclusão da implantação.

    ![](../media/1-11-24(8).png)

    ![](../media/1-11-24(9).png)

### Tarefa 2: Implantar um modelo

O Azure OpenAI fornece um portal baseado na Web chamado Azure AI Foundry, que você pode usar para implantar, gerenciar e explorar modelos. Você começará sua exploração do Azure OpenAI usando o Azure AI Foundry para implantar um modelo.

1. Na página do Portal do Azure, na caixa Pesquisar recursos, serviços e documentos (G+/) na parte superior do portal, insira **Azure OpenAI (1)** e selecione **Azure OpenAI (2)** em serviços.

    ![](../media/1-11-24(5).png)

1. No painel **AI Foundry | OpenAI (1)**, selecione **OpenAI-<inject key="Deployment-id" enableCopy="false"></inject> (2)**.

    ![](../media/1-11-24(10).png)

1. No painel de recursos do Azure OpenAI, selecione **Visão geral (1)** no menu à esquerda e clique em **Go to Azure AI Foundry (2)**. Isso o levará ao Azure AI Studio.

    ![](../media/1-11-24(11).png)

    >**Observação:** se o pop-up Discover an even better Azure AI Studio experience aparecer, clique em Fechar para descartá-lo.

1. Clique em **Implantações (1)** em **Recursos compartilhados** e selecione **+ Implante o modelo (2)**. Em seguida, **Implantar o modelo básico (3)**.

    ![](../media/1-11-24(12).png)

1. Pesquise por **gpt-35-turbo (1)** e clique em **Confirmar (2)**.

    ![](../media/1-11-24(13).png)

1. Na interface pop-up do **Implantar Modelo**, clique em **Personalizar** e insira os seguintes dados:

    - **Nome da implantação (1)**: text-turbo
    - **Tipo de implantação (2)**: Standard
    - **Versão do modelo (3)**: 0301(Padrão)
    - **Limite de Taxa de Tokens por Minuto (4)**: 20K
    - **Habilitar cota dinâmica (5)**: Habilitado
    - Clique em **Implantar (6)**

        ![](../media/1-11-24(14).png)

        >**Observação:** se a opção **Personalizar** não aparecer, você pode inserir diretamente os detalhes da implantação do modelo.

1. Clique em **Implantações (1)** em **Recursos compartilhados** e selecione **+ Implante o modelo (2)**. Em seguida, **Implantar o modelo básico (3)**.

    ![](../media/1-11-24(12).png)

1. Pesquise por **text-embedding-ada-002 (1)** e clique em **Confirmar (2)**.

    ![](../media/1-11-24(15).png)

1. Na interface pop-up do **Implantar Modelo**, clique em **Personalizar** e insira os seguintes dados:

    - **Nome da implantação (1)**: text-ada-002
    - **Tipo de implantação (2)**: Standard
    - **Versão do modelo (3)**: 2 (Padrão)
    - **Limite de Taxa de Tokens por Minuto (4)**: 20K
    - **Habilitar cota dinâmica (5)**: Habilitado
    - Clique em **Implantar (6)**

        ![](../media/1-11-24(16).png)

        >**Observação:** se a opção **Personalizar** não aparecer, você pode inserir diretamente os detalhes da implantação do modelo.

1. De volta à página Implantações, você deve ver os modelos de implantação **text-turbo** e **text-ada-002** criados.

    ![](../media/1-11-24(17).png)


## Critérios de Sucesso:

- Verifique se o serviço Azure OpenAI foi implantado com sucesso no grupo de recursos  -<inject key="Resource Group Name"/>.
- Verifique se os Modelos de Linguagem Grande (LLM), `gpt-35-turbo` e `text-embedding-ada-002`, foram implantados com sucesso no Serviço Azure OpenAI.
  
## Recursos Adicionais:

- Consulte a [documentação do serviço Azure OpenAI](https://learn.microsoft.com/pt-br/azure/ai-services/openai/) para obter orientação sobre a implantação do serviço.

### Prossiga com o próximo desafio clicando em **Avançar**>>.
