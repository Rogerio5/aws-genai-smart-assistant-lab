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

## 🏗️ Arquitetura da solução

A arquitetura combina **IA Generativa, recuperação de conhecimento e execução de ações**, permitindo que o assistente não apenas responda perguntas, mas também interaja com outros serviços.

```mermaid
flowchart LR

    USER["👤 Usuário"]
    WEB["💬 Web Application<br/>HR Assistant"]

    AGENT["🤖 Amazon Bedrock<br/>AgentCore"]

    KB["🧠 Amazon Bedrock<br/>Knowledge Base"]
    S3KB[("🪣 Amazon S3<br/>Knowledge Base")]

    GATEWAY["🔌 Amazon Bedrock<br/>AgentCore Gateway"]
    MCP["🔗 MCP<br/>Model Context Protocol"]

    LAMBDA["⚡ AWS Lambda<br/>submit_benefits"]

    DB[("🗄️ Amazon DynamoDB<br/>BenefitsTable")]

    USER --> WEB
    WEB --> AGENT

    AGENT -->|"Recuperação de conhecimento"| KB
    KB -->|"Acessa documentos"| S3KB

    AGENT -->|"Executa ferramenta"| GATEWAY
    GATEWAY --> MCP
    MCP --> LAMBDA

    LAMBDA -->|"Grava solicitação"| DB

    classDef user fill:#1565C0,stroke:#0D47A1,color:#ffffff,stroke-width:2px
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff,stroke-width:2px
    classDef knowledge fill:#00875A,stroke:#006644,color:#ffffff,stroke-width:2px
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff,stroke-width:2px
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111,stroke-width:2px
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff,stroke-width:2px

    class USER,WEB user
    class AGENT ai
    class KB,S3KB knowledge
    class GATEWAY,MCP integration
    class LAMBDA compute
    class DB database
```

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

## 🧠 IA Generativa e agentes de IA

A arquitetura demonstra que o assistente não atua apenas como chatbot. O agente pode recuperar conhecimento e também executar ações externas.

```mermaid
flowchart TB

    REQUEST["💬 Solicitação do usuário"]

    AGENT["🤖 Agente de IA<br/>Amazon Bedrock AgentCore"]

    DECISION{"O que o agente<br/>precisa fazer?"}

    RAG["📚 Recuperar conhecimento"]
    TOOL["🛠️ Executar ferramenta"]

    KB["🧠 Knowledge Base<br/>RAG"]
    MCP["🔗 MCP Gateway"]

    ANSWER["💡 Gerar resposta"]
    ACTION["⚙️ Executar ação"]

    REQUEST --> AGENT
    AGENT --> DECISION

    DECISION -->|"Consultar informação"| RAG
    DECISION -->|"Executar tarefa"| TOOL

    RAG --> KB
    KB --> ANSWER

    TOOL --> MCP
    MCP --> ACTION

    ANSWER --> RESULT["✅ Resposta ao usuário"]
    ACTION --> RESULT

    classDef input fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef rag fill:#00875A,stroke:#006644,color:#ffffff
    classDef tool fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef result fill:#455A64,stroke:#263238,color:#ffffff

    class REQUEST input
    class AGENT,DECISION ai
    class RAG,KB rag
    class TOOL,MCP,ACTION tool
    class ANSWER,RESULT result
```

Essa arquitetura permite que o modelo de linguagem seja integrado a recursos externos em vez de funcionar apenas como um chatbot isolado.

---


## 🔎 Knowledge Base e RAG

O Amazon Bedrock Knowledge Base permite recuperar informações armazenadas no Amazon S3 para fornecer contexto ao agente.

```mermaid
flowchart LR

    QUESTION["❓ Pergunta do usuário"]

    AGENT["🤖 Amazon Bedrock<br/>AgentCore"]

    SEARCH["🔎 Consulta à<br/>Knowledge Base"]

    KB["🧠 Amazon Bedrock<br/>Knowledge Base"]

    S3[("🪣 Amazon S3<br/>Documentos")]

    CONTEXT["📄 Contexto relevante"]

    RESPONSE["💬 Resposta baseada<br/>nos documentos"]

    QUESTION --> AGENT
    AGENT --> SEARCH
    SEARCH --> KB

    KB -->|"Consulta fonte"| S3
    S3 -->|"Documentos relevantes"| KB

    KB --> CONTEXT
    CONTEXT --> AGENT
    AGENT --> RESPONSE

    classDef user fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef rag fill:#00875A,stroke:#006644,color:#ffffff
    classDef output fill:#455A64,stroke:#263238,color:#ffffff

    class QUESTION user
    class AGENT ai
    class SEARCH,KB,S3,CONTEXT rag
    class RESPONSE output
```


