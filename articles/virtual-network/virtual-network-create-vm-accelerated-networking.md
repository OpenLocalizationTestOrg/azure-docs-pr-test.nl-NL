---
title: een virtuele machine van Azure met versnelde toegang aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtuele machine met versnelde netwerken.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="c6622-103">Een virtuele machine met versnelde toegang maken</span><span class="sxs-lookup"><span data-stu-id="c6622-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="c6622-104">In deze zelfstudie leert u hoe een Azure-virtuele Machine (VM) met versnelde toegang toocreate.</span><span class="sxs-lookup"><span data-stu-id="c6622-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="c6622-105">Versnelde netwerken wordt GA voor Windows en een openbare Preview voor specifieke Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="c6622-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="c6622-106">Versnelde netwerken kan één hoofdelement i/o-virtualisatie (SR-IOV) tooa VM, aanzienlijk verbeteren de prestaties van netwerken.</span><span class="sxs-lookup"><span data-stu-id="c6622-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="c6622-107">Dit pad krachtige omzeilt Hallo host Hallo gegevenspad waardoor latentie en jitter CPU-gebruik, voor gebruik met Hallo zwaarste netwerkbelasting op ondersteunde VM-typen.</span><span class="sxs-lookup"><span data-stu-id="c6622-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="c6622-108">Hallo volgende afbeelding toont communicatie tussen twee virtuele machines (VM) met en zonder versnelde netwerken:</span><span class="sxs-lookup"><span data-stu-id="c6622-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Vergelijking](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="c6622-110">Alle netwerkverkeer naar en vanuit Hallo VM moet zonder versnelde netwerken passeren Hallo host en Hallo virtuele switch.</span><span class="sxs-lookup"><span data-stu-id="c6622-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="c6622-111">Hallo-switch biedt alle afdwingen van beleid, zoals zoals beveiligingsgroepen, het netwerk toegang tot toegangsbeheerlijsten-, isolatie- en andere gevirtualiseerd services toonetwork netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="c6622-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="c6622-112">meer informatie over virtuele switches, Hallo lezen toolearn [Hyper-V-netwerkvirtualisatie en virtuele switch](https://technet.microsoft.com/library/jj945275.aspx) artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="c6622-113">Met versnelde netwerken netwerkverkeer binnenkomt op Hallo van de virtuele machine netwerkinterface (NIC) en wordt vervolgens doorgestuurd toohello VM.</span><span class="sxs-lookup"><span data-stu-id="c6622-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="c6622-114">Alle netwerkbeleid dat Hallo virtuele switch wordt toegepast zonder versnelde netwerken worden ge-offload en toegepast in hardware.</span><span class="sxs-lookup"><span data-stu-id="c6622-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="c6622-115">Toepassen van beleid in hardware schakelt Hallo NIC tooforward netwerkverkeer rechtstreeks toohello VM, het omzeilen van Hallo-host en Hallo virtuele switch, terwijl alle Hallo beleid wordt toegepast in Hallo host.</span><span class="sxs-lookup"><span data-stu-id="c6622-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="c6622-116">Hallo voordelen van versnelde netwerken alleen van toepassing toohello VM die is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c6622-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="c6622-117">Voor de beste resultaten hello, is het ideaal tooenable deze functie op ten minste twee virtuele machines verbonden toohello dezelfde Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="c6622-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="c6622-118">Tijdens de communicatie tussen VNets of verbindende on-premises, heeft dit onderdeel minimale gevolgen toooverall latentie.</span><span class="sxs-lookup"><span data-stu-id="c6622-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="c6622-119">Deze Linux Public Preview mogelijk geen Hallo zijn van hetzelfde niveau van beschikbaarheid en betrouwbaarheid als functies beschreven die in het algemeen beschikbaarheid vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="c6622-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="c6622-120">Hallo-functie wordt niet ondersteund, kan hebben beperkte mogelijkheden en mogelijk niet beschikbaar in alle Azure-locaties.</span><span class="sxs-lookup"><span data-stu-id="c6622-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="c6622-121">Meest recente meldingen Hallo niet op de beschikbaarheid en de status van deze functie, Controleer pagina hello Azure Virtual Network-updates.</span><span class="sxs-lookup"><span data-stu-id="c6622-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="c6622-122">Voordelen</span><span class="sxs-lookup"><span data-stu-id="c6622-122">Benefits</span></span>
* <span data-ttu-id="c6622-123">**Lagere latentie / hoger pakketten per seconde (pps):** verwijderen Hallo virtuele switch van Hallo gegevenspad verwijdert Hallo tijd te besteden aan de pakketten in Hallo host voor de verwerking van beleid en toeneemt Hallo aantal pakketten dat kan worden verwerkt binnen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c6622-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="c6622-124">**Minder jitter:** virtuele switch verwerking is afhankelijk van de vraag Hallo hoeveelheid beleid die behoeften toobe toegepast en Hallo werkbelasting Hallo CPU die Hallo verwerking doet.</span><span class="sxs-lookup"><span data-stu-id="c6622-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="c6622-125">Offloading van Hallo beleid afdwingen toohello hardware verwijdert die variabiliteit door het leveren van pakketten direct toohello VM, Hallo host tooVM communicatie en alle software-interrupts en context verwijderd verandert.</span><span class="sxs-lookup"><span data-stu-id="c6622-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="c6622-126">**CPU-gebruik verlaagd:** Bypassing Hallo virtuele switch op de host Hallo leidt tooless CPU-gebruik voor het verwerken van netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="c6622-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="c6622-127"><a name="Limitations"></a>Beperkingen</span><span class="sxs-lookup"><span data-stu-id="c6622-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="c6622-128">Hallo volgen beperkingen bestaan wanneer deze wordt met deze mogelijkheid:</span><span class="sxs-lookup"><span data-stu-id="c6622-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="c6622-129">**Interface maken van een netwerk:** Accelerated netwerken kan alleen worden ingeschakeld voor een nieuwe NIC.</span><span class="sxs-lookup"><span data-stu-id="c6622-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="c6622-130">Deze kan niet worden ingeschakeld voor een bestaande NIC.</span><span class="sxs-lookup"><span data-stu-id="c6622-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="c6622-131">**Maken van VM:** een NIC met versnelde netwerken ingeschakeld kan slechts worden aangesloten tooa VM wanneer hello virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6622-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="c6622-132">Hallo NIC mag geen gekoppelde tooan bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6622-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="c6622-133">**Gebieden:** Windows virtuele machines met versnelde netwerken worden aangeboden in de meeste Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="c6622-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="c6622-134">Virtuele Linux-machines met versnelde netwerken worden aangeboden in meerdere regio's.</span><span class="sxs-lookup"><span data-stu-id="c6622-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="c6622-135">Deze mogelijkheid is beschikbaar in Hallo-regio's is uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="c6622-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="c6622-136">Zie de blog onder Azure virtuele netwerken Updates voor de meest recente informatie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6622-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="c6622-137">**Ondersteunde besturingssystemen:** Windows: Microsoft Windows Server 2012 R2 Datacenter- en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c6622-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="c6622-138">Linux: Ubuntu Server 16.04 TNS met kernel 4.4.0-77 of hoger, SLES 12 SP2, RHEL 7.3 en CentOS 7.3 (gepubliceerd door 'Rogue Wave Software').</span><span class="sxs-lookup"><span data-stu-id="c6622-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="c6622-139">**VM-grootte:** algemeen en de grootte van de compute-geoptimaliseerde exemplaar met acht of meer cores.</span><span class="sxs-lookup"><span data-stu-id="c6622-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="c6622-140">Zie voor meer informatie, Hallo [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) en [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen.</span><span class="sxs-lookup"><span data-stu-id="c6622-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="c6622-141">Hallo wordt set ondersteunde grootten voor VM-exemplaar uitgebreid in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6622-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="c6622-142">**Implementatie via Azure Resource Manager (ARM) alleen:** versnelde toegang is niet beschikbaar voor implementatie via ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="c6622-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="c6622-143">Wijzigingen toothese beperkingen zijn aangekondigd door Hallo [virtuele netwerken van Azure updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) pagina.</span><span class="sxs-lookup"><span data-stu-id="c6622-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="c6622-144">Een Windows-VM maken</span><span class="sxs-lookup"><span data-stu-id="c6622-144">Create a Windows VM</span></span>
<span data-ttu-id="c6622-145">U kunt hello Azure-portal of Azure [PowerShell](#windows-powershell) toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c6622-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="c6622-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="c6622-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="c6622-147">Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="c6622-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="c6622-148">Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="c6622-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="c6622-149">Klik in de portal Hallo op **+ nieuw** > **Compute** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="c6622-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="c6622-150">In Hallo **Windows Server 2016 Datacenter** blade die wordt weergegeven, laat de eigenschap *Resource Manager* geselecteerde onder **een implementatiemodel selecteren**, en klik op **maken** .</span><span class="sxs-lookup"><span data-stu-id="c6622-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="c6622-151">In Hallo **basisbeginselen** blade die wordt weergegeven, Voer Hallo waarden te volgen, laat Hallo resterende standaardopties of selecteren of uw eigen waarden en klikt u op Hallo **OK** knop:</span><span class="sxs-lookup"><span data-stu-id="c6622-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="c6622-152">Instelling</span><span class="sxs-lookup"><span data-stu-id="c6622-152">Setting</span></span>|<span data-ttu-id="c6622-153">Waarde</span><span class="sxs-lookup"><span data-stu-id="c6622-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="c6622-154">Naam</span><span class="sxs-lookup"><span data-stu-id="c6622-154">Name</span></span>|<span data-ttu-id="c6622-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="c6622-155">MyVm</span></span>|
    |<span data-ttu-id="c6622-156">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="c6622-156">Resource group</span></span>|<span data-ttu-id="c6622-157">Laat **nieuw** geselecteerd en voer *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="c6622-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="c6622-158">Locatie</span><span class="sxs-lookup"><span data-stu-id="c6622-158">Location</span></span>|<span data-ttu-id="c6622-159">VS - west 2</span><span class="sxs-lookup"><span data-stu-id="c6622-159">West US 2</span></span>|

    <span data-ttu-id="c6622-160">Als u nieuwe tooAzure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (tooas regio's zijn ook genoemd).</span><span class="sxs-lookup"><span data-stu-id="c6622-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="c6622-161">In Hallo **een grootte kiezen** blade die wordt weergegeven, invoeren *8* in Hallo **Minimum kernen** vak en klik vervolgens op **weergeven van alle**.</span><span class="sxs-lookup"><span data-stu-id="c6622-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="c6622-162">Klik op **DS4_V2 standaard**, of een ondersteunde VM, klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="c6622-163">In Hallo **instellingen** blade die wordt weergegeven, laat u alle instellingen als-is, met uitzondering van Klik **ingeschakeld** onder **versnelde netwerken**, klikt u vervolgens op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="c6622-164">**Opmerking:** als, in de vorige stappen hebt u waarden voor VM-grootte, besturingssysteem of locatie die niet zijn opgenomen in Hallo geselecteerd [beperkingen](#Limitations) sectie van dit artikel **Accelerated netwerken**niet zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="c6622-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="c6622-165">In Hallo **samenvatting** blade die wordt weergegeven, klikt u op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="c6622-166">Azure begint Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="c6622-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="c6622-167">Maken van VM duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="c6622-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="c6622-168">tooinstall Hallo-netwerkstuurprogramma versnelde voor Windows, volledige Hallo stappen voor het Hallo [Windows configureren](#configure-windows) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="c6622-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6622-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="c6622-170">Installeer de nieuwste versie Hallo van hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="c6622-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="c6622-171">Als u nieuwe tooAzure PowerShell, lezen Hallo [overzicht van Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="c6622-172">Een PowerShell-sessie starten door te klikken op de knop Start van Windows hello typen **powershell**, vervolgens te klikken op **PowerShell** van Hallo zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="c6622-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="c6622-173">Voer in het PowerShell-venster Hallo `login-azurermaccount` opdracht toosign aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="c6622-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="c6622-174">Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="c6622-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="c6622-175">In uw browser kopiëren Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="c6622-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="c6622-176">Met de rechtermuisknop op toopaste Hallo script en beginnen met de uitvoering van deze in uw PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="c6622-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="c6622-177">U wordt gevraagd om een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="c6622-177">You are prompted for a username and password.</span></span> <span data-ttu-id="c6622-178">Deze referenties toolog in toohello VM gebruiken bij het verbinden van tooit in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6622-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="c6622-179">Als Hallo script mislukt en u de waarden in de script Hallo gewijzigd voordat deze wordt uitgevoerd, bevestig Hallo-waarden die u voor VM-grootte, besturingssysteem gebruikt, en locatie staan in Hallo [beperkingen](#Limitations) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="c6622-180">tooinstall Hallo-netwerkstuurprogramma versnelde voor Windows, volledige Hallo stappen voor het Hallo [Windows configureren](#configure-windows) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="c6622-181"><a name="configure-windows"></a>Windows configureren</span><span class="sxs-lookup"><span data-stu-id="c6622-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="c6622-182">Zodra u Hallo VM in Azure maakt, moet u Hallo versnelde-netwerkstuurprogramma installeren voor Windows.</span><span class="sxs-lookup"><span data-stu-id="c6622-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="c6622-183">Voordat u Hallo stappen te volgen, moet u een virtuele Windows-machine gemaakt met versnelde netwerken met behulp van beide Hallo [portal](#windows-portal) of [PowerShell](#windows-powershell) stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="c6622-184">Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="c6622-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="c6622-185">Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="c6622-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="c6622-186">In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="c6622-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="c6622-187">Wanneer **MyVm** wordt weergegeven in zoekresultaten hello, klik erop.</span><span class="sxs-lookup"><span data-stu-id="c6622-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="c6622-188">In Hallo **MyVm** blade die wordt weergegeven, klikt u op Hallo **Connect** knop in Hallo linksboven Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="c6622-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="c6622-189">**Opmerking:** als **maken** zichtbaar onder Hallo **Connect** knop Azure is nog niet voltooid Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="c6622-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="c6622-190">Klik op **Connect** pas nadat u niet meer zien **maken** onder Hallo **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="c6622-191">Uw browser toodownload Hallo toestaan **MyVm.rdp** bestand.</span><span class="sxs-lookup"><span data-stu-id="c6622-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="c6622-192">Nadat u hebt gedownload, klikt u op Hallo bestand tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="c6622-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="c6622-193">Klik op Hallo **Connect** knop in Hallo **verbinding met extern bureaublad** vak dat wordt weergegeven, meegedeeld dat Hallo uitgever van Hallo externe verbinding kan niet worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="c6622-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="c6622-194">In Hallo **Windows-beveiliging** dat verschijnt, klikt u op **meer opties**, klikt u vervolgens op **gebruik een ander account**.</span><span class="sxs-lookup"><span data-stu-id="c6622-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="c6622-195">Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven in stap 4 invoeren, en klik vervolgens op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="c6622-196">Klik op Hallo **Ja** knop in Hallo verbinding met extern bureaublad-vak dat wordt weergegeven om u te informeren dat de identiteit van de externe computer Hallo Hallo kan niet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="c6622-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="c6622-197">Met de rechtermuisknop op de knop Start van Windows hello en klik op **Apparaatbeheer**.</span><span class="sxs-lookup"><span data-stu-id="c6622-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="c6622-198">Vouw Hallo **netwerkadapters** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c6622-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="c6622-199">Bevestig dat Hallo **Mellanox ConnectX 3 virtuele functie Ethernet-Adapter** wordt weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="c6622-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Apparaatbeheer](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="c6622-201">Versnelde netwerken is nu ingeschakeld voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6622-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="c6622-202">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="c6622-202">Create a Linux VM</span></span>
<span data-ttu-id="c6622-203">U kunt hello Azure-portal of Azure [PowerShell](#linux-powershell) toocreate een Ubuntu of SLES VM.</span><span class="sxs-lookup"><span data-stu-id="c6622-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="c6622-204">Er is een andere werkstroom voor RHEL en CentOS virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c6622-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="c6622-205">Zie de onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="c6622-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="c6622-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="c6622-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="c6622-207">Registreren voor Hallo versnelde netwerken voor Linux-preview via stappen 1-5 Hallo [maken van een Linux-VM - PowerShell](#linux-powershell) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="c6622-208">U registreren niet voor preview Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="c6622-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="c6622-209">Volledige stappen 1-8 in Hallo [maken van een Windows-VM - portal](#windows-portal) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="c6622-210">Klik in stap 2 op **Ubuntu Server 16.04 LTS** in plaats van **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="c6622-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="c6622-211">Voor deze zelfstudie kiest toouse een wachtwoord, in plaats van een SSH-sleutel al is voor productie-implementaties, gebruikt u een.</span><span class="sxs-lookup"><span data-stu-id="c6622-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="c6622-212">Als **versnelde netwerken** wordt niet weergegeven wanneer u bij het voltooien van stap 7 van Hallo [maken van een Windows-VM - portal](#windows-portal) sectie van dit artikel, is het waarschijnlijk voor een van de volgende redenen Hallo:</span><span class="sxs-lookup"><span data-stu-id="c6622-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="c6622-213">U nog niet zijn geregistreerd voor Hallo preview.</span><span class="sxs-lookup"><span data-stu-id="c6622-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="c6622-214">Controleer of de status van uw registratie **geregistreerde**, zoals wordt beschreven in stap 4 van Hallo [maken van een Linux-VM - Powershell](#linux-powershell) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="c6622-215">**Opmerking:** als u hebt deelgenomen aan Hallo Accelerated netwerken voor VM's van Windows-preview (het niet langer nodig tooregister toouse versnelde netwerken voor Windows-VM's), u worden niet automatisch geregistreerd voor Hallo Accelerated voor netwerken Voorbeeld van de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="c6622-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="c6622-216">U moet registreren voor Hallo Accelerated netwerken voor virtuele Linux-machines tooparticipate in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c6622-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="c6622-217">U hebt geen geselecteerd voor een VM-grootte, besturingssysteem of locatie die worden vermeld in Hallo [beperkingen](#limitations) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="c6622-218">tooinstall Hallo-netwerkstuurprogramma versnelde voor Linux, volledige Hallo stappen voor het Hallo [Linux configureren](#configure-linux) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="c6622-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6622-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="c6622-220">Als u virtuele Linux-machines met versnelde netwerken in een abonnement maken en vervolgens een virtuele machine van Windows met versnelde netwerken in Hallo toocreate probeert hetzelfde abonnement, het maken van de virtuele machine van Windows hello mislukken.</span><span class="sxs-lookup"><span data-stu-id="c6622-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="c6622-221">Tijdens deze preview kunt u het beste Linux- en Windows-VM's te met versnelde netwerken in afzonderlijke abonnementen testen.</span><span class="sxs-lookup"><span data-stu-id="c6622-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="c6622-222">Installeer de nieuwste versie Hallo van hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="c6622-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="c6622-223">Als u nieuwe tooAzure PowerShell, lezen Hallo [overzicht van Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="c6622-224">Een PowerShell-sessie starten door te klikken op de knop Start van Windows hello typen **powershell**, vervolgens te klikken op **PowerShell** van Hallo zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="c6622-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="c6622-225">Voer in het PowerShell-venster Hallo `login-azurermaccount` opdracht toosign aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="c6622-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="c6622-226">Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="c6622-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="c6622-227">Registreren voor Hallo versnelde netwerken voor Azure preview door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c6622-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="c6622-228">E-mailbericht te verzenden[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) met uw Azure-abonnement-ID en het beoogde gebruik.</span><span class="sxs-lookup"><span data-stu-id="c6622-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="c6622-229">Wacht totdat een e-mailbevestiging van Microsoft over uw abonnement wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c6622-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="c6622-230">Voer Hallo opdracht tooconfirm die u zijn geregistreerd voor het Hallo-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="c6622-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="c6622-231">Ga niet verder met stap 5 tot en met **geregistreerde** wordt weergegeven in Hallo uitvoeren nadat u de vorige opdracht Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="c6622-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="c6622-232">De uitvoer moet eruitzien als Hallo volgende voordat u doorgaat met de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c6622-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="c6622-233">Als u hebt deelgenomen aan Hallo Accelerated netwerken voor VM's van Windows-preview (het niet langer nodig tooregister toouse versnelde netwerken voor Windows-VM's), u worden niet automatisch geregistreerd voor Hallo Accelerated netwerken voor virtuele Linux-machines preview.</span><span class="sxs-lookup"><span data-stu-id="c6622-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="c6622-234">U moet registreren voor Hallo Accelerated netwerken voor virtuele Linux-machines tooparticipate in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c6622-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="c6622-235">Kopieer Hallo script vervangen door Ubuntu of SLES naar wens te volgen in uw browser.</span><span class="sxs-lookup"><span data-stu-id="c6622-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="c6622-236">Redhat en CentOS hebben weer een andere workflow onderstaande:</span><span class="sxs-lookup"><span data-stu-id="c6622-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="c6622-237">Met de rechtermuisknop op toopaste Hallo script en beginnen met de uitvoering van deze in uw PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="c6622-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="c6622-238">U wordt gevraagd om een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="c6622-238">You are prompted for a username and password.</span></span> <span data-ttu-id="c6622-239">Deze referenties toolog in toohello VM gebruiken bij het verbinden van tooit in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6622-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="c6622-240">Als het Hallo-script is mislukt, controleert u dat:</span><span class="sxs-lookup"><span data-stu-id="c6622-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="c6622-241">U bent geregistreerd voor Hallo preview, zoals beschreven in stap 4</span><span class="sxs-lookup"><span data-stu-id="c6622-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="c6622-242">Als u VM-grootte, besturingssysteemtype of locatie-waarden in Hallo script gewijzigd voordat deze wordt uitgevoerd, dat Hallo waarden staan in Hallo [beperkingen](#Limitations) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="c6622-243">tooinstall Hallo-netwerkstuurprogramma versnelde voor Linux, volledige Hallo stappen voor het Hallo [Linux configureren](#configure-linux) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="c6622-244"><a name="configure-linux"></a>Configureren van Linux</span><span class="sxs-lookup"><span data-stu-id="c6622-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="c6622-245">Zodra u Hallo VM in Azure maakt, moet u Hallo versnelde-netwerkstuurprogramma voor Linux installeren.</span><span class="sxs-lookup"><span data-stu-id="c6622-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="c6622-246">Voordat u Hallo stappen uitvoert, moet u een Linux-VM gemaakt met versnelde netwerken met behulp van beide Hallo [portal](#linux-portal) of [PowerShell](#linux-powershell) stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c6622-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="c6622-247">Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="c6622-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="c6622-248">Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="c6622-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="c6622-249">Hallo boven aan het portal toohello rechts Hallo Hallo *zoeken bronnen* balk, klikt u op Hallo **> _** pictogram toostart een cloud Bash-shell (Preview).</span><span class="sxs-lookup"><span data-stu-id="c6622-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="c6622-250">Hallo Bash cloud shell deelvenster verschijnt onderin Hallo van Hallo-portal en na een paar seconden geeft een  **username@Azure:~ $** prompt.</span><span class="sxs-lookup"><span data-stu-id="c6622-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="c6622-251">Hoewel u SSH toohello VM vanaf uw computer in plaats van door Hallo cloud shell kunt, Hallo-instructies in deze zelfstudie wordt ervan uitgegaan dat u Hallo cloud shell.</span><span class="sxs-lookup"><span data-stu-id="c6622-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="c6622-252">Bovenaan Hallo Hallo-portal, in Hallo vak die bevat tekst hello *zoeken bronnen*, type *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="c6622-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="c6622-253">Wanneer **MyVm** wordt weergegeven in zoekresultaten hello, klik erop.</span><span class="sxs-lookup"><span data-stu-id="c6622-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="c6622-254">In Hallo **MyVm** blade die wordt weergegeven, klikt u op Hallo **Connect** knop in Hallo linksboven Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="c6622-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="c6622-255">**Opmerking:** als **maken** zichtbaar onder Hallo **Connect** knop Azure is nog niet voltooid Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="c6622-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="c6622-256">Klik op **Connect** pas nadat u niet meer zien **maken** onder Hallo **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="c6622-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="c6622-257">Azure opent u een melding tooenter hello `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="c6622-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="c6622-258">Voer deze opdracht Hallo cloud shell (of kopiëren van Hallo vak die werden weergegeven in stap 4 en plak deze in de cloud-shell toohello), druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="c6622-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="c6622-259">Voer **Ja** toohello vraag waarin u indien toocontinue verbinding maakt gewenst, druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="c6622-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="c6622-260">U hebt ingevoerd bij het maken van VM Hallo Hallo-wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="c6622-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="c6622-261">Eenmaal aangemeld toohello VM, ziet u een adminuser@MyVm:~ $ prompt.</span><span class="sxs-lookup"><span data-stu-id="c6622-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="c6622-262">U bent nu aangemeld toohello VM via Hallo cloud shell-sessie.</span><span class="sxs-lookup"><span data-stu-id="c6622-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="c6622-263">**Opmerking:** Cloud shell sessies time-out na 10 minuten van inactiviteit.</span><span class="sxs-lookup"><span data-stu-id="c6622-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="c6622-264">Op dit moment afhankelijk Hallo instructies van Hallo-distributie die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c6622-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="c6622-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="c6622-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="c6622-266">Voer bij Hallo-prompt `uname -r` en Bevestig Hallo-versie voor:</span><span class="sxs-lookup"><span data-stu-id="c6622-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="c6622-267">Ubuntu is '4.4.0-77-generic,' of hoger</span><span class="sxs-lookup"><span data-stu-id="c6622-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="c6622-268">SLES is '4.4.59-92.20-default' of hoger</span><span class="sxs-lookup"><span data-stu-id="c6622-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="c6622-269">Actieve Hallo-opdrachten die achter een band tussen Hallo standaard netwerken vNIC en Hallo versnelde netwerken vNIC maken.</span><span class="sxs-lookup"><span data-stu-id="c6622-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="c6622-270">Netwerkverkeer gebruikt Hallo beter presteren versnelde netwerken vNIC, terwijl Hallo obligatie zorgt ervoor dat netwerkverkeer via de configuratiewijzigingen niet wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="c6622-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="c6622-271">Na het Hallo-script wordt uitgevoerd, hebben Hallo VM wordt opnieuw opgestart nadat een 60 seconden onderbreken.</span><span class="sxs-lookup"><span data-stu-id="c6622-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="c6622-272">Hallo VM opnieuw wordt opgestart, verbinding eenmaal tooit door stap 5-7 opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c6622-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="c6622-273">Voer Hallo `ifconfig` opdracht in en Bevestig dat bond0 is actief en Hallo-interface wordt weergegeven als omhoog.</span><span class="sxs-lookup"><span data-stu-id="c6622-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="c6622-274">Toepassingen die gebruikmaken van versnelde netwerken moeten communiceren via Hallo *bond0* interface niet *eth0*.</span><span class="sxs-lookup"><span data-stu-id="c6622-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="c6622-275">Hallo Interfacenaam overgaan voordat versnelde netwerken algemene beschikbaarheid bereikt.</span><span class="sxs-lookup"><span data-stu-id="c6622-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="c6622-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="c6622-276">RHEL/CentOS</span></span>

<span data-ttu-id="c6622-277">Maken van een Red Hat Enterprise Linux of CentOS 7.3 VM, is enkele extra stappen tooload Hallo meest recente stuurprogramma's die nodig is voor SR-IOV en hello (VF stuurprogramma Virtual Function) voor de netwerkkaart Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="c6622-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="c6622-278">Hallo bereidt eerste fase van de instructies Hallo een installatiekopie die gebruikt toomake worden kan een of meer virtuele machines die Hallo-stuurprogramma's die vooraf is geladen.</span><span class="sxs-lookup"><span data-stu-id="c6622-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="c6622-279">Stap 1: een Red Hat Enterprise Linux of CentOS 7.3 basisinstallatiekopie voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="c6622-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="c6622-280">Inrichten van een niet - SRIOV CentOS 7.3 VM op Azure</span><span class="sxs-lookup"><span data-stu-id="c6622-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="c6622-281">LIS 4.2.2 installeren:</span><span class="sxs-lookup"><span data-stu-id="c6622-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="c6622-282">De config-bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="c6622-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="c6622-283">Inrichting ervan ongedaan maakt deze VM</span><span class="sxs-lookup"><span data-stu-id="c6622-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="c6622-284">Vanuit Azure-portal stop deze virtuele machine; en gaat u tooVM van '-schijven genoemd, vastleggen Hallo OSDisk van VHD-URI.</span><span class="sxs-lookup"><span data-stu-id="c6622-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="c6622-285">Deze URI bevat Hallo basisinstallatiekopie van VHD-naam en de storage-account.</span><span class="sxs-lookup"><span data-stu-id="c6622-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="c6622-286">Fase twee: inrichten van nieuwe virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="c6622-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="c6622-287">Nieuwe virtuele machines op basis van nieuw AzureRMVMConfig inrichten met behulp van Hallo basisinstallatiekopie VHD vastgelegd in stap 1, met AcceleratedNetworking ingeschakeld op Hallo vNIC:</span><span class="sxs-lookup"><span data-stu-id="c6622-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="c6622-288">Nadat de virtuele machines wordt opgestart, 'lspci' hello VF apparaat controleren en Hallo Mellanox invoer.</span><span class="sxs-lookup"><span data-stu-id="c6622-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="c6622-289">Bijvoorbeeld, zien we dit item in Hallo lspci uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c6622-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="c6622-290">Hallo binding script door uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c6622-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="c6622-291">Start opnieuw op Hallo van nieuwe virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="c6622-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="c6622-292">Hallo VM moet beginnen met bond0 geconfigureerd en Hallo versnelde netwerken pad ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c6622-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="c6622-293">Voer `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c6622-293">Run `ifconfig` tooconfirm.</span></span>
