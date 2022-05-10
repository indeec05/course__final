## Модель предметной области

![erd](https://plantuml.w1.money/png/ZLRBRXD95DttLvIyH1Z1QYI4ef465eWTqkmYHKweW9LsEt8xGX4WsKuY5a6JUGGHHH08i63PSTB4iTtEBrJz4UVUgkgkzWCcKkpkkkzpxptbt-DshTNUQeH1y4TOYsDHKSTgf0OgLPdkLKGj5cjXNKPjyI8G-5CVLA8kLH-V6McPmoCSVp2FfsgYkxg7pmDVWym6QankrMJQ_3CUhuKwmzSbpbFTLKdkJPqZdmH7C1MwA_GEdaViP80OOpKGU3dJ7VWyGzYU6gh1SgIkuQS3VNN1mJAzh_VkYjLcCvIro7X_1yaGXYcKHvmQjDILi7ccCFrENe9NGR1cqVd8-XTSOy8vzF0-qcyGSbWWfnB6hY4RgxBbiFiAe4vSoIc5rBl8FVFzVqQj7NZTPNiqfxw-xcE_4CJtUCmO2e3G8I3SEHNPdICvGTa3mjftSmozCHr307nBleUGeKBzcbg46ljg8aopkN0IzwU2_d-JKmOqetQXRptJYg9XW4X6MmqWD3LX-a3C0HvZtPQnk7Vl0OnagzQkDwEbfG98X2N_-HnmLy-vxXxZtt486vM_KKuFCVebKP4KZx3UdnfYJcLrAwv7CevNsjkRYrFwP06Qy22NHc9An4vR4XLkjMg_M4oxMKCipHwTks8kg5xTDQ__mOPcaOuE18qa1NDfqUfTSxicj0t6-rsnRCAoqY6BpzakkLcSVpDWqIaVBh_YhuVtXGbVrAGIeVhYSNL3oatPciRLAu2BtwYtrvx9o0BwmXLr2Tq4xUjY7X8tkc_HQ6eOw41TbKN7lC13mYqN-9iEgmiQBVqNZQyf7AaiHxmQNLvyBEESOWnlDgD8hb6NNOeZPhE1cwcFF7OJ8W_7TYaxnP8G2oLvcqh3O6ZkDVnS4RdHrB_XWC-RhOrwz7JbIMtRHVoNvtfCEuAqO4ITJcPa4rx4ZELPiVQ7nhcmN4YCDV1pEItssBBLQYXTwECvcqzmqOktyUZNZXl4kOHqf0xBZ657vL4-Abx3w9gWFNMap6cjXowd8oht5mJy3_Say_USaZ6ht6mImZyjyTpIK-hOvP2Ad05z0GGUf4NvVBlDv4IDAmFX2B9moemqtzWlQCNIfK-F-4_Td68Hk3pYYEzcvXn1d43Whilyy0jpHghtdB-KRsrpv0yGaGFOVWS-2UMXe9kOqz_bRHhhVSvJDZR3vhQauPhQK3GPYyzrbPh-PvpVkmyQjNguOEK-sHTujNTrvVQjMtSgebgzON_v1FO740bka619LA1WhkO5GeFd0c7vGWWyAiyLyzZpXCPBYGG3Zsmy9uLru9C3QVmses6sTxvru2O_HyUMKfgVafPriXxEdBRgJv-ruO03OcfTR_q2pQC5uISQjWkkUTNgooLkVO2bBrvo1_dH3m00 "erd")

[Исходник](../../src/erd.wsd)

### Опсиание свойств сущностей

#### Клиент

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Название                                   | string  | Да | Наименование клиента в Системе                       |
| ИНН                                        | string  | Да | ИНН клиента                                          |
| Состояние                                  | enum    | Да | Состояние клиента из перечня                         |
| Наименование                               | string  | Да | Полное наименование клиента                          |
| Тип бизнеса                                | string  | Да | Тип бизнеса из перечня                               |
| Согласен с условиями обработки перс данных | boolean | Да | Согласен ли клиент с политикой обработки перс данных |
| Закрепленный менеджер                      | uuid    |    | Закрепленный за клиентом менеджер                    |

#### Представитель Клиента

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| ФИО     | string | Да | ФИО представителя Клиента     |
| Телефон | string | Да | Телефон представителя Клиента |

#### Тариф

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Наименование             | string  | Да | Наименование тарифа в Системе                                           |
| Мин оборот               | integer |    | Минимальный оборот, к которому применим тариф, коп                      |
| Макс оборот              | integer |    | Максимальный оборот, к которому применим тариф, коп                     |
| Описание                 | string  |    | Описание тарифа                                                         |
| Комиссия                 | integer | Да | Размер комиссии, взимаемый за использование Системы, коп                |
| Мин количество столиков  | integer |    | Минимальное количество столиков, к котором может быть применим тариф    |
| Макс количество столиков | integer |    | Максимальное количество столиков, к котором может быть применим тариф   |
| Стандартный              | boolean | Да | Флаг, показывающий, будет ли тариф отображаться на форме выбора тарифов |

#### Ресторан

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Название                | string | Да | Название ресторана                             |
| Тип кухни               | enum   | Да | Тип кухни                                      |
| Адрес                   | string | Да | Адрес ресторана                                |
| Галерея фото            | array  |    | Массив с изображениями ресторана               |
| Долгота                 | double |    | Долгота расположения ресторана                 |
| Широта                  | double |    | Широта расположения ресторана                  |
| ID ресторана в R-keeper | string |    | Идентификатор ресторана в справочнике R-Keeper |

#### Соединение

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Логин         | string | Да | Логин соединения         |
| Пароль        | string | Да | Пароль соединения        |
| Сетевой адрес | string | Да | Сетевой адрес соединения |

#### Рабочий день

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Время начала    | time | Да | Время начала рабочего дня ресторана    |
| Время окончания | time | Да | Время окончания рабочего дня ресторана |
| День недели     | enum | Да | День недели                            |

#### Столик

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Количество мест       | integer |    | Количество мест за столиком        |
| Статус                | enum    | Да | Статус столика из перечня статусов |
| Описание              | string  |    | Описание столики                   |
| ИД столика в R-Keeper | string  | Да | ИД столика в R-Keeper              |

#### Посетитель

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Имя     | string | Да | Имя посетителя     |
| Телефон | string | Да | Телефон посетителя |

#### Бронирование

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Количество гостей          | integer |    | Количество гостей в бронировании           |
| Дата                       | date    | Да | Дата бронирования                          |
| Время                      | time    | Да | Время бронирования                         |
| Статус                     | enum    | Да | Статус бронирования                        |
| Столик                     | uuid    | Да | Идентификатор столика, который бронируется |
| ИД бронирования в R-Keeper | string  | Да | ИД бронирования в R-Keeper                 |

#### Пользователь

| Название свойства | Тип | Обязательность | Описание | 
| ----------------- | --- | -------------- | -------- |
| Email  | string | Да | Email пользователя                 |
| Пароль | string | Да | Пароль пользователя                |
| Роль   | uuid   | Да | Роль пользователя из перечня ролей |

## Диаграммы состояний

### Диаграмма состояний бронирования

![](https://plantuml.w1.money/png/bP7D3S8m38NlJ94pWWKui4XX1MQWL4WW8G43y2En05GDXB-mmij6FAT0APIY7ghOVhO_smtgNTLijXKMi8ZvwLfcfieC9pU0OUYAhMefp5sVwXN6lp6sOaDtUhZHJvWSGrFR8u6cPZizUjg5L2mjoRUuV86Mr2--mbULevYaglBocrHdsdpoByndp-8hhlEbp-iXPaosIPXyPdHNTcqNuYo7C3Yy8OsRShR8Yr9YS2oUAgXt2w-oOUcDKmnbq9N7Q3TEUmkQldqCFnK6xKaZczLDbATBYv5qBOGig4P_GFut_wUbQH_8R8dNgdda8tm7)

[Исходник](../../src/booking-state-machine.wsd)

### Диаграмма состояний Клиента

![erd](https://plantuml.w1.money/png/bP4x3i8m44Hxdy8rKYv0WN8Fe4223b90w0CD1KZGKN47AyHWOXAkCBuHOqC1Y8ye_5bxTjv86q_ItZYTZeP2j1jT6KKjYHrgv6w9asnAN5m6ZSBDt1mAEGnF3UjMdGGbB0ohol-nhg3SWYehASpfKdZvNLhVP2YvLtJNaj-AFQ4G3zGGOailJzxJWcpU3HSblkVVOCSlPfOlQ_635o9jGdOJM4zHpXxbm-00xJ82rHkfVGqcFZXw68SXH3n8-XpD5G00 "erd")