# 02.2 - 示例数据库与 ER 图

> **模块状态**: ✅ 已完成  
> **上级目录**: [← 返回数据模型总览](./README.md)

---

本项目提供了两套示例数据源，用于演示智能体的建模、查询与分析能力：

1. **产品交易库（MySQL）**：`docker-file/config/mysql/product_db.sql`
2. **人口统计库（PostgreSQL）**：`docker-file/config/postgres/china_population_db.sql`

它们体现了两类典型业务：**交易型数据** 与 **统计型数据**，便于验证 NL2SQL 与数据分析能力。

---

## 🛒 产品交易库（product_db）ER 图

```mermaid
erDiagram
    users {
        INT id PK "用户ID"
        VARCHAR username "用户名"
        VARCHAR email "邮箱"
        DATETIME created_at "注册时间"
    }

    products {
        INT id PK "商品ID"
        VARCHAR name "商品名称"
        DECIMAL price "商品单价"
        INT stock "库存"
        DATETIME created_at "上架时间"
    }

    orders {
        INT id PK "订单ID"
        INT user_id FK "下单用户"
        DATETIME order_date "下单时间"
        DECIMAL total_amount "订单金额"
        VARCHAR status "订单状态"
    }

    order_items {
        INT id PK "订单明细ID"
        INT order_id FK "订单"
        INT product_id FK "商品"
        INT quantity "购买数量"
        DECIMAL unit_price "成交单价"
    }

    categories {
        INT id PK "分类ID"
        VARCHAR name "分类名称"
    }

    product_categories {
        INT product_id FK "商品ID"
        INT category_id FK "分类ID"
    }

    users ||--o{ orders : "1:N"
    orders ||--o{ order_items : "1:N"
    products ||--o{ order_items : "1:N"
    products ||--o{ product_categories : "N:M"
    categories ||--o{ product_categories : "N:M"
```

### 业务语义解析

- 这是典型的电商交易模型，`orders` 是事实表，`order_items` 是明细表。
- `product_categories` 把商品与分类解耦，支持多对多，适合检索“某类商品的销售情况”。

**二次开发指南**：
- 若新增促销或优惠券，建议引入独立的 `promotion` 与 `order_discount` 表，避免污染订单主表结构。

---

## 📈 人口统计库（china_population_db）ER 图

```mermaid
erDiagram
    population_total {
        INT id PK "主键"
        INT year UK "年份"
        BIGINT total_population "总人口"
        DECIMAL natural_growth_rate "自然增长率"
        DECIMAL birth_rate "出生率"
        DECIMAL death_rate "死亡率"
    }

    gender_ratio {
        INT id PK "主键"
        INT year UK "年份"
        BIGINT male_population "男性人口"
        BIGINT female_population "女性人口"
        DECIMAL sex_ratio "性别比"
    }

    age_structure {
        INT id PK "主键"
        INT year UK "年份"
        VARCHAR age_group "年龄段"
        BIGINT population "人口数"
        DECIMAL percentage "占比"
    }

    urban_rural_distribution {
        INT id PK "主键"
        INT year UK "年份"
        BIGINT urban_population "城镇人口"
        BIGINT rural_population "农村人口"
        DECIMAL urban_percentage "城镇化率"
    }

    province_population {
        INT id PK "主键"
        INT year UK "年份"
        VARCHAR province_code "省份代码"
        VARCHAR province_name "省份名称"
        BIGINT total_population "人口总数"
    }

    population_total ||--o{ gender_ratio : "1:1(按year)"
    population_total ||--o{ age_structure : "1:N(按year)"
    population_total ||--o{ urban_rural_distribution : "1:1(按year)"
    population_total ||--o{ province_population : "1:N(按year)"
```

### 业务语义解析

- 这是典型的**统计维度型模型**，`year` 是事实粒度。
- 该模型适合做趋势分析和多维钻取，例如“某年城镇化率与性别比的相关性”。

**二次开发指南**：
- 如需增加更细粒度（季度、月度），应引入 `time_dim` 维度表，避免仅用 `year` 造成扩展困难。
