# TP 3 : A little script

## I. Script carte d'identité

**Fichier [`/srv/idcard/idcard.sh`](https://github.com/AntoineMACHY/TP/blob/main/fichier_tp3/idcard.md)**

### Ce qui donne

```
Machine name: toto-VirtualBox
IP : 192.168.56.144/24
OS Ubuntu and kernel version is 5.13.0-20-generic
Ram : 126Mi  RAM restante sur 971Mi  RAM totale
Disque : 507M space left
Top 5 processes by RAM usage :   20107       1 /usr/bin/xfce4-terminal      3.8  0.0
    893     637 /usr/lib/policykit-1-gnome/  3.7  0.0
    781     637 Thunar --daemon              3.7  0.0
    612     552 /usr/lib/xorg/Xorg -core :0  2.9  0.0
    754     637 xfwm4 --replace              2.7  0.0
Listening ports :
LISTEN 0      4096    127.0.0.53%lo:53          0.0.0.0:*     users:(("systemd-resolve",pid=424,fd=14))
LISTEN 0      128           0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=20153,fd=3))
LISTEN 0      128         127.0.0.1:631         0.0.0.0:*     users:(("cupsd",pid=26640,fd=7))
LISTEN 0      128              [::]:22             [::]:*     users:(("sshd",pid=20153,fd=4))
LISTEN 0      128             [::1]:631            [::]:*     users:(("cupsd",pid=26640,fd=6))
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   115  100   115    0     0    333      0 --:--:-- --:--:-- --:--:--   333

Here's your random cat : https://cdn2.thecatapi.com/images/ESj_RCNJ4.png
```

## II. Script youtube-dl

**Fichier [`/srv/yt/yt.sh`](https://github.com/AntoineMACHY/TP/blob/main/fichier_tp3/yt_sh.md)**

**Log [/var/log/yt/download.log``](https://github.com/AntoineMACHY/TP/blob/main/fichier_tp3/log.md)**

```
toto@toto-VirtualBox:/srv/yt$ bash yt.sh https://www.youtube.com/watch?v=jjs27jXL0Zs
Video https://www.youtube.com/watch?v=jjs27jXL0Zs was downloaded.
File path : /srv/yt/downloads/SI LA VIDÉO DURE 1 SECONDE LA VIDÉO S'ARRÊTE/SI LA VIDÉO DURE 1 SECONDE LA VIDÉO S'ARRÊTE.mp4
```