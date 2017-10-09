
1. <span data-ttu-id="9c9a8-101">tooescalate bevoegdheden, type:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="9c9a8-102">Voer uw wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-102">Enter your password.</span></span>
2. <span data-ttu-id="9c9a8-103">tooinstall MySQL Community Server edition, typt u:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="9c9a8-104">Een ogenblik geduld terwijl MySQL downloadt en installeert.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="9c9a8-105">tooset MySQL toostart wanneer Hallo-systeem wordt opgestart, type:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="9c9a8-106">Hallo MySQL-daemon (mysqld) handmatig starten met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="9c9a8-107">toocheck hello status Hallo MySQL-daemon, typt u:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="9c9a8-108">toostop hello MySQL-daemon, typt u:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="9c9a8-109">Hallo MySQL hoofdwachtwoord is na de installatie standaard leeg.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="9c9a8-110">Het is raadzaam dat u uitvoert **mysql\_beveiligde\_installatie**, een script waarmee veilige MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="9c9a8-111">Hallo script toochange Hallo MySQL hoofdwachtwoord wordt u gevraagd, verwijdert anonieme gebruikersaccounts, externe hoofdmap aanmeldingen uitschakelen, test databases verwijderen en opnieuw laden Hallo bevoegdheden tabel.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="9c9a8-112">We raden u antwoord Ja tooall van deze opties en Hallo root-wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="9c9a8-113">Typ deze toorun Hallo script installatiescript MySQL:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="9c9a8-114">Meld u bij tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="9c9a8-115">Voer Hallo MySQL hoofdwachtwoord (die u in de vorige stap Hallo gewijzigd) en u moet worden gepresenteerd met een prompt waar kunt u SQL-instructies toointeract uitgeven met Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="9c9a8-116">toocreate een nieuwe MySQL-gebruiker, voert u Hallo volgende op Hallo **mysql >** prompt:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="9c9a8-117">Opmerking: Hallo puntkomma's (;) aan einde Hallo Hallo regels zijn essentieel voor het Hallo-opdrachten beëindigen.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="9c9a8-118">een database en verleen Hallo toocreate `mysqluser` gebruikersmachtigingen voor het probleem Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="9c9a8-119">Houd er rekening mee database gebruikersnamen en wachtwoorden alleen worden gebruikt door de scripts toohello database verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="9c9a8-120">Account voor database gebruikersnamen noodzakelijkerwijs niet werkelijke gebruikersaccounts op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="9c9a8-121">toolog in van een andere computer, type:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="9c9a8-122">waar `ip-address` Hallo IP-adres van Hallo computer van waaruit u tooMySQL verbinding.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="9c9a8-123">tooexit hello beheerprogramma MySQL-database, typt u:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="9c9a8-124">Een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="9c9a8-124">Add an endpoint</span></span>
1. <span data-ttu-id="9c9a8-125">Nadat de MySQL is geïnstalleerd, moet u een eindpunt tooaccess MySQL tooconfigure op afstand.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="9c9a8-126">Meld u bij toohello [klassieke Azure-portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="9c9a8-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="9c9a8-127">Klik op **virtuele Machines**Hallo-naam van uw nieuwe virtuele machine op en klik vervolgens op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="9c9a8-128">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="9c9a8-129">Toevoegen van een eindpunt met de naam 'MySQL' met protocol **TCP**, en **openbare** en **persoonlijke** poorten set te '3306'.</span><span class="sxs-lookup"><span data-stu-id="9c9a8-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="9c9a8-130">tooremotely verbinding toohello virtuele machine maken van uw computer, type:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="9c9a8-131">Gebruik Hallo virtuele machine die we in deze zelfstudie hebt gemaakt, typ deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="9c9a8-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
