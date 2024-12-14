# Estrutura do Projeto

Abaixo está a estrutura do projeto para a implementação do fluxo de ingestão e validação de XML.

```bash
project-root/
│
├── src/
│   ├── parsers/
│   │   └── xmlParser.js         # Parsing do XML e validação XSD
│   ├── validators/
│   │   ├── xmlSyntaxValidator.js # Validação de sintaxe XML
│   │   ├── xsdValidator.js      # Validação contra XSD
│   │   └── securityValidator.js # Prevenção contra XXE e conteúdo malicioso
│   ├── utils/
│   │   ├── logger.js            # Log/Auditoria no S3
│   │   └── contentChecker.js    # Checagem de padrões perigosos
│   ├── services/
│   │   └── persistData.js       # Persistência no banco de dados
│   └── index.js                 # Orquestração do fluxo
│
├── tests/                       # Testes unitários
├── schemas/
│   └── news.xsd                 # Esquema XSD para validação do XML
├── data/
│   └── sample-news.xml          # Exemplo de XML para teste
├── .env                         # Configurações (chaves AWS, etc.)
└── package.json                 # Dependências do projeto
```

## **Descrição das Pastas e Arquivos**

- **src/**
  - **parsers/**:
    - `xmlParser.js`: Faz o parsing do XML usando a biblioteca `fast-xml-parser`.
  - **validators/**:
    - `xmlSyntaxValidator.js`: Valida a sintaxe do XML.
    - `xsdValidator.js`: Valida o XML contra um esquema XSD.
    - `securityValidator.js`: Previne ataques XXE e verifica a presença de conteúdo malicioso.
  - **utils/**:
    - `logger.js`: Responsável por enviar logs para o S3.
    - `contentChecker.js`: Checagem de padrões perigosos, como scripts ou comandos SQL maliciosos.
  - **services/**:
    - `persistData.js`: Salva os dados processados no banco (DynamoDB/RDS).
  - **index.js**: Arquivo principal que orquestra todas as etapas do processamento XML.

- **tests/**:
  - Pasta reservada para testes unitários e de integração.

- **schemas/**:
  - `news.xsd`: Esquema XSD usado para validar os arquivos XML.

- **data/**:
  - `sample-news.xml`: Exemplo de XML usado como entrada no processo.

- **.env**:
  - Contém configurações sensíveis, como credenciais AWS.

- **package.json**:
  - Gerencia as dependências do projeto Node.js.

---

## **Executando o Projeto**

1. **Instale as dependências**:

   ```bash
   npm install
   ```

2. **Configure o arquivo `.env`** com suas credenciais AWS:

   ```plaintext
   AWS_REGION=us-east-1
   S3_BUCKET_NAME=your-s3-bucket-name
   DYNAMODB_TABLE_NAME=your-dynamodb-table-name
   ```

3. **Execute o fluxo de processamento**:

   ```bash
   node src/index.js
   ```

4. **Logs**:
   - Logs de validação e processamento serão enviados para o S3 configurado.

---

## **Tecnologias Utilizadas**

- **Node.js**
- **fast-xml-parser**
- **libxmljs2**
- **AWS SDK v3** (para S3 e DynamoDB)

---

### **Objetivo da Funcionalidade**

Integrar o fluxo de ingestão de dados provenientes de consultas ao site de notícias externo (via HTTP GET). O XML recebido passará por validações de sintaxe, XSD, segurança e conformidade antes de ser salvo no banco de dados.
