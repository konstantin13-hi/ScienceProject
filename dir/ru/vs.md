# Roadmap & Future Versions

В данном разделе представлен план поэтапного развития прототипа от текущего состояния (PoC) до полнофункциональной системы автоматизации CG/CI/CD.

---

## 🚀 Текущее состояние (Version 1: Core PoC)
**Фокус:** Генерация базового CRUD backend-приложения из структурной модели предметной области.
- **Вход:** `model.yaml` (сущности и поля) + `domain.puml` (UML-документация).
- **Выход:** Spring Boot REST API (GET, POST, DELETE), интеграция с БД (H2).

---

## 📈 План развития (Roadmap)

### Version 2: Управление доступом через Use Cases
Добавление файла `usecases.yaml` для управления генерацией эндпоинтов.
- **Логика:** Генерируются только те операции, которые явно описаны в сценариях использования.
- *Пример:* Если в `usecases.yaml` указан только `ViewStudents`, эндпоинты на удаление созданы не будут.

### Version 3: Полный цикл CRUD
Расширение набора стандартных операций.
- **Добавление:** Реализация метода `PUT` для обновления данных.
- **Результат:** Поддержка полного цикла обработки данных: Create, Read, Update, Delete.

### Version 4: Валидация данных
Внедрение правил проверки полей на уровне модели.
- **Вход:** Описание ограничений в YAML (например, `required: true`, `pattern: email`).
- **Эффект:** Автоматическая генерация аннотаций Bean Validation (`@NotNull`, `@Email`, `@Size`) в Java-коде.

### Version 5: Связи между сущностями (Relationships)
Переход от плоских таблиц к реляционной структуре.
- **Поддержка:** Описание связей `OneToMany`, `ManyToMany` в модели.
- **Эффект:** Генерация JPA-аннотаций и логики связывания объектов в Service-слое.
- Но пока нет:

* cascade
* join tables customization
* bidirectional sync logic
* advanced service logic
* DTO mapping
* lazy/eager configs

### Version 6: Генерация Frontend-слоя
Расширение системы до Full-stack генерации.
- **Результат:** Автоматическое создание пользовательских интерфейсов (React/HTML forms + tables) на основе структуры `model.yaml`.

### Version 7: Интеграция с профессиональными CASE-средствами
Переход от ручного редактирования YAML к использованию специализированного ПО.
- **Инструменты:** Enterprise Architect, Visual Paradigm, StarUML.
- **Процесс:** `Export UML/XMI` → `Generator` → `Full Application`.

---

## 📝 Заключение для отчета (Summary)
> *The first version of the prototype focuses on generation of CRUD backend applications from a structural domain model. Future versions may extend the pipeline with use case artifacts, field validation rules, entity relationships, frontend generation and integration with CASE tools.*
