# VK-Highload-YandexEda
## 1. Тема и целевая аудитория
### Тема
Яндекс Еда — сервис заказа быстрой доставки еды из ресторанов и продуктов из магазинов.



### Целевая аудитория 
По официальной статистике 71% пользователей сервиса - это молодежь до 35 лет. Также в целевую аудиторию входят люди, не имеющие достаточно свободного времени, чтобы готовить самостоятельно, семьи и жители крупных городов. [^1]

### Аналоги

- Сбермаркет
- Самокат
- ВкусВилл
- Delivery club

### Число активных пользователей
Каждый месяц Яндекс Едой пользуется 15 млн пользователей в более чем 400 городах. Данная статистика актуальна на 2023 год. Ежегодный прирост количества пользователей по официальным данным составляет 42%. Учитывая данный прирост, можно сделать вывод, что количество активных пользователей в месяц продолжает расти и превысило 20 млн.[^2]

### Веб-трафик по странам
![Трафик по странам](assets/geograpic.png)
<em>Данные согласно сайту SimilarWeb</em>[^3]

### Веб-трафик по демографическим показателям
![Трафик по демографическим показателям](assets/demograpic.png)
- 62,2% пользователей - мужчины
- 37,8% пользователей - женщины
- Основной процент аудитори приходится на молодых людей 25-34 лет (29,58%).
  
<em>Данные согласно сайту SimilarWeb</em>[^3]

### Ключевой функционал

- Просмотр рейтинга с ресторана 
- Регистрация и авторизация пользователей
- Поиск и выбор ресторанов
- Написание и чтение отзыва с оценкой
- Меню ресторанов
- Оформление заказа
- Онлайн-оплата
- Отслеживание заказа
- Уведомления
- Регистрация ресторана


### Ключевые продуктовые решения

- Интеграция с экосистемой Яндекс
- Разбиение зоны доставки на зоны с точками питания
- Подписка «Яндекс Плюс»

## 2. Расчет нагрузки
### Продуктовые метрики

#### Основные метрики
- **MAU (monthly active users)** - 15 000 000 пользователей[^2]
- **DAU (daily active users)** - 3 000 000 пользователей (данные посчитаны с помощью среднего значения Sticky Factor(отношение DAU к MAU) = 20%)

#### Средний размер хранилища пользователя

Для расчета хранилища необходимо определить вес ключевых данных. Возьмем среднюю заполненность данных, и при учете кодировки UTF-8 (от 1 до 4 байт, возьму 3 байта как среднее) получим:

**Профиль пользователя**

| Параметр                             | Вес                          |
| ------------------------------------ | ---------------------------- |
| Имя пользователя                     | 128 символов (3\*128=384 Б)  |
| Email                                | 255 символов (3\*255=765 Б)  |
| Адрес доставки                       | 512 символов (3\*512=1536 Б) |
| История заказов (среднее 50 заказов) | 50 \* 2 КБ = 100 КБ          |
| Уведомления (среднее 30)             | 30 \* 512 Б = 15 КБ          |
| **Итого**                            | **\~118 КБ**                 |

**Один заказ**

| Параметр                                     | Вес                |
| -------------------------------------------- | ------------------ |
| ID заказа                                    | 8 Б                |
| Дата и время заказа                          | 8 Б                |
| Список блюд (среднее 5 блюд, 100 Б на блюдо) | 5 \* 100 Б = 500 Б |
| Адрес доставки                               | 512 Б              |
| Статус заказа                                | 32 Б               |
| История обновлений статуса (5 записей)       | 5 \* 32 Б = 160 Б  |
| **Итого**                                    | **\~1,2 КБ**       |

Среднее количество заказов в день в сервисе составляет 1 млн заказов/день.[^4]

**Размер хранилища на 1 пользователя**:
- Среднее количество заказов за год: 50
- 50 \* 1,2 КБ = **60 КБ**
- Общий размер профиля + история заказов = **\~180 КБ**

#### Среднее количество действий пользователя в день
- Просмотр рейтинга ресторана: 5 раз в день.
- Поиск ресторанов: 3 раза в день.
- Чтение отзывов: 5 раз в день.
- Написание отзыва: 0.1 раза в день.
- Оформление заказа: 1 раз в день.
- Оплата заказа: 1 раз в день.
- Отслеживание заказа: 3 раза в день.
- Получение уведомлений: 5 раз в день.

#### Итоговая таблица
| Параметр                             | Значение                     |
| ------------------------------------ | ---------------------------- |
| Месячная аудитория                   | 15 млн человек               |
| Дневная аудитория                    | 3 млн человек                |
| Средний размер хранилища пользователя| \~180 КБ                     |
| Количество заказов в день            | 1 млн                        |
| Просмотр рейтинга ресторана          | 5 запросов/день              |
| Поиск ресторанов                     | 3 запросов/день              |
| Чтение отзывов                       | 5 запросов/день              |
| Написание отзыва                     | 0.1 запросов/день            |
| Оформление заказа                    | 0.33 запросов/день           |
| Оплата заказа                        | 0.33 запросов/день           |
| Отслеживание заказа                  | 1 запросов/день              |
| Получение уведомлений                | 5 запросов/день              |

### Технические метрики

#### Данные ресторанов
- Количество ресторанов: 29 000[^5]
- Среднее количество позиций в меню: 73[^6]
- Данные на одну позицию меню:
  - Название блюда: 128 символов (384 Б)
  - Фото блюда: ~100 КБ
  - Описание блюда: 512 символов (1,5 КБ)
  - Цена: 8 Б
