### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="9e935-101">Een DNS-label configureren voor het openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="9e935-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="9e935-102">Als u vanaf internet verbinding wilt maken met de SQL Server Database Engine, kunt u overwegen om een DNS-label te maken voor uw openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9e935-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="9e935-103">U kunt ook verbinding maken met behulp van een IP-adres, maar het DNS-label resulteert in een A-record die eenvoudiger te identificeren is en die het onderliggende openbare IP-adres maskeert.</span><span class="sxs-lookup"><span data-stu-id="9e935-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="9e935-104">DNS-labels zijn niet vereist als u alleen verbinding wilt maken met het SQL Server-exemplaar binnen hetzelfde virtuele netwerk of alleen lokaal verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="9e935-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="9e935-105">Als u een DNS-label wilt maken, selecteert u eerst **Virtuele machines** in de portal.</span><span class="sxs-lookup"><span data-stu-id="9e935-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="9e935-106">Selecteer uw SQL Server VM om de eigenschappen op te halen.</span><span class="sxs-lookup"><span data-stu-id="9e935-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="9e935-107">Selecteer uw **openbare IP-adres** in het overzicht van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9e935-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![openbaar ip adres](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="9e935-109">Vouw in de eigenschappen voor uw openbare IP-adres **Configuratie** open.</span><span class="sxs-lookup"><span data-stu-id="9e935-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="9e935-110">Voer een naam voor het DNS-label in.</span><span class="sxs-lookup"><span data-stu-id="9e935-110">Enter a DNS Label name.</span></span> <span data-ttu-id="9e935-111">Deze naam is een A-Record die kan worden gebruikt om verbinding maken met uw SQL Server VM met uw naam in plaats van rechtstreeks met het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9e935-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="9e935-112">Klik op de knop **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9e935-112">Click the **Save** button.</span></span>

    ![dns label](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="9e935-114">Verbinding maken met de Database-engine vanaf een andere computer</span><span class="sxs-lookup"><span data-stu-id="9e935-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="9e935-115">Open SQL Server Management Studio (SSMS) op een computer die is verbonden met internet.</span><span class="sxs-lookup"><span data-stu-id="9e935-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9e935-116">Als u niet beschikt over SQL Server Management Studio, kunt u dit programma [hier](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) downloaden.</span><span class="sxs-lookup"><span data-stu-id="9e935-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="9e935-117">Bewerk in het dialoogvenster **Verbinding maken met server** of **Verbinding maken met Database-engine** de waarde voor **Servernaam**.</span><span class="sxs-lookup"><span data-stu-id="9e935-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="9e935-118">Voer het IP-adres of de volledige DNS-naam van de virtuele machine in (zoals bepaald in de vorige taak).</span><span class="sxs-lookup"><span data-stu-id="9e935-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="9e935-119">U kunt ook een komma toevoegen en de TCP-poort van SQL Server opgeven.</span><span class="sxs-lookup"><span data-stu-id="9e935-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="9e935-120">Bijvoorbeeld `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="9e935-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="9e935-121">Kies in het vak **Verificatie** **SQL Server-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="9e935-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="9e935-122">Typ in het vak **Aanmelden** een geldige SQL-aanmeldingsnaam.</span><span class="sxs-lookup"><span data-stu-id="9e935-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="9e935-123">Typ in het vak **Wachtwoord** het wachtwoord van de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9e935-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="9e935-124">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="9e935-124">Click **Connect**.</span></span>

    ![ssms verbinden](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)