

![Virtuele machines in een zelfstandige cloudservice](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="a2ba8-102">Als u uw virtuele machines in een virtueel netwerk inschakelt, kunt u bepalen hoeveel cloud-services die u wilt dat toouse voor load balancing en beschikbaarheid sets.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want toouse for load balancing and availability sets.</span></span> <span data-ttu-id="a2ba8-103">Bovendien kunt u virtuele machines van Hallo indelen op subnetten in Hallo dezelfde manier als uw on-premises netwerk en verbinding Hallo virtueel netwerk tooyour maken lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-103">Additionally, you can organize hello virtual machines on subnets in hello same way as your on-premises network and connect hello virtual network tooyour on-premises network.</span></span> <span data-ttu-id="a2ba8-104">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a2ba8-104">Here's an example:</span></span>

![Virtuele machines in een virtueel netwerk](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="a2ba8-106">Virtuele netwerken zijn Hallo aanbevolen manier tooconnect virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-106">Virtual networks are hello recommended way tooconnect virtual machines in Azure.</span></span> <span data-ttu-id="a2ba8-107">Hallo aanbevolen procedure is tooconfigure elke laag van uw toepassing in een afzonderlijke cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-107">hello best practice is tooconfigure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="a2ba8-108">Echter, moet u mogelijk toocombine sommige virtuele machines van verschillende toepassingslagen in Hallo cloud dezelfde service tooremain binnen Hallo maximaal 200 cloudservices per abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-108">However, you may need toocombine some virtual machines from different application tiers into hello same cloud service tooremain within hello maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="a2ba8-109">tooreview dit en andere beperkingen, Zie [Azure-abonnement en Service-limieten, quota's en beperkingen](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a2ba8-109">tooreview this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="a2ba8-110">Verbinding maken met virtuele machines in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="a2ba8-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="a2ba8-111">tooconnect virtuele machines in een virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="a2ba8-111">tooconnect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="a2ba8-112">Hallo Hallo virtueel netwerk maken [Azure-portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) en 'klassieke implementatie' opgeven.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-112">Create hello virtual network in hello [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="a2ba8-113">Hallo-set van cloud-services voor uw implementatie tooreflect uw ontwerp voor beschikbaarheidssets maken en taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-113">Create hello set of cloud services for your deployment tooreflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="a2ba8-114">In hello Azure-portal, klikt u op **Nieuw > berekenen > Cloudservice** voor elke cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-114">In hello Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="a2ba8-115">Als u details van Hallo cloud service invullen, kies dezelfde Hallo _resourcegroep_ gebruikt met Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-115">As you fill out hello cloud service details, choose hello same _resource group_ used with hello virtual network.</span></span>

3. <span data-ttu-id="a2ba8-116">toocreate elke nieuwe virtuele machine, klikt u op **Nieuw > berekenen**, en selecteer Hallo juiste VM-installatiekopie uit Hallo **aanbevolen apps**.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-116">toocreate each new virtual machine, click **New > Compute**, then select hello appropriate VM image from hello **Featured apps**.</span></span>

  <span data-ttu-id="a2ba8-117">In Hallo VM **basisbeginselen** blade kiezen Hallo dezelfde _resourcegroep_ gebruikt met Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-117">In hello VM **Basics** blade, choose hello same _resource group_ used with hello virtual network.</span></span>

  ![Basisprincipes van VM-blade wanneer u een VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="a2ba8-119">Terwijl u Hallo VM invult **instellingen**, kies de juiste Hallo _Cloudservice_ of _virtueel netwerk_ voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-119">As you fill out hello VM **Settings**, choose hello correct _Cloud service_ or _virtual network_ for hello VM.</span></span>

  <span data-ttu-id="a2ba8-120">Azure selecteert Hallo andere item op basis van uw selectie.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-120">Azure will select hello other item based on your selection.</span></span>

  ![Blade van de VM-instellingen wanneer u een VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="a2ba8-122">Verbinding maken met virtuele machines in een zelfstandige cloudservice</span><span class="sxs-lookup"><span data-stu-id="a2ba8-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="a2ba8-123">tooconnect virtuele machines in een zelfstandige cloudservice:</span><span class="sxs-lookup"><span data-stu-id="a2ba8-123">tooconnect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="a2ba8-124">Hallo-cloudservice maken in Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2ba8-124">Create hello cloud service in hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a2ba8-125">Klik op **Nieuw > berekenen > Cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="a2ba8-126">Of u kunt Hallo cloudservice voor uw implementatie maken bij het maken van uw eerste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-126">Or, you can create hello cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="a2ba8-127">Wanneer u Hallo virtuele machines maakt, kiest u Hallo dezelfde resourcegroep met Hallo-cloudservice gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-127">When you create hello virtual machines, choose hello same resource group used with hello cloud service.</span></span>

  ![Een virtuele machine tooan bestaande cloudservice toevoegen](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="a2ba8-129">Als u details van de VM Hallo invullen, kiest u Hallo-naam van cloudservice gemaakt in de eerste stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2ba8-129">As you fill out hello VM details, choose hello name of cloud service created in hello first step.</span></span>

  ![Een cloudservice voor een virtuele machine selecteren](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
