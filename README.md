# 🎵 Online Music Library API (Go)

REST API для управления библиотекой песен с интеграцией внешнего музыкального сервиса.  
**Техническое задание**: [ТЗ Effective Mobile GO.pdf](ТЗ%20Effective%20Mobile%20GO.pdf)

---

## 🚀 Features
- 📌 **CRUD операций** с песнями (добавление, удаление, редактирование)
- 🔍 **Фильтрация и пагинация** по всем полям
- ♪ **Получение текста песни** с пагинацией по куплетам
- 🌐 **Интеграция с внешним API** для обогащения данных (release date, текст, YouTube-ссылка)
- 🐘 **Автомиграции PostgreSQL** при старте сервиса
- 📝 **Swagger-документация**
- ⚙ **Конфигурация через .env**

---

## 📦 Технологический стек
| Компонент       | Технологии                          |
|-----------------|-------------------------------------|
| Фреймворк       | `chi` + `render`                    |
| База данных     | PostgreSQL + `golang-migrate`       |
| Логирование     | `slog` (structured logging)         |
| Конфигурация    | `.env` + `github.com/caarlos0/env`  |
| Документация    | `swaggo/swag`                       |
| Тестирование    | `httptest` + `testcontainers`       |

---

## 🛠 Установка
1. **Клонировать репозиторий**:
   ```bash
   git clone https://github.com/Xeney/Music-Library-API.git
   cd Music-Library-API
   ```

2. **Настроить окружение**:
   - Создать `.env` файл (см. [.env.example](.env.example)):
     ```ini
     DB_HOST=localhost
     DB_PORT=5432
     DB_USER=postgres
     DB_PASSWORD=postgres
     DB_NAME=Music-Library-API
     EXTERNAL_API_URL=http://Music-Library-API-info:8080/info
     ```

3. **Запустить PostgreSQL**:
   ```bash
   docker-compose up -d
   ```

4. **Применить миграции**:
   ```bash
   make migrate-up
   ```

5. **Запустить сервис**:
   ```bash
   go run cmd/main.go
   ```

---

## 📚 API Endpoints
| Метод | Путь                   | Описание                          |
|-------|-------------------------|-----------------------------------|
| GET   | `/songs`                | Список песен (фильтрация + пагинация) |
| GET   | `/songs/{id}/lyrics`    | Текст песни с пагинацией куплетов |
| POST  | `/songs`                | Добавление новой песни            |
| PUT   | `/songs/{id}`           | Обновление данных песни           |
| DELETE| `/songs/{id}`           | Удаление песни                    |

### 📄 Пример запроса (POST /songs)
```json
{
    "group": "Muse",
    "song": "Supermassive Black Hole"
}
```

---

## 📊 Swagger Docs
Документация доступна после запуска сервиса:  
🔗 [http://localhost:8080/swagger/index.html](http://localhost:8080/swagger/index.html)

## 🧪 Тестирование
```bash
# Юнит-тесты
go test -v ./...

# Интеграционные тесты (требует Docker)
make test-integration
```

---

## 🏗 Структура проекта
```
Music-Library-API/
├── cmd/
│   └── main.go          # Точка входа
├── internal/
│   ├── api/             # HTTP-обработчики
│   ├── db/              # Миграции + репозиторий
│   ├── models/          # Сущности БД
│   └── service/         # Бизнес-логика
├── migrations/          # SQL-миграции
├── pkg/                 # Вспомогательные пакеты
└── docs/                # Swagger-документация
```

---

## 📜 Лицензия
MIT License. Подробнее в файле LICENSE.
