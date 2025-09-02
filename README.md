# ETL Pipeline - Séries Históricas de Preços de Combustíveis (GOV.BR)

## Base de dados

### **Metadados da Série Histórica de Preços de Combustíveis**

**Descrição**
Série Histórica de Preços de Combustíveis, com dados da pesquisa de preços da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), em formato de dados abertos. A ANP, no desempenho de suas atribuições legais, acompanha o comportamento de preços praticados pelas distribuidoras e postos revendedores de combustíveis por meio do Levantamento de Preços de Combustíveis (LPC).

**Fonte de Dados**

- **Órgão**: Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)
- **Formato**: CSVs semestrais (Histórico de preços)
- **Disponibilidade**: [Portal de Dados Abertos do Governo Federal](https://dados.gov.br/dados/conjuntos-dados/serie-historica-de-precos-de-combustiveis-e-de-glp)
- **Documentação**: [Informações sobre Levantamento de Preços de Combustíveis](https://www.gov.br/anp/pt-br/assuntos/precos-e-defesa-da-concorrencia/precos/precos-revenda-e-de-distribuicao-combustiveis/informacoes-levantamento-de-precos-de-combustiveis)

- **Dados utilizados**
Entre os dados disponíveis na base da ANP, este projeto utilizou as séries dos últimos 5 anos, com possibilidade de atualização anual automatizada. Os dados foram restritos aos relatórios semestrais de Combustíveis Automotivos.

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

### **Tecnologias Utilizadas**

| Categoria | Tecnologia | Descrição |
|---|---|---|
| **Linguagem de Programação** | Python | Linguagem principal para desenvolvimento dos pipelines ETL |
| **Framework de Processamento** | Apache Spark | Engine distribuída para processamento de big data em larga escala |
| **Plataforma de Dados** | Databricks | Plataforma unificada de analytics baseada em Apache Spark |
| **Formato de Dados** | Delta Lake | Formato de armazenamento para data lakes com versionamento e ACID |
| **Controle de Versão** | Git | Sistema de controle de versão distribuído para código e notebooks |
| **Repositório** | GitHub | Plataforma de hospedagem e colaboração de código |
| **Notebooks** | Databricks Notebooks | Ambiente interativo para desenvolvimento e documentação |
| **Visualização** | Databricks Dashboards | Dashboards nativos para visualização de dados |
| **IA Conversacional** | Databricks Genie | Interface de consulta em linguagem natural |

#### **Vantagens**

- **Python + Apache Spark**:
Permite o desenvolvimento de pipelines ETL escaláveis e eficientes, aproveitando a simplicidade do Python e o poder de processamento distribuído do Spark. Ideal para manipulação de grandes volumes de dados, transformações complexas e integração com bibliotecas analíticas.

- **Databricks**:
Plataforma colaborativa que integra processamento distribuído, notebooks interativos e gerenciamento de clusters. Facilita o desenvolvimento, execução e monitoramento de fluxos de dados, além de oferecer integração nativa com Spark e Delta Lake.

- **Delta Tables**:
Formato otimizado para data lakes, com suporte a transações ACID, versionamento e auditoria de dados. Garante integridade, rastreabilidade e alta performance em operações de leitura e escrita, essenciais para o tratamento confiável de dados.

- **Databricks Dashboards**:
Permite a criação rápida de visualizações interativas diretamente dos notebooks, facilitando o acompanhamento dos resultados do tratamento de dados e a comunicação com áreas de negócio.

- **Databricks Genie**:
Interface de consulta em linguagem natural que agiliza o acesso e análise dos dados tratados, tornando o processo de exploração e geração de insights mais intuitivo e acessível para usuários não técnicos.

### **Camadas da Arquitetura**

A **Medallion Architecture** é um padrão de design para data lakes que organiza os dados em três camadas progressivas de qualidade e refinamento, garantindo flexibilidade, escalabilidade e governança de dados.

#### **🥉 Bronze Layer - Ingestão Bruta**
**Conceito**: Camada de armazenamento de dados brutos, exatamente como recebidos da fonte, sem qualquer transformação. Atua como um "backup" dos dados originais, preservando a integridade e permitindo reprocessamento quando necessário.

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
**Conceito**: Camada intermediária onde os dados passam por processos de limpeza, validação e padronização. Transforma dados brutos em datasets confiáveis e consistentes, servindo como base para análises e transformações posteriores.

- **Objetivo**: Padronização e limpeza dos dados
- **Transformações**:
  - Conversão de tipos de dados
  - Padronização de nomes de colunas
  - Remoção de registros duplicados
  - Validação de dados
- **Qualidade**: Dados confiáveis e estruturados para análise

#### **🥇 Gold Layer - Enriquecimento e Agregações**
**Conceito**: Camada final que contém dados refinados, agregados e otimizados para consumo específico. Fornece datasets prontos para análises de negócio, relatórios e com alta performance e usabilidade.

- **Objetivo**: Dados otimizados para consumo analítico
- **Agregações**:
  - Preço médio por cidade/estado/semana
  - Índices de variação (% mensal, % anual)
  - Análises temporais e geográficas
- **Preparação**: Tabelas otimizadas para BI e Machine Learning

### **Arquitetura das tabelas**
O projeto utiliza a arquitetura star schema, que organiza os dados em uma estrutura centralizada e otimizada para análise. Neste modelo, as tabelas dimensão fornecem contexto e detalhamento para a tabela fato, facilitando consultas analíticas e agregações.

As tabelas construídas incluem:
- **Dimensão Produtos**: contém os campos `Produto` (tipo de combustível) e `UnidadeMedida` (unidade de comercialização), permitindo detalhar as características dos combustíveis presentes na base.
- **Dimensão Tempo**: composta por `DataColeta` (data da coleta), `dia`, `mes`, `ano`, `semana` e `trimestre`, possibilitando análises temporais em diferentes granularidades.
- **Dimensão Localidade**: inclui `Cep` (código postal), `RegiaoSigla` (região), `EstadoSigla` (UF) e `Municipio`, fornecendo contexto geográfico para os dados de revenda e consumo.
- **Dimensão Revenda**: abrange `CNPJRevenda` (identificador do posto), `Revenda` (nome), `NomeRua`, `NumeroRua`, `Complemento`, `Bandeira` e `cep`, detalhando a localização e características dos postos revendedores.
- **Tabela Fato de Combustíveis**: registra os dados de transações, com as colunas `CNPJRevenda`, `Cep`, `Produto`, `DataColeta`, `ValorVenda` e `ValorCompra`, conectando-se às dimensões por meio de chaves e permitindo análises detalhadas e cruzamentos entre produto, tempo, localidade e revenda.

### **Consumo e Visualização**

#### **Business Intelligence**
- **Dashboard Databricks**: Visualizações interativas e relatórios
- **Databricks Genie**: Interface de consulta em linguagem natural

### **Estrutura do Projeto**

```
Databricks_ETL_Combustivel/
├── 00_Architecture_Builder/     # Configuração do catálogo e esquemas
├── 01_Bronze_Ingestion/        # Ingestão de dados brutos
├── 02_Silver_Treatment/        # Transformação, limpeza, fato e dimensão
├── 03_Gold_Enrichment/         # Agregações e enriquecimento
└── 04_BI/                      # Dashboards e visualizações

```

---

# Como utilizar o repositório no Databricks Free Edition

1. **Crie uma conta gratuita no Databricks**
  - Acesse https://www.databricks.com/learn/free-edition e registre-se na opção Sign up.

2. **Faça login e crie um workspace**
  - Após o login, acesse o workspace padrão da Free Edition.

3. **Importe os notebooks do repositório**
  - No menu lateral, clique em "Workspace" > "Users" > Seu usuário.
  - Clique em "Import" e selecione os arquivos `.ipynb` do repositório para importar os notebooks.


4. **Implemente o pipeline ETL automatizado**
  - Configure o pipeline ETL utilizando o recurso de Jobs do Databricks, conforme o exemplo abaixo:

```yaml
resources:
  jobs:
    ETL_Pipeline:
      name: ETL Pipeline
      email_notifications:
        on_start:
          - seu_email@dominio.com
        on_success:
          - seu_email@dominio.com
        on_failure:
          - seu_email@dominio.com
      schedule:
        quartz_cron_expression: 34 0 5 1 * ?
        timezone_id: America/Sao_Paulo
        pause_status: UNPAUSED
      tasks:
        - task_key: Arch_build
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/00_Architectury_Builder/catalog_build
            source: WORKSPACE
        - task_key: Bronze_Ingestion
          depends_on:
            - task_key: Arch_build
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/01_Bronze_Ingestion/gov_br_data
            source: WORKSPACE
        - task_key: Silver_data_before_2020
          depends_on:
            - task_key: Bronze_Ingestion
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/01_tables_before_2020
            source: WORKSPACE
        - task_key: Join_full_Bronze_Tables
          depends_on:
            - task_key: Silver_data_before_2020
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/02_enrichment_fuel_data
            source: WORKSPACE
        - task_key: Build_Dim_Localidade
          depends_on:
            - task_key: Join_full_Bronze_Tables
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/05_dim_localidade
            source: WORKSPACE
        - task_key: Build_Dim_Product
          depends_on:
            - task_key: Join_full_Bronze_Tables
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/03_dim_produtos
            source: WORKSPACE
        - task_key: Build_Dim_Revenda
          depends_on:
            - task_key: Join_full_Bronze_Tables
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/06_dim_revenda
            source: WORKSPACE
        - task_key: Build_Dim_tempo
          depends_on:
            - task_key: Join_full_Bronze_Tables
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/04_dim_tempo
            source: WORKSPACE
        - task_key: Set_Pk_Dim_Tables
          depends_on:
            - task_key: Build_Dim_Localidade
            - task_key: Build_Dim_Product
            - task_key: Build_Dim_Revenda
            - task_key: Build_Dim_tempo
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/07_ajuste_pks
            source: WORKSPACE
        - task_key: Build_Fact_Table
          depends_on:
            - task_key: Set_Pk_Dim_Tables
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/02_Silver_Treatment/08_fact_fuel
            source: WORKSPACE
        - task_key: ComparacoesGeograficas
          depends_on:
            - task_key: Build_Fact_Table
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/03_Gold_Enrichment/03_comparacoes_geograficas
            source: WORKSPACE
        - task_key: IndicadoresTemporais
          depends_on:
            - task_key: Build_Fact_Table
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/03_Gold_Enrichment/02_indicadores_temporais
            source: WORKSPACE
        - task_key: infoProdutos
          depends_on:
            - task_key: Build_Fact_Table
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/03_Gold_Enrichment/01_info_preco_produto
            source: WORKSPACE
        - task_key: InfoBandeira
          depends_on:
            - task_key: Build_Fact_Table
          notebook_task:
            notebook_path: /Workspace/Users/SEU_USUARIO/Databricks_ETL_Combustivel/03_Gold_Enrichment/04_Bandeira
            source: WORKSPACE
      queue:
        enabled: true
      performance_target: STANDARD
```

  > **Atenção:**
  > - Substitua `seu_email@dominio.com` pelo(s) e-mail(s) que devem receber notificações do job.
  > - Altere `SEU_USUARIO` para o nome do seu usuário Databricks.
  > - Ajuste os caminhos dos notebooks conforme a estrutura do seu workspace.
  > - Complete outros campos conforme a necessidade do seu ambiente.

  O exemplo acima mostra como orquestrar a execução dos notebooks do projeto em etapas dependentes, com notificações e agendamento automático. Basta adaptar os caminhos dos notebooks e configurar o job no Databricks para automatizar todo o pipeline ETL.


## **Configurando job runs pela interface**

Também é possível configurar a pipeline ETL diretamente pela interface gráfica do Databricks. Siga os passos abaixo:

1. No menu lateral, acesse **Jobs Runs**.
2. Clique em **Create Job** para iniciar a configuração de um novo job.
3. Para cada etapa da pipeline, adicione uma tarefa (**Add Task**) e selecione o notebook correspondente.
4. **Atenção à ordem dos notebooks:**
  - Os notebooks e pastas do projeto estão nomeados sequencialmente (00, 01, 02, ...).
  - Siga essa ordem ao adicionar as tarefas no job, garantindo que cada etapa dependa da anterior.
  - Por exemplo, configure o notebook de ingestão (01_Bronze_Ingestion) para ser executado após o de arquitetura (00_Architectury_Builder), e assim por diante.
5. Para definir dependências entre tarefas, utilize a opção **Depends on** ao adicionar cada notebook.
6. Configure notificações, agendamento e outros parâmetros conforme sua necessidade.

> **Importante:**
> - A sequência dos notebooks reflete a ordem lógica de processamento dos dados. Seguir essa ordem é fundamental para garantir que arquivos que dependem de outros sejam executados corretamente.
> - Caso altere nomes ou a estrutura das pastas, ajuste a configuração do job para refletir essas mudanças.

Ao finalizar, salve e execute o job para automatizar o pipeline ETL conforme a arquitetura do projeto.

6. **Visualize os resultados**
  - Utilize os dashboards e queries criados para explorar os dados tratados.

**Observações:**
- A free edition possui limitações de recursos e armazenamento, mas permite testar todo o pipeline ETL e visualizar os resultados.
- Caso utilize outro ambiente Databricks, o processo de importação e execução é similar, podendo aproveitar recursos adicionais.



# Como utilizar o repositório no Azure Databricks

Para utilizar este repositório no Azure Databricks, é necessário configurar um armazenamento externo para os dados e arquivos do pipeline. Recomenda-se a criação de um **Azure Blob Storage** para servir como base do DBFS (Databricks File System), permitindo o armazenamento e acesso eficiente aos dados.

**Passos principais:**

1. Crie uma conta de armazenamento do tipo Blob no portal do Azure.
2. Crie um container para armazenar os arquivos de dados e resultados do pipeline.
3. No Azure Databricks, monte o Blob Storage como DBFS utilizando as credenciais de acesso (SAS Token ou chave de acesso).
4. Importe os notebooks do repositório normalmente e ajuste os caminhos de leitura/escrita para utilizar o DBFS montado.

> **Atenção:**
> - O uso do DBFS via Blob Storage é essencial para garantir persistência, escalabilidade e integração nativa com os recursos do Azure Databricks.
> - Certifique-se de que as permissões de acesso ao Blob Storage estejam corretamente configuradas para leitura e escrita.
> - Adapte os notebooks e jobs para utilizar os caminhos do DBFS conforme o ambiente configurado.


Com essa configuração, o pipeline ETL poderá ser executado de forma automatizada e segura no Azure Databricks, aproveitando todos os recursos de armazenamento e processamento distribuído da plataforma.

---

## Diferenças entre Databricks Free Edition e Azure Databricks

| Recurso/Característica         | Free Edition Databricks           | Azure Databricks                       |
|-------------------------------|-----------------------------------|----------------------------------------|
| **Armazenamento**             | Limitado ao DBFS local, sem Blob  | Integração nativa com Azure Blob, ADLS |
| **Escalabilidade**            | Recursos computacionais restritos  | Clusters escaláveis sob demanda        |
| **Segurança**                 | Básica, sem integração corporativa | Integração com Azure AD, RBAC, redes   |
| **Integração**                | Sem integração com outros serviços | Integração total com Azure (Data Lake, Synapse, Key Vault, etc.) |
| **Persistência de Dados**     | Dados podem ser apagados           | Persistência garantida em Blob/ADLS    |
| **Agendamento de Jobs**       | Limitado, sem triggers avançadas   | Agendamento flexível e triggers        |
| **Limite de Usuários**        | Apenas 1 usuário                   | Multiusuário, colaboração corporativa  |
| **Suporte e SLA**             | Sem suporte oficial                | Suporte Microsoft, SLA corporativo     |
| **Recursos Avançados**        | Não disponível                     | MLflow, Delta Sharing, Unity Catalog   |

> **Resumo:**
> - O Free Edition é ideal para testes, prototipagem e aprendizado, mas possui limitações de recursos, armazenamento e integração.
> - O Azure Databricks é recomendado para ambientes produtivos, com escalabilidade, segurança, integração corporativa e persistência de dados garantida.


