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

## 3. Запуск приложения

<table cellpadding="10">
  <tr>
    <td><img width="1915" height="1013" alt="image" src="https://github.com/user-attachments/assets/fb71d599-a549-4d7a-9ea2-65034c5514fd" /></td>
  </tr>
</table>

## 4. Проверка HTTPS-маршрута

<table cellpadding="10">
  <tr>
    <td><img width="974" height="523" alt="image" src="https://github.com/user-attachments/assets/75337c3a-0e0d-465a-b4b3-d1751d72ef22" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="522" alt="image" src="https://github.com/user-attachments/assets/f51033f2-6726-4138-9ea4-fe0df04200ef" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/0eb85b1c-f5ca-4310-a037-e944a1ed55da" /></td>
  </tr>
</table>
