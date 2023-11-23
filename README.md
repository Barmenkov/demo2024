# demo2024
|Имя устройства  |Интерфейс           |IPv4/IPv6       |Маска/Префикс   |Шлюз                  |                       
|  ------------- | -------------      | -------------  |  ------------- |  -------------       |                    
|ISP             |ens192              |10.10.12.10     |/24             |10.12.12.254          |      
|                |ens256              |192.168.0.162   |/30             |                      |
|                |ens224              |192.168.0.166   |/ 30            |                      |
|HQ-R            |ens192              |192.168.0.161   |/30             |192.168.0.162         |                                   
|                |ens224              |192.168.0.1     |/25             |                      |
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

## ISP