Esse padrão é conhecido como **Retrieval-Augmented Generation (RAG)**.

O RAG permite combinar modelos de linguagem com informações externas ou corporativas, aumentando a capacidade do assistente de responder utilizando um contexto específico.

---

## 🔌 Integração com MCP

Durante o laboratório, foi configurado um destino chamado `submitBenefits` no AgentCore Gateway.

```mermaid
flowchart LR

    AGENT["🤖 Amazon Bedrock<br/>AgentCore"]

    GATEWAY["🔌 AgentCore Gateway"]

    TARGET["🎯 Destino<br/>submitBenefits"]

    MCP["🔗 MCP"]

    LAMBDA["⚡ AWS Lambda<br/>submit_benefits"]

    DB[("🗄️ DynamoDB<br/>BenefitsTable")]

    AGENT -->|"Solicita execução"| GATEWAY
    GATEWAY --> TARGET
    TARGET --> MCP
    MCP --> LAMBDA
    LAMBDA -->|"Persistência"| DB

    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff

    class AGENT ai
    class GATEWAY,TARGET,MCP integration
    class LAMBDA compute
    class DB database
```

utilizando o **Model Context Protocol (MCP)**.

O MCP permite disponibilizar ferramentas e recursos externos para agentes de IA através de uma interface padronizada.

---

## 📄 Schema da ferramenta

O AgentCore Gateway utiliza um schema armazenado no Amazon S3 para compreender a estrutura da ferramenta disponível ao agente.

```mermaid
flowchart LR

    S3[("🪣 Amazon S3")]

    SCHEMA["📄 submit_benefits.json"]

    GATEWAY["🔌 AgentCore Gateway"]

    MCP["🔗 MCP"]

    LAMBDA["⚡ AWS Lambda<br/>submit_benefits"]

    S3 --> SCHEMA
    SCHEMA -->|"Define ferramenta"| GATEWAY
    GATEWAY --> MCP
    MCP --> LAMBDA

    classDef storage fill:#00875A,stroke:#006644,color:#ffffff
    classDef schema fill:#0277BD,stroke:#01579B,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111

    class S3 storage
    class SCHEMA schema
    class GATEWAY,MCP integration
    class LAMBDA compute
```

---

## ⚡ Execução da AWS Lambda

A função `submit_benefits` processa a solicitação recebida pelo agente e grava os dados no DynamoDB.

```mermaid
flowchart LR

    REQUEST["📨 Solicitação de benefício"]

    AGENT["🤖 AgentCore"]

    MCP["🔗 MCP Gateway"]

    LAMBDA["⚡ AWS Lambda<br/>submit_benefits"]

    PROCESS["⚙️ Processamento<br/>da solicitação"]

    DB[("🗄️ DynamoDB<br/>BenefitsTable")]

    CONFIRM["✅ Confirmação<br/>ao assistente"]

    REQUEST --> AGENT
    AGENT --> MCP
    MCP --> LAMBDA
    LAMBDA --> PROCESS
    PROCESS --> DB
    DB --> CONFIRM

    classDef input fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff
    classDef result fill:#2E7D32,stroke:#1B5E20,color:#ffffff

    class REQUEST input
    class AGENT ai
    class MCP integration
    class LAMBDA,PROCESS compute
    class DB database
    class CONFIRM result
```

Esse processo demonstra como agentes de IA podem utilizar funções serverless para executar ações dentro de uma aplicação.

---

## 🗄️ Persistência no DynamoDB

O resultado da execução da função Lambda foi registrado na tabela `BenefitsTable`.

```mermaid
flowchart TB

    LAMBDA["⚡ AWS Lambda<br/>submit_benefits"]

    DB[("🗄️ Amazon DynamoDB<br/>BenefitsTable")]

    RECORD["📋 Registro criado"]

    NAME["employee_name<br/>Jane Doe"]
    TYPE["benefit_type<br/>medical"]
    VALUE["claim_amount<br/>250"]

    LAMBDA -->|"PutItem"| DB
    DB --> RECORD

    RECORD --> NAME
    RECORD --> TYPE
    RECORD --> VALUE

    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff
    classDef data fill:#1565C0,stroke:#0D47A1,color:#ffffff

    class LAMBDA compute
    class DB database
    class RECORD,NAME,TYPE,VALUE data
```

A presença desse registro confirmou que a chamada realizada pelo assistente percorreu corretamente a arquitetura até a camada de persistência.

---

## 💬 Validação pelo assistente

O fluxo foi testado através da aplicação de chat fornecida no laboratório.

