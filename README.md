# Lapres Modul 5

Joseph Eric Amadeo S. / 05111840000077   
Feinard / 05111840000081

## Gambar Pembagian Subnet

**![](https://lh3.googleusercontent.com/32tLbgsSSPSI4CBVnlyd-pMew37z4D2PV5oxxh6EwtgRaxf4i5lk6R7KGyGW_kUslfktEUc3UqkSsoVt_4hljPt_Hel2tugOiMYK4E2fvtPnUJ7u9C8Yj3X1_wkx4A_U6M2QTDsI)**  
## Tree Pembagian Subnet
**![](https://lh5.googleusercontent.com/qK3E2Oi5XeNcD663cob82aGLfCsHUnaEdAL974_H4bgAtshVdAe0apEImUQKayde5_gji6QodyiVKldS4jtrewqgK8akgEnRcbCujHPmuaDmN7dbV-C5Z-ysALqiP93F9w3HPr2L)**  

## Pembagian IP
**![](https://lh6.googleusercontent.com/OJj1DP1Oxc4qWeDYyShMPe8nq4MxqBazMIr6_10fmgf80VG_GW6Cw0i9RlDzhmpJXluKDfjx0KryvQaGkA8x6j9AKJDTvCAU2JdLX1Z-TkkdBBGaScc-NNcg8Goxt4itJ1kkuRar)**  
## Switch  
```
# Switch

uml_switch -unix switch1 > /dev/null < /dev/null & #A6

uml_switch -unix switch2 > /dev/null < /dev/null & #A1

uml_switch -unix switch3 > /dev/null < /dev/null & #A2

uml_switch -unix switch4 > /dev/null < /dev/null & #A5

uml_switch -unix switch5 > /dev/null < /dev/null & #A3

uml_switch -unix switch6 > /dev/null < /dev/null & #A4

# Router

xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.25 eth1=daemon,,,switch5 eth2=daemon,,,switch6 mem=96M &

xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch5 eth1=daemon,,,switch3 eth2=daemon,,,switch2 mem=96M &

xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch6 eth1=daemon,,,switch4 eth2=daemon,,,switch1 mem=96M &

# Server

xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &

xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &

xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &

xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &

# Klien

xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch3 mem=96M &

xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch4 mem=96M &

  
```  
## Settingan:
```  
#SURABAYA

nano /etc/sysctl.conf (surabaya)

uncomment net.ipv4.ip_forward=1

sysctl -p

nano /etc/network/interfaces

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 10.151.76.26

netmask 255.255.255.252

gateway 10.151.76.25

auto eth1

iface eth1 inet static

address 192.168.0.1

netmask 255.255.255.252

auto eth2

iface eth2 inet static

address 192.168.0.5

netmask 255.255.255.252

#batu

nano /etc/network/interfaces

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 192.168.0.2

netmask 255.255.255.252

gateway 192.168.0.1

#A2

auto eth1

iface eth1 inet static

address 192.168.1.1

netmask 255.255.255.0

#A1

auto eth2

iface eth2 inet static

address 10.151.77.48

netmask 255.255.255.248

#kediri

nano /etc/network/interfaces

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 192.168.0.6

netmask 255.255.255.252

gateway 192.168.0.5

#A5

auto eth1

iface eth1 inet static

address 192.168.2.1

netmask 255.255.255.0

#A6

auto eth2

iface eth2 inet static

address 192.168.0.9

netmask 255.255.255.248

#malang

nano /etc/network/interfaces

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 10.151.77.50

netmask 255.255.255.248

gateway 10.151.77.49

#mojokerto

nano /etc/network/interfaces

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 10.151.77.51

netmask 255.255.255.248

gateway 10.151.77.49

service networking restart

#madiun

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 192.168.0.10

netmask 255.255.255.248

gateway 192.168.0.9

#probolinggo

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet static

address 192.168.0.11

netmask 255.255.255.248

gateway 192.168.0.9

#sidoarjo and gresik

auto lo

iface lo inet loopback

auto eth0

iface eth0 inet dhcp  
```

## DHCP:
```  
#mojokerto

subnet 10.151.77.48 netmask 255.255.255.248 {

option routers 10.151.77.49;

option broadcast-address 10.151.77.55;

}

subnet 192.168.1.0 netmask 255.255.255.0 {

range 192.168.1.2 192.168.1.202;

option routers 192.168.1.1;

option broadcast-address 192.168.1.255;

option domain-name-servers 10.151.77.50;

option domain-name-servers 202.46.129.2;

default-lease-time 600;

max-lease-time 7200;

}

subnet 192.168.2.0 netmask 255.255.255.0 {

range 192.168.2.2 192.168.2.212;

option routers 192.168.2.1;

option broadcast-address 192.168.2.255;

option domain-name-servers 10.151.77.50;

option domain-name-servers 202.46.129.2;

default-lease-time 600;

max-lease-time 7200;

}

``` 


## Route:
```

#route surabaya

route add -net 10.151.77.48 netmask 255.255.255.248 gw 192.168.0.2

route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.2

route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.0.6

route add -net 192.168.0.8 netmask 255.255.255.248 gw 192.168.0.6
```  

## Jawaban:  
### no 1

iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.76.26 #surabaya  
Hasil:  
Sebelum iptables:  
**![](https://lh4.googleusercontent.com/NMqmzRmaR4lkiZpdevV761JgtsDa57ARGcAWNWhnMUkpgjzovKfKN_kAbJFrIfamKjmbLtWIBMqSTRVTCTm2x8TYy-5aNmkdwKRGArKbfdqeDKYF-78ga52hg-hZhIPAu8PAeipj)**  
Setelah iptables:  
**![](https://lh3.googleusercontent.com/CJGX7wJjn_hawK-_WedPrMEM8kYCABsj745y5XdV_AXNaIdK8nQ5gqf8uB2IzamBfTm46tQRL1u7iAF20h32FBM9_pJQJpmJtaMtMlK9EXy5Z820-i-pZ7zZzyNS47WacV7RcGKf)**  

### no 2

iptables -A FORWARD -d 10.151.77.48/29 -i eth0 -p tcp --dport 22 -j DROP    
#surabaya  
Sebelumnya:  
**![](https://lh3.googleusercontent.com/bROMwxRECkSttjOZzQG66lUVbPZeixDJ8G_M6xvDL1bB6MJ1CxdhFxprKvO6Nec5VU1STeaK-I6ilhUfaV4M0BQgXDzlRrikugNyRyHxB5VQTo1Nk1SRU148K4T5tE1a1x9DEiJm)**  
Setelah iptables:  
**![](https://lh6.googleusercontent.com/Im6eoWOMSTG0OoOwpUe-leVyOjwIod6mq0_p0hNtghJl98PuXZ82hKg9vh6xqHn3n3mUSMYmyW5P9ss-vv_X5JaE0x7flYyC1vA-fRjsSRXU5n9L0ndvvQEcTfEEXvN8sPmiznGX)**  
### no 3

iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP #malang dan mojokerto  
Sebelum:  
**![](https://lh6.googleusercontent.com/v1k7BbVn6NDTxJaIHmelyu5oEiIp1e8F3WGwIoUd8VoldpKWMsi1o6ssRkyNWW9dP6wVPh1rVxoUMPaOZStUJlH44DzF5mLJ06S_WP96aiDrzd3MpLADV1243JCeXSOGfd4EBovm)**  
Sesudah:  
**![](https://lh4.googleusercontent.com/HSi500eQ5z-dGWzoMsED6sPKMIel3Odz9Jilj1XZ-tsK0biTP-fGV7Lqbbgsi8kNt58uToa0wOqQ5-4PrlFZZ2QZckU3RCK2PZFQYFl2YxwMa9bvHcTsyLskgBN0EuFgr3srjITd)**  
### no 4

iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT #malang

iptables -A INPUT -s 192.168.1.0/24 -j REJECT #malang

### no 5

iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 07:00 --timestop 17:00 -j REJECT #malang

### no 6

iptables -A PREROUTING -t nat -p tcp -d 10.151.77.50 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.0.11:80 #surabaya

iptables -A PREROUTING -t nat -p tcp -d 10.151.77.50 --dport 80 -j DNAT --to-destination 192.168.0.10:80

### no 7

iptables -N LOGGING

iptables -A INPUT -j LOGGING

iptables -A OUTPUT -j LOGGING

iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4

iptables -A LOGGING -j DROP

