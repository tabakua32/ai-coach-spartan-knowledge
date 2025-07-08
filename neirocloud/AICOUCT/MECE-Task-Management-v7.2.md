# MECE TASK MANAGEMENT SYSTEM v7.2
## Enhanced v7.1 + Complex Projects + All Operations + 99.99% Validation

### 🚀 НОВІ МОЖЛИВОСТІ v7.2

1. **Complex Project Management**
   - Автоматичне визначення складності (8+ Pomodoros)
   - Префікс-система: [P1] → [P1.1] → [P1.1.1]
   - Smart context inheritance + overrides
   - Batch creation з візуалізацією ієрархії

2. **Duplicate Management**
   - Auto-detection: same context + similar title
   - Smart merge: Full (повне злиття) або Hierarchical (parent-child)
   - Preview перед merge
   - Automatic cleanup

3. **Enhanced Validation (99.99% accuracy)**
   - Validation Gate: 4 обов'язкові кроки
   - No direct API calls - тільки через wrapper
   - Auto-fix common errors
   - Mandatory preview artifacts

4. **All Task Operations**
   - CREATE: single, batch, complex, template
   - UPDATE: fields, bulk, convert to project
   - MERGE: full, hierarchical
   - SPLIT: by DoD, by time, by context
   - MOVE: between projects, to archive
   - SEARCH: by title, context, date, overdue

5. **SPARTAN Integration++**
   - Auto-activation enhanced
   - Context memory expanded
   - Validation enforcement
   - Error prevention protocols

---

## 🛡️ VALIDATION GATE SYSTEM (NEW!)

### ОБОВ'ЯЗКОВІ КРОКИ ПЕРЕД СТВОРЕННЯМ:

```javascript
class TaskValidationGate {
    constructor() {
        this.required_gates = {
            "workflow_loaded": false,      // v7.2 файл завантажено
            "fields_validated": false,     // всі поля перевірені
            "preview_shown": false,        // artifact показано
            "user_confirmed": false        // явне підтвердження
        };
        this.validation_errors = [];
    }
    
    can_proceed() {
        if (!all(this.required_gates.values())) {
            const failed = this.required_gates.filter(g => !g.value);
            throw new Error(`BLOCKED: Не пройдені gates: ${failed}`);
        }
        return true;
    }
}
```

### AUTO-FIX СИСТЕМА:

```javascript
function autoFixCommonErrors(task) {
    // Title: видалити емодзі на початку
    task.title = task.title.replace(/^[^\w\s]+\s*/, '');
    
    // Priority: default якщо відсутній
    if (!task.priority) {
        task.priority = "Medium";
    }
    
    // Context: конвертувати старий формат
    if (task.context && (task.context.includes('СМ_') || task.context.includes('ВХ_'))) {
        task.context = convertOldContextFormat(task.context);
    }
    
    // DoD: обрізати до 7 слів
    if (task.dod_items) {
        task.dod_items = task.dod_items.map(item => 
            item.split(' ').slice(0, 7).join(' ')
        );
    }
    
    return task;
}
```

---

## 📊 СТРУКТУРА ПОЛІВ NOTION v7.2 (INHERITED FROM v7.1)

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

**NEW v7.2: Auto-fix видаляє емодзі автоматично!**

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

**NEW v7.2: Default = "Medium" якщо не вказано!**

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

**NEW v7.2: Підзадачі можуть мати власні контексти!**

#### 6. 🍅 Pomodoro Time (Оцінка часу)
**Тільки для типів "Проектна" та "Підзадача":**
- `1🍅` = 30 хвилин
- `2🍅` = 1 година
- `4🍅` = 2 години
- `6🍅` = 3 години
- `8🍅` = 4 години

**NEW v7.2: 8+ 🍅 автоматично активує префікс-систему!**

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
🔹 MUST - 60%
1. Створи [конкретна дія]
2. Налаштуй [конкретна дія]

🔹 SHOULD - 80%
3. Запрограмуй [конкретна дія]

🔹 NICE - 100%
4. Оптимізуй [конкретна дія]

Достатньо виконати 60%
```

**Правила DoD v7.1:**
- Дієслово в наказовому способі (Створи, Налаштуй, Склади)
- Максимум 7 слів на пункт
- Нумерований список
- 🔹 замість повних назв

**NEW v7.2: Для складних проектів DoD перетворюється в підзадачі!**

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

## 🚀 COMPLEX PROJECT MANAGEMENT (NEW!)

### АВТОМАТИЧНЕ ВИЗНАЧЕННЯ СКЛАДНОСТІ:

```javascript
class ComplexProjectHandler {
    analyzeComplexity(task) {
        let score = 0;
        
        // Критерії складності
        if (task.pomodoro_time >= 8) score += 3;
        if (task.dod_must_items.length > 3) score += 2;
        if (task.task_type === '🚀 Проектна') score += 1;
        
        return {
            is_complex: score >= 4,
            score: score,
            recommendation: score >= 4 ? 'PREFIX_SYSTEM' : 'SIMPLE_DOD'
        };
    }
}
```

### ПРЕФІКС-СИСТЕМА ДЛЯ СКЛАДНИХ ПРОЕКТІВ:

```
Проект: [P1] Розробити курс з AI автоматизації

