## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="f37ed-101">Hoe toocreate een klassiek VNet met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f37ed-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="f37ed-102">U kunt uw Azure-resources via de opdrachtprompt Hallo vanaf elke computer met Windows, Linux of OS x hello Azure CLI toomanage.</span><span class="sxs-lookup"><span data-stu-id="f37ed-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="f37ed-103">een VNet met behulp van Azure CLI Hallo toocreate Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f37ed-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="f37ed-104">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../articles/cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="f37ed-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f37ed-105">Voer Hallo **azure network vnet maken** opdracht toocreate een VNet en een subnet, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f37ed-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="f37ed-106">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f37ed-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="f37ed-107">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f37ed-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="f37ed-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-108">**--vnet**.</span></span> <span data-ttu-id="f37ed-109">Naam van Hallo VNet toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f37ed-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="f37ed-110">In ons scenario *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="f37ed-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="f37ed-111">**-e (of--adresruimte)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="f37ed-112">VNet-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="f37ed-112">VNet address space.</span></span> <span data-ttu-id="f37ed-113">In ons scenario *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="f37ed-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="f37ed-114">**-i (of de cidr-)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="f37ed-115">Het netwerkmasker in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="f37ed-115">Network mask in CIDR format.</span></span> <span data-ttu-id="f37ed-116">In ons scenario *16*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="f37ed-117">**-n (of--subnet naam**).</span><span class="sxs-lookup"><span data-stu-id="f37ed-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="f37ed-118">Naam van het eerste subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="f37ed-118">Name of hello first subnet.</span></span> <span data-ttu-id="f37ed-119">In ons scenario *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="f37ed-120">**-p (of--begin-ip-subnet)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="f37ed-121">IP-adres voor het subnet of subnetadresruimte wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="f37ed-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="f37ed-122">In ons scenario *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="f37ed-123">**-r (of--subnet cidr)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="f37ed-124">Het netwerkmasker in CIDR-indeling voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="f37ed-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="f37ed-125">In ons scenario *24*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="f37ed-126">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-126">**-l (or --location)**.</span></span> <span data-ttu-id="f37ed-127">Azure-regio waar Hallo VNet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f37ed-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="f37ed-128">In ons scenario *VS-midden*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="f37ed-129">Voer Hallo **azure network vnet subnet maken** opdracht toocreate een subnet, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f37ed-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="f37ed-130">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f37ed-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="f37ed-131">Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="f37ed-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="f37ed-132">**-t (of--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="f37ed-133">Naam van Hallo VNet waar Hallo subnet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f37ed-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="f37ed-134">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="f37ed-135">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-135">**-n (or --name)**.</span></span> <span data-ttu-id="f37ed-136">Naam van nieuw subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="f37ed-136">Name of hello new subnet.</span></span> <span data-ttu-id="f37ed-137">In ons scenario *back-end*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="f37ed-138">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="f37ed-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="f37ed-139">Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="f37ed-139">Subnet CIDR block.</span></span> <span data-ttu-id="f37ed-140">Vier in ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f37ed-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="f37ed-141">Voer Hallo **azure network vnet show** opdracht tooview Hallo eigenschappen van nieuwe vnet hello, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f37ed-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="f37ed-142">Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="f37ed-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
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

