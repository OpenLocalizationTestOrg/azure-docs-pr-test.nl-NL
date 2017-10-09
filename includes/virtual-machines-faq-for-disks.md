# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="945c1-101">Veelgestelde vragen over Azure IaaS VM-schijven en beheerde en onbeheerde premium-schijven</span><span class="sxs-lookup"><span data-stu-id="945c1-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="945c1-102">Dit artikel worden enkele veelgestelde vragen over Azure beheerd schijven en Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="945c1-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="945c1-103">Beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="945c1-103">Managed Disks</span></span>

<span data-ttu-id="945c1-104">**Wat is Azure beheerd schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="945c1-105">Beheerde schijven is een functie die vereenvoudigt Schijfbeheer voor Azure IaaS VM's met opslagbeheer-account voor u verwerken.</span><span class="sxs-lookup"><span data-stu-id="945c1-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="945c1-106">Zie voor meer informatie, Hallo [schijven beheerd overzicht](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="945c1-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="945c1-107">**Als ik een standard-beheerde schijven van een bestaande VHD 80 GB maken, hoeveel die kost mij?**</span><span class="sxs-lookup"><span data-stu-id="945c1-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="945c1-108">Een standard-beheerde schijven gemaakt op basis van een VHD 80 GB wordt beschouwd als Hallo volgende beschikbare standaard schijf, grootte, die een schijf S10.</span><span class="sxs-lookup"><span data-stu-id="945c1-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="945c1-109">U bent in rekening gebracht volgens toohello S10 schijf prijzen.</span><span class="sxs-lookup"><span data-stu-id="945c1-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="945c1-110">Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="945c1-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="945c1-111">**Zijn er transactiekosten voor standard-beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="945c1-112">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-112">Yes.</span></span> <span data-ttu-id="945c1-113">U kosten in rekening gebracht voor elke transactie.</span><span class="sxs-lookup"><span data-stu-id="945c1-113">You're charged for each transaction.</span></span> <span data-ttu-id="945c1-114">Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="945c1-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="945c1-115">**Voor een standaard beheerde schijf wordt ik in rekening gebracht voor de werkelijke grootte van gegevens op schijf Hallo HALLO hallo of voor Hallo ingerichte capaciteit van Hallo schijf?**</span><span class="sxs-lookup"><span data-stu-id="945c1-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="945c1-116">U bent in rekening gebracht op basis van Hallo ingerichte capaciteit van Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="945c1-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="945c1-117">Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="945c1-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="945c1-118">**Hoe wordt de prijzen van beheerde premium-schijven verschilt van niet-beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="945c1-119">Hallo prijzen van beheerde premium-schijven is hetzelfde als niet-beheerde premium-schijven Hallo.</span><span class="sxs-lookup"><span data-stu-id="945c1-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="945c1-120">**Kan ik Hallo opslagaccounttype (Standard of Premium) van mijn beheerde schijven wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="945c1-121">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-121">Yes.</span></span> <span data-ttu-id="945c1-122">U kunt Hallo opslagaccounttype van uw beheerde schijven wijzigen met behulp van hello Azure-portal, PowerShell of hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="945c1-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="945c1-123">**Is er een manier die ik kan kopiëren of exporteren van een beheerde schijf tooa persoonlijke storage-account?**</span><span class="sxs-lookup"><span data-stu-id="945c1-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="945c1-124">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-124">Yes.</span></span> <span data-ttu-id="945c1-125">U kunt uw beheerde schijven exporteren met behulp van hello Azure-portal, PowerShell of hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="945c1-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="945c1-126">**Kan ik een VHD-bestand in een Azure storage-account toocreate een beheerde schijf met een ander abonnement gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="945c1-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="945c1-127">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-127">No.</span></span>

<span data-ttu-id="945c1-128">**Kan ik een VHD-bestand in een Azure storage-account toocreate een beheerde schijf gebruiken in een andere regio?**</span><span class="sxs-lookup"><span data-stu-id="945c1-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="945c1-129">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-129">No.</span></span>

