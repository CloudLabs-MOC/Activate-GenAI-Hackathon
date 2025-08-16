# Desafio 1: Implantar o Serviço OpenAI do Azure e Modelos LLM

### Duração Estimada: 30 minutos

## Introdução:

**Serviço OpenAI do Azure** fornece acesso via API REST aos poderosos modelos de linguagem da OpenAI, incluindo as séries de modelos GPT-4, GPT-4 Turbo with Vision, gpt-35-turbo e Embeddings. Além disso, as novas séries de modelos `GPT-4` e `gpt-35-turbo` estão agora disponíveis para uso geral.

Um **Modelo de Linguagem Grande(Large Language Model-LLM)** é um algoritmo de deep learning que pode realizar uma variedade de tarefas de processamento de linguagem natural (PLN). Os modelos de linguagem grandes usam modelos transformer e são treinados com conjuntos de dados massivos — daí o nome "grande". Isso lhes permite reconhecer, traduzir, prever ou gerar texto e outros conteúdos.

A **Contoso Ltda**, uma empresa líder em tecnologia, busca aprimorar suas operações de suporte ao produto. Eles recebem um grande número de consultas diariamente, o que resulta em maiores tempos de espera e menor satisfação do cliente. Para resolver isso, a Contoso está planejando implementar uma solução potencializada por IA que possa lidar com as perguntas dos clientes de forma eficaz e eficiente.

Eles escolheram implantar o serviço OpenAI do Azure juntamente com seus Modelos de Linguagem Grandes (LLM), como o `gpt-35-turbo` e o `text-embedding-ada-002`. Esses modelos são conhecidos por sua capacidade de processar e gerar texto semelhante ao humano, tornando-os ideais para esta aplicação.

Como parte deste desafio, sua tarefa é criar um serviço OpenAI do Azure e implantar Modelos de Linguagem Grandes (LLM). Os LLMs incluem o **gpt-35-turbo** e **text-embedding-ada-002**.

### Acessando o Portal do Azure

1. Para acessar o portal do Azure, abra uma janela privada/anônima no seu navegador e navegue até o Portal do Azure.

1. Na tela de login do **Microsoft Azure**, você verá campo para login. Insira o seguinte e-mail/nome de usuário e clique em **Avançar**.

   - **E-mail/Nome de usuário:** <inject key="AzureAdUserEmail"></inject>

1. Agora insira a seguinte senha e clique em **Entrar**.

   - **Senha:** <inject key="AzureAdUserPassword"></inject>

1. Se aparecer o pop-up **Continuar conectado?**, clique em **Não**.

1. Se aparecer o pop-up **Você tem recomendações gratuitas do Azure Advisor!**, feche a janela para continuar com o desafio.

1. Se uma janela pop-up **Bem-vindo ao Microsoft Azure** aparecer, clique em **Talvez mais tarde** para ignorar o tour.

## Pré-requisitos

Certifique-se de que você possui o seguinte no ambiente integrado fornecido pelo CloudLabs:

> **Observação:** Os pré-requisitos já estão configurados no ambiente fornecido pelo CloudLabs. Se você estiver usando seu computador pessoal ou laptop, certifique-se de que todos os pré-requisitos necessários estejam instalados para concluir este hackathon.

  - [Assinatura de Azure](https://azure.microsoft.com/en-us/free/)
  - Acesso ao [OpenAI do Azure](https://aka.ms/oai/access) com os seguintes modelos:
    - gpt-35-turbo
    - text-embedding-ada-002
    - gpt-4

## Objetivos do Desafio:

1. **Implantação do Serviço OpenAI do Azure:**
   - Configure uma instância do Serviço OpenAI do Azure com o SKU de tamanho Padrão `S0`.
   - Implante-o no grupo de recursos existente com o nome - **<inject key="Resource Group Name"/>**
   - Obtenha a chave e o Ponto de Extremidade necessários do OpenAI do Azure.

   <validation step="ad89350a-8a60-4fcd-88f1-38493f6f74f7" />

2. **Implantação dos Modelos de Linguagem Grandes (LLM):**
   - O OpenAI do Azure oferece um portal baseado na web chamado Azure OpenAI Studio que você pode usar para implantar, gerenciar e explorar modelos. Você começará sua exploração usando o Azure OpenAI Studio para implantar um modelo.
   - Inicie o Azure AI Foundry a partir do painel Visão geral e implemente dois modelos OpenAI, ou seja, `gpt-35-turbo` e `text-embedding-ada-002`, com uma capacidade TPM de 20k.

   <validation step="22eb5371-de7d-426c-be18-594c9e05c080" />

## Critérios de Sucesso:

- Verifique se o serviço OpenAI do Azure foi implantado com sucesso no grupo de recursos  - <inject key="Resource Group Name"/>.
- Verifique se os Modelos de Linguagem Grande (LLM), `gpt-35-turbo` e `text-embedding-ada-002`, foram implantados com sucesso no Serviço OpenAI do Azure.
  
## Recursos Adicionais:

- Consulte a [documentação do serviço OpenAI do Azure](https://learn.microsoft.com/pt-br/azure/ai-services/openai/) para obter orientação sobre a implantação do serviço.
