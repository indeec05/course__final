## Общее описание архитектуры

Эта секция описывает выбранный подход к архитектуре, решения, причины выбора и накладываемые им ограничения.

|Ограничение|Мотивация|
|-----------|---------|
|Использовать облачный слой инфраструктуры в составе Azure|1. Уменьшение нагрузки на команду за счет снижения издержек на поддержку инфраструктуры. 2. Возможность быстрого масштабирования. 3. Уже в стеке Компании|
|Стек решения - .Net Core 6, PostgreSQL, Keycloak|Низкая стоимость реализации за счет того, что все эти технологии уже в стеке Компании. И они Open Source|
|Монолитная архитектура Системы|Так как основным критерием является низкий Time to market, было принято решение сознательно уменьшать сложность|
|Контейнеризация и оркестрация на Kubernetis|Несмотря на то, что приложение монолитно, принято решение сразу использовать практики devops, чтобы не выбиваться из общего стека Компании|
|Система ведения документации - Git, рядом с кодом. Для форматирования текста - Markdown. Для диаграмм - plantUml|Удобство написания документации и сопровождения как разработчиками, так и аналитиком проекта|
|Программный интерфейс - restAPI|Характер нагрузки не накладывает ограничений, по которым мы бы не могли выбрать этот наиболее распространенный протокол взаимодействия систем поверх http|

## Слой контекста

![](../../img/unnamed.png)

В ИТ ландшафт нашего домена входят перечисленные на диаграмме системы, которые можно разделить по зонам ответственности (внешние и внутренние по отношению к нам) и по степени важности реализации на этапе MVP (первый этап) или в дальнейшем по ходу развития Системы (второй этап).

|Название системы|Описание|Зона ответственности|Этап|
|----------------|--------|--------------------|----------------|
|Booking system|Основное приложение Системы, реализующее весь ее бизнес-функционал. Именно его мы будем разрабатывать|Компания|1|
|Email Service|Почтовый сервис. Обслуживает домен системы booking-system.example|Компания|1|
|R-Keeper|Система учета ресторанов. Каждый ресторан имеет свою копию, однако система бронирования работает централизованно|Клиент|1|
|1С|ERP система предприятия. Нужна для организации документооборота.|Компания|2|
|Wallet One|Платежная система для организации процесса оплат на сайте|Подрядчик|2|
|Google Maps|Сервис бесплатных карт. Планируется для интеграции в Приложения для удобства поиска ресурсов Клиентов|Подрядчик|1|
|Google Analitycs|Сервис поисковой и поведенческой аналитики. Планируется использовать его в Приложении для анализа действий Посетителей|Подрядчик|1|
|Контур.Фокус|Сервис проверки и предоставления информации о юридических лицах. Используется менеджерами Компании и на этапе MVP, однако полноценная интеграция с ним предполагается только на втором этапе|Подрядчик|2|

## Слой контейнеров

![](../../img/unnamed2.png)

