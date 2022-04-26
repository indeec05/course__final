![](img/Screenshot_124.png)

**TODO**

- [x] БП
- [x] Сваггер - ресурс, он не должен быть в оглавлении. Возможно, в архитектуру
- [x] Закончить описание US для ЛК клиента
- [x] Закончить описание US для ЛК менеджера
- [x] Для UC удобно было бы удобно иметь сквозную нумерацию
- [ ] Вычитать на противоречия и поправить
- [ ] Описать таски по задачам _in progress_
- [ ] Сопроводить пояснениями и аннотациями

## Описание

Данный документ содержит требования к разработке Системы бронирования, представляющей из себя MVP продукта компании А.

На этапе MVP разрабатываемая Система будет включать в себя следующие разделы:

* ЛК Клиента;
* ЛК Посетителя;
* ЛК Менеджера.

Эти три раздела, укрупненно, будут предоставлять следующий функционал:

* возможность регистрации Клиентов и Посетителей;
* добавление и управление ресторанами;
* бронирование столиков.

Большее представление о системе можно получить из документа об [образе и границах Системы](structure/requirements/concepts-and-borders.md).

## Оглавление

* [Глоссарий](#глоссарий)
* [Требования к Системе](#требования-к-системе)
  * [Нефункциональные требования](#нефункциональные-требованияstructurerequirementsnon-functionalmd)
  * [Бизнес процессы](#бизнес-процессы)
  * [Роли пользователей системы](#роли-пользователей-системы)
  * [Функциональные требования к частям Системы](#функциональные-требования-к-частям-системы)
* [Модель предметной области](#модель-предметной-области)
* [Архитектура системы](#архитектура-системыstructurearchc4-containersmd)

## Глоссарий

**Личный кабинет (ЛК)** - раздел сайта, доступный только авторизированным пользователям и клиентам с соответствующей ролью.

**Клиент** - юридическое лицо, регистрирующееся в Системе с целью предоставления услуг бронирования.

**Пользователь** - физическое лицо, взаимодействующее с Системой и использующее ее сервисы.

**Посетитель** - физическое лицо, решившее воспользоваться услугами бронирования, предоставляемыми Системой.

**Компания** - разработчики и владелец Системы.

**Учетная запись (УЗ)** - набор свойств, однозначно идентифицирующих пользователя в Системе.

**Приложение** - мобильное приложение или сайт, через который пользователи взаимодействуют с Системой.

**Сайт** - часть Системы, набор логически связанных веб-страниц, через которые Пользователи взаимодействуют с Системой.

**Мобильное приложение** - программное обеспечение, предназначенное для работы на смартфоне или планшете, через которое Пользователи взаимодействуют с Системой.

**MVP, минимальный жизнеспособный продукт** - версия продукта, позволяющая команде с минимальными затратами собрать максимум информации о клиентах и обратной связи от них.

## Требования к Системе

### Роли пользователей Системы

|Название роли|Описание|
|-------------|--------|
|Представитель клиента|Сотрудник клиента, взаимодействующий с Системой|
|Посетитель|Пользователь, использующий Систему для бронирования ресурсов Клиентов|
|Менеджер|Сотрудник Компании, осуществляющий набор взаимодействий с Клиентом от лица Компании|

### [Нефункциональные требования](structure/requirements/non-functional.md)

В разделе перечислены основные нефункциональные требования.

### Бизнес-процессы

Следующий раздел содержит описание бизнес процессов в формате EPC. Эти процессы бли выделены в связи с тем, что они, во-первых, включают в себя участие сотрудников подразделений компании, не являющихся участниками Системы, а, во-вторых, нуждаются в детализации для дальнейшего проектирования.

* [регистрацию ЮЛ](structure/requirements/client-registration.md)
* [БП оплаты тарифа](structure/requirements/renewal-bp.md)

### Функциональные требования к частям Системы

Ниже перечислены функциональные требования к Системе, разделенные для удобства работы по основным интерфейсам

* [ЛК Клиента](structure/uc/client-profile.md)
* [ЛК Менеджера](structure/uc/manager-profile.md)
* [ЛК Посетителя](structure/uc/user-profile.md)
* [Регистрация ЮЛ](structure/uc/client-registration.md)

## [Модель предметной области](structure/erd/erd.md)

## [Архитектура системы](structure/arch/c4-containers.md)

## [Задачи](structure/tasks/tasks.md)
