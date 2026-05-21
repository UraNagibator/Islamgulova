Автор: Исламгулова Дарина Сергеевна
Дата создания: 18.05.2026
```markdown
# enhance-repo – Git Cherry-pick и разрешение конфликтов

Демонстрационный проект для отработки навыков работы с Git: клонирование репозитория, создание ветки, выполнение cherry-pick с разрешением конфликтов и отправка изменений через Visual Studio.

## Задача

1. Клонировать удалённый репозиторий
2. Создать ветку `enhance` и добавить файл `Feature.cs`
3. Выполнить `git cherry-pick` коммита из ветки `feature-old`
4. Разрешить конфликты (если возникнут)
5. Отправить изменения в удалённый репозиторий через Visual Studio

## Исходные данные

- **Удалённый репозиторий:** `https://github.com/user/enhance-repo.git`
- **Рабочая ветка:** `enhance`
- **Ветка-источник для cherry-pick:** `feature-old`
- **Файл:** `Feature.cs`
- **Начальное содержимое:** `Console.WriteLine("New feature");`

## Структура проекта

```
enhance-repo/
├── .git/
├── Feature.cs
└── README.md
```

## Пошаговое выполнение

### 1. Клонирование репозитория

**Командная строка:**
```bash
git clone https://github.com/user/enhance-repo.git
cd enhance-repo
```

**В Visual Studio:**
- `Team Explorer → Connect → Clone` → вставить URL `https://github.com/user/enhance-repo.git`
- Выбрать локальную папку → `Clone`

---

### 2. Создание ветки `enhance` и добавление файла `Feature.cs`

**Командная строка:**
```bash
git checkout -b enhance
echo 'Console.WriteLine("New feature");' > Feature.cs
git add Feature.cs
git commit -m "Add Feature.cs with initial content"
```

**В Visual Studio:**
- `Team Explorer → Branches → New Branch` → имя `enhance` → `Create Branch`
- `Solution Explorer` → добавить новый файл `Feature.cs`
- Вставить содержимое: `Console.WriteLine("New feature");`
- `Team Explorer → Changes` → сообщение `Add Feature.cs with initial content` → `Commit All`

---

### 3. Выполнение cherry-pick коммита из ветки `feature-old`

**Предварительные шаги — найти нужный коммит:**

```bash
# Загрузить все ветки с удалённого репозитория
git fetch origin

# Просмотреть историю ветки feature-old
git log origin/feature-old --oneline
# Пример вывода:
# 1a2b3c4d Update feature implementation
# e5f6g7h Previous commit
```

**Выполнение cherry-pick (находясь на ветке `enhance`):**
```bash
git checkout enhance
git cherry-pick 1a2b3c4d   # замените на реальный хэш коммита
```

**В Visual Studio:**
- `Team Explorer → Branches` → переключиться на `enhance`
- `Git Repository (Ctrl+0, Ctrl+R)` → найти нужный коммит в ветке `feature-old`
- Кликнуть правой кнопкой по коммиту → `Cherry-pick`

---

### 4. Разрешение конфликтов (если возникли)

При конфликте Git выведет сообщение:
```
Auto-merging Feature.cs
CONFLICT (content): Merge conflict in Feature.cs
error: could not apply 1a2b3c4d... Update feature implementation
```

**Проверка состояния:**
```bash
git status
# Вывод: both modified: Feature.cs
```

**Содержимое файла `Feature.cs` с маркерами конфликта:**
```csharp
<<<<<<< HEAD
Console.WriteLine("New feature");
=======
Console.WriteLine("Old feature from feature-old");
>>>>>>> 1a2b3c4d (Update feature implementation)
```

**Разрешение конфликта — итоговый вариант:**
```csharp
Console.WriteLine("New feature from enhance and feature-old combined");
```

**Завершение cherry-pick:**
```bash
git add Feature.cs
git cherry-pick --continue
```

**В Visual Studio:**
- В окне `Changes` отобразятся конфликтующие файлы
- Открыть `Feature.cs` → убрать маркеры `<<<<<<<`, `=======`, `>>>>>>>`
- Оставить нужный код или объединить оба варианта
- Нажать `Commit All` — Team Explorer автоматически продолжит cherry-pick

**Отмена cherry-pick при необходимости:**
```bash
git cherry-pick --abort
```

---

### 5. Отправка изменений в удалённый репозиторий

**Командная строка:**
```bash
git push origin enhance
```

**В Visual Studio:**
- `Team Explorer → Sync` → `Push`
- Если ветка `enhance` существует только локально — Visual Studio предложит `Publish Branch`
- Нажать `Push` → ветка `enhance` появится на GitHub

---

## Полный скрипт решения (командная строка)

```bash
# 1. Клонирование
git clone https://github.com/user/enhance-repo.git
cd enhance-repo

# 2. Создание ветки enhance и коммит Feature.cs
git checkout -b enhance
echo 'Console.WriteLine("New feature");' > Feature.cs
git add Feature.cs
git commit -m "Add Feature.cs with initial content"

# 3. Cherry-pick из feature-old (замените хэш на реальный)
git fetch origin
git cherry-pick 1a2b3c4d

# 4. Если конфликт:
# - отредактировать Feature.cs вручную
# - git add Feature.cs
# - git cherry-pick --continue

# 5. Отправка изменений
git push origin enhance
```

---

## Итоговый файл `Feature.cs` (после успешного cherry-pick и разрешения конфликта)

```csharp
Console.WriteLine("New feature from enhance and feature-old combined");
```

## Граф коммитов (схематично)

```
* (enhance) New feature from enhance and feature-old combined  ← cherry-pick из feature-old
* Add Feature.cs with initial content                          ← создан в enhance
* ... (предыдущие коммиты main)
```

---
---

## Примечания

- **Cherry-pick** позволяет перенести конкретный коммит из одной ветки в другую без полного слияния веток
- **Конфликты при cherry-pick** решаются так же, как и при слиянии — через ручное редактирование файла
- **Visual Studio** предоставляет графический интерфейс для cherry-pick через контекстное меню в окне Git Repository
- Все операции можно выполнять как через командную строку, так и через интерфейс Visual Studio
```


git commit -m "Add README.md with project documentation"
git push
```
