# Desafio 04: Interaja com o aplicativo de bate-papo

### Tempo Estimado: 30 minutos

## Introdução:

Após implantar com sucesso a aplicação de chat com IA no desafio anterior, o próximo passo é avaliar suas funcionalidades. Neste desafio, você interagirá com o aplicativo para analisar seu potencial de uso em cenários reais na Contoso Ltda, explorando a eficiência das respostas, as capacidades multilíngues e o impacto das configurações avançadas, com o objetivo de construir um caso de negócio convincente para a integração dessas tecnologias na empresa.

## Guia da Solução

### Tarefa 1: Interaja com a Aplicação de Chat com o LLM do OpenAI do Azure

Um dos temas mais populares no momento são os modelos de grande porte; os usuários estão particularmente interessados no GPT de conversação. O mais intrigante sobre todos esses modelos base — incluindo o Chat GPT — é que, embora eles tenham um desempenho admirável por si sós, eles se saem ainda melhor quando combinados com seus próprios dados.

1. Na página do Portal de Azure, na caixa **Pesquisar recursos, serviços e documentos (G+/)** no topo do portal, digite **Aplicativos de Contêiner**, e, em seguida, selecione **Aplicativos de Contêiner**.

   ![](../media/imag06.png)

1. Selecione **Webapp**.

   ![](../media/imag07.png)
      
1. Em seguida, clique em **URL da Aplicação** para abrir a sua aplicação web.

   ![](../media/imag08.png)
   
1. Você será direcionado para a **Northwind Health chat application** como mostrado abaixo. 

   ![](../media/lab03-04.png)

1. Na aplicação de chat, forneça o prompt abaixo e verifique como as respostas são dadas pelos serviços do ChatGPT e da Pesquisa Cognitiva do Azure, interagindo para construir consultas de pesquisa e recuperar informações candidatas da base de conhecimento.

   ```
   What does a Product Manager do?
   ```

   ![](../media/Active-image115.png)

- A resposta não apenas utiliza o conteúdo dos documentos para responder à pergunta, mas também apresenta **citações (1)** que validam a precisão das informações. Ao clicar em uma anotação, o aplicativo direciona você diretamente para a página do **documento (2**) que compara os planos, permitindo ler mais detalhes ou realizar uma validação adicional na seção de **citação**.

- Ao clicar em uma citação, o aplicativo leva diretamente à página do documento que detalha a comparação dos planos, permitindo ler mais informações ou validar a precisão da resposta.
  
- Insira outro prompt e analise a resposta: 

   ```
   Does the project manager manage the human resources team?
   ```

- Na aplicação que construímos, é possível enviar ao prompt, nos bastidores, o contexto das interações anteriores do chat, permitindo que o ChatGPT responda, por exemplo, se o gerente de projeto gerencia a equipe de recursos humanos. Ao clicar na citação, você será direcionado para a parte do plano que contém a informação correspondente.


   ![](../media/3-6.1.png)
   
   ![](../media/3-7.png)

1. Vamos fazer uma pequena alteração no prompt para pedir à OpenAI que receba qualquer pergunta que não seja feita em inglês e responda no idioma em que foi feita. Vá para **Configurações de Desenvolvedor** e adicione a mensagem abaixo na seção **Substituir o modelo de prompt**. Clique em **Fechar**.

      ```
      convert prompts to English and respond when asked questions in a different language
      ```

      ![](../media/Active-image117.png)
   
      ![](../media/Active-image118.png)

1. Com essa substituição, quando uma pergunta é feita em outro idioma, o prompt é convertido nos bastidores para o inglês a fim de realizar a pesquisa. Em seguida, o modelo responde no mesmo idioma em que a pergunta foi feita. Insira o prompt abaixo na seção de chat e observe: a pergunta é detectada em francês, traduzida para o inglês, processada normalmente e, por fim, a resposta é retornada em francês, como esperado.

   ```
   Quelles sont les responsabilités du responsible marketing?
   ```

   ![](../media/3-8.png)

1. Em **Configurações de Desenvolvedor**, e, na seção **Excluir categoria**, marque a caixa de seleção para **Usar opções semânticas** e **Sugerir perguntas de acompanhamento**. Clique em **Fechar** e observe como as respostas ao prompt mudarão no chat ao inserir a seguinte pergunta.

   ![](../media/Active-image119.png)

1. Insira o prompt e observe como as respostas ao prompt mudarão no chat ao fornecer o prompt abaixo.

   ```
   What happens in a performance review?
   ```

   ![](../media/3-10.png)

## Critérios de Sucesso:

  - Interação bem-sucedida com a aplicação de chat, explorando diferentes casos de uso em conversas.
  - Compreensão completa das capacidades do aplicativo em lidar com consultas multilíngues, explorar configurações avançadas e demonstrar seu potencial geral para o ambiente da Contoso.
     
    > **Importante**: Não há validação específica para este desafio, mas sua exploração e compreensão são cruciais.

## Recursos Adicionais:

- Consulte [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) para mais informação.

## Prossiga para o próximo Desafio clicando em **Próximo**>>.
