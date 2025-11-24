JavaLibrarySite это реализация сайта-библиотеки книг с настроенной коммуникацией с сервисами юзеров и книг.

Сервисы:
- [JavaBookService](https://github.com/GigaGitCoder/JavaBookService)
- [JavaUserService](https://github.com/GigaGitCoder/JavaUserService)

# Особенности:

- При первом запуске сервисов и сайта, первого админа следует создать через POST запрос `ip-user-service:8092/api/admin/registerAsAdmin/` с соответствующим body контентом.
- Запросы из .js файлов проксируются Controller файлами и перенаправляются на ip контейнеров. По надобности стоит поменять ссылки для запросов в Controller файлах.
- Ошибки пока не имеют четких пояснений ясных для любого пользователя.
