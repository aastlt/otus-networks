# Архитектура сетей

## Планируемая архитектура

построить следующую архитектуру

Сеть office1

192.168.2.0/26 - dev

192.168.2.64/26 - test servers

192.168.2.128/26 - managers

192.168.2.192/26 - office hardware

Сеть office2

192.168.1.0/25 - dev

192.168.1.128/26 - test servers

192.168.1.192/26 - office hardware

Сеть central

192.168.0.0/28 - directors

192.168.0.32/28 - office hardware

192.168.0.64/26 - wifi

```
Office1 ---\
                  -----> Central --IRouter --> internet
Office2----/
```


## Итого должны получится следующие сервера

inetRouter

centralRouter

office1Router

office2Router

centralServer

office1Server

office2Server


## Теоретическая часть

1. Найти свободные подсети.

|Subnet|Min IP|Max IP|Broadcast|Hosts|Mask|
|---|---|---|---|:---:|---|
|192.168.0.16/28|192.168.0.17|192.168.0.30|192.168.0.31|14|255.255.255.240|
|192.168.0.48/28|192.168.0.49|192.168.0.62|192.168.0.63|14|255.255.255.240|
|192.168.0.128/25|192.168.0.129|192.168.0.254|192.168.0.255|126|255.255.255.128|

2. Посчитать сколько узлов в каждой подсети, включая свободные. Указать broadcast адрес для каждой подсети.

Сеть office1

|Name|Subnet|Hosts|Broadcast|Mask|
|---|---|---|---|---|
|dev|192.168.2.0/26|62|192.168.2.63|255.255.255.192|
|test servers|192.168.2.64/26|62|192.168.2.127|255.255.255.192|
|managers|192.168.2.128/26|62|192.168.2.191|255.255.255.192|
|office hardware|192.168.2.192/26|62|192.168.2.255|255.255.255.192|

Сеть office2

|Name|Subnet|Hosts|Broadcast|Mask|
|---|---|---|---|---|
|dev|192.168.1.0/25|126|192.168.1.127|255.255.255.128|
|test servers|192.168.1.128/26|62|192.168.1.191|255.255.255.192|
|office hardware|192.168.1.192/26|62|192.168.1.255|255.255.255.192|

Сеть central

|Name|Subnet|Hosts|Broadcast|Mask|
|---|---|---|---|---|
|directors|192.168.0.0/28|14|192.168.0.15|255.255.255.240|
|office hardware|192.168.0.32/28|14|192.168.0.47|255.255.255.240|
|wifi|192.168.0.64/26|62|192.168.0.127|255.255.255.192|

3. Проверить нет ли ошибок при разбиении.

Ошибок при разбиении сетей не обнаружено.

## Практическая часть

* Соединить офисы в сеть согласно схеме и настроить роутинг

* Все сервера и роутеры должны ходить в инет черз inetRouter

* Все сервера должны видеть друг друга

* У всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи

* При нехватке сетевых интервейсов добавить по несколько адресов на интерфейс

### Для проверки выполнить ```vagrant up``` и запустить ping с любого узла сети до любого другого узла.
