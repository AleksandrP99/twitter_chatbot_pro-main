# Twitter Бот (Python)

Готовый к использованию Twitter-бот с функционалом:
- Ежедневная публикация цитат (9:00 по индийскому времени) с изображениями и хэштегами
- Автоматические ответы на упоминания и личные сообщения с использованием GPT-4
- Мониторинг хэштегов с оценкой лидов и вовлечённости
- Анализ тональности с уведомлениями и ежедневным отчётом
- Сбор данных для аналитической панели и экспорт в CSV

## Технологический стек
- Python 3.10+
- Tweepy (Twitter API v2 + v1.1 для работы с медиа)
- OpenAI GPT-4 (через `openai` Python SDK)
- SQLite (через `sqlite3`)
- APScheduler (задачи по расписанию)
- VADER (анализ тональности)
- Pillow (генерация изображений)

## Установка и настройка
1. Создайте виртуальное окружение и установите зависимости:
```bash
python -m venv .venv
. .venv/Scripts/activate  # Windows PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

2. Создайте файл .env на основе .env.example и заполните ключи:
```
TWITTER_API_KEY=...
TWITTER_API_SECRET=...
TWITTER_ACCESS_TOKEN=...
TWITTER_ACCESS_TOKEN_SECRET=...
TWITTER_BEARER_TOKEN=...
OPENAI_API_KEY=...
```

3. Запустите бота:
```bash
python -m twitter_bot.main
```

Бот будет:
- Публиковать ежедневную цитату 
- Проверять упоминания каждую минуту и отвечать в течение 2 минут
- Мониторить хэштеги каждые 10 минут
- Генерировать ежедневный CSV-отчёт с аналитикой

## Структура проекта
```
twitter_bot/
├── main.py
├── config.py
├── bot/
│   ├── quote_poster.py
│   ├── reply_handler.py
│   ├── hashtag_monitor.py
│   ├── sentiment_analyzer.py
│   └── analytics.py
├── utils/
│   ├── twitter_api.py
│   ├── openai_helper.py
│   └── database.py
├── data/
│   ├── quotes.json
│   └── bot.db (auto-created)
├── requirements.txt
└── .env.example
```

## Примечания
- Ключи API считываются из переменных окружения.
- База данных инициализируется автоматически при первом запуске.
- Реализована обработка ограничений скорости запросов с повторными попытками и экспоненциальной задержкой.
- Если загрузка медиа или отправка личных сообщений ограничены для вашего уровня аккаунта, функции запишут предупреждение в лог и продолжат работу.
