# demo2024
|Имя устройства  |Интерфейс           |IPv4/IPv6       |Маска/Префикс   |Шлюз                  |                       
|  ------------- | -------------      | -------------  |  ------------- |  -------------       |                    
|ISP             |ens192              |10.12.11.12     |/24             |10.12.11.254          |      
|                |ens256              |192.168.0.162   |/30             |                      |
|                |ens224              |192.168.0.166   |/30             |                      |
|HQ-R            |ens192              |192.168.0.16    |/25             |                      |                                   
|                |ens224              |192.168.0.161   |/30             |192.168.0.162         |
|BR-R            |ens192              |192.168.0.165   |/30             |192.168.0.166         |                                  
|                |ens224              |192.168.0.129   |/27             |                      |
|HQ-SRV          |ens192              |192.168.0.126   |/25             |192.168.0.1           |                                   
|BR-SRV          |ens192              |192.168.0.158   |/27             |192.168.0.129         |   

## Топология
![Топология](https://github.com/Barmenkov/demo2024/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA.PNG)

## 1. Настройка интерфейсов
Посмотрел существующие интерфейсы с помощью команды 

``ip a``

Зашел в файл настройки интерфейсов ISP, с помощью команды

``nano /etc/network/interfaces``

Ввёл IP-адреса, маску подсети и шлюз по умолчанию

## ISP
```
auto ens192
iface ens192 inet static
address 10.12.11.12
netmask 255.255.255.0
gateway 10.12.11.254

auto ens256
iface ens256 inet static
address 192.168.0.162
netmask 255.255.255.252
        
auto ens224
iface ens224 inet static
address 192.168.0.166
netmask 255.255.255.252
```

## HQ-R
```
auto ens192
iface ens192 inet static
address 192.168.0.161
netmask 255.255.255.252
gateway 192.168.0.162
        
auto ens224
iface ens224 inet static
address 192.168.0.1
netmask 255.255.255.128
```

## BR-R
```
auto ens192
iface ens192 inet static
address 192.168.0.165
netmask 255.255.255.252
gateway 192.168.0.166
        
auto ens224
iface ens224 inet static
address 192.168.0.129
netmask 255.255.255.224
```

## HQ-SRV
```
auto ens192
iface ens192 inet static
address 192.168.0.126
netmask 255.255.255.128
gateway 192.168.0.1
```

## BR-SRV
```
auto ens192
iface ens192 inet static
address 192.168.0.158
netmask 255.255.255.224
gateway 192.168.0.129
```
### Сохранил конфигурацию
```
Ctrl+S
```
### Вышел из конфигурационного файла
```
Ctrl+X
```
### Перезагрузил сервис работы с сетью
```
systemctl restart networking
```
## 2. Установка и настройка frr
### Установил пакет frr
```
apt-get install frr
```
### Проверил состояние
```
systemctl statys frr
```
### Вошел в файл конфигурации
```
nano /etc/frr/daemons
```
### Изменил значение 
```
ospf=yes
```
### Перезагрузил службу 
```
systemctl restart frr
```
### Вошел в настройку маршрутизации 
```
vtysh
```
### Просмотрел ip адреса и их состояние
```
show ip interface brief
```
### Вошел в конфигурацию терминала 
```
conf t
```
### Запустил процесс 
```
router ospf
```
### Добавил интерфейсы 
```
network (ip адрес) area 0
```
### Просмотрел соседей  
```
do show ip ospf neighbor
```
### Сохранил конфигурацию  
```
copy running-config startup-config
```


