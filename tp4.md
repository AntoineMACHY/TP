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

**clef**
```
toto@toto-VirtualBox:~/.ssh$ cat id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```
**Connection sans mot de passe**
```
toto@toto-VirtualBox:~/.ssh$ ssh root@192.168.56.150
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Thu Nov 25 03:28:42 2021 from 192.168.56.144
[root@localhost ~]#
```