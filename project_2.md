# Проект №2: Моделирование данных и работа с базой данных интернет-магазина «Накарабине»

## Задача: Разработка логической модели данных

Требуется разработать логическую модель данных на основе спецификации требований, выполнив следующие шаги:

1.  Построить логическую модель данных в нотации Crow’s Foot.
2.  Привести модель данных к третьей нормальной форме (3НФ).
3.  Составить словарь данных, включающий описание всех сущностей и атрибутов модели.

## Процесс работы
Из табличного описание каждого прецедента выделила атрибуты, которые используются в системе. 
![Прецеденты в табличной форме](https://github.com/EVTrukhina/practicum_Y/blob/main/Прецеденты%20в%20табличном%20варианте.png)
<p align="center">Рис 1. Прецеденты в табличной форме</p>

В задании указано следующее: в первой MVP необходимо заменить личный кабинет на активацию по телефону. Это подразумевает следующее:

*   **Отсутствие учетных записей**: Пользователи не создают учетные записи и не проходят регистрацию.
*   **Форма заказа**: В форме оформления заказа обязательно запрашиваются все необходимые данные пользователя.


## Нормализация баз данных

### Нулевая (0НФ) нормальная форма

Сейчас наша модель находится в ненормализованной или нулевой нормальной форме. Относительно сущности «Заказ» выделены все атрибуты, первичный ключ — «Номер заказа».

![Логическая ER-модель](https://github.com/EVTrukhina/practicum_Y/blob/main/0%20НФ.png)

### Первая (1НФ) нормальная форма

Избавляюсь от связи «многие-ко-многим» между сущностями «Заказ» и «Товар» и добавляю промежуточную сущность «Товар в заказе».

![Логическая ER-модель](https://github.com/EVTrukhina/practicum_Y/blob/main/1%20НФ.png)


### Вторая (2НФ) нормальная форма
Поскольку у нас единственная сущность с составным ключом, и количество товара полностью зависит от всего составного ключа, никаких дополнительных преобразований не требуется. Следовательно, таблица уже соответствует 2НФ (второй нормальной форме).
![Логическая ER-модель](https://github.com/EVTrukhina/practicum_Y/blob/main/1%20НФ.png)

### Третья (3НФ) нормальная форма

Модель данных соответствует 2НФ (второй нормальной форме): все столбцы зависят только от первичного ключа целиком, а не от каких-либо других столбцов.
Для приведения модели к 3НФ (третьей нормальной форме) данные о «Категории товара» и «Чеке» выделены в отдельные сущности. Благодаря этому все атрибуты в сущности «Заказ» зависят только от ее первичного ключа.
Составлена логическая модель данных в нотации Мартина, приведенная к третьей нормальной форме.

![Логическая ER-модель](https://github.com/EVTrukhina/practicum_Y/blob/main/Логическая%20ER-модель.png)

<p align="center">Рис 2. Логическая ER-модель в 3НФ веб-приложения «Накарабине»</p>

В сущности «Заказ» целесообразно хранить адрес доставки, чтобы упростить процесс получения необходимой информации для выполнения каждого заказа. Индекс города доставки не подходит в качестве первичного ключа для адреса, так как один и тот же адрес может быть использован для разных заказов. Даже составной ключ (индекс страны и город) не гарантирует уникальность, так как по одному адресу может быть несколько заказов в день.

## Словарь данных
| Элемент данных | Описание | Состав или тип данных | Длина | Значения |
|---|---|---|---|---|
| Заказ | Информация о заказе | Номер заказа<br>+ Дата создания<br>+ Статус заказа<br>+ Сумма<br>+ Почтовый индекс<br>+ Страна доставки<br>+ Город доставки<br>+ Улица доставки<br>+ Дом доставки<br>+ Квартира доставки<br>+ Фамилия<br>+ Имя<br>+ Отчество<br>+ Электронная почта<br>+ Номер телефона<br>+ Товар в заказе {1:50} |  |  |
| Номер заказа | Уникальный идентификатор заказа | Целое и положительное | 10 | Начальное значение – 1.<br>Увеличивается на 1 с каждым последующим заказом |
| Дата создания | Дата, когда был создан заказ | Дата, время, ДД.ММ.ГГГГ ЧЧ:MM |  |  |
| Статус заказа | Состояние заказа | Символьное значение | 10 | создан, в работе, оплачен,<br>ожидает доставки, в пути,<br>доставлен |
| Сумма | Стоимость заказа – это сумма стоимости всех товаров в заказе с учетом скидок и налогов | Числовое значение | 10 | 10 знаков, включая запятую |
| Почтовый индекс | Почтовый индекс доставки | Числовое значение | 6 |  |
| Страна доставки | Страна доставки заказа | Символьное значение | 50 |  |
| Город доставки | Город отправки заказа | Символьное значение | 50 |  |
| Улица доставки | Название улицы | Символьно-числовое значение | 50 |  |
| Дом доставки | Номер дома | Символьно-числовое значение | 10 |  |
| Квартира доставки | Номер квартиры | Числовое значение | 4 |  |
| Имя | Имя клиента, разместившего заказ | Символьное значение | 60 |  |
| Отчество | Отчество клиента, разместившего заказ | Символьное значение | 60 |  |
| Фамилия | Фамилия клиента, разместившего заказ | Символьное значение | 60 |  |
| Электронная почта | Электронная почта клиента, разместившего заказ | Символьно-числовое значение | 100 | Должно содержать символ @ |
| Номер телефона | Телефон клиента, разместившего заказ | Числовое значение | 19 | Заполняется по формату:<br>+7(000)-00-00 |
| Товар | Информация о товарах в заказе | Артикул товара<br>+ Название товара<br>+ Описание товара<br>+ Цена товара<br>+ Фотография<br>+ Наличие |  |  |
| Артикул товара | Бизнес-идентификатор товара | Числовое значение | 12 |  |
| Название товара | Название товара | Символьное значение | 256 |  |
| Описание товара | Описание товара | Символьное значение | 400 |  |
| Цена товара | Стоимость товара | Числовое значение | 10 | Значение в рублях |
| Фотография | Изображение товара | Файл |  | .img |
| Наличие | Состояние товара в отношении доступности | Символьное значение | 10 | В наличие, нет в наличии, в архиве, ожидается, под заказ |
| Категория товара | Информация о категории товара | Код категории<br>+ Название категории<br>+ Описание категории |  |  |
| Код категории | Уникальный ID категории | Числовое значение | 20 |  |
| Название категории | Название категории | Символьное значение | 256 |  |
| Описание категории | Описание категории | Символьное значение | 250 |  |
| Товар в заказе |  | Номер заказа<br>+ Артикул товара<br>+ Количество товара в заказе |  |  |
| Артикул товара | Бизнес-идентификатор товара | Числовое значение | 12 |  |
| Количество товара в заказе | Общее количество товаров в заказе | Целое и положительное число | 3 |  |
| Чек | Документ, подтверждающий факт совершения покупки  | Номер чека<br>+ Способ оплаты<br>+ Статус оплаты<br>+ Дата оплаты |  |  |
| Номер чека | Уникальный идентификатор чека, выданного при оплате заказа. | Целое и положительное | 50 |  |
| Способ оплаты | Способ, которым пользователь оплатил заказ | Символьное значение | 50 |  |
| Статус оплаты | Состояние оплаты за заказ | Символьное значение | 20 | Оплачен, не оплачен, ошибка оплаты|
| Дата оплаты | Дата и время, когда оплачен заказ | Дата, время, ДД.ММ.ГГГГ ЧЧ:MM |  |  |


## Ссылки на документы

*   [Спецификация требований к ПО Накарабине](https://docs.google.com/document/d/107EXPVnw_AmJjyhJLbln0gAJQz-442bz-lB_EVDmZ7Q/edit?usp=sharing)  

[Назад](https://github.com/EVTrukhina/practicum_Y/blob/main/project_1.md) | [Дальше](https://github.com/EVTrukhina/practicum_Y/blob/main/project_3.md)
