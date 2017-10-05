---
title: Gebruik Azure Premium-opslag met SQL Server | Microsoft Docs
description: Dit artikel maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel en biedt richtlijnen over het gebruik van Azure Premium-opslag met SQL Server wordt uitgevoerd op Azure Virtual Machines.
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
ms.openlocfilehash: 6790db207fc7ec8a4b1546ef07c97ef30abe9513
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="8af9f-103">Azure Premium Storage gebruiken met SQL Server op Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="8af9f-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="8af9f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8af9f-104">Overview</span></span>
<span data-ttu-id="8af9f-105">[Azure Premium-opslag](../../../storage/common/storage-premium-storage.md) is de volgende generatie van opslag die een lage latentie hoge doorvoersnelheid IO en.</span><span class="sxs-lookup"><span data-stu-id="8af9f-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="8af9f-106">Het meest geschikt is voor belangrijke IO intensieve werkbelastingen, zoals SQL Server op IaaS [virtuele Machines](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="8af9f-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8af9f-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8af9f-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8af9f-108">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8af9f-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8af9f-109">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="8af9f-110">Dit artikel bevat plannen en richtlijnen voor het migreren van een virtuele Machine met SQL Server met Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="8af9f-111">Dit omvat de Azure-infrastructuur (netwerk-, opslag) en Gast Windows VM stappen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="8af9f-112">Het voorbeeld in de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) ziet u een volledige uitgebreide end-to-end-migratie van het verplaatsen van grotere virtuele machines om te profiteren van betere lokale SSD-opslag met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8af9f-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="8af9f-113">Het is belangrijk te weten met Azure Premium-opslag met SQL Server op IAAS VM's van het end-to-end-proces.</span><span class="sxs-lookup"><span data-stu-id="8af9f-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="8af9f-114">Dit omvat:</span><span class="sxs-lookup"><span data-stu-id="8af9f-114">This includes:</span></span>

