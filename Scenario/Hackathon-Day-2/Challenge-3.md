# Desafio 03: Desenvolva um Chat Inteligente com IA

### Tempo Estimado: 150 minutos

## Introdução:

Neste desafio, você implantará uma aplicação de chat com IA desenvolvida especificamente para a Contoso Electronics. Construída com React no frontend e Python no backend, a aplicação oferece recursos avançados, incluindo interfaces de chat e de Perguntas e Respostas (Q&A), todos potencializados por capacidades de IA. Esta é uma excelente oportunidade para explorar a integração do Serviço OpenAI do Azure com o modelo GPT-3.5 Turbo, além do Azure Cognitive Search, garantindo indexação e recuperação eficientes de dados.

Mais do que uma simples interface de chat, esta aplicação de exemplo demonstra o padrão de Geração Aumentada por Recuperação (RAG), proporcionando uma experiência rica, semelhante à do ChatGPT, aplicada aos dados da Contoso. Entre seus recursos estão a avaliação da confiabilidade das respostas com citações, rastreamento da origem do conteúdo, preparação de dados, construção de prompts e orquestração da interação entre o modelo ChatGPT e o Cognitive Search. A interface do usuário permite ajustes e experimentações, além de oferecer monitoramento opcional de desempenho por meio do Application Insights.

Sua missão neste desafio é implantar essa solução de chat completa, permitindo que a Contoso avalie suas capacidades e a integre em seu ambiente corporativo. O repositório inclui dados de amostra, oferecendo uma solução ponta a ponta pronta para uso. Essa aplicação é uma ferramenta valiosa para que os funcionários da Contoso consultem informações sobre benefícios, políticas internas, descrições de cargos e funções.

Você usará Bicep para provisionar a aplicação de chat.

A aplicação se integra de forma transparente com diversos serviços do Azure para fornecer uma experiência de usuário inteligente. A seguir, apresentamos uma visão geral de cada serviço utilizado:

- **Container Apps:** O Azure Container Apps implanta e escala aplicações em contêineres sem esforço, garantindo confiabilidade com escalonamento automático e integração com o Azure Monitor.
- **Application Insights:** Monitoriza proativamente o desempenho da aplicação, cuidando dos problemas antes que se tornem significativos.
- **Document Intelligence:** Usando IA, entende o conteúdo dos documentos carregados, tornando as informações do usuário mais perspicazes.
- **OpenAI do Azure:** Aprimora as capacidades da aplicação com compreensão e respostas em linguagem natural.
- **Painel Compartilhado:** Atua como um hub central para colaboração da equipe e compartilhamento de dados.
- **Regra de Alerta do Detector Inteligente:** Monitora a saúde da aplicação e notifica a equipe se surgirem problemas.
- **Serviço de Pesquisa:** Capacita os usuários com funcionalidades de pesquisa dinâmicas e eficientes dentro da aplicação.
- **Log Analytics Workspace:** Rastreia e analisa a atividade da aplicação, oferecendo insights valiosos e logs.
- **Plano de Serviço de Aplicativo:** Otimiza a alocação de recursos para um desempenho ideal da aplicação.
- **Conta de Armazenamento:** Armazena com segurança os dados que serão usados pelo serviço Azure AI Search para fornecer as entradas para a aplicação de chat.

Juntos, esses serviços criam uma aplicação de chat responsiva que combina recursos de IA, capacidades de monitoramento e gerenciamento eficiente de dados, proporcionando à Contoso uma experiência de usuário excepcional.

## Diagrama de arquitetura:

![](../media/Active-image258.png)


## Pré-requisitos

Certifique-se de ter o seguinte no ambiente integrado fornecido pela CloudLabs:

> **Observação:** Os pré-requisitos já estão configurados no ambiente fornecido pela CloudLabs. Se você estiver usando seu computador pessoal ou notebook, certifique-se de que todos os pré-requisitos necessários estão instalados para concluir este hackathon.

  - [Assinatura do Azure](https://azure.microsoft.com/en-us/free/)
  - Acesso ao [OpenAI do Azure](https://aka.ms/oai/access) disponível com os seguintes modelos:
    - gpt-35-turbo
    - text-embedding-ada-002
   - Bicep 
   - Azd 
   - Poweshell 7 

## Objetivos do Desafio:

> **Observação**: Ao implantar serviços neste desafio, certifique-se de usar o grupo de recursos chamado Activate-GenAI.

> **Importante**: Execute o Powershell 7 ou superior.

1. **Clone o Repositório:**
   - Clone o repositório Active Gen AI: `https://github.com/Azure-Samples/azure-search-openai-demo`.
   - Verifique se o Bicep está instalado em sua máquina. Se não, siga o [guia de instalação de Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/install)).

1. **Implantar a Aplicação de Chat com IA:**

    - Implante uma aplicação de chat com IA no Azure, integrando os serviços de IA do Azure e o Azure Search, e garantindo que ela esteja acessível e funcional após a implantação.
    
      > **Dica** : Comece garantindo que você tenha as credenciais adequadas. Este comando o guiará para fazer login em sua conta do Azure usando a CLI do Desenvolvedor do Azure. Uma vez autenticado, você terá acesso aos seus recursos do Azure.
    
      > **Dica** : Inicialize seu projeto com um modelo específico. Este comando o ajudará a configurar o ambiente do seu projeto.

      > **Dica** : Coloque o seu projeto em ação. Este comando provisionará a sua aplicação no Azure, configurando automaticamente todos os recursos e configurações necessários.

   <validation step="36681298-5586-4465-ae71-717f0f69e6dc" />

## Critérios de Sucesso:

- Provisionamento bem sucedido da aplicação de Chat.
- Verifique se os seguintes serviços estão provisionados com sucesso no Grupo de Recursos.
  - App Service
  - Document Intelligence
  - OpenAI do Azure
  - Painel Compartilhado
  - Regra de Alerta do Detector Inteligente
  - Serviço de Pesquisa
  - Log Analytics Workspace
  - Plano de Serviço de Aplicativo
  - Conta de Armazenamento
- Validar se os dados foram populados no contêiner de armazenamento chamado `content`.
- A aplicação de Chat deve estar acessível usando o Serviço de Aplicativo do Azure.

## Recursos Adicionais:

-  Consulte o [repositório do GitHub da demonstração do Azure Search OpenAI](https://github.com/cmendible/azure-search-openai-demo) para informações detalhadas sobre a arquitetura.
-  [Azure copilot](https://learn.microsoft.com/en-us/azure/copilot/overview)
