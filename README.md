# 🤖 AWS GenAI Smart Assistant Lab

![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Amazon Bedrock](https://img.shields.io/badge/Amazon_Bedrock-Generative_AI-FF9900?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-Knowledge_Base-1565C0?style=for-the-badge)
![MCP](https://img.shields.io/badge/MCP-Agent_Tools-6A1B9A?style=for-the-badge)
![Lambda](https://img.shields.io/badge/AWS_Lambda-Serverless-FF9900?style=for-the-badge&logo=awslambda&logoColor=white)
![DynamoDB](https://img.shields.io/badge/DynamoDB-NoSQL-4053D6?style=for-the-badge&logo=amazondynamodb&logoColor=white)

Laboratório hands-on de **Inteligência Artificial Generativa na AWS**, realizado no **AWS SimuLearn** durante o programa **AWS re/Start**.

O laboratório teve como objetivo configurar e validar um **assistente inteligente de RH** capaz de consultar uma base de conhecimento e executar ações por meio da integração entre serviços de IA, serverless e armazenamento da AWS.

---

## 🎯 Objetivo

Configurar e validar uma arquitetura de assistente de IA capaz de:

- responder perguntas utilizando uma base de conhecimento;
- recuperar informações por meio de RAG;
- conectar o agente a ferramentas externas;
- utilizar MCP para integração entre agente e serviços;
- executar funções AWS Lambda;
- registrar solicitações no Amazon DynamoDB;
- utilizar arquivos armazenados no Amazon S3;
- validar o funcionamento completo da solução.

---

## 🏗️ Arquitetura

O fluxo utilizado no laboratório pode ser representado da seguinte forma:

```text
Usuário
   │
   ▼
Web Application / Chat
   │
   ▼
Amazon Bedrock AgentCore
   │
   ├──────────────────────► Knowledge Base / RAG
   │                              │
   │                              ▼
   │                          Amazon S3
   │
   ▼
Amazon Bedrock AgentCore Gateway
   │
   │ MCP
   ▼
AWS Lambda
submit_benefits
   │
   ▼
Amazon DynamoDB
BenefitsTable
```

A arquitetura combina **IA Generativa, recuperação de conhecimento e execução de ações**, permitindo que o assistente não apenas responda perguntas, mas também interaja com outros serviços.

---

## ☁️ Serviços e tecnologias

Durante o laboratório foram utilizados conceitos e serviços relacionados a:

- Amazon Bedrock AgentCore
- Amazon Bedrock AgentCore Gateway
- Amazon Bedrock Knowledge Base
- RAG — Retrieval-Augmented Generation
- MCP — Model Context Protocol
- AWS Lambda
- Amazon DynamoDB
- Amazon S3
- AWS CloudFormation
- AWS IAM
- Aplicação Web / Chat
- Arquitetura Serverless
- Integração entre serviços AWS

---

## 🧠 IA Generativa e Agentes de IA

O laboratório demonstra um padrão no qual um assistente de IA pode combinar geração de respostas com recuperação de conhecimento e utilização de ferramentas.

```text
Assistente de IA
      │
      ├──── Recupera conhecimento
      │           │
      │           ▼
      │     Knowledge Base / RAG
      │
      └──── Executa ações
                  │
                  ▼
             MCP Gateway
                  │
                  ▼
               Lambda
                  │
                  ▼
              DynamoDB
```

Essa arquitetura permite que o modelo de linguagem seja integrado a recursos externos em vez de funcionar apenas como um chatbot isolado.

---

## 🔎 Knowledge Base e RAG

O assistente utiliza uma **Knowledge Base do Amazon Bedrock** para recuperar informações relevantes a partir de documentos armazenados no Amazon S3.

O fluxo conceitual é:

```text
Pergunta do usuário
        │
        ▼
Amazon Bedrock AgentCore
        │
        ▼
Knowledge Base
        │
        ▼
Recuperação de contexto
        │
        ▼
Resposta fundamentada nos documentos
```

Esse padrão é conhecido como **Retrieval-Augmented Generation (RAG)**.

O RAG permite combinar modelos de linguagem com informações externas ou corporativas, aumentando a capacidade do assistente de responder utilizando um contexto específico.

---

## 🔌 Integração com MCP

Durante a etapa prática foi configurado um destino no **Amazon Bedrock AgentCore Gateway**.

O destino criado foi:

```text
submitBenefits
```

Esse destino foi integrado à função:

```text
submit_benefits
```

utilizando o **Model Context Protocol (MCP)**.

O MCP permite disponibilizar ferramentas e recursos externos para agentes de IA através de uma interface padronizada.

---

## 📄 Schema da ferramenta

Para disponibilizar a função ao agente, foi utilizado um arquivo de schema armazenado no Amazon S3.

Arquivo utilizado:

```text
submit_benefits.json
```

O schema define a estrutura dos dados esperados pela ferramenta e permite que o agente compreenda como utilizá-la.

O fluxo foi:

```text
Amazon S3
   │
   ▼
Schema da ferramenta
   │
   ▼
AgentCore Gateway
   │
   ▼
MCP
   │
   ▼
AWS Lambda
```

---

## ⚡ AWS Lambda

A função AWS Lambda utilizada no laboratório foi:

```text
submit_benefits
```

Ela foi integrada ao AgentCore Gateway para processar solicitações de benefícios enviadas pelo assistente.

Fluxo:

```text
Usuário
   │
   ▼
Assistente de IA
   │
   ▼
Amazon Bedrock AgentCore
   │
   ▼
MCP Gateway
   │
   ▼
AWS Lambda
   │
   ▼
Amazon DynamoDB
```

Esse processo demonstra como agentes de IA podem utilizar funções serverless para executar ações dentro de uma aplicação.

---

## 🗄️ Amazon DynamoDB

Após a execução da função Lambda, os dados da solicitação foram persistidos no Amazon DynamoDB.

Tabela utilizada:

```text
BenefitsTable
```

Durante a validação foi possível confirmar atributos como:

```text
employee_name
benefit_type
claim_amount
```

Exemplo utilizado durante o laboratório:

```text
employee_name: Jane Doe
benefit_type: medical
claim_amount: 250
```

A presença desse registro confirmou que a chamada realizada pelo assistente percorreu corretamente a arquitetura até a camada de persistência.

---

## 💬 Validação pelo assistente

A aplicação disponibilizou uma interface de chat para interação com o assistente de RH.

Durante a validação foi enviada uma solicitação de benefício pelo chat.

O fluxo executado foi:

```text
Chat
  │
  ▼
Amazon Bedrock AgentCore
  │
  ▼
AgentCore Gateway
  │
  ▼
MCP
  │
  ▼
AWS Lambda
  │
  ▼
Amazon DynamoDB
```

O assistente confirmou o processamento da solicitação e o registro correspondente foi posteriormente verificado no DynamoDB.

---

## 🧪 Atividades hands-on realizadas

Durante o laboratório:

- explorei a arquitetura de uma solução de IA Generativa na AWS;
- utilizei o Amazon Bedrock AgentCore;
- trabalhei com Amazon Bedrock Knowledge Base;
- analisei o funcionamento de RAG em uma solução de IA;
- configurei um destino no AgentCore Gateway;
- utilizei MCP para integração entre agente e ferramenta;
- conectei o Gateway a uma função AWS Lambda;
- utilizei um schema armazenado no Amazon S3;
- configurei o destino `submitBenefits`;
- integrei a função `submit_benefits`;
- utilizei a aplicação de chat do laboratório;
- enviei uma solicitação através do assistente;
- validei a execução da ação;
- consultei os dados no Amazon DynamoDB;
- confirmei a persistência das informações na `BenefitsTable`;
- naveguei pelos recursos provisionados via AWS CloudFormation;
- validei o fluxo completo da solução.

---

## ✅ Resultado

O laboratório foi concluído e validado com sucesso no **AWS SimuLearn**.

Fluxo validado:

```text
Usuário
  │
  ▼
Chat
  │
  ▼
Amazon Bedrock AgentCore
  │
  ▼
Knowledge Base / RAG
  │
  └───────────────┐
                  │
                  ▼
         AgentCore Gateway
                  │
                  ▼
                 MCP
                  │
                  ▼
             AWS Lambda
                  │
                  ▼
          Amazon DynamoDB
```

A solicitação enviada pelo assistente foi processada corretamente e o registro foi confirmado no DynamoDB.

---

## 💡 Principais aprendizados

O laboratório proporcionou prática em conceitos relacionados a:

- Inteligência Artificial Generativa;
- agentes de IA;
- Amazon Bedrock;
- Amazon Bedrock AgentCore;
- RAG;
- Knowledge Bases;
- MCP;
- integração de agentes com ferramentas;
- AWS Lambda;
- arquiteturas serverless;
- Amazon DynamoDB;
- Amazon S3;
- bancos de dados NoSQL;
- persistência de dados;
- integração entre serviços AWS;
- IAM;
- CloudFormation;
- execução de ações por agentes;
- validação end-to-end de aplicações de IA.

---

## 🔄 Fluxo de dados

Uma das principais práticas observadas no laboratório foi compreender como os diferentes componentes trabalham em conjunto.

```text
1. Usuário envia uma solicitação
               │
               ▼
2. Aplicação envia a mensagem ao agente
               │
               ▼
3. AgentCore interpreta a solicitação
               │
               ├────► Knowledge Base / RAG
               │
               ▼
4. Agente identifica necessidade de executar ação
               │
               ▼
5. AgentCore Gateway disponibiliza ferramenta
               │
               ▼
6. MCP conecta o agente à ferramenta
               │
               ▼
7. AWS Lambda processa a solicitação
               │
               ▼
8. DynamoDB armazena os dados
               │
               ▼
9. Resultado é retornado ao usuário
```

---

## 🎓 Contexto do projeto

Este projeto foi realizado em um **ambiente hands-on de laboratório AWS SimuLearn**, como parte do processo de aprendizagem em cloud e Inteligência Artificial.

O laboratório disponibilizou uma arquitetura e recursos previamente preparados, enquanto a atividade prática envolveu **configuração, integração, execução e validação dos componentes da solução**.

Portanto, este repositório representa experiência prática em laboratório e não uma aplicação comercial implantada em ambiente de produção.

---

## 📚 AWS re/Start

O laboratório faz parte da experiência prática desenvolvida durante o programa **AWS re/Start**, complementando estudos e atividades relacionados a:

- Amazon EC2
- Amazon VPC
- Amazon S3
- Amazon EBS
- AWS IAM
- AWS Lambda
- Amazon CloudWatch
- Amazon Route 53
- AWS CloudFormation
- AWS CLI
- redes em cloud
- segurança
- armazenamento
- automação
- troubleshooting
- arquitetura AWS
- alta disponibilidade
- boas práticas de cloud
- Inteligência Artificial Generativa na AWS

---

## 🔐 Segurança

Por segurança, informações sensíveis do ambiente de laboratório não são publicadas neste repositório.

Não são disponibilizados:

- IDs de contas AWS;
- credenciais;
- tokens;
- chaves de acesso;
- sessões temporárias;
- ARNs completos contendo identificadores da conta;
- URLs temporárias do AWS Labs;
- usuários temporários;
- arquivos internos restritos do laboratório.

As evidências utilizadas no portfólio devem ser revisadas ou anonimizadas antes de serem publicadas.

---

## ⚠️ Observação

Este repositório possui finalidade **educacional e de portfólio**.

Ele documenta as atividades e os conhecimentos adquiridos durante um laboratório hands-on da AWS.

Não representa uma implementação comercial ou uma infraestrutura AWS utilizada em produção.

---

## 🚀 Próximos passos

Como evolução dos estudos, alguns pontos que podem ser explorados são:

- desenvolvimento de uma aplicação própria utilizando Amazon Bedrock;
- criação de uma Knowledge Base própria;
- implementação de RAG com dados personalizados;
- desenvolvimento de funções Lambda próprias;
- criação de APIs serverless;
- observabilidade com Amazon CloudWatch;
- autenticação e autorização com IAM;
- infraestrutura como código;
- CI/CD;
- segurança de aplicações de IA;
- monitoramento;
- controle de custos;
- deploy de soluções de IA na AWS.

---

## 🧩 Competências demonstradas

Este laboratório contribui para demonstrar prática em:

**GenAI • RAG • AI Agents • Amazon Bedrock • AgentCore • MCP • AWS Lambda • DynamoDB • S3 • CloudFormation • Serverless • Cloud Computing**

---

## 👨‍💻 Autor

**Rogério Augusto Sabino**

Engenharia de IA & Dados  
GenAI • RAG • LLMs • Python • Machine Learning • AWS • OCI

GitHub: [Rogerio5](https://github.com/Rogerio5)

LinkedIn: [Rogério Augusto Sabino](https://www.linkedin.com/in/rogerio-augusto-sabino/)

---

## ⭐ Sobre este repositório

Este repositório faz parte do meu portfólio de estudos e projetos voltados para **Inteligência Artificial, IA Generativa, Engenharia de Dados, Cloud Computing e Engenharia de Software**.

O objetivo é documentar experiências práticas e demonstrar a evolução na construção e integração de soluções modernas de IA.
