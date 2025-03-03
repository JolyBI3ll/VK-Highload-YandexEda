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
- **DAU (daily active users)** - 6 000 000 пользователей (данные посчитаны с помощью среднего значения Sticky Factor(отношение DAU к MAU) = 40%)

#### Средний размер хранилища пользователя

Для расчета хранилища необходимо определить вес ключевых данных. Возьмем среднюю заполненность данных, и при учете кодировки UTF-8 (от 1 до 4 байт, возьму 3 байта как среднее) получим:

**Профиль пользователя**

| Параметр                             | Вес                          |
| ------------------------------------ | ---------------------------- |
| Имя пользователя                     | 128 символов (3\*128=384 Б)  |
| Email                                | 255 символов (3\*255=765 Б)  |
| Адрес доставки                       | 512 символов (3\*512=1536 Б) |
| Аватар                               | 100 КБ                       |
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
- Среднее количество заказов за год: 120
- 120 \* 1,2 КБ = **144 КБ**
- Общий размер профиля + история заказов = **\~262 КБ**

#### Среднее количество действий пользователя в день
- Просмотр рейтинга ресторана: 3 раз в день.
- Поиск ресторанов: 3 раза в день.
- Чтение отзывов: 2.5 раз в день.
- Написание отзыва: 0.05 раза в день.
- Оформление заказа: 0.33 раз в день.
- Оплата заказа: 0.25 раз в день.
- Отслеживание заказа: 1 раза в день.
- Получение уведомлений: 5 раз в день.
- Просмотр меню: 3 раза в день.
- Просмотр ресторана: 3 раза в день
- Регистрация ресторана: 0.002 раза в день

#### Итоговая таблица
| Параметр                             | Значение                     |
| ------------------------------------ | ---------------------------- |
| Месячная аудитория                   | 15 млн человек               |
| Дневная аудитория                    | 3 млн человек                |
| Средний размер хранилища пользователя| \~262 КБ                     |
| Количество заказов в день            | 1 млн                        |
| Просмотр рейтинга ресторана          | 3 запросов/день              |
| Поиск ресторанов                     | 3 запросов/день              |
| Чтение отзывов                       | 2.5 запросов/день            |
| Написание отзыва                     | 0.05 запросов/день           |
| Оформление заказа                    | 0.33 запросов/день           |
| Оплата заказа                        | 0.25 запросов/день           |
| Отслеживание заказа                  | 1 запросов/день              |
| Получение уведомлений                | 5 запросов/день              |
| Просмотр меню                        | 3 запросов/день              |
| Просмотр ресторана                   | 3 запросов/день              |
| Регистрация ресторана                | 0.002 запросов/день          |

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
Чтобы посчитать размер хранения сервиса "Яндекс еда" примерно посчитаем общее количество пользователей сервиса за счет среднего значения Retention Rate. В итоге получаем, что общее колдичество пользователей - 90 000 000 человек.

| Тип данных                                      | Размер                       |
| ----------------------------------------------- | ---------------------------- |
| Данные пользователей (90 млн \* 118 КБ)         | **9.89 ТБ**                   |
| Данные заказов (120 заказов \* 90 млн \* 1,2 КБ)| **12 ТБ**                     |
| Отзывы (среднее 1 отзыв на пользователя)        | **90 млн \* 512 Б = 42.9 ГБ** |
| Данные ресторанов (29 000 \* 73 позиций)        | **211 ГБ**                   |


#### Сетевой трафик

Посчитаем сетевой трафик для основных действий пользователя:

1. **Просмотр рейтинга ресторана**:
   - 3 запросов в день \* 1 КБ = **3 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 3 КБ = **18 ГБ/день**.

2. **Поиск ресторанов**:
   - 3 запроса в день \* 10 КБ = **30 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 30 КБ = **180 ГБ/день**.

3. **Чтение отзывов**:
   - 2.5 запросов в день \* 10 КБ = **25 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 25 КБ = **150 ГБ/день**.

