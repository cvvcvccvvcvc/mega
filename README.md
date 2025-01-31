# Проект: API для запросов к AI агенту с возможностью поиска и анализа веб-страниц 

Этот проект предоставляет API для асинхронной обработки запросов с использованием Yandex GPT API и Yandex Search API. API получает запросы от пользователей, ищет информацию в интернете, анализирует её и предоставляет ответ с пояснением и ссылками на источники.

## Работоспособность
В данный момент сервис доступен по адресу `http://158.160.137.90:8080/api/request`

Input: POST запрос с json {id: int, query:str}

Output: json {id: int, answer: int / None, reasoning: str, sources: list(urls)}

## Основная идея работы

1. Вопрос в нескольких формах передается в **Yandex Search API**. Собираются только наиболее релевантные источники (первые).
2. С веб-страниц собирается ключевая информация с помощью **BeautifulSoup**.
3. Источники фильтруются с помощью **Yandex GPT API** по принципу "Полезна ли эта информация для ответа на вопрос?"
4. С помощью **Yandex GPT API** формируется односложный ответ и пояснение к ответу с помощью дополнительной информации с полезных источников.

## Основные функции:
1. Принимает запросы с вопросами и вариантами ответов (или без них).
2. Ищет релевантные источники в интернете.
3. Парсит источники
4. Использует Yandex GPT для анализа источников и выбора наиболее подходящего ответа.
5. Возвращает ответ, пояснение и ссылки на источники.

### Требования
- Python 3.8+
- Docker (для запуска через контейнеры)

## Установка зависимостей

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/cvvcvccvvcvc/mega.git
   cd repository-name
   ```
2. Создайте файл .env в корне проекта и добавьте ваши ключи
   ```
   FOLDER_ID=your_folder_id
   YANDEXGPT_KEY=your_yandex_gpt_api_key
   YANDEX_SEARCH_KEY=your_yandex_search_api_key
   ```
3. Соберите и запустите контейнер
   ```bash
   docker-compose up -d
   ```
