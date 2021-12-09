## _Руководство по установке и настройке MySQL в Ubuntu 20.04_

MySQL -- реляционная система управления базами данных. Обычно используется в качестве сервера, к котормоу обращаются локальные или удаленные пользователи.

Для получения рабочей базы данных, необходимо не только установить MySQL, но и настроить систему так, чтобы эффективно использовать ее в своих проектах.
 
 ## Подготовка к установке MySQL
 Итак, конечно же понадобится сервер Ubuntu 20.04, non-root user с правами администратора и  брандмауэр. Для настройки брандмауэра используйтие утилиту UFW. 
 Перед установкой рекомендую обновить индекс пакетов на вашем сервере:
 ```sh
 sudo apt update
```
 ## Установка MySQL
Установите MySQL сервер командой:
  ```sh
 sudo apt install mysql-server
```
Команда не запросит у вас настроки конфигураций, по умалчанию установит последнюю версию MySQL сервера. Ответ терминала будет примерно такой:
```sh
Reading package lists... Done
Building dependency tree
Reading state information... Done
mysql-server is already the newest version (8.0.27-0ubuntu0.20.04.1).
0 upgraded, 0 newly installed, 0 to remove and 44 not upgraded.
root@user:/home/user#
```
Заметьте, на момент написания инструкции была возможна версия MySQL 8.0.27. Следующим шагом настроим конфигурацию, чтобы сделть сервер более защищенным.

 ## Настройка MySQL
 Настраивать базу данных будем  вручную с помощью запуска встроенного скрипта безопасности. Таким образом сможем вносить изменения в ряд наиболее важных для защиты опций. При установке сервера настройки безопасности были сгенерированы по умолчанию. К примеру,  в качестве пароля система использует, как правило, имя пользователя. К сожалению, ваша база данных будет успешна взломана с ненадежным паролем.
 
 Запускаем систему безопасности MySQL:
 ```sh
 sudo mysql_secure_installation
```
После активации команды вам будут предложены опции для настройки. Через серию диалоговых окон поэтапно отрегулируете небходимые функции. Первая опция, предложенная терминалом -- настройка валидации пароля. Вас спросят, хотите ли вы настроить проверку сложности пароля? Вы можете как согласиться,так и отказаться. В моем случае плагин валидации уже был установлен на сервере. Следовательно, последующие шаги будут выполняться с существующей конфигурацией. Поэтому я сразу приступила к созданию пароля для пользователя root MySQL.

 ```sh
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.
The 'validate_password' component is installed on the server.
The subsequent steps will run with the existing configuration
of the component.
Please set the password for root here.
```
После ввода пароля сразу получаю информацию о его надежности. Если пароль не достаточно надежный,то нажмите любую клавишу кроме Y  и попытайтесь создать более безопасный пароль.  Для создания устойчивого к атакам из вне пароля, используйте строчные и заглавные буквы, цифры, специальные символы. Также  пароль должен быть не менее восьми символов.

После создания пароля вы получите ответ о степени его надежностив числовом эквиваленте.
Пример надежного пароля:
```sh
New password:

Re-enter new password:

Estimated strength of the password: 100
```
Пример не очень надежного пароля:
```sh
New password:

Re-enter new password:

Estimated strength of the password: 25
```
Если вы удовлетворены надежность пароля, то нажмите Y.

Следующие вопросы не требуют особых дествий. Достаточно ответить да -- это Y или нет -- это любая клавиша. Ниже приведен список вопросов с сохранением последовательности их повяления в терминале.
- Желаете ли вы удалить анонимных пользователей?
- Хотели бы вы запретить удаленный вход root?
- Удалить тестовую базу данных и получить к ней доступ?
- Cогласны ли вы загрузить новые правила, чтобы внесенные изменения немедленно активировались в MySQL?

Подравляем, вы настроили базу данных!