## <a name="install-wordpress"></a><span data-ttu-id="7b954-101">WordPress installeren</span><span class="sxs-lookup"><span data-stu-id="7b954-101">Install WordPress</span></span>

<span data-ttu-id="7b954-102">Als u uw stack proberen wilt, installeert u een voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="7b954-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="7b954-103">Als u bijvoorbeeld de volgende stappen uit de open source installeren [WordPress](https://wordpress.org/) platform om websites en blogs te maken.</span><span class="sxs-lookup"><span data-stu-id="7b954-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="7b954-104">Andere werkbelastingen om te proberen behoren [Drupal](http://www.drupal.org) en [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="7b954-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="7b954-105">Dit WordPress is voor het testen van het concept.</span><span class="sxs-lookup"><span data-stu-id="7b954-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="7b954-106">Zie voor meer informatie en instellingen voor de installatie van de productie, de [WordPress documentatie](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="7b954-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="7b954-107">De WordPress-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="7b954-107">Install the WordPress package</span></span>

<span data-ttu-id="7b954-108">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="7b954-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="7b954-109">WordPress configureren</span><span class="sxs-lookup"><span data-stu-id="7b954-109">Configure WordPress</span></span>

<span data-ttu-id="7b954-110">Configureer WordPress voor het gebruik van MySQL en PHP.</span><span class="sxs-lookup"><span data-stu-id="7b954-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="7b954-111">Voer de volgende opdracht te open een teksteditor van uw keuze en maak het bestand `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="7b954-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="7b954-112">Kopieer de volgende regels op het bestand, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten).</span><span class="sxs-lookup"><span data-stu-id="7b954-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7b954-113">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="7b954-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="7b954-114">Maak een tekstbestand in een werkmap `wordpress.sql` de WordPress-database configureren:</span><span class="sxs-lookup"><span data-stu-id="7b954-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="7b954-115">Voeg de volgende opdrachten, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten).</span><span class="sxs-lookup"><span data-stu-id="7b954-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7b954-116">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="7b954-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="7b954-117">Voer de volgende opdracht om de database te maken:</span><span class="sxs-lookup"><span data-stu-id="7b954-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="7b954-118">Nadat de opdracht is voltooid, verwijdert u het bestand `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="7b954-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="7b954-119">De WordPress-installatie verplaatsen naar de hoofdmap van het web server-document:</span><span class="sxs-lookup"><span data-stu-id="7b954-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="7b954-120">U kunt nu de WordPress-installatie is voltooid en publiceren van het platform.</span><span class="sxs-lookup"><span data-stu-id="7b954-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="7b954-121">Open een browser en Ga naar `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="7b954-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="7b954-122">Vervang het openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b954-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="7b954-123">Het moet eruitzien als aan deze installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7b954-123">It should look similar to this image.</span></span>

![Pagina met WordPress-installatie](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)