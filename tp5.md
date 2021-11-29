# TP5-linux

##

**Installer mariadb**
```
Installé:
  mariadb-backup-3:10.3.28-1.module+el8.4.0+427+adf35707.x86_64             mariadb-errmsg-3:10.3.28-1.module+el8.4.0+427+adf35707.x86_64                   mariadb-gssapi-server-3:10.3.28-1.module+el8.4.0+427+adf35707.x86_64
  mariadb-server-3:10.3.28-1.module+el8.4.0+427+adf35707.x86_64             mariadb-server-utils-3:10.3.28-1.module+el8.4.0+427+adf35707.x86_64             perl-DBD-MySQL-4.046-3.module+el8.4.0+577+b8fe2d92.x86_64
  perl-DBI-1.641-3.module+el8.4.0+509+59a8d9b3.x86_64                       perl-Math-BigInt-1:1.9998.11-7.el8.noarch                                       perl-Math-Complex-1.59-420.el8.noarch
  psmisc-23.1-5.el8.x86_64

Terminé !
```
**lancer mariadc**
```
[toto@db ~]$ sudo systemctl start mariadb
[toto@db ~]$ sudo systemctl enable mariadb
Created symlink /etc/systemd/system/mysql.service → /usr/lib/systemd/system/mariadb.service.
Created symlink /etc/systemd/system/mysqld.service → /usr/lib/systemd/system/mariadb.service.
Created symlink /etc/systemd/system/multi-user.target.wants/mariadb.service → /usr/lib/systemd/system/mariadb.service.
```
**vérifier l'état de mariadb**
```
[toto@db ~]$ systemctl status mariadb
● mariadb.service - MariaDB 10.3 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2021-11-27 01:48:07 CET; 1min 28s ago
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
 Main PID: 5126 (mysqld)
   Status: "Taking your SQL requests now..."
    Tasks: 30 (limit: 4956)
   Memory: 84.2M
   CGroup: /system.slice/mariadb.service
           └─5126 /usr/libexec/mysqld --basedir=/usr

nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: See the MariaDB Knowledgebase at http://mariadb.com/kb or the
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: MySQL manual for more instructions.
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: Please report any problems at http://mariadb.org/jira
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: The latest information about MariaDB is available at http://mariadb.org/.
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: You can find additional information about the MySQL part at:
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: http://dev.mysql.com
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: Consider joining MariaDB's strong and vibrant community:
nov. 27 01:48:07 db.tp5.linux mysql-prepare-db-dir[5023]: https://mariadb.org/get-involved/
nov. 27 01:48:07 db.tp5.linux mysqld[5126]: 2021-11-27  1:48:07 0 [Note] /usr/libexec/mysqld (mysqld 10.3.28-MariaDB) starting as process 5126 ...
nov. 27 01:48:07 db.tp5.linux systemd[1]: Started MariaDB 10.3 database server.
```
**le port de base**
```
[toto@db ~]$ sudo ss -lanpt | grep mysqld
LISTEN 0      80                 *:3306            *:*     users:(("mysqld",pid=5126,fd=21))
```
**processus sous l'utilisateur mysql**
```
[toto@db ~]$ ps -ef | grep mysqld
mysql       5126       1  0 01:48 ?        00:00:00 /usr/libexec/mysqld --basedir=/usr
```
**ouverture du port 3306**
```
[toto@db ~]$ sudo firewall-cmd --add-port=3306/tcp --permanent
success
[toto@db ~]$ sudo firewall-cmd --reload
success
```
**question securité**
```
[toto@db ~]$ mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y
New password:
Re-enter new password:
Sorry, you can't use an empty password here.

New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.
```
**Description des questions**
Pour la premiere question on change ou ajoute un mot de passe a root afin de reforcer la sécurité et qu'il n'y ai que moi qui puisse s'y connecter.
Pour la deuxieme question on supprime l'utilisateur anonyme afin de commencer a travailler car sans ça il peut être dangereux car 
Interdire la connexion a root a distance permet de sécurisé root a une éventuelle attaque de l'exterrieur.
Il faut supprimer la base de donnée test car tous le monde y a accés.
Recharger les privileges rendra les changement opérer immédiat.

**test**

## WEB

**installer httpd**
```
[toto@localhost ~]$ sudo dnf install httpd
```
**lancement de httpd**
```
[toto@localhost ~]$ systemctl start httpd
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ====
Authentification requise pour démarrer « httpd.service ».
Authenticating as: toto
Password:
==== AUTHENTICATION COMPLETE ====
[toto@localhost ~]$ systemctl enable httpd
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-unit-files ====
Authentication is required to manage system service or unit files.
Authenticating as: toto
Password:
==== AUTHENTICATION COMPLETE ====
Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service → /usr/lib/systemd/system/httpd.service.
==== AUTHENTICATING FOR org.freedesktop.systemd1.reload-daemon ====
Authentication is required to reload the systemd state.
Authenticating as: toto
Password:
```
**processus lié à httpd**
```
[toto@localhost ~]$ ps -ef | grep httpd
root        6194       1  0 20:31 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache      6195    6194  0 20:31 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache      6196    6194  0 20:31 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache      6197    6194  0 20:31 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache      6198    6194  0 20:31 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
toto        6471    6138  0 20:34 pts/1    00:00:00 grep --color=auto httpd
```
**Le port d'écoute**
```
[toto@localhost ~]$ sudo ss -lanpt | grep httpd
LISTEN 0      128                *:80              *:*     users:(("httpd",pid=6198,fd=4),("httpd",pid=6197,fd=4),("httpd",pid=6196,fd=4),("httpd",pid=6194,fd=4))
```
```L'utilisateur de httpd est apache```
**ouverture du port 80**
```
[toto@localhost ~]$ sudo firewall-cmd --add-port=80/tcp --permanent
success
[toto@localhost ~]$ sudo firewall-cmd --reload
success
```
**[curl](https://github.com/AntoineMACHY/TP/blob/main/fichier-td5/page-web.md)**

**Telecharger PHP**
```
sudo dnf install epel-release
sudo dnf update
sudo dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf module enable php:remi-7.4
sudo dnf install zip unzip libxml2 openssl php74-php php74-php-ctype php74-php-curl php74-php-gd php74-php-iconv php74-php-json php74-php-libxml php74-php-mbstring php74-php-openssl php74-php-posix php74-php-session php74-php-xml php74-php-zip php74-php-zlib php74-php-pdo php74-php-mysqlnd php74-php-intl php74-php-bcmath php74-php-gmp
```
**Analyser de la conf**
```
# Load config files in the "/etc/httpd/conf.d" directory, if any.
IncludeOptional conf.d/*.conf
```
