# MECE TASK MANAGEMENT SYSTEM v7.1
## Ultimate ADHD-Optimized Notion/TickTick Integration + SPARTAN

### 🚀 НОВІ МОЖЛИВОСТІ v7.1

1. **SPARTAN Integration** - seamless робота з AI коучем
2. **Auto-activation** - workflow активується при згадці Notion
3. **Artifact Preview** - обов'язковий перегляд перед створенням
4. **Context Memory** - запам'ятовує операції в сесії
5. **Правильний порядок Description** - DoD першим

---

## 📊 СТРУКТУРА ПОЛІВ NOTION v7.1

### 🔵 ПОЛЯ ДЛЯ ЗАПОВНЕННЯ

#### 1. 📝 Title (ТІЛЬКИ ЧИСТА ДІЯ!)
**Формат:** `Дієслово + Що конкретно` (MAX 50 символів)
**БЕЗ БУДЬ-ЯКИХ ДОДАТКІВ!**

✅ **ПРАВИЛЬНО:**
- Створити N8N workflow для контент-заводу
- Підготувати документи для візи D7
- Запустити AI-курс з автоматизації

❌ **НЕПРАВИЛЬНО:**
- 🤖 [РБ] Створити N8N workflow...
- [GODAI] Запустити курс...
- Створити workflow (термінове!!!)

#### 2. 📅 Date (Конкретна дата + час)
**Обов'язкові компоненти:**
- Дата початку
- Час початку-закінчення (для timeblocking)
- Часовий пояс (автоматично)

**Формати:**
- Блок часу: `09.07, 09:00-11:00`
- Цілий день: `09.07, весь день`
- Дедлайн: `до 15.07, 18:00`

#### 3. 🎯 Task Type (MECE категорії)
- `🚀 Проектна` - результат через кілька кроків
- `🔄 Рутинна` - повторювана регулярно
- `⚡ Швидка` - менше 15 хвилин
- `🧩 Підзадача` - частина великого проекту
- `⏳ Очікування` - залежить від інших

#### 4. 🔴 Priority (ПРЯМИЙ ВИБІР)
**Формула визначення Priority:**
```javascript
function calculatePriority(task) {
    // Фактори впливу (вага кожного 0-10)
    const urgency = task.deadline_proximity; // Наскільки близький дедлайн
    const impact = task.goal_impact;         // Вплив на ключові цілі
    const effort = task.effort_required;     // Зусилля (інверсія)
    const dependencies = task.blocks_others; // Чи блокує інші задачі
    
    // Розрахунок загального скору
    const score = (urgency * 0.3) + (impact * 0.4) + 
                  ((10 - effort) * 0.2) + (dependencies * 0.1);
    
    // Мапування на Priority
    if (score >= 8) return "High";
    if (score >= 5) return "Medium";
    if (score >= 2) return "Low";
    return "None";
}
```

**Швидке визначення Priority:**
- `High` - Критично для цілей АБО дедлайн < 24 год АБО блокує інших
- `Medium` - Важливо для прогресу АБО дедлайн < 7 днів 
- `Low` - Бажано зробити АБО довгостроковий вплив
- `None` - Можна відкласти без наслідків

#### 5. 🏷️ Context (ЧИСТІ ТЕГИ БЕЗ СПЕЦСИМВОЛІВ!)
**Формат: Окремі теги для кожної категорії**

**А) Категорії проектів (з емодзі):**
```
😎 Життя
👁️‍🗨️ N8N
🦾 GODAI
🎆 Телепортація
📕 AI контент
💡 Заповіді
📆 Дні народження
🏦 SEKTA
📚 Навчання
💰 Фінанси
🧠 Здоров'я
🏕️ Відпочинок
👨‍👩‍👧‍👧 Сім'я
👁️‍🗨️ Цілі 2025
```

**Б) Контексти виконання (з емодзі):**
```
🧠 deep
⚡ quick
📞 call
🎨 creative
📊 analysis
🏃 physical
```

**ПРАВИЛА ТЕГУВАННЯ:**
- Формат: `[Категорія] + [Контекст1] + [Контекст2]`
- Приклад: `[👁️‍🗨️ N8N] + [🧠 deep] + [🎨 creative]`
- Мінімум 1 категорія + 1 контекст
- Максимум 2 категорії + 2 контексти

#### 6. 🍅 Pomodoro Time (Оцінка часу)
**Тільки для типів "Проектна" та "Підзадача":**
- `1🍅` = 30 хвилин
- `2🍅` = 1 година
- `4🍅` = 2 години
- `6🍅` = 3 години
- `8🍅` = 4 години

#### 7. ⚡ Energy (Рівень енергії)
- `🔴 Висока` - ранок, креативні задачі
- `🟡 Середня` - стандартна робота
- `🟢 Низька` - рутина, адмін

