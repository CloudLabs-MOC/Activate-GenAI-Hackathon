# Desafio 04: Interagir com o Chat App

### Duração Estimada: 30 minutos

## Introdução:

Após implantar com sucesso o chat app aprimorado com IA no desafio anterior, é hora de avaliar suas capacidades. Este desafio foca na interação com o aplicativo para entender seu potencial para aplicações do mundo real na Contoso Ltd. Você explorará a eficiência das respostas às consultas, as capacidades multilíngues e o impacto das configurações avançadas, criando um caso de negócio convincente para a integração dessas tecnologias na Contoso.

## Objetivos do Desafio

**1. Acessar a Aplicação Web e Testar Consultas:**
   
   - No Portal do Azure, procure por **Container Apps** e selecione o aplicativo que você implantou no desafio anterior.
   - Clique na URL da Aplicação (*Application URL*) para abrir sua aplicação. Você será direcionado para a aplicação de chat **Northwind Health**, como mostrado abaixo.

     ![](../media/lab03-04.png)

- Na aplicação de chat, insira o prompt abaixo e verifique como as respostas são fornecidas pelos serviços ChatGPT e Azure Cognitive Search, interagindo para construir consultas de busca e recuperar informações da base de conhecimento.

   ```
   What does a Product Manager do?
   ```
   
- A resposta não apenas aborda a pergunta com base no conteúdo dos documentos, mas também incluiu **citações (1)** para validar a precisão das informações. Ao clicar em uma anotação, o aplicativo vai diretamente para a página do **documento (2)** que compara os planos, permitindo que você leia mais ou faça uma validação adicional sobre a precisão da resposta na seção de **citação**. 

- Veja como, ao clicarmos em uma anotação, o aplicativo nos leva diretamente para a página do documento que contém a informação, para que possamos ler mais ou validar a precisão da resposta.
  
- Insira outro prompt e analise a resposta: 

   ```
   Does the project manager manage the human resources team?
   ```

- Conforme a arquitetura do nosso aplicativo, podemos passar o contexto de partes anteriores do chat para o prompt nos bastidores, o que permite ao ChatGPT responder se o gerente de projetos gerencia a equipe de recursos humanos. Clique na citação e você verá a parte do documento que cobre a informação relacionada.

**2. Capacidade de Consulta Multilíngue:**
   
- Vamos fazer uma pequena alteração no prompt para pedir ao OpenAI que responda a qualquer pergunta que não seja feita em inglês no idioma em que foi perguntada. Vá para **Developer Settings** e adicione a mensagem abaixo na seção **Override prompt template**. Clique em **Close**.

  ```
   convert prompts to English and respond when asked questions in different language
   ```

- Com essa substituição, quando fazemos uma pergunta em um idioma diferente, nos bastidores, o prompt é convertido para o inglês para realizar a busca, e então o modelo responderá no mesmo idioma em que a pergunta foi feita. Insira o prompt abaixo na seção de chat e observe que ele recebe a pergunta, detecta que está em francês, converte para o inglês, executa a busca como antes e, em seguida, retorna a resposta esperada, também em francês.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

**3. Impacto das Configurações Avançadas:** 

- Em **Developer Settings**, e, na seção **Exclude category**, marque a caixa para **Use query-contextual summaries instead of whole documents** e **Suggest follow-up questions**. Clique em **Close** e observe como as respostas ao prompt mudarão no chat ao inserir a seguinte pergunta.

   ```
   What happens in a performance review?
   ```
**4. Exploração das Capacidades do OpenAI e AI Search:**

  - Conduza seus próprios testes usando vários prompts para avaliar o alcance e a profundidade das capacidades de conversação e busca do aplicativo.
  - Concentre-se em entender como o aplicativo integra o modelo da OpenAI e o AI Search para interações de usuário fluidas e integradas.

## Critérios de Sucesso:
  - Interação bem-sucedida com a aplicação de chat, explorando uma variedade de casos de uso conversacionais.
  - Compreensão abrangente das capacidades do aplicativo em lidar сom consultas multilíngues, configurações avançadas e seu potencial geral para o ambiente da Contoso.
     
> **Observação**:  Não há uma validação técnica específica para este desafio, mas sua exploração e compreensão são cruciais.


## Recursos Adicionais:

- Consulte o repositório [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) para informações detalhadas.
  
