# osinkina.a-itmo-megaolymp-devops-2026

! скриншоты с соответствующими происходящему на снимке названиями хранятся в ./screens !
(спасибо за понимание)

1. создадим репозиторий, авторизуемся с помощью токена github на удалённом сервере (vps). для удобства будем работать с репозиторием и с локальной машины (подгрузка снимков экрана), и с удалённой (конфиги)

2. создадим группу admins (user test-admin), ![alt text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/admin-sudo.png. создавать будем с помощью команды sudo useradd test_developer -d /home/test_developer -m, затем назначим нужную группу с помощью usermod.

с помощью sudo visudo отредактируем файл, добавив права на исполнение sudo команд: ![alt text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/visudo.png. Этот же трюк используем и для developers (user test-developer)

!в линуксе нельзя создавать вложенные подгруппы, поэтому в качестве альтернативы выдадим developers права на запуск докер-команд. они могут писать sudo docker ..., но им не нужно вводить пароль для sudo!
![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/developer-run-docker.png

сделаем возможность логина только под ssh (так как это безопаснее, чем пароль, и снижает риск несанкционированного доступа к серверу), создадим в корневых директориях пользователей папки .ssh, где впоследствии будут находиться публичные ключи для подлкючения по протоколу, а также known-hosts.

3. установим docker, docker-compose, добавим docker.service в автозапуск: ![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/docker-auto.png

права на докер мы выдали admins и developers ещё на предыдущем пункте.
возьмём готовый образ nexus и сделаем проксирование докер-контейнеров:

![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/nexus.png
![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/nexus-proxy.png

это всё по-хорошему нужно детальнее настраивать, но мы ограничены по времени.

4. установим grafana, prometheus (более привычный мне инструмент). напишем docker-compose для запуска графаны (также возьмём её готовый образ):
  ![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/docker-compose-grafana.png

добавим тестовый дашборд:
![alt-text] https://github.com/nastosinka/osinkina.a-itmo-megaolymp-devops-2026/blob/main/screens/grafana.png

  очень хотелось настроить больше дашбордов на реальных данных, но у меня не хватает времени

  !дашборд в формате yaml, не json (автогенерация, открыла порт 3000 через ufw для gui grafana)