#### 8. 💰 ROI Score (1-10)
**Тільки для бізнес-задач:**
- 10 = Критичний вплив на дохід
- 7-9 = Високий ROI
- 4-6 = Середній ROI
- 1-3 = Низький ROI

#### 9. 🔗 Dependencies
**Тільки для типу "Очікування":**
```
Від: [Ім'я/Компанія]
Що: [Конкретно чекаю]
До: [Дедлайн]
План Б: [Альтернатива]
```

#### 10. ✅ DoD (Definition of Done - ОКРЕМЕ ПОЛЕ!)
**НОВИЙ ФОРМАТ v7.1:**
```
🔹 MUST (60%)
1. Створи [конкретна дія]
2. Налаштуй [конкретна дія]

🔹 SHOULD (80%)
3. Запрограмуй [конкретна дія]

🔹 NICE (100%)
4. Оптимізуй [конкретна дія]

Готовність: [  ]% (мінімум 60% для закриття)
```

**Правила DoD v7.1:**
- Дієслово в наказовому способі (Створи, Налаштуй, Склади)
- Максимум 7 слів на пункт
- Нумерований список
- 🔹 замість повних назв

#### 11. ⚡ SPARTAN AI (ОКРЕМЕ ПОЛЕ!)
**Структура AI-допомоги:**
```
🔍 [Проблема] Основний виклик цієї задачі
🎯 [Стратегія] Найефективніший підхід
⚔️ [Екзекуція] Крок 1 → Крок 2 → Крок 3
🚀 [AI-хак] Конкретний інструмент або prompt
```

#### 12. 📝 Description (ГОЛОВНЕ СХОВИЩЕ ІНФОРМАЦІЇ!)
**НОВА СТРУКТУРА v7.1 (порядок критичний!):**

```markdown
✅ DoD (Definition of Done):
[Копія з поля DoD]

🎯 РЕЗУЛЬТАТ: [Що конкретно буде після виконання - 1 речення]

📋 Додаткова інформація:
[Технічні деталі, контекст, посилання - якщо потрібно]

🔗 Dependencies (якщо є):
[Копія з поля Dependencies]

⚡ SPARTAN AI:
[Копія з поля SPARTAN AI]
```

---

## 🤖 SPARTAN INTEGRATION MODULE

### AUTO-ACTIVATION SYSTEM
```javascript
// Workflow автоматично активується при:
const ACTIVATION_TRIGGERS = [
    "notion",
    "задач",
    "створи",
    "додай",
    "планування",
    "todo",
    "ticktick"
];

// Context Memory System
class WorkflowContext {
    constructor() {
        this.sessionHistory = [];
        this.currentDatabase = "🎆 Телепортація";
        this.lastOperation = null;
        this.userPreferences = {};
    }
    
    remember(operation) {
        this.sessionHistory.push({
            timestamp: new Date(),
            type: operation.type,
            data: operation.data,
            result: operation.result
        });
        this.lastOperation = operation;
    }
    
    getContext() {
        return {
            history: this.sessionHistory.slice(-10), // Last 10 operations
            database: this.currentDatabase,
            lastOp: this.lastOperation
        };
    }
}
```

### ARTIFACT PREVIEW SYSTEM
```javascript
function createTaskWithPreview(taskData) {
    // КРОК 1: Генерація preview в artifact
    const preview = {
        title: "📋 Preview: " + taskData.title,
        content: formatTaskForPreview(taskData)
    };
    
    // КРОК 2: Показати користувачу
    showArtifact(preview);
    
    // КРОК 3: Очікування підтвердження
    const userResponse = await getUserConfirmation();
    
    if (userResponse === "approve") {
        // КРОК 4: Створення в Notion
        return createInNotion(taskData);
    } else if (userResponse === "edit") {
        // КРОК 5: Редагування
        return editAndRetry(taskData);
    } else {
        // КРОК 6: Скасування
        return cancelOperation();
    }
}
```

---

## 🛡️ СИСТЕМА ВАЛІДАЦІЇ v7.1

### ✅ АВТОМАТИЧНА ПЕРЕВІРКА ПЕРЕД СТВОРЕННЯМ:

