# Специфікація архітектури (Component Diagram) — B2B CRM (Лабораторна робота 5)

## 1. Мета та архітектурний підхід

Мета — побудувати компонентну модель архітектури B2B CRM-системи, яка об'єднує модель даних (Lab 1), функціональні та нефункціональні вимоги (Lab 2), діаграми послідовності (Lab 3) та процес створення угоди (Lab 4).

Обрано **багаторівневу модульну архітектуру (5 рівнів)**:
1. **Рівень UI (Presentation Layer)** — веб-клієнт (SPA) для менеджера, клієнта та адміністратора.
2. **Рівень API (Backend Controllers)** — приймання HTTP/REST запитів і первинна маршрутизація.
3. **Рівень сервісів (Service Layer)** — бізнес-логіка створення угод, валідації клієнтів і товарів, розрахунку знижок та відправки сповіщень.
4. **Рівень доступу до даних (Data Access Layer)** — репозиторії для роботи з сутностями домену.
5. **Рівень бази даних (Database Layer)** — реляційна СУБД PostgreSQL зі схемою даних за 3NF.

## 2. Межа системи (System Boundary) та зовнішні інтеграції

- **Усередині межі системи (`CRM System Boundary`):** усі модулі UI, API-контролери, доменні сервіси, репозиторії та реляційна база даних CRM.
- **Зовні межі системи:**
  - **Користувачі (Actors):** `Manager`, `Client`, `Administrator` (із Lab 2).
  - **Зовнішні сервіси (External Integrations):**
    1. `Identity Provider (OAuth2 / OIDC)` — перевірка облікових даних і видача токенів (NFR-03, сценарій S5).
    2. `Notification Gateway (SMS / Email)` — зовнішній шлюз доставки повідомлення клієнту «Підтвердьте умови угоди» (крок 6 із процесу Lab 4).
    3. `Payment Gateway` — зовнішній платіжний шлюз для оплати рахунків за угодами.
    4. `External ERP / Inventory API` — зовнішня складська система для звірки наявності товарів.

## 3. Внутрішні компоненти за рівнями

### 3.1 Рівень UI (Presentation Layer)
- `DealManagementUI` — форма створення та перегляду угод менеджером (UC-3, UC-8).
- `ClientManagementUI` — робота з клієнтами та кабінет підтвердження умов угоди клієнтом (UC-2, Lab 4).
- `ProductCatalogUI` — вибір товарів із каталогу (UC-5, UC-7).
- `AuthUI` — сторінка входу та керування сесією (UC-1, S5).

### 3.2 Рівень API / Backend Controllers
- `DealController` — приймає запити на створення та перегляд угод (`submitDeal` із Lab 3).
- `ClientController` — обробляє запити щодо клієнтів.
- `ProductController` — обробляє запити до каталогу товарів.
- `AuthController` — вхід у систему та перевірка токенів.

### 3.3 Рівень сервісів (Service Layer)
- `DealService` — координує створення угоди (`createDeal` із Lab 3): перевіряє клієнта, товари, суму угоди, викликає розрахунок знижки, зберігає угоду та ініціює сповіщення клієнту.
- `ClientService` — бізнес-перевірка клієнта.
- `ProductService` — перевірка обраних товарів та звірка залишків із зовнішнім ERP.
- `AuthService` — перевірка автентифікації та ролей (`isAuthenticated` із S5 у Lab 3).
- `NotificationService` — формування та відправка повідомлення клієнту для підтвердження умов угоди (крок 6 із Lab 4).
- `PricingEngine` — розрахунок суми угоди та застосування знижки (`applyDiscount` із UC-6 Lab 2 та `opt`-фрагмента S1 у Lab 3).

### 3.4 Рівень доступу до даних (Data Access Layer)
- `DealRepository` — збереження та читання сутності `Deal` і зв'язків із товарами.
- `ClientRepository` — пошук клієнтів (`findById` із Lab 3).
- `ProductRepository` — пошук товарів за списком ідентифікаторів (`findByIds` із Lab 3).
- `ManagerRepository` — доступ до даних менеджерів (`Manager` із Lab 1).

### 3.5 Рівень бази даних (Database Layer)
- `PostgreSQL Database` — зберігає таблиці сутностей `Manager`, `Client`, `Deal`, `Product` (відповідно до ER-моделі Lab 1 та NFR-06 із Lab 2).

## 4. Інтерфейси компонентів (Provided / Required)

