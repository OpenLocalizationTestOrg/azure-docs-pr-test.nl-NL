## <a name="how-to-create-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="fa793-101">Het maken van een klassiek VNet met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fa793-101">How to create a classic VNet using Azure CLI</span></span>
<span data-ttu-id="fa793-102">U kunt Azure CLI gebruiken voor het beheer van uw Azure-resources via de opdrachtprompt op elke computer met Windows, Linux of OS X.</span><span class="sxs-lookup"><span data-stu-id="fa793-102">You can use the Azure CLI to manage your Azure resources from the command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="fa793-103">Volg de onderstaande stappen om een VNet te maken met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fa793-103">To create a VNet by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="fa793-104">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../articles/cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="fa793-104">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../articles/cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fa793-105">Voer de opdracht **azure network vnet create** uit om een VNet en een subnet te maken, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa793-105">Run the **azure network vnet create** command to create a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="fa793-106">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="fa793-106">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="fa793-107">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="fa793-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="fa793-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="fa793-108">**--vnet**.</span></span> <span data-ttu-id="fa793-109">Naam van de VNet die moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa793-109">Name of the VNet to be created.</span></span> <span data-ttu-id="fa793-110">In ons scenario *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="fa793-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="fa793-111">**-e (of--adresruimte)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="fa793-112">VNet-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="fa793-112">VNet address space.</span></span> <span data-ttu-id="fa793-113">In ons scenario *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="fa793-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="fa793-114">**-i (of de cidr-)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="fa793-115">Het netwerkmasker in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="fa793-115">Network mask in CIDR format.</span></span> <span data-ttu-id="fa793-116">In ons scenario *16*.</span><span class="sxs-lookup"><span data-stu-id="fa793-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="fa793-117">**-n (of--subnet naam**).</span><span class="sxs-lookup"><span data-stu-id="fa793-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="fa793-118">Naam van het eerste subnet.</span><span class="sxs-lookup"><span data-stu-id="fa793-118">Name of the first subnet.</span></span> <span data-ttu-id="fa793-119">In ons scenario *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="fa793-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="fa793-120">**-p (of--begin-ip-subnet)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="fa793-121">IP-adres voor het subnet of subnetadresruimte wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="fa793-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="fa793-122">In ons scenario *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="fa793-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="fa793-123">**-r (of--subnet cidr)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="fa793-124">Het netwerkmasker in CIDR-indeling voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="fa793-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="fa793-125">In ons scenario *24*.</span><span class="sxs-lookup"><span data-stu-id="fa793-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="fa793-126">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-126">**-l (or --location)**.</span></span> <span data-ttu-id="fa793-127">De Azure-regio waar de VNet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa793-127">Azure region where the VNet will be created.</span></span> <span data-ttu-id="fa793-128">In ons scenario *VS-midden*.</span><span class="sxs-lookup"><span data-stu-id="fa793-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="fa793-129">Voer de opdracht **azure network vnet subnet create** om een subnet te maken, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa793-129">Run the **azure network vnet subnet create** command to create a subnet as shown below.</span></span> <span data-ttu-id="fa793-130">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="fa793-130">The list shown after the output explains the parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="fa793-131">Dit is de verwachte uitvoer voor de bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="fa793-131">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="fa793-132">**-t (of--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="fa793-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="fa793-133">Naam van de VNet waar het subnet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa793-133">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="fa793-134">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="fa793-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="fa793-135">**-n (of --name)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-135">**-n (or --name)**.</span></span> <span data-ttu-id="fa793-136">Naam van het nieuwe subnet.</span><span class="sxs-lookup"><span data-stu-id="fa793-136">Name of the new subnet.</span></span> <span data-ttu-id="fa793-137">In ons scenario *back-end*.</span><span class="sxs-lookup"><span data-stu-id="fa793-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="fa793-138">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="fa793-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="fa793-139">Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="fa793-139">Subnet CIDR block.</span></span> <span data-ttu-id="fa793-140">Vier in ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="fa793-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="fa793-141">Voer de opdracht **azure network vnet show** uit om de eigenschappen van de nieuwe VNet weer te geven, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa793-141">Run the **azure network vnet show** command to view the properties of the new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="fa793-142">Dit is de verwachte uitvoer voor de bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="fa793-142">Here is the expected output for the command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

