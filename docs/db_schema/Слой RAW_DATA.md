---
title: Сырые данные
parent: Схема данных
nav_order: 2
---

# Слой сырых данных

Ниже представлены таблицы слоя сырых данны. Это исторические данные, полученные от источников "как есть".

Некоторые связанные сущности приведены к плоскому виду. Каждая запись имеет код системы-источника и дату загрузки.

## raw_client

```mermaid
erDiagram

raw_client {
    client_id text PK "ID клиента"
    name text "ФИО клиента"
    birthdate date "Дата рождения клиента"
    gender text "Пол клиента"
    phone_number text "Номер телефона клиента"
    email text "Электронна япочта клиента"
    registration_dttm datetime "Дата регистрации клиента"
    address_country text "Страна проживания"
    address_region text "Регион"
    address_city text "Город"
    address_street text "Название улицы"
    address_house text "Номер дома"
    address_postal_code text "Почтовый индекс"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_product

```mermaid
erDiagram

raw_product {
    product_id text PK "ID продукта"
    product_name text "Наименование продукта"
    description text "Описание продукта"
    category_id int FK "Ссылка на категорию"
    weight_kg int "Вес единицы товара в кг"
    product_length int "Длина упаковки"
    product_width int "Ширина упаковки"
    product_height int "Высота упаковки"
    sku text "Номер единицы складского учёта"
    price_value int "Цена продукта"
    price_currency int FK "Ссылка на валюту цены"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_category

```mermaid
erDiagram

raw_category {
    category_id int PK "ID категории"
    category_name text "Наименование категории"
    description text "Описание категории"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_currency

```mermaid
erDiagram

raw_currency {
    currency_id int PK "ID валюты"
    currency_code text "Буквенный код валюты"
    currency_name text "Наименование валюты"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_stock

```mermaid
erDiagram

raw_stock {
    product_id text PK,FK "Ссылка на продукт"
    last_update timestamptz PK "Время последнего обновления остатка"
    quantity int "Остаток, единиц продукции"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_supply

```mermaid
erDiagram
raw_supply {
    supply_id text PK "ID поставки"
    supply_datetime timestamptz "Время поставки"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_supply_item 

```mermaid
erDiagram

raw_supply_item {
    supply_id text PK,FK "Ссылка на поставку"
    product_id text PK,FK "Ссылка на продукт"
    quantity int "Количество единиц продукции"
    batch_number text "Номер партии"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_shipment

```mermaid
erDiagram

raw_shipment {
    shipment_id text PK "ID отгрузки"
    shipment_datetime timestamptz "Время отгрузки"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_shipment_item

```mermaid
erDiagram

raw_shipment_item {
    shipment_id text PK,FK "Ссылка на отгрузку"
    product_id text PK,FK "Ссылка на продукт"
    quantity int "Количество единиц товара"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_order

```mermaid
erDiagram

raw_order {
    order_id text PK "ID заказа"
    client_id text FK "Ссылка на клиента"
    pick_up_point_id text FK "Ссылка на пункт выдачи"
    positions List~OrderPosition~
    status text "Статус заказа"
    track_number text "Трек-номер заказа"
    total_price_value int "Итогоавая цена"
    total_price_currency int FK "Ссылка на валюту"
    creation_dttm timestamptz "Время создания заказа"
    update_dttm datetime "Время последнего обновления заказа"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_order_position

```mermaid
erDiagram

raw_order_position {
    order_id text PK,FK "Ссылка на заказ"
    product_id text PK,FK "Ссылка на продукт"
    quantity int
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```

## raw_pick_up_point
```mermaid
erDiagram

raw_pick_up_point {
    point_id text PK "ID пункта выдачи"
    open_date date "Дата открытия пункта выдачи"
    address_country text "Страна проживания"
    address_region text "Регион"
    address_city text "Город" 
    address_street text "Название улицы"
    address_house text "Номер дома"
    address_postal_code int "Почтовый индекс"
    src_system text "Наименование системы-источника"
    load_dttm timestamptz "Время загрузки заипси с источника"
}

```
