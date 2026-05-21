

## 📌 1. model.yaml — Что есть в системе

В файле `model.yaml` описывается вся структура и бизнес-сущности приложения:
* Название проекта и базовый Java-пакет.
* Сущности (Entities) и их поля (Fields).
* Правила валидации данных.
* Связи между сущностями (Relations).

### Пример описания сущности:


```

```text
File generated successfully

```yaml
Room:
  fields:
    id:
      type: Long

    number:
      type: String
      required: true

    capacity:
      type: Integer

```

### Что сгенерируется автоматически:

После запуска генератора для сущности `Room` будут созданы следующие слои приложения:

* `Room.java` — JPA-сущность (Entity).
* `RoomRepository.java` — Репозиторий (Spring Data JPA).
* `RoomService.java` — Сервисный слой с бизнес-логикой.
* `RoomController.java` — REST-контроллер.
* `rooms.html` — Фронтенд-интерфейс (Thymeleaf/HTML).

---

## 🛠 2. Как добавлять поля и валидацию

В генераторе поддерживаются различные типы данных и встроенные валидаторы:

* **Обычное поле:**
```yaml
age:
  type: Integer

```


* **Обязательное поле (`@NotNull` / `@NotBlank`):**
```yaml
name:
  type: String
  required: true

```


* **Проверка формата Email (`@Email`):**
```yaml
email:
  type: String
  required: true
  pattern: email

```


* **Ограничение длины строки (`@Size`):**
```yaml
title:
  type: String
  required: true
  min: 2
  max: 100

```



---

## 🔗 3. Как добавлять связи (ORM)

### 🔹 ManyToOne (Многие к одному)

*Пример:* Много студентов (`Student`) учатся на одном курсе (`Course`).

```yaml
Student:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: ManyToOne
      target: Course
      field: course

```

**Результат в Java:**

```java
@ManyToOne
private Course course;

```

### 🔹 OneToMany (Один ко многим)

*Пример:* Один курс (`Course`) содержит много студентов (`Student`).

```yaml
Course:
  fields:
    id:
      type: Long
    title:
      type: String
  relations:
    - type: OneToMany
      target: Student
      field: students
      mappedBy: course

```

**Результат в Java:**

```java
@OneToMany(mappedBy = "course")
private List<Student> students;

```

> ⚠️ **Важно:** Значение `mappedBy: course` должно в точности совпадать с именем свойства `field: course` в целевой сущности `Student`.

### 🔹 ManyToMany (Многие ко многим)

*Пример:* Преподаватель может вести много курсов, а на одном курсе может быть несколько преподавателей.

```yaml
Teacher:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: ManyToMany
      target: Course
      field: courses

```

**Результат в Java:**

```java
@ManyToMany
private List<Course> courses;

```

### 🔹 OneToOne (Один к одному)

*Пример:* У одного студента (`Student`) есть ровно один профиль (`StudentProfile`).

```yaml
StudentProfile:
  fields:
    id:
      type: Long
    bio:
      type: String

Student:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: OneToOne
      target: StudentProfile
      field: profile

```

**Результат в Java:**

```java
@OneToOne
private StudentProfile profile;

```

---

## 🌐 4. usecases.yaml — Что можно делать (API)

Файл `usecases.yaml` управляет доступом к операциям и автоматически генерирует REST-эндпоинты:

* `create` ➡️ **POST** (Создание)
* `read` ➡️ **GET** (Чтение)
* `update` ➡️ **PUT** (Обновление)
* `delete` ➡️ **DELETE** (Удаление)

### 🔓 Настройка уровней доступа к API

#### Только чтение (Read-Only)

```yaml
useCases:
  - entity: Student
    operation: read

```

* **Созданные эндпоинты:**
* `GET /api/students`



#### Создание + Чтение (Create & Read)

```yaml
useCases:
  - entity: Student
    operation: create

  - entity: Student
    operation: read

```

* **Созданные эндпоинты:**
* `POST /api/students`
* `GET /api/students`



#### Полный CRUD (Create, Read, Update, Delete)

