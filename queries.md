# Perguntas sobre vendas:

## 1. Quais são os TOP 3 produtos mais vendidos nos últimos 3 meses?
Essa query identifica os três produtos mais vendidos nos últimos três meses:

```sql
SELECT 
	Produto, 
    COUNT(*) AS Qtd_Vendida
FROM 
	vendas
WHERE 
	Data_Venda BETWEEN '05/04/2022' AND '05/07/2022'
GROUP BY 
	Produto
ORDER BY 
	Qtd_Vendida DESC
LIMIT 3;
```

Resultado da Query:

```markdown
| Produto                                   | Qtd_Vendida |
|------------------------------------------|--------------|
| Hand Games men M30 Amarelo              | 59           |
| Hand Games for kids E300 Amarelo        | 51           |
| Simulador de Vôo de Combate 2 M400    | 31           |
```

---

## 2. Qual a categoria mais vendida por continente?
Essa query retorna a categoria de produto mais vendida em cada continente:

```sql
SELECT 
Continente, 
Categoria,
COUNT(*) AS Qtd_Vendida
FROM
	vendas
GROUP BY 
	Continente, Categoria
ORDER BY 
	Qtd_Vendida DESC;
```

Resultado da Query:

```markdown
| Continente         | Categoria        | Qtd_Vendida |
|--------------------|-----------------|--------------|
| América do Norte  | Ventiladores     | 27082        |
| Europa            | Sistema de Som   | 13253        |
| América do Sul   | Ventiladores     | 6724         |
| Ásia             | Games            | 2750         |
| África           | Sistema de Som   | 1736         |
```

---

## 3. Qual o faturamento mensal total?
Essa query calcula o faturamento total por mês:

```sql
SELECT 
DATE_FORMAT(STR_TO_DATE(data_venda, '%d/%m/%Y'), '%Y-%m') AS Mes_Ano, 
       SUM(Faturamento) AS Faturamento_Total
FROM 
	vendas
GROUP BY 
	Mes_Ano
ORDER BY 
	Mes_Ano;
```

Resultado da Query:

```markdown
| Mes_Ano | Faturamento_Total |
|---------|------------------|
| 2022-01 | 1952089         |
| 2022-02 | 1745508         |
| 2022-03 | 2012728         |
| 2022-04 | 1654909         |
| 2022-05 | 2016388         |
| 2022-06 | 3401361         |
| 2022-07 | 308263          |
```

---

## 4. Qual o faturamento total por região?
Essa query apresenta o faturamento total separado por região:

```sql
SELECT 
Continente, 
SUM(Faturamento) AS Faturamento
FROM 
	vendas
GROUP BY 
	Continente
ORDER BY 
	Faturamento DESC;
```

Resultado da Query:

```markdown
| Continente         | Faturamento |
|--------------------|------------|
| América do Norte  | 6943364    |
| Europa            | 3381300    |
| América do Sul   | 1683191    |
| Ásia             | 642446     |
| África           | 440945     |
```

---

## 5. Média de quantidade de vendas por mês
Essa query calcula a média de vendas por mês:

```sql
SELECT 
DATE_FORMAT(STR_TO_DATE(data_venda, '%d/%m/%Y'), '%Y-%m') AS Mes_Ano, 
       AVG(Qtd_Vendida) AS Media_Quantidade
FROM
	vendas
GROUP BY 
	Mes_Ano;
```

Resultado da Query:

```markdown
| Mes_Ano | Media_Quantidade |
|---------|------------------|
| 2022-01 | 1.9852           |
| 2022-02 | 1.9766           |
| 2022-03 | 1.9751           |
| 2022-04 | 2.0124           |
| 2022-05 | 1.9932           |
| 2022-06 | 1.9670           |
| 2022-07 | 1.9462           |
```

---

## 6. Qual a marca mais vendida por continente?
Essa query identifica a marca mais vendida por continente:

```sql
SELECT Continente, 
Marca, 
SUM(Qtd_Vendida) AS Qtd_Total
FROM 
	vendas
GROUP BY
	Continente, Marca
ORDER BY
	Qtd_Total DESC;
```

Resultado da Query:

```markdown
| Continente         | Marca          | Qtd_Total |
|--------------------|---------------|-----------|
| América do Norte  | Litware       | 53889     |
| Europa            | Litware        | 26338     |
| América do Sul   | Litware       | 13246     |
| Ásia             | Hashtag Toys  | 5302      |
| África           | Litware        | 3341      |
```

---

## 7. Qual o produto com maior ticket (maior valor médio por venda)?
Essa query identifica o produto com maior ticket médio:

```sql
SELECT Produto, 
SUM(Faturamento) / COUNT(*) AS Ticket_Medio
FROM 
	vendas
GROUP BY 
	Produto
ORDER BY 
	Ticket_Medio DESC
LIMIT 1;
```

Resultado da Query:

```markdown
| Produto                                  | Ticket_Medio |
|-----------------------------------------|--------------|
| Coffee Maker Super-Auto 12C X1250 Preto | 3080         |
```

---

