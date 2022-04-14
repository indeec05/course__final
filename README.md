![](src/Screenshot_124.png)

## Глоссарий
## Оглавление

## Бизнес цели

## Варианты использования

### Верхнеуровневая схема

![README](https://plantuml.w1.money/png/ZPBDIiD058NtynINxhFG_Yoab8hFu0E4cbQnhP8V4ApGMj2De6wjYABh4bgZeJ_fAvnv8q-ciKeMOc18Sk_vpZqpITtpRTSFEcsbTXl-YIi5Z7KVCTuHwsj4Ue0P4aI2EGjNI0fYUnAqD-etQZ__qZP_j8-8iEHwnmVLVTFks5sxvRXAdTgDOpu9NWWFz2Lr2uHoheHNu3aDstFeyOeLyuMOS4Zg5dCU2v514jDQSYqG6_lzlQsSmHDMH4EgGz53Pfxh8QQPU3idVkQCwJfFQirDnVfMCCOe0uevu9wo98rbxXEJnaGqyTA3uHc56LpwnzxIMOA9O8I732ldi3lCQ1uJsqnbt9lVCIlgGgcWBLRDd0YNL7kMUzGwzArqsx8ZrQfpvZlTWrgDxQ9OLc-jLKrYXYifbNsjh53ElLT8Lhx9eb9rsl7N-W80 "README")

[Исходник](src/use-case-general.wsd)

### [Управление ресторанами и оплата услуг](structure/uc/client-profile.md)
## Управление ЮЛ в ЛК

```plantuml
@startuml

Actor "Менеджер" as manager
package "Система" {
    usecase "Просмотр списка ЮЛ" as UC1
    usecase "Просмотр информации о ЮЛ" as UC2
    usecase "Редактирование информации о ЮЛ" as UC3
    usecase "Смена активности ЮЛ" as UC4
}

manager -down-> UC1
UC2 -up-|> UC1
UC3 -up-|> UC2
UC4 -up-|> UC3

@enduml
```

## Бронирование столика


```plantuml
@startuml

actor "ФЛ" as fl
package "Система" {
    usecase "Просмотр списка\nресторанов" as UC1
    usecase "Просмотр информации\nо ресторане" as UC2
    usecase "Просмотр списка\nстоликов" as UC3
    usecase "Бронирование\nстолика" as UC4
    usecase "Оставить отзыв" as UC5
    usecase "Просмотр\nрекомендаций" as UC6
    usecase "Смена пароля" as UC7
    usecase "Авторизация" as UC8
    usecase "Регистрация" as UC9

    usecase "Восстановление пароля" as UC10
    usecase "Просмотр профиля" as UC11
    usecase "Поиск столика" as UC12
    usecase "Просмотр списка\nбронирований" as UC13
    usecase "Просмотр активных\nбронирований" as UC14
    usecase "Просмотр брони" as UC15
    usecase "Отмена брони" as UC16
    usecase "Редактирование\nданных профиля" as UC17
}

fl -- UC4
fl -- UC12
fl -- UC14
fl -- UC17

' Авторизация
UC8 <.up. UC12 : <<include>>
UC8 <.up. UC14 : <<include>>
UC8 <.up. UC17 : <<include>>
UC8 <.up. UC4 : <<include>>

UC9 -up-|> UC8 : <<extend>>
UC6 -up-|> UC1 : <<extend>>
UC2 -up-|> UC1
UC3 -up-|> UC4
UC2 -up-|> UC4
UC7 -up-|> UC17 : <<extend>>
UC1 -up-|> UC12
UC10 -up-|> UC8 : <<extend>>
UC14 --|> UC13 : <<extend>>
UC15 -up-|> UC13
UC15 -up-|> UC14
UC5 -up-|> UC15 : <<extend>>
UC16 -up-|> UC15
UC11 -up-|> UC17

@enduml
```

## Модель предметной области

```plantuml
@startuml

Class "Клиент" as client {
    Название
    ИНН
    Состояние
    Наименование
    Тип бизнеса
}

class "Представитель\nклиента" as member {
    ФИО
    Телефон
    Email
    Пароль
}

class "Тариф" as tariff {
    Наименование
    Мин оборот
    Макс оборот
    Описание
    Комиссия
    Стандартный: boolean
}

class "Состояния клиента" as states <<Enumeration>> {
    Новый
    Зарегистрирован
    Активирован
}

class "Типы бизнеса" as business_types <<Enumeration>> {
    Ресторан
}

class "Ресторан" as restaurant {
    Название
    Тип кухни
    Адрес
    Галерея фото
    Расположение: \{
        Долгота,
        Широта
    \}
}

class "Подключение к\nсистеме ресторана" as connection {

}

class "Рабочий день" as working_day {
    Время начала
    Время окончания
    День недели
}

class "Столик" as table {
    Количество мест
    Статус
    Описание
}

class "Авторизованный\nклиент" as fl {
    Имя
    Телефон
    Email
    Пароль
}

class "Бронирование" as booking {
    Количество гостей
    Дата
    Время
    Статус
    Столик
}

class "Статусы бронирования" as booking_states {
    Новое
    Подтверждено
    Отменено
    Успех
    Неуспех
}

class "Сотрудник плтаформы" as employee {
    Email
    Пароль
}

member "0..1" --* client
client "0..*" --> "1" tariff
client "0..*" --> "1" states
client "0..*" --> "1" business_types
restaurant "0..*" --* client
connection "0..*" --* restaurant
working_day "0..7" --* restaurant
table "0..*" --* restaurant

booking "0..1" --> "1" booking_states
booking "0..*" --* fl
booking "0..*" -right-* table

employee "0..*" --> "0..*" client
employee "0..*" --> "0..*" tariff

@enduml
```

## Информационная модель

### Context

![](src/unnamed.png)

### Containers

![](src/unnamed2.png)

| №П/П | Тип             | Наименование              | Технологии               | Описание                                               |
| ---- | --------------- | ------------------------- | ------------------------ | ------------------------------------------------------ |
| 1    | Software System | BookingSystem             | Java, Spring Boot        | Сервис, реализующий бизнес логику.                     |
| 2    | Container       | BookingWebApp             | React, JavaScript        | Веб-интерфейс для клиентов и сотрудников. SPA          |
| 3    | Container       | BookingAndroidApplication | Kotlin                   | Мобильное приложение для клиентов, Android.            |
| 4    | Container       | BookingIOSApplication     | Swift                    | Мобильное приложение для клиентов, iOS.                |
| 5    | Container       | Booking database          | PostgreSQL               | Основная БД проекта.                                   |
| 6    | Software System | 1C                        | Платформа 1С:Предприятие | Хранение клиентов, автоматизация учета                 |
| 7    | Software System | Wallet One                | REST API                 | Платежная система для реализации функционала оплаты    |
| 8    | Software System | Email Service             | SMTP                     | Отправка уведомлений клиентам                          |
| 9    | Software System | R-Keeper                  | REST API                 | Информация о столиках, расписание, бронирование        |
| 10   | Software System | Google Maps               | REST API                 | Просмотр ресторанов на карте в интерфейсе пользователя |
| 11   | Software System | Google Analitycs          | REST API                 | Формирование аналитики по посещениям                   |
| 12   | Software System | Контур.Фокус              | REST API                 | Проверка контрагентов-юридических лиц                  |
| 13   | Container       | Keycloak                  | Java, Oauth2             | Сервис авторизации и аутотентификации                  |