<span data-ttu-id="945c1-130">**Zijn er beperkingen scale voor klanten die gebruikmaken van beheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="945c1-131">Beheerde schijven elimineert Hallo-limieten die zijn gekoppeld aan de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="945c1-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="945c1-132">Hallo-aantal beheerde schijven per abonnement is echter beperkt too2, 000 standaard.</span><span class="sxs-lookup"><span data-stu-id="945c1-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="945c1-133">U kunt ondersteuning tooincrease dit aantal aanroepen.</span><span class="sxs-lookup"><span data-stu-id="945c1-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="945c1-134">**Kan ik een incrementele momentopname van een beheerde schijf volgen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="945c1-135">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-135">No.</span></span> <span data-ttu-id="945c1-136">de huidige Snapshots Hallo maakt een volledige kopie van een beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="945c1-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="945c1-137">We hebben wel echter toosupport incrementele momentopnamen in toekomstige Hallo plannen.</span><span class="sxs-lookup"><span data-stu-id="945c1-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="945c1-138">**Kunnen de virtuele machines in een beschikbaarheidsset bestaan uit een combinatie van beheerde en onbeheerde schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="945c1-139">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-139">No.</span></span> <span data-ttu-id="945c1-140">Hallo virtuele machines in een beschikbaarheidsset moet gebruiken voor alle beheerde schijven of alle niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="945c1-141">Wanneer u een beschikbaarheidsset maakt, kunt u kiezen welk type schijven gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="945c1-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="945c1-142">**Is beheerd schijven Hallo standaardoptie in hello Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="945c1-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="945c1-143">Momenteel niet, maar deze worden standaard in toekomstige Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="945c1-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="945c1-144">**Kan ik een lege beheerde schijf maken?**</span><span class="sxs-lookup"><span data-stu-id="945c1-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="945c1-145">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-145">Yes.</span></span> <span data-ttu-id="945c1-146">U kunt een lege schijf maken.</span><span class="sxs-lookup"><span data-stu-id="945c1-146">You can create an empty disk.</span></span> <span data-ttu-id="945c1-147">Een beheerde schijf kan worden gemaakt onafhankelijk van een virtuele machine, bijvoorbeeld zonder tooa VM kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="945c1-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="945c1-148">**Wat is Hallo ondersteund aantal foutdomeinen voor een beschikbaarheidsset die gebruikmaakt van schijven beheerd?**</span><span class="sxs-lookup"><span data-stu-id="945c1-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="945c1-149">Hallo ondersteund aantal foutdomeinen is afhankelijk van Hallo regio waar Hallo beschikbaarheidsset die gebruikmaakt van schijven beheerd zich bevindt, 2 of 3.</span><span class="sxs-lookup"><span data-stu-id="945c1-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="945c1-150">**Hoe wordt Hallo standaard opslagaccount voor diagnostische gegevens instellen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="945c1-151">Instellen van een persoonlijke opslagaccount voor diagnostische gegevens van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="945c1-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="945c1-152">In toekomstige hello, die we zullen tooswitch diagnostics ook tooManaged schijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="945c1-153">**Wat voor soort toegangsbeheer op basis van rollen ondersteuning is beschikbaar voor schijven beheerd?**</span><span class="sxs-lookup"><span data-stu-id="945c1-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="945c1-154">Schijven ondersteunt drie belangrijkste standaardrollen beheerd:</span><span class="sxs-lookup"><span data-stu-id="945c1-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="945c1-155">Eigenaar: Kunnen alles beheren, inclusief toegang</span><span class="sxs-lookup"><span data-stu-id="945c1-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="945c1-156">Inzender: Kunnen alles beheren behalve toegang</span><span class="sxs-lookup"><span data-stu-id="945c1-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="945c1-157">Lezer: Kunnen alles weergeven, maar geen wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="945c1-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="945c1-158">**Is er een manier die ik kan kopiëren of exporteren van een beheerde schijf tooa persoonlijke storage-account?**</span><span class="sxs-lookup"><span data-stu-id="945c1-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="945c1-159">U kunt een alleen-lezen shared access signature URI voor Hallo beheerd schijf en deze gebruiken toocopy Hallo inhoud tooa persoonlijke opslag account of on-premises opslag ophalen.</span><span class="sxs-lookup"><span data-stu-id="945c1-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="945c1-160">**Kan ik een kopie van de beheerde computer maken?**</span><span class="sxs-lookup"><span data-stu-id="945c1-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="945c1-161">Klanten kunnen een momentopname van het bijbehorende beheerde schijven en gebruik vervolgens Hallo momentopname toocreate een andere beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="945c1-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="945c1-162">**Worden niet-beheerde schijven nog steeds ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="945c1-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="945c1-163">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-163">Yes.</span></span> <span data-ttu-id="945c1-164">Wij ondersteunen onbeheerde en beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="945c1-165">U wordt aangeraden dat u beheerde schijven voor nieuwe werkbelastingen en uw huidige werkbelastingen toomanaged schijven migreren.</span><span class="sxs-lookup"><span data-stu-id="945c1-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="945c1-166">**Als ik een schijf van 128 GB maken en vervolgens te Hallo grootte too130 GB verhogen, ik gefactureerd voor volgende schijfgrootte hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="945c1-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="945c1-167">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-167">Yes.</span></span>