Підзадачі 1-го рівня:
├── [P1.1] Створити структуру курсу
├── [P1.2] Записати відео-уроки
├── [P1.3] Розробити практичні завдання
└── [P1.4] Запустити продажі

Підзадачі 2-го рівня:
├── [P1.1.1] Проаналізувати конкурентів
├── [P1.1.2] Визначити унікальну пропозицію
└── [P1.1.3] Створити детальний план модулів
```

### ПРАВИЛА ПРЕФІКСІВ:
1. **Parent task**: [P{number}] на початку Title
2. **Level 1 subtasks**: [P{number}.{sub}] 
3. **Level 2 subtasks**: [P{number}.{sub}.{subsub}]
4. **Priority**: Успадковується від parent
5. **Context**: Може мати власний або успадковувати

---

## 🔄 DUPLICATE MANAGEMENT (NEW!)

### АВТОМАТИЧНЕ ВИЯВЛЕННЯ ДУБЛІКАТІВ:

```javascript
class DuplicateDetector {
    findPotentialDuplicates(newTask, existingTasks) {
        const duplicates = [];
        
        for (const existing of existingTasks) {
            if (this.sameContext(newTask, existing)) {
                const similarity = this.calculateTitleSimilarity(
                    newTask.title, 
                    existing.title
                );
                if (similarity > 0.7) {
                    duplicates.push({
                        task: existing,
                        similarity: similarity,
                        merge_type: this.suggestMergeType(newTask, existing)
                    });
                }
            }
        }
        
        return duplicates;
    }
}
```

### ТИПИ ОБ'ЄДНАННЯ:

1. **FULL MERGE** (Повне злиття)
   - Коли задачі майже ідентичні (>80% схожості)
   - Об'єднуються всі поля
   - Зберігається найвищий Priority
   - DoD комбінуються

2. **HIERARCHICAL** (Ієрархічне)
   - Коли задачі про одне, але різні аспекти
   - Одна стає parent, інша subtask
   - Зберігаються обидві з префіксами
   - Контексти можуть відрізнятись

---

## 🤖 SPARTAN INTEGRATION MODULE v7.2

### AUTO-ACTIVATION SYSTEM (ENHANCED):
```javascript
// Workflow автоматично активується при:
const ACTIVATION_TRIGGERS = [
    "notion", "задач", "створи", "додай",
    "планування", "todo", "ticktick",
    // NEW in v7.2:
    "об'єднай", "merge", "розбий", "split",
    "підзадач", "проект", "складн"
];

