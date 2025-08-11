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

