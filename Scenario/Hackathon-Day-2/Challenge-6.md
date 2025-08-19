# Desafio-06: Implementar Monitoramento e Logging do OpenAI do Azure com o Serviço de Gerenciamento de API (APIM)

### Duração Estimada: 90 minutos

## Introdução:

Com base no sucesso da integração do processamento de documentos sem servidor à aplicação de chat com IA da Contoso, o próximo objetivo é operacionalizar essas soluções do Azure OpenAI com mecanismos robustos de monitoramento e geração de logs. Neste desafio, você explorará em profundidade a configuração e análise de sistemas avançados de monitoramento utilizando o Azure API Management e o Log Analytics Workspace. Esse é um passo essencial para garantir a operação contínua e estável das soluções de IA desenvolvidas, além de fornecer insights valiosos sobre o desempenho do sistema e as interações dos usuários, permitindo uma gestão mais proativa e eficiente.

Sua tarefa é implementar um monitoramento completo do serviço Azure OpenAI, utilizando configurações de diagnóstico e consultas Kusto para realizar uma análise detalhada dos logs. Além disso, você integrará o Azure API Management para acompanhar as interações de chat, supervisionando as conclusões de mensagens e investigando de forma mais profunda os prompts e as respostas. Esse nível de monitoramento é fundamental para que a Contoso mantenha uma aplicação de chat com IA confiável, eficiente e voltada para a melhor experiência do usuário.

## Objetivos do Desafio:

> **Importante**: Ao implantar serviços neste desafio, certifique-se de usar o grupo de recursos chamado **rg-activategenai**!

1. **Monitorando o Serviço do OpenAI do Azure:**
   
   - Configure as configurações de diagnóstico para os serviços existentes do OpenAI do Azure.
   - Acesse o Playground do Chat usando GPT-3.5 ou superior e utilize a API de Conclusões de Chat para ingerir logs adicionais e interagir com eles, permitindo analisar e testar respostas de forma prática.

      > **Observação:** Configure o Playground do Chat para que o modelo se comporte como um professor de IA.
    
    - Conduza a análise de logs utilizando **Consultas Kusto** para monitorar o desempenho e o uso do serviço.
        -  Use esta consulta para visualizar rapidamente eventos de diagnóstico recentes e focar em detalhes-chave como hora, recurso, categoria e tipo de operação.

           ```
           AzureDiagnostics
           take 100
           project TimeGenerated, _ResourceId, Category, OperationName
           ```

            > **Observação:** Os logs podem levar de 10 a 15 minutos para aparecer, então aguarde um pouco se eles não surgirem imediatamente.

2. **Monitorando os prompts do OpenAI usando o Gerenciamento de API do Azure:**  

    - Configure o Gerenciamento de API do Azure no grupo de recursos: **rg-activategenai** e na camada de preço: **Standard (99.95% SLA)**.
    - Implante o serviço de Gerenciamento de API e também habilite as **Identidades Gerenciadas atribuídas pelo sistema**.
    - Atribua a função de **Usuário dos Serviços Cognitivos** à identidade gerenciada do serviço de Gerenciamento de API nas configurações de **Controle de Acesso (IAM)** do Serviço OpenAI. 
    - Do recurso OpenAI criado anteriormente, recupere os valores da chave e do ponto de extremidade para o OpenAI do Azure. 
    - Configure o Gerenciamento de API do Azure para capturar as solicitações do usuário e as respostas do modelo OpenAI, que não são registradas apenas pelo workspace do Log Analytics.
        
        - Importe a especificação OpenAPI usando a seguinte URL:

          ```
          https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
          ```

          > **Observação:** Para evitar a duplicação da API, escolha o método "Atualizar" em vez de "Criar nova". Além disso, verifique se a URL do OpenAPI está correta e acessível, pois, caso contrário, a importação poderá falhar silenciosamente sem exibir erros evidentes. 

    -  Revise a API recém-adicionada para confirmar que várias operações POST estão presentes e, em seguida, atualize suas configurações para usar o cabeçalho correto da chave de assinatura. 
    - Crie um novo **Produto** no Gerenciamento de API e vincule-o à API do Serviço OpenAI do Azure.

    - Adicione uma nova **Assinatura** no Gerenciamento de API para fins de teste.

    - Edite a política de entrada (*inbound policy*) usando a política fornecida abaixo para **All Operations**, utilizando o Editor de Código.

      ```
      <inbound>
      <base />
      <set-header name="api-key" exists-action="delete" />
      <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
      <set-header name="Authorization" exists-action="override">
      <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
      </set-header>
      <set-backend-service base-url="https://<<Azure_OpenAI_Endpoint>>/openai" />
      </inbound>
      ```

      > **Observação:** Substitua https://<<Azure_OpenAI_Endpoint>>  pelo endpoint copiado anteriormente.
    
    - Configure os **Diagnósticos** para a API recém-adicionada, habilitando a geração de logs do Azure Monitor. Isso ajudará a capturar os payloads detalhados de solicitação e resposta para monitoramento e solução de problemas.
      
    - Teste a API configurada executando uma solicitação **POST** para gerar conclusões de chat e validar a integração.
        
        -  Na seção **Request body**, atualize o conteúdo de amostra com o seguinte prompt:

            ```
            {"model":"gpt-35-turbo","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
            ``` 
    - Utilize **Consultas Kusto** dentro do Serviço de Gerenciamento de API para analisar os logs do OpenAI.
        
        - Elabore uma nova consulta inserindo a seguinte consulta no editor para monitorar o uso de tokens por IP e modelo.

            ```
            ApiManagementGatewayLogs
            | where tolower(OperationId) in ('completions_create','chatcompletions_create')
            | where ResponseCode  == '200'
            | extend modelkey = substring(parse_json(BackendResponseBody)['model'], 0, indexof(parse_json(BackendResponseBody)['model'], 
            '-', 0, -1, 2))
            | extend model = tostring(parse_json(BackendResponseBody)['model'])
            | extend prompttokens = parse_json(parse_json(BackendResponseBody)['usage'])['prompt_tokens']
            | extend completiontokens = parse_json(parse_json(BackendResponseBody)['usage'])['completion_tokens']
            | extend totaltokens = parse_json(parse_json(BackendResponseBody)['usage'])['total_tokens']
            | extend ip = CallerIpAddress
            | where model !=  ''
            | summarize
            sum(todecimal(prompttokens)),
            sum(todecimal(completiontokens)),
            sum(todecimal(totaltokens)),
            avg(todecimal(totaltokens))
            by ip, model
            ```
            
             > **Observação:** Se você receber o erro informando "Nenhum resultado encontrado no intervalo de tempo personalizado, Tente <u>select another time range</u>" levará algum tempo para que os dados sejam refletidos. 

   <validation step="9f41c452-42da-4841-9ee1-0c8fcbdbd9ad" />
  
## Critérios de Sucesso:

Os participantes serão avaliados com base nos seguintes critérios:

1. Configurar com sucesso o serviço OpenAI do Azure com as configurações de diagnóstico apropriadas e analisar seus logs usando Consultas Kusto.
   
3. Criar e configurar eficazmente o Gerenciamento de API do Azure, garantindo uma visibilidade clara dos logs e dos prompts do OpenAI através de uma análise detalhada com Consultas Kusto.

## Recursos Adicionais:

- Consulte [Como Configurar o Serviço de Gerenciamento de API do Azure](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md) para mais informações.
- Consulte este video sobre [Gerando Logs e Monitorando Tudo no Azure OpenAI com o Serviço de Gerenciamento de API](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md).
- Consulte o tutorial [Tutorial de Consultas Kusto](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial) para mais informações.
