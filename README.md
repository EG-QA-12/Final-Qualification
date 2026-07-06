# Final-Qualification Project

## Тестирование книжного онлайн-магазина: https://www.chitai-gorod.ru/

## Задача: 
## Автоматизировать от 5 UI тестов, составленных по функциональному чек-листу из Финальной работы по ручному тестированию:
```
1. Найти товар в поиске по имени на кириллице : "Манюня";
2. Найти товар в поиске по его id :3022420;
3. Добавление товара в корзину с помощью кнопки "Купить": книга "Пес по имени Мани";
4. Увеличение количества товара в корзине с помощью "+" : книга "Пес по имени Мани" увеличить до 2-х штук;
5. Корректное суммирование стоимости товаров в корзине;
6. Удаление товара из корзины: книга "Манюня".
```
## Автоматизировать от 5 API тестов, составленных на основе коллекции и кейсов из финальной работы по ручному тестированию:
### API-тестирование корзины
Base-URL: https://web-gate.chitai-gorod.ru/api/v1/cart

## Позитивные проверки:
### 1. Добавление товара в корзину
```
Первый шаг: Post-запрос
URL: {{Base_url}}/product
Body: {"id":2248089,"adData":{"item_list_name":"product-page"}}
Проверка этого товара в корзине:
Второй шаг: GET-запрос
URL: {{Base_url}}
```
### 2. Увеличение количества товара в корзине
```
Первый шаг: PUT-запрос
URL: {{Base_url}}
BODY: [{"id":132850748,"quantity":4}]
Проверка этого товара в корзине:
Второй шаг: GET-запрос
URL: {{Base_url}}
```
### 3. Удаление товара из корзины
```
Первый шаг: Delete-запрос 
URL: {{Base_url}}/product/132850748
Привязываем конкретное id товара для удаления
Body нет
Проверка этого товара в корзине:
Второй шаг: GET-запрос
URL: {{Base_url}}
```
## Негативные проверки: 

### 4. Изменение количества товара на несуществующее количество
```
Первый шаг: Добавить товар в корзину
Post-Запрос 
URL:{{Base_url}}/product
BODY: {"id":2884565,"adData":{"item_list_name":"product-page"}}

Второй шаг: Изменить количество товара на несуществующее количество товара
PUT-Запрос 
URL: {{Base_url}}
BODY: [{"id":131920052,"quantity":500}]
```
### 5. Добавление несуществующего товара в корзину
```
Один шаг: POST-запрос
URL: {{Base_url}}/product
BODY: {"id":1111111,"adData":{"item_list_name":"product-page"}}
```
## Структура Проекта:
```
Final-Qualification/
├── Tests/
│   ├── test_api.py
│   ├── test_api_playwright.py
│   ├── test_ui.py
│   ├── test_ui_playwright.py
│   ├── conftest.py
│   ├── services/
│   ├── pages/
│   └── utils/
├── .env
├── .gitignore
├── pytest.ini
├── requirements.txt
└── README.md
```

## Переменные окружения
Секреты хранятся в `.env` (файл не коммитится в Git).
- `CHITAI_GOROD_API_TOKEN` — Bearer-токен API
- `CHITAI_GOROD_USER_ID` — ID пользователя
- `CHITAI_GOROD_COOKIES` — cookies для UI
- `CHITAI_GOROD_API_URL` — базовый URL API
- `CHITAI_GOROD_UI_URL` — базовый URL сайта

## Запуск тестов
```powershell
pytest                    # все тесты
pytest -m ui              # только UI
pytest -m api             # только API
pytest -m smoke           # smoke
```

## Allure-отчёты
```powershell
pytest --alluredir=allure-results
allure serve allure-results
```
