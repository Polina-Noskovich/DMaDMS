# DMaDCS
Database models and database control systems labs
## Прокат автомобилей
## Functional requirements
* User authorithation
* Role system (client, employee)
* Logging user actions
### For unathorised user:
* watching cars list
* wathcing cars categories
### For authorised user:
* Make an order
* Add feedback
### For employee:
* Rent management
* Rent category management
* Supplier_delivery management
* Sale management
## Entities
### user
    "id" BIGINT PRIMARY KEY NOT NULL,
    "name" VARCHAR(255) NOT NULL,
    "surname" VARCHAR(255) NOT NULL,
    "birth_date" DATE NOT NULL,
    "role_id" BIGINT NOT NULL -> role,
    "car_dep_id" BIGINT NULL -> car_department,
    "login" VARCHAR(255) NOT NULL,
    "password" VARCHAR(255) NOT NULL
### role
    "id" BIGINT PRIMARY KEY NOT NULL,
    "name" VARCHAR(255) NOT NULL
### car_department
    "id" BIGINT PRIMARY KEY NOT NULL,
    "address" VARCHAR(255) NOT NULL
### feedback
    "id" BIGINT PRIMARY KEY NOT NULL,
    "user_id" BIGINT NOT NULL -> user,
    "rate" INTEGER NOT NULL,
    "content" VARCHAR(255) NULL,
    "car_dep_id" BIGINT NOT NULL -> car_department
### supplier
    "id" BIGINT PRIMARY KEY NOT NULL,
    "name" VARCHAR(255) NOT NULL,
    "address" VARCHAR(255) NOT NULL
### supplier_delivery
    "id" BIGINT PRIMARY KEY NOT NULL,
    "car_dep_id" BIGINT NOT NULL -> car_department,
    "supplier_id" BIGINT NOT NULL -> supplier,
    "date" DATE NOT NULL
### category
    "id" BIGINT NOT NULL,
    "name" VARCHAR(255) NOT NULL
### medicine
    "id" BIGINT PRIMARY KEY NOT NULL,
    "name" BIGINT NOT NULL,
    "description" BIGINT NOT NULL,
    "supplier_id" BIGINT NOT NULL -> supplier,
    "category_id" BIGINT NOT NULL -> category,
    "price" NUMERIC NOT NULL
### sale
    "id" BIGINT PRIMARY KEY NOT NULL,
    "date" DATE NOT NULL,
    "car_dep_id" BIGINT NOT NULL -> car_department,
    "user_id" BIGINT NOT NULL -> user,
    "is_complete" BOOLEAN NOT NULL,
    "total_price" NUMERIC
### Log
    "id" BIGINT PRIMARY KEY NOT NULL,
    "user_id" BIGINT NOT NULL,
    "date" DATE NOT NULL,
    "action" VARCHAR(255) NOT NULL
## Block-scheme
