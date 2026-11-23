# Промпт 2 — Початкова генерація Mermaid erDiagram

**Задача для AI:** Згенерувати код Mermaid erDiagram на основі моєї специфікації `spec.md`.

**Промпт:**

> На основі наступної специфікації згенеруй код Mermaid erDiagram. Відобрази всі сутності, атрибути з типами та зв'язки між ними з відповідними кардинальностями.
>
> [вставлено текст spec.md версії v1]

**Відповідь AI:**

Ось код Mermaid erDiagram, згенерований за наданою специфікацією:

```mermaid
erDiagram
    Manager ||--o{ Deal : manages
    Client ||--o{ Deal : has
    Deal ||--o{ DealProduct : contains
    DealProduct }o--|| Product : references

    Manager {
        UUIDv7 manager_id PK
        string email UK
        string full_name
        timestamp created_at
    }
    Client {
        int client_id PK
        string company_name
        string contact_email UK
        timestamp created_at
    }
    Deal {
        UUIDv7 deal_id PK
        UUIDv7 client_id FK
        UUIDv7 manager_id FK
        string title
        float deal_amount
        string status
        timestamp created_at
    }
    DealProduct {
        UUIDv7 deal_id FK
        UUIDv7 product_id FK
    }
    Product {
        UUIDv7 product_id PK
        string name UK
        float price
        string description
    }
```