// Context Memory System (EXPANDED)
class WorkflowContext {
    constructor() {
        this.sessionHistory = [];
        this.currentDatabase = "🎆 Телепортація";
        this.lastOperation = null;
        this.userPreferences = {};
        // NEW in v7.2:
        this.projectCounter = 0;
        this.mergeHistory = [];
        this.validationStats = {
            total: 0,
            passed: 0,
            auto_fixed: 0,
            blocked: 0
        };
    }
}
```

### SAFE TASK CREATOR (NEW!):
```javascript
function createNotionTaskSAFE(taskData) {
    // КРОК 1: Validation Gate
    if (!validationGate.canProceed()) {
        throw new Error("Validation gates not passed");
    }
    
    // КРОК 2: Auto-fix
    taskData = autoFixCommonErrors(taskData);
    
    // КРОК 3: Final validation
    const errors = validateAllFieldsV72(taskData);
    if (errors.length > 0) {
        return {error: "Validation failed", issues: errors};
    }
    
    // КРОК 4: Create
    return notionAPI.createPage(taskData);
}
```

---

## 🛡️ СИСТЕМА ВАЛІДАЦІЇ v7.2

### ✅ РОЗШИРЕНА АВТОМАТИЧНА ПЕРЕВІРКА:

```javascript
function validateTaskV72(task) {
    const errors = [];
    
    // 1. Title валідація (ENHANCED)
    if (/^[^\w\s]/.test(task.title)) {
        errors.push("❌ Title починається з емодзі або спецсимволу");
    }
    if (task.title.includes('[') || task.title.includes(']')) {
        errors.push("❌ Title містить квадратні дужки");
    }
    if (task.title.length > 50) {
        errors.push("❌ Title задовгий (>50 символів)");
    }
    
    // 2. Priority валідація (NEW)
    if (!task.priority) {
        errors.push("⚠️ Priority не вказано - буде встановлено Medium");
    }
    
    // 3. Complex project валідація (NEW)
    if (task.pomodoro_time >= 8 && !task.title.includes('[P')) {
        errors.push("⚠️ Складний проект - рекомендується префікс-система");
    }
    
    // 4. DoD валідація v7.1
    if (!task.dod_field || !task.dod_field.includes('🔹 MUST')) {
        errors.push("❌ DoD не містить 🔹 MUST критеріїв");
    }
    
    // 5. Description order валідація
    const correctOrder = ['✅ DoD', '🎯 РЕЗУЛЬТАТ', '📋 Додаткова', '🔗 Dependencies', '⚡ SPARTAN AI'];
    if (!checkDescriptionOrder(task.description, correctOrder)) {
        errors.push("❌ Неправильний порядок блоків в Description");
    }
    
    return errors;
}
```

### 🔄 ALL OPERATIONS SUPPORT:

```javascript
const SUPPORTED_OPERATIONS = {
    CREATE: {
        single: createSingleTask,
        batch: createBatchTasks,
        complex: createComplexProject,
        template: createFromTemplate
    },
    UPDATE: {
        fields: updateTaskFields,
        bulk: bulkUpdateTasks,
        convert: convertToProject
    },
    MERGE: {
        full: fullMergeTasks,
        hierarchical: hierarchicalMerge
    },
    SPLIT: {
        byDoD: splitByDoD,
        byTime: splitByTimeEstimate,
        byContext: splitByContext
    },
    MOVE: {
        toProject: moveToProject,
        toArchive: archiveTask,
        betweenDatabases: moveBetweenDatabases
    },
    SEARCH: {
        byTitle: searchByTitle,
        byContext: searchByContext,
        overdue: findOverdueTasks,
        byDate: searchByDateRange
    }
};
```

---

## 🎯 ПРИКЛАДИ ВИКОРИСТАННЯ v7.2

### Приклад 1: Складний проект (автоматичні підзадачі)
```yaml
USER: "Створи задачу: Розробити курс з AI автоматизації (15 годин роботи)"

SYSTEM RESPONSE:
🔍 Виявлено складний проект (15 годин = 30🍅)
📊 Рекомендую використати префікс-систему

PREVIEW ARTIFACT:
┌─────────────────────────────────────────────────────┐
│ 📋 Preview: Complex Project Structure                │
├─────────────────────────────────────────────────────┤
│ [P1] Розробити курс з AI автоматизації             │
│ Priority: High | 30🍅 | 🎆 Телепортація            │
│                                                     │
│ Автоматично створені підзадачі:                     │
│ ├── [P1.1] Створити структуру курсу (4🍅)          │
│ ├── [P1.2] Записати теоретичні модулі (8🍅)        │
│ ├── [P1.3] Розробити практичні завдання (6🍅)      │
│ ├── [P1.4] Створити додаткові матеріали (4🍅)      │
│ └── [P1.5] Налаштувати платформу продажів (8🍅)    │
│                                                     │
│ [Approve] [Edit] [Cancel]                           │
└─────────────────────────────────────────────────────┘
```

### Приклад 2: Виявлення та об'єднання дублікатів
```yaml
USER: "Створи задачу: Підготувати презентацію для інвесторів"

SYSTEM RESPONSE:
⚠️ Знайдено потенційний дублікат:

EXISTING: "Зробити pitch deck для інвесторів" 
Context: [🦾 GODAI] + [🎨 creative]
Created: 2 дні тому
Status: In Progress

SIMILARITY: 85%

Рекомендую FULL MERGE:
┌─────────────────────────────────────────────────────┐
│ 📋 Merge Preview                                    │
├─────────────────────────────────────────────────────┤
│ RESULT: "Підготувати презентацію для інвесторів"   │
│ Priority: High (збережено вищий)                    │
│ DoD: Об'єднано критерії з обох задач               │
│ Progress: 40% (збережено прогрес)                  │
│                                                     │
│ [Merge] [Create New] [Cancel]                       │
└─────────────────────────────────────────────────────┘
```

### Приклад 3: Auto-fix помилок
```yaml
USER: "Створи задачу: 🎉 Організувати вечірку з друзями"

SYSTEM AUTO-FIX:
✅ Видалено емодзі з початку Title
✅ Priority встановлено: Medium (default)
✅ Context визначено автоматично: [😎 Життя] + [🎨 creative]

