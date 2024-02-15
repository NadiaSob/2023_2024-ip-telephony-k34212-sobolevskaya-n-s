University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)

Year: 2023/2024

Group: K34212

Author: Sobolevskaya Nadezhda Sergeevna

Lab: Lab1

Date of create: 15.02.2024

Date of finished: 

# Отчет по лабораторной работе №1: "Базовая настройка ip-телефонов в среде Сisco packet tracer"

## Цель работы

Изучить рабочую среду Cisco Packet Tracer, ознакомиться с интерфейсами основных устройств, типами кабелей, научиться собирать топологию. Изучить построение сети IP-телефонии с помощью маршрутизатора, коммутатора и IP телефонов Cisco 7960 в среде Packet tracer

## Ход работы

### Часть 1

1. Соберем схему соединения

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/9b1d913d-4612-489b-b2aa-d403e05e94fe)

2. Присвоим компьютерам статические IP-адреса 192.168.20.1 - 192.168.20.7 с маской 255.255.255.0

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/f98d4e83-b635-487b-9a59-d1affa4ced75)

3. Проверяем связность, для этого отправляем пакеты с одного компьютера на другой с помощью команды ping. Пинги проходят успешно.

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/4a2406d2-b415-433c-8d26-5455aed0df79)

### Часть 2

1. Соберем схему соединения, изменим имя маршрутизатора на CMERouter

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/4e4c759a-d988-41d1-84a7-f8de7c125ab6)

2. Настроим интерфейс fa0/0 на маршрутизаторе Cisco 2811 (CMERouter), присвоим ему IP-адрес 192.168.1.1 с маской 255.255.255.0

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/8e4bc695-9434-4bdb-b88a-2048b049cf93)

3. Подключим оба IP-телефона к источнику питания

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/c04b0ca7-903c-46e6-a0ba-20077f93d7bc)

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/a393d651-6562-416b-ac6c-d4b5b4e8af6f)

4. Настроим DHCP сервер для передачи голоса и данных на маршрутизаторе - Cisco 2811. Для этого создаем DHCP-пул под названием IpPhones с адресами 192.168.1.0 и маской 255.255.255.0, указываем адрес маршрутизатора, для передачи голоса включаем опцию 150.

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/97dce13d-7e72-46fe-bf8c-b6c1065de167)

5. На маршрутизаторе настроим VoIP параметры. Указываем максимальное количество номеров и IP-телефонов - 20, шлюз - 3100, порт интерфейса маршрутизатора 192.168.1.1. Также настраиваем автоматическое назначение внешних номеров

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/1b80b11a-f10d-4afe-88cc-7ec405b170bd)

6. 
7. в
8. 