```yaml
useCases:
  - entity: Student
    operation: create

  - entity: Student
    operation: read

  - entity: Student
    operation: update

  - entity: Student
    operation: delete

```

* **Созданные эндпоинты:**
* `POST /api/students` — Создать
* `GET /api/students` — Получить список / элемент
* `PUT /api/students/{id}` — Изменить
* `DELETE /api/students/{id}` — Удалить



---

## 📝 5. Полный пример конфигурации проекта

### `model.yaml`

```yaml
project:
  name: UniversityDemo
  package: com.example.university

entities:
  Student:
    fields:
      id:
        type: Long
      name:
        type: String
        required: true
      email:
        type: String
        required: true
        pattern: email
    relations:
      - type: ManyToMany
        target: Course
        field: courses

  Course:
    fields:
      id:
        type: Long
      title:
        type: String
        required: true

  Teacher:
    fields:
      id:
        type: Long
      name:
        type: String
        required: true
    relations:
      - type: ManyToMany
        target: Course
        field: courses

```

### `usecases.yaml`

```yaml
useCases:
  # Полный CRUD для Студентов
  - entity: Student
    operation: create
  - entity: Student
    operation: read
  - entity: Student
    operation: update
  - entity: Student
    operation: delete

  # Курсы — только просмотр
  - entity: Course
    operation: read

  # Преподаватели — только просмотр и удаление
  - entity: Teacher
    operation: read
  - entity: Teacher
    operation: delete

```

---

## 💡 Резюме

