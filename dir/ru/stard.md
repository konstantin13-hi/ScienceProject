

## 1. Перегенерировать приложение

Перейди в cg-source-repo:

cd ~/science_project/cg-source-repo

Активируй venv:

source .venv/bin/activate

Запусти генератор:

python generator/generate.py artifacts/model.yaml ../generated-app-repo

Если всё ок — появятся сообщения генерации.

⸻

## 2. Запустить Spring Boot заново

Перейди в generated repo:

cd ../generated-app-repo

Запусти:

mvn spring-boot:run

Дождись:

Started UniversityDemoApplication



с управлением через usecases.yaml.

Это уже очень сильная часть PoC для диплома.
