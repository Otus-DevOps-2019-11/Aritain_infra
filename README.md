# Aritain_infra
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

Aritain Infra repository

Доступ на интернал-хост в GCP осуществляется при помощи команды
ssh -t -i ~/.ssh/Ganhart -A Ganhart@*Внешний IP-адрес bastion* ssh *Внутренний IP-адрес интернал-хоста*

Для простоты был создал соответствующий алиас в конфиге ssh
ssh someinternalhost

Конфиг SSH выглядит следующим образом:
host bastion
        User Ganhart
        HostName 35.210.214.67
        Port 22
        IdentityFile ~/.ssh/Ganhart
        ForwardAgent yes

host someinternalhost
        User Ganhart
        hostname 10.132.0.4
        Port 22
        ProxyJump bastion

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

Разные полезные вещи:
----------
Добавить SSH ключ для проброса в GCP

eval $(ssh-agent)
ssh-add ~/.ssh/Ganhart
ssh-add -L - проверка
----------