4. **Написание отзыва**:
   - 0.05 запроса в день \* 1 КБ = **0.05 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 0.05 КБ = **0.3 ГБ/день**.

5. **Оформление заказа**:
   - 0.33 запроса в день \* 5 КБ = **1.65 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 1.65 КБ = **9.9 ГБ/день**.

6. **Оплата заказа**:
   - 0.25 запроса в день \* 2 КБ = **0.5 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 0.5 КБ = **3 ГБ/день**.

7. **Отслеживание заказа**:
   - 1 запрос в день \* 1 КБ = **1 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 1 КБ = **6 ГБ/день**.

8. **Получение уведомлений**:
   - 5 запросов в день \* 512 Б = **2,5 КБ** на пользователя.
   - Общий объем: 6 000 000 \* 2,5 КБ = **15 ГБ/день**.

9. **Просмотр меню**:
   - 3 запроса в день \* 15 КБ = 45 КБ на пользователя.
   - Общий объем: 6 000 000 \* 45 КБ = **270 ГБ/день**.

10. **Просмотр ресторана**:
   - 3 запроса в день \* 8 КБ = 24 КБ на пользователя.
   - Общий объем: 6 000 000 \* 24 КБ = **144 ГБ/день**.

11. **Регистрация ресторана**:
    - 0.002 запроса в день \* 20 КБ = 0.04 КБ на пользователя.
    - Общий объем: 6000000 \* 0.04 КБ = **0.24 ГБ/день**.

**Потребление трафика**:
Возьмем, что пиковое значение превышает среднее в 2 раза.

| Тип трафика                     | Данные (ГБ/день) | Пиковое в Мбит/c | Суммарный суточный (ГБ/день) |
| ------------------------------- | ---------------- | ---------------- | ---------------------------- |
| Просмотр рейтинга ресторана     | 18               | 3.41             | 36                           |
| Поиск ресторанов                | 180              | 34.13            | 360                          |
| Чтение отзывов                  | 150              | 28.4             | 300                          |
| Написание отзыва                | 0.3              | 0.05             | 0.6                          |
| Оформление заказа               | 9.9              | 1.88             | 19.8                         |
| Оплата заказа                   | 3.0              | 0.57             | 6.0                          |
| Отслеживание заказа             | 6.0              | 1.13             | 12.0                         |
| Получение уведомлений           | 15.0             | 2.84             | 30.0                         |
| Просмотр меню                   | 270              | 51.2             | 540                          |
| Просмотр ресторана              | 144              | 27.31            | 288                          |
| Регистрация ресторана           | 0.24             | 0.045            | 0.48                         |
| **Итого**                       | **796.44 ГБ**    | **151.2 Мбит/с** | **1 592.88 ГБ**              |


#### RPS (Requests Per Second)

Возьмем, что пиковое значение превышает среднее в 2 раза.

| Действие                    | RPS (средний)                       | RPS (пиковый) |
| --------------------------- | ----------------------------------- | ------------- |
| Просмотр рейтинга ресторана | 208                                 | **416**           |
| Поиск ресторанов            | 208                                 | **416**           |
| Чтение отзывов              | 173                                 | **346**           |
| Написание отзыва            | 3.5                                 | **7**             |
| Оформление заказа           | 23                                  | **46**            |
| Оплата заказа               | 17.4                                | **34.8**          |
| Отслеживание заказа         | 69.4                                | **138.8**         |
| Получение уведомлений       | 347                                 | **694**           |
| Просмотр меню               | 208                                 | **416**           |
| Просмотр ресторана          | 208                                 | **416**           |
| Регистрация ресторана       | 0.14                                | **0.28**          |
| **Итого**                   | **1 465.74**                        | **2 931.48**  |


