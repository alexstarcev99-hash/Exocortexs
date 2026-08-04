# ИИ Инженерство — Roadmap обучения

**Статус:** Активный курс обучения  
**Уровень:** Новичок → Мастер (0→3, 9 месяцев)  
**Фокус:** RAG системы + Агентские системы

---

## Структура обучения

```
/docs                          — теория и концепции
  ├── fundamentals/            — основы LLM и архитектура
  ├── rag-patterns/            — паттерны RAG систем
  ├── agents-patterns/         — паттерны агентских систем
  └── integration-patterns/    — интеграция и production

/projects/                      — практические проекты
  ├── month-1-2/              — фундамент
  ├── month-3-4/              — RAG мастерство
  ├── month-5-6/              — Agents
  └── month-7-9/              — Advanced и production

/progress/                      — еженедельное отслеживание
  └── ai-engineering/         — логи практики
```

---

## Фаза 1: Фундамент (Месяц 1-2)

### Неделя 1-2: Теория LLM

**Необходимо изучить:**
1. Что такое трансформеры (high-level)
2. Tokens и tokenization
3. Context window и limitations
4. Embeddings (зачем нужны)
5. Температура, top-p, и другие параметры

**Материалы:**
- Anthropic Cookbook: https://github.com/anthropic-ai/anthropic-cookbook
- "Attention is All You Need" (концептуально, не в деталях)
- OpenAI GPT papers (overview)

**Практика:**
- Экспериментировать с параметрами в Claude
- Посчитать tokens в разных текстах
- Прочувствовать context window

**Результат:** Понимание как работает модель на концептуальном уровне

---

### Неделя 3-4: Первый API проект

**Проект: Чат с памятью**

```python
# Основные компоненты
- Инициализация Anthropic SDK
- Ведение истории сообщений
- Обработка streaming
- Error handling
```

**Задачи:**
1. Установить Anthropic SDK
2. Создать простой чат-бот
3. Добавить историю (persistent storage)
4. Добавить обработку ошибок
5. Документировать код

**Результат:** Рабочее приложение, готовое к расширению

---

### Неделя 5-6: Введение в Embeddings

**Концепции:**
- Что такое embedding
- Embedding models (OpenAI, Anthropic, local)
- Similarity search
- Vector databases (теория)

**Практика:**
- Создать простой embedding search
- Использовать готовый vector DB (например, FAISS)
- Экспериментировать с различными моделями

**Результат:** Первое понимание RAG компонентов

---

### Неделя 7-8: Reflection и Документирование

**Сделать:**
- Написать summary первого месяца
- Задокументировать "aha moments"
- Выявить пробелы для второго месяца
- Обновить диагностику уровня

**Результат:** Уровень 0.5→1

---

## Фаза 2: RAG Мастерство (Месяц 3-4)

### Неделя 9-10: RAG Архитектура

**Компоненты RAG системы:**

1. **Indexing Pipeline**
   - Загрузка документов
   - Chunking стратегии (fixed-size, semantic, hierarchical)
   - Embedding и хранение
   - Metadata и filtering

2. **Retrieval**
   - BM25 (keyword search)
   - Semantic search (vector similarity)
   - Hybrid search (комбинирование)
   - Re-ranking

3. **Generation**
   - Prompt construction
   - Context management
   - Chain-of-thought prompting
   - Quality assurance

**Практика:**
- Реализовать chunking вручную
- Сравнить BM25 vs semantic
- Экспериментировать с prompt formats

---

### Неделя 11-14: Практический RAG проект

**Проект: RAG для Exocortexs**

**Стек:**
- LangChain или LlamaIndex (или собственное решение)
- Vector DB (Pinecone, Weaviate, FAISS, или Anthropic Files API)
- Anthropic SDK для generation

**Шаги:**
1. Экспортировать markdown файлы из GitHub
2. Обработать и создать embeddings
3. Настроить retrieval pipeline
4. Построить retrieval-augmented generation
5. Оптимизировать quality metrics

**Метрики:**
- Relevance of retrieved documents
- Accuracy of generated answers
- Latency and cost

**Результат:** Production-ready RAG система

---

### Неделя 15-16: Оптимизация и Production

**Фокус:**
- Кэширование (prompt caching, результатов поиска)
- Оптимизация стоимости (модель выбора, batch processing)
- Мониторинг и логирование
- A/B тестирование разных подходов

**Результат:** Уровень 1→2

---

## Фаза 3: Агентские системы (Месяц 5-6)

### Неделя 17-18: Теория Agents

**Концепции:**
- ReAct (Reasoning + Acting)
- Tool use (function calling)
- Planning strategies
- Memory в агентах

