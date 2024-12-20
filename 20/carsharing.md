# Содержание
1. [Введение](#1-введение)
   - [Цели](#цели)
   - [Границы применения](#границы-применения)
   - [Термины и аббревиатуры](#термины-и-аббревиатуры)
   - [Ссылки](#ссылки)
   - [Краткий обзор](#краткий-обзор)
2. [Общее описание](#2-общее-описание)
   - [Описание изделия](#описание-изделия)
   - [Функции изделия](#функции-изделия)
   - [Характеристики пользователей](#характеристики-пользователей)
   - [Ограничения](#ограничения)
   - [Предположения и зависимости](#предположения-и-зависимости)
3. [Детальные требования](#3-детальные-требования)
   - [Функциональные требования](#функциональные-требования)
   - [Надежность](#надежность)
   - [Производительность](#производительность)
   - [Ремонтопригодность](#ремонтопригодность)
   - [Ограничения проекта](#ограничения-проекта)
   - [Требования к пользовательской документации](#требования-к-пользовательской-документации)
   - [Используемые компоненты](#используемые-компоненты)
   - [Интерфейсы](#интерфейсы)
   - [Требования лицензирования](#требования-лицензирования)
   - [Применимые стандарты](#применимые-стандарты)
4. [Индекс](#индекс)

---

# История изменений
| Дата       | Версия | Описание         | Авторы           |
|------------|--------|------------------|------------------|
| 2024-11-21 | 0.1    | Написаны 1-3 пункты |Владимирова Юлия <br/> Страхов Андрей <br/> Чернова Наталья|   
---


# 1. Введение
Данный документ предназначен для описания требований к программному обеспечению для системы контроля проката легковых автомобилей.

## Цели
Цель создания документа заключается в чётком определении требований и спецификации к программному обеспечению, а также описание его интерфейса и ограничений. 

## Границы применения
Данный документ распространяется на спецификацию приложения для проката легковых автомобилей.
Приложение осуществляет первичную коммуникацию с пользователем услуги аренды автомобиля, а именно предложение и заключение аренды, расчёт стоимости услуги и осуществление её оплаты по окончании пользования услугой пользователем. Также приложение осуществляет частичный контроль за исполнением условий договора аренды со стороны арендатора, частичный контроль включает в себя время и область использования арендованного транспорта, а также следование ограничениям скорости. Приложение отслеживает местонахождение и статус всех зарегистрированных в приложении автомобилей.    

## Термины и аббревиатуры
|||
|-------------|-------------|
|Автомобиль | легковая машина, зарегистрированная в собственность компании, имеющая QR код на корпусе, оснащённая системой блокировки дверей, способная выйти в сотовую сеть, принять и отправить сообщение, в котором сообщает своё текущее местоположение.|
|Штраф                    | сумма, представляющая собой надбавку к итоговой стоимости проката за определённые лёгкие и средние нарушения договора пользования услугой, в т.ч. превышение скорости.|
|ПО                       | программное обеспечение - программа или множество программ, используемых для управления компьютером.|
|API                      | программный интерфейс, с помощью которого приложения, веб-сервисы и программы обмениваются информацией |
|QR-код                   |тип штрих-кода, который хранит информацию в виде набора квадратов и считывается камерой смартфона или специальным сканером.|

## Ссылки
| Обозначение | Расшифровка           |
|-------------|-----------------------|
| [IEEE-830]  | IEEE Std 830-1998     |

## Краткий обзор
Структура документа:
1. Раздел 1 содержит введение, краткий обзор программного обеспечения и некоторые необходимые данные для лучшего понимания документа.
2. Раздел 2 содержит более полное описание продукта.
3. Раздел 3 содержит требования к продукту, описание ожидаемых от него функций и интерфейса в более точном виде, достаточном для понимания квалифицированным работником.
4. Раздел 4 содержит индекс приложения, определения, не указанные в разделе 1, а также другую дополнительную информацию.

---

# 2. Общее описание

## Описание изделия
- **Интерфейсы системы**: 
  - API для взаимодействия с устройствами автомобилей.
  - API для обработки бронирования и расчёта стоимости аренды.
  - API для управления пользовательскими данными.
  - Геолокационный сервис для работы с картой и ограничениями скорости.
- **Интерфейсы пользователя**: 
  - Интерфейс для бронирования автомобиля, просмотра карт и получения уведомлений.
  - Интерфейс для загрузки фотографий автомобиля перед и после аренды.
  - Интерфейс администратора для мониторинга состояния автомобилей и управления запросами.
- **Интерфейсы аппаратных средств ЭВМ**:не требуется специфическое оборудование, работает на планшетах или мобильных устройствах, с камерой, способное считывать QR-код, с доступом к интернету.
- **Интерфейсы программного обеспечения**: Приложение будет интегрироваться с различными программными системами, включая:
	- Платежные системы для обработки финансовых транзакций.
	- Системы геолокации для визуализации местоположения разрешенных мест стоянки автомобилей, зон с ограничениями скорости.
- **Интерфейсы коммуникаций**: В приложении будут использоваться следующие интерфейсы для связи:
	- Уведомления из самого приложения для осведомления о выгодных предложениях, о нарушениях с их последствиями, в случае нарушения условий договора.
	- Электронная почта и сотовая связь для подтверждения действий пользователей или при необходимости оказания дополнительной технической поддержки.
	- Протоколы для передачи данных о местоположении автомобилей.
- **Ограничения памяти**: Ограничения памяти минимальные.
- **Действия**: Приложение будет поддерживать такие действия как:
	- Регистрация и аутентификация.
	- Поиск доступных мест стоянки автомобилей на карте и зон с ограничениями скорости.
	- Аренда автомобилей.
	  - Фотографирование автомобиля.
	- Получение уведомлений о статусе аренды и инструкциях по возврату.
	- Оплата аренды через интегрированные платёжные системы.
	- Управление учётной записью.

## Функции изделия
- **Работа с автомобилем**:
  - Бронирование ближайшего доступного автомобиля.
  - Фотографирование автомобиля перед началом и завершением аренды.
  - Подсчёт стоимости аренды и штрафов за нарушения.
- **Работа с системой**:
  - Заведение базы данных о пользователях, автомобилях и поездках.
  - Отслеживание скорости и местоположения автомобиля.
  - Генерация штрафов за превышение скорости в обозначенных зонах.
 
- **Работа в системе**:
	- отслеживание, где находится автомобиль
	- отправка запросов на блокировку или разблокировку дверей.


## Характеристики пользователей
Система ориентирована на два вида пользователей:
1. Техники по обслуживанию - те, кто поддерживает рабочее состояние автомобиля и его модуля, а также следит за его правильным местоположением стоянки.
2. Системный администратор - обслуживает систему, следит за её корректной работой и функционированием системы. Обладает навыками системного администрирования, имеет техническое образование.
3. Пользователи старше 18 лет, имеющие возможность безналичной оплаты, зарегистрированные в офсие компании.

## Ограничения
- Заправка автомобилей осуществляется вне системы.
- Приложение не позволяет выбрать конкретный автомобиль, бронируется ближайший доступный.
- Пользователи должны быть зарегистрированы заранее.


## Предположения и зависимости
- Карта зон ограничения скорости всегда актуальна и предоставляется компанией.
- Данные с устройств GPS передаются корректно и регулярно.
---

# 3. Детальные требования

## Функциональные требования

**Работа с системой**
|Идентификатор|	Наименование	|Содержание|	Важность|
|-------|-----------------------------|-----------------------------------------------------------------------------------------------|---------------|
| ID01   | Бронирование автомобиля     | Пользователь может забронировать ближайший доступный автомобиль.                              | Важно         |
| ID02   | Фотографирование автомобиля | Перед началом и завершением аренды пользователь должен загрузить фотографии автомобиля.       | Важно         |
| ID03   | Расчёт стоимости            | Система рассчитывает стоимость аренды на основании времени использования.                     | Важно         |
| ID04   | Штрафы за превышение        | Система автоматически начисляет штрафы за превышение скорости на основе передаваемых данных.  | Важно         |
| ID05   | Отображение зон             | Приложение отображает зоны с ограничениями скорости на карте.                                 | Средней важности |
| ID06   | Уведомления                 | Система отправляет уведомления о завершении бронирования, начислении штрафов и рекламных акций.| Средней важности |
| ID07   | Завершение аренды           | Пользователь завершает аренду через приложение.  

**Работа с пользователем**
|Идентификатор|Наименование	|Содержание|	Важность|
|-------------|-----------------|----------|------------|
|ID09	|Сканирование QR-кода|	Сканирование QR-кода для осуществления поездки на выбранном автомобиле.|	Важно|
|ID10|	Информация о поездке|	Отображение информации о текущей поездке.|	Средней важности|
|ID11	|Информация о стоянках|	Отображение карты с текущим местоположением и ближайшими местами стоянки автомобиле.|	Средней важности|
|ID12	|Информация об автомобиле |	Отображение информации об арендованном автомобиле.|	Средней важности|
|ID13	|Отправка уведомлений	|Отправка уведомлений, отображающих текущее состояние поездки (длительность и текущую стоимость), а также рекламные предложение.|	Средней важности|
|ID14	|Обучение	|Обучение правилам пользования услугой.|	Важно|
|ID15	|Запрос информации	|Отправка запроса на сервер на получение информации об автомобиле|	Средней важности|
|ID16	|Работа с платёжной системой|	Возможность оплаты поездки с помощью привязанной карты|	Важно|



## Надежность
- **Доступность**: xx.xx%
- **MTBF**: подлежит уточнению.
- **MTTR**: подлежит уточнению.
- **Точность**: подлежит уточнению.
- **Макс. количество ошибок**: подлежит уточнению.

## Производительность
- **Время отклика**: подлежит выяснению.
- **Пропускная способность**: подлежит выяснению.
- **Утилизация ресурсов**: подлежит выяснению.

## Ремонтопригодность
[Требования к ремонтопригодности.]

## Ограничения проекта
[Ограничения по проекту.]

## Требования к пользовательской документации
[Требования к документации.]

## Используемые компоненты
[Перечень приобретаемых компонентов.]

## Интерфейсы
- **Интерфейс пользователя**: подлежит выяснению.
- **Аппаратные интерфейсы**: подлежат выяснению.
- **Программные интерфейсы**: подлежат выяснению.
- **Интерфейсы коммуникаций**: подлежат выяснению.

## Требования лицензирования
[Требования по лицензированию.]

## Применимые стандарты
[Применимые стандарты.]

---

# Индекс
[Индекс.]
