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

4. Настроим интерфейс fa0/0 на маршрутизаторе. Поднимем его и присвоим ip адрес:
```
CMERouter(config)#int fa0/0
CMERouter(config-if)#ip address 192.168.0.1 255.255.255.0
CMERouter(config-if)#no shutdown
```

5. На маршрутизаторе настроим DHCP сервера для передачи голоса и данных:
```
CMERouter(config)#ip dhcp pool phones
CMERouter(dhcp-config)#network 192.168.1.0 255.255.255.0
CMERouter(dhcp-config)#default-router 192.168.1.1
CMERouter(dhcp-config)#option 150 ip 192.168.1.1
```

6. На маршрутизаторе настроим услуги телефонии Cisco CallManager Express с помощью команд:
```
CMERouter(config)#telephony-service
CMERouter(config-telephony)#max-dn 5
CMERouter(config-telephony)#max-ephones 5
CMERouter(config-telephony)#ip source-address 192.168.10.1 port 2000
CMERouter(config-telephony)#auto assign 1 to 5
```

7. Теперь на коммутаторе создаем VLAN порты для взаимодействия коммутатора с маршрутизатором и подключаем IP телефоны. Порты переводим в режим acess и прокидываем voice канал:
```
Switch(config)#interface range FastEthernet 0/1-4
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport voice vlan 1
```

8. Настраиваем телефоны. На коммутаторе присваиваем каждому номер:
```
CMERouter(config)#ephone-dn 1
CMERouter(config-ephone-dn)#number 101
CMERouter(config-ephone-dn)#exit
CMERouter(config)#ephone-dn 2
CMERouter(config-ephone-dn)#number 102
CMERouter(config-ephone-dn)#exit
CMERouter(config)#ephone-dn 3
CMERouter(config-ephone-dn)#number 103
CMERouter(config-ephone-dn)#exit
```

9. Теперь видим, что каждому телефону был присвоен ip адрес на vlan 1 и номер. Проверим звонки между телефонами.

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/a5d33dae-494a-48a1-bc54-31da5c684018)

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/30e62273-3c0c-470f-81cf-43a6130f56bb)

![Снимок экрана 2024-02-26 151859](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/722d74b1-c612-4410-b4bd-5ba21e27a29e)

  


