University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)

Year: 2023/2024

Group: K34212

Author: Sobolevskaya Nadezhda Sergeevna

Lab: Lab2

Date of create: 26.02.2024

Date of finished: 

# Отчет по лабораторной работе №3: "Использование Asterisk в качестве SIP proxy"

## Цель работы
Изучить программный комплекс Asterisk. Настройка Asterisk для локальных звонков.

## Ход работы

Работу будем выполнять на Ubuntu 22.04.3

1. Установим Asterisk

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/2cd817fb-4aa1-4fc5-be45-3ee4c3f12eb2)

2. Настроим SIP каналы. Для этого открываем файл /etc/asterisk/sip.conf, добавляем информацию о телефонах 1000 и 1001:

```
[1000]
type=friend
host=dynamic
secret=1000
context=ext_1000

[1001]
type=friend
host=dynamic
secret=1001
context=ext_1001
```

Затем открываем файл /etc/asterisk/extensions.conf, добавляем информацию:

```
[ext_1000]
exten => _XXXX,1,Dial(SIP/${EXTEN})

[ext_1001]
exten => _XXXX,1,Dial(SIP/${EXTEN})
```

3. Перезапускаем Asterisk:

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/9dd38549-2326-4876-9ade-b43b059e1835)

4. Проверим статус:

![image](https://github.com/NadiaSob/2023_2024-ip-telephony-k34212-sobolevskaya-n-s/assets/43678322/20a161ec-444d-4d3a-98b6-48e5235ab190)

5. В качестве soft-телефона устанавливаем Zoiper5. Для этого скачиваем архив и запускаем программу. При входе вводим данные аккаунта: логин - 1000, пароль - 1000


6. а


## Вывод
В результате выполнения лабораторной работы удалось изучить программный комплекс Asterisk, настроить Asterisk для локальных звонков.