```javascript
function validateTask(task) {
    const errors = [];
    
    // 1. Title валідація
    if (task.title.includes('[') || task.title.includes('🤖')) {
        errors.push("❌ Title містить заборонені символи");
    }
    if (task.title.length > 50) {
        errors.push("❌ Title задовгий (>50 символів)");
    }
    
    // 2. DoD валідація v7.1
    if (!task.dod_field || !task.dod_field.includes('🔹 MUST')) {
        errors.push("❌ DoD не містить 🔹 MUST критеріїв");
    }
    if (!checkImperativeVerbs(task.dod_field)) {
        errors.push("❌ DoD має містити дієслова в наказовому способі");
    }
    
    // 3. Description валідація v7.1
    const correctOrder = ['✅ DoD', '🎯 РЕЗУЛЬТАТ', '📋 Додаткова', '🔗 Dependencies', '⚡ SPARTAN AI'];
    if (!checkDescriptionOrder(task.description, correctOrder)) {
        errors.push("❌ Неправильний порядок блоків в Description");
    }
    
    // 4. Priority валідація
    if (!['High', 'Medium', 'Low', 'None'].includes(task.priority)) {
        errors.push("❌ Priority має неправильне значення");
    }
    
    return errors;
}
```

### 🔄 BATCH PROCESSING З КОНТРОЛЕМ ЯКОСТІ:

```
🔄 BATCH MODE v7.1 + SPARTAN
━━━━━━━━━━━━━━━━━━━━━━━━━━
Всього задач: 35
Батчів: 7 (по 5 задач)

Batch 1/7: Processing...
├─ Task 1: ✓ Validated → 📋 Preview shown
├─ Task 2: ✓ Validated → 📋 Preview shown
├─ Task 3: ⚠️ Fixed DoD → 📋 Preview shown
├─ Task 4: ✓ Validated → 📋 Preview shown
└─ Task 5: ✓ Validated → 📋 Preview shown
[■■■■■] 5/5 ✓ Quality: 96%

⏸️ Пауза для перевірки якості
Продовжити? [Y/N]
```

---

## 🎯 ПРИКЛАДИ ПРАВИЛЬНОГО ЗАПОВНЕННЯ v7.1

### Приклад 1: Технічна задача (N8N)
```yaml
Title: Створити N8N workflow для контент-заводу
Date: 10.07.2025, 09:00-13:00
Type: 🚀 Проектна
Priority: High  # (дедлайн близько + критично для бізнесу)
Context: [👁️‍🗨️ N8N] + [🧠 deep] + [🎨 creative]
Pomodoro: 8🍅
Energy: 🔴 Висока
ROI: 10

DoD:
🔹 MUST (60%)
1. Створи workflow для YouTube, TikTok, Instagram
2. Налаштуй автоматичне нарізання відео

🔹 SHOULD (80%)
3. Запрограмуй розклад публікацій на тиждень

🔹 NICE (100%)
4. Налаштуй A/B тестування заголовків

Готовність: [  ]% (мінімум 60% для закриття)

Dependencies: -

SPARTAN AI:
🔍 [Проблема] Ручна адаптація забирає 3-4 години щодня
🎯 [Стратегія] Єдиний workflow з розумним розподілом
⚔️ [Екзекуція] Аналіз → Архітектура → Імплементація
🚀 [AI-хак] ChatGPT для генерації описів по платформах

Description:
✅ DoD (Definition of Done):
🔹 MUST (60%)
1. Створи workflow для YouTube, TikTok, Instagram
2. Налаштуй автоматичне нарізання відео

🔹 SHOULD (80%)
3. Запрограмуй розклад публікацій на тиждень

🔹 NICE (100%)
4. Налаштуй A/B тестування заголовків

Готовність: [  ]% (мінімум 60% для закриття)

🎯 РЕЗУЛЬТАТ: Повністю автоматизований контент-завод для 3 платформ з одного відео

📋 Додаткова інформація:
• YouTube: довгі відео 10-20 хв
• TikTok: кліпи 15-60 сек з highlights
• Instagram: Reels 30-90 сек + карусель

⚡ SPARTAN AI:
🔍 [Проблема] Ручна адаптація забирає 3-4 години щодня
🎯 [Стратегія] Єдиний workflow з розумним розподілом
⚔️ [Екзекуція] Аналіз → Архітектура → Імплементація
🚀 [AI-хак] ChatGPT для генерації описів по платформах
```

