
Чтобы проверить добавление и удаление, в usecases.yaml должны быть:

useCases:
  - entity: Student
    operation: create
  - entity: Student
    operation: read
  - entity: Student
    operation: delete

Если delete нет — endpoint DELETE /api/students/{id} не сгенерируется.

1. Проверить список студентов

curl http://localhost:8080/api/students

Ожидаемо сначала:

[]

2. Добавить студента

curl -X POST http://localhost:8080/api/students \
-H "Content-Type: application/json" \
-d '{"name":"Anna","email":"anna@example.com"}'

Ожидаемый результат:

{"id":1,"name":"Anna","email":"anna@example.com"}

3. Проверить, что студент добавился

curl http://localhost:8080/api/students

4. Удалить студента

curl -X DELETE http://localhost:8080/api/students/1

5. Проверить, что удалился

curl http://localhost:8080/api/students

Ожидаемо:

[]

Проверка validation

У тебя для Student.email стоит pattern: email, а name required/min/max.

Проверь плохие данные:

curl -X POST http://localhost:8080/api/students \
-H "Content-Type: application/json" \
-d '{"name":"A","email":"wrong"}'

Ожидаемо должен быть:

400 Bad Request

Если DELETE не работает, добавь operation: delete в usecases.yaml, перегенерируй приложение и перезапусти Spring Boot.