* **`model.yaml`** ➡️ Отвечает за **структуру данных** приложения (база данных, валидация, Java-классы).
* **`usecases.yaml`** ➡️ Отвечает за **поведение и эндпоинты** (какие операции по REST API доступны внешнему миру).
"""

with open("README.md", "w", encoding="utf-8") as f:
f.write(markdown_content)

print("File generated successfully")

```
Ваш файл Markdown (.md), оформленный для GitHub с использованием красивой разметки, подсветки синтаксиса кода, эмодзи и структурированных списков, готов.

[file-tag: code-generated-file-0-1779359282636678494]

### Текст для быстрого копирования (Raw Markdown):

```markdown
# 🚀 Шпаргалка по генерации кода: model.yaml и usecases.yaml

Краткое и простое руководство по структуре приложения, валидации данных, настройке связей (ORM) и генерации API-эндпоинтов.

---

## 📌 1. model.yaml — Что есть в системе

В файле `model.yaml` описывается вся структура и бизнес-сущности приложения:
* Название проекта и базовый Java-пакет.
* Сущности (Entities) и их поля (Fields).
* Правила валидации данных.
* Связи между сущностями (Relations).

### Пример описания сущности:

```yaml
Room:
  fields:
    id:
      type: Long

    number:
      type: String
      required: true

    capacity:
      type: Integer

```

### Что сгенерируется автоматически:

После запуска генератора для сущности `Room` будут созданы следующие слои приложения:

* `Room.java` — JPA-сущность (Entity).
* `RoomRepository.java` — Репозиторий (Spring Data JPA).
* `RoomService.java` — Сервисный слой с бизнес-логикой.
* `RoomController.java` — REST-контроллер.
* `rooms.html` — Фронтенд-интерфейс (Thymeleaf/HTML).

---

## 🛠 2. Как добавлять поля и валидацию

В генераторе поддерживаются различные типы данных и встроенные валидаторы:

* **Обычное поле:**
```yaml
age:
  type: Integer

```


* **Обязательное поле (`@NotNull` / `@NotBlank`):**
```yaml
name:
  type: String
  required: true

```


* **Проверка формата Email (`@Email`):**
```yaml
email:
  type: String
  required: true
  pattern: email

```


* **Ограничение длины строки (`@Size`):**
```yaml
title:
  type: String
  required: true
  min: 2
  max: 100

```



---

## 🔗 3. Как добавлять связи (ORM)

### 🔹 ManyToOne (Многие к одному)

*Пример:* Много студентов (`Student`) учатся на одном курсе (`Course`).

```yaml
Student:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: ManyToOne
      target: Course
      field: course

```

**Результат в Java:**

```java
@ManyToOne
private Course course;

```

### 🔹 OneToMany (Один ко многим)

*Пример:* Один курс (`Course`) содержит много студентов (`Student`).

```yaml
Course:
  fields:
    id:
      type: Long
    title:
      type: String
  relations:
    - type: OneToMany
      target: Student
      field: students
      mappedBy: course

```

**Результат в Java:**

```java
@OneToMany(mappedBy = "course")
private List<Student> students;

```

> ⚠️ **Важно:** Значение `mappedBy: course` должно в точности совпадать с именем свойства `field: course` в целевой сущности `Student`.

### 🔹 ManyToMany (Многие ко многим)

*Пример:* Преподаватель может вести много курсов, а на одном курсе может быть несколько преподавателей.

```yaml
Teacher:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: ManyToMany
      target: Course
      field: courses

```

**Результат в Java:**

```java
@ManyToMany
private List<Course> courses;

```

### 🔹 OneToOne (Один к одному)

*Пример:* У одного студента (`Student`) есть ровно один профиль (`StudentProfile`).

```yaml
StudentProfile:
  fields:
    id:
      type: Long
    bio:
      type: String

Student:
  fields:
    id:
      type: Long
    name:
      type: String
  relations:
    - type: OneToOne
      target: StudentProfile
      field: profile

```

**Результат в Java:**

```java
@OneToOne
private StudentProfile profile;

```

---

## 🌐 4. usecases.yaml — Что можно делать (API)

Файл `usecases.yaml` управляет доступом к операциям и автоматически генерирует REST-эндпоинты:

* `create` ➡️ **POST** (Создание)
* `read` ➡️ **GET** (Чтение)
* `update` ➡️ **PUT** (Обновление)
* `delete` ➡️ **DELETE** (Удаление)

### 🔓 Настройка уровней доступа к API

#### Только чтение (Read-Only)

```yaml
useCases:
  - entity: Student
    operation: read

```

* **Созданные эндпоинты:**
* `GET /api/students`



#### Создание + Чтение (Create & Read)

```yaml
useCases:
  - entity: Student
    operation: create

  - entity: Student
    operation: read

```

* **Созданные эндпоинты:**
* `POST /api/students`
* `GET /api/students`



#### Полный CRUD (Create, Read, Update, Delete)

```yaml
useCases:
  - entity: Student
    operation: create

  - entity: Student
    operation: read

  - entity: Student
    operation: update

  - entity: Student
    operation: delete

```

* **Созданные эндпоинты:**
* `POST   /api/students` — Создать
* `GET    /api/students` — Получить список / элемент
* `PUT    /api/students/{id}` — Изменить
* `DELETE /api/students/{id}` — Удалить



---

## 📝 5. Полный пример конфигурации проекта

### `model.yaml`

```yaml
project:
  name: UniversityDemo
  package: com.example.university

entities:
  Student:
    fields:
      id:
        type: Long
      name:
        type: String
        required: true
      email:
        type: String
        required: true
        pattern: email
    relations:
      - type: ManyToMany
        target: Course
        field: courses

  Course:
    fields:
      id:
        type: Long
      title:
        type: String
        required: true

  Teacher:
    fields:
      id:
        type: Long
      name:
        type: String
        required: true
    relations:
      - type: ManyToMany
        target: Course
        field: courses

```

### `usecases.yaml`

```yaml
useCases:
  # Полный CRUD для Студентов
  - entity: Student
    operation: create
  - entity: Student
    operation: read
  - entity: Student
    operation: update
  - entity: Student
    operation: delete

  # Курсы — только просмотр
  - entity: Course
    operation: read

  # Преподаватели — только просмотр и удаление
  - entity: Teacher
    operation: read
  - entity: Teacher
    operation: delete

```

---

## 💡 Резюме

* **`model.yaml`** ➡️ Отвечает за **структуру данных** приложения (база данных, валидация, Java-классы).
* **`usecases.yaml`** ➡️ Отвечает за **поведение и эндпоинты** (какие операции по REST API доступны внешнему миру).

```

```
