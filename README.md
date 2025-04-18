# FastAPI GPT-2 Question Answering

Это приложение на FastAPI использует модель GPT-2 для генерации ответов на вопросы на русском языке. Модель загружается из библиотеки `transformers` и предоставляет API для взаимодействия с ней.

## Установка

Для запуска приложения вам понадобятся следующие зависимости. Убедитесь, что у вас установлен Python 3.7 или выше.

1. Клонируйте репозиторий:

   ```bash
   git clone <URL_репозитория>
   cd <имя_папки>
   ```

2. Установите необходимые библиотеки:

   ```bash
   pip install -r requirements.txt
   ```

   В `requirements.txt` должны быть указаны следующие зависимости:

   ```
   fastapi
   uvicorn
   torch
   transformers
   pydantic
   ```

## Запуск приложения

Для запуска приложения выполните следующую команду:

```bash
uvicorn main:app --host 0.0.0.0 --port 5000
```

Здесь `main` — это имя файла (без расширения), в котором находится ваш код, а `app` — это экземпляр FastAPI.

После запуска приложение будет доступно по адресу `http://localhost:5000`.

## Использование API

### Генерация ответа

Для генерации ответа на вопрос отправьте POST-запрос на `/generate` с JSON-телом, содержащим вопрос.

**Пример запроса:**

```bash
curl -X POST "http://localhost:5000/generate" -H "Content-Type: application/json" -d '{"question": "Какой сегодня день?"}'
```

**Пример ответа:**

```json
{
  "answer": "Сегодня понедельник."
}
```

### Описание кода

1. **Импорт библиотек**:
   - `FastAPI`: основной фреймворк для создания API.
   - `HTTPException`: для обработки ошибок HTTP.
   - `BaseModel`: для валидации входящих данных.
   - `GPT2LMHeadModel` и `GPT2Tokenizer`: для работы с моделью GPT-2.
   - `torch`: для работы с тензорами.

2. **Инициализация приложения**:
   - Создается экземпляр FastAPI.

3. **Загрузка модели и токенизатора**:
   - Модель `sberbank-ai/rugpt3small_based_on_gpt2` загружается из библиотеки `transformers`.
   - Устанавливается `pad_token_id` для корректной работы модели.

4. **Функция `generate_answer`**:
   - Принимает вопрос в виде строки, генерирует ответ с помощью модели и возвращает его.

5. **Определение модели запроса**:
   - Класс `Question` определяет структуру входящих данных, ожидая поле `question`.

6. **Маршрут `/generate`**:
   - Обрабатывает POST-запросы, проверяет наличие вопроса и возвращает сгенерированный ответ.

7. **Запуск приложения**:
   - Если файл запускается напрямую, приложение запускается на `0.0.0.0:5000`.

## Заключение

Это приложение демонстрирует, как использовать FastAPI и модель GPT-2 для создания простого API для генерации ответов на вопросы. Вы можете расширить функциональность, добавив дополнительные маршруты или улучшив обработку запросов.
