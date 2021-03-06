# Клиент-серверное приложение для текстового чата

## Структура
  Приложение состоит из серверной части, обрабатывающей соединения от клиентов, и клиентской части.
  - server.py
  - client.py
  
  Рассчитано на 10 людей, но значение можно поменять на серверной части в параметре server.listen().

## Описание работы
С помощью сокетов клиент может взаимодействовать с другими клиентами через сервер. Сокет со стороны сервера связывает себя с каким-либо своим портом. Любой клиент с сокетом, связанным с тем же портом, может взаимодействовать с серверным сокетом.

Каждый раз, когда пользователь подключается к серверу, для него создается отдельный поток. Связь от сервера к клиенту происходит по отдельным потокам на основе сокета, созданного для его идентификации.

Для создания чата написано два скрипта: один служит для поддержания работы чата, второй должен быть запущен каждым участником, чтобы подключиться к серверу.

### Сервер
Программа на стороне сервера пытается установить сокет и связать его с IP-адресом клиента и портом. После этого скрипт остается открытым и получает запросы на подключение. Данные клиентов заносятся в соответствующие списки для отслеживания активных подключений. Для каждого участника создается отдельный поток, в каждом из которых сервер ожидает сообщения и отправляет это сообщение в чат.

Если сервер обнаруживает ошибку, то он удаляет пользователя из чата.

Помимо прочего, сервер дополнительно транслирует чат в терминале.

Подробное описание используемых функций дано в самом коде.

### Клиент
Скрипт со стороны пользователя пытается получить доступ к сокету сервера, созданному на IP-адресе и порте. После подключения он постоянно проверяет поступуление ввода с сервера или от клиента. После чего перенаправляет вывод.

Если ввод от пользователя, он отправляет полученное сообщение на сервер.

## Что можно исправить?
Для отображения сообщений на терминале можно добавить шифрование всех сообщений - будет только видно имя и адрес пользователя, отправившего послание.

На данный момент у участника, отправившего сообщение, оно видится дважды: когда он его вводит и когда это сообщение рассылается всем участникам (ему в том числе). Нужно исключить пользователя из рассылки своих сообщений.

Необходимо также добавить возможность выхода не только путем закрытия терминала: использовать стоп-слово по типу 'exit', и, если полученная строка совпадает с ним, то исключать клиента из чата и оповещать об этом.
  
  
