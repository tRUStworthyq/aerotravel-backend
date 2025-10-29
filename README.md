# AeroTravel

[![Status](https://img.shields.io/badge/status-in%20development-orange)](https://github.com/your_username/AeroTravel)
[![Java](https://img.shields.io/badge/Java-21-blue)](https://openjdk.org/projects/jdk/21/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.5-brightgreen)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/license-MIT-green)](https://opensource.org/licenses/MIT)

**AeroTravel** — это учебный веб-сервис для поиска, бронирования и покупки авиабилетов. Проект реализуется на современном стеке Java-технологий и предназначен для отработки навыков full-stack разработки с использованием микросервисной архитектуры.

## Основной функционал

*   **Поиск рейсов** с фильтрацией по дате вылета/прилета, аэропорту назначения и отправления, цене.
*   **Бронирование** выбранных рейсов.
*   **Процесс оплаты** (симуляция).
*   **Просмотр истории** всех бронирований и покупок.
*   **Управление активными бронированиями**.

## Технологический стек

*   **Бэкенд:** Java 21, Spring Boot 3.5.5, Spring Cloud
*   **Аутентификация и авторизация:** Keycloak 26
*   **База данных:** PostgreSQL 16
*   **Кэширование:** Redis 8.0
*   **Асинхронная обработка событий:** Apache Kafka 3.9
*   **Сборка:** Apache Maven 3.9.6
*   **Контейнеризация и развертывание:** Docker 25.0.2, Docker Compose

## Структура проекта

Проект будет использовать микросервисную архитектуру со следующими сервисами:

*   **gateway-service** - API Gateway для маршрутизации запросов [README](./services/gateway-service/README.md)
*   **discovery-service** - Service Discovery (Eureka Server) [README](./services/discovery-service/README.md)
*   **flight-service** - Поиск и управление рейсами [README](./services/flight-service/README.md)
*   **booking-service** - Управление бронированием с использованием Saga Pattern [README](./services/booking-service/README.md)
*   **payment-service** - Обработка платежей (симуляция) [README](./services/payment-service/README.md)
*   **user-service** - Хранение, обработка и изменение информации о пользователе [README](./services/user-service/README.md)
*   **notification-service** - Отправка уведомлений [README](./services/notification-service/README.md)
*   **idempotency-service** - Обеспечение идемпотентности для HTTP-запросов и Kafka сообщений [README](./services/idempotency-service/README.md)

**Общие модули:**
*   **internal-interface** - Общий модуль с DTO, событиями Kafka для межсервисного взаимодействия ([README](./libs/internal-interface/README.md))

## Быстрый старт

Проект находится на начальной стадии разработки. Инструкции по запуску будут добавлены по мере реализации функциональности.

### Предварительные требования

* Установленный Docker >= 25.0.3
* Установленный Docker Compose >= v2.24.6
* Свободные порты на локальной машине:
  * 8080 - Keycloak
  * 5432 - PostgreSQL
  * 6379 - Redis
  * 9092 - Kafka
  * 2181 - ZooKeeper

### Запуск инфраструктуры

1. Клонируйте репозиторий:
    ```bash
    git clone https://github.com/tRUStworthyq/aerotravel-backend.git
    cd AeroTravel
    ```

2. Запустите сервисы с помощью Docker Compose:
   ```bash
   docker compose -f infra/docker-compose.dev.yml up -d
   ```
3. После запуска будут доступны следующие сервисы:
* Keycloak - ```http://localhost:8080```
  * Логин - ```admin```
  * Пароль - ```adminpassword```
* PostgreSQL - ```localhost:5432```
  * База данных - ```keycloak```
  * Пользователь - ```keycloak```
  * Пароль - ```keycloak```
* Redis - ```localhost:6379```
  * Пароль - ```redispassword```
* Kafka - ```localhost:9092```
  * ZooKeeper порт - ```2181```

4. Для остановки сервисов выполните:
   ```bash
   docker compose -f infra/docker-compose.dev.yml down
   ```

### Примечания

* Для полной очистки данных (Включая базу данных) используйте команду:
   ```bash
   docker compose -f infra/docker-compose.dev.yml down -v
   ```
* Данная конфигурация предназначена только для локальной разработки и не подходит для использования в production

Дополнительные инструкции по настройке и разработке будут добавляться по мере реализации функциональности.

## Roadmap (Планы по развитию)

### Фаза 0: Подготовка и инициализация

*   [&check;] Создание структуры многомодульного проекта
*   [&check;] Инициализация общего модуля internal-interface с DTO и событиями
*   [&check;] Настройка репозитория и веток
*   [&check;] Создание базовой документации (README, ADR шаблон)
*   [&check;] Написание docker-compose.yml для инфраструктуры

### Фаза 1: Базовая инфраструктура и поиск

*   [] Настройка API Gateway
*   [] Поднятие инфраструктуры: Kafka, PostgreSQL, Redis, Keycloak
*   [] Разработка Flight Service с интеграцией Amadeus API
*   [] Реализация кеширования результатов поиска 
*   [] Настройка шаблона CI для микросервисов
*   [] Создание документации API через Swagger/OpenAPI

### Фаза 2: Бронирование и пользователи

*   [] Создание User Service и интеграция с Keycloak
*   [] Реализация Booking Service с паттерном SAGA
*   [] Настройка асинхронной коммуникации через Kafka
*   [] Создание диаграмм архитектуры (C4 модель)

### Фаза 3: Платежи и уведомления

*   [] Разработка Payment Service (Симуляция платежного шлюза)
*   [] Реализация Notification Service 
*   [] Интеграция платежей в процесс бронирования через SAGA
*   [] Написание интеграционных тестов для ключевых сценариев

### Фаза 4: Доп функции и оптимизация

*   [] Реализация механизма идемпотентности для обработки событий
*   [] Настройка централизованного логирования
*   [] Настройка трассировки запросов
*   [] Оптимизация производительности и нагрузочное тестирование
*   [] Рефакторинг и улучшение тестового покрытия
*   [] Настройка CI/CD для прода
*   [] Финальное документирование всех компонентов системы
*   [] Подготовка демонстрации проекта


## Лицензия

Этот проект распространяется под лицензией MIT. Подробнее см. в файле [LICENSE](LICENSE.txt).