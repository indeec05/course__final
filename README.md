![](img/Screenshot_124.png)

## Оглавление

* [Глоссарий](#глоссарий)
* [Бизнес цели](#бизнес-цели) в процессе наполнения
* [Требования к частям системы](#требования-к-частям-системы)
  * [Роли пользователей системы](#роли-пользователей-системы)
  * [ЛК Клиента](#лк-клиентаstructureucclient-profilemd) нет текстовой части
  * [ЛК Менеджера](#лк-менеджераstructureucmanager-profilemd)
  * [ЛК Постетителя](#лк-постетителяstructureucuser-profilemd)
  * [Регистрация ЮЛ](#регистрация-юлstructureucclient-registrationmd)
* [Модель предметной области](#модель-предметной-области)
* [Информационная модель](#информационная-модель)
* [Swagger](https://app.swaggerhub.com/apis/indeec05/Booking_system/1.0.0)

## Глоссарий

**Личный кабинет (ЛК)** - раздел сайта, доступный только авторизированным пользователям и клиетам с соответствующей ролью.

**Клиент** - юридическое лицо, регистрирующееся в Системе с целью предоставления услуг бронирования.

**Пользователь** - физическое лицо, взаимодействующее с Системой и использующее ее сервисы.

**Компания** - разработчки и владелец Системы.

**Учетная запись (УЗ)** - набор свойств, однозначно идентифицирующих пользователя в Системе.

**Приложение** - мобильное приложение или веб-сайт, через который пользователи взаимодействуют с Системой.

**Веб-сайт** - часть Системы, набор логически связанных веб-страниц, через которые Пользователи взаимодействуют с Системой.

**Мобильное приложение** - программное обеспечение, предназначенное для работы на смартфоне или планшете, через которое Пользователи взаимодействуют с Системой.

## Бизнес цели

Раздел пока пуст

## Требования к частям системы

### Роли пользователей Системы

|Название роли|Описание|
|-------------|--------|
|Представитель клиента|Сотрудник клиента, взаимодействующий с Системой|
|Посетитель|Пользователь, использующий Систему для бронирования ресурсов Клиентов|
|Менеджер|Сотрудник Компании, осуществляющий набор взаимодействий с Клиентом от лица Компании|

### [ЛК Клиента](structure/uc/client-profile.md)

### [ЛК Менеджера](structure/uc/manager-profile.md)

### [ЛК Постетителя](structure/uc/user-profile.md)

### [Регистрация ЮЛ](structure/uc/client-registration.md)

## [Модель предметной области](structure/erd/erd.md)

## [Архитектура системы](structure/arch/c4-containers.md)