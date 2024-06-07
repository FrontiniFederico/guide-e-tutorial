## Configurare ip statico in su RHEL8

Qui trovi la [documentazione ufficiale](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/part-managing_ip_networking). Puoi configurare l'ip statico con o senza interagire direttamente con [NetworkManager](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/getting_started_with_networkmanager) ma in questa guida noi configureremo l'ip statico senza NetworkManager lavorando direttamente sui file ifcfg. Durante il boot della macchina, vengono usati per determinare quali interfacce mettere in piedi e come configurarle e per convenzione si chiamano `ifcfg-<interfaccia>`.

Innanztitutto verifichiamo le interfacce attive del satellite. Nell'esempio, l'indirizzo ip statico `172.16.13.170` è già attivo e configurato sull'interfaccia `eth0`.

```shell
ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:70:03:a9 brd ff:ff:ff:ff:ff:ff
    inet 172.16.13.170/24 brd 172.16.13.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:fe70:3a9/64 scope link 
       valid_lft forever preferred_lft forever 
```

Non ci interessano le interfacce virtuali come lo (loopback) ma solo quelle fisice. Creiamo uno script di configurazione per l'interfaccia in `/etc/sysconfig/network-scripts/`:

```
TYPE=Ethernet
HWADDR=00:15:5D:70:03:A9
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
IPADDR=172.16.13.170
PREFIX=24
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6_DISABLED=yes
IPV6INIT=no
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=default
NAME=eth0
UUID=779e23af-b595-4ca6-a624-0786237349fb
DEVICE=eth0
ONBOOT=yes
GATEWAY=172.16.13.252
```

Il netmask non serve, perché viene calcolato automaticamente da **ipcalcp** ma se lo sappiamo tanto vale settarlo subito con `ifconfig eth0 172.16.13.170 netmask 255.255.255.0`

A questo punto verichiamo l'interfaccia fisica su cui abbiamo fatto modifiche:

```shell
ifconfig

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.16.13.170  netmask 255.255.255.0  broadcast 172.16.13.255
        inet6 fe80::215:5dff:fe70:3a9  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:70:03:a9  txqueuelen 1000  (Ethernet)
        RX packets 75058  bytes 6153038 (5.8 MiB)
        RX errors 0  dropped 32103  overruns 0  frame 0
        TX packets 1990  bytes 196027 (191.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0 
```

e verifichiamo che le modifiche siano andate a buon fine:

```shell
ip route show

default via 172.16.13.252 dev eth0 
169.254.0.0/16 dev eth0 scope link metric 1002 
172.16.13.0/24 dev eth0 proto kernel scope link src 172.16.13.170 
```

Facciamo ripartire infine il NetworkManager con `systemctl start NetworkManager`.