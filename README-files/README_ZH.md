<div align="center">
  
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white) ![Thymeleaf](https://img.shields.io/badge/Thymeleaf-%23364437.svg?style=for-the-badge&logo=thymeleaf&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)


[![License](https://img.shields.io/badge/license-GNU%20GPL%20v3.0-brightgreen)](LICENSE) ![Stars](https://img.shields.io/github/stars/GigaGitCoder/JavaLibrarySite)
</div>


JavaLibrarySite 是一个使用 Spring 和 Thymeleaf 构建的图书馆 Web 应用程序。该网站与两个微服务通信以管理用户和图书。

## 相关服务

该项目使用以下微服务：
- [JavaBookService](https://github.com/GigaGitCoder/JavaBookService) — 图书管理
- [JavaUserService](https://github.com/GigaGitCoder/JavaUserService) — 用户管理和身份验证

## 初始设置

### 创建第一个管理员

在首次启动所有服务后，需要创建管理员帐户：

**端点：**
```http
POST http://ip-user-service:8092/api/admin/registerAsAdmin/
Content-Type: application/json
```

**请求体：**
```json
{
    "nickname": "admin",
    "email": "admin@example.com",
    "password": "your_secure_password"
}
```

## 架构

### 请求代理

该网站使用 Controller 将来自 JavaScript 文件的请求代理到微服务：

- JavaScript 文件向本地 Controller 发送请求
- Controller 将请求转发到 Docker 容器 IP 地址
- 容器处理请求并返回结果

**重要：** 更改 Docker 配置或端口时，必须更新 Controller 文件中的 URL。

### 请求流程

```
浏览器 → JavaScript → Controller（代理）→ 微服务（Docker）→ 数据库
```

## 已知限制

- **错误处理：** 在当前版本中，错误消息对最终用户可能不够清晰。建议添加更详细的错误描述。

## 配置

### 配置微服务 URL

如果您更改了服务端口或 IP 地址，请更新 Controller 文件中的相应 URL：

**示例：**
```java
// 在 BookController.java 文件中
private static final String BOOK_SERVICE_URL = "http://book-service:8090";

// 在 UserController.java 文件中
private static final String USER_SERVICE_URL = "http://user-service:8092";
```

## 技术栈

- **前端：** Thymeleaf、JavaScript
- **后端：** Spring Boot、Spring MVC
- **架构：** 微服务
- **容器化：** Docker