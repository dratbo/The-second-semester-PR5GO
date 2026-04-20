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

## 5. Проверка безопасного запроса к БД

<table cellpadding="10">
  <tr>
    <td><img width="974" height="515" alt="image" src="https://github.com/user-attachments/assets/b5ca074f-e147-4aa6-8ae7-3e073dd18d46" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="522" alt="image" src="https://github.com/user-attachments/assets/2e1b5682-e51b-47fa-a9b6-cf03b4ff580c" />
</td>
  </tr>
</table>

## 6. Дополнительное задание 

Вариант 1. Добавить HTTPS-редирект
Реализуйте отдельный HTTP-сервер на порту 8080, который будет перенаправлять все запросы на https://localhost:8443.

### Доп задание далось нелегко, пришлось гуглить и разбираться :monocle_face:

6.1 Создаём redirectMux — маршрутизатор, который на любой запрос ("/") вызывает функцию редиректа

6.2 Функция редиректа:
- Берёт исходный путь r.URL.Path и параметры r.URL.RawQuery
- Склеивает "https://localhost:8443" + путь + параметры
- Отправляет ответ с кодом 301 Moved Permanently и заголовком Location

6.3 HTTP-сервер слушает порт :8080 и использует redirectMux

6.4 Запуск HTTP-сервера в горутине (go func()) позволяет ему работать параллельно с HTTPS-сервером

6.5 HTTPS-сервер запускается как обычно в основном потоке

<table cellpadding="10">
  <tr>
    <td><img width="974" height="513" alt="image" src="https://github.com/user-attachments/assets/9ca18d76-0652-44d9-b9cf-02bd47e3d39f" /></td>
  </tr>
</table>

Откроем в браузере  http://localhost:8080/health

<table cellpadding="10">
  <tr>
    <td><img width="974" height="522" alt="image" src="https://github.com/user-attachments/assets/b3820515-d1ba-40d5-9f01-09d8e1840818" /></td>
  </tr>
</table>

Всё, осталось самое сложное :no_good:

## Контрольные вопросы 🦧

Вопрос 1. Чем HTTP отличается от HTTPS?

HTTP передаёт данные без криптографической защиты, поэтому содержимое запроса и ответа может быть прочитано или изменено при перехвате трафика. HTTPS использует TLS для шифрования канала, что обеспечивает защиту данных от прослушивания и подмены.

Вопрос 2. Какую роль выполняет TLS в защищённом соединении?

TLS обеспечивает криптографическую защиту сетевого взаимодействия: шифрует передаваемые данные, подтверждает подлинность сервера (с помощью сертификата) и гарантирует целостность сообщений.

Вопрос 3. Что такое TLS-сертификат?

TLS-сертификат — это криптографический объект, используемый для подтверждения идентичности сервера и установления защищённого соединения. Он содержит открытый ключ и информацию о владельце.

Вопрос 4. Что делает tls.LoadX509KeyPair?

Функция `tls.LoadX509KeyPair(certFile, keyFile)` читает и парсит пару открытого (сертификат) и закрытого (ключ) ключей из файлов, содержащих PEM-кодированные данные, и возвращает объект `tls.Certificate` для использования в TLS-конфигурации сервера.

Вопрос 5. Почему self-signed certificate подходит для локальной учебной среды, но не для публичного production-сервиса?

Самоподписанный сертификат не заверен ни одним доверенным удостоверяющим центром (CA). Браузеры и клиенты выдают предупреждение о безопасности, так как не могут проверить подлинность сервера. В production для доверия пользователей и корректной работы требуется сертификат, подписанный публичным CA.

Вопрос 6. Что такое SQL-инъекция?

SQL-инъекция — это вид атаки, при котором злоумышленник внедряет в запрос произвольный SQL-код через небезопасную подстановку пользовательского ввода, что может привести к чтению, изменению или удалению данных, а также к выполнению произвольных команд.

Вопрос 7. Почему конкатенация строки SQL с пользовательским вводом опасна?

Конкатенация позволяет злоумышленнику подставить в запрос специальные символы и SQL-команды (например, `' OR 1=1; --`), изменяя логику запроса. Это даёт возможность обойти проверки, получить несанкционированный доступ или повредить базу данных.

Вопрос 8. Что такое parameterized query?

Параметризованный запрос — это способ выполнения SQL, при котором текст запроса и значения параметров передаются в СУБД раздельно. Значения интерпретируются только как данные, а не как часть SQL-синтаксиса, что полностью предотвращает SQL-инъекции.

Вопрос 9. Что такое prepared statement?

Prepared statement — это SQL-выражение, которое предварительно разбирается и сохраняется СУБД. Затем его можно многократно выполнять с разными параметрами, передавая их отдельно. В Go `db.Prepare()` возвращает `*sql.Stmt`, который после использования нужно закрывать `stmt.Close()`.

Вопрос 10. Почему placeholder syntax может отличаться в разных СУБД и драйверах?

Синтаксис плейсхолдеров зависит от драйвера и СУБД, потому что каждая СУБД реализует свой протокол и способ передачи параметров. Например, PostgreSQL использует `$1`, `$2`, MySQL — `?`, SQLite — `?` или именованные параметры. Драйверы Go следуют этим особенностям.