- Общий объем хранения данных ресторанов: 29 000 * 73 * (384 Б + 100 КБ + 1,5 КБ + 8 Б) = 211 ГБ

#### Размер хранения в разбивке по типам данных

| Тип данных                                      | Размер                       |
| ----------------------------------------------- | ---------------------------- |
| Данные пользователей (15 млн \* 180 КБ)         | **2,5 ТБ**                   |
| Данные заказов (50 заказов \* 15 млн \* 1,2 КБ) | **900 ГБ**                   |
| Отзывы (среднее 1 отзыв на пользователя)        | **15 млн \* 512 Б = 7,5 ГБ** |
| Данные ресторанов (29 000 \* 73 позиций)        | **211 ГБ**                   |


#### Сетевой трафик

Посчитаем сетевой трафик для основных действий пользователя:

1. **Просмотр рейтинга ресторана**:
   - 5 запросов в день \* 1 КБ = **5 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 5 КБ = **15 ГБ/день**.

2. **Поиск ресторанов**:
   - 3 запроса в день \* 10 КБ = **30 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 30 КБ = **90 ГБ/день**.

3. **Чтение отзывов**:
   - 5 запросов в день \* 10 КБ = **50 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 50 КБ = **150 ГБ/день**.

4. **Написание отзыва**:
   - 0.1 запроса в день \* 1 КБ = **0.1 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 0.1 КБ = **0.3 ГБ/день**.

5. **Оформление заказа**:
   - 0.33 запроса в день \* 5 КБ = **1.65 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 1.65 КБ = **4.95 ГБ/день**.

6. **Оплата заказа**:
   - 0.33 запроса в день \* 2 КБ = **0.66 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 0.66 КБ = **1.98 ГБ/день**.

7. **Отслеживание заказа**:
   - 1 запрос в день \* 1 КБ = **1 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 1 КБ = **3 ГБ/день**.

8. **Получение уведомлений**:
   - 5 запросов в день \* 512 Б = **2,5 КБ** на пользователя.
   - Общий объем: 3 000 000 \* 2,5 КБ = **7,5 ГБ/день**.

**Потребление трафика**:
Возьмем, что пиковое значение превышает среднее в 2 раза.

| Тип трафика                     | Данные (ГБ/день) | Пиковое в Гбит/c | Суммарный суточный (ГБ/день) |
| ------------------------------- | ---------------- | ---------------- | ---------------------------- |
| Просмотр рейтинга ресторана     | 15               | 0.35             | 30                           |
| Поиск ресторанов                | 90               | 2.08             | 180                          |
| Чтение отзывов                  | 150              | 3.47             | 300                          |
| Написание отзыва                | 0.3              | 0.007            | 0.6                          |
| Оформление заказа               | 4.95             | 0.11             | 9.9                          |
| Оплата заказа                   | 1.98             | 0.046            | 3.96                         |
| Отслеживание заказа             | 3                | 0.07             | 6                            |
| Получение уведомлений           | 7.5              | 0.17             | 15                           |
| **Итого**                       | **272,73 ГБ**    | **6,3 Гбит/c**   | **545,46 ГБ**                |


#### RPS (Requests Per Second)

Возьмем, что пиковое значение превышает среднее в 2 раза.

| Действие                    | RPS (средний)                       | RPS (пиковый) |
| --------------------------- | ----------------------------------- | ------------- |
| Просмотр рейтинга ресторана | 3 000 000 \* 5 / 86 400 = **173**   | **346**       |
| Поиск ресторанов            | 3 000 000 \* 3 / 86 400 = **104**   | **208**       |
| Чтение отзывов              | 3 000 000 \* 5 / 86 400 = **173**   | **346**       |
| Написание отзыва            | 3 000 000 \* 0.1 / 86 400 = **3,5** | **7**         |
| Оформление заказа           | 3 000 000 \* 0.33 / 86 400 = **11,5** | **23**       |
| Оплата заказа               | 3 000 000 \* 0.33 / 86 400 = **11,5** | **23**       |
| Отслеживание заказа         | 3 000 000 \* 1 / 86 400 = **34,7**  | **69,4**      |
| Получение уведомлений       | 3 000 000 \* 5 / 86 400 = **173**   | **346**       |
| **Итого**                   | **685,7**                           | **1 371,4**   |

## Список источников

[^1]: [Яндекс Еда и Деливери поделилась статистикой по аудитории и онлайн-заказам](https://m.seonews.ru/events/yandeks-eda-i-deliveri-podelilas-statistikoy-po-auditorii-i-onlayn-zakazam/)
[^2]: [Сервис, который кормит миллионы пользователей](https://dev.go.yandex/services/eda)
[^3]: [Анализ трафика по SimilarWeb](https://pro.similarweb.com/#/digitalsuite/websiteanalysis/overview/website-performance/*/999/28d?webSource=Total&key=eda.yandex.ru)
[^4]: [«Яндекс» впервые раскрыл число заказов в сервисе «Яндекс.Еда»](https://vc.ru/food/55365-yandeks-vpervye-raskryl-chislo-zakazov-v-servise-yandekseda)
[^5]: [Что заказывают в Яндекс Еде?](https://yandex.ru/company/researches/2020/food)
[^6]: [Продающее меню. Способы его создания](https://traktir.ru/publications/14216/#:~:text=От%20концепции%20зависит%20и%20общее%20количество%20блюд.&text=Заведения%20русской%20кухни%20предполагают%20наличие,Больше%20позиций%20–%20не%20значит%20лучше!)

