---
title: Тестовая БД
nav_order: 2
---

## Тестовая БД

Тестовая БД представляет хранилище данных интернет-магазина (маркетплейса). 

Данные из операционных БД отдельных сервисов агрегируются на слое сырых данных, после чего попадают в таблицы измерений и таблицы фактов (детальный слой). На основе детального слоя строятся прикладные витрины.

```mermaid
block

block:apps
    columns 1
    a1[("ClientService")]
    a2[("OrderService")]
    a3[("ProductService")]
end 

space

block:raw_data
    columns 1
    raw_client
    raw_product
    raw_order
    _1["..."]
end

space

block:detail
    columns 1
    dim_product
    dim_client
    fact_order
    _2["..."]
end

space

marts

apps --> raw_data
raw_data --> detail
detail --> marts

```
