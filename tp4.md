# TP4-linux 

## Configuration IP statique

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
```
**Le resultat de la commande "ip a"**
```
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
**Vérification accés internet**
```
[root@localhost .ssh]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=16.1 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=16.5 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=18.1 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=56 time=14.8 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=56 time=15.9 ms
^C
--- 1.1.1.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4008ms
rtt min/avg/max/mdev = 14.800/16.277/18.114/1.084 ms
[root@localhost .ssh]#
```
**Vérification via un domaine**
```
[root@localhost .ssh]# ping youtube
PING nc-ass-vip.sdv.fr (212.95.74.75) 56(84) bytes of data.
^C
--- nc-ass-vip.sdv.fr ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3082ms
```
**Nommage de la machine**
```
[root@localhost ~]# sudo nano /etc/hostname
[root@localhost ~]# hostname
node1.tp4.linux
```
## Mettre en place un service

**installation de nginx**
```
[root@node1 ~]# sudo yum install nginx
Last metadata expiration check: 2:47:47 ago on jeu. 25 nov. 2021 01:05:42 CET.
Dependencies resolved.
=============================================================================================================================================================================================================================================
 Package                                                         Architecture                               Version                                                                      Repository                                     Size
=============================================================================================================================================================================================================================================
Installing:
 nginx
 ...
 complete!
 
```
**Analyse**
```
[root@node1 ~]# sudo systemctl start nginx
[root@node1 ~]# sudo systemctl status nginx
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: active (running) since Thu 2021-11-25 04:04:51 CET; 6s ago
  Process: 6038 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
  Process: 6037 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
  Process: 6035 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
 Main PID: 6040 (nginx)
    Tasks: 2 (limit: 4944)
   Memory: 4.3M
   CGroup: /system.slice/nginx.service
           ├─6040 nginx: master process /usr/sbin/nginx
           └─6041 nginx: worker process

nov. 25 04:04:51 node1.tp4.linux systemd[1]: Starting The nginx HTTP and reverse proxy server...
nov. 25 04:04:51 node1.tp4.linux nginx[6037]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nov. 25 04:04:51 node1.tp4.linux nginx[6037]: nginx: configuration file /etc/nginx/nginx.conf test is successful
nov. 25 04:04:51 node1.tp4.linux systemd[1]: nginx.service: Failed to parse PID from file /run/nginx.pid: Invalid argument
nov. 25 04:04:51 node1.tp4.linux systemd[1]: Started The nginx HTTP and reverse proxy server.
```
**L'utilisateur est Nginx**
```
utilisateur tourne le processus du service NGINX
root        6040  0.0  0.2 119160  2180 ?        Ss   04:04   0:00 nginx: master process /usr/sbin/nginx
nginx       6041  0.0  0.9 151820  7944 ?        S    04:04   0:00 nginx: worker process
```
**Le port par defaut est 80**
```
LISTEN                0                     128                                            [::]:80                                           [::]:*                    users:(("nginx",pid=6041,fd=9),("nginx",pid=6040,fd=9))
```
**La racine web**
```
/usr/share/nginx/html
```
**Les fichiers peuveut être lu par l'utilisateur**
```
[root@node1 html]# ls -l
total 20
-rw-r--r--. 1 root root 3332 10 juin  11:09 404.html
-rw-r--r--. 1 root root 3404 10 juin  11:09 50x.html
-rw-r--r--. 1 root root 3429 10 juin  11:09 index.html
-rw-r--r--. 1 root root  368 10 juin  11:09 nginx-logo.png
-rw-r--r--. 1 root root 1800 10 juin  11:09 poweredby.png
```
**Autorisation des connexions au service du port 80 (NGINX)y**
```
[root@node1 html]# sudo firewall-cmd --add-port=80/tcp --permanent
success
[root@node1 html]# sudo firewall-cmd --reload
success
```
**[Page Nginx](https://github.com/AntoineMACHY/TP/blob/main/fichier_tp4/page-nginx.md)**

**Changement du port**
```
server {
        listen       8080 default_server;
        listen       [::]:8080 default_server;
```
**Vérifion s'il marche toujours**
```
[root@node1 nginx]# sudo systemctl status nginx
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: active (running) since Thu 2021-11-25 04:46:12 CET; 18s ago
  Process: 6151 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
  Process: 6148 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
  Process: 6146 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
 Main PID: 6153 (nginx)
    Tasks: 2 (limit: 4944)
   Memory: 3.7M
   CGroup: /system.slice/nginx.service
           ├─6153 nginx: master process /usr/sbin/nginx
           └─6154 nginx: worker process

nov. 25 04:46:12 node1.tp4.linux systemd[1]: nginx.service: Succeeded.
nov. 25 04:46:12 node1.tp4.linux systemd[1]: Stopped The nginx HTTP and reverse proxy server.
nov. 25 04:46:12 node1.tp4.linux systemd[1]: Starting The nginx HTTP and reverse proxy server...
nov. 25 04:46:12 node1.tp4.linux nginx[6148]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nov. 25 04:46:12 node1.tp4.linux nginx[6148]: nginx: configuration file /etc/nginx/nginx.conf test is successful
nov. 25 04:46:12 node1.tp4.linux systemd[1]: nginx.service: Failed to parse PID from file /run/nginx.pid: Invalid argument
nov. 25 04:46:12 node1.tp4.linux systemd[1]: Started The nginx HTTP and reverse proxy server.
```
**Le changement a bien pris effet**
```
[root@node1 nginx]# ss -lanpt | grep nginx
LISTEN 0      128           0.0.0.0:8080        0.0.0.0:*     users:(("nginx",pid=6154,fd=8),("nginx",pid=6153,fd=8))
LISTEN 0      128              [::]:8080           [::]:*     users:(("nginx",pid=6154,fd=9),("nginx",pid=6153,fd=9))
```
**On ferme l'ancien port et on ouvre le nouveau**
```
[root@node1 nginx]# sudo firewall-cmd --remove-port=80/tcp --permanent
success
[root@node1 nginx]# sudo firewall-cmd --add-port=8080/tcp --permanent
success
[root@node1 nginx]# sudo firewall-cmd --reload
success
```
**[Page Nginx avec nouveau port](https://github.com/AntoineMACHY/TP/blob/main/fichier_tp4/new-port.md)**

**créationdu nouvelle utilisateur**
```
[root@node1 nginx]# useradd coco -m -s /home/web
[root@node1 etc]# sudo nano nginx.conf
```
**homedir de l'utilisateur coco**
```
coco:x:1001:1001::/home/coco:/home/web
```
**Mot de passe de l'utilisateur "coco"**
```
root:$6$U0YeoeorhqMUpMfD$wy4bhF9LxyBqHmf3RWgyQBj66FtReb9y5Dd6qXMn1OmuD0UDpC1qt6nCHhVylit0quaApcqtbCUX6W2UGPrRP1::0:99999:7:::
bin:*:18700:0:99999:7:::
daemon:*:18700:0:99999:7:::
adm:*:18700:0:99999:7:::
lp:*:18700:0:99999:7:::
sync:*:18700:0:99999:7:::
shutdown:*:18700:0:99999:7:::
halt:*:18700:0:99999:7:::
mail:*:18700:0:99999:7:::
operator:*:18700:0:99999:7:::
games:*:18700:0:99999:7:::
ftp:*:18700:0:99999:7:::
nobody:*:18700:0:99999:7:::
dbus:!!:18955::::::
systemd-coredump:!!:18955::::::
systemd-resolve:!!:18955::::::
tss:!!:18955::::::
polkitd:!!:18955::::::
libstoragemgmt:!!:18955::::::
cockpit-ws:!!:18955::::::
cockpit-wsinstance:!!:18955::::::
sssd:!!:18955::::::
chrony:!!:18955::::::
sshd:!!:18955::::::
toto:$6$47cGh5zp5iLxmlny$cu4isDTDM9FCLDcuIMlNdGlfGLeLBR4ZuEuJQ9kX4YoPgoxATFgznN45wsWtDlhDqASmEdoM7/rNskXHsUFNW1::0:99999:7:::
nginx:!!:18956::::::
coco$toto
```
**Modification du fichier configuration**
```
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user coco;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;
```
**Vérification de l'effet de la modification**
```
[root@node1 nginx]# ps -ef |grep nginx
root        6238       1  0 05:09 ?        00:00:00 nginx: master process /usr/sbin/nginx
coco        6239    6238  0 05:09 ?        00:00:00 nginx: worker process
root        6243    2990  0 05:10 pts/0    00:00:00 grep --color=auto nginx
```
**Mon index.html**
```
#!/etc/web
<h1>toto<h1>
```
**Je modifie la racine web**
```
server {
        listen       8080 default_server;
        listen       [::]:8080 default_server;
        server_name  _;
        root         /var/www/super_site_web;
```
**On a notre page qui s'affiche**
```
[root@node1 nginx]# curl 192.168.56.150:8080
#!/etc/web
<h1>toto<h1>
```