```mermaid
sequenceDiagram

    participant U as 👤 Usuário
    participant W as 💬 Web App
    participant A as 🤖 AgentCore
    participant G as 🔌 MCP Gateway
    participant L as ⚡ Lambda
    participant D as 🗄️ DynamoDB

    U->>W: Solicitação de benefício
    W->>A: Envia mensagem
    A->>G: Solicita execução da ferramenta
    G->>L: Invoke submit_benefits
    L->>D: Registra benefício
    D-->>L: Confirma gravação
    L-->>G: Resultado
    G-->>A: Resultado da ferramenta
    A-->>W: Confirma solicitação
    W-->>U: Solicitação enviada com sucesso
```

O assistente confirmou o processamento da solicitação e o registro correspondente foi posteriormente verificado no DynamoDB.

---

## 🔄 Fluxo end-to-end

A execução completa do laboratório pode ser representada da seguinte maneira:

```mermaid
flowchart TB

    STEP1["1️⃣ Usuário envia solicitação"]

    STEP2["2️⃣ Web Application envia mensagem"]

    STEP3["3️⃣ AgentCore interpreta a solicitação"]

    STEP4{"4️⃣ Precisa consultar<br/>ou executar?"}

    RAG["5️⃣ Knowledge Base / RAG"]
    TOOL["5️⃣ AgentCore Gateway / MCP"]

    CONTEXT["6️⃣ Recuperação de contexto"]
    LAMBDA["6️⃣ AWS Lambda"]

    DB["7️⃣ Amazon DynamoDB"]

    RESULT["8️⃣ Resultado retorna ao agente"]

    RESPONSE["9️⃣ Resposta ao usuário"]

    STEP1 --> STEP2
    STEP2 --> STEP3
    STEP3 --> STEP4

    STEP4 -->|"Conhecimento"| RAG
    STEP4 -->|"Ação"| TOOL

    RAG --> CONTEXT
    CONTEXT --> RESULT

    TOOL --> LAMBDA
    LAMBDA --> DB
    DB --> RESULT

    RESULT --> RESPONSE

    classDef user fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef rag fill:#00875A,stroke:#006644,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff
    classDef output fill:#2E7D32,stroke:#1B5E20,color:#ffffff

    class STEP1,STEP2 user
    class STEP3,STEP4 ai
    class RAG,CONTEXT rag
    class TOOL integration
    class LAMBDA compute
    class DB database
    class RESULT,RESPONSE output
```

---

## ☁️ Infraestrutura do laboratório

Os recursos utilizados no laboratório foram provisionados através da infraestrutura preparada para o AWS SimuLearn.

```mermaid
flowchart TB

    CF["☁️ AWS CloudFormation"]

    CF --> AGENT["🤖 Amazon Bedrock<br/>AgentCore"]

    CF --> GATEWAY["🔌 AgentCore Gateway"]

    CF --> LAMBDA["⚡ AWS Lambda"]

    CF --> DYNAMO[("🗄️ Amazon DynamoDB")]

    CF --> S3[("🪣 Amazon S3")]

    CF --> KB["🧠 Bedrock<br/>Knowledge Base"]

    CF --> IAM["🔐 AWS IAM"]

    classDef infra fill:#263238,stroke:#000000,color:#ffffff,stroke-width:2px
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff
    classDef storage fill:#00875A,stroke:#006644,color:#ffffff
    classDef security fill:#455A64,stroke:#263238,color:#ffffff

    class CF infra
    class AGENT,KB ai
    class GATEWAY integration
    class LAMBDA compute
    class DYNAMO database
    class S3 storage
    class IAM security
```


---

## ✅ Resultado final

O laboratório foi validado com sucesso.

```mermaid
flowchart LR

    CHAT["💬 Chat"]
    AGENT["🤖 Amazon Bedrock<br/>AgentCore"]
    MCP["🔌 Gateway / MCP"]
    LAMBDA["⚡ AWS Lambda"]
    DB[("🗄️ DynamoDB")]
    SUCCESS["✅ Validação concluída"]

    CHAT --> AGENT
    AGENT --> MCP
    MCP --> LAMBDA
    LAMBDA --> DB
    DB --> SUCCESS

    classDef user fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef ai fill:#6A1B9A,stroke:#4A148C,color:#ffffff
    classDef integration fill:#E65100,stroke:#BF360C,color:#ffffff
    classDef compute fill:#F9A825,stroke:#F57F17,color:#111111
    classDef database fill:#C2185B,stroke:#880E4F,color:#ffffff
    classDef success fill:#2E7D32,stroke:#1B5E20,color:#ffffff

    class CHAT user
    class AGENT ai
    class MCP integration
    class LAMBDA compute
    class DB database
    class SUCCESS success
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
