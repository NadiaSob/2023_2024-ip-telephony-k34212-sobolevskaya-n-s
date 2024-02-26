University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)

Year: 2023/2024

Group: K34212

Author: Sobolevskaya Nadezhda Sergeevna

Lab: Lab2

Date of create: 26.02.2024

Date of finished: 

# Отчет по лабораторной работе №2: "Конфигурация voip в среде Сisco packet tracer"

## Цель работы
Иизучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.

## Ход работы

### Часть 1

1. Соберем схему соединения (для маршрутизатора задаем имя CMERouter):

   ![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/53d533e2-3802-41f6-b5ee-b8a1499136a0)

2. Для отключения синтаксиса ввода слов от DNS серверов, на маршрутизаторе выполним команду:
```
CMERouter(config)#no ip domain-lookup
```

3. Зададим пароли для защиты маршрутизатора как в удаленном режиме, так и в режиме консоли с помощью команд:
```
CMERouter(config)#line vty 0 4
CMERouter(config-line)#password admin
CMERouter(config-line)#login
CMERouter(config-line)#exit
CMERouter(config)#line console 0
CMERouter(config-line)#password admin
CMERouter(config-line)#login
```





