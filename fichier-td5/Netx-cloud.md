```
<VirtualHost *:80>
  # on précise ici le dossier qui contiendra le site : la racine Web
  DocumentRoot /var/www/nextcloud/html/  

  # ici le nom qui sera utilisé pour accéder à l'application
  ServerName  web.tp5.linux  

  <Directory /var/www/nextcloud/html/>
    Require all granted
    AllowOverride All
    Options FollowSymLinks MultiViews

    <IfModule mod_dav.c>
      Dav off
    </IfModule>
  </Directory>
</VirtualHost>
```