### Приклад 2: Адміністративна задача (Віза)
```yaml
Title: Підготувати документи для візи D7 Португалія
Date: 25.07.2025, 10:00-18:00
Type: 🚀 Проектна
Priority: High  # (критичний дедлайн + блокує переїзд)
Context: [🎆 Телепортація] + [📊 analysis] + [🧠 deep]
Pomodoro: 8🍅
Energy: 🔴 Висока
ROI: 10
Dependencies: VFS Global - запис до 01.08.2025

DoD:
🔹 MUST (60%)
1. Склади список необхідних документів
2. Зібери 10 основних документів

🔹 SHOULD (80%)
3. Замов переклади документів

🔹 NICE (100%)
4. Створи backup копії всього

Готовність: [  ]% (мінімум 60% для закриття)

SPARTAN AI:
🔍 [Проблема] Багато документів потребують перекладу
🎯 [Стратегія] Паралельна обробка всіх треків
⚔️ [Екзекуція] Список → Збір → Переклад → Апостиль
🚀 [AI-хак] Notion tracker з чек-боксами для кожного

Description:
✅ DoD (Definition of Done):
🔹 MUST (60%)
1. Склади список необхідних документів
2. Зібери 10 основних документів

🔹 SHOULD (80%)
3. Замов переклади документів

🔹 NICE (100%)
4. Створи backup копії всього

Готовність: [  ]% (мінімум 60% для закриття)

🎯 РЕЗУЛЬТАТ: Повний пакет документів готовий для подачі на візу D7

📋 Додаткова інформація:
• Паспорт + докази доходу (6 міс)
• Банківські виписки (12 міс)
• Довідка про несудимість + апостиль
• Медстраховка для Португалії

🔗 Dependencies (якщо є):
Від: VFS Global
Що: Підтвердження запису на подачу
До: 01.08.2025
План Б: Подача через консульство напряму

⚡ SPARTAN AI:
🔍 [Проблема] Багато документів потребують перекладу
🎯 [Стратегія] Паралельна обробка всіх треків
⚔️ [Екзекуція] Список → Збір → Переклад → Апостиль
🚀 [AI-хак] Notion tracker з чек-боксами для кожного
```

---

## 📋 КОНТРОЛЬНИЙ ЧЕКЛИСТ v7.1

### Перед створенням КОЖНОЇ задачі:
- [ ] **Title** = тільки дія, без [кодів] та емодзі
- [ ] **Date** = конкретний час або дедлайн
- [ ] **Type** = обрано правильну категорію
- [ ] **Priority** = визначено за формулою (High/Medium/Low/None)
- [ ] **Context** = формат `[Категорія] + [Контекст1] + [Контекст2]`
- [ ] **DoD** = 🔹 MUST/SHOULD/NICE з дієсловами в наказовому способі
- [ ] **SPARTAN AI** = заповнено в окремому полі
- [ ] **Description** = DoD першим, потім інші блоки в правильному порядку
- [ ] **Preview** = artifact створено та перевірено

### При batch processing:
- [ ] Валідація кожної задачі
- [ ] Preview для кожної задачі
- [ ] Пауза кожні 5 задач
- [ ] Перевірка якості батчу
- [ ] Збереження в context memory

### Показники успіху:
- [ ] 100% чистих Title в TickTick
- [ ] 100% правильних Priority
- [ ] 100% правильний порядок Description
- [ ] 100% preview перед створенням
- [ ] 95%+ успішна синхронізація

---

## 🚀 РЕЖИМИ СТВОРЕННЯ ЗАДАЧ

### 🎯 РЕЖИМ 1: SINGLE TASK (Одна задача)
```
1. SPARTAN аналізує контекст
2. Workflow створює preview в artifact
3. Користувач перевіряє
4. Підтвердження → створення в Notion
5. Context memory зберігає операцію
```

### 📦 РЕЖИМ 2: BATCH MODE (5+ задач)
```
1. SPARTAN планує список задач
2. Workflow створює batch preview
3. Валідація кожної задачі
4. Artifact з усіма задачами
5. Поетапне створення з паузами
6. Checkpoint після кожного батчу
```

### 🚨 РЕЖИМ 3: EMERGENCY (Все горить)
```
1. Тільки Title + Date + Priority (High)
2. DoD = 1 MUST критерій
3. Швидкий preview
4. Негайне створення
5. Повернутись пізніше для деталей
```

---

## ⚠️ КРИТИЧНІ ПРАВИЛА v7.1

1. **Title - святе** - НІКОЛИ не додавай туди нічого крім дії
2. **DoD action-oriented** - дієслова в наказовому способі
3. **Description order** - DoD завжди першим
4. **Preview обов'язковий** - кожна задача через artifact
5. **Context memory** - зберігаємо всі операції
6. **SPARTAN compatible** - seamless інтеграція
7. **Auto-activation** - workflow завжди готовий

---

## 🔗 SPARTAN + WORKFLOW = PRODUCTIVITY

```
SPARTAN (планування/аналіз) 
    ↓
WORKFLOW v7.1 (структурування/валідація)
    ↓
ARTIFACT PREVIEW (візуальна перевірка)
    ↓
NOTION (збереження/організація)
    ↓
TICKTICK (виконання/нагадування)
```

---

*v7.1 FINAL - Повна сумісність з v7.0 + критичні виправлення + SPARTAN integration.
Clean titles. Smart priorities. Action-oriented DoD. Preview workflow. Context memory.*
*ADHD-friendly. SPARTAN-compatible. Battle-tested.*