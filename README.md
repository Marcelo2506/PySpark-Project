# Análise de Dados de E-commerce com PySpark

Este projeto demonstra um processo completo de ETL (Extração, Transformação e Carga) utilizando **PySpark** para limpar, transformar e preparar um dataset de vendas de um e-commerce para futuras análises. O objetivo é demonstrar a capacidade da ferramenta em manipular e enriquecer dados de forma eficiente e escalável.

---

## 🛠️ Tecnologias Utilizadas
* **PySpark:** Para o processamento distribuído e manipulação dos dados.
* **Python:** Como linguagem principal para a criação do script.
* **Parquet:** Formato de arquivo utilizado para armazenamento dos dados.

---

## 🎯 O Desafio
O desafio consistiu em pegar um dataset bruto de pedidos (`orders_data.parquet`) e aplicar uma série de regras de negócio e limpeza para gerar um novo dataset tratado e consistente, pronto para ser consumido por equipes de análise e business intelligence.

---

## 🔄 Processo de ETL (Extração, Transformação e Carga)
As seguintes transformações foram aplicadas ao dataset original utilizando PySpark:

1.  **Filtragem e Conversão de Datas (`order_date`):**
    * Pedidos realizados na madrugada (entre 00h e 05h) foram removidos para focar nos horários de maior atividade comercial.
    * A coluna foi convertida do tipo `timestamp` para `date`, simplificando análises baseadas apenas no dia.

2.  **Criação da Coluna de Período do Dia (`time_of_day`):**
    * Uma nova coluna foi criada para categorizar os pedidos em "morning", "afternoon" e "evening", permitindo análises sazonais sobre o comportamento de compra ao longo do dia.

3.  **Limpeza da Coluna de Produtos (`product`):**
    * As linhas referentes ao produto "TV" foram removidas, pois o produto foi descontinuado pela empresa.
    * Todos os nomes de produtos foram convertidos para letras minúsculas para garantir a padronização.

4.  **Padronização da Categoria (`category`):**
    * Similarmente aos produtos, os nomes das categorias foram padronizados para letras minúsculas.

5.  **Extração do Estado (`purchase_state`):**
    * Uma nova coluna foi criada para armazenar apenas o estado da compra, extraindo essa informação da coluna `purchase_address`. Isso facilita a criação de análises geográficas.

O DataFrame final, limpo e transformado, foi salvo no formato Parquet sob o nome `orders_data_clean.parquet`.

---

## 📊 Sobre o Dataset Original (`orders_data.parquet`)

| column | data type | description | cleaning requirements |
|---|---|---|---|
| `order_date` | `timestamp` | Date and time when the order was made | _Modify: Remove orders placed between 12am and 5am (inclusive); convert from timestamp to date_ |
| `time_of_day` | `string` | Period of the day when the order was made | _New column containing (lower bound inclusive, upper bound exclusive): "morning" for orders placed 5-12am, "afternoon" for orders placed 12-6pm, and "evening" for 6-12pm_ |
| `order_id` | `long` | Order ID | _N/A_ |
| `product` | `string` | Name of a product ordered | _Remove rows containing "TV" as the company has stopped selling this product; ensure all values are lowercase_ |
| `product_ean` | `double` | Product ID | _N/A_ |
| `category` | `string` | Broader category of a product | _Ensure all values are lowercase_ |
| `purchase_address` | `string` | Address line where the order was made ("House Street, City, State Zipcode") | _N/A_ |
| `purchase_state` | `string` | US State of the purchase address | _New column containing: the State that the purchase was ordered from_ |
| `quantity_ordered` | `long` | Number of product units ordered | _N/A_ |
| `price_each` | `double` | Price of a product unit | _N/A_ |
| `cost_price` | `double` | Cost of production per product unit | _N/A_ |
| `turnover` | `double` | Total amount paid for a product (quantity x price) | _N/A_ |
| `margin` | `double` | Profit made by selling a product (turnover - cost) | _N/A_ |

---

## 🚀 A Importância do PySpark para Big Data e Tomada de Decisão
O **PySpark** é uma ferramenta fundamental no ecossistema de Big Data por sua capacidade de processar volumes massivos de dados de forma distribuída e paralela. Sua velocidade e escalabilidade permitem que empresas realizem análises complexas rapidamente, transformando dados brutos em insights valiosos e suportando tomadas de decisão mais inteligentes e estratégicas.