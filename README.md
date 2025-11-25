<div align="center">
  
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white) ![Thymeleaf](https://img.shields.io/badge/Thymeleaf-%23364437.svg?style=for-the-badge&logo=thymeleaf&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)


[![License](https://img.shields.io/badge/license-GNU%20GPL%20v3.0-brightgreen)](LICENSE) ![Stars](https://img.shields.io/github/stars/GigaGitCoder/JavaLibrarySite)
</div>

JavaLibrarySite is a library web application built with Spring and Thymeleaf. The site communicates with two microservices to manage users and books.

## Related Services

The project uses the following microservices:
- [JavaBookService](https://github.com/GigaGitCoder/JavaBookService) — book management
- [JavaUserService](https://github.com/GigaGitCoder/JavaUserService) — user management and authentication

## Initial Setup

### Creating the First Administrator

After the first launch of all services, you need to create an administrator account:

**Endpoint:**
```http
POST http://ip-user-service:8092/api/admin/registerAsAdmin/
Content-Type: application/json
```

**Request Body:**
```json
{
    "nickname": "admin",
    "email": "admin@example.com",
    "password": "your_secure_password"
}
```

## Architecture

### Request Proxying

The site uses Controllers to proxy requests from JavaScript files to microservices:

- JavaScript files send requests to local Controllers
- Controllers forward requests to Docker container IP addresses
- Containers process requests and return results

**Important:** When changing Docker configuration or ports, you must update the URLs in Controller files.

### Request Flow

```
Browser → JavaScript → Controller (Proxy) → Microservice (Docker) → Database
```

## Known Limitations

- **Error Handling:** In the current version, error messages may not be clear enough for end users. It is recommended to add more informative error descriptions.

## Configuration

### Configuring Microservice URLs

If you changed service ports or IP addresses, update the corresponding URLs in Controller files:

**Example:**
```java
// In BookController.java file
private static final String BOOK_SERVICE_URL = "http://book-service:8090";

// In UserController.java file
private static final String USER_SERVICE_URL = "http://user-service:8092";
```

## Technology Stack

- **Frontend:** Thymeleaf, JavaScript
- **Backend:** Spring Boot, Spring MVC
- **Architecture:** Microservices
- **Containerization:** Docker

# Localizations

- [Русский](./README-files/README_RU.md)
- [中文](./README-files/README_ZH.md)