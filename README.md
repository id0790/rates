<h2>Тестовое задание</h2>
<p>Необходимо реализовать сервис, выдающий текущий курс валюты и историю изменения курса через HTTP REST API, с доступом только для авторизованных пользователей. Фреймворк Yii2/Laravel. В результате должна быть ссылка на репозиторий.</p>

<h3>Requires</h3>
- PHP 7.1+<br/>
- Postgresql<br/>


<h3>Деплоймент</h3>

- клонуємо репозиторій: git clone https://github.com/id0790/rates.git<br/>
- переходимо в теку проекту: cd rates<br/>
- встановлення додатків: composer update<br/>
- ініціалізація проекту: php init -> Вибираємо Development (Відкрив дебаг панель всім для підтвердження пошти)<br/>
- Налаштовуємо базу в: common/config/main-local.php<br/>
- Міграції: php yii migrate/up<br/>

<h3>Запуск</h3>

- Отримуємо ключ: https://currencylayer.com/<br/>
- Прописуємо ключ: common/config/params-local.php<br/>
- Запускаємо імпорт валют: php yii rate/import USD,UAH,RUB,CAD<br/>

<h3>Функціонал</h3>
- Отримати рейти: /v1/rates?code=UAH&from=2020-01-01&to=2021-01-01<br/>
- Отримати рейт: /v1/rates/UAH<br/>
- Реєстрація: /site/signup (Конфірм в дебагері) <br/>
- Авторизація: /site/login<br/>

<h3>Приклад запиту апі</h3>
GET https://адрес/v1/rates/UAH<br/>
Accept: application/json<br/>
Authorization: Basic dGVzdEB0ZXN0LmNvbTp0ZXN0QHRlc3QuY29t<br/>

<h3>Структура</h3>

- common/config/container.php - DI
- common/services/RateService.php - основна логіка 
- common/sources/ApiLayerSource.php - джерело імпорту валют. Підключення http клієнта через агрегацію
- common/sources/Source.php - інтерфейс апі
- common/sources/RateDto.php - dto для результату даних стронього апі
- common/repositories/RateRepository.php - репозиторій для роботи з валютами. Потрібен був для реалізації batch insert. 
- common/repositories/PersistRepository.php - інтерфейс для зберігання
- common/repositories/Repository.php - загальний інтерфейс для роботи з репозиторієм
- common/models/Rate.php - ентіті валюти
- frontend/controllers/RatesController.php - апі

<h3>Особливості реалізації</h3>
- Акцент був на демонстрації коду в реалізації валют<br/>
- Реєстрації, аутентифікації лише для прикладу. Взята з "коробки". Ніяким чином не модифікована. За умовами завдання реалізовувати не потрібно<br/>
- Апі прикрито авторизацією(одна з умов завдання). Вибраний найшвидший варіант HttpBasicAuth. На тому що було.  Не варто сприймати як пропозицію до реалізації в реальних умовах. Логін\пароль для запитів ніхто використовувати не збирається. Тут мав би бути який access_token. Можливо auth. Але все це виходить за рамки завдання <br/>
- Api можливо було винести в окремий application. Але на те не було часу і не дає великого сенсу враховуючи управління користувачами буде відокремлене від апі<br/>
- В прикладі не використовується ніякого виду оптимізації(лише індекс). Деякі частини коду можна було реалізувати для оптимізованого відгуку АПІ. Прикрити кешем. Але то інша тема<br/>


