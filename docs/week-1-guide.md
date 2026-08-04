# Неделя 1: Старт в ИИ инженерство

**Дата:** Август 2026  
**Таймлайн:** 1 неделя  
**Часы:** 10-12 часов  
**Результат:** Рабочее Python окружение + первый API проект

---

## День 1: Подготовка (2-3 часа)

### Задача 1.1: Установить Python окружение

**Шаги:**

1. **Убедитесь, что Python 3.9+ установлен**
```bash
python --version  # должно быть 3.9+
```

2. **Создайте виртуальное окружение**
```bash
mkdir ai-engineering-workspace
cd ai-engineering-workspace
python -m venv venv

# Активировать (Linux/Mac)
source venv/bin/activate

# Активировать (Windows)
venv\Scripts\activate
```

3. **Установите основные пакеты**
```bash
pip install anthropic python-dotenv requests
```

4. **Получите API ключ от Anthropic**
   - Перейти: https://console.anthropic.com
   - Создать новый API key
   - Сохранить в `.env` файл:
```
ANTHROPIC_API_KEY=your_key_here
```

**Проверка:**
```python
from anthropic import Anthropic

client = Anthropic()
print("✓ SDK установлен и готов")
```

**Время:** 30-45 мин

---

### Задача 1.2: Читать документацию Anthropic

**Что изучить (45-60 мин):**

1. **API Overview** (15 мин)
   - https://docs.anthropic.com/en/docs/about/overview
   - Главная идея: как работает Claude API

2. **Getting Started** (15 мин)
   - https://docs.anthropic.com/en/docs/quickstart
   - Ваш первый запрос к API

3. **Models** (10 мин)
   - https://docs.anthropic.com/en/docs/about/models/overview
   - Какие модели существуют и их характеристики

4. **Messages API** (15 мин)
   - https://docs.anthropic.com/en/docs/build-with-claude/messages-api
   - Основной API интерфейс

**Что писать:**
- Заметки в `/docs/week-1-notes.md`
- Ключевые моменты, которые поняли
- Вопросы, которые остались

**Время:** 45-60 мин

---

### Задача 1.3: Первый простой скрипт (45 мин)

**Создайте файл: `hello_claude.py`**

```python
from anthropic import Anthropic
import os
from dotenv import load_dotenv

load_dotenv()

# Инициализировать клиент
client = Anthropic()

# Простой запрос
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    messages=[
        {
            "role": "user",
            "content": "Объясни кратко, что такое LLM в 2-3 предложениях"
        }
    ]
)

# Вывести результат
print("Ответ Claude:")
print(response.content[0].text)
print("\n---")
print(f"Использовано токенов: {response.usage.input_tokens + response.usage.output_tokens}")
```

**Запустить:**
```bash
python hello_claude.py
```

**Что понять:**
- Как работает базовый API запрос
- Что такое messages (role, content)
- Как читать ответ и использовать токены

**Результат:** ✓ Вывод от Claude в консоли

**Время:** 30-45 мин

---

**День 1 завершен:** Окружение готово, первый скрипт работает ✓

---

## День 2-3: Базовое обучение (4-5 часов)

### Задача 2.1: Изучить концепции (2-3 часа)

**Понять следующее:**

1. **Tokens** (30 мин)
   - Что такое токен (примерно 4 символа)
   - Как считаются токены
   - Почему это важно (cost, context window)
   - Прочитать: https://docs.anthropic.com/en/docs/build-with-claude/tokens

   **Практика:**
   ```python
   from anthropic import Anthropic
   
   client = Anthropic()
   
   # Напишите разные текст и посмотрите, сколько токенов
   texts = [
       "Hello",
       "Hello, how are you?",
       "Российская Федерация — многонациональное государство...",
   ]
   
   for text in texts:
       response = client.messages.create(
           model="claude-3-5-sonnet-20241022",
           max_tokens=10,
           messages=[{"role": "user", "content": text}]
       )
       tokens = response.usage.input_tokens
       print(f"'{text}' = {tokens} tokens")
   ```

2. **Context Window** (20 мин)
   - Что такое контекст (входной + выходной размер)
   - Ограничения разных моделей
   - Как это влияет на дизайн системы

