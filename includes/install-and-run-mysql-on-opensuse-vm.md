
1. <span data-ttu-id="557fd-101">Als u wilt escaleren bevoegdheden, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-101">To escalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="557fd-102">Voer uw wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="557fd-102">Enter your password.</span></span>
2. <span data-ttu-id="557fd-103">Voor het installeren van MySQL-Community servereditie, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-103">To install MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="557fd-104">Een ogenblik geduld terwijl MySQL downloadt en installeert.</span><span class="sxs-lookup"><span data-stu-id="557fd-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="557fd-105">Om in te stellen MySQL wordt gestart wanneer het systeem wordt opgestart, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-105">To set MySQL to start when the system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="557fd-106">De MySQL-daemon (mysqld) handmatig starten met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="557fd-106">Start the MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="557fd-107">Als u wilt de status van de MySQL-daemon controleren, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-107">To check the status of the MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="557fd-108">Als u wilt de MySQL-daemon stoppen, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-108">To stop the MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="557fd-109">Na de installatie is het hoofdwachtwoord MySQL standaard leeg.</span><span class="sxs-lookup"><span data-stu-id="557fd-109">After installation, the MySQL root password is empty by default.</span></span> <span data-ttu-id="557fd-110">Het is raadzaam dat u uitvoert **mysql\_beveiligde\_installatie**, een script waarmee veilige MySQL.</span><span class="sxs-lookup"><span data-stu-id="557fd-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="557fd-111">Het script vraagt u om te wijzigen van het hoofdwachtwoord MySQL, verwijdert u anonieme gebruikersaccounts, externe hoofdmap aanmeldingen uitschakelen, test databases verwijderen en opnieuw laden van de tabel bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="557fd-111">The script prompts you to change the MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload the privileges table.</span></span> <span data-ttu-id="557fd-112">We raden u antwoord Ja op al deze opties en het root-wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="557fd-112">We recommended that you answer yes to all of these options and change the root password.</span></span>
   > 
   > 
5. <span data-ttu-id="557fd-113">Typ dit script van MySQL voor installatie van het script uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="557fd-113">Type this to run the script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="557fd-114">Aanmelden bij MySQL:</span><span class="sxs-lookup"><span data-stu-id="557fd-114">Log in to MySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="557fd-115">Voer het hoofdwachtwoord van MySQL (die u hebt gewijzigd in de vorige stap) en er moet worden weergegeven met een prompt waar SQL-instructies om te communiceren met de database kunnen worden verleend.</span><span class="sxs-lookup"><span data-stu-id="557fd-115">Enter the MySQL root password (which you changed in the previous step) and you'll be presented with a prompt where you can issue SQL statements to interact with the database.</span></span>
7. <span data-ttu-id="557fd-116">Voor het maken van een nieuwe MySQL-gebruiker, voert u de volgende op de **mysql >** prompt:</span><span class="sxs-lookup"><span data-stu-id="557fd-116">To create a new MySQL user, run the following at the **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="557fd-117">Opmerking: de puntkomma (;) aan het einde van de regels zijn essentieel voor het beëindigen van de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="557fd-117">Note, the semi-colons (;) at the end of the lines are crucial for ending the commands.</span></span>
8. <span data-ttu-id="557fd-118">Een database maken en verlenen de `mysqluser` gebruikersmachtigingen voor het uitgeven van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="557fd-118">To create a database and grant the `mysqluser` user permissions on it, issue the following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="557fd-119">Houd er rekening mee dat database gebruikersnamen en wachtwoorden alleen worden gebruikt door scripts verbinden met de database.</span><span class="sxs-lookup"><span data-stu-id="557fd-119">Note that database user names and passwords are only used by scripts connecting to the database.</span></span>  <span data-ttu-id="557fd-120">Account voor database gebruikersnamen noodzakelijkerwijs niet werkelijke gebruikersaccounts op het systeem.</span><span class="sxs-lookup"><span data-stu-id="557fd-120">Database user account names do not necessarily represent actual user accounts on the system.</span></span>
9. <span data-ttu-id="557fd-121">Als u wilt zich aanmelden vanaf een andere computer, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-121">To log in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="557fd-122">waar `ip-address` het IP-adres van de computer van waaruit u verbinding met MySQL.</span><span class="sxs-lookup"><span data-stu-id="557fd-122">where `ip-address` is the IP address of the computer from which you will connect to MySQL.</span></span>
10. <span data-ttu-id="557fd-123">Typ de MySQL-database-beheerprogramma om af te sluiten:</span><span class="sxs-lookup"><span data-stu-id="557fd-123">To exit the MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="557fd-124">Een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="557fd-124">Add an endpoint</span></span>
1. <span data-ttu-id="557fd-125">Nadat de MySQL is geïnstalleerd, moet u een eindpunt voor MySQL op afstand toegang tot configureren.</span><span class="sxs-lookup"><span data-stu-id="557fd-125">After MySQL is installed, you'll need to configure an endpoint to access MySQL remotely.</span></span> <span data-ttu-id="557fd-126">Meld u aan bij de [klassieke Azure-portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="557fd-126">Log in to the [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="557fd-127">Klik op **virtuele Machines**, klik op de naam van uw nieuwe virtuele machine en klik vervolgens op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="557fd-127">Click **Virtual Machines**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="557fd-128">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="557fd-128">Click **Add** at the bottom of the page.</span></span>
3. <span data-ttu-id="557fd-129">Toevoegen van een eindpunt met de naam 'MySQL' met protocol **TCP**, en **openbare** en **persoonlijke** poorten ingesteld op '3306'.</span><span class="sxs-lookup"><span data-stu-id="557fd-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set to "3306".</span></span>
4. <span data-ttu-id="557fd-130">Om extern verbinding maken met de virtuele machine van de computer, typt u:</span><span class="sxs-lookup"><span data-stu-id="557fd-130">To remotely connect to the virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="557fd-131">Met behulp van de virtuele machine die we in deze zelfstudie hebt gemaakt, typ deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="557fd-131">For example, using the virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