* <span data-ttu-id="8af9f-115">Identificatie van de vereisten voor het gebruik van Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="8af9f-116">Voorbeelden van de implementatie van SQL Server op IaaS naar Premium-opslag voor nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="8af9f-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="8af9f-117">Voorbeelden van migreren bestaande implementaties, zowel zelfstandige servers en implementaties met behulp van SQL AlwaysOn-beschikbaarheidsgroepen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="8af9f-118">Mogelijke migratie nadert.</span><span class="sxs-lookup"><span data-stu-id="8af9f-118">Possible migration approaches.</span></span>
* <span data-ttu-id="8af9f-119">Volledige end-to-end-voorbeeld is van de stapsgewijze instructies voor de migratie van een bestaande implementatie altijd op Azure, Windows en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8af9f-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="8af9f-120">Zie voor meer achtergrondinformatie op SQL Server in Azure Virtual Machines, [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8af9f-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="8af9f-121">**Auteur:** Daniel Sol **technische controleurs:** Luis Jeroen Vargas haring, Sanjay Mishra, Pravin Mital, Schwertl Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="8af9f-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="8af9f-122">Vereisten voor de Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="8af9f-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="8af9f-123">Er zijn verschillende vereisten voor het gebruik van Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="8af9f-124">Grootte van de machine</span><span class="sxs-lookup"><span data-stu-id="8af9f-124">Machine size</span></span>
<span data-ttu-id="8af9f-125">U moet DS-serie virtuele Machines (VM) gebruiken voor het gebruik van Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="8af9f-126">Als u DS-serie machines niet in uw cloudservice voordat u hebt gebruikt, moet u de bestaande virtuele machine verwijderen, houden van de gekoppelde schijven en vervolgens een nieuwe cloudservice maken vóór het opnieuw maken van de virtuele machine als de grootte van de rol DS *.</span><span class="sxs-lookup"><span data-stu-id="8af9f-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS* role size.</span></span> <span data-ttu-id="8af9f-127">Zie voor meer informatie over grootten van virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8af9f-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="8af9f-128">Cloud services</span><span class="sxs-lookup"><span data-stu-id="8af9f-128">Cloud services</span></span>
<span data-ttu-id="8af9f-129">U kunt alleen virtuele machines DS * met Premium-opslag gebruiken wanneer ze worden gemaakt in een nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8af9f-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="8af9f-130">Als u SQL Server Always On in Azure, wordt het altijd-Listener voor verwijzen naar het Azure interne of externe Load Balancer-IP-adres dat is gekoppeld aan een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8af9f-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="8af9f-131">Dit artikel is gericht op het migreren van behoud van beschikbaarheid in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8af9f-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-132">Een reeks DS * moet de eerste virtuele machine die wordt geïmplementeerd naar de nieuwe Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="8af9f-132">A DS* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="8af9f-133">Regionaal vnet 's</span><span class="sxs-lookup"><span data-stu-id="8af9f-133">Regional VNETS</span></span>
<span data-ttu-id="8af9f-134">U moet het virtuele netwerk (VNET) die als host fungeert voor uw virtuele machines worden regionale configureren voor virtuele machines DS *.</span><span class="sxs-lookup"><span data-stu-id="8af9f-134">For DS* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="8af9f-135">Dit 'genereren' in het VNET om toe te staan de grotere virtuele machines kunnen worden ingericht in andere clusters en toestaan dat communicatie ertussen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="8af9f-136">In de volgende schermafbeelding ziet u de gemarkeerde locatie regionaal vnet's, terwijl het eerste resultaat een 'smalle' VNET toont.</span><span class="sxs-lookup"><span data-stu-id="8af9f-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="8af9f-138">U kunt een Microsoft-ondersteuningsticket om te migreren naar een regionaal VNET verhogen, Microsoft wordt een wijziging aanbrengt en klik vervolgens op voor het voltooien van de migratie naar een regionaal vnet's, de eigenschap AffinityGroup in de netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="8af9f-139">De netwerkconfiguratie in PowerShell eerst te exporteren en vervang de **AffinityGroup** eigenschap in de **VirtualNetworkSite** element met een **locatie** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8af9f-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="8af9f-140">Geef `Location = XXXX` waar `XXXX` is een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="8af9f-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="8af9f-141">De nieuwe configuratie importeren.</span><span class="sxs-lookup"><span data-stu-id="8af9f-141">Then import the new configuration.</span></span>

<span data-ttu-id="8af9f-142">Bijvoorbeeld, overweegt de volgende VNET-configuratie:</span><span class="sxs-lookup"><span data-stu-id="8af9f-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="8af9f-143">Als u wilt dit verplaatsen naar een regionaal VNET in West-Europa, de configuratie te wijzigen met het volgende:</span><span class="sxs-lookup"><span data-stu-id="8af9f-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="8af9f-144">Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="8af9f-144">Storage accounts</span></span>
<span data-ttu-id="8af9f-145">U moet een nieuw opslagaccount die is geconfigureerd voor Premium-opslag maken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="8af9f-146">Houd er rekening mee dat het gebruik van Premium-opslag is ingesteld op het opslagaccount niet op afzonderlijke VHD's, maar bij gebruik van een DS * reeks VM u de VHD van Premium en Standard-opslag-accounts koppelen kunt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="8af9f-147">U kunt dit overwegen als u niet wilt dat de OS-VHD doorsturen naar de Premium-opslagaccount plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="8af9f-148">De volgende **nieuw AzureStorageAccountPowerShell** opdracht met de 'Premium_LRS' **Type** maakt een Premium-Opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="8af9f-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="8af9f-149">Cache-instellingen voor virtuele harde schijven</span><span class="sxs-lookup"><span data-stu-id="8af9f-149">VHDs Cache Settings</span></span>
<span data-ttu-id="8af9f-150">Het belangrijkste verschil tussen het maken van schijven die deel van een Premium Storage-account uitmaken is de schijfcache-instelling.</span><span class="sxs-lookup"><span data-stu-id="8af9f-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="8af9f-151">Voor SQL Server-gegevens volume het schijven wordt aanbevolen dat u '**Lees-Caching**'.</span><span class="sxs-lookup"><span data-stu-id="8af9f-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="8af9f-152">Voor transactie logboekvolumes, de schijfcache-instelling moet worden ingesteld op '**geen**'.</span><span class="sxs-lookup"><span data-stu-id="8af9f-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="8af9f-153">Dit wijkt af van de aanbevelingen voor Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="8af9f-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="8af9f-154">Zodra de VHD's zijn gekoppeld, kan de cache-instelling kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="8af9f-155">U moet ontkoppelen en opnieuw koppelen van de VHD met een bijgewerkte cache-instelling.</span><span class="sxs-lookup"><span data-stu-id="8af9f-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="8af9f-156">Windows-opslagruimten</span><span class="sxs-lookup"><span data-stu-id="8af9f-156">Windows storage spaces</span></span>
<span data-ttu-id="8af9f-157">U kunt [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) zoals u deed met vorige Standard-opslag, Hierdoor kunt u voor het migreren van een virtuele machine die wordt al gebruikt door opslagruimten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="8af9f-158">Het voorbeeld in [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (stap 9 en voorwaarts) ziet u de Powershell-code voor het uitpakken en importeren van een virtuele machine met meerdere gekoppelde VHD's.</span><span class="sxs-lookup"><span data-stu-id="8af9f-158">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="8af9f-159">Opslaggroepen zijn gebruikt met standaard Azure storage-account om de doorvoer te verbeteren en de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="8af9f-160">Wellicht waarde in nieuwe implementaties het testen van opslaggroepen met Premium-opslag, maar ze extra complexiteit met setup opslag toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="8af9f-161">Welke virtuele Azure-schijven zijn toegewezen aan opslaggroepen zoeken</span><span class="sxs-lookup"><span data-stu-id="8af9f-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="8af9f-162">Als er verschillende cache-instelling aanbevelingen voor het gekoppelde VHD's zijn, moet u besluiten de VHD's kopiëren naar een Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="8af9f-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="8af9f-163">Echter, wanneer u opnieuw aan de nieuwe virtuele machine van de DS-serie koppelen, mogelijk moet u voor het wijzigen van de cache-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="8af9f-164">Het is eenvoudiger om toe te passen de Premium-opslag aanbevolen cache-instellingen wanneer u afzonderlijke VHD's voor de SQL-gegevensbestanden en logboekbestanden (eerder dan een enkele VHD met zowel) bevatten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-165">Als u SQL Server-gegevens en logboekbestanden bestanden op hetzelfde volume hebt, afhankelijk van de cache in optie die u kiest de i/o-toegangspatronen voor de werkbelasting van uw database.</span><span class="sxs-lookup"><span data-stu-id="8af9f-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="8af9f-166">Alleen testen kunt laten zien welke cache-instelling wordt aanbevolen voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8af9f-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="8af9f-167">Als u gebruikmaakt van Windows Storage Spaces die bestaan uit meerdere VHD's moet u kijken naar uw oorspronkelijke scripts te identificeren die gekoppeld VHD's zijn echter in welke specifieke groep, dus vervolgens stelt u de cache-instellingen dienovereenkomstig voor elke schijf.</span><span class="sxs-lookup"><span data-stu-id="8af9f-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="8af9f-168">Als u geen oorspronkelijke script beschikbaar om weer te geven die VHD's zijn toegewezen aan de opslaggroep, kunt u de volgende stappen uit om te bepalen van de toewijzing van schijfopslag/groep.</span><span class="sxs-lookup"><span data-stu-id="8af9f-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="8af9f-169">Gebruik de volgende stappen uit voor elke schijf:</span><span class="sxs-lookup"><span data-stu-id="8af9f-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="8af9f-170">Haal de lijst met schijven die zijn gekoppeld aan VM met de **Get-AzureVM** opdracht:</span><span class="sxs-lookup"><span data-stu-id="8af9f-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="8af9f-171">Get-AzureVM - ServiceName <servicename> -naam <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="8af9f-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="8af9f-172">Noteer de Diskname en LUN.</span><span class="sxs-lookup"><span data-stu-id="8af9f-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="8af9f-174">Extern bureaublad in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8af9f-174">Remote desktop into the VM.</span></span> <span data-ttu-id="8af9f-175">Ga vervolgens naar **Computerbeheer** | **Apparaatbeheer** | **schijfstations**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="8af9f-176">Bekijk de eigenschappen van elk van de 'Microsoft virtuele schijven'</span><span class="sxs-lookup"><span data-stu-id="8af9f-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="8af9f-178">Hier het nummer van de LUN is een verwijzing naar het LUN-nummer dat u opgeeft bij het toevoegen van de VHD naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8af9f-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="8af9f-179">Voor de 'Microsoft virtuele schijf, gaat u naar de **Details** tabblad en klik dan in de **eigenschap** lijst, gaat u naar **stuurprogrammasleutel**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="8af9f-180">In de **waarde**, Opmerking de **Offset**, namelijk 0002 in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="8af9f-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="8af9f-181">De 0002 geeft aan dat de PhysicalDisk2 die de opslaggroep naar verwijst.</span><span class="sxs-lookup"><span data-stu-id="8af9f-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="8af9f-183">Voor elke opslaggroep dump uit de gekoppelde schijven:</span><span class="sxs-lookup"><span data-stu-id="8af9f-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="8af9f-184">Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="8af9f-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="8af9f-186">Nu kunt u deze informatie om te koppelen virtuele harde schijven gekoppeld aan fysieke schijven in opslaggroepen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="8af9f-187">Wanneer u de VHD's aan de fysieke schijven in opslaggroepen vervolgens loskoppelen en kopieer deze naar een Premium Storage-account toegewezen hebt via, koppelt u ze met de juiste cache-instelling.</span><span class="sxs-lookup"><span data-stu-id="8af9f-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="8af9f-188">Zie het voorbeeld in de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), stappen 8 tot en met 12.</span><span class="sxs-lookup"><span data-stu-id="8af9f-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="8af9f-189">Deze stappen laten zien hoe een schijfconfiguratie VHD VM gekoppeld aan een CSV-bestand uitpakken, kopieert u de VHD's, wijzigen van de schijf configuratie cache-instellingen en ten slotte de virtuele machine opnieuw te implementeren als een reeks DS VM met alle gekoppelde schijven.</span><span class="sxs-lookup"><span data-stu-id="8af9f-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="8af9f-190">VM-opslag bandbreedte en opslagdoorvoer VHD</span><span class="sxs-lookup"><span data-stu-id="8af9f-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="8af9f-191">Het bedrag van de prestaties van de opslag, is afhankelijk van de DS * VM-grootte die is opgegeven en de grootte van de VHD.</span><span class="sxs-lookup"><span data-stu-id="8af9f-191">The amount of storage performance depends on the DS* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="8af9f-192">De virtuele machines hebben verschillende rechten voor het aantal virtuele harde schijven die kunnen worden gekoppeld en de maximale bandbreedte (MB/s) wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8af9f-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="8af9f-193">Zie voor de getallen specifieke bandbreedte [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8af9f-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="8af9f-194">Verbeterde IOPS worden verkregen met grotere schijf.</span><span class="sxs-lookup"><span data-stu-id="8af9f-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="8af9f-195">Dit moet u overwegen wanneer u over het migratiepad voor de nadenkt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="8af9f-196">Voor meer informatie [Zie de tabel voor IOPS en schijftypen](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="8af9f-196">For details, [see the table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="8af9f-197">Overweeg tot slot dat virtuele machines hebben verschillende maximale schijf-bandbreedten die wordt ondersteund voor alle schijven die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8af9f-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="8af9f-198">U kunt de maximale schijf-bandbreedte die beschikbaar zijn voor de grootte van die VM-rol kan verzadigen onder hoge belasting.</span><span class="sxs-lookup"><span data-stu-id="8af9f-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="8af9f-199">Bijvoorbeeld ondersteunt een Standard_DS14 maximaal 512 MB/s; Daarom kan u de bandbreedte van de schijf van de virtuele machine verzadigen met drie P30 schijven.</span><span class="sxs-lookup"><span data-stu-id="8af9f-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="8af9f-200">Maar in dit voorbeeld wordt de doorvoer kan worden overschreden, afhankelijk van de combinatie van lees- en IOs.</span><span class="sxs-lookup"><span data-stu-id="8af9f-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="8af9f-201">Nieuwe implementaties</span><span class="sxs-lookup"><span data-stu-id="8af9f-201">New deployments</span></span>
<span data-ttu-id="8af9f-202">De volgende twee secties laten zien hoe u SQL Server-VM's kunt implementeren naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="8af9f-203">Zoals al eerder vermeld, wilt u niet per se plaatsen van de schijf met het besturingssysteem naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="8af9f-204">U kunt kiezen om dit te doen als u wilde een intensieve i/o-werkbelastingen op de VHD OS plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="8af9f-205">Het eerste voorbeeld laat zien met behulp van de bestaande Azure-galerie met installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="8af9f-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="8af9f-206">Het tweede voorbeeld toont hoe u een aangepaste VM-installatiekopie die u in een bestaand Standard-opslag-account hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-207">Deze voorbeelden wordt ervan uitgegaan dat u al een regionaal VNET hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="8af9f-208">Maak een nieuwe virtuele machine met Premium-opslag met afbeelding</span><span class="sxs-lookup"><span data-stu-id="8af9f-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="8af9f-209">Het volgende voorbeeld laat zien hoe u plaatst de OS-VHD naar premium-opslag en Premium-opslag-VHD's koppelen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="8af9f-210">U kunt echter ook de OS-schijf in een Standard-opslagaccount plaatsen en vervolgens VHD's die zich in een Premium Storage-account bevinden koppelen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="8af9f-211">Beide scenario's worden uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="8af9f-212">Stap 1: Een Premium Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="8af9f-213">Stap 2: Maak een nieuwe Cloudservice</span><span class="sxs-lookup"><span data-stu-id="8af9f-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="8af9f-214">Stap 3: Gereserveerd VIP van de Cloud-Service (optioneel)</span><span class="sxs-lookup"><span data-stu-id="8af9f-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="8af9f-215">Stap 4: Een VM-Container maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="8af9f-216">Stap 5: Brengen OS VHD Standard of Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="8af9f-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="8af9f-217">Stap 6: Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

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


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="8af9f-218">Een nieuwe virtuele machine voor het gebruik van Premium-opslag met een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="8af9f-219">Dit scenario laat zien waar u de bestaande aangepaste installatiekopieën die zich in een Standard-opslag-account bevinden hebt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="8af9f-220">Zoals vermeld als u wilt de OS-VHD op Premium-opslag plaatsen, moet u kopiëren van de installatiekopie die voorkomt in de Standard-opslagaccount en dragen deze naar een Premium-opslag voordat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="8af9f-221">Als u een installatiekopie van een lokale, kunt u deze methode ook gebruiken om te kopiëren die rechtstreeks aan de Premium-opslag-account.</span><span class="sxs-lookup"><span data-stu-id="8af9f-221">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="8af9f-222">Stap 1: De Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="8af9f-223">Stap 2-Cloudservice maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="8af9f-224">Stap 3: Een bestaande installatiekopie gebruiken</span><span class="sxs-lookup"><span data-stu-id="8af9f-224">Step 3: Use existing image</span></span>
<span data-ttu-id="8af9f-225">U kunt een bestaande installatiekopie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-225">You can use an existing image.</span></span> <span data-ttu-id="8af9f-226">U kunt [nemen van een installatiekopie van een bestaande machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8af9f-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="8af9f-227">Let op de machine installatiekopie u niet hoeft te worden DS * machine.</span><span class="sxs-lookup"><span data-stu-id="8af9f-227">Note the machine you image does not have to be DS* machine.</span></span> <span data-ttu-id="8af9f-228">Zodra u de installatiekopie hebt, de volgende stappen laten zien hoe dit te kopiëren naar de Premium-opslag-account met de **Start AzureStorageBlobCopy** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8af9f-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="8af9f-229">Stap 4: Kopieer Blob tussen Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="8af9f-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="8af9f-230">Stap 5: Controleer regelmatig de status van het exemplaar:</span><span class="sxs-lookup"><span data-stu-id="8af9f-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="8af9f-231">Stap 6: Installatiekopie schijf toevoegen aan de schijf van Azure-opslagplaats in abonnement</span><span class="sxs-lookup"><span data-stu-id="8af9f-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="8af9f-232">Kan het gebeuren dat hoewel de statusrapporten als geslaagd u kan nog steeds een schijffout lease.</span><span class="sxs-lookup"><span data-stu-id="8af9f-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="8af9f-233">In dit geval wacht tien minuten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="8af9f-234">Stap 7: De virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="8af9f-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="8af9f-235">U maakt hier de virtuele machine van uw installatiekopie en twee Premium-opslag-VHD's koppelen:</span><span class="sxs-lookup"><span data-stu-id="8af9f-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="8af9f-236">Bestaande implementaties die altijd op beschikbaarheidsgroepen niet wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="8af9f-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="8af9f-237">Voor bestaande implementaties raadpleegt u eerst de [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8af9f-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="8af9f-238">Er zijn verschillende overwegingen voor implementaties van SQL Server die niet altijd op beschikbaarheidsgroepen en programma's die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="8af9f-239">Als u altijd op niet gebruikt en een bestaande zelfstandige SQL Server hebt, kunt u upgraden naar de Premium-opslag met behulp van een nieuw cloud service- en storage-account.</span><span class="sxs-lookup"><span data-stu-id="8af9f-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="8af9f-240">Houd rekening met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="8af9f-240">Consider the following options:</span></span>

* <span data-ttu-id="8af9f-241">**Maak een nieuwe SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="8af9f-242">U kunt een nieuwe versie van SQL Server VM die gebruikmaakt van een Premium-opslagaccount maken, zoals beschreven in nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="8af9f-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="8af9f-243">Vervolgens back-up en herstel van SQL Server-configuratie- en databases.</span><span class="sxs-lookup"><span data-stu-id="8af9f-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="8af9f-244">De toepassing moet worden bijgewerkt om te verwijzen naar de nieuwe SQL-Server als intern of extern wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8af9f-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="8af9f-245">U moet alle objecten voor buiten-db' kopiëren als je bezig een gelijktijdige (SxS) SQL Server-migratie was mee.</span><span class="sxs-lookup"><span data-stu-id="8af9f-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="8af9f-246">Dit omvat objecten, zoals aanmeldingen, certificaten en gekoppelde servers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="8af9f-247">**Migreren van een bestaande SQL Server VM**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="8af9f-248">Hiervoor moet de virtuele machine van SQL Server offline moet worden gezet en u deze overbrengt naar een nieuwe cloudservice, waaronder alle van de gekoppelde VHD's te kopiëren naar de Premium-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8af9f-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="8af9f-249">Wanneer de virtuele machine online wordt gezet, wordt de naam van de server-host als voordat verwijzen naar de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8af9f-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="8af9f-250">Let erop dat de grootte van de bestaande schijf invloed is op de prestatiekenmerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="8af9f-251">Bijvoorbeeld een schijf 400 GB opgehaald naar boven afgerond op een P20.</span><span class="sxs-lookup"><span data-stu-id="8af9f-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="8af9f-252">Als u weet dat u niet nodig hebt die schijfprestaties kan u opnieuw de virtuele machine als een reeks DS VM maken en koppelen van Premium Storage VHD's van de grootte van/prestatiegebeurtenissen-specificatie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="8af9f-253">Vervolgens kan loskoppelen en koppelt u de bestanden van de SQL-database opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8af9f-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-254">Wanneer welk type opslagschijf Premium kopiëren van de VHD-schijven die u moet rekening houden met de grootte, afhankelijk van de grootte betekent dat ze vallen, dit schijf prestaties specificatie bepaalt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="8af9f-255">Azure worden afgerond op het dichtstbijzijnde schijf grootte, dus als er een schijf 400 GB, dit wordt afgerond op een P20.</span><span class="sxs-lookup"><span data-stu-id="8af9f-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="8af9f-256">Afhankelijk van uw bestaande i/o-vereisten van de OS-VHD moet u mogelijk niet dit migreren naar een Premium Storage-account.</span><span class="sxs-lookup"><span data-stu-id="8af9f-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="8af9f-257">Als uw SQL-Server extern is geopend, wordt het VIP van cloud service wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="8af9f-258">Er wordt ook zijn update eindpunten, ACL's en DNS-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="8af9f-259">Bestaande implementaties die gebruikmaken van altijd op beschikbaarheidsgroepen</span><span class="sxs-lookup"><span data-stu-id="8af9f-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="8af9f-260">Voor bestaande implementaties raadpleegt u eerst de [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8af9f-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="8af9f-261">In eerste instantie in dit gedeelte kijken we altijd op de interactie met Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="8af9f-262">We vervolgens migraties in twee scenario's wordt opsplitsen: waar u enige uitvaltijd kan verdragen migraties en migraties waar u de minimale downtime moet bereiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="8af9f-263">Lokale SQL Server AlwaysOn-beschikbaarheidsgroepen gebruiken een Listener op lokale waarmee een virtuele DNS-naam samen met een IP-adres dat wordt gedeeld tussen een of meer SQL-Servers geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="8af9f-264">Wanneer clients verbinding maken ze doorgestuurd via de listener-IP voor de primaire SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="8af9f-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="8af9f-265">Dit is de server die eigenaar is van de altijd op IP-resource op dat moment.</span><span class="sxs-lookup"><span data-stu-id="8af9f-265">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways op][6]

<span data-ttu-id="8af9f-267">In Microsoft Azure die kunt u slechts één IP-adres is toegewezen aan een NIC op de virtuele machine hebt, dus het oog op dezelfde laag van abstractie als on-premises Azure maakt gebruik van het IP-adres dat is toegewezen aan de interne of externe Load Balancers (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="8af9f-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="8af9f-268">De IP-resource die wordt gedeeld tussen de servers is ingesteld op het hetzelfde IP-adres als de ILB-/ ELB.</span><span class="sxs-lookup"><span data-stu-id="8af9f-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="8af9f-269">Dit is gepubliceerd in de DNS-server en clientverkeer via de ILB-/ ELB wordt doorgegeven aan de primaire SQL Server-replica.</span><span class="sxs-lookup"><span data-stu-id="8af9f-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="8af9f-270">De ILB-/ ELB kent die SQL Server is de primaire omdat deze tests gebruikt voor de resource altijd op IP-test.</span><span class="sxs-lookup"><span data-stu-id="8af9f-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="8af9f-271">Deze tests op elk knooppunt dat een waarnaar wordt verwezen door de ELB/ILB-eindpunt is in het vorige voorbeeld, afhankelijk van wat reageert, wordt de primaire SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="8af9f-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-272">De ILB en ELB zijn beide toegewezen aan een bepaald Azure-cloudservice, dus cloudmigratie in Azure waarschijnlijk betekent dat dat het IP-adres van Load Balancer wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="8af9f-273">Migreren altijd op implementaties die enige downtime kunnen toestaan</span><span class="sxs-lookup"><span data-stu-id="8af9f-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="8af9f-274">Er zijn twee strategieën voor het migreren van altijd op implementaties die voor enige downtime toestaan:</span><span class="sxs-lookup"><span data-stu-id="8af9f-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="8af9f-275">**Meer secundaire replica's toevoegen aan een bestaand altijd op Cluster**</span><span class="sxs-lookup"><span data-stu-id="8af9f-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="8af9f-276">**Migreren naar een nieuwe altijd op Cluster**</span><span class="sxs-lookup"><span data-stu-id="8af9f-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="8af9f-277">1. Meer secundaire replica's toevoegen aan een bestaand altijd op Cluster</span><span class="sxs-lookup"><span data-stu-id="8af9f-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="8af9f-278">Er is een strategie voor een meer secundaire databases toevoegen aan de AlwaysOn-beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="8af9f-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="8af9f-279">U moet deze in een nieuwe cloudservice toevoegen en bijwerken van de listener met de nieuwe load balancer IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8af9f-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="8af9f-280">De punten van downtime:</span><span class="sxs-lookup"><span data-stu-id="8af9f-280">Points of downtime:</span></span>
* <span data-ttu-id="8af9f-281">Clustervalidatie van het.</span><span class="sxs-lookup"><span data-stu-id="8af9f-281">Cluster Validation.</span></span>
* <span data-ttu-id="8af9f-282">Always On failover testen voor de nieuwe secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="8af9f-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="8af9f-283">Als u Windows-opslaggroepen vanuit de virtuele machine voor een hogere i/o-doorvoer en vervolgens deze zal offline worden gehaald tijdens een volledige validatie van de Cluster.</span><span class="sxs-lookup"><span data-stu-id="8af9f-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="8af9f-284">De validatietest is vereist als u knooppunten aan het cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="8af9f-285">De tijd die nodig is voor het uitvoeren van de test kan variëren, dus moet u dit in uw testomgeving om op te halen bij benadering de tijd van hoe lang dit gaat testen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="8af9f-286">U moet inrichten tijd waar u handmatige failover en chaos testen op de zojuist toegevoegde knooppunten uitvoeren kunt om ervoor te zorgen altijd op hoge beschikbaarheid functies zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="8af9f-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="8af9f-288">Alle exemplaren van SQL Server waar de opslaggroepen worden gebruikt moet worden gestopt voordat de validatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="8af9f-289">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="8af9f-289">High-level steps</span></span>
>

1. <span data-ttu-id="8af9f-290">Maak twee nieuwe SQL-Servers in de nieuwe cloudservice met gekoppelde Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="8af9f-291">Kopiëren via volledige back-ups en herstellen met **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="8af9f-292">Kopiëren via 'buiten user DB' afhankelijke objecten, zoals aanmeldingen enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8af9f-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="8af9f-293">Maken van nieuwe een nieuwe interne Load Balancer (ILB) of gebruik een externe Load Balancer (ELB) en vervolgens Load Balanced eindpunten instellen op beide nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8af9f-294">Controleer dat alle knooppunten de eindpuntconfiguratie juist hebt voordat u doorgaat</span><span class="sxs-lookup"><span data-stu-id="8af9f-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="8af9f-295">Stop de toepassing/gebruiker toegang tot de SQL-Server (als u de opslaggroepen).</span><span class="sxs-lookup"><span data-stu-id="8af9f-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="8af9f-296">SQL Server-Engine-Services stoppen op alle knooppunten (als u de opslaggroepen).</span><span class="sxs-lookup"><span data-stu-id="8af9f-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="8af9f-297">Toevoegen van nieuwe knooppunten om te clusteren en volledige validatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="8af9f-298">Wanneer validatie voltooid is, start u alle SQL Server-Services.</span><span class="sxs-lookup"><span data-stu-id="8af9f-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="8af9f-299">Transactielogboeken back-up en herstel van gebruikersdatabases.</span><span class="sxs-lookup"><span data-stu-id="8af9f-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="8af9f-300">Nieuwe knooppunten toevoegen aan de AlwaysOn-beschikbaarheidsgroep en replicatie in plaats **synchroon**.</span><span class="sxs-lookup"><span data-stu-id="8af9f-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="8af9f-301">De bron van de IP-adres van de nieuwe Cloud Service ILB-/ ELB via PowerShell toevoegen voor altijd op op basis van het voorbeeld van meerdere sites in de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="8af9f-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="8af9f-302">In het Windows-clustering, stelt u de **mogelijke eigenaars** van de **IP-adres** resource toe aan de nieuwe knooppunten oude.</span><span class="sxs-lookup"><span data-stu-id="8af9f-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="8af9f-303">Zie de sectie 'Toe te voegen IP-adres Resource op hetzelfde Subnet' van de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="8af9f-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="8af9f-304">Failover naar een van de nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="8af9f-305">Controleer de nieuwe knooppunten automatisch Failoverpartners en test failovers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="8af9f-306">Oorspronkelijke knooppunten verwijderen uit de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="8af9f-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="8af9f-307">Voordelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-307">Advantages</span></span>
* <span data-ttu-id="8af9f-308">Nieuwe SQL-Servers kunnen worden getest (SQL Server en toepassing) voordat ze worden toegevoegd aan altijd op.</span><span class="sxs-lookup"><span data-stu-id="8af9f-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="8af9f-309">U kunt de VM-grootte wijzigen en aanpassen van de opslag voor uw exacte vereisten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="8af9f-310">Het normaal zou zijn echter handig zijn om alle SQL-bestandspaden hetzelfde blijven.</span><span class="sxs-lookup"><span data-stu-id="8af9f-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="8af9f-311">U kunt bepalen wanneer de overdracht van de database back-ups naar de secundaire replica's worden gestart.</span><span class="sxs-lookup"><span data-stu-id="8af9f-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="8af9f-312">Dit wijkt af van het gebruik van Azure **Start AzureStorageBlobCopy** commandlet kopiëren VHD's, omdat die een asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="8af9f-313">Nadelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-313">Disadvantages</span></span>
* <span data-ttu-id="8af9f-314">Wanneer met behulp van Windows-opslaggroepen, is dit Cluster uitvaltijd tijdens de validatie van het volledige Cluster voor de nieuwe extra knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="8af9f-315">Afhankelijk van de versie van SQL Server en het bestaande aantal secundaire replica's, kunnen mogelijk niet meer secundaire replica's toevoegen zonder te verwijderen van bestaande secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="8af9f-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="8af9f-316">Kan er lang SQL gegevens overdrachtstijd tijdens het instellen van de secundaire replica's zijn.</span><span class="sxs-lookup"><span data-stu-id="8af9f-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="8af9f-317">Er is extra kosten tijdens de migratie terwijl u nieuwe machines parallelle uitvoering zijn.</span><span class="sxs-lookup"><span data-stu-id="8af9f-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="8af9f-318">2. Migreren naar een nieuwe altijd op Cluster</span><span class="sxs-lookup"><span data-stu-id="8af9f-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="8af9f-319">Een andere strategie is een geheel nieuwe altijd op Cluster maken met de nieuwe knooppunten in een nieuwe cloudservice en leid de clients om dit te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="8af9f-320">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="8af9f-320">Points of downtime</span></span>
<span data-ttu-id="8af9f-321">Er is uitvaltijd wanneer u toepassingen en gebruikers overdraagt naar de nieuwe listener altijd op.</span><span class="sxs-lookup"><span data-stu-id="8af9f-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="8af9f-322">Afhankelijk van de uitvaltijd:</span><span class="sxs-lookup"><span data-stu-id="8af9f-322">The downtime depends on:</span></span>

* <span data-ttu-id="8af9f-323">De tijd laatste transactielogboekback-ups terugzetten naar databases op nieuwe servers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="8af9f-324">De tijd die nodig is voor het bijwerken van de clienttoepassingen kunnen gebruikmaken van nieuwe listener altijd op.</span><span class="sxs-lookup"><span data-stu-id="8af9f-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="8af9f-325">Voordelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-325">Advantages</span></span>
* <span data-ttu-id="8af9f-326">U kunt de werkelijke productieomgeving, SQL Server, testen en OS-build-wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="8af9f-327">U hebt de optie voor het aanpassen van de opslag en grootte van virtuele machine mogelijk te verminderen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="8af9f-328">Dit kan leiden tot kosten te beperken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="8af9f-329">Tijdens dit proces kunt u uw versie van SQL Server of een versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="8af9f-330">U kunt ook het besturingssysteem bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="8af9f-331">Het vorige altijd op Cluster kan fungeren als een doel effen terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="8af9f-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="8af9f-332">Nadelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-332">Disadvantages</span></span>
* <span data-ttu-id="8af9f-333">U moet de DNS-naam van de listener wijzigen als u wilt dat beide AlwaysOn-clusters die tegelijkertijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="8af9f-334">Beheer overhead tijdens de migratie wordt toegevoegd als client toepassing tekenreeksen moeten overeenstemming met de naam van de nieuwe Listener.</span><span class="sxs-lookup"><span data-stu-id="8af9f-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="8af9f-335">U moet een mechanisme voor synchronisatie tussen de twee omgevingen te houden zo dicht mogelijk bij de laatste synchronisatievereisten voor de migratie minimaliseren implementeren.</span><span class="sxs-lookup"><span data-stu-id="8af9f-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="8af9f-336">Er is toegevoegd kosten tijdens de migratie als u de nieuwe omgeving uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="8af9f-337">Migreren altijd op implementaties voor minimale downtime</span><span class="sxs-lookup"><span data-stu-id="8af9f-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="8af9f-338">Er zijn twee strategieën voor het migreren altijd op implementaties voor minimale downtime:</span><span class="sxs-lookup"><span data-stu-id="8af9f-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="8af9f-339">**Gebruikmaken van een bestaande secundaire: één Site**</span><span class="sxs-lookup"><span data-stu-id="8af9f-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="8af9f-340">**Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties**</span><span class="sxs-lookup"><span data-stu-id="8af9f-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="8af9f-341">1. Gebruikmaken van een bestaande secundaire: één Site</span><span class="sxs-lookup"><span data-stu-id="8af9f-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="8af9f-342">Een strategie voor minimale downtime is een bestaande cloud secundaire nemen en te verwijderen uit de huidige cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8af9f-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="8af9f-343">Vervolgens de VHD's kopiëren naar het nieuwe account voor de Premium-opslag en de virtuele machine in de nieuwe cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="8af9f-344">Werk vervolgens de listener in clustering en failover.</span><span class="sxs-lookup"><span data-stu-id="8af9f-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="8af9f-345">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="8af9f-345">Points of downtime</span></span>
* <span data-ttu-id="8af9f-346">Er is uitvaltijd wanneer u het laatste knooppunt met het eindpunt met gelijke taakverdeling bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="8af9f-347">Opnieuw verbinden met uw client mogelijk afhankelijk van de client en DNS-configuratie worden uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="8af9f-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="8af9f-348">Er is extra uitvaltijd als u de altijd op clustergroep offline nemen wilt om het wisselen van de IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="8af9f-349">U kunt dit vermijden met behulp van een afhankelijkheid of en mogelijke eigenaars voor de toegevoegde IP-adres-resource.</span><span class="sxs-lookup"><span data-stu-id="8af9f-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="8af9f-350">Zie de sectie 'Toe te voegen IP-adres Resource op hetzelfde Subnet' van de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="8af9f-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="8af9f-351">Wanneer u wilt dat de toegevoegde knooppunt partake in als altijd op Failover-Partner, moet u een Azure-eindpunt met een verwijzing naar de Load Balanced Set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="8af9f-352">Bij het uitvoeren van de **toevoegen AzureEndpoint** opdracht om dit te doen, huidige verbindingen in stand moeten blijven, maar nieuwe verbindingen met de listener kan niet worden vastgesteld totdat de load balancer is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="8af9f-353">In dit testen is gezien naar de laatste 90-120seconds dit moet worden getest.</span><span class="sxs-lookup"><span data-stu-id="8af9f-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="8af9f-354">Voordelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-354">Advantages</span></span>
* <span data-ttu-id="8af9f-355">Er zijn geen extra kosten die zijn gemaakt tijdens de migratie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="8af9f-356">Een-op-een migratie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-356">A one-to-one migration.</span></span>
* <span data-ttu-id="8af9f-357">Minder complexiteit.</span><span class="sxs-lookup"><span data-stu-id="8af9f-357">Reduced complexity.</span></span>
* <span data-ttu-id="8af9f-358">Verbeterde IOPS staat van Premium-opslag-SKU's.</span><span class="sxs-lookup"><span data-stu-id="8af9f-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="8af9f-359">Wanneer de schijven losgekoppeld van de virtuele machine zijn en een 3rd partij gekopieerd naar de nieuwe cloudservice kan hulpprogramma worden gebruikt om de VHD-grootte die hoger doorvoercapaciteit biedt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="8af9f-360">Zie voor het VHD-grootte verhogen, [forumdiscussie](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="8af9f-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="8af9f-361">Nadelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-361">Disadvantages</span></span>
* <span data-ttu-id="8af9f-362">Er is een tijdelijk onderbroken HA en Noodherstel tijdens de migratie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="8af9f-363">Omdat dit een migratie 1:1, moet u een minimale VM-grootte die wordt ondersteuning voor het aantal virtuele harde schijven, zodat u mogelijk niet afslanken van uw virtuele machines gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="8af9f-364">Dit scenario gebruikt Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is.</span><span class="sxs-lookup"><span data-stu-id="8af9f-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="8af9f-365">Er is geen SLA op voltooiing van de kopie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="8af9f-366">De tijd van de exemplaren varieert, terwijl dit afhankelijk van de wachttijd in wachtrij die het is ook afhankelijk van de hoeveelheid gegevens om over te dragen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="8af9f-367">De tijd kopie verhoogd als de overdracht wordt een andere Azure-datacenter die ondersteuning biedt voor Premium-opslag in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="8af9f-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="8af9f-368">Als u zojuist 2 knooppunten hebt, kunt u overwegen een mogelijke Risicobeperking voor het geval de kopie langer dan in de testfase duurt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="8af9f-369">Dit omvat de volgende ideeën.</span><span class="sxs-lookup"><span data-stu-id="8af9f-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="8af9f-370">Toevoegen van een tijdelijk 3e SQL Server-knooppunt voor HA vóór de migratie overeengekomen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="8af9f-371">Voer de migratie buiten Azure gepland onderhoud.</span><span class="sxs-lookup"><span data-stu-id="8af9f-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="8af9f-372">Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="8af9f-373">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="8af9f-373">High-level steps</span></span>
<span data-ttu-id="8af9f-374">Dit document niet illustratie van een volledige end-to-end-voorbeeld, maar het [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) voorziet in gedetailleerde informatie die kunnen worden gebruikt om deze.</span><span class="sxs-lookup"><span data-stu-id="8af9f-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="8af9f-376">De schijfconfiguratie verzamelen en verwijderen van het knooppunt (gekoppelde VHD's niet verwijderd).</span><span class="sxs-lookup"><span data-stu-id="8af9f-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="8af9f-377">Premium-opslagaccount maken en VHD's van het standaard opslagaccount kopiëren</span><span class="sxs-lookup"><span data-stu-id="8af9f-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="8af9f-378">Nieuwe cloudservice maken en implementeren van de VM SQL2 in deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8af9f-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="8af9f-379">Maak de virtuele machine met behulp van de gekopieerde oorspronkelijke besturingssysteem-VHD en koppelen van de gekopieerde VHD's.</span><span class="sxs-lookup"><span data-stu-id="8af9f-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="8af9f-380">Configureer ILB / ELB en het toevoegen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="8af9f-381">Update-Listener door:</span><span class="sxs-lookup"><span data-stu-id="8af9f-381">Update Listener by either:</span></span>
  * <span data-ttu-id="8af9f-382">De altijd op groep offline te halen en het bijwerken van de altijd op Listener met nieuwe ILB / ELB-IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="8af9f-383">Of het IP-adres resource van nieuwe Cloud Service ILB-/ ELB via PowerShell in Windows-clustering toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="8af9f-384">Vervolgens stelt de mogelijke eigenaars van de bron-IP-adres gemigreerde-knooppunt, SQL2, en dit als afhankelijkheid of in de netwerknaam.</span><span class="sxs-lookup"><span data-stu-id="8af9f-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="8af9f-385">Zie de sectie 'Toe te voegen IP-adres Resource op hetzelfde Subnet' van de [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="8af9f-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="8af9f-386">Controleer de DNS-configuratie/doorgiftetaak voor clients.</span><span class="sxs-lookup"><span data-stu-id="8af9f-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="8af9f-387">SQL1 VM gemigreerd en doorloop de stappen 2-4.</span><span class="sxs-lookup"><span data-stu-id="8af9f-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="8af9f-388">Als stappen 5ii wordt gebruikt, voegt u SQL1 als een mogelijke eigenaar voor de bron van de toegevoegde IP-adres</span><span class="sxs-lookup"><span data-stu-id="8af9f-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="8af9f-389">Testfailovers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="8af9f-390">2. Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="8af9f-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="8af9f-391">Als u knooppunten in meer dan één Azure-datacenter (DC hebben) of als u een hybride omgeving hebt, kunt klikt u vervolgens u een AlwaysOn-configuratie in deze omgeving uitvaltijd te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8af9f-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="8af9f-392">De aanpak is om te wijzigen van de synchronisatie altijd op in synchrone voor de on-premises of secundaire Azure domeincontroller, en vervolgens failover via naar SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8af9f-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="8af9f-393">Vervolgens kopieert u de VHD's naar een Premium Storage-account en de machine implementeren in een nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8af9f-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="8af9f-394">Werk de listener en vervolgens een failback uit.</span><span class="sxs-lookup"><span data-stu-id="8af9f-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="8af9f-395">Punten van uitvaltijd</span><span class="sxs-lookup"><span data-stu-id="8af9f-395">Points of downtime</span></span>
<span data-ttu-id="8af9f-396">De uitvaltijd bestaat uit de tijd om failover naar de alternatieve DC en terug.</span><span class="sxs-lookup"><span data-stu-id="8af9f-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="8af9f-397">Ook afhankelijk van de client en DNS-configuratie en de client opnieuw verbinden mag worden uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="8af9f-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="8af9f-398">Houd rekening met het volgende voorbeeld van een hybride altijd op de configuratie:</span><span class="sxs-lookup"><span data-stu-id="8af9f-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="8af9f-400">Voordelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-400">Advantages</span></span>
* <span data-ttu-id="8af9f-401">U kunt gebruikmaken van bestaande infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="8af9f-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="8af9f-402">U hebt de optie voor het Azure-opslag op de DC DR Azure eerst vóór de upgrade.</span><span class="sxs-lookup"><span data-stu-id="8af9f-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="8af9f-403">De DC DR Azure-opslag opnieuw kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="8af9f-404">Er is een minimum van twee failovers tijdens de migratie, met uitzondering van testfailovers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="8af9f-405">U hoeft niet te verplaatsen van SQL Server-gegevens met back-up en herstellen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="8af9f-406">Nadelen</span><span class="sxs-lookup"><span data-stu-id="8af9f-406">Disadvantages</span></span>
* <span data-ttu-id="8af9f-407">Afhankelijk van de clienttoegang tot SQL Server, kunnen er langere latentie als SQL Server wordt uitgevoerd in een andere domeincontroller aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8af9f-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="8af9f-408">De tijd van de kopie van VHD's voor Premium-opslag kan lang zijn.</span><span class="sxs-lookup"><span data-stu-id="8af9f-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="8af9f-409">Dit kan invloed hebben op uw beslissing op of het knooppunt in de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="8af9f-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="8af9f-410">U kunt dit wanneer logboek intensieve werk belastingen worden uitgevoerd tijdens de migratie vereist, is omdat het primaire knooppunt moet niet-gerepliceerde transacties in het transactielogboek behouden.</span><span class="sxs-lookup"><span data-stu-id="8af9f-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="8af9f-411">Daarom kan dit aanzienlijk groeien.</span><span class="sxs-lookup"><span data-stu-id="8af9f-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="8af9f-412">Dit scenario gebruikt Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is.</span><span class="sxs-lookup"><span data-stu-id="8af9f-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="8af9f-413">Er is geen SLA op voltooiing.</span><span class="sxs-lookup"><span data-stu-id="8af9f-413">There is no SLA on completion.</span></span> <span data-ttu-id="8af9f-414">De tijd van de exemplaren varieert, terwijl dit afhankelijk van de wachttijd in wachtrij, het is ook afhankelijk van de hoeveelheid gegevens om over te dragen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="8af9f-415">Daarom alleen hebt u één knooppunt in uw datacenter 2e, u moet treffen Risicobeperking voor het geval de kopie langer duurt dan in de testfase.</span><span class="sxs-lookup"><span data-stu-id="8af9f-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="8af9f-416">Dit omvat de volgende ideeën.</span><span class="sxs-lookup"><span data-stu-id="8af9f-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="8af9f-417">Een tijdelijke SQL-knooppunt 2e toevoegen voor HA vóór de migratie overeengekomen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="8af9f-418">Voer de migratie buiten Azure gepland onderhoud.</span><span class="sxs-lookup"><span data-stu-id="8af9f-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="8af9f-419">Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="8af9f-420">Dit scenario wordt ervan uitgegaan dat u de installatie hebt gedocumenteerd en weten hoe de opslag is toegewezen om te kunnen aanbrengen voor optimale schijf cache-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="8af9f-421">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="8af9f-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="8af9f-423">De on-premises / DC van Azure naar de SQL Server-primaire alternatieve, en kunnen de andere automatische Failover Partner (AFP).</span><span class="sxs-lookup"><span data-stu-id="8af9f-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="8af9f-424">Verzamelen van gegevens over de schijfconfiguratie van SQL2 en verwijderen van het knooppunt (gekoppelde VHD's niet verwijderd).</span><span class="sxs-lookup"><span data-stu-id="8af9f-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="8af9f-425">Premium-opslagaccount maken en kopieer VHD's van het standaard opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8af9f-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="8af9f-426">Maak een nieuwe cloudservice en de SQL2 virtuele machine maken met de opslag van premies schijven die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8af9f-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="8af9f-427">Configureer ILB / ELB en het toevoegen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8af9f-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="8af9f-428">De altijd op Listener bijwerken met nieuwe ILB / ELB IP-adres en test failover.</span><span class="sxs-lookup"><span data-stu-id="8af9f-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="8af9f-429">Controleer de DNS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="8af9f-430">Wijzig de AFP in SQL2, SQL1 migreren en stappen 2 tot en met 5 doorlopen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="8af9f-431">Testfailovers.</span><span class="sxs-lookup"><span data-stu-id="8af9f-431">Test failovers.</span></span>
* <span data-ttu-id="8af9f-432">De AFP overschakelen naar SQL1 en SQL2</span><span class="sxs-lookup"><span data-stu-id="8af9f-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="8af9f-433">Bijlage: Een implementatie voor meerdere locaties altijd op een Cluster migreren naar de Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="8af9f-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="8af9f-434">De rest van dit onderwerp biedt een gedetailleerd voorbeeld van het converteren van een altijd op clusters op meerdere locaties naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="8af9f-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="8af9f-435">Ook converteert naar een interne load balancer (ILB) de Listener van het gebruik van een externe load balancer (ELB).</span><span class="sxs-lookup"><span data-stu-id="8af9f-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="8af9f-436">Omgeving</span><span class="sxs-lookup"><span data-stu-id="8af9f-436">Environment</span></span>
* <span data-ttu-id="8af9f-437">Windows 2k 12 / SQL 2k 12</span><span class="sxs-lookup"><span data-stu-id="8af9f-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="8af9f-438">Bestanden op SP 1 DB</span><span class="sxs-lookup"><span data-stu-id="8af9f-438">1 DB Files on SP</span></span>
* <span data-ttu-id="8af9f-439">2 x opslaggroepen per knooppunt</span><span class="sxs-lookup"><span data-stu-id="8af9f-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="8af9f-441">VIRTUELE MACHINE:</span><span class="sxs-lookup"><span data-stu-id="8af9f-441">VM:</span></span>
<span data-ttu-id="8af9f-442">In dit voorbeeld gaan we demonstreren verplaatsen van een ELB naar ILB.</span><span class="sxs-lookup"><span data-stu-id="8af9f-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="8af9f-443">ELB is beschikbaar voordat ILB, zodat dit overschakelen naar dit tijdens de migratie worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8af9f-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="8af9f-445">Pre-stappen: Verbinding maken met abonnement</span><span class="sxs-lookup"><span data-stu-id="8af9f-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="8af9f-446">Stap 1: Nieuw Opslagaccount maken en in de Cloud Service</span><span class="sxs-lookup"><span data-stu-id="8af9f-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
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

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="8af9f-447">Stap 2: Verhoog de toegestane fouten op resources<Optional></span><span class="sxs-lookup"><span data-stu-id="8af9f-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="8af9f-448">Bepaalde bronnen die deel uitmaken van de AlwaysOn-beschikbaarheidsgroep er gelden beperkingen op hoeveel storingen die kunnen optreden in een periode waarin de cluster-service probeert het opnieuw opstarten van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8af9f-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="8af9f-449">Het is raadzaam dat u deze terwijl u via deze procedure zijn doorlopen sinds als u niet handmatig failover en trigger failovers door het afsluiten van computers die u dicht bij deze limiet krijgt verhogen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="8af9f-450">Moet worden beperkt te verdubbelen het tegoed is mislukt om dit te doen in Failoverclusterbeheer, gaat u naar de eigenschappen van de resourcegroep altijd op:</span><span class="sxs-lookup"><span data-stu-id="8af9f-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="8af9f-452">Wijzig het maximum aantal fouten in 6.</span><span class="sxs-lookup"><span data-stu-id="8af9f-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="8af9f-453">Stap 3: Aanvullende IP-adres resource voor de clustergroep<Optional></span><span class="sxs-lookup"><span data-stu-id="8af9f-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="8af9f-454">Als er slechts één IP-adres voor de clustergroep en dit wordt uitgelijnd op het subnet van de cloud, houd er rekening mee, als u per ongeluk offline alle clusterknooppunten in de cloud op dat netwerk vervolgens de Cluster-IP-resource halen en de clusternetwerknaam kan niet worden online worden gezet.</span><span class="sxs-lookup"><span data-stu-id="8af9f-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="8af9f-455">In het geval van dit kan updates voor andere clusterbronnen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="8af9f-456">Stap 4: DNS-configuratie</span><span class="sxs-lookup"><span data-stu-id="8af9f-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="8af9f-457">Voor het implementeren van een vloeiende overgang is afhankelijk van hoe DNS wordt gebruikt en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="8af9f-458">Wanneer altijd op is geïnstalleerd, wordt er een resourcegroep van Windows-Cluster gemaakt als u Failoverclusterbeheer opent, ziet u dat ten minste deze drie bronnen heeft, zijn de twee dat het document naar verwijst:</span><span class="sxs-lookup"><span data-stu-id="8af9f-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="8af9f-459">Virtuele-netwerknaam (VNN) – Dit is de DNS-naam die client verbinding maken wanneer er verbinding maken met SQL-Servers via altijd op willen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="8af9f-460">IP-adres van bron: dit is het IP-adres dat aan de VNN gekoppeld, kunt u meer dan één hebben en in een configuratie voor meerdere sites hebt u een IP-adres per site/subnet.</span><span class="sxs-lookup"><span data-stu-id="8af9f-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="8af9f-461">Bij het verbinding maken met SQL Server, SQL Server Client stuurprogramma wordt de DNS-records die zijn gekoppeld aan de listener ophalen en probeer het verbinding maken met elke altijd op gekoppelde IP-adres, bespreken hieronder we een aantal factoren die van invloed kunnen zijn op dit.</span><span class="sxs-lookup"><span data-stu-id="8af9f-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="8af9f-462">Het aantal gelijktijdige DNS-records die gekoppeld aan de naam van de listener zijn afhankelijk is, niet alleen op het aantal IP-adressen die zijn gekoppeld, maar de ' RegisterAllIpProviders'setting in Failover Clustering voor de resource altijd ON VNN.</span><span class="sxs-lookup"><span data-stu-id="8af9f-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="8af9f-463">Wanneer u altijd op in Azure implementeert, er zijn verschillende stappen voor het maken van de Listener en IP-adressen, u moet handmatig configureren van de 'RegisterAllIpProviders' 1, dit is anders dan bij een on-premises altijd op implementatie waarop deze is al ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="8af9f-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="8af9f-464">Als 'RegisterAllIpProviders' 0 is, klikt u vervolgens ziet alleen u een DNS-record in DNS die zijn gekoppeld aan de Listener:</span><span class="sxs-lookup"><span data-stu-id="8af9f-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="8af9f-466">Als 'RegisterAllIpProviders' 1:</span><span class="sxs-lookup"><span data-stu-id="8af9f-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="8af9f-468">Hieronder de code wordt uit de instellingen VNN dump en voor u ingesteld, houd er rekening mee voor deze duurt Listener offline waardoor de wijziging door te voeren u moet de VNN offline zetten en schakel deze weer online onderbreking van de client-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="8af9f-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="8af9f-469">In een latere migratiestap van een moet u de listener Always On bijwerken met een bijgewerkte IP-adres dat verwijst naar een load balancer, dient hiervoor een IP-adres resource verwijderen en toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="8af9f-470">Nadat de IP-update moet u ervoor zorgen het nieuwe IP-adres is bijgewerkt in DNS-Zone en dat de clients hun lokale DNS-cache wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8af9f-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="8af9f-471">Als uw clients bevinden zich in een ander netwerksegment en verwijzen naar een andere DNS-server, moet u nagaan wat er gebeurt over het overdragen van DNS-Zone tijdens de migratie als de toepassing opnieuw tijd worden beperkt door ten minste de Zone Transfer-tijd van alle nieuwe IP-adressen voor de listener.</span><span class="sxs-lookup"><span data-stu-id="8af9f-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="8af9f-472">Als u hier tijd-beperking, u moet worden behandeld en testen forceren van een incrementele zoneoverdracht met uw Windows-teams en plaatst de DNS-hostrecord ook naar een lagere tijd To Live (TTL), zodat de clients bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8af9f-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="8af9f-473">Zie voor meer informatie [incrementele zoneoverdrachten](https://technet.microsoft.com/library/cc958973.aspx) en [Start DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="8af9f-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="8af9f-474">Standaard de TTL voor DNS-Record die is gekoppeld aan de Listener altijd op in Azure is 1200 seconden.</span><span class="sxs-lookup"><span data-stu-id="8af9f-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="8af9f-475">Mogelijk wilt u dit reduceren als u onder tijd beperking tijdens de migratie om te controleren of de clients hun DNS bijwerken met de bijgewerkte IP-adres voor de listener.</span><span class="sxs-lookup"><span data-stu-id="8af9f-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="8af9f-476">U kunt zien en de configuratie wijzigen door het dumpen van een van de configuratie van de VNN:</span><span class="sxs-lookup"><span data-stu-id="8af9f-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="8af9f-477">Houd er rekening mee hoe lager het 'HostRecordTTL', een hogere mate van DNS-verkeer wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="8af9f-478">Instellingen voor client-toepassing</span><span class="sxs-lookup"><span data-stu-id="8af9f-478">Client application settings</span></span>
<span data-ttu-id="8af9f-479">Als u de SQL-clienttoepassing de .net 4.5 ondersteunt SQLClient, dan hebt u kunt gebruiken ' MULTISUBNETFAILOVER = TRUE' sleutelwoord, dit wordt aanbevolen om te worden toegepast zoals maakt het mogelijk sneller verbinding met SQL AlwaysOn-beschikbaarheidsgroep tijdens failover.</span><span class="sxs-lookup"><span data-stu-id="8af9f-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="8af9f-480">Het inventariseren via alle IP-adressen die zijn gekoppeld aan de listener altijd op parallel en een agressievere TCP opnieuw verbindingssnelheid tijdens een failover uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8af9f-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="8af9f-481">Zie voor meer informatie over de bovenstaande instellingen [MultiSubnetFailover sleutelwoord en functies die zijn gekoppeld](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="8af9f-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="8af9f-482">Zie ook [SqlClient-ondersteuning voor hoge beschikbaarheid, herstel na noodgevallen](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8af9f-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="8af9f-483">Stap 5: Instellingen van het clusterquorum</span><span class="sxs-lookup"><span data-stu-id="8af9f-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="8af9f-484">Als u te hebben van ten minste één SQL-Server niet actief op een tijdstip gaat, moet u de instelling van het clusterquorum wijzigen als bestand Share Witness (FSW) met 2 knooppunten, moet u de Quorumconfiguratie Knooppuntmeerderheid toestaan en gebruikmaken van dynamische stemmen instellen , en dit is om toe te staan voor één knooppunt in het permanente blijven.</span><span class="sxs-lookup"><span data-stu-id="8af9f-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="8af9f-485">Zie voor meer informatie over het beheren en configureren van het clusterquorum [configureren en beheren van het Quorum in een Windows Server 2012-failovercluster](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="8af9f-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="8af9f-486">Stap 6: Extraheren bestaande eindpunten en ACL 's</span><span class="sxs-lookup"><span data-stu-id="8af9f-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="8af9f-487">Sla deze naar een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="8af9f-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="8af9f-488">Stap 7: Failoverpartners en replicatie-modi wijzigen</span><span class="sxs-lookup"><span data-stu-id="8af9f-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="8af9f-489">Als u meer dan 2 SQL-Servers hebt, moet u de failover van een andere secundaire in een andere domeincontroller of on-premises wijzigen in 'Synchrone' en kunt u een Partner voor automatische Failover (AFP), is dit zodat u HA onderhouden terwijl u wijzigingen doorvoert.</span><span class="sxs-lookup"><span data-stu-id="8af9f-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="8af9f-490">U kunt dit doen via TSQL van echter SSMS wijzigen:</span><span class="sxs-lookup"><span data-stu-id="8af9f-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="8af9f-492">Stap 8: Verwijder secundaire virtuele machine van de cloudservice</span><span class="sxs-lookup"><span data-stu-id="8af9f-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="8af9f-493">U rekening mee moet houden voor het migreren van een secundaire knooppunt cloud eerst als dit momenteel primaire is, moet u een handmatige failover initiëren.</span><span class="sxs-lookup"><span data-stu-id="8af9f-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="8af9f-494">Stap 9: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan</span><span class="sxs-lookup"><span data-stu-id="8af9f-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="8af9f-495">Voor gegevensvolumes moeten deze worden ingesteld op alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="8af9f-496">Voor TLOG volumes moeten deze worden ingesteld op NONE.</span><span class="sxs-lookup"><span data-stu-id="8af9f-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="8af9f-498">Stap 10: Kopie VHD 's</span><span class="sxs-lookup"><span data-stu-id="8af9f-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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



<span data-ttu-id="8af9f-499">U kunt de status van het exemplaar van de VHD's met de Premium-opslagaccount controleren:</span><span class="sxs-lookup"><span data-stu-id="8af9f-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

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

<span data-ttu-id="8af9f-501">Wacht totdat deze worden geregistreerd als geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="8af9f-502">Voor informatie over afzonderlijke blobs:</span><span class="sxs-lookup"><span data-stu-id="8af9f-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="8af9f-503">Stap 11: Register OS-schijf</span><span class="sxs-lookup"><span data-stu-id="8af9f-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="8af9f-504">Stap 12: Secundaire importeren in de nieuwe cloudservice</span><span class="sxs-lookup"><span data-stu-id="8af9f-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="8af9f-505">De volgende code gebruikt ook de optie toegevoegde hier kunt u de machine importeren en gebruiken van het retainable VIP.</span><span class="sxs-lookup"><span data-stu-id="8af9f-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
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

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="8af9f-506">Stap 13: Maak ILB op nieuwe Cloud Svc toevoegen van Load Balanced eindpunten en ACL's</span><span class="sxs-lookup"><span data-stu-id="8af9f-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="8af9f-507">Stap 14: Altijd bijwerken op</span><span class="sxs-lookup"><span data-stu-id="8af9f-507">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="8af9f-509">Nu de oude IP-adres van de cloudservice verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="8af9f-511">Stap 15: DNS-updates controleren</span><span class="sxs-lookup"><span data-stu-id="8af9f-511">Step 15: DNS update check</span></span>
<span data-ttu-id="8af9f-512">Nu moet u DNS-Servers in uw SQL Server client netwerken controleren en zorg ervoor dat het clustering de extra hostrecord toegevoegde IP-adres heeft toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="8af9f-513">Als deze DNS-servers niet hebt bijgewerkt, houd rekening met het forceren van een DNS-Zone-overdracht en zorg ervoor dat de clients in er subnet kunnen worden omgezet in beide altijd op IP-adressen, dit is dus u hoeft niet te wachten op automatische DNS-replicatie.</span><span class="sxs-lookup"><span data-stu-id="8af9f-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="8af9f-514">Stap 16: Configureer altijd opnieuw op</span><span class="sxs-lookup"><span data-stu-id="8af9f-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="8af9f-515">Op dit moment wachten op de secundaire dat knooppunt die volledig zijn gesynchroniseerd met het lokale knooppunt en overschakelen naar het knooppunt synchrone replicatie en kunt u de AFP is gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="8af9f-516">Stap 17: Tweede knooppunt migreren</span><span class="sxs-lookup"><span data-stu-id="8af9f-516">Step 17: Migrate second node</span></span>
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

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="8af9f-517">Stap 18: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan</span><span class="sxs-lookup"><span data-stu-id="8af9f-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="8af9f-518">Voor gegevensvolumes moeten deze worden ingesteld op alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="8af9f-519">Voor TLOG volumes moeten deze worden ingesteld op NONE.</span><span class="sxs-lookup"><span data-stu-id="8af9f-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="8af9f-521">Stap 19: Maak een nieuwe onafhankelijke Storage-Account voor secundair knooppunt</span><span class="sxs-lookup"><span data-stu-id="8af9f-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="8af9f-522">Stap 20: Kopie VHD 's</span><span class="sxs-lookup"><span data-stu-id="8af9f-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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


<span data-ttu-id="8af9f-523">U kunt de status van het VHD-exemplaar controleren voor alle virtuele harde schijven: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Schijflabel $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="8af9f-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="8af9f-525">Wacht totdat deze worden geregistreerd als geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="8af9f-526">Voor informatie over afzonderlijke blobs:</span><span class="sxs-lookup"><span data-stu-id="8af9f-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="8af9f-527">Stap 21: Register OS-schijf</span><span class="sxs-lookup"><span data-stu-id="8af9f-527">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
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

    #Join to existing Avaiability Set

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

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="8af9f-528">Stap 22: Toevoegen Load Balanced eindpunten en ACL's</span><span class="sxs-lookup"><span data-stu-id="8af9f-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="8af9f-529">Stap 23: De testfailover</span><span class="sxs-lookup"><span data-stu-id="8af9f-529">Step 23: Test failover</span></span>
<span data-ttu-id="8af9f-530">U moet nu gebruiken om het gemigreerde knooppunt synchroniseren met het lokale altijd aan knooppunt in naar de modus voor synchrone replicatie plaats en wacht totdat deze is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="8af9f-530">You should now let the migrated node synchronize with the on-premises Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="8af9f-531">Vervolgens wordt de failover van on-premises naar het eerste knooppunt gemigreerd, die de AFP is.</span><span class="sxs-lookup"><span data-stu-id="8af9f-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="8af9f-532">Zodra die eerder heeft gewerkt, wijzigt u het laatste knooppunt van de gemigreerde in de AFP.</span><span class="sxs-lookup"><span data-stu-id="8af9f-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="8af9f-533">U moet testfailovers tussen alle knooppunten en hoewel chaos tests uit om ervoor te zorgen failovers work als verwacht en in een tijdige manor uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8af9f-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="8af9f-534">24 stap: Opnieuw clusterquoruminstellingen zetten / DNS TTL / Failover Pntrs / synchronisatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="8af9f-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="8af9f-535">Toevoegen van de bron van het IP-adres op hetzelfde Subnet</span><span class="sxs-lookup"><span data-stu-id="8af9f-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="8af9f-536">Als u alleen 2 SQL-Servers hebt en wilt deze migreren naar een nieuwe cloudservice maar wilt houden in hetzelfde subnet, kunt u voorkomen dat de listener offline brengen naar de oorspronkelijke altijd op IP-adres verwijderen en het nieuwe IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8af9f-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="8af9f-537">Als u de virtuele machines naar een ander subnet migreert moet u niet om dit te doen omdat er een extra clusternetwerk dat verwijst naar dat subnet.</span><span class="sxs-lookup"><span data-stu-id="8af9f-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="8af9f-538">Zodra u hebt de gemigreerde secundaire beschikbaar komen en in de nieuwe resource IP-adres voor de nieuwe cloudservice vóór de failover de bestaande primaire toegevoegd, moet u deze stappen binnen de failover-Clusterbeheer uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8af9f-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="8af9f-539">Als u wilt toevoegen aan IP-adres, Zie de [bijlage](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), stap 14.</span><span class="sxs-lookup"><span data-stu-id="8af9f-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="8af9f-540">Wijzig de mogelijke eigenaar 'Bestaande primaire SQL-Server', in het onderstaande voorbeeld 'dansqlams4' voor de huidige bron van de IP-adres:</span><span class="sxs-lookup"><span data-stu-id="8af9f-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="8af9f-542">Wijzig de mogelijke eigenaar naar 'Gemigreerd secundaire SQL-Server', in het onderstaande voorbeeld 'dansqlams5' voor de nieuwe bron voor het IP-adres:</span><span class="sxs-lookup"><span data-stu-id="8af9f-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="8af9f-544">Wanneer deze optie is ingesteld, kunt u failover en wanneer het laatste knooppunt is gemigreerd de mogelijke eigenaars worden bewerkt zodat dit knooppunt wordt toegevoegd als een mogelijke eigenaar:</span><span class="sxs-lookup"><span data-stu-id="8af9f-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="8af9f-546">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8af9f-546">Additional resources</span></span>
* [<span data-ttu-id="8af9f-547">Azure Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="8af9f-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="8af9f-548">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="8af9f-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="8af9f-549">SQL Server in Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="8af9f-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