<span data-ttu-id="945c1-168">**Kan ik geografisch redundante opslag met lokaal redundante opslag maken en zone-redundante opslag schijven die worden beheerd?**</span><span class="sxs-lookup"><span data-stu-id="945c1-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="945c1-169">Azure-beheerde schijven ondersteunt momenteel alleen lokaal redundante opslag beheerd schijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="945c1-170">**Kan ik verkleinen of mijn beheerde schijven afslanken?**</span><span class="sxs-lookup"><span data-stu-id="945c1-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="945c1-171">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-171">No.</span></span> <span data-ttu-id="945c1-172">Deze functie is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="945c1-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="945c1-173">**Kan ik Hallo computer name-eigenschap wijzigen wanneer een gespecialiseerde (niet gemaakt met behulp van hulpprogramma voor systeemvoorbereiding Hallo of gegeneraliseerd) systeemschijf besturingssystemen gebruikte tooprovision een virtuele machine zijn?**</span><span class="sxs-lookup"><span data-stu-id="945c1-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="945c1-174">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-174">No.</span></span> <span data-ttu-id="945c1-175">U kunt Hallo computer name-eigenschap niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="945c1-175">You can't update hello computer name property.</span></span> <span data-ttu-id="945c1-176">Hallo neemt nieuwe virtuele machine deze van Hallo bovenliggende virtuele machine gebruikte toocreate hello besturingssysteemschijf is.</span><span class="sxs-lookup"><span data-stu-id="945c1-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="945c1-177">**Waar vind ik voorbeelden Azure Resource Manager-sjablonen toocreate virtuele machines met beheerde-schijven**</span><span class="sxs-lookup"><span data-stu-id="945c1-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="945c1-178">Lijst met sjablonen met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="945c1-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="945c1-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="945c1-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="945c1-180">Beheerd schijven en versleuteling van opslag-Service</span><span class="sxs-lookup"><span data-stu-id="945c1-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="945c1-181">**Is Azure Storage-Service: versleuteling standaard ingeschakeld wanneer ik een beheerde schijf maken?**</span><span class="sxs-lookup"><span data-stu-id="945c1-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="945c1-182">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-182">Yes.</span></span>

<span data-ttu-id="945c1-183">**Wie beheert Hallo versleutelingssleutels?**</span><span class="sxs-lookup"><span data-stu-id="945c1-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="945c1-184">Microsoft beheert Hallo versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="945c1-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="945c1-185">**Kan ik voor mijn beheerde schijven versleuteling van opslag Service uitschakelen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="945c1-186">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-186">No.</span></span>

