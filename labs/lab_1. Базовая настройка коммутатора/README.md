# Часть 1. Создание сети и проверка настроек коммутатора по умолчанию

## Шаг 1. Создайте сеть согласно топологии.
**a.** Подсоедините консольный кабель, как показано в топологии. На данном этапе не подключайте кабель Ethernet компьютера PC-A.

**b.** Установите консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.

![Screenshot_1](https://user-images.githubusercontent.com/45486651/191250926-7f782a6a-6d53-4217-9b6f-45af7f2546d7.jpg)

**Вопрос:**
- Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? 
- Почему нельзя подключиться к коммутатору через Telnet или SSH?

```Подключение через Telnet и SSH требует знание ip адреса. На начальном этапе настройки мы еще не задали ip.```

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
- Сколько интерфейсов FastEthernet имеется на коммутаторе 2960? ```24```
- Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960? ```2```
- Каков диапазон значений, отображаемых в vty-линиях? ```0 - 4, 5 - 15```

**c.** Изучите файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM).

**Вопрос:**

Почему появляется это сообщение?
![2](https://user-images.githubusercontent.com/45486651/191252593-dc2ed45c-8901-4d6c-a2cb-d6d6faa5bea6.jpg)

```Т.к. нет сохраненных настроек на данном устройстве.```

**d.** Изучите характеристики SVI для VLAN 1.

**Вопросы:**

- Назначен ли IP-адрес сети VLAN 1?
```interface Vlan1
no ip address
```
- Какой MAC-адрес имеет SVI? Возможны различные варианты ответов.
```Никакого```
- Данный интерфейс включен?
```shutdown```

**e.** Изучите IP-свойства интерфейса SVI сети VLAN 1.

**Вопрос:**

- Какие выходные данные вы видите?

**f.** Подсоедините кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучите IP-свойства интерфейса SVI сети VLAN 1. Дождитесь согласования параметров скорости и дуплекса между коммутатором и ПК.

**Вопрос:**

- Какие выходные данные вы видите?

**g.** Изучите сведения о версии ОС Cisco IOS на коммутаторе.

**Вопросы:**

- Под управлением какой версии ОС Cisco IOS работает коммутатор?
```15.0(2)SE4```
- Как называется файл образа системы?
```C2960-LANBASEK9-M```
- Какой базовый MAC-адрес назначен коммутатору?
```Base ethernet MAC Address : 00:09:7C:C4:61:00```

**h.** Изучите свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A. Switch# show interface f0/6

**Вопрос:**
- Интерфейс включен или выключен?
```FastEthernet0/6 is up, line protocol is up (connected)```
- Что нужно сделать, чтобы включить интерфейс?
```no shutdown```
- Какой MAC-адрес у интерфейса?
```Hardware is Lance, address is 0060.7027.e806 (bia 0060.7027.e806)```
- Какие настройки скорости и дуплекса заданы в интерфейсе?
```Full-duplex, 100Mb/s```

**i.** Изучите параметры сети VLAN по умолчанию на коммутаторе. (show vlan brief)
- Какое имя присвоено сети VLAN 1 по умолчанию?

![3](https://user-images.githubusercontent.com/45486651/191254308-ad70538c-b756-4bcd-9484-fc486ec7cfe3.jpg)
- Какие порты расположены в сети VLAN 1?

![4](https://user-images.githubusercontent.com/45486651/191254373-2ea25b2d-804c-42a9-8434-f9b1b8def0cd.jpg)
- Активна ли сеть VLAN 1?

![5](https://user-images.githubusercontent.com/45486651/191254437-f4c06cba-7bd9-4eb7-9b81-6acd9fe8c434.jpg)
- К какому типу сетей VLAN принадлежит VLAN по умолчанию?
```VLAN1```

**j.** Изучите флеш-память.
- Какое имя присвоено образу Cisco IOS?

![6](https://user-images.githubusercontent.com/45486651/191254752-b02f0705-fd40-440f-b118-ce71f1a35473.jpg)



