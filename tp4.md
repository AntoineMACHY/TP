# TP4-linux 

# Sommaire

- [1 : Configuration IP statique](#1-:-Configuration-IP-statique)

# 1 : Configuration IP statique

```
# chemin pour configurer l'interface host-only
cd /etc/sysconfig/network-scripts

# changer l'interface  host-only
sudo nano ifcfg-enp0s8
```

**Les ajouts et changements à faire du fichier**

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

#Le resultat de la commande "ip a"
[toto@localhost network-scripts]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:28:ba:75 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 82909sec preferred_lft 82909sec
    inet6 fe80::a00:27ff:fe28:ba75/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:10:50:91 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.150/24 brd 192.168.56.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe10:5091/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
**Connection SSH fonctionnelle**

```
[toto@localhost network-scripts]$ sudo systemctl status sshd
[sudo] Mot de passe de toto :
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2021-11-24 17:45:30 CET; 1h 4min ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 863 (sshd)
    Tasks: 1 (limit: 4944)
   Memory: 4.7M
   CGroup: /system.slice/sshd.service
           └─863 /usr/sbin/sshd -D -oCiphers=aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes256-cbc,aes128-gcm@openssh.com,aes128-ctr,aes128-cbc -oMACs=hmac-sha2-256-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-128>

nov. 24 17:45:30 localhost.localdomain systemd[1]: Starting OpenSSH server daemon...
nov. 24 17:45:30 localhost.localdomain sshd[863]: Server listening on 0.0.0.0 port 22.
nov. 24 17:45:30 localhost.localdomain sshd[863]: Server listening on :: port 22.
nov. 24 17:45:30 localhost.localdomain systemd[1]: Started OpenSSH server daemon.
nov. 24 18:01:55 localhost.localdomain sshd[1506]: Accepted password for toto from 192.168.56.141 port 53036 ssh2
nov. 24 18:01:55 localhost.localdomain sshd[1506]: pam_unix(sshd:session): session opened for user toto by (uid=0)
```
```
C:\Users\fridi>ssh toto@192.168.56.150
toto@192.168.56.150's password:
Activate the web console with: systemctl enable --now cockpit.socket
```
