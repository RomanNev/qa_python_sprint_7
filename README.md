# QA Python Sprint 7

## Описание 
Этот проект представляет собой набор автотестов для API сервиса доставки "Самокат"

## Структура проекта
- **`tests/`** — папка с тестами:
  - `test_create_courier.py` — тесты для создания курьеров.
  - `test_login_courier.py` — тесты для авторизации курьеров.
  - `test_create_order.py` — тесты для создания заказов.
  - `test_get_orders.py` — тесты для получения списка заказов.
- **`conftest.py`** — фикстуры для создания тестовых данных и очистки после тестов.
- **`scooter_api.py`** — класс для работы с API.
- **`helper.py`** — утилиты для генерации тестовых данных.
- **`data.py`** — предопределённые данные для тестов.
- **`urls.py`** — константы с URL эндпоинтов API.
- **`requirements.txt`** — список зависимостей проекта.

## Тестовые сценарии
### Создание курьера
- Успешное создание курьера (код 201, тело `{"ok":true}`).
- Попытка создать двух одинаковых курьеров (код 409, сообщение "Этот логин уже используется...").
- Создание курьера с существующим логином (код 409, сообщение "Этот логин уже используется...").
- Создание курьера без обязательных полей (логин или пароль пустые, код 400, сообщение "Недостаточно данных...").

### Логин курьера
- Успешная авторизация (код 200, возвращается `id`).
- Авторизация с пустыми обязательными полями (логин или пароль, код 400, сообщение "Недостаточно данных...").
- Авторизация с некорректными данными (логин или пароль, код 404, сообщение "Учетная запись не найдена").
- Авторизация несуществующего пользователя (код 404, сообщение "Учетная запись не найдена").

### Создание заказа
- Создание заказа с цветами `["BLACK", "GREY"]` (код 201, возвращается `track`).
- Создание заказа с цветом `["BLACK"]` (код 201, возвращается `track`).
- Создание заказа с цветом `["GREY"]` (код 201, возвращается `track`).
- Создание заказа без цвета `[]` (код 201, возвращается `track`).

### Список заказов
- Получение списка заказов (код 200, возвращается поле `orders` типа список).

## Требования к запуску
- **Python**: 3.8 или выше.
- **Зависимости**:
  - `pytest` — для запуска тестов.
  - `allure-pytest` — для генерации отчётов (опционально).
  - `requests` — для HTTP-запросов.
  - `faker` — для генерации тестовых данных.
- **Allure**: Для генерации HTML-отчётов (устанавливается отдельно).

## Установка
1. **Клонируйте репозиторий**:
   ```bash
   git clone <URL_репозитория>
2. **Установите зависимости**:
   ```bash
   pip install -r requirements.txt  

## Запуск тестов без отчетов 
1. **Перейти в корневую директорию проекта**:
2. **Выполнить команду**:
   ```bash
   pytest -v
2. **Для запуска конкретного файла тестов**
   ```bash
   pytest tests/test_create_courier.py
   
## Генерация Allure отчетов
1. **Запустить тесты с сохранением данных для Allure**:
   ```bash
   pytest --alluredir=./allure-results
2. **Сгенерировать HTML-отчёт с очисткой предыдущих результатов (опционально)**:
   ```bash
   allure generate ./allure-results -o ./allure-report --clean
2. **Открыть отчёт**
   ```bash
   allure open ./allure-report
**Либо открыть файл allure-report/index.html в браузере вручную**