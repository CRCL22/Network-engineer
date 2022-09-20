# Часть 1. Создание сети и проверка настроек коммутатора по умолчанию

## Шаг 1. Создайте сеть согласно топологии.
**a.** Подсоедините консольный кабель, как показано в топологии. На данном этапе не подключайте кабель Ethernet компьютера PC-A.

**b.** Установите консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.

![Screenshot_1](https://user-images.githubusercontent.com/45486651/191250926-7f782a6a-6d53-4217-9b6f-45af7f2546d7.jpg)

**Вопрос:**
- Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? 
- Почему нельзя подключиться к коммутатору через Telnet или SSH?

**Ответ:**
Подключение через Telnet и SSH требует знание ip адреса. На начальном этапе настройки мы еще не задали ip.

## Шаг 2. Проверьте настройки коммутатора по умолчанию.

**a.** Введите команду enable, чтобы войти в привилегированный режим EXEC.
Убедитесь, что на коммутаторе находится пустой файл конфигурации по умолчанию, с помощью команды show running-config привилегированного режима EXEC. 

```Switch>enable
Switch#show running-config
Building configuration...

Current configuration : 1080 bytes

version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption

hostname Switch

spanning-tree mode pvst
spanning-tree extend system-id

interface FastEthernet0/1
interface FastEthernet0/2
interface FastEthernet0/3
interface FastEthernet0/4
interface FastEthernet0/5
interface FastEthernet0/6
interface FastEthernet0/7
interface FastEthernet0/8
interface FastEthernet0/9
interface FastEthernet0/10
interface FastEthernet0/11
interface FastEthernet0/12
interface FastEthernet0/13
interface FastEthernet0/14
interface FastEthernet0/15
interface FastEthernet0/16
interface FastEthernet0/17
interface FastEthernet0/18
interface FastEthernet0/19
interface FastEthernet0/20
interface FastEthernet0/21
interface FastEthernet0/22
interface FastEthernet0/23
interface FastEthernet0/24
interface GigabitEthernet0/1
interface GigabitEthernet0/2
interface Vlan1
no ip address
shutdown

line con 0
line vty 0 4
login
line vty 5 15
login
end
```

**b.** Изучите текущий файл running configuration.
**Вопросы:**
- Сколько интерфейсов FastEthernet имеется на коммутаторе 2960? **24**
- Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960? **2**
- Каков диапазон значений, отображаемых в vty-линиях? **0 - 4**, **5 - 15**
