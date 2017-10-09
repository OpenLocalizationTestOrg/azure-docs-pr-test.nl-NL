## <a name="install-wordpress"></a><span data-ttu-id="ec71a-101">WordPress installeren</span><span class="sxs-lookup"><span data-stu-id="ec71a-101">Install WordPress</span></span>

<span data-ttu-id="ec71a-102">Als u uw stack tootry wilt, installeert u een voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="ec71a-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="ec71a-103">Als u bijvoorbeeld Hallo stappen te volgen Hallo open-source installeren [WordPress](https://wordpress.org/) platform toocreate websites en blogs.</span><span class="sxs-lookup"><span data-stu-id="ec71a-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="ec71a-104">Andere werkbelastingen tootry omvatten [Drupal](http://www.drupal.org) en [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="ec71a-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="ec71a-105">Dit WordPress is voor het testen van het concept.</span><span class="sxs-lookup"><span data-stu-id="ec71a-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="ec71a-106">Zie voor meer informatie en instellingen voor de installatie van de productie Hallo [WordPress documentatie](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="ec71a-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="ec71a-107">Hallo WordPress pakket installeren</span><span class="sxs-lookup"><span data-stu-id="ec71a-107">Install hello WordPress package</span></span>

<span data-ttu-id="ec71a-108">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ec71a-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="ec71a-109">WordPress configureren</span><span class="sxs-lookup"><span data-stu-id="ec71a-109">Configure WordPress</span></span>

<span data-ttu-id="ec71a-110">WordPress toouse MySQL en PHP configureren.</span><span class="sxs-lookup"><span data-stu-id="ec71a-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="ec71a-111">Hallo opdracht tooopen na een teksteditor van uw keuze uitvoeren en het Hallo-bestand maken `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="ec71a-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="ec71a-112">Kopiëren Hallo volgende regels toohello, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten).</span><span class="sxs-lookup"><span data-stu-id="ec71a-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="ec71a-113">Sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="ec71a-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="ec71a-114">Maak een tekstbestand in een werkmap `wordpress.sql` tooconfigure Hallo WordPress database:</span><span class="sxs-lookup"><span data-stu-id="ec71a-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="ec71a-115">Toevoegen van Hallo opdrachten te volgen, vervangen door een wachtwoord voor de database voor *yourPassword* (andere waarden ongewijzigd laten).</span><span class="sxs-lookup"><span data-stu-id="ec71a-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="ec71a-116">Sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="ec71a-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="ec71a-117">Voer Hallo opdracht toocreate Hallo database te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec71a-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="ec71a-118">Nadat het Hallo-opdracht is voltooid, verwijdert Hallo bestand `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="ec71a-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="ec71a-119">Hallo WordPress installatie toohello web server documenthoofdmap verplaatsen:</span><span class="sxs-lookup"><span data-stu-id="ec71a-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="ec71a-120">U kunt nu Hallo WordPress-installatie is voltooid en publiceren op Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="ec71a-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="ec71a-121">Open een browser en ga te`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="ec71a-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="ec71a-122">Vervang Hallo openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ec71a-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="ec71a-123">Dit ziet vergelijkbare toothis afbeelding.</span><span class="sxs-lookup"><span data-stu-id="ec71a-123">It should look similar toothis image.</span></span>

![Pagina met WordPress-installatie](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)