3. **Temperature и Parameters** (30 мин)
   - `temperature` = 0 (детерминированный) vs 1 (креативный)
   - `max_tokens` = максимум в ответе
   - `top_p` = diversity
   - Когда какие использовать

   **Практика:**
   ```python
   # Два запроса с разными temperature
   for temp in [0, 1]:
       response = client.messages.create(
           model="claude-3-5-sonnet-20241022",
           max_tokens=100,
           temperature=temp,
           messages=[
               {"role": "user", 
                "content": "Напиши короткий совет для начинающего инженера"}
           ]
       )
       print(f"Temperature {temp}: {response.content[0].text}\n")
   ```

**Результат:** Понимание как параметры влияют на ответы

---

### Задача 2.2: Про embeddings (1-2 часа)

**Что такое embeddings:**

1. **Концептуально** (30 мин)
   - Текст → числовой вектор (например, 1536 чисел)
   - Похожие тексты → похожие векторы
   - Зачем это нужно для поиска и RAG

2. **Практика с embeddings** (45 мин)
   ```python
   # Используя Anthropic Batch API для embeddings
   # Или альтернатива: использовать OpenAI embeddings
   
   from openai import OpenAI  # если используете OpenAI
   
   client = OpenAI()
   
   texts = [
       "Я люблю программировать",
       "Кодирование очень интересно",
       "Погода сегодня хорошая"
   ]
   
   embeddings = []
   for text in texts:
       resp = client.embeddings.create(
           model="text-embedding-3-small",
           input=text
       )
       embeddings.append(resp.data[0].embedding)
   
   # Вычислить похожесть
   import numpy as np
   
   def cosine_similarity(a, b):
       return np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))
   
   sim = cosine_similarity(embeddings[0], embeddings[1])
   print(f"Похожесть 1 и 2: {sim:.3f}")  # должна быть высокой
   
   sim = cosine_similarity(embeddings[0], embeddings[2])
   print(f"Похожесть 1 и 3: {sim:.3f}")  # должна быть низкой
   ```

**Результат:** Прочувствовал, как работают embeddings

---

**День 2-3 завершены:** Концепции усвоены, практика проведена ✓

---

## День 4-5: Первый полноценный проект (4-5 часов)

### Задача 3: Проект "Умный чат с памятью"

**Описание:**
Чат-бот, который помнит всю историю разговора и может ссылаться на предыдущие сообщения.

**Файл: `smart_chat.py`**

```python
from anthropic import Anthropic
import json
import os
from dotenv import load_dotenv

load_dotenv()

class SmartChat:
    def __init__(self):
        self.client = Anthropic()
        self.conversation_history = []
        self.model = "claude-3-5-sonnet-20241022"
    
    def add_message(self, role, content):
        """Добавить сообщение в историю"""
        self.conversation_history.append({
            "role": role,
            "content": content
        })
    
    def get_response(self, user_message):
        """Получить ответ от Claude с историей"""
        # Добавить пользовательское сообщение
        self.add_message("user", user_message)
        
        # Запрос к API с полной историей
        response = self.client.messages.create(
            model=self.model,
            max_tokens=1024,
            system="Ты помощник, который помнит всю историю разговора и может ссылаться на предыдущие сообщения.",
            messages=self.conversation_history
        )
        
        # Получить ответ
        assistant_message = response.content[0].text
        
        # Добавить в историю
        self.add_message("assistant", assistant_message)
        
        return assistant_message
    
    def save_history(self, filename="chat_history.json"):
        """Сохранить историю в файл"""
        with open(filename, 'w', encoding='utf-8') as f:
            json.dump(self.conversation_history, f, ensure_ascii=False, indent=2)
    
    def load_history(self, filename="chat_history.json"):
        """Загрузить историю из файла"""
        if os.path.exists(filename):
            with open(filename, 'r', encoding='utf-8') as f:
                self.conversation_history = json.load(f)
    
    def print_stats(self):
        """Вывести статистику"""
        print(f"\n=== Статистика ===")
        print(f"Сообщений в истории: {len(self.conversation_history)}")
        print(f"Примерно токенов в истории: {len(str(self.conversation_history)) // 4}")

def main():
    chat = SmartChat()
    
    print("=== Умный чат с памятью ===")
    print("Введите 'quit' для выхода, 'save' для сохранения, 'load' для загрузки")
    print()
    
    # Загрузить предыдущую историю если есть
    chat.load_history()
    
    while True:
        user_input = input("Вы: ").strip()
        
        if user_input.lower() == 'quit':
            print("До свидания!")
            break
        elif user_input.lower() == 'save':
            chat.save_history()
            print("✓ История сохранена")
            continue
        elif user_input.lower() == 'load':
            chat.load_history()
            print("✓ История загружена")
            chat.print_stats()
            continue
        elif not user_input:
            continue
        
        # Получить ответ
        response = chat.get_response(user_input)
        print(f"\nClaude: {response}\n")

if __name__ == "__main__":
    main()
```