<span data-ttu-id="945c1-187">**Is versleuteling van opslag Service alleen beschikbaar in specifieke gebieden?**</span><span class="sxs-lookup"><span data-stu-id="945c1-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="945c1-188">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-188">No.</span></span> <span data-ttu-id="945c1-189">Het is beschikbaar in alle Hallo regio's waar beheerd schijven beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="945c1-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="945c1-190">Beheerde schijven is beschikbaar in alle openbare regio's en Duitsland.</span><span class="sxs-lookup"><span data-stu-id="945c1-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="945c1-191">**Hoe vind ik als mijn beheerde schijf worden versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="945c1-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="945c1-192">U vindt hier Hallo tijd waarop een beheerde schijf is gemaakt in hello Azure-portal, Azure CLI Hallo en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="945c1-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="945c1-193">De schijf wordt versleuteld als Hallo tijd na 9 juni 2017.</span><span class="sxs-lookup"><span data-stu-id="945c1-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="945c1-194">**Hoe kan ik mijn bestaande schijven die zijn gemaakt vóór 10 juni 2017 coderen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="945c1-195">Vanaf 10 juni 2017 nieuwe gegevens geschreven tooexisting beheerd schijven automatisch versleuteld.</span><span class="sxs-lookup"><span data-stu-id="945c1-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="945c1-196">We zijn ook tooencrypt bestaande gegevens plannen en Hallo versleuteling asynchroon op Hallo achtergrond gebeurt.</span><span class="sxs-lookup"><span data-stu-id="945c1-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="945c1-197">Als u bestaande gegevens moet nu worden versleuteld, maakt u een kopie van de schijf.</span><span class="sxs-lookup"><span data-stu-id="945c1-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="945c1-198">Nieuwe schijf wordt versleuteld.</span><span class="sxs-lookup"><span data-stu-id="945c1-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="945c1-199">Beheerde schijven kopiëren via hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="945c1-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="945c1-200">Beheerde schijven met behulp van PowerShell kopiëren</span><span class="sxs-lookup"><span data-stu-id="945c1-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="945c1-201">**Zijn beheerde momentopnamen en installatiekopieën versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="945c1-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="945c1-202">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-202">Yes.</span></span> <span data-ttu-id="945c1-203">Alle beheerde momentopnamen en installatiekopieën die zijn gemaakt na 9 juni 2017 worden automatisch versleuteld.</span><span class="sxs-lookup"><span data-stu-id="945c1-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="945c1-204">**Kan ik virtuele machines met niet-beheerde schijven die zich bevinden op opslagaccounts die zijn of zijn eerder versleutelde toomanaged schijven converteren**</span><span class="sxs-lookup"><span data-stu-id="945c1-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="945c1-205">Ja</span><span class="sxs-lookup"><span data-stu-id="945c1-205">Yes</span></span>

<span data-ttu-id="945c1-206">**Een geëxporteerde VHD van een beheerde schijf of een momentopname ook worden versleuteld?**</span><span class="sxs-lookup"><span data-stu-id="945c1-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="945c1-207">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-207">No.</span></span> <span data-ttu-id="945c1-208">Maar als u een VHD-tooan exporteren gecodeerd storage-account van een versleutelde-beheerde schijven of een momentopname en ze zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="945c1-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="945c1-209">Premium-schijven: beheerde en onbeheerde</span><span class="sxs-lookup"><span data-stu-id="945c1-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="945c1-210">**Als een virtuele machine gebruikmaakt van een reeks grootte die ondersteuning biedt voor Premium-opslag, zoals een DSv2 kan ik koppelen zowel premium en standard gegevensschijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="945c1-211">Ja.</span><span class="sxs-lookup"><span data-stu-id="945c1-211">Yes.</span></span>

