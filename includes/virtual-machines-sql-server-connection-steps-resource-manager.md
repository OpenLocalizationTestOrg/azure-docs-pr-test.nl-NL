### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="03152-101">Een DNS-Label configureren voor het openbare IP-adres Hallo</span><span class="sxs-lookup"><span data-stu-id="03152-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="03152-102">tooconnect toohello SQL Server Database Engine van Hallo Internet, overweeg te maken van een DNS-Label voor uw openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="03152-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="03152-103">U kunt verbinding maken met IP-adres, maar Hallo DNS-Label maakt een A-Record is eenvoudiger tooidentify en samenvattingen Hallo onderliggende openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="03152-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="03152-104">DNS-Labels zijn niet vereist als u plan tooonly verbinding toohello SQL Server-exemplaar binnen Hallo hetzelfde virtuele netwerk of alleen lokaal.</span><span class="sxs-lookup"><span data-stu-id="03152-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="03152-105">selecteert u eerst een DNS-Label toocreate **virtuele machines** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="03152-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="03152-106">Selecteer uw SQL Server VM toobring kunt u de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="03152-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="03152-107">Selecteer in het overzicht van de virtuele machines hello, uw **openbaar IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="03152-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![openbaar ip adres](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="03152-109">Vouw in de eigenschappen voor uw openbare IP-adres van Hallo **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="03152-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="03152-110">Voer een naam voor het DNS-label in.</span><span class="sxs-lookup"><span data-stu-id="03152-110">Enter a DNS Label name.</span></span> <span data-ttu-id="03152-111">Deze naam is een A-Record dat gebruikte tooconnect tooyour SQL Server-VM met de naam in plaats van met IP-adres kan rechtstreeks worden.</span><span class="sxs-lookup"><span data-stu-id="03152-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="03152-112">Klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="03152-112">Click hello **Save** button.</span></span>

    ![dns label](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="03152-114">Verbinding maken met Database-Engine toohello vanaf een andere computer</span><span class="sxs-lookup"><span data-stu-id="03152-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="03152-115">Op een computer verbonden toohello internet, open SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="03152-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="03152-116">Als u niet beschikt over SQL Server Management Studio, kunt u dit programma [hier](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) downloaden.</span><span class="sxs-lookup"><span data-stu-id="03152-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="03152-117">In Hallo **verbinding tooServer** of **tooDatabase Engine verbinding** dialoogvenster, bewerken Hallo **servernaam** waarde.</span><span class="sxs-lookup"><span data-stu-id="03152-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="03152-118">Voer Hallo IP-adres of de volledige DNS-naam van Hallo virtuele machine (bepaald in de vorige taak Hallo).</span><span class="sxs-lookup"><span data-stu-id="03152-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="03152-119">U kunt ook een komma toevoegen en de TCP-poort van SQL Server opgeven.</span><span class="sxs-lookup"><span data-stu-id="03152-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="03152-120">Bijvoorbeeld `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="03152-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="03152-121">In Hallo **verificatie** de optie **SQL Server-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="03152-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="03152-122">In Hallo **aanmelding** vak, type Hallo-naam van een geldige SQL-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="03152-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="03152-123">In Hallo **wachtwoord** vak, het type wachtwoord op Hallo van Hallo aanmelding.</span><span class="sxs-lookup"><span data-stu-id="03152-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="03152-124">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="03152-124">Click **Connect**.</span></span>

    ![ssms verbinden](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)