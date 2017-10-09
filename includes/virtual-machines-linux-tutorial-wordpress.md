## <a name="install-wordpress"></a>WordPress installeren

Als u uw stack tootry wilt, installeert u een voorbeeld-app. Als u bijvoorbeeld Hallo stappen te volgen Hallo open-source installeren [WordPress](https://wordpress.org/) platform toocreate websites en blogs. Andere werkbelastingen tootry omvatten [Drupal](http://www.drupal.org) en [Moodle](https://moodle.org/). 

Dit WordPress is voor het testen van het concept. Zie voor meer informatie en instellingen voor de installatie van de productie Hallo [WordPress documentatie](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Hallo WordPress pakket installeren

Hallo volgende opdracht uitvoeren:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>WordPress configureren

WordPress toouse MySQL en PHP configureren. Hallo opdracht tooopen na een teksteditor van uw keuze uitvoeren en het Hallo-bestand maken `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Kopiëren Hallo volgende regels toohello, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten). Sla Hallo-bestand.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

Maak een tekstbestand in een werkmap `wordpress.sql` tooconfigure Hallo WordPress database: 

```bash
sudo sensible-editor wordpress.sql
```

Toevoegen van Hallo opdrachten te volgen, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten). Sla Hallo-bestand.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Voer Hallo opdracht toocreate Hallo database te volgen:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Nadat het Hallo-opdracht is voltooid, verwijdert Hallo bestand `wordpress.sql`.

Hallo WordPress installatie toohello web server documenthoofdmap verplaatsen:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

U kunt nu Hallo WordPress-installatie is voltooid en publiceren op Hallo-platform. Open een browser en ga te`http://yourPublicIPAddress/wordpress`. Vervang Hallo openbare IP-adres van uw virtuele machine. Dit ziet vergelijkbare toothis afbeelding.

![Pagina met WordPress-installatie](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)