| Компонент | Provided-інтерфейс (надає) | Required-інтерфейс (потребує) | Цільовий компонент | Призначення |
|---|---|---|---|---|
| `DealManagementUI` | — | `IDealAPI` | `DealController` | Відправка заявки на створення угоди (HTTPS/REST) |
| `ClientManagementUI` | — | `IClientAPI` | `ClientController` | Перегляд клієнтів та відповідь на умови угоди |
| `ProductCatalogUI` | — | `IProductAPI` | `ProductController` | Отримання переліку товарів |
| `AuthUI` | — | `IAuthAPI` | `AuthController` | Автентифікація користувача |
| `DealController` | `IDealAPI` | `IDealService`, `IAuthService` | `DealService`, `AuthService` | Перевірка сесії та делегування створення угоди |
| `ClientController` | `IClientAPI` | `IClientService` | `ClientService` | Запити по клієнтах |
| `ProductController` | `IProductAPI` | `IProductService` | `ProductService` | Запити по товарах |
| `AuthController` | `IAuthAPI` | `IAuthService` | `AuthService` | Логін та перевірка сесії |
| `DealService` | `IDealService` | `IClientService`, `IProductService`, `IPricingEngine`, `INotificationService`, `IDealRepository`, `IPaymentApi` | Відповідні сервіси, репозиторій та Payment Gateway | Повний цикл валідації, збереження та сповіщення по угоді |
| `ClientService` | `IClientService` | `IClientRepository` | `ClientRepository` | Перевірка існування клієнта |
| `ProductService` | `IProductService` | `IProductRepository`, `IErpInventoryApi` | `ProductRepository`, `External ERP API` | Перевірка товарів у БД та залишків у ERP |
| `AuthService` | `IAuthService` | `IManagerRepository`, `IOAuthIdentityApi` | `ManagerRepository`, `Identity Provider` | Перевірка користувача та OAuth2/OIDC токена |
| `NotificationService` | `INotificationService` | `IMessageGatewayApi` | `Notification Gateway` | Відправка клієнту запиту на підтвердження умов |
| `PricingEngine` | `IPricingEngine` | — | — | Обчислення знижки та фінальної суми угоди |
| `DealRepository` | `IDealRepository` | `ISqlDatabase` | `PostgreSQL Database` | SQL-запити до таблиці угод |
| `ClientRepository` | `IClientRepository` | `ISqlDatabase` | `PostgreSQL Database` | SQL-запити до таблиці клієнтів |
| `ProductRepository` | `IProductRepository` | `ISqlDatabase` | `PostgreSQL Database` | SQL-запити до таблиці товарів |
| `ManagerRepository` | `IManagerRepository` | `ISqlDatabase` | `PostgreSQL Database` | SQL-запити до таблиці менеджерів |
| `PostgreSQL Database` | `ISqlDatabase` | — | — | Транзакційне збереження даних (ACID) |

## 5. Трасування до моделей Lab 1–4

| Компонент (Lab 5) | Дані (Lab 1) | Вимоги (Lab 2) | Взаємодія (Lab 3) | Процес (Lab 4) |
|---|---|---|---|---|
| `DealManagementUI` | — | UC-3, NFR-04, NFR-05 | Актор `Manager` | Крок 1: подання заявки |
| `DealController` | — | FR-01..FR-06 | `DealController` (`submitDeal`) | Приймання заявки |
| `AuthController` / `AuthService` | `Manager` | UC-1, FR-05, S5, NFR-03 | `AuthService` (`isAuthenticated`) | Крок 2: перевірка автентифікації |
| `DealService` | `Deal` | UC-3, FR-01, FR-04, FR-06, S1–S4 | `DealService` (`createDeal`) | Кроки 3–7: координація процесу |
| `ClientService` / `ClientRepository` | `Client` | UC-2, UC-4, FR-02, S2 | `ClientRepository` (`findById`) | Крок 3: гілка перевірки клієнта |
| `ProductService` / `ProductRepository` | `Product` | UC-5, UC-7, FR-03, S3 | `ProductRepository` (`findByIds`) | Крок 3: гілка перевірки товарів |
| `PricingEngine` | `Deal.amount`, `Product.price` | UC-6 Apply Discount | `opt discount` (`applyDiscount`) | Крок 5: перевірка й розрахунок суми |
| `NotificationService` | `Client.contact_email` | — | — | Крок 6: повідомлення клієнту |
| `DealRepository` | `Deal`, зв'язок `Deal–Product` | FR-01, FR-07, NFR-06 | `INSERT deal` | Крок 7: збереження угоди (`new` / `draft`) |
| `PostgreSQL Database` | Усі 4 сутності (3NF) | NFR-06 | `Database` | Збереження стану угоди |

## 6. Критерії прийняття

1. Артефакти: декларативний опис компонентної діаграми у `model/component-diagram.mmd` (та `model/component-diagram.puml`) і графічний рендер у `model/component-diagram.png`.
2. Присутні всі 5 рівнів архітектури (UI, API, сервіси, Data Access, БД) та зовнішні інтеграції.
3. Визначено Provided та Required інтерфейси між компонентами.
4. Кожен компонент трасується до попередніх моделей (Lab 1–4).
