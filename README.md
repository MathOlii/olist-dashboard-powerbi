# Dashboard de Vendas e Logística: Olist E-commerce

Dashboard interativo em Power BI que analisa vendas, entregas e satisfação de clientes de um marketplace brasileiro.

![Visão geral](images/pagina1-visao-geral.png)

## Contexto

A Olist conecta pequenos comércios a grandes marketplaces no Brasil. O objetivo deste projeto foi entender o desempenho de vendas, o impacto da logística e a satisfação dos clientes, transformando dados brutos de pedidos em um painel que apoia decisões de negócio.

## Perguntas de negócio

- Como a receita evoluiu ao longo do tempo?
- Quais categorias de produtos e quais estados mais vendem?
- Qual o ticket médio e como ele varia?
- Atrasos na entrega afetam a nota dos clientes?

## Dados

- **Fonte:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle, licença CC BY-NC-SA 4.0)
- **Período analisado:** jan/2017 a ago/2018 (fora desse intervalo os dados são escassos ou incompletos)
- **Filtro de status:** apenas pedidos entregues (`delivered`)
- **Observação:** os arquivos CSV não estão neste repositório por causa do tamanho. Baixe-os pelo link acima.

## Ferramentas

- Power BI Desktop
- Power Query (limpeza e transformação)
- DAX (medidas e colunas calculadas)

## Etapas do projeto

1. **Limpeza e transformação** no Power Query: ajuste de tipos, filtro de período e status, agrupamento das avaliações por pedido e tradução das categorias de produto.
2. **Modelagem** em esquema estrela, com a tabela de itens de pedido como fato e tabelas de pedidos, clientes, produtos, vendedores, avaliações e calendário como dimensões.
3. **Criação de medidas em DAX**: receita, pedidos, ticket médio, crescimento mensal, nota média e percentual de entregas no prazo.
4. **Construção do dashboard** em duas páginas: Visão Geral de Vendas e Logística e Satisfação.

As medidas estão documentadas em [docs/medidas_dax.md](docs/medidas_dax.md).

## Principais insights

> Substitua os itens abaixo pelos números reais que você encontrar no seu dashboard.

1. **[PREENCHER]** Evolução da receita: em qual mês houve o pico, de quanto foi e o que pode explicar.
2. **[PREENCHER]** Concentração por categoria: as 3 principais categorias respondem por X% da receita.
3. **[PREENCHER]** Concentração geográfica: o estado líder responde por X% da receita, contra Y% do segundo colocado.
4. **[PREENCHER]** Logística e satisfação: pedidos entregues com atraso têm nota média de X, contra Y dos entregues no prazo.

## Dashboard

### Visão Geral de Vendas

![Visão geral de vendas](images/pagina1-visao-geral.png)

### Logística e Satisfação

![Logística e satisfação](images/pagina2-logistica.png)

## Como abrir o projeto

1. Baixe o arquivo [`dashboard/olist_dashboard.pbix`](dashboard/olist_dashboard.pbix).
2. Abra no [Power BI Desktop](https://powerbi.microsoft.com/desktop/)

## Próximos passos

- Adicionar uma análise por vendedor
- Incluir previsão de vendas
- Explorar a relação entre frete e desistência de compra

## Autor

**Matheus**

- GitHub: https://github.com/MathOlii
- LinkedIn: https://www.linkedin.com/in/matheus-barbosa-a28656179/
