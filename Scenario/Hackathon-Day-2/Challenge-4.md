# Desafio 04: Interaja com a Aplicação de Chat

### Duração Estimada: 30 minutos

## Introdução:

Após implantar com sucesso a aplicação de chat com IA no desafio anterior, o próximo passo é avaliar suas funcionalidades. Neste desafio, você interagirá com o aplicativo para analisar seu potencial de uso em cenários reais na Contoso Ltda, explorando a eficiência das respostas, as capacidades multilíngues e o impacto das configurações avançadas, com o objetivo de construir um caso de negócio convincente para a integração dessas tecnologias na empresa.

## Objetivos do Desafio

**1. Acessar a Aplicação Web e Testar Consultas:**
   
   - No Portal do Azure, procure por **Container Apps** e selecione o aplicativo que você implantou no desafio anterior.
     
   - Clique em **URL da Aplicação** (*Application URL*) para abrir sua aplicação. Você será direcionado para a aplicação de chat **Northwind Health**, como mostrado abaixo.

     ![](../media/lab03-04.png)

- Na aplicação de chat, insira o prompt abaixo e observe como as respostas são geradas pelos serviços do ChatGPT e da Pesquisa Cognitiva do Azure, que interagem para formular consultas de pesquisa e recuperar informações relevantes da base de conhecimento.

   ```
   What does a Product Manager do?
   ```
   
- A resposta não apenas utiliza o conteúdo dos documentos para responder à pergunta, mas também apresenta **citações (1)** que validam a precisão das informações. Ao clicar em uma anotação, o aplicativo direciona você diretamente para a página do **documento (2**) que compara os planos, permitindo ler mais detalhes ou realizar uma validação adicional na seção de **citação**.

- Ao clicar em uma citação, o aplicativo leva diretamente à página do documento que detalha a comparação dos planos, permitindo ler mais informações ou validar a precisão da resposta.
  
- Insira outro prompt e analise a resposta: 

   ```
   Does the project manager manage the human resources team?
   ```

- Na aplicação que construímos, é possível enviar ao prompt, nos bastidores, o contexto das interações anteriores do chat, permitindo que o ChatGPT responda, por exemplo, se o gerente de projeto gerencia a equipe de recursos humanos. Ao clicar na citação, você será direcionado para a parte do plano que contém a informação correspondente.

**2. Capacidade de Consulta Multilíngue:**
   
- Vamos fazer uma pequena alteração no prompt para pedir à OpenAI que receba qualquer pergunta que não seja feita em inglês e responda no idioma em que foi feita. Vá para **Configurações de Desenvolvedor** e adicione a mensagem abaixo na seção **Substituir o modelo de prompt**. Clique em **Fechar**.

  ```
   convert prompts to English and respond when asked questions in different language
   ```

- Com essa substituição, quando uma pergunta é feita em outro idioma, o prompt é convertido nos bastidores para o inglês a fim de realizar a pesquisa. Em seguida, o modelo responde no mesmo idioma em que a pergunta foi feita. Insira o prompt abaixo na seção de chat e observe: a pergunta é detectada em francês, traduzida para o inglês, processada normalmente e, por fim, a resposta é retornada em francês, como esperado.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

**3. Impacto das Configurações Avançadas:** 

- Em **Configurações de Desenvolvedor**, e, na seção **Excluir categoria**, marque a caixa de seleção para **Usar opções semânticas** e **Sugerir perguntas de acompanhamento**. Clique em **Fechar** e observe como as respostas ao prompt mudarão no chat ao inserir a seguinte pergunta.

   ```
   What happens in a performance review?
   ```
**4. Exploração das Capacidades do OpenAI e da Pesquisa de IA:**

  - Conduza seus próprios testes usando vários prompts para avaliar o alcance e a profundidade das capacidades de conversação e pesquisa do aplicativo.
  - Concentre-se em entender como o aplicativo integra o modelo da OpenAI e a Pesquisa de IA para interações de usuário fluidas.

## Critérios de Sucesso:
  - Interação bem-sucedida com a aplicação de chat, explorando diferentes casos de uso em conversas.
  - Compreensão completa das capacidades do aplicativo em lidar com consultas multilíngues, explorar configurações avançadas e demonstrar seu potencial geral para o ambiente da Contoso.
     
> **Observação**: Não há uma validação técnica específica para este desafio, mas sua exploração e compreensão são cruciais.


## Recursos Adicionais:

- Consulte o repositório [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) para informações detalhadas.
