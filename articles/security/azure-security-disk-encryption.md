---
title: aaaAzure schijfversleuteling voor Windows en Linux IaaS VM's | Microsoft Docs
description: Dit artikel bevat een overzicht van Microsoft Azure Disk Encryption for Windows en Linux IaaS VM's.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="7da43-103">Azure Disk Encryption for Windows and Linux IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="7da43-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="7da43-104">Microsoft Azure wordt ten zeerste doorgevoerd tooensuring uw privacy van gegevens, onafhankelijkheid van gegevens en kunt u uw Azure gehoste toocontrol gegevens via een reeks technologieën voor geavanceerde tooencrypt, beheren en beheren van versleutelingssleutels besturingselement & audit toegang van gegevens.</span><span class="sxs-lookup"><span data-stu-id="7da43-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="7da43-105">Dit biedt Azure-klanten Hallo flexibiliteit toochoose Hallo oplossing die het beste voldoet aan de behoeften van hun bedrijf.</span><span class="sxs-lookup"><span data-stu-id="7da43-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="7da43-106">In dit artikel, we vindt u tooa nieuwe technologieoplossing 'Azure Disk Encryption for Windows and Linux IaaS VM' toohelp beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="7da43-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="7da43-107">Hallo artikel biedt gedetailleerde richtlijnen voor hoe toouse-hello Azure disk encryption functies zoals Hallo ondersteund scenario's en Hallo gebruikerservaringen.</span><span class="sxs-lookup"><span data-stu-id="7da43-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-108">Bepaalde aanbevelingen mogelijk meer gegevens, netwerk of compute-Resourcegebruik, wat leidt tot extra kosten in licentie of abonnement.</span><span class="sxs-lookup"><span data-stu-id="7da43-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="7da43-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7da43-109">Overview</span></span>
<span data-ttu-id="7da43-110">Azure Disk Encryption is een nieuwe functie waarmee u uw Windows- en Linux IaaS-schijven voor virtuele machine versleutelen.</span><span class="sxs-lookup"><span data-stu-id="7da43-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="7da43-111">Azure Disk Encryption maakt gebruik van Hallo industrie-initiatief [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) functie van Windows en Hallo [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) functie van Linux tooprovide volumeversleuteling voor hello OS- en gegevensschijven Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="7da43-112">Hallo-oplossing is geïntegreerd met [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp u controleren en beheren van Hallo schijfversleuteling sleutels en geheimen in uw abonnement sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="7da43-113">Hallo oplossing zorgt er ook voor dat alle gegevens op schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="7da43-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="7da43-114">Versleuteling van de schijf van Azure voor Windows en Linux IaaS VM's wordt nu **algemene beschikbaarheid** in alle openbare Azure-regio en AzureGov regio's voor de standaard virtuele machines en virtuele machines met premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="7da43-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="7da43-115">Versleuteling scenario 's</span><span class="sxs-lookup"><span data-stu-id="7da43-115">Encryption scenarios</span></span>
<span data-ttu-id="7da43-116">Hello Azure Disk Encryption-oplossing ondersteunt Hallo klant scenario's te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="7da43-117">Schakel versleuteling in op de nieuwe IaaS VM's die worden gemaakt op basis van vooraf zijn versleuteld VHD- en versleutelingssleutels</span><span class="sxs-lookup"><span data-stu-id="7da43-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="7da43-118">Schakel versleuteling in op nieuwe gemaakt op basis van installatiekopieën van Hallo ondersteund galerie van Azure IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="7da43-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="7da43-119">Schakel versleuteling in op bestaande IaaS virtuele machines die worden uitgevoerd in Azure</span><span class="sxs-lookup"><span data-stu-id="7da43-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="7da43-120">Schakel versleuteling in op IaaS VM's van Windows</span><span class="sxs-lookup"><span data-stu-id="7da43-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="7da43-121">Versleuteling op gegevensstations voor Linux IaaS VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="7da43-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="7da43-122">Versleuteling van beheerde schijf virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="7da43-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="7da43-123">Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="7da43-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="7da43-124">Back-up en herstel van versleutelde virtuele machines, versleuteld met sleutelcodering sleutel</span><span class="sxs-lookup"><span data-stu-id="7da43-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="7da43-125">Hallo-oplossing ondersteunt Hallo volgen scenario's voor IaaS VM's wanneer ze zijn ingeschakeld in Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="7da43-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="7da43-126">Integratie met Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="7da43-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="7da43-127">Standard-laag VMs: [A, D, DS, G, GS, F en enzovoort reeks IaaS VM's](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="7da43-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="7da43-128">Versleuteling inschakelen voor Windows en Linux IaaS VM's en beheerde schijf VM's van Hallo ondersteund galerie van Azure-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="7da43-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="7da43-129">Versleuteling op besturingssysteem en stations voor Windows IaaS VM's en beheerde schijf-VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="7da43-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="7da43-130">Versleuteling op gegevensstations voor Linux IaaS VM's en beheerde schijf-VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="7da43-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="7da43-131">Schakel versleuteling in op IaaS VM's met Windows Client-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="7da43-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="7da43-132">Schakel versleuteling in op volumes met koppelpunten paden</span><span class="sxs-lookup"><span data-stu-id="7da43-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="7da43-133">Schakel versleuteling in op Linux VM's zijn geconfigureerd met schijf striping (RAID) met behulp van mdadm</span><span class="sxs-lookup"><span data-stu-id="7da43-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="7da43-134">Schakel versleuteling in op de virtuele Linux-machines met behulp van LVM voor gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="7da43-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="7da43-135">Schakel versleuteling in op Windows VM's zijn geconfigureerd met opslagruimten</span><span class="sxs-lookup"><span data-stu-id="7da43-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="7da43-136">Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="7da43-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="7da43-137">Alle openbare Azure en AzureGov regio's worden ondersteund</span><span class="sxs-lookup"><span data-stu-id="7da43-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="7da43-138">Hallo-oplossing biedt geen ondersteuning voor Hallo volgen scenario's, functies en -technologie:</span><span class="sxs-lookup"><span data-stu-id="7da43-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="7da43-139">Basisstaffel IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="7da43-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="7da43-140">Het uitschakelen van Linux IaaS VM's op een station OS versleuteling</span><span class="sxs-lookup"><span data-stu-id="7da43-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="7da43-141">Het uitschakelen van versleuteling op een gegevensstation als Hallo OS station wordt versleuteld voor Linux Iaas VM 's</span><span class="sxs-lookup"><span data-stu-id="7da43-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="7da43-142">IaaS VM's die zijn gemaakt met behulp van Hallo-methode voor het maken van klassieke VM</span><span class="sxs-lookup"><span data-stu-id="7da43-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="7da43-143">Schakel versleuteling in op Windows en Linux-IaaS VM's klanten aangepaste installatiekopieën wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="7da43-144">Enccryption inschakelen op Linux-besturingssysteem voor LVM schijf wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="7da43-145">Deze ondersteuning wordt binnenkort worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="7da43-145">This support will come soon.</span></span>
* <span data-ttu-id="7da43-146">Integratie met uw on-premises Key Management Service</span><span class="sxs-lookup"><span data-stu-id="7da43-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="7da43-147">Azure Files (gedeelde bestandssysteem), Network File System (NFS), dynamische volumes en virtuele machines van Windows die zijn geconfigureerd met software gebaseerde RAID-systemen</span><span class="sxs-lookup"><span data-stu-id="7da43-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="7da43-148">Back-up en herstel van versleutelde virtuele machines, zonder sleutelcodering sleutel is gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="7da43-149">Instellingen voor codering van een bestaande versleutelde premium-opslag VM bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7da43-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-150">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da43-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="7da43-151">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="7da43-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="7da43-152">KEK-sleutel is een optionele parameter waarmee de VM-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7da43-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="7da43-153">Deze ondersteuning is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7da43-153">This support is coming soon.</span></span>
> <span data-ttu-id="7da43-154">Bijwerken van instellingen voor codering van een bestaande versleutelde premium-opslag virtuele machine worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="7da43-155">Deze ondersteuning is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7da43-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="7da43-156">Coderingsfuncties</span><span class="sxs-lookup"><span data-stu-id="7da43-156">Encryption features</span></span>
<span data-ttu-id="7da43-157">Wanneer u inschakelen en implementeren van Azure Disk Encryption voor Azure IaaS VM's, zijn hello volgende mogelijkheden ingeschakeld, afhankelijk van Hallo configuratie die is opgegeven:</span><span class="sxs-lookup"><span data-stu-id="7da43-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="7da43-158">Versleuteling van Hallo OS volume tooprotect Hallo opstartvolume in rust in uw opslagruimte</span><span class="sxs-lookup"><span data-stu-id="7da43-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="7da43-159">Versleuteling van gegevens volumes tooprotect Hallo hoeveelheden gegevens in rust in uw opslagruimte</span><span class="sxs-lookup"><span data-stu-id="7da43-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="7da43-160">Het uitschakelen van versleuteling op Hallo OS en gegevens schijven voor Windows IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="7da43-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="7da43-161">Versleuteling van gegevens Hallo uitschakelen schijven voor Linux IaaS VM's (alleen als het besturingssysteem IS niet versleuteld station)</span><span class="sxs-lookup"><span data-stu-id="7da43-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="7da43-162">Hallo versleutelingssleutels en geheimen in uw abonnement sleutelkluis beveiligen</span><span class="sxs-lookup"><span data-stu-id="7da43-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="7da43-163">Hallo coderingsstatus van Hallo Reporting versleuteld IaaS VM</span><span class="sxs-lookup"><span data-stu-id="7da43-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="7da43-164">Verwijderen van configuratie-instellingen voor schijf-codering van Hallo IaaS virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7da43-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="7da43-165">Back-up en herstel van versleutelde virtuele machines met behulp van hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="7da43-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-166">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da43-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="7da43-167">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="7da43-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="7da43-168">KEK-sleutel is een optionele parameter waarmee de VM-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7da43-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="7da43-169">Azure Disk Encryption voor IaaS VMS voor Windows en Linux-oplossing omvat:</span><span class="sxs-lookup"><span data-stu-id="7da43-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="7da43-170">Hallo schijfversleuteling extensie voor Windows.</span><span class="sxs-lookup"><span data-stu-id="7da43-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="7da43-171">Hallo schijfversleuteling extensie voor Linux.</span><span class="sxs-lookup"><span data-stu-id="7da43-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="7da43-172">Hallo-schijfversleuteling PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7da43-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="7da43-173">Hallo schijfversleuteling cmdlets van Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="7da43-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="7da43-174">Hallo-schijfversleuteling Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="7da43-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="7da43-175">Hello Azure Disk Encryption oplossing wordt ondersteund op IaaS VM's met Windows of Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="7da43-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="7da43-176">Zie voor meer informatie over de besturingssystemen ondersteund Hallo Hallo 'vereisten' sectie.</span><span class="sxs-lookup"><span data-stu-id="7da43-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-177">Er zijn geen extra kosten voor het versleutelen van VM-schijven met Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="7da43-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="7da43-178">Waardevoorstel</span><span class="sxs-lookup"><span data-stu-id="7da43-178">Value proposition</span></span>
<span data-ttu-id="7da43-179">Wanneer u hello Azure Disk Encryption-management-oplossing toepast, kunt u voldoen aan Hallo bedrijfsbehoeften te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="7da43-180">IaaS VM's worden beveiligd in rust, omdat u de gestandaardiseerde technologie tooaddress organisatie beveiliging en naleving versleutelingsvereisten kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7da43-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="7da43-181">Opstarten van IaaS VM's onder de klant beheerde sleutel en beleid en u kunt hun gebruik in de sleutelkluis controleren.</span><span class="sxs-lookup"><span data-stu-id="7da43-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="7da43-182">Codering-werkstroom</span><span class="sxs-lookup"><span data-stu-id="7da43-182">Encryption workflow</span></span>
<span data-ttu-id="7da43-183">schijfversleuteling tooenable voor Windows en Linux-machines Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="7da43-184">Kies een versleutelingsscenario uit Hallo voorafgaand aan scenario's voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7da43-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="7da43-185">Opt-in tooenabling schijfversleuteling via hello Azure Disk Encryption Resource Manager-sjabloon, PowerShell-cmdlets of de opdracht CLI en Hallo versleuteling configuratie opgeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="7da43-186">Hallo klant versleuteld VHD scenario Hallo versleuteld VHD tooyour storage-account en Hallo encryption key wezenlijke tooyour sleutelkluis te uploaden.</span><span class="sxs-lookup"><span data-stu-id="7da43-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="7da43-187">Vervolgens opgeven configuratie Hallo-tooenable versleuteling op een nieuwe IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="7da43-188">Nieuwe virtuele machines die zijn gemaakt van Hallo Marketplace en bestaande virtuele machines die al worden uitgevoerd in Azure, bieden configuratie Hallo-tooenable versleuteling op Hallo IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="7da43-189">Verleen toegang toohello Azure-platform tooread Hallo versleutelingssleutel materiaal (versleutelingssleutels BitLocker voor Windows-systemen) en de wachtwoordzin voor Linux van uw sleutelkluis tooenable versleuteling op Hallo IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="7da43-190">Geef hello Azure Active Directory (Azure AD) toepassing identiteit toowrite Hallo encryption key wezenlijke tooyour sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="7da43-191">In dat geval schakelt u versleuteling op Hallo IaaS VM voor Hallo scenario's die zijn vermeld in stap 2.</span><span class="sxs-lookup"><span data-stu-id="7da43-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="7da43-192">Azure VM-servicemodel Hallo bijgewerkt met versleuteling en Hallo sleutelkluis configuratie en stelt uw versleutelde VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="7da43-194">Werkstroom voor ontsleuteling</span><span class="sxs-lookup"><span data-stu-id="7da43-194">Decryption workflow</span></span>
<span data-ttu-id="7da43-195">schijfversleuteling toodisable voor IaaS VM's voltooid Hallo op hoog niveau stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="7da43-196">Kies toodisable-versleuteling (decodering) op een actieve IaaS VM in Azure via hello Azure Disk Encryption Resource Manager-sjabloon of PowerShell-cmdlets en Hallo ontsleuteling configuratie opgeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="7da43-197">Deze stap schakelt versleuteling van Hallo OS of Hallo gegevensvolume of beide op Hallo Windows IaaS VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="7da43-198">Echter, zoals vermeld in de vorige sectie hello, uitschakelen van Linux-besturingssysteem schijfversleuteling wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="7da43-199">Hallo ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines, zolang Hallo besturingssysteemschijf is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="7da43-200">Azure-updates Hallo VM-servicemodel en Hallo IaaS VM ontsleutelde gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="7da43-201">Hallo-inhoud van Hallo VM zijn niet langer in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-202">Hallo disable-codering bewerking worden niet verwijderd voor uw kluis en Hallo encryption key sleutelmateriaal (versleutelingssleutels BitLocker voor Windows-systemen) of de wachtwoordzin voor Linux.</span><span class="sxs-lookup"><span data-stu-id="7da43-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="7da43-203">Het uitschakelen van Linux OS schijf-versleuteling wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="7da43-204">Hallo ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7da43-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="7da43-205">Het uitschakelen van de schijf van gegevensversleuteling voor Linux wordt niet ondersteund als Hallo OS station wordt versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da43-206">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7da43-206">Prerequisites</span></span>
<span data-ttu-id="7da43-207">Voordat u Azure Disk Encryption op Azure IaaS VM's voor Hallo ondersteund scenario's die zijn beschreven in de sectie 'Overzicht' hello inschakelen, Zie Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="7da43-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="7da43-208">U moet een geldige actief Azure-abonnement toocreate resources in Azure in Hallo ondersteunde regio's hebben.</span><span class="sxs-lookup"><span data-stu-id="7da43-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="7da43-209">Azure Disk Encryption wordt ondersteund op de volgende versies van Windows Server Hallo: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7da43-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="7da43-210">Azure Disk Encryption wordt ondersteund op Windows-clientversies na Hallo: Windows 8 client en Windows 10-client.</span><span class="sxs-lookup"><span data-stu-id="7da43-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-211">Voor Windows Server 2008 R2, moet u .NET Framework 4.5 is geïnstalleerd voordat u Azure-versleuteling inschakelen hebben.</span><span class="sxs-lookup"><span data-stu-id="7da43-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="7da43-212">U kunt deze installeren via Windows Update door Hallo optionele update Microsoft .NET Framework 4.5.2 voor Windows Server 2008 R2 x64 64-systemen te installeren ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="7da43-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="7da43-213">Azure Disk Encryption wordt ondersteund op Hallo galerie van Azure te volgen op basis van Linux-server distributies en versies:</span><span class="sxs-lookup"><span data-stu-id="7da43-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="7da43-214">Linux-distributie</span><span class="sxs-lookup"><span data-stu-id="7da43-214">Linux Distribution</span></span> | <span data-ttu-id="7da43-215">Versie</span><span class="sxs-lookup"><span data-stu-id="7da43-215">Version</span></span> | <span data-ttu-id="7da43-216">Type van het volume voor de versleuteling wordt ondersteund</span><span class="sxs-lookup"><span data-stu-id="7da43-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="7da43-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7da43-217">Ubuntu</span></span> | <span data-ttu-id="7da43-218">16.04-DAGELIJKS-TNS</span><span class="sxs-lookup"><span data-stu-id="7da43-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="7da43-219">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-219">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7da43-220">Ubuntu</span></span> | <span data-ttu-id="7da43-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="7da43-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="7da43-222">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-222">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7da43-223">Ubuntu</span></span> | <span data-ttu-id="7da43-224">12.10</span><span class="sxs-lookup"><span data-stu-id="7da43-224">12.10</span></span> | <span data-ttu-id="7da43-225">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-225">Data disk</span></span> |
| <span data-ttu-id="7da43-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7da43-226">Ubuntu</span></span> | <span data-ttu-id="7da43-227">12.04</span><span class="sxs-lookup"><span data-stu-id="7da43-227">12.04</span></span> | <span data-ttu-id="7da43-228">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-228">Data disk</span></span> |
| <span data-ttu-id="7da43-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="7da43-229">RHEL</span></span> | <span data-ttu-id="7da43-230">7.3</span><span class="sxs-lookup"><span data-stu-id="7da43-230">7.3</span></span> | <span data-ttu-id="7da43-231">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-231">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="7da43-232">RHEL</span></span> | <span data-ttu-id="7da43-233">7.2</span><span class="sxs-lookup"><span data-stu-id="7da43-233">7.2</span></span> | <span data-ttu-id="7da43-234">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-234">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="7da43-235">RHEL</span></span> | <span data-ttu-id="7da43-236">6.8</span><span class="sxs-lookup"><span data-stu-id="7da43-236">6.8</span></span> | <span data-ttu-id="7da43-237">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-237">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="7da43-238">RHEL</span></span> | <span data-ttu-id="7da43-239">6.7</span><span class="sxs-lookup"><span data-stu-id="7da43-239">6.7</span></span> | <span data-ttu-id="7da43-240">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-240">Data disk</span></span> |
| <span data-ttu-id="7da43-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-241">CentOS</span></span> | <span data-ttu-id="7da43-242">7.3</span><span class="sxs-lookup"><span data-stu-id="7da43-242">7.3</span></span> | <span data-ttu-id="7da43-243">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-243">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-244">CentOS</span></span> | <span data-ttu-id="7da43-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="7da43-245">7.2n</span></span> | <span data-ttu-id="7da43-246">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-246">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-247">CentOS</span></span> | <span data-ttu-id="7da43-248">6.8</span><span class="sxs-lookup"><span data-stu-id="7da43-248">6.8</span></span> | <span data-ttu-id="7da43-249">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-249">OS and Data disk</span></span> |
| <span data-ttu-id="7da43-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-250">CentOS</span></span> | <span data-ttu-id="7da43-251">7.1</span><span class="sxs-lookup"><span data-stu-id="7da43-251">7.1</span></span> | <span data-ttu-id="7da43-252">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-252">Data disk</span></span> |
| <span data-ttu-id="7da43-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-253">CentOS</span></span> | <span data-ttu-id="7da43-254">7.0</span><span class="sxs-lookup"><span data-stu-id="7da43-254">7.0</span></span> | <span data-ttu-id="7da43-255">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-255">Data disk</span></span> |
| <span data-ttu-id="7da43-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-256">CentOS</span></span> | <span data-ttu-id="7da43-257">6.7</span><span class="sxs-lookup"><span data-stu-id="7da43-257">6.7</span></span> | <span data-ttu-id="7da43-258">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-258">Data disk</span></span> |
| <span data-ttu-id="7da43-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-259">CentOS</span></span> | <span data-ttu-id="7da43-260">6.6</span><span class="sxs-lookup"><span data-stu-id="7da43-260">6.6</span></span> | <span data-ttu-id="7da43-261">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-261">Data disk</span></span> |
| <span data-ttu-id="7da43-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="7da43-262">CentOS</span></span> | <span data-ttu-id="7da43-263">6.5</span><span class="sxs-lookup"><span data-stu-id="7da43-263">6.5</span></span> | <span data-ttu-id="7da43-264">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-264">Data disk</span></span> |
| <span data-ttu-id="7da43-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7da43-265">openSUSE</span></span> | <span data-ttu-id="7da43-266">13.2</span><span class="sxs-lookup"><span data-stu-id="7da43-266">13.2</span></span> | <span data-ttu-id="7da43-267">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-267">Data disk</span></span> |
| <span data-ttu-id="7da43-268">SLES</span><span class="sxs-lookup"><span data-stu-id="7da43-268">SLES</span></span> | <span data-ttu-id="7da43-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="7da43-269">12 SP1</span></span> | <span data-ttu-id="7da43-270">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-270">Data disk</span></span> |
| <span data-ttu-id="7da43-271">SLES</span><span class="sxs-lookup"><span data-stu-id="7da43-271">SLES</span></span> | <span data-ttu-id="7da43-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="7da43-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="7da43-273">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-273">Data disk</span></span> |
| <span data-ttu-id="7da43-274">SLES</span><span class="sxs-lookup"><span data-stu-id="7da43-274">SLES</span></span> | <span data-ttu-id="7da43-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="7da43-275">HPC 12</span></span> | <span data-ttu-id="7da43-276">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-276">Data disk</span></span> |
| <span data-ttu-id="7da43-277">SLES</span><span class="sxs-lookup"><span data-stu-id="7da43-277">SLES</span></span> | <span data-ttu-id="7da43-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="7da43-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="7da43-279">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-279">Data disk</span></span> |
| <span data-ttu-id="7da43-280">SLES</span><span class="sxs-lookup"><span data-stu-id="7da43-280">SLES</span></span> | <span data-ttu-id="7da43-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="7da43-281">11 SP4</span></span> | <span data-ttu-id="7da43-282">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="7da43-282">Data disk</span></span> |

* <span data-ttu-id="7da43-283">Azure Disk Encryption is vereist dat uw sleutelkluis en de virtuele machines zich in Hallo dezelfde bevinden Azure-regio en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="7da43-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-284">Hallo-resources configureren in afzonderlijke regio's zorgt ervoor dat een fout opgetreden bij het inschakelen van hello Azure Disk Encryption functie.</span><span class="sxs-lookup"><span data-stu-id="7da43-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="7da43-285">tooset omhoog en uw sleutelkluis configureren voor Azure Disk Encryption, Zie de sectie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in Hallo *vereisten* sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7da43-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="7da43-286">tooset omhoog en Azure AD-toepassing in Azure Active directory configureren voor Azure Disk Encryption, Zie de sectie **hello Azure AD-toepassing in Azure Active Directory instellen** in Hallo *vereisten* sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7da43-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="7da43-287">tooset omhoog en Hallo sleutelkluis toegangsbeleid voor de toepassing hello Azure AD configureren, Zie de sectie **hello sleutelkluis-beleid instellen voor de toepassing hello Azure AD** in Hallo *vereisten* sectie in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7da43-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="7da43-288">tooprepare een Windows-VHD vooraf zijn versleuteld, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Windows VHD** in Hallo *bijlage*.</span><span class="sxs-lookup"><span data-stu-id="7da43-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="7da43-289">tooprepare een vooraf zijn versleuteld Linux VHD, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Linux VHD** in Hallo *bijlage*.</span><span class="sxs-lookup"><span data-stu-id="7da43-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="7da43-290">Hello Azure-platform moet toegang toohello versleutelingssleutels of geheimen in uw sleutelkluis toomake ze beschikbaar toohello virtuele machine wanneer deze wordt opgestart en Hallo virtuele machine OS volume ontsleutelt.</span><span class="sxs-lookup"><span data-stu-id="7da43-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="7da43-291">toogrant machtigingen tooAzure platform, set Hallo **EnabledForDiskEncryption** eigenschap in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="7da43-292">Zie voor meer informatie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in Hallo bijlage.</span><span class="sxs-lookup"><span data-stu-id="7da43-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="7da43-293">Uw sleutelkluis geheim en de KEK-URL's moeten samengestelde zijn.</span><span class="sxs-lookup"><span data-stu-id="7da43-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="7da43-294">Azure zorgt ervoor dat deze beperking versiebeheer.</span><span class="sxs-lookup"><span data-stu-id="7da43-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="7da43-295">Zie Hallo volgen voorbeelden voor geldige geheim en KEK-URL's:</span><span class="sxs-lookup"><span data-stu-id="7da43-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="7da43-296">Voorbeeld van een geldige URL geheime: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="7da43-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="7da43-297">Voorbeeld van een geldige KEK-URL: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="7da43-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="7da43-298">Azure Disk Encryption biedt geen ondersteuning voor het opgeven van poortnummers als onderdeel van de sleutelkluis geheimen en KEK-URL's.</span><span class="sxs-lookup"><span data-stu-id="7da43-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="7da43-299">Zie voor voorbeelden van niet-ondersteunde en ondersteunde sleutelkluis-URL's Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7da43-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="7da43-300">Onaanvaardbaar sleutelkluis-URL *https://contosovault.vault.azure.net:443/geheimen/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="7da43-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="7da43-301">Acceptabele sleutelkluis-URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="7da43-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="7da43-302">tooenable hello Azure Disk Encryption functie Hallo IaaS VM's moet voldoen aan Hallo netwerkvereisten endpoint-configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="7da43-303">een token tooconnect tooyour sleutelkluis, Hallo IaaS VM tooget moet kunnen tooconnect tooan Azure Active Directory-eindpunt \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="7da43-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="7da43-304">toowrite hello versleuteling sleutels tooyour sleutelkluis, Hallo IaaS VM moet kunnen tooconnect toohello sleutelkluis-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="7da43-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="7da43-305">Hallo IaaS VM moet kunnen tooconnect tooan Azure storage-eindpunt dat hosts Hallo extensie Azure-opslagplaats en Azure storage-account dat hosts Hallo VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7da43-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7da43-306">Als uw beveiligingsbeleid beperkt de toegang van Azure Virtual machines toohello Internet, kunt u oplossen Hallo voorafgaand aan de URI en configureren van een specifieke regel tooallow uitgaande verbinding toohello IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="7da43-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="7da43-307">tooconfigure en toegang tot Azure Key Vault achter een firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="7da43-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="7da43-308">Hallo meest recente versie van Azure PowerShell SDK versie tooconfigure Azure Disk Encryption gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7da43-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="7da43-309">Download de nieuwste versie Hallo van [Azure PowerShell-versie](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="7da43-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="7da43-310">Azure Disk Encryption wordt niet ondersteund op [Azure PowerShell SDK-versie 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="7da43-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="7da43-311">Als er een fout gerelateerd toousing Azure PowerShell 1.1.0, Zie [Azure schijf versleuteling fout gerelateerde tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="7da43-312">toorun willekeurige opdracht van de Azure CLI en deze koppelen aan uw Azure-abonnement, moet u eerst Azure CLI installeren:</span><span class="sxs-lookup"><span data-stu-id="7da43-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="7da43-313">tooinstall Azure CLI en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7da43-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="7da43-314">Zie toouse Azure CLI voor Mac, Linux en Windows gebruiken met Azure Resource Manager [Azure CLI-opdrachten in de modus Resource Manager](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="7da43-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="7da43-315">Bij het versleutelen van een beheerde schijf is een momentopname van Hallo beheerd schijf of een back-up van schijf Hallo buiten Azure Disk Encryption voorafgaande tooenabling versleuteling verplicht vereiste tootake.</span><span class="sxs-lookup"><span data-stu-id="7da43-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="7da43-316">Zonder een back-up in plaats kan een onverwachte fout opgetreden tijdens het versleutelen weergeven Hallo schijf en de VM toegankelijk zijn zonder een hersteloptie.</span><span class="sxs-lookup"><span data-stu-id="7da43-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="7da43-317">Set AzureRmVMDiskEncryptionExtension momenteel geen back-up beheerde schijven en wordt fout als op een beheerde schijf gebruikt, tenzij het Hallo - skipVmBackup parameter is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="7da43-318">Deze parameter is onveilige toouse tenzij buiten Azure Disk Encryption al een back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7da43-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="7da43-319">Wanneer het Hallo - skipVmBackup parameter wordt opgegeven, wordt Hallo cmdlet een back-ups van eerdere tooencryption van Hallo beheerde schijf niet maken.</span><span class="sxs-lookup"><span data-stu-id="7da43-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="7da43-320">Daarom wordt het beschouwd als een verplichte vereisten toomake zeker van te zijn dat een back-up van de beheerde schijf Hallo die VM bevindt zich in de plaats voorafgaande tooenabling Azure Disk Encryption als herstel hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="7da43-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="7da43-321">Hallo - skipVmBackup parameter mag nooit worden gebruikt tenzij een momentopname of een back-up al is gemaakt buiten Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="7da43-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="7da43-322">Hallo BitLocker externe-sleutelbeveiliging Hello Azure Disk Encryption oplossing gebruikt voor IaaS VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="7da43-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="7da43-323">Push Groepsbeleid dat TPM beveiligingen afdwingen voor domein gekoppelde virtuele machines, niet.</span><span class="sxs-lookup"><span data-stu-id="7da43-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="7da43-324">Zie voor meer informatie over Groepsbeleid Hallo voor 'Toestaan dat BitLocker zonder een compatibele TPM' [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="7da43-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="7da43-325">BitLocker-Groepsbeleid op virtuele machines die lid van domein voor de aangepaste Hallo instelling na moet bevatten: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption mislukken wanneer aangepaste groepsbeleidsinstellingen voor Bitlocker niet compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="7da43-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="7da43-326">Op computers die geen Hallo juist beleidsinstelling Hallo nieuw beleid toepassen forceren Hallo nieuw beleid tooupdate (gpupdate.exe/Force) en start vervolgens opnieuw mogelijk vereist.</span><span class="sxs-lookup"><span data-stu-id="7da43-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="7da43-327">toocreate een Azure AD-toepassing een sleutelkluis maken of een bestaande sleutelkluis instellen en versleuteling inschakelen, raadpleegt u Hallo [vereiste PowerShell-script voor Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="7da43-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="7da43-328">Zie tooconfigure schijfversleuteling vereisten hello Azure CLI met [dit script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7da43-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="7da43-329">toouse hello Azure Backup-service tooback up en herstel versleuteld virtuele machines, als versleuteling is ingeschakeld met Azure Disk Encryption versleutelen van uw virtuele machines met hello Azure Disk Encryption key configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da43-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="7da43-330">Hallo Backup-service biedt ondersteuning voor virtuele machines die zijn versleuteld met alleen een KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da43-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="7da43-331">Zie [tooback up en herstel versleuteld hoe virtuele machines met Azure Backup-versleuteling](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="7da43-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="7da43-332">Bij het versleutelen van een volume met het Linux-besturingssysteem, houd er rekening mee dat VM moet worden opgestart momenteel achter Hallo Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="7da43-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="7da43-333">Dit kan worden gedaan via Hallo-portal, powershell of CLI.</span><span class="sxs-lookup"><span data-stu-id="7da43-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="7da43-334">tootrack hello voortgang van de versleuteling, pollen periodiek Hallo-statusbericht dat is geretourneerd door Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="7da43-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="7da43-335">Zodra de codering is voltooid, wordt dit door Hallo Hallo-statusbericht geretourneerd door deze opdracht aangegeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="7da43-336">Bijvoorbeeld ' ProgressMessage: besturingssysteemschijf is versleuteld, start opnieuw op Hallo VM ' op dit punt Hallo VM kan worden gestart en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da43-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="7da43-337">Azure Disk Encryption voor Linux moet gegevens schijven toohave een gekoppeld bestandssysteem in de voorafgaande tooencryption Linux</span><span class="sxs-lookup"><span data-stu-id="7da43-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="7da43-338">Recursief gekoppelde schijven worden niet ondersteund door Azure Disk Encryption Hallo voor Linux.</span><span class="sxs-lookup"><span data-stu-id="7da43-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="7da43-339">Bijvoorbeeld, als hello doelsysteem een schijf is gekoppeld op /foo/bar en slaagt op /foo/bar/baz, Hallo versleuteling van /foo/bar/baz, maar versleuteling van foo/balk zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="7da43-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="7da43-340">Azure Disk Encryption wordt alleen ondersteund op Azure-galerie ondersteund installatiekopieën die voldoen aan de hiervoor genoemde Hallo-vereisten.</span><span class="sxs-lookup"><span data-stu-id="7da43-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="7da43-341">Klanten aangepaste installatiekopieën worden niet ondersteund vanwege toocustom partitieschema's en het proces gedrag die op deze installatiekopieën kunnen bestaan.</span><span class="sxs-lookup"><span data-stu-id="7da43-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="7da43-342">Bovendien is zelfs afbeelding op basis van de virtuele machine die in eerste instantie vereisten wordt voldaan, maar zijn gewijzigd nadat het maken van zijn mogelijk niet compatibel.</span><span class="sxs-lookup"><span data-stu-id="7da43-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="7da43-343">Voor dat reden Hallo procedure aanbevolen voor het versleutelen van een Linux-VM is toostart vanuit een schone afbeelding, versleutelen Hallo VM en voeg vervolgens aangepaste software of gegevens toohello VM indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7da43-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="7da43-344">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met Hallo KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da43-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="7da43-345">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="7da43-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="7da43-346">KEK-sleutel is een optionele parameter waarmee de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="7da43-347">Hallo ingesteld met Azure AD-toepassing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da43-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="7da43-348">Wanneer u versleuteling toobe ingeschakeld op een actieve virtuele machine in Azure, wordt Azure Disk Encryption genereert en schrijft Hallo versleuteling sleutels tooyour sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="7da43-349">Het beheren van versleutelingssleutels in de sleutelkluis vereist Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="7da43-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="7da43-350">Maak een Azure AD-toepassing voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="7da43-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="7da43-351">U vindt gedetailleerde stappen voor het registreren van een toepassing in 'Een identiteit voor de toepassing hello ophalen' Hallo-sectie van Hallo blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="7da43-352">Dit bericht bevat ook een aantal handige voorbeelden voor het instellen en configureren van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="7da43-353">U kunt op basis van een geheim clientverificatie of clientverificatie Azure AD op basis van certificaten gebruiken voor verificatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="7da43-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="7da43-354">Clientverificatie op basis van een geheim voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da43-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="7da43-355">Hallo secties kunt u een client geheim gebaseerde verificatie voor Azure AD configureren.</span><span class="sxs-lookup"><span data-stu-id="7da43-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="7da43-356">Een Azure AD-toepassing maken met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7da43-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="7da43-357">Gebruik de volgende PowerShell-cmdlet toocreate een Azure AD-toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="7da43-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="7da43-358">$azureAdApplication.ApplicationId hello Azure AD ClientID en $aadClientSecret Hallo-clientgeheim dat u later tooenable Azure Disk Encryption moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7da43-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="7da43-359">Geheim hello Azure AD-client op de juiste wijze beveiligt.</span><span class="sxs-lookup"><span data-stu-id="7da43-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="7da43-360">Hello Azure AD-client-ID en geheim instellen vanuit de klassieke Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="7da43-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="7da43-361">U kunt ook van uw Azure AD-client-ID en geheim instellen met behulp van Hallo [klassieke Azure-portal]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7da43-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="7da43-362">tooperform dit taak Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="7da43-363">Klik op Hallo **Active Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7da43-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="7da43-365">Klik op **toepassing toevoegen**, en vervolgens type Hallo toepassingsnaam.</span><span class="sxs-lookup"><span data-stu-id="7da43-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="7da43-367">Klik op de knop pijl Hallo en configureer vervolgens de toepassingseigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="7da43-369">Klik op het vinkje Hallo in Hallo lager zijn linkerhoek toofinish.</span><span class="sxs-lookup"><span data-stu-id="7da43-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="7da43-370">configuratiepagina Hallo-toepassing wordt weergegeven en hello Azure AD-client-ID wordt weergegeven aan de onderkant Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="7da43-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="7da43-372">Hello Azure AD-clientgeheim opslaan door te klikken op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7da43-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="7da43-373">Houd er rekening mee clientgeheim hello Azure AD in Hallo sleutels tekstvak.</span><span class="sxs-lookup"><span data-stu-id="7da43-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="7da43-374">Op de juiste wijze beveiligt.</span><span class="sxs-lookup"><span data-stu-id="7da43-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="7da43-376">Hallo voorafgaand aan de stroom wordt niet ondersteund op Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7da43-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="7da43-377">Gebruik een bestaande toepassing</span><span class="sxs-lookup"><span data-stu-id="7da43-377">Use an existing application</span></span>
<span data-ttu-id="7da43-378">tooexecute Hallo van de volgende opdrachten, downloaden en gebruiken van Hallo [Azure AD PowerShell-module](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-379">Hallo moeten volgende opdrachten worden uitgevoerd vanuit een nieuwe PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="7da43-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="7da43-380">Gebruik geen Azure PowerShell of Azure Resource Manager Hallo tooexecute Hallo opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7da43-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="7da43-381">Deze aanpak wordt aangeraden omdat deze cmdlets in Hallo MSOnline module of Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7da43-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="7da43-382">Verificatie op basis van certificaten voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da43-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="7da43-383">Azure AD gebaseerde verificatie is momenteel niet ondersteund op virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7da43-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="7da43-384">Hallo secties tonen hoe tooconfigure een op certificaten gebaseerde verificatie voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da43-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="7da43-385">Een Azure AD-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="7da43-385">Create an Azure AD application</span></span>
<span data-ttu-id="7da43-386">toocreate een Azure AD-toepassing hello volgende PowerShell-cmdlets uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7da43-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-387">Vervang de volgende Hallo `yourpassword` tekenreeks met beveiligd wachtwoord en beveiliging Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7da43-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="7da43-388">Nadat u deze stap hebt voltooid, uploaden van een sleutelkluis voor PFX-bestand tooyour en Hallo toegang beleid nodig toodeploy dat certificaat tooa VM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7da43-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="7da43-389">Gebruik een bestaande Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="7da43-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="7da43-390">Als u verificatie op basis van certificaten voor een bestaande toepassing configureren wilt, gebruikt u Hallo PowerShell-cmdlets die hier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="7da43-391">Ervoor tooexecute worden van een nieuwe PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="7da43-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="7da43-392">Nadat u deze stap hebt voltooid, uploaden van een sleutelkluis voor PFX-bestand tooyour en Hallo toegangsbeleid dat nodig is toodeploy Hallo certificaat tooa VM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7da43-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="7da43-393">Een sleutelkluis voor PFX-bestand tooyour uploaden</span><span class="sxs-lookup"><span data-stu-id="7da43-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="7da43-394">Zie voor een gedetailleerde uitleg van dit proces [Hallo officiële Azure Key Vault-teamblog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="7da43-395">Hallo volgende PowerShell-cmdlets zijn echter alles wat die u nodig hebt voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="7da43-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="7da43-396">Worden ervoor tooexecute van Azure PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="7da43-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-397">Vervang de volgende Hallo `yourpassword` tekenreeks met beveiligd wachtwoord en beveiliging Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7da43-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="7da43-398">Een certificaat in uw sleutelkluis tooan bestaande virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="7da43-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="7da43-399">Nadat u Hallo PFX uploaden, moet u een certificaat in Hallo sleutelkluis tooan bestaande virtuele machine met de volgende Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="7da43-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="7da43-400">Hallo sleutelkluis-beleid voor hello Azure AD-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="7da43-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="7da43-401">Uw Azure AD-toepassing moet rechten tooaccess Hallo sleutels of geheimen in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="7da43-402">Gebruik Hallo [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant machtigingen toohello toepassing, Hallo client-ID (die is gegenereerd toen de toepassing hello is geregistreerd) als Hallo _– ServicePrincipalName_ waarde voor parameter.</span><span class="sxs-lookup"><span data-stu-id="7da43-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="7da43-403">toolearn Zie meer Hallo blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="7da43-404">Hier volgt een voorbeeld van hoe tooperform dit taak PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7da43-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="7da43-405">Azure Disk Encryption, moet u tooconfigure Hallo toegang beleid tooyour Azure AD-clienttoepassing te volgen: _WrapKey_ en _ingesteld_ machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7da43-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="7da43-406">Terminologie</span><span class="sxs-lookup"><span data-stu-id="7da43-406">Terminology</span></span>
<span data-ttu-id="7da43-407">toounderstand aantal algemene termen Hallo gebruikt door deze technologie, gebruik Hallo volgende terminologie tabel:</span><span class="sxs-lookup"><span data-stu-id="7da43-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="7da43-408">Terminologie</span><span class="sxs-lookup"><span data-stu-id="7da43-408">Terminology</span></span> | <span data-ttu-id="7da43-409">Definitie</span><span class="sxs-lookup"><span data-stu-id="7da43-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da43-410">Azure AD</span></span> | <span data-ttu-id="7da43-411">Azure AD [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="7da43-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="7da43-412">Een Azure AD-account is een vereiste voor verificatie, opslaan en ophalen van geheimen van een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="7da43-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7da43-413">Azure Key Vault</span></span> | <span data-ttu-id="7da43-414">Sleutelkluis is een cryptografische, key management service die gebaseerd op de Federal Information Processing Standards FIPS-gevalideerde hardware security modules, die ter bescherming van uw cryptografische sleutels en geheimen gevoelige.</span><span class="sxs-lookup"><span data-stu-id="7da43-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="7da43-415">Zie voor meer informatie [Sleutelkluis](https://azure.microsoft.com/services/key-vault/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="7da43-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="7da43-416">ARM</span><span class="sxs-lookup"><span data-stu-id="7da43-416">ARM</span></span> | <span data-ttu-id="7da43-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7da43-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="7da43-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="7da43-418">BitLocker</span></span> |<span data-ttu-id="7da43-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is een industrie herkend Windows volume versleuteling technologie die tooenable schijfversleuteling op IaaS VM's van Windows is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da43-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="7da43-420">BEK</span><span class="sxs-lookup"><span data-stu-id="7da43-420">BEK</span></span> | <span data-ttu-id="7da43-421">BitLocker-versleutelingssleutels zijn gebruikte tooencrypt Hallo OS opstartvolume en gegevensvolumes.</span><span class="sxs-lookup"><span data-stu-id="7da43-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="7da43-422">Hallo BitLocker-sleutels worden beveiligd in een sleutelkluis als geheimen.</span><span class="sxs-lookup"><span data-stu-id="7da43-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="7da43-423">CLI</span><span class="sxs-lookup"><span data-stu-id="7da43-423">CLI</span></span> | <span data-ttu-id="7da43-424">Zie [Azure-opdrachtregelinterface](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7da43-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="7da43-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="7da43-425">DM-Crypt</span></span> |<span data-ttu-id="7da43-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is Hallo op basis van Linux, transparant schijfversleuteling subsysteem tooenable schijfversleuteling op Linux IaaS VM's is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da43-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="7da43-427">KEK</span><span class="sxs-lookup"><span data-stu-id="7da43-427">KEK</span></span> | <span data-ttu-id="7da43-428">Sleutelcodering sleutel is Hallo asymmetrische sleutel (RSA 2048) tooprotect gebruiken of Hallo geheim teruglopen.</span><span class="sxs-lookup"><span data-stu-id="7da43-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="7da43-429">U kunt bieden een hardware security modules (HSM)-sleutel of met software beschermde sleutel beveiligd.</span><span class="sxs-lookup"><span data-stu-id="7da43-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="7da43-430">Zie voor meer informatie [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="7da43-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="7da43-431">PS-cmdlets</span><span class="sxs-lookup"><span data-stu-id="7da43-431">PS cmdlets</span></span> | <span data-ttu-id="7da43-432">Zie [Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7da43-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="7da43-433">Installeren en configureren van de sleutelkluis voor Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="7da43-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="7da43-434">Azure Disk Encryption helpt de Hallo schijfversleuteling sleutels en geheimen in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="7da43-435">tooset van de sleutelkluis voor Azure Disk Encryption voltooid Hallo stappen voor elk Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7da43-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="7da43-436">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="7da43-436">Create a key vault</span></span>
<span data-ttu-id="7da43-437">een sleutelkluis toocreate gebruik een van Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="7da43-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="7da43-438">Resource Manager-sjabloon '101-sleutel-kluis-maken'</span><span class="sxs-lookup"><span data-stu-id="7da43-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="7da43-439">Azure PowerShell-cmdlets voor sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="7da43-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="7da43-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7da43-440">Azure Resource Manager</span></span>
* <span data-ttu-id="7da43-441">Hoe te[beveiligen van uw sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="7da43-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-442">Als u hebt al een sleutelkluis ingesteld voor uw abonnement, slaat u de volgende sectie toohello.</span><span class="sxs-lookup"><span data-stu-id="7da43-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="7da43-444">Instellen van een coderingssleutel voor de sleutel (optioneel)</span><span class="sxs-lookup"><span data-stu-id="7da43-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="7da43-445">Als u toouse een KEK-sleutel voor een extra beveiligingslaag voor Hallo BitLocker versleutelingssleutels wilt, voegt u een KEK tooyour-sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="7da43-446">Gebruik Hallo [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate een sleutel sleutelcodering in Hallo sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="7da43-447">U kunt ook een KEK importeren uit uw lokale Sleutelbeheer HSM.</span><span class="sxs-lookup"><span data-stu-id="7da43-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="7da43-448">Zie voor meer informatie [Sleutelkluis documentatie](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="7da43-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="7da43-449">U kunt Hallo KEK toevoegen door te gaan tooAzure Resource Manager of met behulp van de sleutelkluis-interface.</span><span class="sxs-lookup"><span data-stu-id="7da43-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="7da43-451">Sleutelkluis-machtigingen instellen</span><span class="sxs-lookup"><span data-stu-id="7da43-451">Set key vault permissions</span></span>
<span data-ttu-id="7da43-452">Hello Azure-platform moet toegang toohello versleutelingssleutels of geheimen in uw sleutelkluis toomake ze beschikbaar toohello VM voor het opstarten en ontsleutelen van Hallo volumes.</span><span class="sxs-lookup"><span data-stu-id="7da43-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="7da43-453">toogrant machtigingen toohello Azure-platform set Hallo **EnabledForDiskEncryption** eigenschap in Hallo key vault via Hallo sleutelkluis PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7da43-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="7da43-454">U kunt ook instellen Hallo **EnabledForDiskEncryption** eigenschap via Hallo [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7da43-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="7da43-455">Zoals eerder vermeld, moet u instellen Hallo **EnabledForDiskEncryption** eigenschap in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="7da43-456">Anders mislukt Hallo implementatie.</span><span class="sxs-lookup"><span data-stu-id="7da43-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="7da43-457">U kunt beleidsregels voor toegang instellen voor uw Azure AD-toepassing van de interface van de sleutelkluis hello, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7da43-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="7da43-460">Op Hallo **geavanceerde toegangsbeleid** tabblad, zorg ervoor dat de sleutelkluis voor Azure Disk Encryption is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="7da43-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure sleutelkluis](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="7da43-462">Implementatiescenario's voor schijf-codering en gebruikerservaringen</span><span class="sxs-lookup"><span data-stu-id="7da43-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="7da43-463">Kunt u veel scenario's voor schijf-codering inschakelen en Hallo stappen kunnen variëren volgens toohello scenario.</span><span class="sxs-lookup"><span data-stu-id="7da43-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="7da43-464">Hallo volgende secties wordt beschreven Hallo scenario's met meer details.</span><span class="sxs-lookup"><span data-stu-id="7da43-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="7da43-465">Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="7da43-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="7da43-466">U kunt schijfversleuteling op de nieuwe IaaS virtuele machine van Windows uit Hallo Marketplace in Azure inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="7da43-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="7da43-467">Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da43-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="7da43-468">Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op een nieuwe IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-469">Deze sjabloon maakt een nieuwe versleutelde Windows virtuele machine die gebruikmaakt van Windows Server 2012 Hallo afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7da43-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="7da43-470">U kunt schijfversleuteling op een nieuwe IaaS RedHat Linux 7.2 virtuele machine met een matrix van 200 GB RAID-0 inschakelen met behulp van dit [Resource Manager-sjabloon](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="7da43-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="7da43-471">Nadat u de sjabloon Hallo hebt geïmplementeerd, Hallo VM versleutelingsstatus controleren via Hallo `Get-AzureRmVmDiskEncryptionStatus` cmdlet, zoals beschreven in [OS versleutelen station op een actieve Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="7da43-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="7da43-472">Wanneer Hallo machine status retourneert _VMRestartPending_, Hallo VM starten.</span><span class="sxs-lookup"><span data-stu-id="7da43-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="7da43-473">Hallo volgende tabel bevat Hallo Resource Manager-Sjabloonparameters voor nieuwe virtuele machines van Hallo Marketplace scenario met behulp van Azure AD-client-ID:</span><span class="sxs-lookup"><span data-stu-id="7da43-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="7da43-474">Parameter</span><span class="sxs-lookup"><span data-stu-id="7da43-474">Parameter</span></span> | <span data-ttu-id="7da43-475">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7da43-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="7da43-476">adminUserName</span></span> | <span data-ttu-id="7da43-477">De beheerdersgebruikersnaam voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="7da43-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="7da43-478">adminPassword</span></span> | <span data-ttu-id="7da43-479">Beheerderswachtwoord voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="7da43-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="7da43-480">newStorageAccountName</span></span> | <span data-ttu-id="7da43-481">Naam van Hallo storage account toostore OS en gegevens VHD's.</span><span class="sxs-lookup"><span data-stu-id="7da43-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="7da43-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="7da43-482">vmSize</span></span> | <span data-ttu-id="7da43-483">Grootte van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-483">Size of hello VM.</span></span> <span data-ttu-id="7da43-484">Op dit moment worden alleen standaard A, D en G reeksen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="7da43-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="7da43-485">virtualNetworkName</span></span> | <span data-ttu-id="7da43-486">Naam van de VNet die Hallo VM NIC Hallo moet bij horen.</span><span class="sxs-lookup"><span data-stu-id="7da43-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="7da43-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="7da43-487">subnetName</span></span> | <span data-ttu-id="7da43-488">Naam van het subnet in VNet dat Hallo VM NIC Hallo Hallo moet bij horen.</span><span class="sxs-lookup"><span data-stu-id="7da43-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="7da43-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="7da43-489">AADClientID</span></span> | <span data-ttu-id="7da43-490">Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="7da43-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="7da43-491">AADClientSecret</span></span> | <span data-ttu-id="7da43-492">Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="7da43-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="7da43-493">keyVaultURL</span></span> | <span data-ttu-id="7da43-494">URL van Hallo key vault die Hallo BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="7da43-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="7da43-495">U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="7da43-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="7da43-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="7da43-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="7da43-497">URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo gegenereerd BitLocker-sleutel (optioneel).</span><span class="sxs-lookup"><span data-stu-id="7da43-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="7da43-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7da43-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="7da43-499">De resourcegroep van de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="7da43-500">vmName</span><span class="sxs-lookup"><span data-stu-id="7da43-500">vmName</span></span> | <span data-ttu-id="7da43-501">Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="7da43-502">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="7da43-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="7da43-503">U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheime wachtwoordzin) zetten in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="7da43-504">Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van de klant versleuteld VHD- en versleutelingssleutels</span><span class="sxs-lookup"><span data-stu-id="7da43-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="7da43-505">In dit scenario kunt u inschakelen versleutelen met behulp van Resource Manager-sjabloon hello, PowerShell-cmdlets of CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7da43-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="7da43-506">Hallo volgende secties wordt uitgelegd in meer detail Hallo Resource Manager-sjabloon en de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7da43-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="7da43-507">Hallo instructies volgt in een van deze secties voor het voorbereiden van vooraf zijn versleuteld afbeeldingen die kunnen worden gebruikt in Azure.</span><span class="sxs-lookup"><span data-stu-id="7da43-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="7da43-508">Nadat het Hallo-installatiekopie is gemaakt, kunt u stappen Hallo in Hallo volgende sectie toocreate een versleutelde Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="7da43-509">Een vooraf zijn versleuteld Windows VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7da43-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="7da43-510">Een vooraf zijn versleuteld Linux VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7da43-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="7da43-511">Hallo Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="7da43-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="7da43-512">U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="7da43-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="7da43-513">Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da43-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="7da43-514">Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo nieuwe IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="7da43-515">Hallo volgende tabel bevat Hallo Resource Manager-Sjabloonparameters voor uw versleutelde VHD:</span><span class="sxs-lookup"><span data-stu-id="7da43-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="7da43-516">Parameter</span><span class="sxs-lookup"><span data-stu-id="7da43-516">Parameter</span></span> | <span data-ttu-id="7da43-517">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7da43-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="7da43-518">newStorageAccountName</span></span> | <span data-ttu-id="7da43-519">Naam van Hallo storage account toostore Hallo versleuteld OS VHD.</span><span class="sxs-lookup"><span data-stu-id="7da43-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="7da43-520">Dit opslagaccount moet al zijn gemaakt in Hallo dezelfde resourcegroep en dezelfde locatie als Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="7da43-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="7da43-521">osVhdUri</span></span> | <span data-ttu-id="7da43-522">De URI van Hallo OS VHD van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="7da43-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="7da43-523">besturingssysteemtype</span><span class="sxs-lookup"><span data-stu-id="7da43-523">osType</span></span> | <span data-ttu-id="7da43-524">Type besturingssysteem product (Windows of Linux).</span><span class="sxs-lookup"><span data-stu-id="7da43-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="7da43-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="7da43-525">virtualNetworkName</span></span> | <span data-ttu-id="7da43-526">Naam van de VNet die Hallo VM NIC Hallo moet bij horen.</span><span class="sxs-lookup"><span data-stu-id="7da43-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="7da43-527">Hallo naam moet al zijn gemaakt in Hallo dezelfde resourcegroep en dezelfde locatie als Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="7da43-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="7da43-528">subnetName</span></span> | <span data-ttu-id="7da43-529">Naam van het Hallo-subnet op Hallo VNet dat Hallo VM NIC moet bij horen.</span><span class="sxs-lookup"><span data-stu-id="7da43-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="7da43-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="7da43-530">vmSize</span></span> | <span data-ttu-id="7da43-531">Grootte van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-531">Size of hello VM.</span></span> <span data-ttu-id="7da43-532">Op dit moment worden alleen standaard A, D en G reeksen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7da43-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="7da43-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="7da43-533">keyVaultResourceID</span></span> | <span data-ttu-id="7da43-534">Hallo ResourceID waarmee Hallo sleutelkluisresource in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7da43-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="7da43-535">U kunt dit downloaden met behulp van PowerShell-cmdlet Hallo `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="7da43-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="7da43-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="7da43-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="7da43-537">De URL van Hallo schijfversleuteling sleutel die ingesteld in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="7da43-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="7da43-538">keyVaultKekUrl</span></span> | <span data-ttu-id="7da43-539">URL van Hallo sleutelcodering sleutel voor het coderen van Hallo gegenereerd versleutelingssleutel op de schijf.</span><span class="sxs-lookup"><span data-stu-id="7da43-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="7da43-540">vmName</span><span class="sxs-lookup"><span data-stu-id="7da43-540">vmName</span></span> | <span data-ttu-id="7da43-541">Naam van Hallo IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="7da43-542">Met behulp van PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="7da43-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="7da43-543">U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van PowerShell-cmdlet Hallo [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="7da43-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="7da43-544">CLI-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="7da43-544">Using CLI commands</span></span>
<span data-ttu-id="7da43-545">schijfversleuteling tooenable voor dit scenario met behulp van de CLI-opdrachten Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="7da43-546">Toegangsbeleid instellen in de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="7da43-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="7da43-547">Set Hallo **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="7da43-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="7da43-548">Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="7da43-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="7da43-549">tooenable versleuteling op een bestaande of actieve virtuele machine, type:</span><span class="sxs-lookup"><span data-stu-id="7da43-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="7da43-550">Versleutelingsstatus ophalen:</span><span class="sxs-lookup"><span data-stu-id="7da43-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="7da43-551">versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="7da43-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="7da43-552">Schakel versleuteling in op de bestaande of IaaS virtuele Windows-machine in Azure wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="7da43-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="7da43-553">In dit scenario kunt u inschakelen versleutelen met behulp van Resource Manager-sjabloon hello, PowerShell-cmdlets of CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7da43-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="7da43-554">Hallo volgende secties wordt uitgelegd in meer detail hoe deze met behulp van Resource Manager-sjabloon en de CLI-opdrachten Hallo tooenable.</span><span class="sxs-lookup"><span data-stu-id="7da43-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="7da43-555">Hallo Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="7da43-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="7da43-556">U kunt schijfversleuteling op de bestaande of IaaS VM's van Windows worden uitgevoerd in Azure met behulp van Hallo inschakelen [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="7da43-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="7da43-557">Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo versleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da43-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="7da43-558">Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo van bestaande of IaaS VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="7da43-559">Hallo bevat volgende tabel Hallo Resource Manager-Sjabloonparameters voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="7da43-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="7da43-560">Parameter</span><span class="sxs-lookup"><span data-stu-id="7da43-560">Parameter</span></span> | <span data-ttu-id="7da43-561">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7da43-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="7da43-562">AADClientID</span></span> | <span data-ttu-id="7da43-563">Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="7da43-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="7da43-564">AADClientSecret</span></span> | <span data-ttu-id="7da43-565">Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="7da43-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="7da43-566">keyVaultName</span></span> | <span data-ttu-id="7da43-567">Naam van de sleutel Hallo kluis die Hallo BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="7da43-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="7da43-568">U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="7da43-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="7da43-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="7da43-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="7da43-570">URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo BitLocker-sleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="7da43-571">Deze parameter is optioneel als u selecteert **nokek** in Hallo UseExistingKek vervolgkeuze-lijst.</span><span class="sxs-lookup"><span data-stu-id="7da43-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="7da43-572">Als u selecteert **kek** in de lijst vervolgkeuzelijst UseExistingKek hello, moet u Hallo _keyEncryptionKeyURL_ waarde.</span><span class="sxs-lookup"><span data-stu-id="7da43-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="7da43-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="7da43-573">volumeType</span></span> | <span data-ttu-id="7da43-574">Het type van het volume dat Hallo coderingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="7da43-575">Geldige waarden zijn _OS_, _gegevens_, en _alle_.</span><span class="sxs-lookup"><span data-stu-id="7da43-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="7da43-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="7da43-576">sequenceVersion</span></span> | <span data-ttu-id="7da43-577">Versie van de reeks van Hallo BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="7da43-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="7da43-578">Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op Hallo dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="7da43-579">vmName</span><span class="sxs-lookup"><span data-stu-id="7da43-579">vmName</span></span> | <span data-ttu-id="7da43-580">Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="7da43-581">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="7da43-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="7da43-582">U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheim BitLocker-versleuteling) in de sleutelkluis Hallo zetten.</span><span class="sxs-lookup"><span data-stu-id="7da43-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="7da43-583">Met behulp van PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="7da43-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="7da43-584">Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets Hallo blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="7da43-585">CLI-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="7da43-585">Using CLI commands</span></span>
<span data-ttu-id="7da43-586">tooenable versleuteling op bestaande of IaaS virtuele machine van Windows worden uitgevoerd in Azure CLI-opdrachten met Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="7da43-587">toegangsbeleid in de sleutelkluis hello tooset:</span><span class="sxs-lookup"><span data-stu-id="7da43-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="7da43-588">Set Hallo **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="7da43-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="7da43-589">Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="7da43-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="7da43-590">tooenable versleuteling op een bestaande of actieve virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="7da43-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="7da43-591">de coderingsstatus tooget:</span><span class="sxs-lookup"><span data-stu-id="7da43-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="7da43-592">versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="7da43-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="7da43-593">Schakel versleuteling in op een bestaande of actief IaaS virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="7da43-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="7da43-594">U kunt schijfversleuteling op een bestaande of actief IaaS virtuele Linux-machine in Azure inschakelen met behulp van Hallo [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="7da43-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="7da43-595">Klik op **implementeren tooAzure** hello Azure snel starten-sjabloon, Voer Hallo versleuteling configuratie op Hallo **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da43-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="7da43-596">Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op Hallo van bestaande of IaaS VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="7da43-597">Hallo volgende tabel geeft een lijst van Resource Manager-Sjabloonparameters voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="7da43-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="7da43-598">Parameter</span><span class="sxs-lookup"><span data-stu-id="7da43-598">Parameter</span></span> | <span data-ttu-id="7da43-599">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7da43-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="7da43-600">AADClientID</span></span> | <span data-ttu-id="7da43-601">Client-ID van hello Azure AD-toepassing die machtigingen toowrite geheimen toohello sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="7da43-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="7da43-602">AADClientSecret</span></span> | <span data-ttu-id="7da43-603">Clientgeheim van hello Azure AD-toepassing die machtigingen toowrite geheimen tooyour sleutelkluis heeft.</span><span class="sxs-lookup"><span data-stu-id="7da43-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="7da43-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="7da43-604">keyVaultName</span></span> | <span data-ttu-id="7da43-605">Naam van de sleutel Hallo kluis die Hallo BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="7da43-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="7da43-606">U kunt dit downloaden met behulp van de cmdlet Hallo `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="7da43-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="7da43-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="7da43-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="7da43-608">URL van Hallo sleutel versleutelingssleutel die wordt gebruikt tooencrypt Hallo BitLocker-sleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="7da43-609">Deze parameter is optioneel als u selecteert **nokek** in Hallo UseExistingKek vervolgkeuze-lijst.</span><span class="sxs-lookup"><span data-stu-id="7da43-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="7da43-610">Als u selecteert **kek** in de lijst vervolgkeuzelijst UseExistingKek hello, moet u Hallo _keyEncryptionKeyURL_ waarde.</span><span class="sxs-lookup"><span data-stu-id="7da43-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="7da43-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="7da43-611">volumeType</span></span> | <span data-ttu-id="7da43-612">Het type van het volume dat Hallo coderingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="7da43-613">Geldige ondersteunde waarden zijn _OS_ of _alle_ (voor RHEL 7.2, CentOS 7.2 en Ubuntu 16.04) en _gegevens_ (voor alle andere distributies).</span><span class="sxs-lookup"><span data-stu-id="7da43-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="7da43-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="7da43-614">sequenceVersion</span></span> | <span data-ttu-id="7da43-615">Versie van de reeks van Hallo BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="7da43-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="7da43-616">Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op Hallo dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="7da43-617">vmName</span><span class="sxs-lookup"><span data-stu-id="7da43-617">vmName</span></span> | <span data-ttu-id="7da43-618">Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="7da43-619">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="7da43-619">passPhrase</span></span> | <span data-ttu-id="7da43-620">Typ een sterke wachtwoordzin als Hallo gegevensversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="7da43-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="7da43-621">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="7da43-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="7da43-622">U kunt uw eigen KEK toofurther safeguard Hallo gegevensversleutelingssleutel (geheime wachtwoordzin) zetten in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="7da43-623">CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="7da43-623">CLI commands</span></span>
<span data-ttu-id="7da43-624">U kunt schijfversleuteling inschakelen op uw versleutelde VHD te installeren en gebruiken van Hallo [CLI opdracht](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7da43-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="7da43-625">tooenable versleuteling op bestaande of IaaS Linux VM's worden uitgevoerd in Azure met behulp van de CLI-opdrachten Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="7da43-626">Toegangsbeleid instellen in de sleutelkluis Hallo:</span><span class="sxs-lookup"><span data-stu-id="7da43-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="7da43-627">Set Hallo **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="7da43-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="7da43-628">Stel machtigingen tooAzure AD toepassing toowrite geheimen tooyour sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="7da43-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="7da43-629">tooenable versleuteling op een bestaande of actieve virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="7da43-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="7da43-630">Versleutelingsstatus ophalen:</span><span class="sxs-lookup"><span data-stu-id="7da43-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="7da43-631">versleuteling op een nieuwe virtuele machine vanaf uw versleutelde VHD, gebruik Hallo volgende parameters Hello tooenable `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="7da43-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="7da43-632">Hallo coderingsstatus van een versleutelde IaaS VM ophalen</span><span class="sxs-lookup"><span data-stu-id="7da43-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="7da43-633">U kunt Hallo coderingsstatus ophalen met behulp van Azure Resource Manager [PowerShell-cmdlets](/powershell/azure/overview), of de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7da43-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="7da43-634">Hallo volgende secties wordt uitgelegd hoe toouse Hallo klassieke Azure-portal en de CLI-opdrachten tooget Hallo coderingsstatus.</span><span class="sxs-lookup"><span data-stu-id="7da43-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="7da43-635">Hallo coderingsstatus van een versleutelde Windows VM ophalen met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7da43-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="7da43-636">U kunt de coderingsstatus Hallo Hallo IaaS VM van Azure Resource Manager krijgen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="7da43-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="7da43-637">Meld u aan toohello [klassieke Azure-portal](https://portal.azure.com/), en klik vervolgens op **virtuele machines** in Hallo linkerdeelvenster toosee een samenvatting weergegeven van Hallo virtuele machines in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7da43-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="7da43-638">U kunt Hallo virtuele machines weergave filteren Hallo abonnement door naam te selecteren in Hallo **abonnement** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7da43-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="7da43-639">Hallo boven aan het Hallo **virtuele machines** pagina, klikt u op **kolommen**.</span><span class="sxs-lookup"><span data-stu-id="7da43-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="7da43-640">Op Hallo **Kies kolom** blade Selecteer **schijfversleuteling**, en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="7da43-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="7da43-641">U ziet Hallo schijfversleuteling kolom tonen Hallo coderingsstatus _ingeschakeld_ of _niet ingeschakeld_ voor elke virtuele machine, zoals wordt weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="7da43-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="7da43-643">Hallo coderingsstatus van een versleutelde (Windows of Linux) IaaS VM ophalen met behulp van Hallo schijfversleuteling PowerShell-cmdlet</span><span class="sxs-lookup"><span data-stu-id="7da43-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="7da43-644">Hallo schijfversleuteling PowerShell-cmdlet kunt u de coderingsstatus Hallo Hallo IaaS VM downloaden `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="7da43-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="7da43-645">tooget Hallo-versleutelingsinstellingen voor uw virtuele machine, Voer Hallo volgende in:</span><span class="sxs-lookup"><span data-stu-id="7da43-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="7da43-646">U kunt de uitvoer van Hallo inspecteren _Get-AzureRmVMDiskEncryptionStatus_ sleutel URL's voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7da43-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="7da43-647">Hallo OSVolumeEncrypted en waarden van DataVolumesEncrypted too_Encrypted_ die aangeeft dat beide volumes zijn versleuteld met behulp van Azure Disk Encryption ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="7da43-648">Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets Hallo blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="7da43-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-649">Op Linux virtuele machines, duurt het drie toofour minuten Hallo `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport Hallo coderingsstatus.</span><span class="sxs-lookup"><span data-stu-id="7da43-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="7da43-650">De coderingsstatus Hallo Hallo IaaS VM ophalen uit Hallo schijfversleuteling CLI-opdracht</span><span class="sxs-lookup"><span data-stu-id="7da43-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="7da43-651">U krijgt Hallo coderingsstatus van Hallo IaaS VM via Hallo schijfversleuteling CLI opdracht `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="7da43-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="7da43-652">tooget Hallo-versleutelingsinstellingen voor uw virtuele machine, Voer uw Azure CLI-sessie:</span><span class="sxs-lookup"><span data-stu-id="7da43-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="7da43-653">Schakel versleuteling voor het uitvoeren van Windows IaaS VM</span><span class="sxs-lookup"><span data-stu-id="7da43-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="7da43-654">U kunt versleuteling op een actieve Windows of Linux IaaS VM via hello Azure Disk Encryption Resource Manager-sjabloon of PowerShell-cmdlets uitschakelen en Hallo ontsleuteling configuratie opgeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="7da43-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="7da43-655">Windows VM</span></span>
<span data-ttu-id="7da43-656">Hallo disable-codering stap Hiermee schakelt u versleuteling van Hallo OS, Hallo gegevensvolume of beide op Hallo Windows IaaS VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="7da43-657">U kan uitschakelen Hallo OS volume en laat Hallo gegevensvolume versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="7da43-658">Hallo disable-codering stap wordt uitgevoerd, Hallo klassieke implementatiemodel Azure VM-servicemodel Hallo updates als Hallo Windows IaaS VM ontsleutelde is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="7da43-659">Hallo-inhoud van Hallo VM zijn niet langer in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="7da43-660">Hallo-ontsleuteling worden niet verwijderd voor uw kluis en Hallo encryption key sleutelmateriaal (versleutelingssleutels BitLocker voor Windows en de wachtwoordzin voor Linux).</span><span class="sxs-lookup"><span data-stu-id="7da43-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="7da43-661">Virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="7da43-661">Linux VM</span></span>
<span data-ttu-id="7da43-662">Hallo disable-codering stap Hiermee schakelt u versleuteling van Hallo gegevensvolume op Hallo IaaS virtuele Linux-machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="7da43-663">Deze stap werkt alleen als de besturingssysteemschijf Hallo is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-664">Uitschakelen van versleuteling op Hallo besturingssysteemschijf is niet toegestaan op de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7da43-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="7da43-665">Schakel versleuteling in op een bestaande of actief IaaS VM</span><span class="sxs-lookup"><span data-stu-id="7da43-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="7da43-666">U kunt schijfversleuteling op IaaS VM's van Windows worden uitgevoerd met behulp van Hallo uitschakelen [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="7da43-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="7da43-667">Op de sjabloon hello Azure snel starten, klikt u op **implementeren tooAzure**, Hallo ontsleuteling configuratie invoeren op Hallo **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da43-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="7da43-668">Selecteer Hallo abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** tooenable versleuteling op een nieuwe IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="7da43-669">Virtuele Linux-machines, kunt u versleuteling uitschakelen met behulp van Hallo [uitschakelen van versleuteling op een actieve Linux VM](https://aka.ms/decrypt-linuxvm) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7da43-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="7da43-670">Hallo bevat volgende tabel de sjabloonparameters Resource Manager voor het uitschakelen van versleuteling op een actieve IaaS VM:</span><span class="sxs-lookup"><span data-stu-id="7da43-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="7da43-671">Parameter</span><span class="sxs-lookup"><span data-stu-id="7da43-671">Parameter</span></span> | <span data-ttu-id="7da43-672">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7da43-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7da43-673">vmName</span><span class="sxs-lookup"><span data-stu-id="7da43-673">vmName</span></span> | <span data-ttu-id="7da43-674">Naam van de virtuele machine die coderingsbewerking Hallo Hallo is toobe uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="7da43-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="7da43-675">volumeType</span></span> | <span data-ttu-id="7da43-676">Het type van het volume dat een ontsleutelingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="7da43-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="7da43-677">Geldige waarden zijn _OS_, _gegevens_, en _alle_.</span><span class="sxs-lookup"><span data-stu-id="7da43-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="7da43-678">U kunt versleuteling voor het uitvoeren van Windows IaaS VM OS/opstartvolume zonder het uitschakelen van versleuteling op Hallo niet uitschakelen _gegevens_ volume.</span><span class="sxs-lookup"><span data-stu-id="7da43-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="7da43-679">Houd er ook rekening mee dat uitschakelen versleuteling op Hallo OS-schijf is niet toegestaan voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7da43-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="7da43-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="7da43-680">sequenceVersion</span></span> | <span data-ttu-id="7da43-681">Versie van de reeks van Hallo BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="7da43-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="7da43-682">Dit versienummer verhoogd telkens wanneer een ontsleutelingsbewerking schijf wordt uitgevoerd op Hallo dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7da43-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="7da43-683">Schakel versleuteling in op een bestaande of actief IaaS VM</span><span class="sxs-lookup"><span data-stu-id="7da43-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="7da43-684">Zie toodisable versleuteling op een bestaande of actief IaaS-VM met behulp van PowerShell-cmdlet Hallo [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="7da43-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="7da43-685">Deze cmdlet biedt ondersteuning voor Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="7da43-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="7da43-686">toodisable versleuteling, wordt een uitbreiding op Hallo virtuele machine geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="7da43-687">Als hello _naam_ parameter niet is opgegeven, een uitbreiding met de standaardnaam Hallo _AzureDiskEncryption voor VM's van Windows_ wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7da43-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="7da43-688">Op Linux virtuele machines, wordt Hallo AzureDiskEncryptionForLinux uitbreiding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da43-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="7da43-689">Deze cmdlet Hallo virtuele machine opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="7da43-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="7da43-690">Schakel versleuteling in op vooraf zijn versleuteld IaaS VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="7da43-691">Hello Azure beheerd schijf ARM-sjabloon toocreate te op een versleutelde virtuele machine van een vooraf zijn versleuteld VHD met Hallo ARM-sjabloon vinden gebruiken</span><span class="sxs-lookup"><span data-stu-id="7da43-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="7da43-692">[Een nieuwe beheerde versleutelde schijf van een vooraf zijn versleuteld VHD/storage-blob maken] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="7da43-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="7da43-693">Schakel versleuteling in op een nieuwe Linux IaaS-VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="7da43-694">Hello Azure beheerd schijf ARM-sjabloon toocreate die een nieuwe versleuteld Linux IaaS-VM met Hallo zich bevindt op ARM-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="7da43-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="7da43-695">[Implementatie RHEL 7.2 met volledige schijfversleuteling] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="7da43-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="7da43-696">Schakel versleuteling in op een nieuwe Windows IaaS-VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="7da43-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="7da43-697">Hello Azure beheerd schijf ARM-sjabloon toocreate die een nieuwe versleuteld Linux IaaS-VM met Hallo zich bevindt op ARM-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="7da43-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="7da43-698">[Een nieuwe versleutelde Windows IaaS beheerd schijf virtuele machine maken van de afbeelding] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="7da43-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="7da43-699">Het is verplicht toosnapshot en/of back-up een beheerde schijf op basis van VM-instantie buiten en eerdere tooenabling Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="7da43-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="7da43-700">Een momentopname van het Hallo-beheerde schijven kan worden uitgevoerd vanuit de portal Hallo of Azure Backup kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da43-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="7da43-701">Back-ups zorgen ervoor dat een hersteloptie mogelijk in geval van Hallo van een onverwachte fout opgetreden tijdens het versleutelen.</span><span class="sxs-lookup"><span data-stu-id="7da43-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="7da43-702">Nadat u een back-up is gemaakt, kan de cmdlet Set-AzureRmVMDiskEncryptionExtension Hallo gebruikte tooencrypt beheerde schijven worden door Hallo - skipVmBackup parameter te geven.</span><span class="sxs-lookup"><span data-stu-id="7da43-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="7da43-703">Met deze opdracht uitvoeren tegen beheerde schijven op basis van de virtuele machine totdat een back-up is gemaakt en deze parameter is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="7da43-704">Versleutelingsinstellingen van een bestaande versleutelde niet premium virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="7da43-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="7da43-705">AAD client-ID/geheime sleutel versleutelingssleutel [KEK] versleutelingssleutel BitLocker voor Windows-VM of de wachtwoordzin voor, zoals Hallo bestaande Azure-schijf codering wordt ondersteund interfaces gebruiken voor het uitvoeren van virtuele machine [PS-cmdlets, CLI of ARM-sjablonen] tooupdate Hallo versleutelingsinstellingen Versleutelingsinstelling voor Linux VM enzovoort Hallo-update wordt alleen ondersteund voor virtuele machines die worden ondersteund door niet-premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="7da43-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="7da43-706">Het is NNOT ondersteund voor virtuele machines die worden ondersteund door de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="7da43-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="7da43-707">Bijlage</span><span class="sxs-lookup"><span data-stu-id="7da43-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="7da43-708">Verbinding maken met tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="7da43-708">Connect tooyour subscription</span></span>
<span data-ttu-id="7da43-709">Lees voordat u doorgaat Hallo *vereisten* sectie in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7da43-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="7da43-710">Nadat u ervoor te zorgen dat aan alle vereisten is voldaan, sluit u tooyour abonnement door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="7da43-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="7da43-711">Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="7da43-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="7da43-712">Als u meerdere abonnementen hebt en één toouse toospecify, typt u Hallo toosee Hallo abonnementen voor uw account te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="7da43-713">toospecify hello abonnement u wilt dat toouse, type:</span><span class="sxs-lookup"><span data-stu-id="7da43-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="7da43-714">tooverify hello abonnement geconfigureerd klopt, type:</span><span class="sxs-lookup"><span data-stu-id="7da43-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="7da43-715">tooconfirm hello Azure Disk Encryption cmdlets zijn geïnstalleerd, type:</span><span class="sxs-lookup"><span data-stu-id="7da43-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="7da43-716">Hallo na uitvoer bevestigt hello Azure schijf versleuteling PowerShell-installatie:</span><span class="sxs-lookup"><span data-stu-id="7da43-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="7da43-717">Een vooraf zijn versleuteld Windows VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7da43-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="7da43-718">Hallo-secties die volgen zijn nodig tooprepare een Windows-VHD voor de implementatie als een gecodeerde VHD in Azure IaaS vooraf zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="7da43-719">Hallo informatie tooprepare gebruiken en een nieuwe Windows VM (VHD) op de Azure Site Recovery of Azure opgestart.</span><span class="sxs-lookup"><span data-stu-id="7da43-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="7da43-720">Bijwerken van de Groepsbeleid tooallow zonder TPM voor OS-beveiliging</span><span class="sxs-lookup"><span data-stu-id="7da43-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="7da43-721">Hallo groepsbeleidsinstellingen voor BitLocker-instelling configureren **BitLocker-stationsversleuteling**, die u vindt hier onder **lokaal computerbeleid** > **Computerconfiguratie**  >  **Beheersjablonen** > **Windows-onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="7da43-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="7da43-722">Deze instelling te wijzigen**besturingssysteem stations** > **aanvullende verificatie bij opstarten vereisen** > **BitLocker zonder een compatibele TPMtoestaan**, zoals weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="7da43-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="7da43-724">BitLocker-onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="7da43-724">Install BitLocker feature components</span></span>
<span data-ttu-id="7da43-725">Voor Windows Server 2012 en hoger, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7da43-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="7da43-726">Gebruik voor Windows Server 2008 R2 Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7da43-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="7da43-727">Hallo volume met het besturingssysteem voorbereiden voor BitLocker met behulp van`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="7da43-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="7da43-728">toocompress Hallo OS partitie en Hallo machine voorbereiden voor BitLocker, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7da43-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="7da43-729">Hallo OS volume beveiligen met behulp van BitLocker</span><span class="sxs-lookup"><span data-stu-id="7da43-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="7da43-730">Gebruik Hallo [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) opdracht tooenable versleuteling op Hallo opstartvolume met behulp van een externe sleutelbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="7da43-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="7da43-731">Ook Hallo externe sleutel (.bek-bestand) op Hallo extern station of volume plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7da43-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="7da43-732">Versleuteling is ingeschakeld op Hallo system/opstartvolume na Hallo opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="7da43-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="7da43-733">Hallo VM met een afzonderlijke gegevens/resource VHD voorbereiden voor het ophalen van externe sleutel Hallo met BitLocker.</span><span class="sxs-lookup"><span data-stu-id="7da43-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="7da43-734">Versleutelen van een OS-station op een actieve Linux VM</span><span class="sxs-lookup"><span data-stu-id="7da43-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="7da43-735">Versleuteling van een OS-station op een actieve Linux VM wordt ondersteund op Hallo distributies te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="7da43-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="7da43-736">RHEL 7.2</span></span>
* <span data-ttu-id="7da43-737">7.2 centOS</span><span class="sxs-lookup"><span data-stu-id="7da43-737">CentOS 7.2</span></span>
* <span data-ttu-id="7da43-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7da43-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="7da43-739">Vereisten voor de OS-schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="7da43-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="7da43-740">Hallo VM moet worden gemaakt vanuit Hallo Marketplace-installatiekopie in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7da43-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="7da43-741">Azure virtuele machine met ten minste 4 GB aan RAM-geheugen (aanbevolen grootte is 7 GB).</span><span class="sxs-lookup"><span data-stu-id="7da43-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="7da43-742">(Voor RHEL en CentOS) SELinux uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="7da43-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="7da43-743">toodisable SELinux, Zie '4.4.2.</span><span class="sxs-lookup"><span data-stu-id="7da43-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="7da43-744">Uitschakelen van SELinux' in hello [SELinux van de gebruiker en de Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="7da43-745">Nadat u SELinux uitgeschakeld, start u ten minste eenmaal Hallo VM opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7da43-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="7da43-746">Stappen</span><span class="sxs-lookup"><span data-stu-id="7da43-746">Steps</span></span>
1. <span data-ttu-id="7da43-747">Een virtuele machine maken met behulp van een Hallo distributies eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="7da43-748">Voor CentOS 7.2, OS schijfversleuteling ondersteund via een speciale installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7da43-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="7da43-749">toouse dit image, '7.2n' als SKU Hallo bij het maken van VM Hallo opgeven:</span><span class="sxs-lookup"><span data-stu-id="7da43-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="7da43-750">Hallo VM volgens tooyour moet configureren.</span><span class="sxs-lookup"><span data-stu-id="7da43-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="7da43-751">Als u tooencrypt gaat alle stations van hello (OS + gegevens), moeten Hallo gegevensstations toobe opgegeven en koppelbaar van /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="7da43-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="7da43-752">Gebruik UUID =... toospecify gegevensstations in/etc/fstab in plaats van Hallo blok apparaatnaam (bijvoorbeeld /dev/sdb1) opgeven.</span><span class="sxs-lookup"><span data-stu-id="7da43-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="7da43-753">Tijdens het versleutelen kan Hallo volgorde van de stations op Hallo VM gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="7da43-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="7da43-754">Als uw virtuele machine afhankelijk van een specifieke volgorde van apparaten is, mislukt het toomount ze na versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7da43-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="7da43-755">Meld u af bij Hallo SSH-sessies.</span><span class="sxs-lookup"><span data-stu-id="7da43-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="7da43-756">tooencrypt hello OS Geef volumeType als **alle** of **OS** wanneer u [versleuteling inschakelen](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="7da43-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="7da43-757">Alle gebruikersruimte innemen processen die niet worden uitgevoerd als `systemd` services moeten worden afgesloten met een `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="7da43-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="7da43-758">Opnieuw opstarten Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-758">Reboot hello VM.</span></span> <span data-ttu-id="7da43-759">Wanneer u OS schijfversleuteling op een actieve virtuele machine inschakelt, plan op VM uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="7da43-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="7da43-760">Periodiek voortgang Hallo van versleuteling met Hallo-instructies in Hallo [volgende sectie](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="7da43-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="7da43-761">Nadat de Get-AzureRmVmDiskEncryptionStatus toont 'VMRestartPending', start u uw virtuele machine tooit aanmelden of via de portal hello, PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="7da43-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="7da43-762">Voordat u opnieuw opstart, wordt aangeraden dat u opslaat [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="7da43-763">OS-versleuteling voortgang controleren</span><span class="sxs-lookup"><span data-stu-id="7da43-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="7da43-764">U kunt voortgang OS versleuteling op drie manieren:</span><span class="sxs-lookup"><span data-stu-id="7da43-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="7da43-765">Gebruik Hallo `Get-AzureRmVmDiskEncryptionStatus` cmdlet en controleer Hallo ProgressMessage veld:</span><span class="sxs-lookup"><span data-stu-id="7da43-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="7da43-766">Nadat het Hallo VM bereikt 'OS schijfversleuteling gestart', duurt het ongeveer 40 minuten too50 op een Premium-opslag ondersteund VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="7da43-767">Omdat [uitgeven #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` en `DataVolumesEncrypted` worden weergegeven als `Unknown` in een aantal distributies.</span><span class="sxs-lookup"><span data-stu-id="7da43-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="7da43-768">Met de versie 2.1.5 WALinuxAgent en later kunt dit probleem automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="7da43-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="7da43-769">Als u ziet `Unknown` u kunt in de uitvoer van Hallo schijfversleuteling status controleren met behulp van hello Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="7da43-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="7da43-770">Ga te[Azure Resource Explorer](https://resources.azure.com/), en vouw vervolgens deze hiërarchie in Hallo selectie Configuratiescherm op links:</span><span class="sxs-lookup"><span data-stu-id="7da43-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="7da43-771">Ga in Hallo InstanceView, toosee Hallo coderingsstatus van uw schijven.</span><span class="sxs-lookup"><span data-stu-id="7da43-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Instantieweergave van virtuele machine](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="7da43-773">Bekijk [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="7da43-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="7da43-774">Berichten van Hallo ADE uitbreiding moeten worden voorafgegaan door `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="7da43-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="7da43-775">Meld u bij toohello VM via SSH en Hallo extensie logboek vanaf ophalen:</span><span class="sxs-lookup"><span data-stu-id="7da43-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="7da43-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="7da43-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="7da43-777">Het is raadzaam dat u niet toohello VM aanmelden zich terwijl OS-versleuteling uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="7da43-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="7da43-778">Kopiëren van Logboeken voor Hallo alleen wanneer hello andere twee methoden zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="7da43-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="7da43-779">Een vooraf zijn versleuteld Linux VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7da43-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="7da43-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="7da43-780">Ubuntu 16</span></span>
<span data-ttu-id="7da43-781">Configureren van versleuteling tijdens de installatie van de distributie Hallo door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="7da43-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="7da43-782">Selecteer **configureren van versleutelde volumes** wanneer het partitioneren van Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="7da43-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="7da43-784">Maak een afzonderlijke opstartstation, moet niet worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7da43-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="7da43-785">Codeer uw basisstation.</span><span class="sxs-lookup"><span data-stu-id="7da43-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="7da43-787">Geef een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="7da43-787">Provide a passphrase.</span></span> <span data-ttu-id="7da43-788">Dit is Hallo wachtwoordzin toohello sleutelkluis te uploaden.</span><span class="sxs-lookup"><span data-stu-id="7da43-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="7da43-790">Voltooi partitioneren.</span><span class="sxs-lookup"><span data-stu-id="7da43-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="7da43-792">Als u Hallo VM opstart en wordt gevraagd een wachtwoordzin, gebruikt u Hallo wachtwoordzin die u hebt opgegeven in stap 3.</span><span class="sxs-lookup"><span data-stu-id="7da43-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="7da43-794">Hallo VM voorbereiden voor het uploaden naar Azure met behulp [deze instructies](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="7da43-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="7da43-795">Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="7da43-796">Versleuteling toowork configureren met Azure door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="7da43-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="7da43-797">Maak een bestand onder /usr/local/sbin/azure_crypt_key.sh, met inhoud in het volgende script Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="7da43-798">Betalen aandacht toohello KeyFileName, omdat het Hallo wachtwoordzin-bestandsnaam gebruikt door Azure.</span><span class="sxs-lookup"><span data-stu-id="7da43-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="7da43-799">Hallo crypt config in wijzigen */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="7da43-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="7da43-800">Dit ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="7da43-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="7da43-801">Als u wilt bewerken *azure_crypt_key.sh* in Windows en u gekopieerd tooLinux, voer `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="7da43-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="7da43-802">Uitvoermachtigingen toohello script toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7da43-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="7da43-803">Bewerken */etc/initramfs-tools/modules* door regels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="7da43-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="7da43-804">Voer `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` te laten treden.</span><span class="sxs-lookup"><span data-stu-id="7da43-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="7da43-805">Nu u kunt inrichting ervan ongedaan Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7da43-805">Now you can deprovision hello VM.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="7da43-807">De volgende stap toohello gaan en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="7da43-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="7da43-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="7da43-808">openSUSE 13.2</span></span>
<span data-ttu-id="7da43-809">tooconfigure versleuteling tijdens de installatie van de distributie van Hallo Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="7da43-810">Wanneer u Hallo schijven partitioneren, selecteert u **versleutelen Volume groep**, en voer vervolgens een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7da43-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="7da43-811">Dit is Hallo wachtwoord dat u de sleutelkluis tooyour wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="7da43-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="7da43-813">Hallo VM die gebruikmaakt van uw wachtwoord worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="7da43-813">Boot hello VM using your password.</span></span>

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="7da43-815">Prepare Hallo VM voor het uploaden van tooAzure door Hallo-instructies in [een SLES of openSUSE virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="7da43-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="7da43-816">Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="7da43-817">tooconfigure versleuteling toowork met Azure, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="7da43-818">Hallo /etc/dracut.conf bewerken en Hallo volgt regel toe:</span><span class="sxs-lookup"><span data-stu-id="7da43-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="7da43-819">Deze regels door Hallo van Hallo commentaar bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="7da43-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="7da43-820">Hallo volgt regel aan Hallo begin van Hallo bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7da43-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="7da43-821">En wijzig alle instanties van:</span><span class="sxs-lookup"><span data-stu-id="7da43-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="7da43-822">in:</span><span class="sxs-lookup"><span data-stu-id="7da43-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="7da43-823">/Usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh bewerken en te toevoegen '# Open LUKS apparaat':</span><span class="sxs-lookup"><span data-stu-id="7da43-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="7da43-824">Voer `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="7da43-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="7da43-825">Nu u inrichting ervan ongedaan kunt Hallo VM en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="7da43-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="7da43-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7da43-826">CentOS 7</span></span>
<span data-ttu-id="7da43-827">tooconfigure versleuteling tijdens de installatie van de distributie van Hallo Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="7da43-828">Selecteer **mijn gegevens versleutelen** wanneer u schijven partitioneren.</span><span class="sxs-lookup"><span data-stu-id="7da43-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="7da43-830">Zorg ervoor dat **versleutelen** is geselecteerd voor de basispartitie.</span><span class="sxs-lookup"><span data-stu-id="7da43-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="7da43-832">Geef een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="7da43-832">Provide a passphrase.</span></span> <span data-ttu-id="7da43-833">Dit is Hallo wachtwoordzin dat u de sleutelkluis tooyour wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="7da43-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="7da43-835">Als u Hallo VM opstart en wordt gevraagd een wachtwoordzin, gebruikt u Hallo wachtwoordzin die u hebt opgegeven in stap 3.</span><span class="sxs-lookup"><span data-stu-id="7da43-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="7da43-837">Prepare Hallo VM voor het uploaden naar Azure met behulp van Hallo 'CentOS 7.0 +'-instructies in [een CentOS-virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="7da43-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="7da43-838">Hallo laatste stap (inrichting hello VM) niet nog uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7da43-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="7da43-839">Nu u inrichting ervan ongedaan kunt Hallo VM en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="7da43-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="7da43-840">tooconfigure versleuteling toowork met Azure, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da43-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="7da43-841">Hallo /etc/dracut.conf bewerken en Hallo volgt regel toe:</span><span class="sxs-lookup"><span data-stu-id="7da43-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="7da43-842">Deze regels door Hallo van Hallo commentaar bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="7da43-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="7da43-843">Hallo volgt regel aan Hallo begin van Hallo bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7da43-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="7da43-844">En wijzig alle instanties van:</span><span class="sxs-lookup"><span data-stu-id="7da43-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="7da43-845">tot</span><span class="sxs-lookup"><span data-stu-id="7da43-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="7da43-846">Bewerk /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh en dit na '# Open LUKS apparaat' hello toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7da43-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="7da43-847">Voer Hallo ' / usr/sbin/dracut - f - v ' tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="7da43-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="7da43-849">Versleutelde VHD tooan Azure storage-account uploaden</span><span class="sxs-lookup"><span data-stu-id="7da43-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="7da43-850">Nadat BitLocker-versleuteling of DM-Crypt versleuteling is ingeschakeld, gecodeerd Hallo lokale VHD behoeften toobe geüpload tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="7da43-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="7da43-851">Hallo schijfversleuteling geheim voor Hallo vooraf zijn versleuteld VM tooyour sleutelkluis uploaden</span><span class="sxs-lookup"><span data-stu-id="7da43-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="7da43-852">Hallo-schijfversleuteling geheim dat u hebt verkregen moet eerder worden geüpload als een geheim in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="7da43-853">Hallo sleutelkluis moet toohave schijfversleuteling en machtigingen die zijn ingeschakeld voor uw Azure AD-client.</span><span class="sxs-lookup"><span data-stu-id="7da43-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="7da43-854">Schijf versleuteling geheim niet versleuteld met een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="7da43-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="7da43-855">tooset up Hallo geheim in de sleutelkluis, gebruik [Set AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="7da43-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="7da43-856">Als u een virtuele Windows-machine hebt, Hallo bek bestand is gecodeerd als een base64-tekenreeks en vervolgens geüpload tooyour sleutelkluis met Hallo `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7da43-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="7da43-857">Voor Linux Hallo wachtwoordzin in als een base64-tekenreeks is gecodeerd en vervolgens geüpload toohello sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7da43-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="7da43-858">Bovendien moet u ervoor zorgen dat Hallo tags te volgen zijn ingesteld bij het maken van Hallo geheim in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="7da43-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="7da43-859">Gebruik Hallo `$secretUrl` in de volgende stap Hallo voor [koppelen Hallo OS-schijf zonder KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="7da43-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="7da43-860">Schijf versleuteling geheim is versleuteld met een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="7da43-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="7da43-861">Voordat u Hallo geheime toohello sleutelkluis uploadt, kunt u deze desgewenst met een sleutel versleutelingssleutel coderen.</span><span class="sxs-lookup"><span data-stu-id="7da43-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="7da43-862">Gebruik Hallo wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst versleutelen met de belangrijkste versleutelingssleutel Hallo Hallo-geheim.</span><span class="sxs-lookup"><span data-stu-id="7da43-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="7da43-863">Hello uitvoer van deze bewerking wrap is een base64-URL gecodeerde tekenreeks, die u vervolgens als een geheim uploaden kunt via Hallo [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7da43-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="7da43-864">Gebruik `$KeyEncryptionKey` en `$secretUrl` in de volgende stap Hallo voor [koppelen Hallo OS-schijf met een KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="7da43-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="7da43-865">Geef een geheime URL wanneer u een besturingssysteemschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="7da43-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="7da43-866">Zonder een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="7da43-866">Without using a KEK</span></span>
<span data-ttu-id="7da43-867">Terwijl u Hallo OS-schijf toevoegen wilt, moet u toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="7da43-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="7da43-868">Hallo-URL is gegenereerd in Hallo 'schijfversleuteling geheim niet versleuteld met een KEK' sectie.</span><span class="sxs-lookup"><span data-stu-id="7da43-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="7da43-869">Met behulp van een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="7da43-869">Using a KEK</span></span>
<span data-ttu-id="7da43-870">Wanneer u Hallo OS-schijf toegevoegd, `$KeyEncryptionKey` en `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="7da43-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="7da43-871">Hallo-URL is gegenereerd in Hallo 'schijfversleuteling geheim niet versleuteld met een KEK' sectie.</span><span class="sxs-lookup"><span data-stu-id="7da43-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="7da43-872">Download deze handleiding</span><span class="sxs-lookup"><span data-stu-id="7da43-872">Download this guide</span></span>
<span data-ttu-id="7da43-873">U kunt deze handleiding downloaden van Hallo [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="7da43-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="7da43-874">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="7da43-874">For more information</span></span>
[<span data-ttu-id="7da43-875">Verken Azure Disk Encryption met Azure PowerShell - deel 1</span><span class="sxs-lookup"><span data-stu-id="7da43-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="7da43-876">Azure Disk Encryption met Azure PowerShell - deel 2 verkennen</span><span class="sxs-lookup"><span data-stu-id="7da43-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