| №П/П | Тип             | Наименование              | Технологии               | Описание                                               |
| ---- | --------------- | ------------------------- | ------------------------ | ------------------------------------------------------ |
| 1    | Software System | BookingSystem             | Java, Spring Boot        | Сервис, реализующий бизнес логику.                     |
| 2    | Container       | BookingWebApp             | React, JavaScript        | Веб-интерфейс для клиентов и сотрудников. SPA          |
| 3    | Container       | BookingAndroidApplication | Kotlin                   | Мобильное приложение для клиентов, Android.            |
| 4    | Container       | BookingIOSApplication     | Swift                    | Мобильное приложение для клиентов, iOS.                |
| 5    | Container       | Booking database          | PostgreSQL               | Основная БД проекта.                                   |
| 6    | Software System | 1C [*](#примечания)    | Платформа 1С:Предприятие | Хранение клиентов, автоматизация учета                 |
| 7    | Software System  | Wallet One [*](#примечания)| REST API                 | Платежная система для реализации функционала оплаты    |
| 8    | Software System | Email Service             | SMTP                     | Отправка уведомлений клиентам                          |
| 9    | Software System | R-Keeper                  | REST API                 | Информация о столиках, расписание, бронирование        |
| 10   | Software System | Google Maps               | REST API                 | Просмотр ресторанов на карте в интерфейсе пользователя |
| 11   | Software System | Google Analitycs          | REST API                 | Формирование аналитики по посещениям                   |
| 12   | Software System | Контур.Фокус [*](#примечания)| REST API                 | Проверка контрагентов-юридических лиц                  |
| 13   | Container       | Keycloak                  | Java, Oauth2             | Сервис авторизации и аутентификации                  |

## API

### Общее описание

Ниже представлено описание интерфейса основного приложения Системы. Оно построено на rest-принципах, работает с реальными объектами и обладает предсказуемым поведением. С его помощью можно управлять ресторанами, столиками, бронированиями и учетными записями Пользователей Системы.

Формат тела запросов и ответов - JSON.

Основной API эндпоинт: ```dev.booking-system.example```

### Авторизация

Авторизация в API построена на принципах oauth 2.0 и использует [Bearer tocken](https://oauth.net/2/bearer-tokens/). Для получения токена необходимо обратиться к ресурсу /auth с набором данных, полученных на этапе регистрации. Пример такого запроса приведен ниже:

```curl
curl --location --request POST 'http://dev.booking-system.exampl/auth/realms/realm/protocol/openid-connect/token/' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username=usernaim' \
--data-urlencode 'password=password' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'tocken_type=bearer' \
--data-urlencode 'client_secret=b6f0b3fc-1a62-4e6b-b483-222d9d5e569e' \
--data-urlencode 'client_id=client_id'
```

В случае успеха в ответе придет access tocken, который и необходимо использовать для авторизации в Системе. Пример вызова с авторизацией:

```
curl -X 'GET' \
  'http://dev.booking-system.exampl/places?offset=0&limit=20' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4NUg2VWtzZFBON2RXU191ZlJQVF9EdUY0MjFJa05sRC10VUE4U1Q1TWNRIn0.eyJleHAiOjE2NTEyNDQ0MjksImlhdCI6MTY1MTI0NDEyOSwianRpIjoiODkxOTE4MmItZWU5OC00OWUzLWI1NjItMmFlYjIyNDI4ODA0IiwiaXNzIjoiaHR0cDovLzEwLjIwMi4xOS4xMDA6ODA4My9hdXRoL3JlYWxtcy9ubXgiLCJhdWQiOlsicGx1dF9wZXIiLCJwbHV0X2ludiIsInBsdXRfYWNjIiwicGx1dF9zbXoiLCJwbHV0X3BpcCIsInBsdXRfa3ljIiwiYWNjb3VudCIsInBsdXRfY25zIiwicGx1dF9wdGwiLCJwbHV0X2lhcCJdLCJzdWIiOiI4Yzc5NWZiOS02OWRkLTRhM2MtOWJjNC03ZGE2OTM2NTAyOWMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJuYWltaXgiLCJzZXNzaW9uX3N0YXRlIjoiM2Y3MzA3MmQtYjQ5Mi00MDU3LTgyMmEtYTU5MjEzZmI1NzM5IiwiYWNyIjoiMSIsInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsInVtYV9hdXRob3JpemF0aW9uIl19LCJyZXNvdXJjZV9hY2Nlc3MiOnsicGx1dF9wZXIiOnsicm9sZXMiOlsiVVNFUiJdfSwicGx1dF9pbnYiOnsicm9sZXMiOlsiVVNFUiJdfSwicGx1dF9hY2MiOnsicm9sZXMiOlsiVVNFUiJdfSwicGx1dF9zbXoiOnsicm9sZXMiOlsiQURNSU4iLCJVU0VSIl19LCJwbHV0X3BpcCI6eyJyb2xlcyI6WyJVU0VSIl19LCJwbHV0X2t5YyI6eyJyb2xlcyI6WyJVU0VSIl19LCJhY2NvdW50Ijp7InJvbGVzIjpbIm1hbmFnZS1hY2NvdW50IiwibWFuYWdlLWFjY291bnQtbGlua3MiLCJ2aWV3LXByb2ZpbGUiXX0sInBsdXRfY25zIjp7InJvbGVzIjpbIlVTRVIiXX0sInBsdXRfcHRsIjp7InJvbGVzIjpbIlVTRVIiXX0sInBsdXRfaWFwIjp7InJvbGVzIjpbIlVTRVIiXX19LCJzY29wZSI6ImVtYWlsIHByb2ZpbGUiLCJMZWdhbEVudGl0eVNldHRpbmdzIjp7ImlkIjoiYTY3YzVjNGYtM2M2Zi00MmQ0LWJmMTMtMWFhNGI4NjAwNmE1In0sImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoibmFpbWl4In0.gRwsq9t6DUQXPwz7MkX7zRGXRiCuk_OqJHUbSfkTVwAb_f_0ZJdACmJpnwdWnMOvEXQMeb0FnCrxRo66LPPU9WbcXt7yJFBCK32Vo1v6Ug_DrMiGDBJGAJizxCJuNE_pcvrBNlX3ft4Rsi5JjCgz_U9aDAzY-ElDnefoYOo7LqiBAiwves_mpjG6Plkor31oOL9pvXeLb9u-5VudbAsd57z1WX8c8-NVn58IRsMzui6_dgiYBQ3iucFVDo2kxLU8gXSrXME4gJdVw-1dLHrc_fAoBdgCncdOM8wUrwB7XJzQESOCZ6_L160aFvc2kmVIThE4LJ4SEgkn_z8YJTpnfQ'
```

Время жизни токена - 300 секунд, после чего вам необходимо получить новый с временем жизни 1 час.

### Обработка ответов

Система обрабатывает полученный запрос немедленно и возвращает результат обработки («успех» или «неудача»). Ответ содержит код ответа HTTP, стандартные заголовки и при необходимости тело ответа в формате JSON.

Если в течение 30 секунд невозможно дать точный ответ, то Система вернет код ответа HTTP 500. Этот статус не говорит об успешности или неуспешности выполнения операции. Поэтому при получении HTTP 500 вам необходимо сначала узнать результат обработки запроса и только после этого принимать любые решения, связанные с этой операцией.

При успешной обработке запроса (HTTP 200) ЮKassa возвращает в теле ответа созданный, измененный или запрошенный объект или список объектов.

### Коды ответов HTTP

В рамках Системы возможны следующие коды ответов HTTP:

|Код ответа|Описание|
|----------|--------|
|200|Успешное выполнение запроса|
|401|Некорректные данные для аутентификации|
|403|Не хватает прав|
|404|Запрашиваемый ресурс не найден|
|500|Внутрення или системная ошибка|

### Опсиание API

Описание API доступно по следующей ссылке: [https://app.swaggerhub.com/apis/indeec05/Booking_system/1.0.0](https://app.swaggerhub.com/apis/indeec05/Booking_system/1.0.0)