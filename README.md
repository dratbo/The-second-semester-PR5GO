<h1 align="center"> Привет! Я <a target="_blank"> Кармеев Артур из группы ЭФМО-01-25 </a> 
<img src="https://github.com/blackcater/blackcater/raw/main/images/Hi.gif" height="32"/></h1>
<h3 align="center"> Данная практика была легкой :frog: </h3>

<h3 align="center"> Практическая работа №5: Реализация HTTPS (TLS-сертификаты). Защита от SQL-инъекций </h3>

Структура работы:

    └── pz5-security/
        ├── go.mod
        ├── go.sum
        ├── sql/
        │   └── init.sql
        ├── certs/
        │   ├── server.crt
        │   └── server.key
        ├── .idea/
        │   ├── .gitignore
        │   ├── modules.xml
        │   ├── pz5-security.iml
        │   └── workspace.xml
        ├── internal/
        │   ├── student/
        │   │   ├── model.go
        │   │   └── repo.go
        │   ├── httpapi/
        │   │   └── handler.go
        │   └── config/
        │       └── config.go
        └── cmd/
            └── server/
                └── main.go


## 1. Создание базы данных, запуск SQL-скрипта

<table cellpadding="10">
  <tr>
    <td><img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/aa5bebb5-0f22-4dab-9533-98fb70640ce5" /></td>
  </tr>
</table>

## 2. Генерация учебного TLS-сертификата

С помощью треёх запретных букв скачали openssl, указали путь PATH, прописали команду `openssl req -x509 -newkey rsa:2048 -nodes -keyout certs/server.key -out certs/server.crt -days 365 -subj "/CN=localhost"`

<table cellpadding="10">
  <tr>
    <td><img width="1915" height="1015" alt="image" src="https://github.com/user-attachments/assets/f4e7d5ba-120c-45fe-87f7-f14a7e92596b" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="1915" height="1014" alt="image" src="https://github.com/user-attachments/assets/13c43c01-33d6-4935-becd-98264c1eb3e2" /></td>
  </tr>
</table>