<span data-ttu-id="945c1-212">**Kan ik zowel premium en standard schijven tooa grootte gegevensreeks die biedt geen ondersteuning voor Premium-opslag, zoals D, Dv2, G of F-serie koppelen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="945c1-213">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-213">No.</span></span> <span data-ttu-id="945c1-214">U kunt alleen standaard gegevens schijven tooVMs die geen gebruikmaken van een reeks grootte die ondersteuning biedt voor Premium-opslag kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="945c1-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="945c1-215">**Als ik een gegevensschijf premium van een bestaande VHD die 80 GB maken is, hoeveel die kost?**</span><span class="sxs-lookup"><span data-stu-id="945c1-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="945c1-216">Een gegevensschijf premium is gemaakt op basis van een VHD 80 GB wordt beschouwd als Hallo beschikbaar zijn voor het volgende premium-schijfgrootte, die een schijf P10.</span><span class="sxs-lookup"><span data-stu-id="945c1-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="945c1-217">U bent in rekening gebracht volgens toohello P10 schijf prijzen.</span><span class="sxs-lookup"><span data-stu-id="945c1-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="945c1-218">**Zijn er transactie kosten toouse Premium-opslag?**</span><span class="sxs-lookup"><span data-stu-id="945c1-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="945c1-219">Er is een vaste kosten voor de grootte van elke schijf, dat wordt meegeleverd met specifieke limieten ingerichte op IOPS en doorvoerlimieten.</span><span class="sxs-lookup"><span data-stu-id="945c1-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="945c1-220">Hallo andere kosten zijn uitgaande bandbreedte en capaciteit van de momentopname, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="945c1-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="945c1-221">Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="945c1-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="945c1-222">**Wat zijn de limieten voor IOPS en doorvoerlimieten die ik van de schijfcache Hallo ophalen kan Hallo?**</span><span class="sxs-lookup"><span data-stu-id="945c1-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="945c1-223">Hallo gecombineerde limieten voor cache en lokale SSD voor een reeks DS 4000 IOP's per core en 33 MB per seconde per core.</span><span class="sxs-lookup"><span data-stu-id="945c1-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="945c1-224">Hallo GS-serie biedt 5000 IOP's per core en 50 MB per seconde per core.</span><span class="sxs-lookup"><span data-stu-id="945c1-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="945c1-225">**Is Hallo die lokale SSD ondersteund voor een VM-schijven beheerd?**</span><span class="sxs-lookup"><span data-stu-id="945c1-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="945c1-226">Hallo is lokale SSD tijdelijke opslag die is opgenomen in een VM-schijven worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="945c1-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="945c1-227">Er is geen extra kosten verbonden voor deze tijdelijke opslag.</span><span class="sxs-lookup"><span data-stu-id="945c1-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="945c1-228">Het is raadzaam dat u niet deze lokale SSD toostore uw toepassingsgegevens gebruiken omdat deze is niet in Azure Blob-opslag permanent.</span><span class="sxs-lookup"><span data-stu-id="945c1-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="945c1-229">**Zijn er gevolgen voor hello gebruiken van TRIM op premium-schijven?**</span><span class="sxs-lookup"><span data-stu-id="945c1-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="945c1-230">Er is geen gebruik van de toohello nadeel van TRIM op Azure ofwel premium-schijven of standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="945c1-231">Nieuwe schijfgrootten: beheerde en onbeheerde</span><span class="sxs-lookup"><span data-stu-id="945c1-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="945c1-232">**Wat is Hallo grootste schijfgrootte voor het besturingssysteem en gegevensschijven ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="945c1-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="945c1-233">Hallo partitietype die ondersteuning biedt voor de schijf van een besturingssysteem voor Azure is Hallo hoofdopstartrecord (MBR).</span><span class="sxs-lookup"><span data-stu-id="945c1-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="945c1-234">Hallo MBR-indeling ondersteunt een schijfgrootte van too2 TB.</span><span class="sxs-lookup"><span data-stu-id="945c1-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="945c1-235">Hallo maximale grootte aan die Azure biedt ondersteuning voor de schijf van een besturingssysteem is 2 TB.</span><span class="sxs-lookup"><span data-stu-id="945c1-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="945c1-236">Azure biedt ondersteuning voor maximaal too4 TB voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="945c1-237">**Wat is Hallo grootste blob paginaformaat dat wordt ondersteund?**</span><span class="sxs-lookup"><span data-stu-id="945c1-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="945c1-238">Hallo is pagina-blob biedt ondersteuning voor Azure maximumgrootte 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="945c1-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="945c1-239">Pagina-blobs die groter zijn dan 4 TB (4095 GB) die zijn gekoppeld tooa VM als gegevens of besturingssysteem schijven worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="945c1-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="945c1-240">**Moet ik toouse een nieuwe versie van Azure-hulpprogramma's toocreate, toevoegen, vergroten of verkleinen en uploaden schijven groter dan 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="945c1-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="945c1-241">U hoeft niet tooupgrade de toocreate van uw bestaande Azure-hulpprogramma's of schijven die groter zijn dan 1 TB vergroten of verkleinen koppelen.</span><span class="sxs-lookup"><span data-stu-id="945c1-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="945c1-242">tooupload uw VHD-bestand van lokale rechtstreeks tooAzure als een pagina-blob of een niet-beheerde schijf, moet u toouse Hallo nieuwste hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="945c1-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="945c1-243">Azure-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="945c1-243">Azure tools</span></span>      | <span data-ttu-id="945c1-244">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="945c1-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="945c1-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="945c1-245">Azure PowerShell</span></span> | <span data-ttu-id="945c1-246">Versienummer 4.1.0: release van juni 2017 of hoger</span><span class="sxs-lookup"><span data-stu-id="945c1-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="945c1-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="945c1-247">Azure CLI v1</span></span>     | <span data-ttu-id="945c1-248">Versienummer 0.10.13: mei 2017 release of hoger</span><span class="sxs-lookup"><span data-stu-id="945c1-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="945c1-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="945c1-249">AzCopy</span></span>           | <span data-ttu-id="945c1-250">Versienummer 6.1.0: release van juni 2017 of hoger</span><span class="sxs-lookup"><span data-stu-id="945c1-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="945c1-251">Hallo-ondersteuning voor Azure CLI v2 en Azure Storage Explorer is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="945c1-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="945c1-252">**Worden P4 en P6 schijfgrootten ondersteund voor niet-beheerde schijven of pagina-blobs?**</span><span class="sxs-lookup"><span data-stu-id="945c1-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="945c1-253">Nee.</span><span class="sxs-lookup"><span data-stu-id="945c1-253">No.</span></span> <span data-ttu-id="945c1-254">P4 (32 GB) en P6 schijfgrootten (64 GB) worden alleen ondersteund voor beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="945c1-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="945c1-255">Ondersteuning voor niet-beheerde schijven en pagina-blobs is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="945c1-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="945c1-256">**Als mijn bestaande premium beheerd schijf kleiner is dan 64 GB is gemaakt voordat Hallo kleine schijf (rond 15 juni 2017) is ingeschakeld, hoe wordt deze in rekening gebracht?**</span><span class="sxs-lookup"><span data-stu-id="945c1-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="945c1-257">Bestaande kleine premium-schijven bevat die kleiner is dan 64 GB blijven toobe kosten in rekening gebracht volgens toohello P10 prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="945c1-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="945c1-258">**Hoe kan ik Hallo schijf laag van kleine premium-schijven bevat die kleiner is dan 64 GB van P10 tooP4 of P6 overschakelen?**</span><span class="sxs-lookup"><span data-stu-id="945c1-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="945c1-259">U kunt een momentopname van de kleine schijven en vervolgens maakt u een schijf tooautomatically switch Hallo prijzen laag tooP4 of P6 op basis van Hallo ingericht grootte.</span><span class="sxs-lookup"><span data-stu-id="945c1-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="945c1-260">Wat gebeurt er als mijn vraag hier niet wordt beantwoord?</span><span class="sxs-lookup"><span data-stu-id="945c1-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="945c1-261">Als uw vraag hier niet is vermeld, laat ons weten en wij helpen u bij een antwoord vinden.</span><span class="sxs-lookup"><span data-stu-id="945c1-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="945c1-262">U kunt een vraag op Hallo einde van dit artikel boeken in Hallo opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="945c1-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="945c1-263">tooengage met hello Azure Storage-team en andere communityleden over dit artikel gebruiken Hallo MSDN [Azure Storage-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="945c1-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="945c1-264">toorequest functies, dienen de aanvragen en ideeën toohello [forum met feedback van Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="945c1-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
