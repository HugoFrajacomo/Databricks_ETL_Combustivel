# ETL Pipeline - Séries Históricas de Preços de Combustíveis (GOV.BR)

## Base de dados

### **Metadados da Série Histórica de Preços de Combustíveis**

**Descrição**
[cite_start]Série Histórica de Preços de Combustíveis, com dados da pesquisa de preços da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), em formato de dados abertos[cite: 1]. [cite_start]A ANP, no desempenho de suas atribuições legais, acompanha o comportamento de preços praticados pelas distribuidoras e postos revendedores de combustíveis por meio do Levantamento de Preços de Combustíveis (LPC)[cite: 1].

**Órgão Responsável**
[cite_start]Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)[cite: 1].

---

### **Campos da Tabela**

| Campo | Descrição do Atributo | Tipo | Fonte dos Dados |
|---|---|---|---|
| **Região - Sigla** | Sigla da Região onde a revenda pesquisada se encontra | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Estado - Sigla** | Sigla da Unidade Federativa (UF) da revenda pesquisada | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Município** | Nome do município da revenda pesquisada | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Revenda** | Nome do Cadastro Nacional de Pessoa Jurídica da revenda | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |
| **CNPJ da Revenda**| Nome do logradouro da revenda pesquisada | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |
| **Nome da Rua** | Número do logradouro da revenda pesquisada | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |
| **Numero Rua** | Complemento do logradouro da revenda | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |
| **Complemento** | Nome do bairro da revenda pesquisada | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |
| **Bairro** | Número do Código de Endereçamento Postal (CEP) do logradouro | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Cep** | Nome do combustível | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Produto** | Data da coleta do preço | Data | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Valor de Venda**| Preço de venda ao consumidor final | Numérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Valor de Compra** | Preço de distribuição (preço de venda da distribuidora para o posto revendedor) | Numérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Unidade de Medida** | Unidade de Medida | Alfanumérico | [cite_start]Levantamento de Preços de Combustíveis (LPC) [cite: 4] |
| **Bandeira** | Nome da bandeira da revenda. Posto que opta por exibir a marca comercial de uma distribuidora, deverá vender somente combustíveis fornecidos pela distribuidora detentora da marca. Posto bandeira branca é aquele que opta por não exibir marca comercial. | Alfanumérico | [cite_start]Sistema de Movimentação de Produtos (SIMP) [cite: 4] |

---