## 3. Глобальная балансировка нагрузки
Возьмем распределение пользователей по странам [[hypestat]](https://hypestat.com/info/eda.yandex.ru)

![image](assets/by_country.png)

Видим что большая часть пользователей приходится на Россию, далее Азербайджан, Германия, Нидерланды, США. С большой вероятностью пользователи из Германии, Нидерландов и США на самом деле не являются пользователями из ранее названных стран. Скорее всего это пользователи из СНГ, что забыли отключить ВПН. Будем считать что большая часть пользователей приходится на Россию и страны СНГ.

**Расположение дата-центров**:

На основе этих данных целесообразно расположить дата-центры в крупных городах, чтобы обеспечить минимальное время отклика для пользователей и стабильную работу сервиса.

**Россия:** Дата-центры стоит расположить в крупных городах с распределением по регионам страны:
- Москва (европейская часть России)
- Санкт-Петербург (северо-западная часть России)
- Новосибирск (сибирский регион)
- Владивосток (дальний восток)
  
**Беларусь:**
- Использует дата-центры из европейской части России

**Казахстан:**
- Астана (центр страны)

**Узбекистан:**
- Использует дата-центы из Казахстана

**Армения:**
- Использует дата-центы из Казахстана

Получаем такую карту:
![image](assets/DC.png)

### Распределение запросов по ДЦ
| Тип запроса                  | RPS (Москва) | RPS (Санкт-Петербург) | RPS (Новосибирск) | RPS (Владивосток) | RPS (Астана) |
|------------------------------|--------------|-----------------------|-------------------|-------------------|--------------|
| Просмотр рейтинга ресторана  | 62.4         | 62.4                  | 41.6              | 24.96             | 16.64        |
| Поиск ресторанов             | 62.4         | 62.4                  | 41.6              | 24.96             | 16.64        |
| Чтение отзывов               | 51.9         | 51.9                  | 34.6              | 20.76             | 13.84        |
| Написание отзыва             | 1.05         | 1.05                  | 0.7               | 0.42              | 0.28         |
| Оформление заказа            | 6.9          | 6.9                   | 4.6               | 2.76              | 1.84         |
| Оплата заказа                | 5.22         | 5.22                  | 3.48              | 2.09              | 1.39         |
| Отслеживание заказа          | 20.82        | 20.82                 | 13.88             | 8.33              | 5.55         |
| Получение уведомлений        | 104.1        | 104.1                 | 69.4              | 41.64             | 27.76        |
| Просмотр меню                | 62.4         | 62.4                  | 41.6              | 24.96             | 16.64        |
| Просмотр ресторана           | 62.4         | 62.4                  | 41.6              | 24.96             | 16.64        |
| Регистрация ресторана        | 0.042        | 0.042                 | 0.028             | 0.017             | 0.011        |
| **Итого**                    | **439.63**   | **439.63**            | **293.09**        | **175.85**        | **117.24**   |

## Список источников

[^1]: [Яндекс Еда и Деливери поделилась статистикой по аудитории и онлайн-заказам](https://m.seonews.ru/events/yandeks-eda-i-deliveri-podelilas-statistikoy-po-auditorii-i-onlayn-zakazam/)
[^2]: [Сервис, который кормит миллионы пользователей](https://dev.go.yandex/services/eda)
[^3]: [Анализ трафика по SimilarWeb](https://pro.similarweb.com/#/digitalsuite/websiteanalysis/overview/website-performance/*/999/28d?webSource=Total&key=eda.yandex.ru)
[^4]: [«Яндекс» впервые раскрыл число заказов в сервисе «Яндекс.Еда»](https://vc.ru/food/55365-yandeks-vpervye-raskryl-chislo-zakazov-v-servise-yandekseda)
[^5]: [Что заказывают в Яндекс Еде?](https://yandex.ru/company/researches/2020/food)
[^6]: [Продающее меню. Способы его создания](https://traktir.ru/publications/14216/#:~:text=От%20концепции%20зависит%20и%20общее%20количество%20блюд.&text=Заведения%20русской%20кухни%20предполагают%20наличие,Больше%20позиций%20–%20не%20значит%20лучше!)

