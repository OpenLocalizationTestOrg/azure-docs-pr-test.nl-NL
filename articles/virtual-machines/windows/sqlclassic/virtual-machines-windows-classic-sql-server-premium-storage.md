---
title: aaaUse Azure Premium-opslag met SQL Server | Microsoft Docs
description: Dit artikel maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel Hallo en biedt richtlijnen over het gebruik van Azure Premium-opslag met SQL Server wordt uitgevoerd op Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="1ceed-103">Azure Premium Storage gebruiken met SQL Server op Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ceed-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="1ceed-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1ceed-104">Overview</span></span>
<span data-ttu-id="1ceed-105">[Azure Premium-opslag](../../../storage/common/storage-premium-storage.md) generatie van opslag die een lage latentie hoge doorvoersnelheid IO en is Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ceed-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="1ceed-106">Het meest geschikt is voor belangrijke IO intensieve werkbelastingen, zoals SQL Server op IaaS [virtuele Machines](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="1ceed-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ceed-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1ceed-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1ceed-108">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1ceed-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1ceed-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="1ceed-110">Dit artikel bevat plannen en richtlijnen voor het migreren van een virtuele Machine met SQL Server-toouse Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="1ceed-111">Dit omvat de Azure-infrastructuur (netwerk-, opslag) en Gast Windows VM stappen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="1ceed-112">Hallo-voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) ziet u de migratie van een volledige uitgebreide end tooend van hoe toomove grotere virtuele machines tootake profiteren van betere lokale SSD-opslag met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ceed-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="1ceed-113">Het is belangrijk toounderstand Hallo end-to-end-proces met Azure Premium-opslag met SQL Server op IAAS VM's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="1ceed-114">Dit omvat:</span><span class="sxs-lookup"><span data-stu-id="1ceed-114">This includes:</span></span>