**Запустить:**
```bash
python smart_chat.py
```

**Задачи для углубления:**

1. **Добавить summarization** (1 час)
   - Когда история становится длинной, реализовать резюме
   - Сохранить резюме + последние 5 сообщений для контекста

2. **Добавить обработку ошибок** (30 мин)
   - Что делать если API недоступен?
   - Retry logic

3. **Добавить логирование** (30 мин)
   - Логировать токены, время ответа, ошибки

**Результат:** Работающий чат, готовый к расширению ✓

---

## День 6-7: Документирование и Reflection (1-2 часа)

### Задача 4: Написать Weekly Report

**Файл: `progress/ai-engineering/week-1-report.md`**

```markdown
# Неделя 1 — AI Инженерство: Старт

## Что было сделано

### Установка и подготовка
- ✓ Установлено Python окружение
- ✓ Установлен Anthropic SDK
- ✓ Получен API ключ
- ✓ Проверена работа базового скрипта

### Обучение (3 часа)
- ✓ Прочитана документация Anthropic
- ✓ Изучены концепции: tokens, context window, temperature
- ✓ Экспериментировал с embeddings
- ✓ Понял базовую структуру API

### Практика (6-7 часов)
- ✓ Написан первый скрипт `hello_claude.py`
- ✓ Экспериментировал с параметрами API
- ✓ Создан проект `smart_chat.py` с памятью
- ✓ Реализовано сохранение/загрузка истории

## Ключевые insights

**Aha moments:**
1. Токены считаются не только по словам, а по смыслу (многоязычность)
2. Temperature 0 используется когда нужна точность, 1 когда креативность
3. История в контексте растет очень быстро (нужно быть внимательным)

**Пробелы в знаниях:**
- Не понимаю еще как работают embeddings на техническом уровне
- Не знаю как масштабировать chat когда история становится большой
- Не знаком с реальными production паттернами

## Проекты и код

- `hello_claude.py` — базовый API запрос
- `smart_chat.py` — умный чат с памятью
- Оба файла работают и готовы к расширению

## Метрики

- Часов практики: 12
- Строк кода написано: ~150
- Документов прочитано: 3
- Ошибок исправлено: 5

## Уровень осознания

**Была оценка:** 0 (Новичок)
**Сейчас оценка:** 0.5 (Осознанный новичок)

**Почему изменилось:**
- Понимаю базовые концепции
- Могу писать рабочий код
- Знаю что не знаю (есть четкие пробелы)

## Следующие приоритеты

На неделю 2:
1. Глубже разобраться с embeddings
2. Создать простой RAG прототип
3. Изучить обработку ошибок и retry logic
4. Документировать learnings

## Notes for next week
- Нужно больше экспериментировать
- Документация Anthropic очень хорошая — использовать ее как основу
- API очень просто использовать — фокусировать на архитектуре, а не на синтаксе
```

**Сохранить файл и запушить в GitHub**

---

## Контрольный список Недели 1

- [ ] Python окружение установлено
- [ ] Anthropic SDK работает
- [ ] API ключ получен и сохранен
- [ ] Документация изучена (4 раздела)
- [ ] Первый скрипт написан и работает
- [ ] Концепции усвоены (токены, context, temperature)
- [ ] Embeddings экспериментированы
- [ ] Проект "smart_chat" завершен
- [ ] Weekly report написан
- [ ] Code закоммичен в GitHub
- [ ] Диагностика обновлена

**Всё завершено? Переходите на Неделю 2: RAG foundations!** 🚀

---

## Полезные ссылки

- Anthropic Docs: https://docs.anthropic.com
- SDK GitHub: https://github.com/anthropic-ai/anthropic-sdk-python
- Cookbook: https://github.com/anthropic-ai/anthropic-cookbook
- Token Counter: https://github.com/anthropic-ai/anthropic-tokenizer-py