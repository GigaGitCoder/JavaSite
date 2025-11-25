<div align="center">
  
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white) ![Thymeleaf](https://img.shields.io/badge/Thymeleaf-%23364437.svg?style=for-the-badge&logo=thymeleaf&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)


[![License](https://img.shields.io/badge/license-GNU%20GPL%20v3.0-brightgreen)](LICENSE) ![Stars](https://img.shields.io/github/stars/GigaGitCoder/JavaLibrarySite)
</div>


JavaLibrarySite — это веб-приложение библиотеки книг, построенное с использованием Spring и Thymeleaf. Сайт взаимодействует с двумя микросервисами для управления пользователями и книгами.

## Связанные сервисы

Проект использует следующие микросервисы:
- [JavaBookService](https://github.com/GigaGitCoder/JavaBookService) — управление книгами
- [JavaUserService](https://github.com/GigaGitCoder/JavaUserService) — управление пользователями и аутентификация

## Первоначальная настройка

### Создание первого администратора

После первого запуска всех сервисов необходимо создать учётную запись администратора:

**Эндпоинт:**
```http
POST http://ip-user-service:8092/api/admin/registerAsAdmin/
Content-Type: application/json
```

**Тело запроса:**
```json
{
    "nickname": "admin",
    "email": "admin@example.com",
    "password": "your_secure_password"
}
```

## Архитектура

### Проксирование запросов

Сайт использует Controller'ы для проксирования запросов из JavaScript файлов к микросервисам:

- JavaScript файлы отправляют запросы к локальным Controller'ам
- Controller'ы перенаправляют запросы на IP-адреса Docker контейнеров
- Контейнеры обрабатывают запросы и возвращают результаты

**Важно:** При изменении конфигурации Docker или портов необходимо обновить URL-адреса в Controller файлах.

### Структура запросов

```
Браузер → JavaScript → Controller (Proxy) → Микросервис (Docker) → База данных
```

## Известные ограничения

- **Обработка ошибок:** В текущей версии сообщения об ошибках могут быть недостаточно понятными для конечных пользователей. Рекомендуется добавить более информативные описания ошибок.

## Конфигурация

### Настройка URL микросервисов

Если вы изменили порты или IP-адреса сервисов, обновите соответствующие URL в Controller файлах:

**Пример:**
```java
// В файле BookController.java
private static final String BOOK_SERVICE_URL = "http://book-service:8090";

// В файле UserController.java
private static final String USER_SERVICE_URL = "http://user-service:8092";
```

## Технологический стек

- **Frontend:** Thymeleaf, JavaScript
- **Backend:** Spring Boot, Spring MVC
- **Архитектура:** Микросервисная
- **Контейнеризация:** Docker