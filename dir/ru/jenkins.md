

## 1. Установка Java
Jenkins является Java-приложением и требует наличия **Java 17 или 21 (LTS)**.

### Проверка наличия Java:
```bash
java -version
```

### Установка через Homebrew:
Если Java не установлена, выполните:
```bash
brew install openjdk@21
```

### Настройка путей (PATH):
Добавьте Java в переменные окружения, чтобы система видела её.

**Для Apple Silicon (M1/M2/M3):**
```bash
echo 'export PATH="/opt/homebrew/opt/openjdk@21/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**Для Intel Mac:**
```bash
echo 'export PATH="/usr/local/opt/openjdk@21/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

---

## 2. Установка Jenkins
Добавьте репозиторий и установите стабильную LTS-версию:

```bash
brew tap jenkins-x/jx
brew install jenkins-lts
```

---

## 3. Управление сервисом
Рекомендуется запускать Jenkins как фоновый сервис macOS.

* **Запуск:** `brew services start jenkins-lts`
* **Остановка:** `brew services stop jenkins-lts`
* **Перезапуск:** `brew services restart jenkins-lts`
* **Проверка статуса:** `brew services list`

---

## 4. Первоначальная настройка
1.  Откройте браузер и перейдите по адресу: [http://localhost:8080](http://localhost:8080)
2.  **Разблокировка:** Jenkins потребует пароль администратора. Получите его командой:
    ```bash
    cat ~/.jenkins/secrets/initialAdminPassword
    ```
3.  **Плагины:** Выберите "Install suggested plugins" (Установить рекомендуемые плагины).
4.  **Пользователь:** Создайте учетную запись администратора.

---

## 5. Работа с логами
Если возникают ошибки, проверьте логи:

**Apple Silicon:**
```bash
tail -f /opt/homebrew/var/log/jenkins-lts.log
```

**Intel Mac:**
```bash
tail -f /usr/local/var/log/jenkins-lts.log
```

---

## Альтернатива: Запуск через Docker
Если вы предпочитаете контейнеризацию:

```bash
docker run -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts
```

---

## Решение проблем
* **Порт 8080 занят:** Измените порт при запуске:
    `JENKINS_PORT=9090 brew services restart jenkins-lts`
* **Ошибка архитектуры (M1/M2/M3):** Попробуйте принудительную установку:
    `arch -arm64 brew install jenkins-lts`