* <span data-ttu-id="1ceed-115">Identificatie van Hallo vereisten toouse Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="1ceed-116">Voorbeelden voor het implementeren van SQL Server op IaaS tooPremium opslag voor nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="1ceed-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="1ceed-117">Voorbeelden van migreren bestaande implementaties, zowel zelfstandige servers en implementaties met behulp van SQL AlwaysOn-beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="1ceed-118">Mogelijke migratie nadert.</span><span class="sxs-lookup"><span data-stu-id="1ceed-118">Possible migration approaches.</span></span>
* <span data-ttu-id="1ceed-119">Volledige end-to-end-voorbeeld Azure, Windows en SQL Server-stappen voor migratie van een bestaande implementatie altijd op Hallo wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1ceed-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="1ceed-120">Zie voor meer achtergrondinformatie op SQL Server in Azure Virtual Machines, [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ceed-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="1ceed-121">**Auteur:** Daniel Sol **technische controleurs:** Luis Jeroen Vargas haring, Sanjay Mishra, Pravin Mital, Schwertl Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="1ceed-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="1ceed-122">Vereisten voor de Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="1ceed-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="1ceed-123">Er zijn verschillende vereisten voor het gebruik van Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="1ceed-124">Grootte van de machine</span><span class="sxs-lookup"><span data-stu-id="1ceed-124">Machine size</span></span>
<span data-ttu-id="1ceed-125">Voor het gebruik van Premium-opslag moet u toouse DS reeks virtuele Machines (VM).</span><span class="sxs-lookup"><span data-stu-id="1ceed-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="1ceed-126">Als u niet DS-serie machines in uw cloudservice voordat u gebruikt hebt, moet u Hallo bestaande VM verwijderen, Hallo gekoppelde schijven houden en vervolgens een nieuwe cloudservice maken voordat de virtuele machine als de grootte van de rol DS * Hallo opnieuw te maken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="1ceed-127">Zie voor meer informatie over grootten van virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ceed-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="1ceed-128">Cloud services</span><span class="sxs-lookup"><span data-stu-id="1ceed-128">Cloud services</span></span>
<span data-ttu-id="1ceed-129">U kunt alleen virtuele machines DS * met Premium-opslag gebruiken wanneer ze worden gemaakt in een nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1ceed-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="1ceed-130">Als u SQL Server Always On in Azure, verwijzen Hallo altijd-Listener voor toohello Azure interne of externe Load Balancer-IP-adres dat is gekoppeld aan een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1ceed-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="1ceed-131">In dit artikel is gericht op het toomigrate behoud van beschikbaarheid in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="1ceed-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-132">Een reeks DS * moet de Hallo eerste virtuele machine die is geïmplementeerd toohello nieuwe Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1ceed-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="1ceed-133">Regionaal vnet 's</span><span class="sxs-lookup"><span data-stu-id="1ceed-133">Regional VNETS</span></span>
<span data-ttu-id="1ceed-134">Voor virtuele machines DS * moet u Hallo virtuele netwerk (VNET) die als host fungeert voor uw virtuele machines van regionale toobe configureren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="1ceed-135">Deze 'breder' hello VNET tooallow Hallo grotere virtuele machines toobe ingericht in andere clusters is en communicatie tussen deze twee toestaan.</span><span class="sxs-lookup"><span data-stu-id="1ceed-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="1ceed-136">In Hallo schermafbeelding te volgen, weergegeven hello gemarkeerde locatie regionaal vnet's, terwijl de eerste resultaat Hallo een 'smalle' VNET toont.</span><span class="sxs-lookup"><span data-stu-id="1ceed-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="1ceed-138">U kunt een Microsoft-ondersteuning ticket toomigrate tooa verhogen regionaal VNET, Microsoft wordt een wijziging aanbrengt toocomplete Hallo migratie tooregional VNETs, wijzig Hallo eigenschap AffinityGroup in Hallo-netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="1ceed-139">Hallo netwerkconfiguratie in PowerShell eerst te exporteren en vervolgens vervangen Hallo **AffinityGroup** eigenschap in Hallo **VirtualNetworkSite** element met een **locatie** de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1ceed-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="1ceed-140">Geef `Location = XXXX` waar `XXXX` is een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="1ceed-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="1ceed-141">Hallo nieuwe configuratie importeren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-141">Then import hello new configuration.</span></span>

<span data-ttu-id="1ceed-142">Bijvoorbeeld, overweegt Hallo VNET-configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="1ceed-143">toomove deze tooa regionaal VNET in West-Europa wijzigen Hallo configuratie toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="1ceed-144">Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="1ceed-144">Storage accounts</span></span>
<span data-ttu-id="1ceed-145">U moet toocreate een nieuw opslagaccount die is geconfigureerd voor Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="1ceed-146">Houd er rekening mee dat Hallo gebruik van Premium-opslag is ingesteld op Hallo storage-account, niet op afzonderlijke VHD's, maar bij gebruik van een DS * reeks VM u de VHD van Premium en Standard-opslag-accounts koppelen kunt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="1ceed-147">U kunt dit overwegen als u niet dat tooplace Hallo OS VHD op toohello Premium Storage-account wilt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="1ceed-148">Hallo volgende **nieuw AzureStorageAccountPowerShell** opdracht 'Premium_LRS' Hello **Type** maakt een Premium-Opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="1ceed-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="1ceed-149">Cache-instellingen voor virtuele harde schijven</span><span class="sxs-lookup"><span data-stu-id="1ceed-149">VHDs Cache Settings</span></span>
<span data-ttu-id="1ceed-150">Hallo belangrijkste verschil tussen het maken van schijven die deel van een Premium Storage-account uitmaken is Hallo schijfcache-instelling.</span><span class="sxs-lookup"><span data-stu-id="1ceed-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="1ceed-151">Voor SQL Server-gegevens volume het schijven wordt aanbevolen dat u '**Lees-Caching**'.</span><span class="sxs-lookup"><span data-stu-id="1ceed-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="1ceed-152">Voor transactie logboekvolumes, Hallo schijfcache-instelling te moet worden ingesteld '**geen**'.</span><span class="sxs-lookup"><span data-stu-id="1ceed-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="1ceed-153">Dit wijkt af van Hallo aanbevelingen voor Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="1ceed-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="1ceed-154">Eenmaal Hallo VHD's zijn gekoppeld, kan Hallo cache-instelling kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="1ceed-155">U moet toodetach en koppelt u Hallo VHD opnieuw met een bijgewerkte cache-instelling.</span><span class="sxs-lookup"><span data-stu-id="1ceed-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="1ceed-156">Windows-opslagruimten</span><span class="sxs-lookup"><span data-stu-id="1ceed-156">Windows storage spaces</span></span>
<span data-ttu-id="1ceed-157">U kunt [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) zoals u deed met vorige Standard-opslag, Hierdoor kunt u een virtuele machine die wordt al gebruikt door opslagruimten toomigrate.</span><span class="sxs-lookup"><span data-stu-id="1ceed-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="1ceed-158">Hallo-voorbeeld in [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (stap 9 en voorwaarts) laat zien Hallo Powershell code tooextract en importeren van een virtuele machine met meerdere gekoppelde VHD's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="1ceed-159">Opslaggroepen zijn gebruikt met standaard Azure storage-account tooenhance doorvoer en de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="1ceed-160">Wellicht waarde in nieuwe implementaties het testen van opslaggroepen met Premium-opslag, maar ze extra complexiteit met setup opslag toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="1ceed-161">Hoe toofind welke virtuele schijven van Azure toostorage groepen toewijzen</span><span class="sxs-lookup"><span data-stu-id="1ceed-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="1ceed-162">Als er verschillende cache-instelling aanbevelingen voor het gekoppelde VHD's zijn, besluiten u toocopy Hallo VHD's tooa Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="1ceed-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="1ceed-163">Echter, wanneer u koppelt u deze opnieuw toohello nieuwe DS reeks VM, moet u mogelijk tooalter Hallo cache-instellingen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="1ceed-164">Het is eenvoudiger tooapply Hallo die Premium-opslag instellingen voor de uitvoercache aanbevolen wanneer er een aparte virtuele harde schijven Hallo SQL-gegevens bestanden en logboek-bestanden (in plaats van voor een enkele VHD met zowel).</span><span class="sxs-lookup"><span data-stu-id="1ceed-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-165">Als u SQL Server-gegevens en logboekbestanden bestanden op hetzelfde volume, Hallo caching optie die u kiest, is afhankelijk van Hallo i/o-toegangspatronen voor de werkbelasting van uw database Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="1ceed-166">Alleen testen kunt laten zien welke cache-instelling wordt aanbevolen voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="1ceed-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="1ceed-167">Als u gebruikmaakt van Windows Storage Spaces die bestaan uit meerdere VHD's moet u toolook op uw oorspronkelijke scripts tooidentify die gekoppeld VHD's zijn echter in welke specifieke groep, dus vervolgens kunt u instellen Hallo cache-instellingen dienovereenkomstig voor elke schijf.</span><span class="sxs-lookup"><span data-stu-id="1ceed-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="1ceed-168">Als u nog geen oorspronkelijke script beschikbaar tooshow u die VHD's zijn toegewezen toohello opslaggroep, kunt u Hallo stappen toodetermine Hallo schijfopslag/groep toewijzing te volgen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="1ceed-169">Gebruik voor elke schijf Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="1ceed-170">Haal de lijst met schijven gekoppeld tooVM Hello **Get-AzureVM** opdracht:</span><span class="sxs-lookup"><span data-stu-id="1ceed-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="1ceed-171">Get-AzureVM - ServiceName <servicename> -naam <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="1ceed-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="1ceed-172">Houd er rekening mee Hallo Diskname en LUN.</span><span class="sxs-lookup"><span data-stu-id="1ceed-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="1ceed-174">Extern bureaublad in Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1ceed-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="1ceed-175">Ga te**Computerbeheer** | **Apparaatbeheer** | **schijfstations**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="1ceed-176">Bekijk Hallo eigenschappen van elke Hallo 'virtuele schijven Microsoft'</span><span class="sxs-lookup"><span data-stu-id="1ceed-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="1ceed-178">Hier Hallo LUN-nummer is een referentienummer toohello LUN dat die u opgeeft bij het toevoegen van Hallo VHD toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1ceed-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="1ceed-179">Ga voor Hallo Microsoft Virtual Disk toohello **Details** tabblad en klik vervolgens in Hallo **eigenschap** weergeven, gaat u te**stuurprogrammasleutel**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="1ceed-180">In Hallo **waarde**, opmerking Hallo **Offset**, namelijk 0002 in Hallo volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="1ceed-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="1ceed-181">Hallo 0002 geeft Hallo PhysicalDisk2 die Hallo storage pool verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="1ceed-183">Voor elke opslaggroep gekoppeld dump uit Hallo schijven:</span><span class="sxs-lookup"><span data-stu-id="1ceed-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="1ceed-184">Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="1ceed-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="1ceed-186">Nu kunt u gekoppelde deze informatie tooassociate VHD's tooPhysical schijven in opslaggroepen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="1ceed-187">Zodra u de VHD's tooPhysical schijven in opslaggroepen vervolgens loskoppelen en kopieert u deze via tooa Premium Storage-account hebt gekoppeld, koppelt u ze met de juiste cache Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="1ceed-188">Zie Hallo voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), stappen 8 tot en met 12.</span><span class="sxs-lookup"><span data-stu-id="1ceed-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="1ceed-189">Deze stappen laten zien hoe tooextract een VM gekoppeld VHD schijf configuratie tooa CSV-bestand kopiëren Hallo VHD's, Hallo schijf configuratie cache-instellingen wijzigen en ten slotte Hallo VM implementeren als een DS-serie VM alle Hello gekoppelde schijven.</span><span class="sxs-lookup"><span data-stu-id="1ceed-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="1ceed-190">VM-opslag bandbreedte en opslagdoorvoer VHD</span><span class="sxs-lookup"><span data-stu-id="1ceed-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="1ceed-191">Hallo bedrag van de prestaties van de opslag, is afhankelijk van Hallo DS * VM-grootte opgegeven en Hallo grootten van de VHD.</span><span class="sxs-lookup"><span data-stu-id="1ceed-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="1ceed-192">Hallo virtuele machines hebben verschillende rechten voor het aantal virtuele harde schijven die kunnen worden bijgevoegd en maximale bandbreedte wordt ondersteund (MB/s) Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ceed-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="1ceed-193">Zie voor Hallo specifieke bandbreedte cijfers [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ceed-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1ceed-194">Verbeterde IOPS worden verkregen met grotere schijf.</span><span class="sxs-lookup"><span data-stu-id="1ceed-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="1ceed-195">Dit moet u overwegen wanneer u over het migratiepad voor de nadenkt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="1ceed-196">Voor meer informatie [Zie Hallo tabel voor IOPS en schijftypen](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="1ceed-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="1ceed-197">Overweeg tot slot dat virtuele machines hebben verschillende maximale schijf-bandbreedten die wordt ondersteund voor alle schijven die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="1ceed-198">U kunt Hallo maximale schijf-bandbreedte die beschikbaar is voor de grootte van die VM-rol kan verzadigen onder hoge belasting.</span><span class="sxs-lookup"><span data-stu-id="1ceed-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="1ceed-199">Bijvoorbeeld wordt een Standard_DS14 ondersteuning voor maximaal too512MB/s; Daarom kan u Hallo schijf bandbreedte van Hallo VM verzadigen met drie P30 schijven.</span><span class="sxs-lookup"><span data-stu-id="1ceed-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="1ceed-200">Maar in dit voorbeeld kan Hallo doorvoer limiet wordt overschreden, afhankelijk van Hallo combinatie van lees- en IOs.</span><span class="sxs-lookup"><span data-stu-id="1ceed-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="1ceed-201">Nieuwe implementaties</span><span class="sxs-lookup"><span data-stu-id="1ceed-201">New deployments</span></span>
<span data-ttu-id="1ceed-202">de volgende twee secties Hallo laten zien hoe u SQL Server-VM's tooPremium opslag kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="1ceed-203">Zoals al eerder vermeld, hoeft niet per se u tooplace hello besturingssysteemschijf naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="1ceed-204">U kunt toodo dit als u tooplace een intensieve i/o-werkbelastingen op Hallo OS VHD wilde weet.</span><span class="sxs-lookup"><span data-stu-id="1ceed-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="1ceed-205">Hallo eerste voorbeeld laat zien met behulp van de bestaande Azure-galerie met installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="1ceed-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="1ceed-206">Hallo tweede voorbeeld laat zien hoe toouse een aangepaste VM-installatiekopie is die u in een bestaand standaard opslagaccount hebt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-207">Deze voorbeelden wordt ervan uitgegaan dat u al een regionaal VNET hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="1ceed-208">Maak een nieuwe virtuele machine met Premium-opslag met afbeelding</span><span class="sxs-lookup"><span data-stu-id="1ceed-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="1ceed-209">Hallo voorbeeld hieronder ziet u hoe tooplace Hallo OS VHD naar premium-opslag en Premium-opslag-VHD's koppelen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="1ceed-210">U kunt echter ook Hallo besturingssysteemschijf plaatsen in een Standard-opslagaccount en koppel vervolgens de VHD's die zich in een Premium-opslagaccount bevinden.</span><span class="sxs-lookup"><span data-stu-id="1ceed-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="1ceed-211">Beide scenario's worden uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="1ceed-212">Stap 1: Een Premium Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="1ceed-213">Stap 2: Maak een nieuwe Cloudservice</span><span class="sxs-lookup"><span data-stu-id="1ceed-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="1ceed-214">Stap 3: Gereserveerd VIP van de Cloud-Service (optioneel)</span><span class="sxs-lookup"><span data-stu-id="1ceed-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="1ceed-215">Stap 4: Een VM-Container maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="1ceed-216">Stap 5: Brengen OS VHD Standard of Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="1ceed-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="1ceed-217">Stap 6: Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="1ceed-218">Een nieuwe VM-toouse Premium-opslag met een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="1ceed-219">Dit scenario laat zien waar u de bestaande aangepaste installatiekopieën die zich in een Standard-opslag-account bevinden hebt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="1ceed-220">Zoals vermeld als u wilt dat tooplace Hallo OS VHD op Premium-opslag moet u toocopy Hallo installatiekopie of aanwezig is op Hallo Standard-opslagaccount en dragen deze tooa Premium-opslag voordat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="1ceed-221">Als u een installatiekopie van een lokale, kunt u ook deze toocopy methode gebruiken die rechtstreeks toohello Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="1ceed-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="1ceed-222">Stap 1: De Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="1ceed-223">Stap 2-Cloudservice maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="1ceed-224">Stap 3: Een bestaande installatiekopie gebruiken</span><span class="sxs-lookup"><span data-stu-id="1ceed-224">Step 3: Use existing image</span></span>
<span data-ttu-id="1ceed-225">U kunt een bestaande installatiekopie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-225">You can use an existing image.</span></span> <span data-ttu-id="1ceed-226">U kunt [nemen van een installatiekopie van een bestaande machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ceed-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="1ceed-227">Opmerking Hallo machine die u een installatiekopie heeft geen toobe DS * machine.</span><span class="sxs-lookup"><span data-stu-id="1ceed-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="1ceed-228">Zodra u de installatiekopie van het Hallo hebt, Hallo volgen stappen tonen hoe toocopy het toohello Premium Storage-account met Hallo **Start AzureStorageBlobCopy** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ceed-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="1ceed-229">Stap 4: Kopieer Blob tussen Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="1ceed-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="1ceed-230">Stap 5: Controleer regelmatig de status van het exemplaar:</span><span class="sxs-lookup"><span data-stu-id="1ceed-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="1ceed-231">Stap 6: Installatiekopie tooAzure schijf opslagplaats in abonnement toevoegen</span><span class="sxs-lookup"><span data-stu-id="1ceed-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="1ceed-232">Kan het gebeuren dat hoewel Hallo als geslaagd statusrapporten u kan nog steeds een schijffout lease.</span><span class="sxs-lookup"><span data-stu-id="1ceed-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="1ceed-233">In dit geval wacht tien minuten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="1ceed-234">Stap 7: Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="1ceed-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="1ceed-235">U maakt hier Hallo VM van uw installatiekopie en twee Premium-opslag-VHD's koppelen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="1ceed-236">Bestaande implementaties die altijd op beschikbaarheidsgroepen niet wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="1ceed-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="1ceed-237">Voor bestaande implementaties raadpleegt u eerst Hallo [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="1ceed-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="1ceed-238">Er zijn verschillende overwegingen voor implementaties van SQL Server die niet altijd op beschikbaarheidsgroepen en programma's die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="1ceed-239">Als u altijd op niet gebruikt en een bestaande zelfstandige SQL Server hebt, kunt u tooPremium opslag upgraden met behulp van een nieuw cloud service- en storage-account.</span><span class="sxs-lookup"><span data-stu-id="1ceed-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="1ceed-240">Houd rekening met Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="1ceed-240">Consider hello following options:</span></span>

* <span data-ttu-id="1ceed-241">**Maak een nieuwe SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="1ceed-242">U kunt een nieuwe versie van SQL Server VM die gebruikmaakt van een Premium-opslagaccount maken, zoals beschreven in nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="1ceed-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="1ceed-243">Vervolgens back-up en herstel van SQL Server-configuratie- en databases.</span><span class="sxs-lookup"><span data-stu-id="1ceed-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="1ceed-244">Hallo toepassing moet toobe bijgewerkt tooreference Hallo nieuwe SQL-Server als intern of extern wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1ceed-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="1ceed-245">U moet toocopy alle objecten voor buiten-db' als u een gelijktijdige (SxS) SQL Server-migratie deed.</span><span class="sxs-lookup"><span data-stu-id="1ceed-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="1ceed-246">Dit omvat objecten, zoals aanmeldingen, certificaten en gekoppelde servers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="1ceed-247">**Migreren van een bestaande SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="1ceed-248">Hiervoor moet Hallo virtuele machine van SQL Server offline moet worden gezet en vervolgens overdragen tooa nieuwe cloudservice, waaronder kopiëren alle van de gekoppelde VHD's toohello Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="1ceed-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="1ceed-249">Wanneer Hallo VM online wordt gezet, wordt de toepassing hello verwijzen naar Hallo hostnaam als voordat.</span><span class="sxs-lookup"><span data-stu-id="1ceed-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="1ceed-250">Let erop dat Hallo grootte van de bestaande schijf Hallo invloed is op Hallo prestatiekenmerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="1ceed-251">Een schijf 400 GB opgehaald bijvoorbeeld tooa P20 afgerond.</span><span class="sxs-lookup"><span data-stu-id="1ceed-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="1ceed-252">Als u weet dat u niet nodig hebt die schijfprestaties kan u Hallo virtuele machine als een reeks DS VM opnieuw te maken en koppelen van Premium Storage VHD's van Hallo grootte/prestaties specificatie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="1ceed-253">Vervolgens kan u loskoppelen en weer koppelt Hallo SQL DB-bestanden.</span><span class="sxs-lookup"><span data-stu-id="1ceed-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-254">Wanneer welk type opslagschijf Premium kopiëren Hallo VHD schijven u rekening moet houden met een grootte van hello, afhankelijk van de grootte Hallo betekent dat ze vallen, dit schijf prestaties specificatie bepaalt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="1ceed-255">Azure worden afgerond up toohello dichtstbijzijnde schijf grootte, dus als er een schijf van 400 GB, dit wordt afgerond tooa P20.</span><span class="sxs-lookup"><span data-stu-id="1ceed-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="1ceed-256">Afhankelijk van uw bestaande i/o-vereisten Hallo OS VHD moet u mogelijk niet toomigrate deze tooa Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="1ceed-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="1ceed-257">Als uw SQL-Server extern wordt geopend, klikt u vervolgens Hallo cloud service VIP gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="1ceed-258">U hebt tevens tooupdate eindpunten, ACL's en DNS-instellingen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="1ceed-259">Bestaande implementaties die gebruikmaken van altijd op beschikbaarheidsgroepen</span><span class="sxs-lookup"><span data-stu-id="1ceed-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="1ceed-260">Voor bestaande implementaties raadpleegt u eerst Hallo [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="1ceed-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="1ceed-261">In eerste instantie in dit gedeelte kijken we altijd op de interactie met Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="1ceed-262">Er wordt vervolgens migraties in scenario's tootwo opsplitsen: waar u enige uitvaltijd kan verdragen migraties en migraties waar u de minimale downtime moet bereiken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="1ceed-263">Lokale SQL Server AlwaysOn-beschikbaarheidsgroepen gebruiken een Listener op lokale waarmee een virtuele DNS-naam samen met een IP-adres dat wordt gedeeld tussen een of meer SQL-Servers geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="1ceed-264">Wanneer clients verbinding maken, worden ze via Hallo listener IP-toohello primaire SQL-Server gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="1ceed-265">Dit is Hallo-server die eigenaar is van Hallo altijd op IP-resource op dat moment.</span><span class="sxs-lookup"><span data-stu-id="1ceed-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways op][6]

<span data-ttu-id="1ceed-267">U kunt slechts één IP-adres toegewezen tooa NIC op Hallo VM, daarom in volgorde van tooachieve Hallo dezelfde laag van abstractie als lokale, Hallo IP-adres dat is toegewezen toohello interne of externe Load Balancers (ILB/ELB) maakt gebruik van Azure hebben in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1ceed-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="1ceed-268">Hallo IP-resource die wordt gedeeld tussen servers Hallo toohello is ingesteld dezelfde IP als Hallo ILB-/ ELB.</span><span class="sxs-lookup"><span data-stu-id="1ceed-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="1ceed-269">Dit is gepubliceerd in Hallo DNS en clientverkeer Hallo ILB-/ ELB toohello primaire SQL Server-replica is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="1ceed-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="1ceed-270">Hallo ILB-/ ELB kent die SQL Server is de primaire omdat hierbij tests tooprobe Hallo altijd op IP-resource.</span><span class="sxs-lookup"><span data-stu-id="1ceed-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="1ceed-271">In het vorige voorbeeld hello, deze tests op elk knooppunt dat een waarnaar wordt verwezen door Hallo ELB/ILB eindpunt, afhankelijk van wat reageert is Hallo primaire SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="1ceed-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-272">Hallo ILB en ELB zijn beide toegewezen tooa bepaald Azure-cloudservice, daarom cloudmigratie in Azure waarschijnlijk betekent dat dat Hallo die Load Balancer IP wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="1ceed-273">Migreren altijd op implementaties die enige downtime kunnen toestaan</span><span class="sxs-lookup"><span data-stu-id="1ceed-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="1ceed-274">Er zijn twee strategieën toomigrate altijd op implementaties die voor enige downtime toestaan:</span><span class="sxs-lookup"><span data-stu-id="1ceed-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="1ceed-275">**Meer secundaire replica's tooan bestaande altijd op de Cluster toevoegen**</span><span class="sxs-lookup"><span data-stu-id="1ceed-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="1ceed-276">**Migreren van tooa nieuwe altijd op Cluster**</span><span class="sxs-lookup"><span data-stu-id="1ceed-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="1ceed-277">1. Voeg meer secundaire replica's tooan bestaande altijd op Cluster</span><span class="sxs-lookup"><span data-stu-id="1ceed-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="1ceed-278">Een strategie tooadd meer secundaire databases toohello AlwaysOn-beschikbaarheidsgroep is.</span><span class="sxs-lookup"><span data-stu-id="1ceed-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="1ceed-279">U moet tooadd deze in een nieuwe cloudservice en het bijwerken van Hallo listener Hallo nieuwe load balancer-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1ceed-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="1ceed-280">De punten van downtime:</span><span class="sxs-lookup"><span data-stu-id="1ceed-280">Points of downtime:</span></span>
* <span data-ttu-id="1ceed-281">Clustervalidatie van het.</span><span class="sxs-lookup"><span data-stu-id="1ceed-281">Cluster Validation.</span></span>
* <span data-ttu-id="1ceed-282">Always On failover testen voor de nieuwe secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="1ceed-283">Als u Windows-opslaggroepen binnen Hallo VM voor een hogere i/o-doorvoer en vervolgens deze zal offline worden gehaald tijdens een volledige validatie van de Cluster.</span><span class="sxs-lookup"><span data-stu-id="1ceed-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="1ceed-284">Hallo validatietest is vereist als u knooppunten toohello cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="1ceed-285">Hallo duurt toorun Hallo test kan variëren, dus u dit in uw omgeving representatief test tooget bij benadering de tijd testen moet van hoe lang dit gaat duren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="1ceed-286">U moet de tijd waarin u de handmatige failover kunt uitvoeren en chaos testen op Hallo zojuist toegevoegd knooppunten tooensure altijd op hoge beschikbaarheid functies zoals verwacht inrichten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="1ceed-288">Alle exemplaren van SQL Server waar de opslaggroepen hello worden gebruikt voordat hello validatie wordt uitgevoerd, moet worden gestopt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="1ceed-289">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="1ceed-289">High-level steps</span></span>
>

1. <span data-ttu-id="1ceed-290">Maak twee nieuwe SQL-Servers in de nieuwe cloudservice met gekoppelde Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1ceed-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="1ceed-291">Kopiëren via volledige back-ups en herstellen met **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="1ceed-292">Kopiëren via 'buiten user DB' afhankelijke objecten, zoals aanmeldingen enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1ceed-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="1ceed-293">Maken van nieuwe een nieuwe interne Load Balancer (ILB) of gebruik een externe Load Balancer (ELB) en vervolgens Load Balanced eindpunten instellen op beide nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1ceed-294">Controleer dat alle knooppunten hebben het juiste eindpuntconfiguratie Hallo voordat u doorgaat</span><span class="sxs-lookup"><span data-stu-id="1ceed-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="1ceed-295">Gebruiker/toepassing toegang toohello SQL Server stoppen (als u de opslaggroepen).</span><span class="sxs-lookup"><span data-stu-id="1ceed-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="1ceed-296">SQL Server-Engine-Services stoppen op alle knooppunten (als u de opslaggroepen).</span><span class="sxs-lookup"><span data-stu-id="1ceed-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="1ceed-297">Toevoegen van nieuwe knooppunten toocluster en volledige validatie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="1ceed-298">Wanneer validatie voltooid is, start u alle SQL Server-Services.</span><span class="sxs-lookup"><span data-stu-id="1ceed-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="1ceed-299">Transactielogboeken back-up en herstel van gebruikersdatabases.</span><span class="sxs-lookup"><span data-stu-id="1ceed-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="1ceed-300">Nieuwe knooppunten toevoegen aan Hallo AlwaysOn-beschikbaarheidsgroep en replicatie in plaats **synchroon**.</span><span class="sxs-lookup"><span data-stu-id="1ceed-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="1ceed-301">Hallo IP toevoegen bron van het adres van Hallo nieuwe Cloud Service ILB-/ ELB via PowerShell voor altijd op op basis van Hallo multi-site voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="1ceed-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="1ceed-302">Stel in het Windows-clustering, Hallo **mogelijke eigenaars** Hallo **IP-adres** resource toohello nieuwe knooppunten oude.</span><span class="sxs-lookup"><span data-stu-id="1ceed-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="1ceed-303">Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="1ceed-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="1ceed-304">Failover tooone van Hallo nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="1ceed-305">Controleer Hallo nieuwe knooppunten automatisch Failoverpartners en testfailovers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="1ceed-306">Oorspronkelijke knooppunten verwijderen uit de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="1ceed-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="1ceed-307">Voordelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-307">Advantages</span></span>
* <span data-ttu-id="1ceed-308">Nieuwe SQL-Servers kunnen worden getest (SQL Server en toepassing) voordat ze worden tooAlways toegevoegd op.</span><span class="sxs-lookup"><span data-stu-id="1ceed-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="1ceed-309">U kunt Hallo VM-grootte wijzigen en aanpassen van Hallo tooyour exacte opslagvereisten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="1ceed-310">Echter, het normaal zou zijn nuttig tookeep alle Hallo SQL bestandspaden Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="1ceed-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="1ceed-311">U kunt bepalen wanneer de overdracht Hallo van Hallo DB back-ups toohello secundaire replica's worden gestart.</span><span class="sxs-lookup"><span data-stu-id="1ceed-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="1ceed-312">Dit wijkt af van het gebruik van Azure **Start AzureStorageBlobCopy** commandlet toocopy VHD's, omdat dit een asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="1ceed-313">Nadelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-313">Disadvantages</span></span>
* <span data-ttu-id="1ceed-314">Wanneer met behulp van Windows-opslaggroepen, is dit Cluster uitvaltijd tijdens Hallo volledige validatie van het Cluster voor Hallo nieuwe extra knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="1ceed-315">Afhankelijk van Hallo SQL Server-versie en Hallo bestaande aantal secundaire replica's, kunt u niet kunt tooadd worden meer secundaire replica's zonder te verwijderen van bestaande secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="1ceed-316">Kan er lang SQL gegevens overdrachtstijd tijdens het instellen van Hallo secundaire replica's zijn.</span><span class="sxs-lookup"><span data-stu-id="1ceed-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="1ceed-317">Er is extra kosten tijdens de migratie terwijl u nieuwe machines parallelle uitvoering zijn.</span><span class="sxs-lookup"><span data-stu-id="1ceed-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="1ceed-318">2. Migreren van tooa nieuwe altijd op Cluster</span><span class="sxs-lookup"><span data-stu-id="1ceed-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="1ceed-319">Een andere strategie is er toocreate een geheel nieuwe altijd op Cluster met nieuwe knooppunten in nieuwe cloudservice omleiding Hallo clients toouse deze.</span><span class="sxs-lookup"><span data-stu-id="1ceed-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="1ceed-320">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="1ceed-320">Points of downtime</span></span>
<span data-ttu-id="1ceed-321">Er is uitvaltijd wanneer u toepassingen en gebruikers toohello nieuwe altijd-listener voor overdraagt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="1ceed-322">afhankelijk van Hallo downtime:</span><span class="sxs-lookup"><span data-stu-id="1ceed-322">hello downtime depends on:</span></span>

* <span data-ttu-id="1ceed-323">Hallo tijd toorestore laatste transactie logboek back-ups toodatabases op nieuwe servers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="1ceed-324">Hallo tijd tooupdate client toepassingen toouse nieuwe altijd op listener.</span><span class="sxs-lookup"><span data-stu-id="1ceed-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="1ceed-325">Voordelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-325">Advantages</span></span>
* <span data-ttu-id="1ceed-326">U kunt Hallo werkelijke productieomgeving, SQL Server, testen en OS-build-wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="1ceed-327">Hallo optie toocustomize Hallo opslag en toopotentially verkleinen van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1ceed-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="1ceed-328">Dit kan leiden tot kosten te beperken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="1ceed-329">Tijdens dit proces kunt u uw versie van SQL Server of een versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="1ceed-330">U kunt ook Hallo besturingssysteem bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="1ceed-331">Hallo die eerder altijd op Cluster als een doel effen terugdraaien fungeren kan.</span><span class="sxs-lookup"><span data-stu-id="1ceed-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="1ceed-332">Nadelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-332">Disadvantages</span></span>
* <span data-ttu-id="1ceed-333">U moet toochange Hallo DNS-naam van de listener Hallo als u wilt dat beide AlwaysOn-clusters die tegelijkertijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="1ceed-334">Beheer overhead tijdens de migratie hello wordt toegevoegd als tekenreeksen van toepassingen voor client Hallo nieuwe Listener-naam moeten geven.</span><span class="sxs-lookup"><span data-stu-id="1ceed-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="1ceed-335">U kunt een mechanisme voor synchronisatie tussen Hallo twee omgevingen tookeep als sluiten als mogelijke toominimize Hallo laatste synchronisatievereisten voor de migratie moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="1ceed-336">Er is toegevoegd kosten tijdens de migratie terwijl u nieuwe Hallo-omgeving actief zijn.</span><span class="sxs-lookup"><span data-stu-id="1ceed-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="1ceed-337">Migreren altijd op implementaties voor minimale downtime</span><span class="sxs-lookup"><span data-stu-id="1ceed-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="1ceed-338">Er zijn twee strategieën voor het migreren altijd op implementaties voor minimale downtime:</span><span class="sxs-lookup"><span data-stu-id="1ceed-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="1ceed-339">**Gebruikmaken van een bestaande secundaire: één Site**</span><span class="sxs-lookup"><span data-stu-id="1ceed-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="1ceed-340">**Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties**</span><span class="sxs-lookup"><span data-stu-id="1ceed-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="1ceed-341">1. Gebruikmaken van een bestaande secundaire: één Site</span><span class="sxs-lookup"><span data-stu-id="1ceed-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="1ceed-342">Een strategie voor minimale downtime is tootake een bestaande secundaire cloud en van de huidige cloudservice Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="1ceed-343">Kopieer Hallo VHD's toohello nieuwe Premium Storage-account en Hallo VM in Hallo nieuwe cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="1ceed-344">Werk vervolgens Hallo-listener in clustering en failover.</span><span class="sxs-lookup"><span data-stu-id="1ceed-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="1ceed-345">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="1ceed-345">Points of downtime</span></span>
* <span data-ttu-id="1ceed-346">Er is uitvaltijd wanneer u het laatste knooppunt Hallo met gelijke taakverdeling Hallo-eindpunt bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="1ceed-347">Opnieuw verbinden met uw client mogelijk afhankelijk van de client en DNS-configuratie worden uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="1ceed-348">Er is extra uitvaltijd als u ervoor tootake Hallo altijd op de Cluster groep offline tooswap Hallo IP-adressen kiest.</span><span class="sxs-lookup"><span data-stu-id="1ceed-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="1ceed-349">U kunt dit vermijden met behulp van een afhankelijkheid of en mogelijke eigenaars voor Hallo bronnen IP-adres toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="1ceed-350">Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="1ceed-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="1ceed-351">Wanneer u wilt dat Hallo toegevoegde knooppunt toopartake in als altijd op Failover-Partner, moet u tooadd een Azure-eindpunt met een verwijzing toohello Load Balanced ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="1ceed-352">Bij het uitvoeren van Hallo **toevoegen AzureEndpoint** opdracht toodo deze, huidige verbindingen tooremain openen, maar nieuwe verbindingen toohello-listener kan niet kunnen toobe tot stand gebracht totdat Hallo load balancer is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="1ceed-353">In testen was dit waargenomen toolast 90-120seconds, dit moet worden getest.</span><span class="sxs-lookup"><span data-stu-id="1ceed-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="1ceed-354">Voordelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-354">Advantages</span></span>
* <span data-ttu-id="1ceed-355">Er zijn geen extra kosten die zijn gemaakt tijdens de migratie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="1ceed-356">Een-op-een migratie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-356">A one-to-one migration.</span></span>
* <span data-ttu-id="1ceed-357">Minder complexiteit.</span><span class="sxs-lookup"><span data-stu-id="1ceed-357">Reduced complexity.</span></span>
* <span data-ttu-id="1ceed-358">Verbeterde IOPS staat van Premium-opslag-SKU's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="1ceed-359">Als Hallo schijven is losgekoppeld van Hallo VM en gekopieerd toohello nieuwe cloudservice, een 3rd partij worden hulpprogramma gebruikte tooincrease Hallo VHD grootte, die hoger doorvoercapaciteit biedt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="1ceed-360">Zie voor het VHD-grootte verhogen, [forumdiscussie](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="1ceed-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="1ceed-361">Nadelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-361">Disadvantages</span></span>
* <span data-ttu-id="1ceed-362">Er is een tijdelijk onderbroken HA en Noodherstel tijdens de migratie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="1ceed-363">Omdat dit een migratie 1:1, hebt u toouse een minimale VM-grootte die wordt ondersteuning voor het aantal virtuele harde schijven, zodat u mogelijk niet kunnen toodownsize uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1ceed-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="1ceed-364">Dit scenario zou gebruiken hello Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is.</span><span class="sxs-lookup"><span data-stu-id="1ceed-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="1ceed-365">Er is geen SLA op voltooiing van de kopie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="1ceed-366">Hallo-tijd van Hallo kopieën varieert, terwijl dit afhankelijk van de wachttijd in wachtrij die het is ook afhankelijk van Hallo hoeveelheid gegevens tootransfer.</span><span class="sxs-lookup"><span data-stu-id="1ceed-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="1ceed-367">Hallo kopie tijd toeneemt als Hallo overdracht gaat tooanother Azure-datacenter die ondersteuning biedt voor Premium-opslag in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="1ceed-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="1ceed-368">Als u zojuist 2 knooppunten hebt, kunt u overwegen een mogelijke risicobeperking geval Hallo kopie langer dan in de testfase duurt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="1ceed-369">Dit omvat bijvoorbeeld Hallo ideeën te volgen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="1ceed-370">Een tijdelijk 3e SQL Server-knooppunt toevoegen voor HA vóór de migratie Hallo overeengekomen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="1ceed-371">Hallo migratie buiten Azure gepland onderhoud worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="1ceed-372">Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="1ceed-373">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="1ceed-373">High-level steps</span></span>
<span data-ttu-id="1ceed-374">Dit document niet illustratie van de voorbeeld van een volledige end-tooend echter Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) vindt u gedetailleerde informatie die overgenomen tooperform worden kunnen dit.</span><span class="sxs-lookup"><span data-stu-id="1ceed-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="1ceed-376">Schijfconfiguratie verzamelen en verwijderen van het knooppunt hello (gekoppelde VHD's niet verwijderd).</span><span class="sxs-lookup"><span data-stu-id="1ceed-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="1ceed-377">Premium-opslagaccount maken en kopieer van VHD's van Hallo Standard-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="1ceed-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="1ceed-378">Nieuwe cloudservice maken en implementeren van Hallo SQL2 VM in deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1ceed-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="1ceed-379">Hallo VM maken met behulp van Hallo gekopieerd oorspronkelijke besturingssysteem-VHD en koppelen van Hallo gekopieerd VHD's.</span><span class="sxs-lookup"><span data-stu-id="1ceed-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="1ceed-380">Configureer ILB / ELB en het toevoegen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="1ceed-381">Update-Listener door:</span><span class="sxs-lookup"><span data-stu-id="1ceed-381">Update Listener by either:</span></span>
  * <span data-ttu-id="1ceed-382">Duurt Hallo altijd op de groep offline en bij te werken altijd op Listener met nieuwe ILB Hallo / ELB-IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="1ceed-383">Of Hallo IP-adres resource van nieuwe Cloud Service ILB-/ ELB via PowerShell in Windows-clustering toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="1ceed-384">Vervolgens set Hallo mogelijke eigenaars van Hallo IP-adres resource toohello gemigreerd knooppunt SQL2, en dit als afhankelijkheid in Hallo netwerknaam of instellen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="1ceed-385">Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="1ceed-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="1ceed-386">Controleer de DNS-configuratie/doorgiftetaak toohello clients.</span><span class="sxs-lookup"><span data-stu-id="1ceed-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="1ceed-387">SQL1 VM gemigreerd en doorloop de stappen 2-4.</span><span class="sxs-lookup"><span data-stu-id="1ceed-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="1ceed-388">Als u stappen 5ii, voegt u SQL1 als mogelijke eigenaar van Hallo bron van het IP-adres toegevoegd</span><span class="sxs-lookup"><span data-stu-id="1ceed-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="1ceed-389">Testfailovers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="1ceed-390">2. Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="1ceed-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="1ceed-391">Als u knooppunten in meer dan één Azure-datacenter (DC hebben) of als u een hybride omgeving hebt, kunt u een configuratie altijd op in deze omgeving toominimize uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="1ceed-392">Hallo aanpak is toochange Hallo altijd op synchronisatie tooSynchronous voor Hallo on-premises of secundaire domeincontroller voor Azure en failover via toothat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1ceed-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="1ceed-393">Kopieer Hallo VHD's tooa Premium Storage-account en Hallo-machine implementeren in een nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1ceed-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="1ceed-394">Hallo-listener bijwerken en vervolgens een failback uit.</span><span class="sxs-lookup"><span data-stu-id="1ceed-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="1ceed-395">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="1ceed-395">Points of downtime</span></span>
<span data-ttu-id="1ceed-396">Hallo uitvaltijd bestaat uit Hallo tijd toofailover toohello alternatieve DC en terug.</span><span class="sxs-lookup"><span data-stu-id="1ceed-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="1ceed-397">Ook afhankelijk van de client en DNS-configuratie en de client opnieuw verbinden mag worden uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="1ceed-398">Houd rekening met Hallo voorbeeld van een hybride altijd op de configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="1ceed-400">Voordelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-400">Advantages</span></span>
* <span data-ttu-id="1ceed-401">U kunt gebruikmaken van bestaande infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="1ceed-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="1ceed-402">Er Hallo optie toopre-upgrade hello Azure-opslag op Hallo DR Azure DC eerst.</span><span class="sxs-lookup"><span data-stu-id="1ceed-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="1ceed-403">Hallo DC DR Azure-opslag opnieuw kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="1ceed-404">Er is een minimum van twee failovers tijdens de migratie, met uitzondering van testfailovers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="1ceed-405">U moet toomove SQL Server-gegevens met back-up en herstellen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="1ceed-406">Nadelen</span><span class="sxs-lookup"><span data-stu-id="1ceed-406">Disadvantages</span></span>
* <span data-ttu-id="1ceed-407">Afhankelijk van de client toegang tooSQL Server, kunnen er langere latentie als SQL Server wordt uitgevoerd in een alternatieve DC toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ceed-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="1ceed-408">Hallo kopie tijd van VHD's tooPremium opslag kan lang zijn.</span><span class="sxs-lookup"><span data-stu-id="1ceed-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="1ceed-409">Dit kan invloed hebben op uw beslissing op of tookeep Hallo knooppunt in het Hallo-beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="1ceed-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="1ceed-410">U kunt dit wanneer logboek intensieve belasting worden uitgevoerd tijdens de migratie Hallo niets te doen, omdat het primaire knooppunt Hallo tookeep Hallo van niet-gerepliceerde transacties in het transactielogboek.</span><span class="sxs-lookup"><span data-stu-id="1ceed-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="1ceed-411">Daarom kan dit aanzienlijk groeien.</span><span class="sxs-lookup"><span data-stu-id="1ceed-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="1ceed-412">Dit scenario zou gebruiken hello Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is.</span><span class="sxs-lookup"><span data-stu-id="1ceed-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="1ceed-413">Er is geen SLA op voltooiing.</span><span class="sxs-lookup"><span data-stu-id="1ceed-413">There is no SLA on completion.</span></span> <span data-ttu-id="1ceed-414">Hallo tijd Hallo kopieën varieert, terwijl dit afhankelijk van de wachttijd in wachtrij, het is ook afhankelijk van Hallo hoeveelheid gegevens tootransfer.</span><span class="sxs-lookup"><span data-stu-id="1ceed-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="1ceed-415">Daarom alleen hebt u één knooppunt in uw datacenter 2e, u moet treffen risicobeperking geval Hallo kopie langer duurt dan in de testfase.</span><span class="sxs-lookup"><span data-stu-id="1ceed-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="1ceed-416">Dit omvat bijvoorbeeld Hallo ideeën te volgen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="1ceed-417">Een tijdelijke SQL-knooppunt 2e toevoegen voor HA vóór de migratie Hallo overeengekomen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="1ceed-418">Hallo migratie buiten Azure gepland onderhoud worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="1ceed-419">Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="1ceed-420">Dit scenario wordt ervan uitgegaan dat u de installatie hebt gedocumenteerd en weten hoe Hallo opslag is toegewezen in volgorde toomake wijzigingen voor optimale schijf cache-instellingen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="1ceed-421">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="1ceed-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="1ceed-423">Lokale Hallo / alternatieve Azure DC Hallo SQL Server de primaire en maken het Hallo andere automatische Failover Partner (AFP) maken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="1ceed-424">Verzamelen van gegevens over de schijfconfiguratie van SQL2 en verwijderen van het knooppunt hello (gekoppelde VHD's niet verwijderd).</span><span class="sxs-lookup"><span data-stu-id="1ceed-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="1ceed-425">Premium-opslagaccount maken en kopieer VHD's van Hallo Standard-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1ceed-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="1ceed-426">Maak een nieuwe cloudservice en Hallo SQL2 VM maken met de opslag van premies schijven die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="1ceed-427">Configureer ILB / ELB en het toevoegen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="1ceed-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="1ceed-428">Update Hallo altijd op Listener met nieuwe ILB / ELB IP-adres en test failover.</span><span class="sxs-lookup"><span data-stu-id="1ceed-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="1ceed-429">Controleer de Hallo DNS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="1ceed-430">Hallo AFP tooSQL2, wijzigen en migreren van SQL1 en stappen 2 tot en met 5 doorlopen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="1ceed-431">Testfailovers.</span><span class="sxs-lookup"><span data-stu-id="1ceed-431">Test failovers.</span></span>
* <span data-ttu-id="1ceed-432">Ga terug tooSQL1 Hallo AFP en SQL2</span><span class="sxs-lookup"><span data-stu-id="1ceed-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="1ceed-433">Bijlage: Een implementatie voor meerdere locaties altijd op Cluster tooPremium opslag migreren</span><span class="sxs-lookup"><span data-stu-id="1ceed-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="1ceed-434">Hallo rest van dit onderwerp biedt een gedetailleerd voorbeeld van het converteren van een opslag voor meerdere locaties tooPremium altijd aan cluster.</span><span class="sxs-lookup"><span data-stu-id="1ceed-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="1ceed-435">Hallo Listener worden geconverteerd van het gebruik van een externe load balancer (ELB) tooan interne load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="1ceed-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="1ceed-436">Omgeving</span><span class="sxs-lookup"><span data-stu-id="1ceed-436">Environment</span></span>
* <span data-ttu-id="1ceed-437">Windows 2k 12 / SQL 2k 12</span><span class="sxs-lookup"><span data-stu-id="1ceed-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="1ceed-438">Bestanden op SP 1 DB</span><span class="sxs-lookup"><span data-stu-id="1ceed-438">1 DB Files on SP</span></span>
* <span data-ttu-id="1ceed-439">2 x opslaggroepen per knooppunt</span><span class="sxs-lookup"><span data-stu-id="1ceed-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="1ceed-441">VIRTUELE MACHINE:</span><span class="sxs-lookup"><span data-stu-id="1ceed-441">VM:</span></span>
<span data-ttu-id="1ceed-442">In dit voorbeeld gaan we toodemonstrate verplaatsen van een ELB-tooILB.</span><span class="sxs-lookup"><span data-stu-id="1ceed-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="1ceed-443">ELB is beschikbaar voordat ILB, zodat dit ziet u hoe tooswitch toothis tijdens de migratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ceed-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="1ceed-445">Pre-stappen: Verbinding maken met tooSubscription</span><span class="sxs-lookup"><span data-stu-id="1ceed-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="1ceed-446">Stap 1: Nieuw Opslagaccount maken en in de Cloud Service</span><span class="sxs-lookup"><span data-stu-id="1ceed-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="1ceed-447">Stap 2: Toename Hallo fouten toegestaan op resources<Optional></span><span class="sxs-lookup"><span data-stu-id="1ceed-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="1ceed-448">Bepaalde bronnen die deel uitmaken van AlwaysOn-beschikbaarheidsgroep tooyour er gelden beperkingen op hoeveel fouten die in een periode optreden, waarbij Hallo cluster-service het toorestart Hallo resourcegroep probeert.</span><span class="sxs-lookup"><span data-stu-id="1ceed-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="1ceed-449">Het is raadzaam dat u deze verhogen, terwijl u via deze procedure worden roulatie van omdat als u niet handmatig failover en trigger failovers door het afsluiten van computers u sluiten toothis limiet kunt krijgen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="1ceed-450">Deze zou worden voorzichtig toodouble Hallo fout vergoeding toodo dit in Failoverclusterbeheer, gaat u toohello-eigenschappen van Hallo altijd op resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="1ceed-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="1ceed-452">Maximum aantal fouten too6 Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="1ceed-453">Stap 3: Aanvullende IP-adres resource voor de clustergroep<Optional></span><span class="sxs-lookup"><span data-stu-id="1ceed-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="1ceed-454">Als u slechts één IP-adres voor de clustergroep Hallo dit uitgelijnde toohello cloud subnet is, houd er rekening mee, als u per ongeluk offline alle clusterknooppunten in Hallo cloud halen op dat netwerk vervolgens Hallo Cluster-IP-resource en de clusternetwerknaam niet zal kunnen toocome Online.</span><span class="sxs-lookup"><span data-stu-id="1ceed-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="1ceed-455">In Hallo-gebeurtenis van dit wordt voorkomen dat tooother clusterbronnen updates.</span><span class="sxs-lookup"><span data-stu-id="1ceed-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="1ceed-456">Stap 4: DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="1ceed-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="1ceed-457">tooimplement een overgang is afhankelijk van hoe DNS wordt gebruikt en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="1ceed-458">Wanneer altijd op is geïnstalleerd, wordt er een resourcegroep van Windows-Cluster gemaakt als u Failoverclusterbeheer opent, ziet u dat ten minste drie middelen beschikken, Hallo twee die Hallo document verwijst tooare:</span><span class="sxs-lookup"><span data-stu-id="1ceed-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="1ceed-459">Virtuele-netwerknaam (VNN) – Dit is Hallo DNS-naam die client toowhen productiviteitsniveau tooconnect tooSQL Servers via altijd op verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="1ceed-460">Bron van het IP-adres – Dit IP-adres die zijn gekoppeld aan Hallo VNN Hallo is, kunt u meer dan één hebben en in een configuratie voor meerdere sites hebt u een IP-adres per site/subnet.</span><span class="sxs-lookup"><span data-stu-id="1ceed-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="1ceed-461">Wanneer verbindende tooSQL Hallo-stuurprogramma voor SQL Server Client-Server wordt Hallo DNS-records die zijn gekoppeld aan het Hallo-listener ophalen en probeer het tooconnect tooeach altijd aan dat IP-adres is gekoppeld, worden hieronder bespreken we een aantal factoren die van invloed kunnen zijn op dit.</span><span class="sxs-lookup"><span data-stu-id="1ceed-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="1ceed-462">Hallo aantal gelijktijdige DNS-records die gekoppeld aan de naam van de beschikbaarheidsgroeplistener Hallo zijn afhankelijk niet alleen Hallo aantal IP-adressen die zijn gekoppeld, maar Hallo ' RegisterAllIpProviders'setting in Failover Clustering voor Hallo altijd ON VNN resource.</span><span class="sxs-lookup"><span data-stu-id="1ceed-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="1ceed-463">Wanneer u altijd op in Azure implementeert er zijn verschillende stappen toocreate Hallo Listener en IP-adressen, hebt u toomanually Hallo 'RegisterAllIpProviders' too1 configureren, is dit verschillende tooan on-premises altijd op implementatie waarbij too1 is al ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="1ceed-464">Als 'RegisterAllIpProviders' 0 is, klikt u vervolgens ziet alleen u een DNS-record in DNS die zijn gekoppeld aan Hallo Listener:</span><span class="sxs-lookup"><span data-stu-id="1ceed-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="1ceed-466">Als 'RegisterAllIpProviders' 1:</span><span class="sxs-lookup"><span data-stu-id="1ceed-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="1ceed-468">Hallo-code hieronder wordt dump uit Hallo VNN instellingen en voor u ingesteld, neem Opmerking voor Hallo wijzigen tootake effect moet u tootake hello VNN offline en weer online inschakelen, deze nemen Hallo Listener offline veroorzaakt client connectiviteit wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="1ceed-469">In een latere migratiestap van de moet u tooupdate Hallo altijd-listener voor met een bijgewerkte IP-adres dat verwijst naar een load balancer, dient hiervoor een IP-adres resource verwijderen en toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="1ceed-470">Na Hallo IP-update moet u tooensure Hallo nieuwe IP-adres is bijgewerkt in DNS-Zone en het Hallo-clients hun lokale DNS-cache bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="1ceed-471">Als uw clients zich in een ander netwerksegment bevinden en verwijzen naar een andere DNS-server, moet u tooconsider wat gebeurt er over het overdragen van DNS-Zone tijdens de migratie Hallo Hallo toepassing bezorgd tijd zal worden beperkt door ten minste Hallo Zone Transfer tijd een nieuwe IP-adressen voor Hallo listener.</span><span class="sxs-lookup"><span data-stu-id="1ceed-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="1ceed-472">Als u hier tijd-beperking, u moet worden behandeld en testen forceren van een incrementele zoneoverdracht met uw Windows-teams, en ook plaatsen Hallo DNS host record tooa verlagen tijd tooLive (TTL), zodat clients Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1ceed-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="1ceed-473">Zie voor meer informatie [incrementele zoneoverdrachten](https://technet.microsoft.com/library/cc958973.aspx) en [Start DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ceed-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="1ceed-474">Hallo standaard TTL-waarde van de DNS-Record die is gekoppeld aan het Hallo-Listener in altijd op in Azure is 1200 seconden.</span><span class="sxs-lookup"><span data-stu-id="1ceed-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="1ceed-475">U kunt desgewenst tooreduce dit als u tijd beperking tijdens de migratie tooensure Hallo clients update hun DNS met Hallo bijgewerkt IP-adres voor Hallo listener.</span><span class="sxs-lookup"><span data-stu-id="1ceed-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="1ceed-476">U kunt zien en Hallo-configuratie wijzigen door het dumpen van Hallo configuratie Hallo VNN:</span><span class="sxs-lookup"><span data-stu-id="1ceed-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="1ceed-477">Houd er rekening mee, Hallo lagere Hallo 'HostRecordTTL', een hogere mate van DNS-verkeer wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="1ceed-478">Instellingen voor client-toepassing</span><span class="sxs-lookup"><span data-stu-id="1ceed-478">Client application settings</span></span>
<span data-ttu-id="1ceed-479">Als uw SQL-client toepassing ondersteunt Hallo .net 4.5 SQLClient, dan hebt u kunt gebruiken ' MULTISUBNETFAILOVER = TRUE' sleutelwoord, dit wordt aanbevolen toobe toegepast zoals maakt het mogelijk sneller verbinding tooSQL AlwaysOn-beschikbaarheidsgroep tijdens failover.</span><span class="sxs-lookup"><span data-stu-id="1ceed-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="1ceed-480">Het inventariseren via alle IP-adressen die zijn gekoppeld aan Hallo altijd-listener voor parallel en een agressievere TCP opnieuw verbindingssnelheid tijdens een failover uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1ceed-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="1ceed-481">Zie voor meer informatie over Hallo bovenstaande instellingen [MultiSubnetFailover sleutelwoord en functies die zijn gekoppeld](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="1ceed-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="1ceed-482">Zie ook [SqlClient-ondersteuning voor hoge beschikbaarheid, herstel na noodgevallen](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="1ceed-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="1ceed-483">Stap 5: Instellingen van het clusterquorum</span><span class="sxs-lookup"><span data-stu-id="1ceed-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="1ceed-484">Als u toobe duurt uit ten minste één SQL-Server niet actief op een tijdstip gaat, moet u Hallo clusterquorum instelling wijzigen als u File Share Witness (FSW) met 2 knooppunten, moet u Hallo quorum tooallow Knooppuntmeerderheid instellen en gebruikmaken van dynamische stemmen, en dit tooallow voor een permanente tooremain van één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1ceed-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="1ceed-485">Zie voor meer informatie over het beheren en configureren van het clusterquorum Hallo [configureren en beheren Hallo Quorum in een Windows Server 2012-failovercluster](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ceed-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="1ceed-486">Stap 6: Extraheren bestaande eindpunten en ACL 's</span><span class="sxs-lookup"><span data-stu-id="1ceed-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="1ceed-487">Sla deze tooa tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="1ceed-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="1ceed-488">Stap 7: Failoverpartners en replicatie-modi wijzigen</span><span class="sxs-lookup"><span data-stu-id="1ceed-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="1ceed-489">Als u meer dan 2 SQL-Servers hebt, u hoeft Hallo failover van een andere secundaire in een andere domeincontroller te wijzigen of on-premises too'Synchronous en kunt u een Partner voor automatische Failover (AFP), is dit zodat u HA onderhouden terwijl u wijzigingen doorvoert.</span><span class="sxs-lookup"><span data-stu-id="1ceed-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="1ceed-490">U kunt dit doen via TSQL van echter SSMS wijzigen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="1ceed-492">Stap 8: Verwijder secundaire virtuele machine van de cloudservice</span><span class="sxs-lookup"><span data-stu-id="1ceed-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="1ceed-493">U rekening mee moet houden toomigrate een secundair knooppunt cloud als dit momenteel primaire is, moet u eerst een handmatige failover initiëren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="1ceed-494">Stap 9: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan</span><span class="sxs-lookup"><span data-stu-id="1ceed-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="1ceed-495">Voor gegevensvolumes moeten deze tooREADONLY worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="1ceed-496">Voor TLOG volumes moeten deze tooNONE worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="1ceed-498">Stap 10: Kopie VHD 's</span><span class="sxs-lookup"><span data-stu-id="1ceed-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="1ceed-499">U kunt Hallo kopiestatus controleren van Hallo VHD's toohello Premium Storage-account:</span><span class="sxs-lookup"><span data-stu-id="1ceed-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="1ceed-501">Wacht totdat deze worden geregistreerd als geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="1ceed-502">Voor informatie over afzonderlijke blobs:</span><span class="sxs-lookup"><span data-stu-id="1ceed-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="1ceed-503">Stap 11: Register OS-schijf</span><span class="sxs-lookup"><span data-stu-id="1ceed-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="1ceed-504">Stap 12: Secundaire importeren in de nieuwe cloudservice</span><span class="sxs-lookup"><span data-stu-id="1ceed-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="1ceed-505">Hallo-code hieronder ook gebruikt Hallo toegevoegd optie hier u kunt Hallo machine importeren en gebruiken van Hallo retainable VIP.</span><span class="sxs-lookup"><span data-stu-id="1ceed-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="1ceed-506">Stap 13: Maak ILB op nieuwe Cloud Svc toevoegen van Load Balanced eindpunten en ACL's</span><span class="sxs-lookup"><span data-stu-id="1ceed-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="1ceed-507">Stap 14: Altijd bijwerken op</span><span class="sxs-lookup"><span data-stu-id="1ceed-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="1ceed-509">Nu Hallo oude cloudservice IP-adres verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="1ceed-511">Stap 15: DNS-updates controleren</span><span class="sxs-lookup"><span data-stu-id="1ceed-511">Step 15: DNS update check</span></span>
<span data-ttu-id="1ceed-512">U moet nu DNS-Servers in uw SQL Server client netwerken controleren en zorg ervoor dat het clustering Hallo heeft toegevoegd extra hostrecord voor Hallo IP-adres toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="1ceed-513">Als deze DNS-servers niet hebt bijgewerkt, houd rekening met het forceren van een DNS-Zone-overdracht en controleer of hello clients in er subnet zijn kunnen tooresolve tooboth altijd op IP-adressen, dit is dus u hoeft geen toowait voor automatische DNS-replicatie.</span><span class="sxs-lookup"><span data-stu-id="1ceed-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="1ceed-514">Stap 16: Configureer altijd opnieuw op</span><span class="sxs-lookup"><span data-stu-id="1ceed-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="1ceed-515">Op dit moment wachten op Hallo secundaire dat knooppunt die gemigreerde toofully is gesynchroniseerd met de Hallo lokale knooppunt- en switch toosynchronous bestandsreplicatie-knooppunt en kunnen Hallo AFP.</span><span class="sxs-lookup"><span data-stu-id="1ceed-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="1ceed-516">Stap 17: Tweede knooppunt migreren</span><span class="sxs-lookup"><span data-stu-id="1ceed-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="1ceed-517">Stap 18: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan</span><span class="sxs-lookup"><span data-stu-id="1ceed-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="1ceed-518">Voor gegevensvolumes moeten deze tooREADONLY worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="1ceed-519">Voor TLOG volumes moeten deze tooNONE worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ceed-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="1ceed-521">Stap 19: Maak een nieuwe onafhankelijke Storage-Account voor secundair knooppunt</span><span class="sxs-lookup"><span data-stu-id="1ceed-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="1ceed-522">Stap 20: Kopie VHD 's</span><span class="sxs-lookup"><span data-stu-id="1ceed-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="1ceed-523">U kunt Hallo VHD kopiestatus controleren voor alle virtuele harde schijven: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Schijflabel $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="1ceed-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="1ceed-525">Wacht totdat deze worden geregistreerd als geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="1ceed-526">Voor informatie over afzonderlijke blobs:</span><span class="sxs-lookup"><span data-stu-id="1ceed-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="1ceed-527">Stap 21: Register OS-schijf</span><span class="sxs-lookup"><span data-stu-id="1ceed-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="1ceed-528">Stap 22: Toevoegen Load Balanced eindpunten en ACL's</span><span class="sxs-lookup"><span data-stu-id="1ceed-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="1ceed-529">Stap 23: De testfailover</span><span class="sxs-lookup"><span data-stu-id="1ceed-529">Step 23: Test failover</span></span>
<span data-ttu-id="1ceed-530">U moet nu laten Hallo gemigreerde knooppunt worden gesynchroniseerd met de Hallo lokale altijd aan knooppunt, plaatst u het in toosynchronous replicatiemodus en wacht totdat deze is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="1ceed-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="1ceed-531">Vervolgens failover van het eerste knooppunt van on-premises toohello gemigreerd, namelijk Hallo AFP.</span><span class="sxs-lookup"><span data-stu-id="1ceed-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="1ceed-532">Zodra die eerder heeft gewerkt, gemigreerd Hallo wijziging laatste knooppunt toohello AFP.</span><span class="sxs-lookup"><span data-stu-id="1ceed-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="1ceed-533">U moet testfailovers tussen alle knooppunten en hoewel chaos tests tooensure failovers zoals werken verwacht en in een tijdige manor uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1ceed-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="1ceed-534">24 stap: Opnieuw clusterquoruminstellingen zetten / DNS TTL / Failover Pntrs / synchronisatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="1ceed-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="1ceed-535">Toevoegen van de bron van het IP-adres op hetzelfde Subnet</span><span class="sxs-lookup"><span data-stu-id="1ceed-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="1ceed-536">Als u alleen 2 SQL-Servers en toomigrate wilt ze tooa nieuwe cloudservice, maar wilt tookeep op hetzelfde subnet hello, kunt u vermijden Hallo listener altijd offline toodelete Hallo oorspronkelijke op IP-adres en Hallo nieuwe IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1ceed-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="1ceed-537">Als u Hallo VMs tooanother subnet hoeft u niet toodo dit migreert omdat er een extra clusternetwerk dat verwijst naar dat subnet.</span><span class="sxs-lookup"><span data-stu-id="1ceed-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="1ceed-538">Als u hebt gebracht Hallo secundaire gemigreerd en toegevoegd in het nieuwe IP-adres resource Hallo voor nieuwe cloudservice Hallo voordat failover Hallo bestaande primaire, moet u deze stappen binnen Hallo Failover-clusterbeheer nemen:</span><span class="sxs-lookup"><span data-stu-id="1ceed-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="1ceed-539">tooadd in IP-adres, Zie Hallo [bijlage](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), stap 14.</span><span class="sxs-lookup"><span data-stu-id="1ceed-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="1ceed-540">Voor Hallo huidige IP-adres resource wijzigen Hallo mogelijke eigenaar too'Existing primaire SQL-Server', in onderstaande 'dansqlams4' Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1ceed-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="1ceed-542">Voor Hallo nieuwe IP-adres resource wijzigen Hallo mogelijke eigenaar too'Migrated secundaire SQL-Server', in onderstaande 'dansqlams5' Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1ceed-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="1ceed-544">Wanneer deze optie is ingesteld, kunt u failover en wanneer het laatste knooppunt hello wordt gemigreerd Hallo mogelijke eigenaars worden bewerkt zodat dit knooppunt wordt toegevoegd als een mogelijke eigenaar:</span><span class="sxs-lookup"><span data-stu-id="1ceed-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="1ceed-546">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1ceed-546">Additional resources</span></span>
* [<span data-ttu-id="1ceed-547">Azure Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="1ceed-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="1ceed-548">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="1ceed-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="1ceed-549">SQL Server in Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ceed-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
