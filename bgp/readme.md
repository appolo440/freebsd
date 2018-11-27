## install

```
cd /usr/ports/net/quagga/
make config-recursive
```

/etc/rc.conf
```
quagga_enable="YES"
quagga_daemons="zebra bgpd"
quagga_flags="-d -A 127.0.0.1"
```

```
touch /var/log/zebra.log /var/log/bgpd.log
chown quagga:quagga /var/log/zebra.log
chown quagga:quagga /var/log/bgpd.log
```

/usr/local/etc/quagga/bgpd.conf

```
hostname TELENET-BGP
password 123
enable password 123
!
router bgp [номер AS выданный провайдером]
 bgp router-id [ip адрес хоста]
 network  [анонсируемая сеть 0.0.0.0/24]
 neighbor 10.11.12.22 remote-as [номер AS провайдера]
 neighbor 10.11.12.22 route-map set-nexthop out
 neighbor 10.11.12.22 ebgp-multihop
 neighbor 10.11.12.22 next-hop-self
!
 access-list all permit any
!
route-map set-nexthop permit 10
 match ip address all
 set ip next-hop [ip адрес хоста]
!
log file /var/log/bgpd.log
!

```

/usr/local/etc/quagga/zebra.conf

```
hostname TELENET-BGP
password 123
enable password 123
!
interface lo
!
interface hn0 [внешний интерфейс]
 ip address 0.0.0.0/0 [ip адрес хоста/маска подсети]
!
interface de0 [локальный интерфейс в сеть провайдера/ маска подсети]
 ip address 0.0.0.0/24
!
ip route [анонсируемая сеть/маска сети] [ip адрес сервера куда анонсируется сеть]
!
log file /var/log/zebra.log
ip forwarding
!
!
line vty
!
```

telnet 127.0.0.1 2605
