# Medidas DAX

Documentação das tabelas calculadas, colunas calculadas e medidas usadas no dashboard Olist.

**Convenções:** medidas ficam na tabela `order_items`; a coluna calculada fica em `orders`; a tabela calendário se chama `dCalendario`.

---

## Tabela calculada

### dCalendario

Tabela de datas contínua, necessária para cálculos de inteligência de tempo (como comparação com o mês anterior). Cobre o período analisado e deve ser marcada como tabela de datas, com a coluna `Date`. A coluna `Mês` é ordenada pela coluna `Mês Nº`.

```dax
dCalendario =
ADDCOLUMNS(
    CALENDAR(DATE(2017,1,1), DATE(2018,8,31)),
    "Ano", YEAR([Date]),
    "Mês Nº", MONTH([Date]),
    "Mês", FORMAT([Date], "MMM/yy")
)
```

---

## Coluna calculada

### Entregue no Prazo (tabela `orders`)

Para cada pedido, retorna `1` se foi entregue até a data estimada, `0` se atrasou e vazio quando não há data de entrega registrada.

```dax
Entregue no Prazo =
IF(
    ISBLANK(orders[order_delivered_customer_date]), BLANK(),
    IF(
        orders[order_delivered_customer_date] <= orders[order_estimated_delivery_date],
        1, 0
    )
)
```

---

## Medidas

### Receita

Soma do preço dos itens vendidos, respeitando os filtros aplicados na tela (período, estado, categoria etc.). Não inclui frete.

```dax
Receita = SUM(order_items[price])
```

### Frete Total

Soma do valor de frete cobrado nos itens vendidos.

```dax
Frete Total = SUM(order_items[freight_value])
```

### Pedidos

Quantidade de pedidos únicos. Usa `DISTINCTCOUNT` porque um mesmo pedido pode ter vários itens.

```dax
Pedidos = DISTINCTCOUNT(order_items[order_id])
```

### Ticket Médio

Receita média por pedido. O `DIVIDE` evita erro de divisão por zero.

```dax
Ticket Médio = DIVIDE([Receita], [Pedidos])
```

### Receita Mês Anterior

Receita do mês imediatamente anterior ao mês filtrado. O `CALCULATE` altera o contexto de filtro, deslocando o período em um mês para trás.

```dax
Receita Mês Anterior =
CALCULATE([Receita], DATEADD(dCalendario[Date], -1, MONTH))
```

### Crescimento MoM

Variação percentual da receita em relação ao mês anterior (*month over month*).

```dax
Crescimento MoM =
DIVIDE([Receita] - [Receita Mês Anterior], [Receita Mês Anterior])
```

### Nota Média

Média das notas de avaliação. Cada pedido já tem uma única nota (a média das avaliações dele), calculada no Power Query.

```dax
Nota Média = AVERAGE(reviews[nota_media])
```

### % Entregas no Prazo

Percentual de pedidos entregues até a data estimada. Pedidos sem data de entrega são ignorados no cálculo.

```dax
% Entregas no Prazo = AVERAGE(orders[Entregue no Prazo])
```

---

## Formatação sugerida

| Medida | Formato |
|---|---|
| Receita, Frete Total, Ticket Médio | Moeda (R$) |
| Pedidos | Número inteiro |
| Crescimento MoM, % Entregas no Prazo | Porcentagem |
| Nota Média | Número decimal (1 casa) |
