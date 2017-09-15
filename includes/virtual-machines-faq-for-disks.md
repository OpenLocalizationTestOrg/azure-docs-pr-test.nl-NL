# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="bc63d-101">Veelgestelde vragen over Azure IaaS VM-schijven en beheerde en onbeheerde premium-schijven</span><span class="sxs-lookup"><span data-stu-id="bc63d-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="bc63d-102">Dit artikel worden enkele veelgestelde vragen over Azure beheerd schijven en Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="bc63d-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="bc63d-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="bc63d-103">Managed Disks</span></span>

<span data-ttu-id="bc63d-104">**Wat is Azure beheerd schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="bc63d-105">Beheerde schijven is een functie die vereenvoudigt Schijfbeheer voor Azure IaaS VM's met opslagbeheer-account voor u verwerken.</span><span class="sxs-lookup"><span data-stu-id="bc63d-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="bc63d-106">Zie voor meer informatie de [schijven beheerd overzicht](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc63d-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="bc63d-107">**Als ik een standard-beheerde schijven van een bestaande VHD 80 GB maken, hoeveel die kost mij?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="bc63d-108">Een standard-beheerde schijven gemaakt op basis van een VHD 80 GB wordt beschouwd als de volgende beschikbare standaard schijfgrootte, die een schijf S10.</span><span class="sxs-lookup"><span data-stu-id="bc63d-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="bc63d-109">U kosten in rekening gebracht volgens de S10 schijf prijzen.</span><span class="sxs-lookup"><span data-stu-id="bc63d-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="bc63d-110">Zie de pagina [prijzen](https://azure.microsoft.com/pricing/details/storage) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bc63d-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="bc63d-111">**Zijn er transactiekosten voor standard-beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="bc63d-112">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-112">Yes.</span></span> <span data-ttu-id="bc63d-113">U kosten in rekening gebracht voor elke transactie.</span><span class="sxs-lookup"><span data-stu-id="bc63d-113">You're charged for each transaction.</span></span> <span data-ttu-id="bc63d-114">Zie de pagina [prijzen](https://azure.microsoft.com/pricing/details/storage) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bc63d-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="bc63d-115">**Voor een standaard beheerde schijf wordt ik in rekening gebracht voor de werkelijke grootte van de gegevens op de schijf of voor de ingerichte capaciteit van de schijf?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="bc63d-116">U bent in rekening gebracht op basis van de ingerichte capaciteit van de schijf.</span><span class="sxs-lookup"><span data-stu-id="bc63d-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="bc63d-117">Zie de pagina [prijzen](https://azure.microsoft.com/pricing/details/storage) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bc63d-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="bc63d-118">**Hoe wordt de prijzen van beheerde premium-schijven verschilt van niet-beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="bc63d-119">De prijzen van beheerde premium-schijven is hetzelfde als niet-beheerde premium-schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="bc63d-120">**Kan ik het opslagaccounttype (Standard of Premium) van mijn beheerde schijven wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="bc63d-121">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-121">Yes.</span></span> <span data-ttu-id="bc63d-122">U kunt het opslagtype voor de account van uw beheerde schijven wijzigen met behulp van de Azure-portal, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bc63d-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="bc63d-123">**Is er een manier die ik kan kopiëren of een beheerde schijf exporteren naar een persoonlijke storage-account?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="bc63d-124">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-124">Yes.</span></span> <span data-ttu-id="bc63d-125">U kunt uw beheerde schijven exporteren met behulp van de Azure-portal, PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bc63d-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="bc63d-126">**Kan ik een VHD-bestand in Azure storage-account gebruiken voor het maken van een beheerde schijf met een ander abonnement?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="bc63d-127">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-127">No.</span></span>

<span data-ttu-id="bc63d-128">**Kan ik een VHD-bestand in Azure storage-account gebruiken voor het maken van een beheerde schijf in een andere regio?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="bc63d-129">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-129">No.</span></span>

<span data-ttu-id="bc63d-130">**Zijn er beperkingen scale voor klanten die gebruikmaken van beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="bc63d-131">Beheerde schijven elimineert de grenzen die aan opslagaccounts is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="bc63d-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="bc63d-132">Het aantal beheerde schijven per abonnement is echter standaard beperkt tot 2000.</span><span class="sxs-lookup"><span data-stu-id="bc63d-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="bc63d-133">U kunt ondersteuning voor dit aantal verhoogt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="bc63d-133">You can call support to increase this number.</span></span>

<span data-ttu-id="bc63d-134">**Kan ik een incrementele momentopname van een beheerde schijf volgen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="bc63d-135">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-135">No.</span></span> <span data-ttu-id="bc63d-136">De huidige momentopname maakt een volledige kopie van een beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="bc63d-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="bc63d-137">We zijn echter van plan om ondersteuning voor incrementele momentopnamen in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="bc63d-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="bc63d-138">**Kunnen de virtuele machines in een beschikbaarheidsset bestaan uit een combinatie van beheerde en onbeheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="bc63d-139">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-139">No.</span></span> <span data-ttu-id="bc63d-140">De virtuele machines in een beschikbaarheidsset moeten gebruiken voor alle beheerde schijven of alle niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="bc63d-141">Wanneer u een beschikbaarheidsset maakt, kunt u kiezen welk type schijven dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc63d-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="bc63d-142">**Is beheerd schijven op de standaardoptie in de Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="bc63d-143">Momenteel niet, maar deze wordt standaard in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="bc63d-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="bc63d-144">**Kan ik een lege beheerde schijf maken?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="bc63d-145">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-145">Yes.</span></span> <span data-ttu-id="bc63d-146">U kunt een lege schijf maken.</span><span class="sxs-lookup"><span data-stu-id="bc63d-146">You can create an empty disk.</span></span> <span data-ttu-id="bc63d-147">Een beheerde schijf kan worden gemaakt onafhankelijk van een virtuele machine, bijvoorbeeld, zonder het image koppelt aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bc63d-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="bc63d-148">**Wat is het aantal ondersteunde foutdomeinen voor een beschikbaarheid instellen die gebruikmaakt van schijven beheerd**</span><span class="sxs-lookup"><span data-stu-id="bc63d-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="bc63d-149">Afhankelijk van de regio waar de beschikbaarheidsset die gebruikmaakt van schijven beheerd zich bevindt, is het aantal ondersteunde foutdomeinen 2 of 3.</span><span class="sxs-lookup"><span data-stu-id="bc63d-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="bc63d-150">**Hoe wordt het standaard opslagaccount voor diagnostische gegevens instellen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="bc63d-151">Instellen van een persoonlijke opslagaccount voor diagnostische gegevens van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bc63d-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="bc63d-152">We zullen in de toekomst ook overschakelen van diagnostische gegevens naar de schijven worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="bc63d-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="bc63d-153">**Wat voor soort toegangsbeheer op basis van rollen ondersteuning is beschikbaar voor schijven beheerd?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="bc63d-154">Schijven ondersteunt drie belangrijkste standaardrollen beheerd:</span><span class="sxs-lookup"><span data-stu-id="bc63d-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="bc63d-155">Eigenaar: Kunnen alles beheren, inclusief toegang</span><span class="sxs-lookup"><span data-stu-id="bc63d-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="bc63d-156">Inzender: Kunnen alles beheren behalve toegang</span><span class="sxs-lookup"><span data-stu-id="bc63d-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="bc63d-157">Lezer: Kunnen alles weergeven, maar geen wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="bc63d-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="bc63d-158">**Is er een manier die ik kan kopiëren of een beheerde schijf exporteren naar een persoonlijke storage-account?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="bc63d-159">U kunt een alleen-lezen shared access signature voor URI ophalen voor de beheerde schijf en de inhoud te kopiëren naar een persoonlijke opslag account of on-premises opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc63d-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="bc63d-160">**Kan ik een kopie van de beheerde computer maken?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="bc63d-161">Klanten kunnen een momentopname van het bijbehorende beheerde schijven en gebruik vervolgens de momentopname maken van een andere beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="bc63d-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="bc63d-162">**Worden niet-beheerde schijven nog steeds ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="bc63d-163">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-163">Yes.</span></span> <span data-ttu-id="bc63d-164">Wij ondersteunen onbeheerde en beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="bc63d-165">U wordt aangeraden dat u beheerde schijven voor nieuwe workloads en migreren van uw huidige werkbelastingen naar beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="bc63d-166">**Als ik een schijf van 128 GB maken en vervolgens de grootte tot 130 GB te verhogen, ik gefactureerd voor de volgende schijfgrootte (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="bc63d-167">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-167">Yes.</span></span>

<span data-ttu-id="bc63d-168">**Kan ik geografisch redundante opslag met lokaal redundante opslag maken en zone-redundante opslag schijven die worden beheerd?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="bc63d-169">Azure-beheerde schijven ondersteunt momenteel alleen lokaal redundante opslag beheerd schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="bc63d-170">**Kan ik verkleinen of mijn beheerde schijven afslanken?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="bc63d-171">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-171">No.</span></span> <span data-ttu-id="bc63d-172">Deze functie is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bc63d-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="bc63d-173">**Kan ik de naameigenschap van de computer wijzigen wanneer een gespecialiseerde (niet gemaakt met behulp van het hulpprogramma voor systeemvoorbereiding of gegeneraliseerd) schijf van besturingssysteem wordt gebruikt voor het inrichten van een virtuele machine?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="bc63d-174">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-174">No.</span></span> <span data-ttu-id="bc63d-175">U kunt de naameigenschap van de computer niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="bc63d-175">You can't update the computer name property.</span></span> <span data-ttu-id="bc63d-176">De nieuwe virtuele machine overgenomen van de bovenliggende VM die is gebruikt voor het maken van de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="bc63d-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="bc63d-177">**Waar vind ik Azure Resource Manager voorbeeldsjablonen virtuele machines maken met beheerde-schijven**</span><span class="sxs-lookup"><span data-stu-id="bc63d-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="bc63d-178">Lijst met sjablonen met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="bc63d-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="bc63d-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="bc63d-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="bc63d-180">Beheerd schijven en versleuteling van opslag-Service</span><span class="sxs-lookup"><span data-stu-id="bc63d-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="bc63d-181">**Is Azure Storage-Service: versleuteling standaard ingeschakeld wanneer ik een beheerde schijf maken?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="bc63d-182">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-182">Yes.</span></span>

<span data-ttu-id="bc63d-183">**De versleutelingssleutels die het account?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="bc63d-184">Microsoft beheert de versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="bc63d-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="bc63d-185">**Kan ik voor mijn beheerde schijven versleuteling van opslag Service uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="bc63d-186">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-186">No.</span></span>

<span data-ttu-id="bc63d-187">**Is versleuteling van opslag Service alleen beschikbaar in specifieke gebieden?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="bc63d-188">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-188">No.</span></span> <span data-ttu-id="bc63d-189">Het is beschikbaar in alle regio's waar beheerd schijven beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="bc63d-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="bc63d-190">Beheerde schijven is beschikbaar in alle openbare regio's en Duitsland.</span><span class="sxs-lookup"><span data-stu-id="bc63d-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="bc63d-191">**Hoe vind ik als mijn beheerde schijf worden versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="bc63d-192">U vindt hier de tijd waarop een beheerde schijf is gemaakt in de Azure-portal, Azure CLI en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc63d-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="bc63d-193">De schijf wordt versleuteld als de tijd na 9 juni 2017.</span><span class="sxs-lookup"><span data-stu-id="bc63d-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="bc63d-194">**Hoe kan ik mijn bestaande schijven die zijn gemaakt vóór 10 juni 2017 coderen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="bc63d-195">Vanaf 10 juni 2017 nieuwe gegevens geschreven naar de bestaande beheerde schijven automatisch versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bc63d-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="bc63d-196">We ook van plan bent om bestaande gegevens te coderen en de versleuteling gebeurt asynchroon op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="bc63d-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="bc63d-197">Als u bestaande gegevens moet nu worden versleuteld, maakt u een kopie van de schijf.</span><span class="sxs-lookup"><span data-stu-id="bc63d-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="bc63d-198">Nieuwe schijf wordt versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bc63d-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="bc63d-199">Beheerde schijven kopiëren met behulp van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc63d-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="bc63d-200">Beheerde schijven met behulp van PowerShell kopiëren</span><span class="sxs-lookup"><span data-stu-id="bc63d-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="bc63d-201">**Zijn beheerde momentopnamen en installatiekopieën versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="bc63d-202">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-202">Yes.</span></span> <span data-ttu-id="bc63d-203">Alle beheerde momentopnamen en installatiekopieën die zijn gemaakt na 9 juni 2017 worden automatisch versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bc63d-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="bc63d-204">**Kan ik virtuele machines met niet-beheerde schijven die zich bevinden op opslagaccounts die zijn of die eerder zijn versleuteld met beheerde schijven converteren**</span><span class="sxs-lookup"><span data-stu-id="bc63d-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="bc63d-205">Ja</span><span class="sxs-lookup"><span data-stu-id="bc63d-205">Yes</span></span>

<span data-ttu-id="bc63d-206">**Een geëxporteerde VHD van een beheerde schijf of een momentopname ook worden versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="bc63d-207">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-207">No.</span></span> <span data-ttu-id="bc63d-208">Maar als u een VHD naar een versleutelde storage-account van een gecodeerd exporteren beheerd schijf of een momentopname en ze zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bc63d-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="bc63d-209">Premium-schijven: beheerde en onbeheerde</span><span class="sxs-lookup"><span data-stu-id="bc63d-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="bc63d-210">**Als een virtuele machine gebruikmaakt van een reeks grootte die ondersteuning biedt voor Premium-opslag, zoals een DSv2 kan ik koppelen zowel premium en standard gegevensschijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="bc63d-211">Ja.</span><span class="sxs-lookup"><span data-stu-id="bc63d-211">Yes.</span></span>

<span data-ttu-id="bc63d-212">**Kan ik zowel premium en standard gegevensschijven koppelen aan een reeks grootte die biedt geen ondersteuning voor Premium-opslag, zoals D, Dv2, G of F-serie?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="bc63d-213">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-213">No.</span></span> <span data-ttu-id="bc63d-214">U kunt alleen standaard gegevensschijven koppelen aan virtuele machines die geen gebruikmaken van een reeks grootte die ondersteuning biedt voor Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="bc63d-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="bc63d-215">**Als ik een gegevensschijf premium van een bestaande VHD die 80 GB maken is, hoeveel die kost?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="bc63d-216">Een gegevensschijf premium is gemaakt op basis van een VHD 80 GB wordt beschouwd als de grootte van de schijf beschikbaar zijn voor het volgende premium, die een schijf P10.</span><span class="sxs-lookup"><span data-stu-id="bc63d-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="bc63d-217">U kosten in rekening gebracht volgens de P10 schijf prijzen.</span><span class="sxs-lookup"><span data-stu-id="bc63d-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="bc63d-218">**Zijn er transactiekosten Premium-opslag gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="bc63d-219">Er is een vaste kosten voor de grootte van elke schijf, dat wordt meegeleverd met specifieke limieten ingerichte op IOPS en doorvoerlimieten.</span><span class="sxs-lookup"><span data-stu-id="bc63d-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="bc63d-220">De andere kosten zijn uitgaande bandbreedte en capaciteit van de momentopname, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc63d-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="bc63d-221">Zie de pagina [prijzen](https://azure.microsoft.com/pricing/details/storage) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bc63d-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="bc63d-222">**Wat zijn de limieten voor IOPS en doorvoerlimieten die ik van de schijfcache ophalen kan?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="bc63d-223">De gecombineerde limieten voor cache en lokale SSD voor een reeks DS zijn 4000 IOP's per core en 33 MB per seconde per core.</span><span class="sxs-lookup"><span data-stu-id="bc63d-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="bc63d-224">De reeks GS biedt 5000 IOP's per core en 50 MB per seconde per core.</span><span class="sxs-lookup"><span data-stu-id="bc63d-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="bc63d-225">**Wordt de lokale SSD ondersteund voor een VM-schijven beheerd?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="bc63d-226">De lokale SSD is tijdelijke opslag die is opgenomen in een VM-schijven worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="bc63d-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="bc63d-227">Er is geen extra kosten verbonden voor deze tijdelijke opslag.</span><span class="sxs-lookup"><span data-stu-id="bc63d-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="bc63d-228">U wordt aangeraden dat u deze lokale SSD niet gebruiken voor het opslaan van uw toepassingsgegevens omdat deze is niet in Azure Blob-opslag permanent.</span><span class="sxs-lookup"><span data-stu-id="bc63d-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="bc63d-229">**Zijn er gevolgen voor het gebruik van TRIM op premium-schijven?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="bc63d-230">Er is geen nadeel van het gebruik van TRIM op Azure ofwel premium-schijven of standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="bc63d-231">Nieuwe schijfgrootten: beheerde en onbeheerde</span><span class="sxs-lookup"><span data-stu-id="bc63d-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="bc63d-232">**Wat is de grootste schijfgrootte voor het besturingssysteem en gegevensschijven ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="bc63d-233">Het partitietype die Azure biedt ondersteuning voor de schijf van een besturingssysteem is de master bootrecord (MBR).</span><span class="sxs-lookup"><span data-stu-id="bc63d-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="bc63d-234">Het formaat van de MBR-indeling ondersteunt een schijf 2 TB.</span><span class="sxs-lookup"><span data-stu-id="bc63d-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="bc63d-235">De maximale grootte aan die Azure biedt ondersteuning voor de schijf van een besturingssysteem is 2 TB.</span><span class="sxs-lookup"><span data-stu-id="bc63d-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="bc63d-236">Azure ondersteunt maximaal 4 TB voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="bc63d-237">**Wat is de grootste blob paginagrootte die wordt ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="bc63d-238">Pagina is-blob de maximumgrootte die ondersteuning biedt voor Azure 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="bc63d-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="bc63d-239">Pagina-blobs die groter zijn dan 4 TB (4095 GB) gekoppeld aan een virtuele machine als gegevens of besturingssysteem schijven worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bc63d-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="bc63d-240">**Moet ik een nieuwe versie van Azure-hulpprogramma's kunt maken, te koppelen, te vergroten of verkleinen en uploaden schijven groter dan 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="bc63d-241">U hoeft niet bijwerken van uw bestaande Azure-hulpprogramma's voor het maken, koppelen of vergroten of verkleinen schijven groter dan 1 TB.</span><span class="sxs-lookup"><span data-stu-id="bc63d-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="bc63d-242">Als u wilt uw VHD-bestand van on-premises naar Azure rechtstreeks als een pagina-blob of een niet-beheerde schijf uploadt, moet u de nieuwste hulpprogramma's gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bc63d-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="bc63d-243">Azure-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="bc63d-243">Azure tools</span></span>      | <span data-ttu-id="bc63d-244">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="bc63d-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="bc63d-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc63d-245">Azure PowerShell</span></span> | <span data-ttu-id="bc63d-246">Versienummer 4.1.0: release van juni 2017 of hoger</span><span class="sxs-lookup"><span data-stu-id="bc63d-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="bc63d-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="bc63d-247">Azure CLI v1</span></span>     | <span data-ttu-id="bc63d-248">Versienummer 0.10.13: mei 2017 release of hoger</span><span class="sxs-lookup"><span data-stu-id="bc63d-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="bc63d-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="bc63d-249">AzCopy</span></span>           | <span data-ttu-id="bc63d-250">Versienummer 6.1.0: release van juni 2017 of hoger</span><span class="sxs-lookup"><span data-stu-id="bc63d-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="bc63d-251">De ondersteuning voor Azure CLI v2 en Azure Storage Explorer is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="bc63d-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="bc63d-252">**Worden P4 en P6 schijfgrootten ondersteund voor niet-beheerde schijven of pagina-blobs?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="bc63d-253">Nee.</span><span class="sxs-lookup"><span data-stu-id="bc63d-253">No.</span></span> <span data-ttu-id="bc63d-254">P4 (32 GB) en P6 schijfgrootten (64 GB) worden alleen ondersteund voor beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="bc63d-255">Ondersteuning voor niet-beheerde schijven en pagina-blobs is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="bc63d-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="bc63d-256">**Als mijn bestaande premium beheerd schijf kleiner is dan 64 GB is gemaakt voordat de kleine schijf (rond 15 juni 2017) is ingeschakeld, hoe wordt deze in rekening gebracht?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="bc63d-257">Bestaande kleine premium schijven minder dan 64 GB worden in rekening gebracht volgens de prijscategorie P10 blijven.</span><span class="sxs-lookup"><span data-stu-id="bc63d-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="bc63d-258">**Hoe kan ik de schijf-laag van kleine premium-schijven bevat die kleiner is dan 64 GB van P10 P4 of P6 overschakelen?**</span><span class="sxs-lookup"><span data-stu-id="bc63d-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="bc63d-259">U kunt een momentopname van de kleine schijven en maak vervolgens een schijf voor de prijscategorie automatisch schakelen P4 of op basis van de grootte van de ingerichte P6.</span><span class="sxs-lookup"><span data-stu-id="bc63d-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="bc63d-260">Wat gebeurt er als mijn vraag hier niet wordt beantwoord?</span><span class="sxs-lookup"><span data-stu-id="bc63d-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="bc63d-261">Als uw vraag hier niet is vermeld, laat ons weten en wij helpen u bij een antwoord vinden.</span><span class="sxs-lookup"><span data-stu-id="bc63d-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="bc63d-262">U kunt een vraag aan het einde van dit artikel plaatsen in de opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="bc63d-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="bc63d-263">Als u wilt gaan met het Azure Storage-team en andere communityleden over dit artikel, gebruiken het MSDN [Azure Storage-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="bc63d-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="bc63d-264">Voor het aanvragen van functies, de aanvragen en ideeën voor het indienen de [forum met feedback van Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="bc63d-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