PREVIEW ARTIFACT:
┌─────────────────────────────────────────────────────┐
│ 📋 Preview: Task (auto-fixed)                       │
├─────────────────────────────────────────────────────┤
│ Title: Організувати вечірку з друзями               │
│ Date: 15.07.2025, весь день                         │
│ Type: 🚀 Проектна                                   │
│ Priority: Medium ⚠️ (auto-set)                      │
│ Context: [😎 Життя] + [🎨 creative]                 │
│                                                     │
│ ⚠️ Auto-fixes applied:                              │
│ • Removed emoji from Title                          │
│ • Set default Priority                              │
│                                                     │
│ [Approve] [Edit] [Cancel]                           │
└─────────────────────────────────────────────────────┘
```

---

## 📋 КОНТРОЛЬНИЙ ЧЕКЛИСТ v7.2

### Перед створенням КОЖНОЇ задачі:
- [ ] **Workflow v7.2 loaded** - файл завантажено
- [ ] **Validation Gate initialized** - всі 4 gates ready
- [ ] **Complexity check** - перевірено на 8+ pomodoros
- [ ] **Duplicate check** - перевірено існуючі задачі
- [ ] **Auto-fix applied** - помилки виправлені
- [ ] **Preview shown** - artifact обов'язково
- [ ] **User confirmed** - явне підтвердження
- [ ] **Safe create** - тільки через wrapper

### При complex projects:
- [ ] Префікс-система активована
- [ ] Підзадачі згенеровані з DoD
- [ ] Priority успадкований
- [ ] Context визначений для кожної
- [ ] Preview показує всю ієрархію

### При merge operations:
- [ ] Duplicates виявлені автоматично
- [ ] Similarity % розрахований
- [ ] Merge type визначений
- [ ] Preview порівняння показаний
- [ ] Історія збережена

### Показники успіху v7.2:
- [ ] 99.99% задач без помилок
- [ ] 100% preview перед створенням
- [ ] 95%+ auto-fix успішних
- [ ] 0% прямих API викликів
- [ ] 100% validation gate compliance

---

## 🚨 КРИТИЧНІ ПРАВИЛА v7.2

1. **NO DIRECT API** - НІКОЛИ не викликати notionApi напряму
2. **Validation Gate MANDATORY** - всі 4 кроки обов'язкові
3. **Auto-fix FIRST** - виправляти помилки автоматично
4. **Preview ALWAYS** - кожна операція через artifact
5. **Complex = Prefix** - 8+ pomodoros → префікс-система
6. **Merge smart** - автоматичне виявлення дублікатів
7. **Context inheritance** - підзадачі можуть override

---

## 🔐 SAFETY PROTOCOLS v7.2

### BLOCKED OPERATIONS:
```javascript
// ЦЕ ЗАБОРОНЕНО:
notionApi.createPage(task); // ❌ BLOCKED

// ТІЛЬКИ ТАК:
createNotionTaskSAFE(task); // ✅ ALLOWED
```

### ERROR HANDLING:
```javascript
try {
    result = createNotionTaskSAFE(task);
} catch (error) {
    if (error.includes("Validation gates")) {
        // Show gates status to user
        showValidationGateStatus();
    } else if (error.includes("Validation failed")) {
        // Show specific errors
        showValidationErrors(error.issues);
    }
}
```

### BYPASS PREVENTION:
```javascript
// Перехоплення всіх спроб обійти систему
window.notionApi = new Proxy(window.notionApi, {
    get(target, prop) {
        if (prop === 'createPage' && isTaskCreation()) {
            throw new Error("USE createNotionTaskSAFE INSTEAD!");
        }
        return target[prop];
    }
});
```

---

## 🔗 INTEGRATION FLOW v7.2

```
USER INPUT
    ↓
SPARTAN ANALYSIS (context + intent)
    ↓
WORKFLOW v7.2 ACTIVATION
    ↓
OPERATION DETECTION (create/merge/split/etc)
    ↓
VALIDATION GATE CHECK
    ↓
COMPLEXITY ANALYSIS (8+ pomodoros?)
    ↓
DUPLICATE DETECTION (if create)
    ↓
AUTO-FIX ERRORS
    ↓
PREVIEW ARTIFACT (mandatory)
    ↓
USER CONFIRMATION
    ↓
SAFE OPERATION EXECUTION
    ↓
CONTEXT MEMORY UPDATE
    ↓
SUCCESS METRICS TRACKING
```

---

*v7.2 PRODUCTION - Full v7.1 compatibility + Complex projects + All operations + 99.99% validation.*
*No direct API. Preview mandatory. Auto-fix enabled. Duplicate detection. Prefix system.*
*SPARTAN-integrated. Battle-tested. Error-proof.*