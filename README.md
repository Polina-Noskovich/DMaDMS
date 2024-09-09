# DATA MODELS AND DATABASE MANAGEMENT SYSTEMS
## Носкович Полина Николаевна гр. 253504
## Интернет-магазин косметики и парфюмерии
# 1. Определение темы проекта
## 1.1 Основные цели проекта
Онлайн-магазин косметики, в котором пользователи могут просматривать каталог товаров, добавлять их в корзину, оформлять заказы и отслеживать их статус. Администраторы могут управлять ассортиментом, заказами и пользователями.
# 2. Определение функциональных требований
## 2.1 Функциональные требования
* Авторизация пользователя. Роли: USER, PM, ADMIN.
* Управление пользователями (CRUD).
* Система ролей.
* Журналирование действий пользователя.
* Управление товарами (CRUD) (PM, ADMIN).
* Управление категориями товаров (CRUD) (ADMIN).
* Управление заказами (CRUD) (USER, PM).
* Управление скидками и акциями (CRUD) (ADMIN).
* Управление запасами на складе (PM, ADMIN).
* Просмотр статистики продаж (ADMIN).
# 3. Определение сущностей базы данных
## 3.1 Сущности

### 1. user
* id BIGINT NOT NULL, PK
* name TEXT NOT NULL
* email TEXT NOT NULL
* password_hash TEXT NOT NULL
* roleId BIGINT NOT NULL -> role
* createdAt DATE
* updatedAt DATE
  
### 2. role
* id BIGINT NOT NULL, PK
* name VARCHAR(255) NOT NULL (Примеры: "ПОКУПАТЕЛЬ", "МЕНЕДЖЕР", "АДМИНИСТРАТОР")
* description TEXT NULL
* createdAt DATE
* updatedAt DATE
  
### 3. product
* id BIGINT NOT NULL, PK
* name TEXT NOT NULL
* description TEXT NULL
* price DECIMAL(10, 2) NOT NULL
* categoryId BIGINT NOT NULL -> category
* stockQuantity INT NOT NULL
* createdAt DATE
* updatedAt DATE
  
### 4. category
* id BIGINT NOT NULL, PK
* name TEXT NOT NULL
* createdAt DATE
* updatedAt DATE
  
### 5. order
* id BIGINT NOT NULL, PK
* userId BIGINT NOT NULL -> user
* totalPrice DECIMAL(10, 2) NOT NULL
* orderDate DATE NOT NULL
* status VARCHAR(255) NOT NULL
* createdAt DATE
* updatedAt DATE
  
### 6. order_item
* id BIGINT NOT NULL, PK
* orderId BIGINT NOT NULL -> order
* productId BIGINT NOT NULL -> product
* quantity INT NOT NULL
* price DECIMAL(10, 2) NOT NULL
* createdAt DATE
* updatedAt DATE
  
### 7. discount
* id BIGINT NOT NULL, PK
* name TEXT NOT NULL
* description TEXT NULL
* discountPercentage DECIMAL(5, 2) NOT NULL
* startDate DATE NOT NULL
* endDate DATE NOT NULL
* createdAt DATE
* updatedAt DATE
  
### 8. stock
* id BIGINT NOT NULL, PK
* productId BIGINT NOT NULL -> product
* quantity INT NOT NULL
* location TEXT NULL
* createdAt DATE
* updatedAt DATE
  
### 9. user_activity
* id BIGINT NOT NULL, PK
* userId BIGINT NOT NULL -> user
* activityType VARCHAR(255)
* createdAt DATE
* updatedAt DATE
  
### 10. promotion
* id BIGINT NOT NULL, PK
* name TEXT NOT NULL
* description TEXT NULL
* discountId BIGINT NULL -> discount
* startDate DATE NOT NULL
* endDate DATE NOT NULL
* createdAt DATE
* updatedAt DATE
  
## 3.2 Описание сущностей
* user: Содержит информацию о пользователях системы, таких как покупатели, менеджеры и администраторы. Хранит данные об имени, электронной почте, пароле и ролях.
* role: Описывает роли, которые могут быть назначены пользователям (например, ПОКУПАТЕЛЬ, МЕНЕДЖЕР, АДМИНИСТРАТОР).
* product: Представляет информацию о товарах, доступных в магазине. Включает название, описание, цену, категорию и количество на складе.
* category: Классификация товаров по категориям (например, уход за лицом, уход за телом).
* order: Содержит информацию о заказах, сделанных пользователями, таких как покупатель, общая стоимость заказа, дата заказа и статус.
* order_item: Связующая таблица между заказами и товарами, содержит информацию о товарах, входящих в заказ.
* discount: Информация о скидках, которые могут быть применены к товарам.
* stock: Учет остатков товаров на складе, позволяет отслеживать количество товаров в наличии и их местоположение.
* user_activity: Логирует действия пользователей в системе, такие как добавление товара в корзину, создание заказа и другие важные операции.
* promotion: Содержит информацию о различных акциях и промо-мероприятиях, связанных с магазином.
