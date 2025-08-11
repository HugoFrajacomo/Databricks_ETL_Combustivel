# ETL Pipeline - Séries Históricas de Preços de Combustíveis (GOV.BR)

## Base de dados

### **Metadados da Série Histórica de Preços de Combustíveis**

**Descrição**
Série Histórica de Preços de Combustíveis, com dados da pesquisa de preços da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), em formato de dados abertos[cite: 1]. A ANP, no desempenho de suas atribuições legais, acompanha o comportamento de preços praticados pelas distribuidoras e postos revendedores de combustíveis por meio do Levantamento de Preços de Combustíveis (LPC).

**Órgão Responsável**
Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)

---

### **Campos da Tabela**

| Campo | Descrição do Atributo | Tipo | Fonte dos Dados |
|---|---|---|---|
| **Região - Sigla** | Sigla da Região onde a revenda pesquisada se encontra | Alfanumérico | Levantamento de Preços de Combustíveis (LPC) |
| **Estado - Sigla** | Sigla da Unidade Federativa (UF) da revenda pesquisada | Alfanumérico | Levantamento de Preços de Combustíveis (LPC) |
| **Município** | Nome do município da revenda pesquisada | Alfanumérico | Levantamento de Preços de Combustíveis (LPC) |
| **Revenda** | Nome do Cadastro Nacional de Pessoa Jurídica da revenda | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |
| **CNPJ da Revenda**| Nome do logradouro da revenda pesquisada | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |
| **Nome da Rua** | Número do logradouro da revenda pesquisada | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |
| **Numero Rua** | Complemento do logradouro da revenda | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |
| **Complemento** | Nome do bairro da revenda pesquisada | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |
| **Bairro** | Número do Código de Endereçamento Postal (CEP) do logradouro | Alfanumérico | Levantamento de Preços de Combustíveis (LPC) |
| **Cep** | Nome do combustível | Alfanumérico | Levantamento de Preços de Combustíveis (LPC) |
| **Produto** | Data da coleta do preço | Data | Levantamento de Preços de Combustíveis (LPC) |
| **Valor de Venda**| Preço de venda ao consumidor final | Numérico | Levantamento de Preços de Combustíveis (LPC) |
| **Valor de Compra** | Preço de distribuição (preço de venda da distribuidora para o posto revendedor) | Numérico | Levantamento de Preços de Combustíveis (LPC) |
| **Unidade de Medida** | Unidade de Medida | Alfanumérico | Levantamento de Preços de Combustíveis (LPC)  |
| **Bandeira** | Nome da bandeira da revenda. Posto que opta por exibir a marca comercial de uma distribuidora, deverá vender somente combustíveis fornecidos pela distribuidora detentora da marca. Posto bandeira branca é aquele que opta por não exibir marca comercial. | Alfanumérico | Sistema de Movimentação de Produtos (SIMP) |

---

## Arquitetura do Projeto

### **Visão Geral**

Este projeto implementa um pipeline ETL seguindo a **Medallion Architecture** para processamento e análise de dados históricos de preços de combustíveis. A arquitetura é composta por três camadas principais: Bronze (dados brutos), Silver (dados limpos e transformados) e Gold (dados agregados e enriquecidos).

### **Fonte de Dados**

- **Órgão**: Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)
- **Formato**: CSVs semestrais (Histórico de preços)
- **Disponibilidade**: [Portal de Dados Abertos do Governo Federal](https://dados.gov.br/dados/conjuntos-dados/serie-historica-de-precos-de-combustiveis-e-de-glp)
- **Documentação**: [Informações sobre Levantamento de Preços de Combustíveis](https://www.gov.br/anp/pt-br/assuntos/precos-e-defesa-da-concorrencia/precos/precos-revenda-e-de-distribuicao-combustiveis/informacoes-levantamento-de-precos-de-combustiveis)

### **Camadas da Arquitetura**

#### **🥉 Bronze Layer - Ingestão Bruta**
- **Objetivo**: Armazenamento de dados brutos sem transformações
- **Implementação**: 
  - Job Databricks para download automático de arquivos CSV
  - Armazenamento no Databricks Catalog
  - Formato: Delta Tables
- **Características**:
  - Preservação dos dados originais
  - Versionamento de dados
  - Auditoria completa

#### **🥈 Silver Layer - Transformação e Limpeza**
- **Objetivo**: Padronização e limpeza dos dados
- **Transformações**:
  - Conversão de tipos de dados
  - Padronização de nomes de colunas
  - Remoção de registros duplicados
  - Validação de dados
- **Qualidade**: Dados confiáveis e estruturados para análise

#### **🥇 Gold Layer - Enriquecimento e Agregações**
- **Objetivo**: Dados otimizados para consumo analítico
- **Agregações**:
  - Preço médio por cidade/estado/semana
  - Índices de variação (% mensal, % anual)
  - Análises temporais e geográficas
- **Preparação**: Tabelas otimizadas para BI e Machine Learning

### **Consumo e Visualização**

#### **Business Intelligence**
- **Dashboard Databricks**: Visualizações interativas e relatórios
- **Databricks Genie**: Interface de consulta em linguagem natural

#### **Machine Learning**
- Dados preparados para modelos preditivos
- Análise de tendências e padrões de preços
- Forecasting de preços de combustíveis

### **Estrutura do Projeto**

```
Databricks_ETL_Combustivel/
├── 00_Architecture_Builder/     # Configuração do catálogo e esquemas
├── 01_Bronze_Ingestion/        # Ingestão de dados brutos
├── 02_Silver_Treatment/        # Transformação e limpeza
├── 03_Gold_Enrichment/         # Agregações e enriquecimento
├── 04_BI/                      # Dashboards e visualizações
└── 05_Machine_Learn/           # Modelos de Machine Learning
```

---