**Паттерны:**
- Single turn agent
- Multi-turn agent (agentic loop)
- Tool composition
- Error handling и recovery

**Практика:**
- Изучить примеры agentskits
- Реализовать простой agent вручную

---

### Неделя 19-22: Практический Agent проект

**Проект: Research Agent**

**Инструменты:**
1. Web search (или браузер)
2. Local file reader
3. Calculator
4. Note writer

**Требования:**
- Agent самостоятельно планирует шаги
- Использует несколько инструментов в комбинации
- Обрабатывает ошибки и retry
- Документирует процесс мышления

**Метрики:**
- Успешность выполнения задач
- Эффективность (количество шагов)
- Cost оптимизация

---

### Неделя 23-24: RAG + Agent интеграция

**Комплексная система:**
- Agent может использовать RAG как инструмент
- RAG обогащает контекст агента
- Production deployment и monitoring

**Результат:** Уровень 1→2/3

---

## Фаза 4: Мастерство (Месяц 7-9)

### Advanced паттерны

**RAG:**
- Hierarchical retrieval
- Multi-index search
- Query expansion и decomposition
- Adaptive retrieval (когда и сколько контекста получать)

**Agents:**
- Multi-agent collaboration
- Agent memory management
- Custom tool creation patterns
- Self-reflection в agents

### Оптимизация и производство

- Production architecture patterns
- Scaling considerations
- Monitoring и alerting
- Cost/performance trade-offs

### Research и Innovation

- Читать свежие papers
- Экспериментировать с новыми подходами
- Вносить собственные идеи

**Результат:** Уровень 2→3

---

## Еженедельный стандарт

### Структура недели (10-15 часов)

**Monday: Планирование (30 мин)**
- Какие концепции изучу?
- Какие коды напишу?
- Какие метрики отслежу?

**Tuesday-Thursday: Обучение + Практика (8-10 часов)**
- 2-3 часа: Deep work (обучение, изучение)
- 4-6 часов: Hands-on практика (кодирование, эксперименты)
- 1-2 часа: Experimentation и тестирование

**Friday: Reflection (1-2 часа)**
- Что получилось?
- Какие insights?
- Что не понял?
- Какой я уровень сейчас?

**Weekend: Документирование (1-2 часа)**
- Написать weekly report
- Обновить прогресс файл
- Подготовиться к следующей неделе

---

## Weekly Report Template

```markdown
# Неделя [номер] — [дата]

## Обучение
- Изучено: [концепции, инструменты, паттерны]
- Материалы: [ссылки на то, что читал]

## Практика
- Код написано: [строки, файлы, проекты]
- Проблемы и решения: [что не сработало и как зафиксил]
- Экспериментировал: [что пробовал]

## Insights
- Aha moment: [главное понимание неделе]
- Пробелы: [что нужно еще изучить]
- Следующие приоритеты: [на что сосредоточиться]

## Уровень осознания
- Предыдущая оценка: [был уровень X]
- Текущая оценка: [сейчас уровень Y]
- Почему изменилось: [конкретные примеры]

## Метрики
- Часы практики: __h
- Проектов завершено: __
- Ошибок выявлено: __
- Документа написано: __

## Код и artifacts
- Ссылки на GitHub commits
- Ссылки на документацию
```

---

## Критерии завершения фаз

### Фаза 1 ✓ (Месяц 2)
- [x] Установлено окружение, работает SDK
- [x] 2-3 API проекта завершено
- [x] Понимаю базовые концепции
- [x] Первый простой RAG работает

### Фаза 2 ✓ (Месяц 4)
- [ ] Production RAG система развёрнута
- [ ] Метрики качества отслеживаются
- [ ] Документация написана
- [ ] Optimization проведена

### Фаза 3 ✓ (Месяц 6)
- [ ] Agent система работает
- [ ] RAG + Agent интегрировано
- [ ] Production ready с monitoring

### Фаза 4 ✓ (Месяц 9)
- [ ] 5+ сложных проектов
- [ ] Собственные паттерны разработаны
- [ ] Гайды и документация
- [ ] Уровень 3 достигнут

---

## Ресурсы и ссылки

### Официальная документация
- Anthropic SDK: https://github.com/anthropic-ai/anthropic-sdk-python
- Claude Cookbook: https://github.com/anthropic-ai/anthropic-cookbook
- API docs: https://docs.anthropic.com

### RAG фреймворки
- LangChain: https://python.langchain.com/
- LlamaIndex: https://www.llamaindex.ai/
- Verba: https://github.com/weaviate/Verba

### Агентские системы
- ReAct papers
- Tool use best practices
- Multi-agent patterns

### Сообщества
- Anthropic Discord
- LangChain community
- Research papers (arXiv)