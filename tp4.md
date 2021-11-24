# TP4-linux 

# Sommaire

- [1 : Configuration IP statique](#1-:-Configuration-IP-statique)

# 1 : Configuration IP statique

```
#chemin pour configurer l'interface host-only
cd /etc/sysconfig/network-scripts

#changer l'interface  host-only
sudo nano ifcfg-enp0s8
```

**Les ajouts et changements à faire**

``` 
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
NAME=enp0s8
UUID=6c5b116d-b016-4482-9fd4-61425654e80e
DEVICE=enp0s8
ONBOOT=yes
NAME=enp0s8
DEVICE=enp0s8
ONBOOT=yes
IPADDR=192.168.56.150
NETMASK=255.255.255.0
```