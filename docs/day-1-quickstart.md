# Стартовый Чеклист — Неделя 1, День 1

**Начало:** Сегодня (Август 2026)  
**Первые 3 часа:** Окружение и первый скрипт  

---

## ✓ Немедленные действия (далее в этом часу)

### Шаг 1: Скачайте и установите (5 мин)

```bash
# Убедитесь что Python 3.9+ установлен
python --version

# Создайте рабочую директорию
mkdir ai-engineering-workspace
cd ai-engineering-workspace
```

### Шаг 2: Виртуальное окружение (5 мин)

```bash
# Создать
python -m venv venv

# Активировать (Mac/Linux)
source venv/bin/activate

# Активировать (Windows)
venv\Scripts\activate
```

### Шаг 3: Установите SDK (3 мин)

```bash
pip install anthropic python-dotenv
```

### Шаг 4: API Ключ (5-10 мин)

1. Откройте: https://console.anthropic.com
2. Создайте новый ключ (или используйте существующий)
3. Создайте файл `.env`:

```
ANTHROPIC_API_KEY=sk_ant_your_key_here
```

**Не коммитьте `.env` в Git!** (добавьте в `.gitignore`)

### Шаг 5: Проверка (2 мин)

Создайте файл `test.py`:

```python
from anthropic import Anthropic
from dotenv import load_dotenv

load_dotenv()

client = Anthropic()

response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=100,
    messages=[{"role": "user", "content": "Say 'Hello from Claude'"}]
)

print(response.content[0].text)
```

Запустите:
```bash
python test.py
```

**Если сработало:** ✓ Все готово!  
**Если ошибка:** Проверьте:
- API ключ в `.env`
- Интернет соединение
- Версию Python (3.9+)

---

## 📚 На сегодня вечер (2-3 часа)

### 1. Читайте документацию (45 мин)

Откройте: https://docs.anthropic.com/en/docs/about/overview

Сосредоточьтесь на:
- "Overview" — что это
- "Getting Started" — как использовать
- "Models" — какие модели есть

Напишите 3-5 заметок о главных идеях.

### 2. Напишите первый полноценный скрипт (45 мин)

Создайте `hello_claude.py`:

```python
from anthropic import Anthropic
from dotenv import load_dotenv

load_dotenv()

client = Anthropic()

# Ваш первый вопрос
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=500,
    messages=[
        {
            "role": "user",
            "content": "Что такое LLM? Объясни кратко (2-3 предложения) для начинающего инженера."
        }
    ]
)

print("=== Ответ Claude ===")
print(response.content[0].text)
print(f"\n=== Статистика ===")
print(f"Input токенов: {response.usage.input_tokens}")
print(f"Output токенов: {response.usage.output_tokens}")
print(f"Всего: {response.usage.input_tokens + response.usage.output_tokens}")
```

Запустите и сохраните результат.

### 3. Экспериментируйте (30 мин)

Измените вопрос в скрипте на:
- "Что такое RAG?" 
- "Чем отличается RAG от обычного LLM?"
- Ваш собственный вопрос

Понаблюдайте как меняется количество токенов.

---

## 🎯 На завтра

Вы завершите:
- Окружение полностью готово
- Первые 3 скрипта написаны
- Понимаете как работает базовый API

**Потом:** Перейдете на документирование и более сложные проекты.

---

## 🚀 После этого

Когда это завершите, откройте: `/docs/week-1-guide.md`

Там полный план на всю неделю с:
- Концепциями для изучения
- Проектом "умный чат с памятью"
- Еженедельным отчетом

---

## ❓ Если что-то не работает

1. **ImportError: No module named 'anthropic'**
   - Убедитесь что venv активирован
   - Переустановите: `pip install anthropic`

2. **AuthenticationError**
   - Проверьте `.env` файл
   - Убедитесь что API ключ правильный
   - Попробуйте ключ из консоли напрямую

3. **ConnectionError**
   - Проверьте интернет
   - API может быть временно недоступна

4. **RateLimitError**
   - Используемый план лимитирован
   - Дождитесь или проверьте billing в console

**Если всё еще не работает:** Пишите в сообщество или reopened issue на GitHub Anthropic.

---

## ✅ Готовы?

1. Откройте терминал
2. Создайте директорию
3. Установите зависимости
4. Запустите `test.py`
5. Напишите `hello_claude.py`

**Let's go! 🚀**

Когда завершите — создайте файл `/progress/ai-engineering/day-1.md` и опишите что сделали.