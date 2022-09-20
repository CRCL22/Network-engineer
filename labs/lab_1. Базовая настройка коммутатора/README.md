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

#Часть 2. Настройка базовых параметров сетевых устройств

##Шаг 1. Настройте базовые параметры коммутатора.

```Заменила имя коммутатору:
Switch#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#
```
**a.** В режиме глобальной конфигурации скопируйте следующие базовые параметры конфигурации и вставьте их в файл на коммутаторе S1.
*no ip domain-lookup
hostname S1
service password-encryption
enable secret class
banner motd #
Unauthorized access is strictly prohibited. #*
![01](https://user-images.githubusercontent.com/45486651/191270794-85604237-d86f-496f-b8df-3b280137fca4.jpg)

**b.** Назначьте IP-адрес интерфейсу SVI на коммутаторе. 
![02](https://user-images.githubusercontent.com/45486651/191271122-017011e3-6093-4de3-8590-decf6a1bd168.jpg)

**c.** Доступ через порт консоли также следует ограничить с помощью пароля. 
![03](https://user-images.githubusercontent.com/45486651/191271493-6d71a1dc-98af-449a-977a-332a14b97295.jpg)

**d.** Настройте каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet.
![04](https://user-images.githubusercontent.com/45486651/191271673-2d42bae8-a56f-48d5-a835-f79ef5b1776d.jpg)

**Вопрос:**
- Для чего нужна команда login?
```Для включения доступа к VTY```

## Шаг 2. Настройте IP-адрес на компьютере PC-A.

![Screenshot_2](https://user-images.githubusercontent.com/45486651/191271972-a8445581-41ad-4264-9362-73b988675813.jpg)

# Часть 3. Проверка сетевых подключений

## Шаг 1. Отобразите конфигурацию коммутатора.

**a.** Пример конфигурации приведен ниже. Параметры, которые вы настроили, выделены желтым. Другие параметры конфигурации — значения IOS по умолчанию.


service password-encryption
hostname S1
enable secret 5 $1$mtvC$6NC.1VKr3p6bj7YGE.jNg0
!enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

![image](https://user-images.githubusercontent.com/45486651/191272967-1d8659ae-d6e1-4b7a-ba6b-6a004595d6c2.png)


no ip domain-lookup

![Screenshot_3](https://user-images.githubusercontent.com/45486651/191273331-5fc34805-5b95-4c48-a88b-d35a79c554f1.jpg)


interface FastEthernet0/24
 switchport access vlan 99

![Screenshot_4](https://user-images.githubusercontent.com/45486651/191273535-4c63f014-6164-43b9-8e94-ff786c1c165a.jpg)

interface GigabitEthernet0/1
 switchport access vlan 99

![Screenshot_5](https://user-images.githubusercontent.com/45486651/191273612-9aee2e88-0183-47da-8e51-45f5a64bb217.jpg)

interface GigabitEthernet0/2
 switchport access vlan 99

![Screenshot_6](https://user-images.githubusercontent.com/45486651/191273699-8995302c-da56-49e7-b52f-d8f53f7704a1.jpg)

interface Vlan1
 ip address 192.168.1.2 255.255.255.0

![Screenshot_7](https://user-images.githubusercontent.com/45486651/191273781-9007dbcd-f668-434b-a36a-6fd112b545ce.jpg)

ip default-gateway 192.168.1.1

![Screenshot_8](https://user-images.githubusercontent.com/45486651/191273877-7a69bc9d-5b27-43aa-a4c0-c471625a3e66.jpg)

banner motd ^C
Unauthorized access is strictly prohibited. ^C

![Screenshot_9](https://user-images.githubusercontent.com/45486651/191273994-3fbc40b2-5bc7-4b14-8e9e-472c3bae69a0.jpg)

 password 7 00071A150754
 logging synchronous
 login

![Screenshot_10](https://user-images.githubusercontent.com/45486651/191274115-2f0ef9a9-0721-44fd-ba4d-fc945cbb7a64.jpg)

line vty 0 4
 password 7 121A0C041104
 login
 
 ![Screenshot_11](https://user-images.githubusercontent.com/45486651/191274236-aa7c8f2f-65b6-43fd-b2f2-7ea05e45cbad.jpg)


line vty 5 15
 password 7 121A0C041104
 login

![Screenshot_12](https://user-images.githubusercontent.com/45486651/191274313-654b55dd-fa76-439e-ab6b-b41c31446517.jpg)


**b.** Проверьте параметры VLAN 1.
- Какова полоса пропускания этого интерфейса?
```BW 100000 Kbit```
- В каком состоянии находится VLAN 1?
```Vlan1 is up```
- В каком состоянии находится канальный протокол?
```line protocol is up```
