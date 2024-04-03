
# 🛵 Desafio Delivery Center: Food & Goods

Este projeto é resultado de um desafio do grupo de assinaturas Universidade dos Dados, feito a partir do dataset Delivery Center: Food & Goods orders in Brazil disponível no [Kaggle](https://www.kaggle.com/datasets/nosbielcs/brazilian-delivery-center) e enviado por [Nosbielcs](https://www.kaggle.com/nosbielcs).

![Imagem](https://images.unsplash.com/photo-1526367790999-0150786686a2?q=80&w=2071&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

### 🛠️ Ferramentas utilizadas
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

## 1.1. O desafio

Trabalhamos em uma startup de delivery, em um time de dados centralizado que atende diversas áreas e recebemos algumas demandas:

- Numa ação de marketing, para atrair mais entregadores, vamos dar uma bonificação para os 20 entregadores que possuem maior distância percorrida ao todo. A bonificação vai variar de acordo com o tipo de profissional que ele é e o modelo que ele usa para se locomover (moto, bike, etc). Levante essas informações.
- Além disso, o time de Pricing precisa ajustar os valores pagos aos entregadores. Para isso, eles precisam da distribuição da distância média percorrida pelos motoqueiros separada por estado, já que cada região terá seu preço.
- Por fim, o CFO precisa de alguns indicadores de receita para apresentar para a diretoria executiva. Dentre esses indicadores, vocês precisarão levantar (1) a receita média e total separada por tipo (Food x Good), (2) A receita média e total por estado. Ou seja, são 4 tabelas ao todo.
- Se a empresa tem um gasto fixo de 5 reais por entrega, recebe 15% do valor de cada entrega como receita e, do total do lucro, distribui 20% em forma de bônus para os 2 mil funcionários, quanto cada um irá receber no período contido no dataset?

## 1.2. Importação das bibliotecas e carregamento dos dados
A bibliotecas utilizadas foram o pandas, numpy, datetime, os, matplotlib, seaborn e warnings.

# 🧱2. Estrutura, limpeza e manipulação dos dados 
![est](https://i.imgur.com/A8JD3RG.png)
##  2.1. Deliveries
No dataset deliveries identifiquei os outliers em "delivery_distance_meters".

![bp1](https://i.imgur.com/Xk0eXuo.png)

E então removi estes dados, este é o resultado após a limpeza. 

![bp2](https://i.imgur.com/tSXj3Tt.png)

Após isso mantive somente as entregas com status de "DELIVERED".

## 2.2. Drivers
Aqui foram mantidas apenas as colunas "driver_id" e "driver_modal".

## 2.3. Hubs
Aqui foram mantidas apenas as colunas "hub_id" e "hub_state".

## 2.4. Orders 
Em orders primeiro foram selcionadas somente as colunas que seriam utilizadas.
![orders](https://i.imgur.com/80l4krT.png)

E então foi criada uma coluna única para data do pedido, nomeada "order_date".
![date](https://i.imgur.com/1azh0wd.png)

E por fim foram mantidas somente as entregas com status "FINISHED"

## 2.5. Payments
Neste dataset também foram identificados outliers, em "payment_amount" e "payment_fee".

![bp3](https://i.imgur.com/E3dTOFK.png)

![bp4](https://i.imgur.com/5qvtHVH.png)

E então segui para o processo de remoção dos outliers. E este foi o resultado. 

![bp5](https://i.imgur.com/qRKTgJn.png)

![bp6](https://i.imgur.com/m9i1nHt.png)

## 2.6. Stores
Aqui foram mantidas apenas as colunas "store_id", "hub_id" e "store_segment".

## 2.7. Criando um dataset unificado 
### Os critérios e ajustes para unir orders, deliveries e payments
O caminho que segui foi o seguinte: cada **pedido (order)**, segue para **entrega (deliveries_clean)** e ao final recebe um **pagamento (payments_clean)**.

Mas antes dos JOINS foi criada a coluna "order_revenue" que define a receita em cada entrega. 

![revenue](https://i.imgur.com/lLsZCIo.png)

Após este processo foram feitos os JOINS e a criação do dataset que será base para responders todas as demandas.

# ✔ 3. Respondendo as demandas
## 3.1. Ranking dos entregadores
Aqui a partir do método groupby foram feitos os rankings para "MOTOBOY" e "BIKER".

![motoboy](https://i.imgur.com/3yCHGvN.png)

![bike](https://i.imgur.com/sRoI6n7.png)

## 3.2. Média de metros percorridas por entrega em cada estado
Também através do método groupby foi feita a tabela das médias de distância percorrida.

![mean](https://i.imgur.com/gTJL0ps.png)

## 3.3. Receitas médias e totais por segmento e estados
Outra vez através do groupby foi possível obter os resultados. 
### Receitas médias e totais por segmento
![receita](https://i.imgur.com/cSjJfNb.png)

![receita2](https://i.imgur.com/mclMYla.png)
### Receitas médias e totais por estado

![estado](https://i.imgur.com/y7VQCaZ.png)

![estado2](https://i.imgur.com/YQYRvZB.png)

## 3.4. Bônus para os funcionários
E ao fim, o bônus para cada funcionário foi de R$ 233,90.
