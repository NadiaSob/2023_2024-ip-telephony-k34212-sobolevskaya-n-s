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
Изучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.

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

  
### Часть 2

1. Соберем схему соединения:

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/62d07bb6-ca6b-4e51-a788-9a698718efcc)

2. Создадим VLAN порты на коммутаторе для взаимодействия коммутатора с маршрутизатором.
```
Switch(config)#vlan 10
Switch(config-vlan)#name data
Switch(config-vlan)#vlan 20
Switch(config-vlan)#name voice
```

3. На коммутаторе настроим интерфейсы
```
Switch(config)#int fa0/1
Switch(config-if)# switchport trunk native vlan 30
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport voice vlan 1
Switch(config-if)#
Switch(config-if)#int fa0/2
Switch(config-if)# switchport access vlan 10
Switch(config-if)# switchport mode access
Switch(config-if)# switchport voice vlan 20
Switch(config-if)#
Switch(config-if)#int fa0/3
Switch(config-if)# switchport access vlan 10
Switch(config-if)# switchport mode access
Switch(config-if)# switchport voice vlan 20
Switch(config-if)#
Switch(config-if)#int fa0/4
Switch(config-if)# switchport access vlan 10
Switch(config-if)# switchport mode access
Switch(config-if)# switchport voice vlan 20
```

4. Зададим маршрут по умолчанию командой ip default-gateway:
```
ip default-gateway 192.168.30.1
```

5. На маршрутизаторе поднимаем подынтерфейсы для vlan 10 и vlan 20
```
Router(config-subif)#interface FastEthernet0/0
Router(config-subif)#no shutdown
Router(config-subif)#interface FastEthernet0/0.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip address 192.168.10.1 255.255.255.0
Router(config-subif)#interface FastEthernet0/0.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 192.168.20.1 255.255.255.0
```

6. На маршрутизаторе настроим DHCP для PC и телефонов:
```
Router(config)#ip dhcp pool data
Router(dhcp-config)#network 192.168.10.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.10.1
Router(dhcp-config)#ip dhcp pool voice
Router(dhcp-config)#network 192.168.20.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.20.1
Router(dhcp-config)#option 150 ip 192.168.20.1
```

7. На PC включаем раздачу адресов по DHCP:
![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/e730119d-2a00-4591-86c1-346218252c5e)

8. Настроим услуги телефонии Cisco CallManager Express на маршрутизаторе. Присвоим телефонам номера.
```
Router(config)#telephony-service
Router(config-telephony)#max-dn 5
Router(config-telephony)#max-ephones 5
Router(config-telephony)#ip source-address 192.168.20.1 port 2000
Router(config-telephony)#auto assign 1 to 5
```

```
CMERouter(config)#ephone-dn 1
CMERouter(config-ephone-dn)#number 111
CMERouter(config-ephone-dn)#exit
CMERouter(config)#ephone-dn 2
CMERouter(config-ephone-dn)#number 222
CMERouter(config-ephone-dn)#exit
CMERouter(config)#ephone-dn 3
CMERouter(config-ephone-dn)#number 333
```

9. Проверка связанности:
Пропингуем компьютеры:

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/04c4a15d-d5d3-4e13-9df7-f0484555474d)

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/c320ab3e-24c8-4f13-af06-565b995dbc9f)

Проверим звонки между телефонами:

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/03fffe8e-ca2b-4ded-a4bb-0222d6dbac35)

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/77fa0f0a-0a42-4adf-9bad-37a27134d72f)

## Вывод
В результате выполнения лабораторной работы удалось изучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.
