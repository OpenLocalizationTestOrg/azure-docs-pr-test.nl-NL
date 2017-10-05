---
title: Azure Disk Encryption for Windows and Linux IaaS VM's | Microsoft Docs
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
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="05c59-103">Azure Disk Encryption for Windows and Linux IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="05c59-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="05c59-104">Microsoft Azure is sterk doorgevoerd om ervoor te zorgen voor uw privacy van gegevens, onafhankelijkheid van gegevens en schakelt u de controle uw Azure gegevens via een bereik van gehoste technologieën geavanceerde voor het versleutelen, beheren en beheren van versleutelingssleutels besturingselement & audit toegang van gegevens.</span><span class="sxs-lookup"><span data-stu-id="05c59-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="05c59-105">Dit biedt Azure-klanten de flexibiliteit om te kiezen welke oplossing het beste voldoet aan de behoeften van hun bedrijf.</span><span class="sxs-lookup"><span data-stu-id="05c59-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="05c59-106">In dit artikel vindt we u een nieuwe technologieoplossing 'Azure Disk Encryption for Windows and Linux IaaS VM van' om te helpen beveiligen en bescherming van uw gegevens om te voldoen aan de beveiliging van de organisatie en de naleving verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="05c59-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="05c59-107">Het artikel biedt gedetailleerde richtlijnen over het gebruik van de Azure disk encryption functies met inbegrip van de ondersteunde scenario's en de gebruiker optreedt.</span><span class="sxs-lookup"><span data-stu-id="05c59-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-108">Bepaalde aanbevelingen mogelijk meer gegevens, netwerk of compute-Resourcegebruik, wat leidt tot extra kosten in licentie of abonnement.</span><span class="sxs-lookup"><span data-stu-id="05c59-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="05c59-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="05c59-109">Overview</span></span>
<span data-ttu-id="05c59-110">Azure Disk Encryption is een nieuwe functie waarmee u uw Windows- en Linux IaaS-schijven voor virtuele machine versleutelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="05c59-111">Azure Disk Encryption maakt gebruik van het industrie-initiatief [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) functie van Windows en de [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) functie van Linux voor volumeversleuteling voor het besturingssysteem en de gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="05c59-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="05c59-112">De oplossing is geïntegreerd met [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) om te controleren en beheren van de schijfversleuteling sleutels en geheimen in uw abonnement sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="05c59-113">De oplossing zorgt er ook voor dat alle gegevens op de virtuele machine-schijven zijn versleuteld in rust in uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="05c59-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="05c59-114">Versleuteling van de schijf van Azure voor Windows en Linux IaaS VM's wordt nu **algemene beschikbaarheid** in alle openbare Azure-regio en AzureGov regio's voor de standaard virtuele machines en virtuele machines met premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="05c59-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="05c59-115">Versleuteling scenario 's</span><span class="sxs-lookup"><span data-stu-id="05c59-115">Encryption scenarios</span></span>
<span data-ttu-id="05c59-116">De oplossing voor Azure Disk Encryption ondersteunt de volgende klant-scenario's:</span><span class="sxs-lookup"><span data-stu-id="05c59-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="05c59-117">Schakel versleuteling in op de nieuwe IaaS VM's die worden gemaakt op basis van vooraf zijn versleuteld VHD- en versleutelingssleutels</span><span class="sxs-lookup"><span data-stu-id="05c59-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="05c59-118">Schakel versleuteling in op nieuwe gemaakt op basis van installatiekopieën van het ondersteunde galerie van Azure IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="05c59-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="05c59-119">Schakel versleuteling in op bestaande IaaS virtuele machines die worden uitgevoerd in Azure</span><span class="sxs-lookup"><span data-stu-id="05c59-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="05c59-120">Schakel versleuteling in op IaaS VM's van Windows</span><span class="sxs-lookup"><span data-stu-id="05c59-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="05c59-121">Versleuteling op gegevensstations voor Linux IaaS VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="05c59-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="05c59-122">Versleuteling van beheerde schijf virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="05c59-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="05c59-123">Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="05c59-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="05c59-124">Back-up en herstel van versleutelde virtuele machines, versleuteld met sleutelcodering sleutel</span><span class="sxs-lookup"><span data-stu-id="05c59-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="05c59-125">De oplossing ondersteunt de volgende scenario's voor IaaS VM's wanneer ze zijn ingeschakeld in Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="05c59-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="05c59-126">Integratie met Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="05c59-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="05c59-127">Standard-laag VMs: [A, D, DS, G, GS, F en enzovoort reeks IaaS VM's](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="05c59-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="05c59-128">Schakel versleuteling in op Windows- en Linux IaaS VM's en beheerde schijven virtuele machines van de ondersteunde Azure-galerie afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="05c59-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="05c59-129">Versleuteling op besturingssysteem en stations voor Windows IaaS VM's en beheerde schijf-VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="05c59-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="05c59-130">Versleuteling op gegevensstations voor Linux IaaS VM's en beheerde schijf-VM's uitschakelen</span><span class="sxs-lookup"><span data-stu-id="05c59-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="05c59-131">Schakel versleuteling in op IaaS VM's met Windows Client-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="05c59-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="05c59-132">Schakel versleuteling in op volumes met koppelpunten paden</span><span class="sxs-lookup"><span data-stu-id="05c59-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="05c59-133">Schakel versleuteling in op Linux VM's zijn geconfigureerd met schijf striping (RAID) met behulp van mdadm</span><span class="sxs-lookup"><span data-stu-id="05c59-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="05c59-134">Schakel versleuteling in op de virtuele Linux-machines met behulp van LVM voor gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="05c59-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="05c59-135">Schakel versleuteling in op Windows VM's zijn geconfigureerd met opslagruimten</span><span class="sxs-lookup"><span data-stu-id="05c59-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="05c59-136">Instellingen voor codering van een bestaande versleutelde niet premium-opslag virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="05c59-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="05c59-137">Alle openbare Azure en AzureGov regio's worden ondersteund</span><span class="sxs-lookup"><span data-stu-id="05c59-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="05c59-138">De oplossing biedt geen ondersteuning voor de volgende scenario's, functies en -technologie:</span><span class="sxs-lookup"><span data-stu-id="05c59-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="05c59-139">Basisstaffel IaaS VM 's</span><span class="sxs-lookup"><span data-stu-id="05c59-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="05c59-140">Het uitschakelen van Linux IaaS VM's op een station OS versleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="05c59-141">Het uitschakelen van versleuteling op een gegevensstation als de OS-schijf versleuteld voor Linux Iaas VM 's</span><span class="sxs-lookup"><span data-stu-id="05c59-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="05c59-142">IaaS VM's die zijn gemaakt met behulp van de methode voor het maken van klassieke VM</span><span class="sxs-lookup"><span data-stu-id="05c59-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="05c59-143">Schakel versleuteling in op Windows en Linux-IaaS VM's klanten aangepaste installatiekopieën wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="05c59-144">Enccryption inschakelen op Linux-besturingssysteem voor LVM schijf wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="05c59-145">Deze ondersteuning wordt binnenkort worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="05c59-145">This support will come soon.</span></span>
* <span data-ttu-id="05c59-146">Integratie met uw on-premises Key Management Service</span><span class="sxs-lookup"><span data-stu-id="05c59-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="05c59-147">Azure Files (gedeelde bestandssysteem), Network File System (NFS), dynamische volumes en virtuele machines van Windows die zijn geconfigureerd met software gebaseerde RAID-systemen</span><span class="sxs-lookup"><span data-stu-id="05c59-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="05c59-148">Back-up en herstel van versleutelde virtuele machines, zonder sleutelcodering sleutel is gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="05c59-149">Instellingen voor codering van een bestaande versleutelde premium-opslag VM bijwerken.</span><span class="sxs-lookup"><span data-stu-id="05c59-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-150">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met de KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="05c59-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="05c59-151">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="05c59-152">KEK-sleutel is een optionele parameter waarmee de VM-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="05c59-153">Deze ondersteuning is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="05c59-153">This support is coming soon.</span></span>
> <span data-ttu-id="05c59-154">Bijwerken van instellingen voor codering van een bestaande versleutelde premium-opslag virtuele machine worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="05c59-155">Deze ondersteuning is binnenkort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="05c59-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="05c59-156">Coderingsfuncties</span><span class="sxs-lookup"><span data-stu-id="05c59-156">Encryption features</span></span>
<span data-ttu-id="05c59-157">Wanneer u inschakelen en implementeren van Azure Disk Encryption voor Azure IaaS VM's, worden de volgende mogelijkheden ingeschakeld, afhankelijk van de opgegeven configuratie:</span><span class="sxs-lookup"><span data-stu-id="05c59-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="05c59-158">Versleuteling van het volume met het besturingssysteem voor het beveiligen van het opstartvolume in rust in uw opslagruimte</span><span class="sxs-lookup"><span data-stu-id="05c59-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="05c59-159">Versleuteling van gegevensvolumes ter bescherming van de gegevensvolumes in rust in uw opslagruimte</span><span class="sxs-lookup"><span data-stu-id="05c59-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="05c59-160">Het uitschakelen van IaaS VM's van Windows op de stations besturingssysteem en versleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="05c59-161">Codering van gegevens uitschakelen schijven voor virtuele machines van Linux IaaS (alleen als het besturingssysteem IS niet versleuteld station)</span><span class="sxs-lookup"><span data-stu-id="05c59-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="05c59-162">Beveiliging van de versleutelingssleutels en geheimen in uw abonnement sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="05c59-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="05c59-163">De coderingsstatus van de versleutelde IaaS VM rapportage</span><span class="sxs-lookup"><span data-stu-id="05c59-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="05c59-164">Verwijderen van configuratie-instellingen van de virtuele machine voor IaaS-schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="05c59-165">Back-up en herstel van versleutelde virtuele machines met behulp van de Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="05c59-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-166">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met de KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="05c59-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="05c59-167">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="05c59-168">KEK-sleutel is een optionele parameter waarmee de VM-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="05c59-169">Azure Disk Encryption voor IaaS VMS voor Windows en Linux-oplossing omvat:</span><span class="sxs-lookup"><span data-stu-id="05c59-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="05c59-170">De extensie van de schijf-codering voor Windows.</span><span class="sxs-lookup"><span data-stu-id="05c59-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="05c59-171">De extensie van de schijf-codering voor Linux.</span><span class="sxs-lookup"><span data-stu-id="05c59-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="05c59-172">De schijf-codering PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05c59-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="05c59-173">De schijf-codering cmdlets van Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="05c59-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="05c59-174">De schijf-codering Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="05c59-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="05c59-175">De oplossing voor Azure Disk Encryption wordt ondersteund op IaaS VM's met Windows of Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="05c59-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="05c59-176">Zie de sectie 'Vereisten' voor meer informatie over de ondersteunde besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="05c59-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-177">Er zijn geen extra kosten voor het versleutelen van VM-schijven met Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="05c59-178">Waardevoorstel</span><span class="sxs-lookup"><span data-stu-id="05c59-178">Value proposition</span></span>
<span data-ttu-id="05c59-179">Wanneer u de Azure Disk Encryption-management-oplossing toepast, kunt u voldoen aan de volgende zakelijke behoeften:</span><span class="sxs-lookup"><span data-stu-id="05c59-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="05c59-180">IaaS VM's worden beveiligd in rust, omdat u versleuteling van industriestandaard technologie gebruiken kunt om de organisatorische vereisten voor beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="05c59-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="05c59-181">Opstarten van IaaS VM's onder de klant beheerde sleutel en beleid en u kunt hun gebruik in de sleutelkluis controleren.</span><span class="sxs-lookup"><span data-stu-id="05c59-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="05c59-182">Codering-werkstroom</span><span class="sxs-lookup"><span data-stu-id="05c59-182">Encryption workflow</span></span>
<span data-ttu-id="05c59-183">Het inschakelen van schijfversleuteling voor Windows en Linux-machines, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="05c59-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="05c59-184">Kies een versleutelingsscenario uit de bovenstaande scenario's voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="05c59-185">U meldt zich aan het inschakelen van schijfversleuteling via het Azure Disk Encryption Resource Manager-sjabloon, het PowerShell-cmdlets of de CLI-opdracht en geeft u de configuratie van de codering.</span><span class="sxs-lookup"><span data-stu-id="05c59-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="05c59-186">Voor de klant versleuteld VHD-scenario de versleutelde harde schijf geüpload naar uw opslagaccount en het sleutelmateriaal versleuteling aan de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="05c59-187">De configuratie van de versleuteling om Schakel versleuteling in op een nieuwe IaaS VM vervolgens opgeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="05c59-188">Voor nieuwe virtuele machines die zijn gemaakt van de Marketplace en bestaande virtuele machines die al worden uitgevoerd in Azure, geeft u de configuratie van de versleuteling om Schakel versleuteling in op de IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="05c59-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="05c59-189">Toegang verlenen tot de Azure-platform het materiaal versleutelingssleutel (versleutelingssleutels BitLocker voor Windows-systemen) en de wachtwoordzin voor Linux lezen uit de sleutelkluis versleuteling op de VM IaaS in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="05c59-190">Geef de toepassings-id van de Azure Active Directory (Azure AD) voor het schrijven van de versleutelingssleutel materiaal naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="05c59-191">In dat geval schakelt u versleuteling op de IaaS-VM voor de scenario's die worden vermeld in stap 2.</span><span class="sxs-lookup"><span data-stu-id="05c59-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="05c59-192">Azure werkt bij het VM-servicemodel met versleuteling en de configuratie van de sleutelkluis en stelt uw versleutelde VM.</span><span class="sxs-lookup"><span data-stu-id="05c59-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="05c59-194">Werkstroom voor ontsleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-194">Decryption workflow</span></span>
<span data-ttu-id="05c59-195">Als u wilt uitschakelen schijfversleuteling voor IaaS VM's, de volgende stappen op hoog niveau:</span><span class="sxs-lookup"><span data-stu-id="05c59-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="05c59-196">Kies versleuteling (decodering) uitschakelen op een actieve IaaS VM in Azure via de Azure Disk Encryption Resource Manager-sjabloon of het PowerShell-cmdlets en geef de configuratie voor ontsleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="05c59-197">Deze stap wordt de versleuteling van het besturingssysteem gegevensvolume en/of op het actieve Windows IaaS VM uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="05c59-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="05c59-198">Echter, zoals vermeld in de vorige sectie, het uitschakelen van Linux OS schijf-versleuteling wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="05c59-199">De ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines, zolang de besturingssysteemschijf is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="05c59-200">Azure werkt het VM-servicemodel en IaaS VM ontsleutelde is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="05c59-201">De inhoud van de virtuele machine worden niet langer in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-202">De bewerking uitschakelen versleuteling verwijdert niet de sleutelkluis en de versleuteling sleutelmateriaal (versleutelingssleutels BitLocker voor Windows-systemen) of de wachtwoordzin voor Linux.</span><span class="sxs-lookup"><span data-stu-id="05c59-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="05c59-203">Het uitschakelen van Linux OS schijf-versleuteling wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="05c59-204">De ontsleuteling stap is alleen toegestaan voor gegevensstations op virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="05c59-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="05c59-205">Het uitschakelen van de schijf van gegevensversleuteling voor Linux wordt niet ondersteund als de OS-schijf is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c59-206">Vereisten</span><span class="sxs-lookup"><span data-stu-id="05c59-206">Prerequisites</span></span>
<span data-ttu-id="05c59-207">Voordat u Azure Disk Encryption op Azure IaaS VM's inschakelen voor de ondersteunde scenario's die zijn beschreven in de sectie 'Overzicht', Zie de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="05c59-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="05c59-208">U moet een geldige actief Azure-abonnement maken van resources in Azure in de ondersteunde regio's hebben.</span><span class="sxs-lookup"><span data-stu-id="05c59-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="05c59-209">Azure Disk Encryption wordt ondersteund op de volgende versies van Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="05c59-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="05c59-210">Azure Disk Encryption wordt ondersteund op de volgende Windows-clientversies: Windows 8 client en Windows 10-client.</span><span class="sxs-lookup"><span data-stu-id="05c59-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-211">Voor Windows Server 2008 R2, moet u .NET Framework 4.5 is geïnstalleerd voordat u Azure-versleuteling inschakelen hebben.</span><span class="sxs-lookup"><span data-stu-id="05c59-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="05c59-212">U kunt deze installeren via Windows Update door de optionele update Microsoft .NET Framework 4.5.2 voor Windows Server 2008 R2 x64 64-systemen te installeren ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="05c59-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="05c59-213">Azure Disk Encryption wordt ondersteund op de volgende galerie van Azure op basis van Linux-server distributies en versies:</span><span class="sxs-lookup"><span data-stu-id="05c59-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="05c59-214">Linux-distributie</span><span class="sxs-lookup"><span data-stu-id="05c59-214">Linux Distribution</span></span> | <span data-ttu-id="05c59-215">Versie</span><span class="sxs-lookup"><span data-stu-id="05c59-215">Version</span></span> | <span data-ttu-id="05c59-216">Type van het volume voor de versleuteling wordt ondersteund</span><span class="sxs-lookup"><span data-stu-id="05c59-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="05c59-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="05c59-217">Ubuntu</span></span> | <span data-ttu-id="05c59-218">16.04-DAGELIJKS-TNS</span><span class="sxs-lookup"><span data-stu-id="05c59-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="05c59-219">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-219">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="05c59-220">Ubuntu</span></span> | <span data-ttu-id="05c59-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="05c59-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="05c59-222">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-222">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="05c59-223">Ubuntu</span></span> | <span data-ttu-id="05c59-224">12.10</span><span class="sxs-lookup"><span data-stu-id="05c59-224">12.10</span></span> | <span data-ttu-id="05c59-225">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-225">Data disk</span></span> |
| <span data-ttu-id="05c59-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="05c59-226">Ubuntu</span></span> | <span data-ttu-id="05c59-227">12.04</span><span class="sxs-lookup"><span data-stu-id="05c59-227">12.04</span></span> | <span data-ttu-id="05c59-228">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-228">Data disk</span></span> |
| <span data-ttu-id="05c59-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="05c59-229">RHEL</span></span> | <span data-ttu-id="05c59-230">7.3</span><span class="sxs-lookup"><span data-stu-id="05c59-230">7.3</span></span> | <span data-ttu-id="05c59-231">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-231">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="05c59-232">RHEL</span></span> | <span data-ttu-id="05c59-233">7.2</span><span class="sxs-lookup"><span data-stu-id="05c59-233">7.2</span></span> | <span data-ttu-id="05c59-234">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-234">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="05c59-235">RHEL</span></span> | <span data-ttu-id="05c59-236">6.8</span><span class="sxs-lookup"><span data-stu-id="05c59-236">6.8</span></span> | <span data-ttu-id="05c59-237">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-237">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="05c59-238">RHEL</span></span> | <span data-ttu-id="05c59-239">6.7</span><span class="sxs-lookup"><span data-stu-id="05c59-239">6.7</span></span> | <span data-ttu-id="05c59-240">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-240">Data disk</span></span> |
| <span data-ttu-id="05c59-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-241">CentOS</span></span> | <span data-ttu-id="05c59-242">7.3</span><span class="sxs-lookup"><span data-stu-id="05c59-242">7.3</span></span> | <span data-ttu-id="05c59-243">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-243">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-244">CentOS</span></span> | <span data-ttu-id="05c59-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="05c59-245">7.2n</span></span> | <span data-ttu-id="05c59-246">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-246">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-247">CentOS</span></span> | <span data-ttu-id="05c59-248">6.8</span><span class="sxs-lookup"><span data-stu-id="05c59-248">6.8</span></span> | <span data-ttu-id="05c59-249">Besturingssysteem en schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-249">OS and Data disk</span></span> |
| <span data-ttu-id="05c59-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-250">CentOS</span></span> | <span data-ttu-id="05c59-251">7.1</span><span class="sxs-lookup"><span data-stu-id="05c59-251">7.1</span></span> | <span data-ttu-id="05c59-252">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-252">Data disk</span></span> |
| <span data-ttu-id="05c59-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-253">CentOS</span></span> | <span data-ttu-id="05c59-254">7.0</span><span class="sxs-lookup"><span data-stu-id="05c59-254">7.0</span></span> | <span data-ttu-id="05c59-255">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-255">Data disk</span></span> |
| <span data-ttu-id="05c59-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-256">CentOS</span></span> | <span data-ttu-id="05c59-257">6.7</span><span class="sxs-lookup"><span data-stu-id="05c59-257">6.7</span></span> | <span data-ttu-id="05c59-258">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-258">Data disk</span></span> |
| <span data-ttu-id="05c59-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-259">CentOS</span></span> | <span data-ttu-id="05c59-260">6.6</span><span class="sxs-lookup"><span data-stu-id="05c59-260">6.6</span></span> | <span data-ttu-id="05c59-261">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-261">Data disk</span></span> |
| <span data-ttu-id="05c59-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="05c59-262">CentOS</span></span> | <span data-ttu-id="05c59-263">6.5</span><span class="sxs-lookup"><span data-stu-id="05c59-263">6.5</span></span> | <span data-ttu-id="05c59-264">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-264">Data disk</span></span> |
| <span data-ttu-id="05c59-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="05c59-265">openSUSE</span></span> | <span data-ttu-id="05c59-266">13.2</span><span class="sxs-lookup"><span data-stu-id="05c59-266">13.2</span></span> | <span data-ttu-id="05c59-267">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-267">Data disk</span></span> |
| <span data-ttu-id="05c59-268">SLES</span><span class="sxs-lookup"><span data-stu-id="05c59-268">SLES</span></span> | <span data-ttu-id="05c59-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="05c59-269">12 SP1</span></span> | <span data-ttu-id="05c59-270">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-270">Data disk</span></span> |
| <span data-ttu-id="05c59-271">SLES</span><span class="sxs-lookup"><span data-stu-id="05c59-271">SLES</span></span> | <span data-ttu-id="05c59-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="05c59-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="05c59-273">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-273">Data disk</span></span> |
| <span data-ttu-id="05c59-274">SLES</span><span class="sxs-lookup"><span data-stu-id="05c59-274">SLES</span></span> | <span data-ttu-id="05c59-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="05c59-275">HPC 12</span></span> | <span data-ttu-id="05c59-276">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-276">Data disk</span></span> |
| <span data-ttu-id="05c59-277">SLES</span><span class="sxs-lookup"><span data-stu-id="05c59-277">SLES</span></span> | <span data-ttu-id="05c59-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="05c59-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="05c59-279">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-279">Data disk</span></span> |
| <span data-ttu-id="05c59-280">SLES</span><span class="sxs-lookup"><span data-stu-id="05c59-280">SLES</span></span> | <span data-ttu-id="05c59-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="05c59-281">11 SP4</span></span> | <span data-ttu-id="05c59-282">Gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="05c59-282">Data disk</span></span> |

* <span data-ttu-id="05c59-283">Azure Disk Encryption is vereist dat uw sleutelkluis en de virtuele machines zich in de dezelfde Azure-regio en het abonnement bevinden.</span><span class="sxs-lookup"><span data-stu-id="05c59-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-284">Configureren van de resources in afzonderlijke regio's zorgt ervoor dat een fout opgetreden bij het inschakelen van de functie Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="05c59-285">Als u wilt installeren en configureren van de sleutelkluis voor Azure Disk Encryption, Zie de sectie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in de *vereisten* sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="05c59-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="05c59-286">Als u wilt installeren en configureren van Azure AD-toepassing in Azure Active directory voor Azure Disk Encryption, Zie de sectie **instellen van de Azure AD-toepassing in Azure Active Directory** in de *vereisten* sectie in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="05c59-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="05c59-287">Als u wilt installeren en configureren van de sleutelkluis-toegangsbeleid voor de Azure AD-toepassing, Zie de sectie **de sleutelkluis-beleid instellen voor de Azure AD-toepassing** in de *vereisten* sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="05c59-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="05c59-288">Als u een Windows-VHD vooraf zijn versleuteld, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Windows VHD** in de *bijlage*.</span><span class="sxs-lookup"><span data-stu-id="05c59-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="05c59-289">Als u een vooraf zijn versleuteld Linux VHD, Zie de sectie **voorbereiden van een vooraf zijn versleuteld Linux VHD** in de *bijlage*.</span><span class="sxs-lookup"><span data-stu-id="05c59-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="05c59-290">De Azure-platform moet toegang tot de versleutelingssleutels of geheimen in de sleutelkluis zodat ze beschikbaar zijn op de virtuele machine is wanneer deze wordt opgestart en het besturingssysteemvolume virtuele machine ontsleutelt.</span><span class="sxs-lookup"><span data-stu-id="05c59-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="05c59-291">Om machtigingen te verlenen voor Azure-platform, stel de **EnabledForDiskEncryption** eigenschap in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="05c59-292">Zie voor meer informatie **instellen boven en uw sleutelkluis configureren voor Azure Disk Encryption** in de bijlage.</span><span class="sxs-lookup"><span data-stu-id="05c59-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="05c59-293">Uw sleutelkluis geheim en de KEK-URL's moeten samengestelde zijn.</span><span class="sxs-lookup"><span data-stu-id="05c59-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="05c59-294">Azure zorgt ervoor dat deze beperking versiebeheer.</span><span class="sxs-lookup"><span data-stu-id="05c59-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="05c59-295">Zie de volgende voorbeelden voor geldige geheim en KEK-URL's:</span><span class="sxs-lookup"><span data-stu-id="05c59-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="05c59-296">Voorbeeld van een geldige URL geheime: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="05c59-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="05c59-297">Voorbeeld van een geldige KEK-URL: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="05c59-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="05c59-298">Azure Disk Encryption biedt geen ondersteuning voor het opgeven van poortnummers als onderdeel van de sleutelkluis geheimen en KEK-URL's.</span><span class="sxs-lookup"><span data-stu-id="05c59-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="05c59-299">Voor voorbeelden van niet-ondersteunde en ondersteunde sleutelkluis-URL's, Zie de volgende:</span><span class="sxs-lookup"><span data-stu-id="05c59-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="05c59-300">Onaanvaardbaar sleutelkluis-URL *https://contosovault.vault.azure.net:443/geheimen/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="05c59-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="05c59-301">Acceptabele sleutelkluis-URL: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="05c59-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="05c59-302">Als u wilt inschakelen, de Azure Disk Encryption functie, de IaaS VM's moet voldoen aan de volgende configuratievereisten voor netwerk-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="05c59-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="05c59-303">Als u een token voor verbinding maken met uw sleutelkluis, de IaaS VM moet verbinding maken met een Azure Active Directory-eindpunt \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="05c59-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="05c59-304">Als de versleutelingssleutels opslaan op uw sleutelkluis, moet de IaaS VM verbinding kunnen maken met het eindpunt van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="05c59-305">De IaaS VM moet verbinding maken met een Azure-opslag-eindpunt dat als host fungeert voor de extensie Azure-opslagplaats en een Azure storage-account dat als host fungeert voor de VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="05c59-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="05c59-306">Als het beveiligingsbeleid van uw Azure VM's toegang heeft tot Internet beperkt, kunt u de voorgaande URI oplossen en configureren van een specifieke regel voor het toestaan van uitgaande verbinding met de IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="05c59-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="05c59-307">Om te configureren en toegang tot Azure Key Vault achter een firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="05c59-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="05c59-308">Gebruik de nieuwste versie van Azure PowerShell SDK-versie van Azure Disk Encryption te configureren.</span><span class="sxs-lookup"><span data-stu-id="05c59-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="05c59-309">Download de nieuwste versie van [Azure PowerShell-versie](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="05c59-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="05c59-310">Azure Disk Encryption wordt niet ondersteund op [Azure PowerShell SDK-versie 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="05c59-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="05c59-311">Als u ontvangt een foutbericht over het gebruik van Azure PowerShell 1.1.0, raadpleegt u [Azure schijf versleuteling fout met betrekking tot Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="05c59-312">Als u wilt willekeurige opdracht van de Azure CLI uitgevoerd en deze koppelen aan uw Azure-abonnement, moet u eerst de Azure CLI installeren:</span><span class="sxs-lookup"><span data-stu-id="05c59-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="05c59-313">Zie wilt Azure CLI installeren en deze koppelen aan uw Azure-abonnement, [installeren en configureren van Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="05c59-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="05c59-314">Zie voor het gebruik van Azure CLI voor Mac, Linux en Windows Azure Resource Manager, [Azure CLI-opdrachten in de modus Resource Manager](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="05c59-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="05c59-315">Bij het versleutelen van een beheerde schijf is verplicht vereiste voor het uitvoeren van een momentopname van de beheerde schijf of een back-up van de schijf buiten Azure Disk Encryption voorafgaand aan de codering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="05c59-316">Zonder een back-up op locatie, ervoor een onverwachte fout opgetreden tijdens het versleutelen zorgen dat de schijf en de VM toegankelijk zijn zonder een hersteloptie.</span><span class="sxs-lookup"><span data-stu-id="05c59-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="05c59-317">Set-AzureRmVMDiskEncryptionExtension momenteel geen back-up beheerde schijven en wordt fout als op een beheerde schijf gebruikt, tenzij de parameter - skipVmBackup is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="05c59-318">Deze parameter is niet veilig om te gebruiken, tenzij een back-up al is gemaakt buiten Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="05c59-319">Als de parameter - skipVmBackup wordt opgegeven, wordt de cmdlet een back-up van de beheerde schijf vóór versleuteling niet maken.</span><span class="sxs-lookup"><span data-stu-id="05c59-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="05c59-320">Daarom wordt het beschouwd als een verplichte vereisten om te controleren of een back-up van de beheerde schijf dat VM is geïmplementeerd voordat u Azure Disk Encryption inschakelt in geval herstel later nodig.</span><span class="sxs-lookup"><span data-stu-id="05c59-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="05c59-321">De parameter - skipVmBackup mag nooit worden gebruikt tenzij een momentopname of een back-up al is gemaakt buiten Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="05c59-322">De oplossing voor Azure Disk Encryption maakt gebruik van de externe BitLocker-sleutelbeveiliging voor IaaS VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="05c59-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="05c59-323">Push Groepsbeleid dat TPM beveiligingen afdwingen voor domein gekoppelde virtuele machines, niet.</span><span class="sxs-lookup"><span data-stu-id="05c59-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="05c59-324">Zie voor meer informatie over het groepsbeleid voor 'Toestaan dat BitLocker zonder een compatibele TPM' [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="05c59-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="05c59-325">BitLocker-Groepsbeleid op virtuele machines die lid van domein voor de aangepaste vergezeld gaan van de volgende instelling: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption mislukken wanneer aangepaste groepsbeleidsinstellingen voor Bitlocker niet compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="05c59-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="05c59-326">Op computers die niet het juiste beleid instelling, het nieuwe beleid wordt toegepast, waardoor het nieuwe beleid om bij te werken (gpupdate.exe/Force) en vervolgens opnieuw te starten mogelijk zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="05c59-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="05c59-327">Een Azure AD-toepassing maken, een sleutelkluis maken of een bestaande sleutelkluis instellen en versleuteling inschakelen, raadpleegt de [vereiste PowerShell-script voor Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="05c59-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="05c59-328">Als u wilt configureren met de Azure CLI-schijfversleuteling-vereisten, Zie [dit script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="05c59-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="05c59-329">Als u de Azure Backup-service wilt back-up en herstel van versleutelde virtuele machines, als versleuteling is ingeschakeld met Azure Disk Encryption, uw virtuele machines te versleutelen met behulp van de configuratie van de Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="05c59-330">De Backup-service biedt ondersteuning voor virtuele machines die zijn versleuteld met alleen een KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="05c59-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="05c59-331">Zie [back-up en herstellen versleuteld virtuele machines met Azure Backup-versleuteling](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="05c59-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="05c59-332">Bij het versleutelen van een volume met het Linux-besturingssysteem, houd er rekening mee dat VM moet worden opgestart op dat moment aan het einde van het proces.</span><span class="sxs-lookup"><span data-stu-id="05c59-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="05c59-333">Dit kan worden gedaan via de portal, powershell of CLI.</span><span class="sxs-lookup"><span data-stu-id="05c59-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="05c59-334">Om de voortgang van versleuteling volgen, het statusbericht dat is geretourneerd door Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus periodiek te pollen.</span><span class="sxs-lookup"><span data-stu-id="05c59-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="05c59-335">Zodra de codering is voltooid, de het statusbericht dat is geretourneerd door deze opdracht wordt dit aangegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="05c59-336">Bijvoorbeeld ' ProgressMessage: besturingssysteemschijf is versleuteld, start u de virtuele machine ' op dit moment de virtuele machine kan worden gestart en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05c59-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="05c59-337">Azure Disk Encryption voor Linux gegevensschijven bevatten een gekoppeld bestandssysteem Linux vóór versleuteling is vereist</span><span class="sxs-lookup"><span data-stu-id="05c59-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="05c59-338">Recursief gekoppelde schijven worden niet ondersteund door de Azure Disk Encryption voor Linux.</span><span class="sxs-lookup"><span data-stu-id="05c59-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="05c59-339">Als bijvoorbeeld het doelsysteem een schijf is gekoppeld op foo/balk en slaagt op /foo/bar/baz, de versleuteling van /foo/bar/baz, maar de versleuteling van foo/balk mislukken.</span><span class="sxs-lookup"><span data-stu-id="05c59-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="05c59-340">Azure Disk Encryption wordt alleen ondersteund op Azure-galerie ondersteund installatiekopieën die voldoen aan de hiervoor genoemde vereisten.</span><span class="sxs-lookup"><span data-stu-id="05c59-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="05c59-341">Klanten aangepaste installatiekopieën worden niet ondersteund als gevolg van proces-gedrag die mogelijk aanwezig zijn op deze installatiekopieën en aangepaste partitieschema's.</span><span class="sxs-lookup"><span data-stu-id="05c59-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="05c59-342">Bovendien is zelfs afbeelding op basis van de virtuele machine die in eerste instantie vereisten wordt voldaan, maar zijn gewijzigd nadat het maken van zijn mogelijk niet compatibel.</span><span class="sxs-lookup"><span data-stu-id="05c59-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="05c59-343">Voor die is daarom moet de aanbevolen procedure voor het versleutelen van een Linux-VM starten vanuit een schone afbeelding, versleutelen van de virtuele machine en vervolgens aangepaste software of gegevens toevoegen aan de virtuele machine zo nodig.</span><span class="sxs-lookup"><span data-stu-id="05c59-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="05c59-344">Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor virtuele machines die zijn versleuteld met de KEK-configuratie.</span><span class="sxs-lookup"><span data-stu-id="05c59-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="05c59-345">Dit wordt niet ondersteund op virtuele machines die zijn versleuteld zonder KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="05c59-346">KEK-sleutel is een optionele parameter waarmee de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="05c59-347">Instellen van de Azure AD-toepassing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05c59-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="05c59-348">U moet de versleuteling zijn ingeschakeld op een actieve virtuele machine in Azure, Azure Disk Encryption genereert als de versleutelingssleutels schrijft naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="05c59-349">Het beheren van versleutelingssleutels in de sleutelkluis vereist Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="05c59-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="05c59-350">Maak een Azure AD-toepassing voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="05c59-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="05c59-351">U vindt gedetailleerde stappen voor het registreren van een toepassing in de sectie 'Een identiteit voor de toepassing ophalen' van het blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="05c59-352">Dit bericht bevat ook een aantal handige voorbeelden voor het instellen en configureren van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="05c59-353">U kunt op basis van een geheim clientverificatie of clientverificatie Azure AD op basis van certificaten gebruiken voor verificatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="05c59-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="05c59-354">Clientverificatie op basis van een geheim voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c59-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="05c59-355">De volgende secties kunt u een client geheim gebaseerde verificatie voor Azure AD configureren.</span><span class="sxs-lookup"><span data-stu-id="05c59-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="05c59-356">Een Azure AD-toepassing maken met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="05c59-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="05c59-357">Gebruik de volgende PowerShell-cmdlet voor het maken van een Azure AD-toepassing:</span><span class="sxs-lookup"><span data-stu-id="05c59-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="05c59-358">$azureAdApplication.ApplicationId is de Azure AD-ClientID en $aadClientSecret het clientgeheim die u later gebruiken moet om Azure Disk Encryption is.</span><span class="sxs-lookup"><span data-stu-id="05c59-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="05c59-359">De Azure AD-clientgeheim op de juiste wijze beveiligt.</span><span class="sxs-lookup"><span data-stu-id="05c59-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="05c59-360">Het Azure AD-client-ID en het geheim instellen vanuit de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="05c59-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="05c59-361">U kunt ook van uw Azure AD-client-ID en geheim instellen met behulp van de [klassieke Azure-portal]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="05c59-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="05c59-362">Ga als volgt te werk als u wilt uitvoeren van deze taak:</span><span class="sxs-lookup"><span data-stu-id="05c59-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="05c59-363">Klik op de **Active Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="05c59-363">Click the **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="05c59-365">Klik op **toepassing toevoegen**, en typ vervolgens de naam van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="05c59-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="05c59-367">Klik op de pijl en configureer vervolgens de eigenschappen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="05c59-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="05c59-369">Klik op het vinkje in de linkerbenedenhoek te voltooien.</span><span class="sxs-lookup"><span data-stu-id="05c59-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="05c59-370">De configuratiepagina van de toepassing wordt weergegeven en de Azure AD-client-ID aan de onderkant van de pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="05c59-372">Opslaan van de Azure AD-clientgeheim door te klikken op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="05c59-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="05c59-373">Let op het Azure AD-clientgeheim in het tekstvak sleutels.</span><span class="sxs-lookup"><span data-stu-id="05c59-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="05c59-374">Op de juiste wijze beveiligt.</span><span class="sxs-lookup"><span data-stu-id="05c59-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="05c59-376">De voorgaande stroom wordt niet ondersteund in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05c59-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="05c59-377">Gebruik een bestaande toepassing</span><span class="sxs-lookup"><span data-stu-id="05c59-377">Use an existing application</span></span>
<span data-ttu-id="05c59-378">De volgende opdrachten worden uitgevoerd, downloadt en gebruikt de [Azure AD PowerShell-module](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-379">De volgende opdrachten moeten worden uitgevoerd vanuit een nieuwe PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="05c59-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="05c59-380">Gebruik geen Azure PowerShell of het venster Azure Resource Manager de opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="05c59-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="05c59-381">Deze aanpak wordt aangeraden omdat deze cmdlets in de MSOnline module of Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05c59-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="05c59-382">Verificatie op basis van certificaten voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c59-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="05c59-383">Azure AD gebaseerde verificatie is momenteel niet ondersteund op virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="05c59-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="05c59-384">De volgende secties laten zien hoe een verificatie op basis van certificaten voor Azure AD configureren.</span><span class="sxs-lookup"><span data-stu-id="05c59-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="05c59-385">Een Azure AD-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="05c59-385">Create an Azure AD application</span></span>
<span data-ttu-id="05c59-386">Uitvoeren van de volgende PowerShell-cmdlets voor het maken van een Azure AD-toepassing:</span><span class="sxs-lookup"><span data-stu-id="05c59-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-387">Vervang de volgende `yourpassword` tekenreeks met uw beveiligd wachtwoord en het wachtwoord te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="05c59-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="05c59-388">Nadat u deze stap, een PFX-bestand uploaden naar de sleutelkluis en het beleid voor toegang nodig is om te implementeren dat certificaat voor een virtuele machine inschakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="05c59-389">Gebruik een bestaande Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="05c59-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="05c59-390">Als u verificatie op basis van certificaten voor een bestaande toepassing configureren wilt, gebruikt u de PowerShell-cmdlets die hier worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="05c59-391">Zorg ervoor dat deze van een nieuwe PowerShell-venster uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="05c59-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="05c59-392">Nadat u deze stap, een PFX-bestand uploaden naar de sleutelkluis en het beleid dat nodig is voor het implementeren van het certificaat op een virtuele machine inschakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="05c59-393">Een PFX-bestand uploaden naar de sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="05c59-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="05c59-394">Zie voor een gedetailleerde uitleg van dit proces [de officiële Azure Key Vault teamblog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="05c59-395">De volgende PowerShell-cmdlets zijn echter alles wat die u nodig hebt voor de taak.</span><span class="sxs-lookup"><span data-stu-id="05c59-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="05c59-396">Zorg ervoor dat ze van Azure PowerShell-console uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="05c59-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-397">Vervang de volgende `yourpassword` tekenreeks met uw beveiligd wachtwoord en het wachtwoord te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="05c59-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="05c59-398">Een certificaat in de sleutelkluis implementeren naar een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="05c59-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="05c59-399">Nadat u de PFX uploaden, moet u een certificaat in de sleutelkluis implementeren naar een bestaande virtuele machine met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="05c59-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
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

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="05c59-400">De sleutelkluis-beleid voor de Azure AD-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="05c59-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="05c59-401">Uw Azure AD-toepassing moet rechten voor toegang tot de sleutels of geheimen in de kluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="05c59-402">Gebruik de [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet machtigen om de toepassing, de client-ID (die is gegenereerd toen de toepassing is geregistreerd) als de _– ServicePrincipalName_ parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="05c59-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="05c59-403">Zie voor meer informatie het blogbericht [Azure Sleutelkluis - stapsgewijze](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="05c59-404">Hier volgt een voorbeeld van hoe deze taak via PowerShell uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="05c59-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="05c59-405">Azure Disk Encryption moet u de volgende beleidsregels voor toegang op de clienttoepassing van uw Azure AD configureren: _WrapKey_ en _ingesteld_ machtigingen.</span><span class="sxs-lookup"><span data-stu-id="05c59-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="05c59-406">Terminologie</span><span class="sxs-lookup"><span data-stu-id="05c59-406">Terminology</span></span>
<span data-ttu-id="05c59-407">Om te begrijpen enkele van de algemene voorwaarden die door deze technologie gebruikt, gebruik de volgende terminologie-tabel:</span><span class="sxs-lookup"><span data-stu-id="05c59-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="05c59-408">Terminologie</span><span class="sxs-lookup"><span data-stu-id="05c59-408">Terminology</span></span> | <span data-ttu-id="05c59-409">Definitie</span><span class="sxs-lookup"><span data-stu-id="05c59-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="05c59-410">Azure AD</span></span> | <span data-ttu-id="05c59-411">Azure AD [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="05c59-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="05c59-412">Een Azure AD-account is een vereiste voor verificatie, opslaan en ophalen van geheimen van een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="05c59-413">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="05c59-413">Azure Key Vault</span></span> | <span data-ttu-id="05c59-414">Sleutelkluis is een cryptografische, key management service die gebaseerd op de Federal Information Processing Standards FIPS-gevalideerde hardware security modules, die ter bescherming van uw cryptografische sleutels en geheimen gevoelige.</span><span class="sxs-lookup"><span data-stu-id="05c59-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="05c59-415">Zie voor meer informatie [Sleutelkluis](https://azure.microsoft.com/services/key-vault/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="05c59-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="05c59-416">ARM</span><span class="sxs-lookup"><span data-stu-id="05c59-416">ARM</span></span> | <span data-ttu-id="05c59-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05c59-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="05c59-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="05c59-418">BitLocker</span></span> |<span data-ttu-id="05c59-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is een industrie herkend Windows volume versleuteling technologie die wordt gebruikt om in te schakelen schijfversleuteling op IaaS VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="05c59-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="05c59-420">BEK</span><span class="sxs-lookup"><span data-stu-id="05c59-420">BEK</span></span> | <span data-ttu-id="05c59-421">BitLocker-versleutelingssleutels worden gebruikt voor het versleutelen van het opstartvolume OS en gegevensvolumes.</span><span class="sxs-lookup"><span data-stu-id="05c59-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="05c59-422">De BitLocker-sleutels worden beveiligd in een sleutelkluis als geheimen.</span><span class="sxs-lookup"><span data-stu-id="05c59-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="05c59-423">CLI</span><span class="sxs-lookup"><span data-stu-id="05c59-423">CLI</span></span> | <span data-ttu-id="05c59-424">Zie [Azure-opdrachtregelinterface](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="05c59-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="05c59-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="05c59-425">DM-Crypt</span></span> |<span data-ttu-id="05c59-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is het subsysteem voor op basis van Linux, transparant schijfversleuteling die wordt gebruikt voor het inschakelen van schijfversleuteling op Linux IaaS VM's.</span><span class="sxs-lookup"><span data-stu-id="05c59-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="05c59-427">KEK</span><span class="sxs-lookup"><span data-stu-id="05c59-427">KEK</span></span> | <span data-ttu-id="05c59-428">Sleutelcodering sleutel is de asymmetrische sleutel (RSA 2048) die u gebruiken kunt om te beveiligen of het geheim inpakken.</span><span class="sxs-lookup"><span data-stu-id="05c59-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="05c59-429">U kunt bieden een hardware security modules (HSM)-sleutel of met software beschermde sleutel beveiligd.</span><span class="sxs-lookup"><span data-stu-id="05c59-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="05c59-430">Zie voor meer informatie [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="05c59-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="05c59-431">PS-cmdlets</span><span class="sxs-lookup"><span data-stu-id="05c59-431">PS cmdlets</span></span> | <span data-ttu-id="05c59-432">Zie [Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05c59-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="05c59-433">Installeren en configureren van de sleutelkluis voor Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="05c59-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="05c59-434">Azure Disk Encryption helpt de de schijfversleuteling sleutels en geheimen in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="05c59-435">Als u de sleutelkluis voor Azure Disk Encryption instelt, voltooi de stappen in elk van de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="05c59-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="05c59-436">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="05c59-436">Create a key vault</span></span>
<span data-ttu-id="05c59-437">Als u wilt een sleutelkluis maken, gebruikt u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="05c59-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="05c59-438">Resource Manager-sjabloon '101-sleutel-kluis-maken'</span><span class="sxs-lookup"><span data-stu-id="05c59-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="05c59-439">Azure PowerShell-cmdlets voor sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="05c59-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="05c59-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05c59-440">Azure Resource Manager</span></span>
* <span data-ttu-id="05c59-441">Hoe [beveiligen van uw sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="05c59-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-442">Als u hebt al een sleutelkluis ingesteld voor uw abonnement, gaat u naar de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="05c59-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="05c59-444">Instellen van een coderingssleutel voor de sleutel (optioneel)</span><span class="sxs-lookup"><span data-stu-id="05c59-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="05c59-445">Als u een KEK-sleutel voor een extra beveiligingslaag voor de versleutelingssleutels BitLocker gebruiken wilt, moet u een KEK toevoegen aan de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="05c59-446">Gebruik de [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet voor het maken van een coderingssleutel voor de sleutel in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="05c59-447">U kunt ook een KEK importeren uit uw lokale Sleutelbeheer HSM.</span><span class="sxs-lookup"><span data-stu-id="05c59-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="05c59-448">Zie voor meer informatie [Sleutelkluis documentatie](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="05c59-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="05c59-449">U kunt de KEK toevoegen door te gaan in Azure Resource Manager of met behulp van de sleutelkluis-interface.</span><span class="sxs-lookup"><span data-stu-id="05c59-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="05c59-451">Sleutelkluis-machtigingen instellen</span><span class="sxs-lookup"><span data-stu-id="05c59-451">Set key vault permissions</span></span>
<span data-ttu-id="05c59-452">De Azure-platform moet toegang tot de versleutelingssleutels of geheimen in de sleutelkluis zodat ze beschikbaar met de virtuele machine voor het opstarten en ontsleutelen van de volumes.</span><span class="sxs-lookup"><span data-stu-id="05c59-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="05c59-453">Om machtigingen te verlenen voor het Azure-platform, stel de **EnabledForDiskEncryption** eigenschap in de sleutel met behulp van de sleutelkluis PowerShell-cmdlet-kluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="05c59-454">U kunt ook instellen de **EnabledForDiskEncryption** eigenschap in via de [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05c59-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="05c59-455">Zoals eerder vermeld, stelt u de **EnabledForDiskEncryption** eigenschap in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="05c59-456">Anders mislukt de implementatie.</span><span class="sxs-lookup"><span data-stu-id="05c59-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="05c59-457">U kunt beleidsregels voor toegang instellen voor uw Azure AD-toepassing van de sleutelkluis-interface, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="05c59-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="05c59-460">Op de **geavanceerde toegangsbeleid** tabblad, zorg ervoor dat de sleutelkluis voor Azure Disk Encryption is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="05c59-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure sleutelkluis](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="05c59-462">Implementatiescenario's voor schijf-codering en gebruikerservaringen</span><span class="sxs-lookup"><span data-stu-id="05c59-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="05c59-463">U kunt veel scenario's voor schijf-codering inschakelen en de stappen kunnen variëren afhankelijk van het scenario.</span><span class="sxs-lookup"><span data-stu-id="05c59-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="05c59-464">De volgende secties hebben betrekking op de scenario's met meer details.</span><span class="sxs-lookup"><span data-stu-id="05c59-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="05c59-465">Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van de Marketplace</span><span class="sxs-lookup"><span data-stu-id="05c59-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="05c59-466">U kunt schijfversleuteling op nieuwe IaaS virtuele machine van Windows uit in Azure Marketplace inschakelen met behulp van de [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="05c59-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="05c59-467">Klik op de Azure snel starten-sjabloon **implementeren in Azure**, voer de configuratie van de versleuteling in op de **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c59-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="05c59-468">Selecteer het abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** versleuteling op een nieuwe IaaS VM in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-469">Deze sjabloon maakt een nieuwe versleutelde Windows virtuele machine die gebruikmaakt van de installatiekopie van het Windows Server 2012-galerie.</span><span class="sxs-lookup"><span data-stu-id="05c59-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="05c59-470">U kunt schijfversleuteling op een nieuwe IaaS RedHat Linux 7.2 virtuele machine met een matrix van 200 GB RAID-0 inschakelen met behulp van dit [Resource Manager-sjabloon](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="05c59-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="05c59-471">Nadat u de sjabloon hebt geïmplementeerd, de status van de versleuteling VM controleren met behulp van de `Get-AzureRmVmDiskEncryptionStatus` cmdlet, zoals beschreven in [OS versleutelen station op een actieve Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="05c59-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="05c59-472">Wanneer de machine de status retourneert _VMRestartPending_, opnieuw opstarten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="05c59-473">De volgende tabel bevat de parameters van de Resource Manager-sjabloon voor de nieuwe virtuele machines van de Marketplace-scenario met behulp van Azure AD-client-ID:</span><span class="sxs-lookup"><span data-stu-id="05c59-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="05c59-474">Parameter</span><span class="sxs-lookup"><span data-stu-id="05c59-474">Parameter</span></span> | <span data-ttu-id="05c59-475">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05c59-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="05c59-476">adminUserName</span></span> | <span data-ttu-id="05c59-477">De beheerdersgebruikersnaam voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="05c59-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="05c59-478">adminPassword</span></span> | <span data-ttu-id="05c59-479">Beheerderswachtwoord voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="05c59-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="05c59-480">newStorageAccountName</span></span> | <span data-ttu-id="05c59-481">De naam van het opslagaccount voor het besturingssysteem en VHD's opslaan.</span><span class="sxs-lookup"><span data-stu-id="05c59-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="05c59-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="05c59-482">vmSize</span></span> | <span data-ttu-id="05c59-483">De grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-483">Size of the VM.</span></span> <span data-ttu-id="05c59-484">Op dit moment worden alleen standaard A, D en G reeksen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="05c59-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="05c59-485">virtualNetworkName</span></span> | <span data-ttu-id="05c59-486">Naam van het VNet dat de VM-NIC tot behoren moet.</span><span class="sxs-lookup"><span data-stu-id="05c59-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="05c59-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="05c59-487">subnetName</span></span> | <span data-ttu-id="05c59-488">Naam van het subnet in het VNet dat de VM-NIC tot behoren moet.</span><span class="sxs-lookup"><span data-stu-id="05c59-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="05c59-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="05c59-489">AADClientID</span></span> | <span data-ttu-id="05c59-490">Client-ID van de Azure AD-toepassing die machtigingen heeft voor het schrijven van geheimen naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="05c59-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="05c59-491">AADClientSecret</span></span> | <span data-ttu-id="05c59-492">Clientgeheim van de Azure AD-toepassing die machtigingen heeft voor het schrijven van geheimen naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="05c59-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="05c59-493">keyVaultURL</span></span> | <span data-ttu-id="05c59-494">URL van de sleutelkluis die de BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="05c59-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="05c59-495">U kunt dit downloaden via de cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="05c59-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="05c59-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="05c59-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="05c59-497">URL van de belangrijkste versleutelingssleutel die wordt gebruikt voor het versleutelen van de gegenereerde BitLocker-sleutel (optioneel).</span><span class="sxs-lookup"><span data-stu-id="05c59-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="05c59-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="05c59-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="05c59-499">De resourcegroep van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="05c59-500">vmName</span><span class="sxs-lookup"><span data-stu-id="05c59-500">vmName</span></span> | <span data-ttu-id="05c59-501">Naam van de virtuele machine die de versleutelingsbewerking op worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="05c59-502">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="05c59-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="05c59-503">U kunt brengt uw eigen KEK voor verdere beveiliging de gegevensversleutelingssleutel (geheime wachtwoordzin) in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="05c59-504">Schakel versleuteling in op de nieuwe IaaS VM's die zijn gemaakt van de klant versleuteld VHD- en versleutelingssleutels</span><span class="sxs-lookup"><span data-stu-id="05c59-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="05c59-505">In dit scenario kunt u inschakelen versleutelen met behulp van de Resource Manager-sjabloon, het PowerShell-cmdlets of de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="05c59-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="05c59-506">De volgende secties wordt uitgelegd in meer detail de Resource Manager-sjabloon en de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="05c59-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="05c59-507">Volg de instructies uit een van deze secties voor het voorbereiden van vooraf zijn versleuteld afbeeldingen die kunnen worden gebruikt in Azure.</span><span class="sxs-lookup"><span data-stu-id="05c59-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="05c59-508">Nadat de installatiekopie is gemaakt, kunt u de stappen in de volgende sectie voor het maken van een versleutelde Azure VM.</span><span class="sxs-lookup"><span data-stu-id="05c59-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="05c59-509">Een vooraf zijn versleuteld Windows VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="05c59-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="05c59-510">Een vooraf zijn versleuteld Linux VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="05c59-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="05c59-511">Met behulp van de Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="05c59-511">Using the Resource Manager template</span></span>
<span data-ttu-id="05c59-512">U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van de [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="05c59-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="05c59-513">Klik op de Azure snel starten-sjabloon **implementeren in Azure**, voer de configuratie van de versleuteling in op de **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c59-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="05c59-514">Selecteer het abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** versleuteling op de nieuwe IaaS VM in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="05c59-515">De volgende tabel bevat de parameters van de Resource Manager-sjabloon voor de versleutelde VHD:</span><span class="sxs-lookup"><span data-stu-id="05c59-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="05c59-516">Parameter</span><span class="sxs-lookup"><span data-stu-id="05c59-516">Parameter</span></span> | <span data-ttu-id="05c59-517">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05c59-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="05c59-518">newStorageAccountName</span></span> | <span data-ttu-id="05c59-519">De naam van het opslagaccount voor het opslaan van de versleutelde OS-VHD.</span><span class="sxs-lookup"><span data-stu-id="05c59-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="05c59-520">Dit opslagaccount moet al zijn gemaakt in dezelfde resourcegroep en dezelfde locatie als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="05c59-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="05c59-521">osVhdUri</span></span> | <span data-ttu-id="05c59-522">De URI van de VHD OS vanuit het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="05c59-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="05c59-523">besturingssysteemtype</span><span class="sxs-lookup"><span data-stu-id="05c59-523">osType</span></span> | <span data-ttu-id="05c59-524">Type besturingssysteem product (Windows of Linux).</span><span class="sxs-lookup"><span data-stu-id="05c59-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="05c59-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="05c59-525">virtualNetworkName</span></span> | <span data-ttu-id="05c59-526">Naam van het VNet dat de VM-NIC tot behoren moet.</span><span class="sxs-lookup"><span data-stu-id="05c59-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="05c59-527">De naam moet al zijn gemaakt in dezelfde resourcegroep en dezelfde locatie als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="05c59-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="05c59-528">subnetName</span></span> | <span data-ttu-id="05c59-529">Naam van het subnet in het VNet dat de VM-NIC tot behoren moet.</span><span class="sxs-lookup"><span data-stu-id="05c59-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="05c59-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="05c59-530">vmSize</span></span> | <span data-ttu-id="05c59-531">De grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-531">Size of the VM.</span></span> <span data-ttu-id="05c59-532">Op dit moment worden alleen standaard A, D en G reeksen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="05c59-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="05c59-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="05c59-533">keyVaultResourceID</span></span> | <span data-ttu-id="05c59-534">De ResourceID die de sleutelkluis-resource in Azure Resource Manager identificeert.</span><span class="sxs-lookup"><span data-stu-id="05c59-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="05c59-535">U kunt dit downloaden met behulp van de PowerShell-cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="05c59-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="05c59-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="05c59-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="05c59-537">De URL van de schijf-versleutelingssleutel die ingesteld in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="05c59-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="05c59-538">keyVaultKekUrl</span></span> | <span data-ttu-id="05c59-539">De URL van de belangrijkste coderingssleutel voor het versleutelen van de versleutelingssleutel van de gegenereerde schijf.</span><span class="sxs-lookup"><span data-stu-id="05c59-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="05c59-540">vmName</span><span class="sxs-lookup"><span data-stu-id="05c59-540">vmName</span></span> | <span data-ttu-id="05c59-541">Naam van de IaaS-VM.</span><span class="sxs-lookup"><span data-stu-id="05c59-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="05c59-542">Met behulp van PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="05c59-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="05c59-543">U kunt schijfversleuteling op uw versleutelde VHD inschakelen met behulp van de PowerShell-cmdlet [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="05c59-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="05c59-544">CLI-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="05c59-544">Using CLI commands</span></span>
<span data-ttu-id="05c59-545">Schakel schijfversleuteling voor dit scenario met behulp van de CLI-opdrachten door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="05c59-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="05c59-546">Toegangsbeleid instellen in de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="05c59-547">Stel de **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="05c59-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="05c59-548">Stel machtigingen in op Azure AD-toepassing geheimen schrijven naar de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="05c59-549">Het inschakelen van versleuteling op een bestaande of actieve virtuele machine, typt u:</span><span class="sxs-lookup"><span data-stu-id="05c59-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="05c59-550">Versleutelingsstatus ophalen:</span><span class="sxs-lookup"><span data-stu-id="05c59-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="05c59-551">Gebruik de volgende parameters met het inschakelen van versleuteling op een nieuwe virtuele machine van de versleutelde VHD, de `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="05c59-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="05c59-552">Schakel versleuteling in op de bestaande of IaaS virtuele Windows-machine in Azure wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="05c59-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="05c59-553">In dit scenario kunt u inschakelen versleutelen met behulp van de Resource Manager-sjabloon, het PowerShell-cmdlets of de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="05c59-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="05c59-554">De volgende secties wordt uitgelegd in meer detail hoe in te schakelen met behulp van de Resource Manager-sjabloon en de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="05c59-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="05c59-555">Met behulp van de Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="05c59-555">Using the Resource Manager template</span></span>
<span data-ttu-id="05c59-556">U kunt inschakelen schijfversleuteling op bestaande of IaaS VM's van Windows worden uitgevoerd in Azure met behulp van de [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="05c59-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="05c59-557">Klik op de Azure snel starten-sjabloon **implementeren in Azure**, voer de configuratie van de versleuteling in op de **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c59-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="05c59-558">Selecteer het abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** versleuteling op de bestaande of actief IaaS VM in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="05c59-559">De volgende tabel bevat de Resource Manager-Sjabloonparameters voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="05c59-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="05c59-560">Parameter</span><span class="sxs-lookup"><span data-stu-id="05c59-560">Parameter</span></span> | <span data-ttu-id="05c59-561">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05c59-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="05c59-562">AADClientID</span></span> | <span data-ttu-id="05c59-563">Client-ID van de Azure AD-toepassing die gemachtigd is te schrijven geheimen tot de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="05c59-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="05c59-564">AADClientSecret</span></span> | <span data-ttu-id="05c59-565">Clientgeheim van de Azure AD-toepassing die gemachtigd is te schrijven geheimen tot de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="05c59-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="05c59-566">keyVaultName</span></span> | <span data-ttu-id="05c59-567">Naam van de sleutelkluis die de BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="05c59-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="05c59-568">U kunt dit downloaden via de cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="05c59-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="05c59-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="05c59-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="05c59-570">URL van de belangrijkste versleutelingssleutel die wordt gebruikt voor het versleutelen van de gegenereerde BitLocker-sleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="05c59-571">Deze parameter is optioneel als u selecteert **nokek** in de vervolgkeuzelijst UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="05c59-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="05c59-572">Als u selecteert **kek** in de vervolgkeuzelijst UseExistingKek moet u de _keyEncryptionKeyURL_ waarde.</span><span class="sxs-lookup"><span data-stu-id="05c59-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="05c59-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="05c59-573">volumeType</span></span> | <span data-ttu-id="05c59-574">Het type van het volume dat de coderingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="05c59-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="05c59-575">Geldige waarden zijn _OS_, _gegevens_, en _alle_.</span><span class="sxs-lookup"><span data-stu-id="05c59-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="05c59-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="05c59-576">sequenceVersion</span></span> | <span data-ttu-id="05c59-577">De versie van de volgorde van de BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="05c59-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="05c59-578">Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="05c59-579">vmName</span><span class="sxs-lookup"><span data-stu-id="05c59-579">vmName</span></span> | <span data-ttu-id="05c59-580">Naam van de virtuele machine die de versleutelingsbewerking op worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="05c59-581">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="05c59-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="05c59-582">U kunt uw eigen KEK de gegevensversleutelingssleutel (geheim BitLocker-versleuteling) in de sleutelkluis om verdere beveiliging te zetten.</span><span class="sxs-lookup"><span data-stu-id="05c59-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="05c59-583">Met behulp van PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="05c59-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="05c59-584">Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets, de blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="05c59-585">CLI-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="05c59-585">Using CLI commands</span></span>
<span data-ttu-id="05c59-586">Voor het inschakelen van versleuteling op bestaande of IaaS virtuele machine van Windows worden uitgevoerd in Azure CLI-opdrachten met het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="05c59-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="05c59-587">Toegangsbeleid instellen in de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="05c59-588">Stel de **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="05c59-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="05c59-589">Stel machtigingen in op Azure AD-toepassing geheimen schrijven naar de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="05c59-590">Schakel versleuteling in op een bestaande of actieve virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="05c59-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="05c59-591">Coderingsstatus ophalen:</span><span class="sxs-lookup"><span data-stu-id="05c59-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="05c59-592">Gebruik de volgende parameters met het inschakelen van versleuteling op een nieuwe virtuele machine van de versleutelde VHD, de `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="05c59-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="05c59-593">Schakel versleuteling in op een bestaande of actief IaaS virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="05c59-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="05c59-594">U kunt schijfversleuteling op een bestaande of actief IaaS Linux virtuele machine in Azure inschakelen met behulp van de [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="05c59-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="05c59-595">Klik op **implementeren in Azure** op de sjabloon voor Azure snel starten, voert u de configuratie van de versleuteling op de **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c59-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="05c59-596">Selecteer het abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** versleuteling op de bestaande of actief IaaS VM in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="05c59-597">De volgende tabel bevat de parameters van de Resource Manager-sjabloon voor bestaande of VM's die gebruikmaken van een client-ID van Azure AD worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="05c59-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="05c59-598">Parameter</span><span class="sxs-lookup"><span data-stu-id="05c59-598">Parameter</span></span> | <span data-ttu-id="05c59-599">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05c59-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="05c59-600">AADClientID</span></span> | <span data-ttu-id="05c59-601">Client-ID van de Azure AD-toepassing die gemachtigd is te schrijven geheimen tot de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="05c59-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="05c59-602">AADClientSecret</span></span> | <span data-ttu-id="05c59-603">Clientgeheim van de Azure AD-toepassing die machtigingen heeft voor het schrijven van geheimen naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="05c59-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="05c59-604">keyVaultName</span></span> | <span data-ttu-id="05c59-605">Naam van de sleutelkluis die de BitLocker-sleutel moet worden geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="05c59-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="05c59-606">U kunt dit downloaden via de cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="05c59-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="05c59-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="05c59-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="05c59-608">URL van de belangrijkste versleutelingssleutel die wordt gebruikt voor het versleutelen van de gegenereerde BitLocker-sleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="05c59-609">Deze parameter is optioneel als u selecteert **nokek** in de vervolgkeuzelijst UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="05c59-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="05c59-610">Als u selecteert **kek** in de vervolgkeuzelijst UseExistingKek moet u de _keyEncryptionKeyURL_ waarde.</span><span class="sxs-lookup"><span data-stu-id="05c59-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="05c59-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="05c59-611">volumeType</span></span> | <span data-ttu-id="05c59-612">Het type van het volume dat de coderingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="05c59-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="05c59-613">Geldige ondersteunde waarden zijn _OS_ of _alle_ (voor RHEL 7.2, CentOS 7.2 en Ubuntu 16.04) en _gegevens_ (voor alle andere distributies).</span><span class="sxs-lookup"><span data-stu-id="05c59-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="05c59-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="05c59-614">sequenceVersion</span></span> | <span data-ttu-id="05c59-615">De versie van de volgorde van de BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="05c59-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="05c59-616">Dit versienummer verhoogd telkens wanneer een schijfversleuteling bewerking wordt uitgevoerd op dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="05c59-617">vmName</span><span class="sxs-lookup"><span data-stu-id="05c59-617">vmName</span></span> | <span data-ttu-id="05c59-618">Naam van de virtuele machine die de versleutelingsbewerking op worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="05c59-619">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="05c59-619">passPhrase</span></span> | <span data-ttu-id="05c59-620">Typ een sterke wachtwoordzin als de gegevensversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="05c59-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="05c59-621">_KeyEncryptionKeyURL_ is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="05c59-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="05c59-622">U kunt brengt uw eigen KEK voor verdere beveiliging de gegevensversleutelingssleutel (geheime wachtwoordzin) in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="05c59-623">CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="05c59-623">CLI commands</span></span>
<span data-ttu-id="05c59-624">U kunt schijfversleuteling inschakelen op uw versleutelde VHD te installeren en gebruiken de [CLI opdracht](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="05c59-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="05c59-625">Ga als volgt te werk voor het inschakelen van versleuteling op bestaande of IaaS Linux VM's worden uitgevoerd in Azure met behulp van de CLI-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="05c59-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="05c59-626">Toegangsbeleid instellen in de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="05c59-627">Stel de **EnabledForDiskEncryption** vlag:</span><span class="sxs-lookup"><span data-stu-id="05c59-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="05c59-628">Stel machtigingen in op Azure AD-toepassing geheimen schrijven naar de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="05c59-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="05c59-629">Schakel versleuteling in op een bestaande of actieve virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="05c59-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="05c59-630">Versleutelingsstatus ophalen:</span><span class="sxs-lookup"><span data-stu-id="05c59-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="05c59-631">Gebruik de volgende parameters met het inschakelen van versleuteling op een nieuwe virtuele machine van de versleutelde VHD, de `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="05c59-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="05c59-632">De coderingsstatus van een versleutelde IaaS VM ophalen</span><span class="sxs-lookup"><span data-stu-id="05c59-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="05c59-633">U kunt de coderingsstatus ophalen met behulp van Azure Resource Manager [PowerShell-cmdlets](/powershell/azure/overview), of de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="05c59-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="05c59-634">De volgende secties wordt uitgelegd hoe de klassieke Azure-portal en de CLI-opdrachten gebruiken voor de coderingsstatus.</span><span class="sxs-lookup"><span data-stu-id="05c59-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="05c59-635">De coderingsstatus van een versleutelde Windows VM ophalen met behulp van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05c59-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="05c59-636">U kunt de coderingsstatus van IaaS VM van Azure Resource Manager krijgen als volgt:</span><span class="sxs-lookup"><span data-stu-id="05c59-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="05c59-637">Aanmelden bij de [klassieke Azure-portal](https://portal.azure.com/), en klik vervolgens op **virtuele machines** in het linkerdeelvenster om te zien van een samenvatting weergegeven van de virtuele machines in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="05c59-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="05c59-638">U kunt de virtuele machines weergave filteren door de naam van het abonnement in de **abonnement** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="05c59-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="05c59-639">Aan de bovenkant van de **virtuele machines** pagina, klikt u op **kolommen**.</span><span class="sxs-lookup"><span data-stu-id="05c59-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="05c59-640">Op de **Kies kolom** blade Selecteer **schijfversleuteling**, en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="05c59-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="05c59-641">U ziet de schijfversleuteling kolom met de coderingsstatus _ingeschakeld_ of _niet ingeschakeld_ voor elke virtuele machine, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="05c59-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="05c59-643">De coderingsstatus van een versleutelde (Windows of Linux) IaaS VM ophalen met behulp van de PowerShell-cmdlet schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="05c59-644">U kunt de coderingsstatus van IaaS VM ophalen uit de PowerShell-cmdlet schijfversleuteling `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="05c59-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="05c59-645">Als u de instellingen voor codering voor uw virtuele machine, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="05c59-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="05c59-646">U kunt de uitvoer van inspecteren _Get-AzureRmVMDiskEncryptionStatus_ sleutel URL's voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="05c59-647">De instellingen OSVolumeEncrypted en DataVolumesEncrypted waarden zijn ingesteld op _versleutelde_, waarmee u aangeeft dat beide volumes zijn versleuteld met behulp van Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="05c59-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="05c59-648">Zie voor informatie over het inschakelen van versleuteling met Azure Disk Encryption met behulp van PowerShell-cmdlets, de blogberichten [Azure Disk Encryption verkennen met Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) en [Azure Disk Encryption verkennen Deel 2 met Azure PowerShell -](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c59-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-649">Op Linux virtuele machines, het drie tot vier minuten duurt voordat de `Get-AzureRmVMDiskEncryptionStatus` cmdlet om de versleutelingsstatus te rapporteren.</span><span class="sxs-lookup"><span data-stu-id="05c59-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="05c59-650">De coderingsstatus van IaaS VM ophalen uit de CLI schijfversleuteling opdracht</span><span class="sxs-lookup"><span data-stu-id="05c59-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="05c59-651">U kunt de coderingsstatus van IaaS VM ophalen door met de opdracht van de CLI-schijfversleuteling `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="05c59-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="05c59-652">Als u de instellingen voor codering voor uw virtuele machine, Voer uw Azure CLI-sessie:</span><span class="sxs-lookup"><span data-stu-id="05c59-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="05c59-653">Schakel versleuteling voor het uitvoeren van Windows IaaS VM</span><span class="sxs-lookup"><span data-stu-id="05c59-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="05c59-654">U kunt versleuteling op een actieve Windows of Linux IaaS VM via de Azure Disk Encryption Resource Manager-sjabloon of het PowerShell-cmdlets uitschakelen en de configuratie ontsleuteling opgeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="05c59-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="05c59-655">Windows VM</span></span>
<span data-ttu-id="05c59-656">Versleuteling van het besturingssysteem, het gegevensvolume of beide op het actieve Windows IaaS VM Hiermee schakelt u de stap uitschakelen-codering.</span><span class="sxs-lookup"><span data-stu-id="05c59-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="05c59-657">U kan het besturingssysteemvolume uitschakelen en laat het gegevensvolume dat is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="05c59-658">Wanneer de stap uitschakelen-versleuteling wordt uitgevoerd, het klassieke implementatiemodel Azure werkt het VM-servicemodel en de Windows IaaS VM ontsleutelde is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="05c59-659">De inhoud van de virtuele machine worden niet langer in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="05c59-660">De ontsleuteling verwijdert niet de sleutelkluis en de versleuteling sleutelmateriaal (versleutelingssleutels BitLocker voor Windows en de wachtwoordzin voor Linux).</span><span class="sxs-lookup"><span data-stu-id="05c59-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="05c59-661">Virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="05c59-661">Linux VM</span></span>
<span data-ttu-id="05c59-662">Versleuteling van het gegevensvolume van de op de actieve virtuele machine IaaS Linux Hiermee schakelt u de stap uitschakelen-codering.</span><span class="sxs-lookup"><span data-stu-id="05c59-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="05c59-663">Deze stap werkt alleen als de besturingssysteemschijf is niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-664">Uitschakelen van versleuteling op de schijf met het besturingssysteem is niet toegestaan op de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="05c59-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="05c59-665">Schakel versleuteling in op een bestaande of actief IaaS VM</span><span class="sxs-lookup"><span data-stu-id="05c59-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="05c59-666">U kunt uitschakelen schijfversleuteling op IaaS VM's van Windows worden uitgevoerd met behulp van de [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="05c59-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="05c59-667">Klik op de Azure snel starten-sjabloon **implementeren in Azure**, voer de configuratie van de ontsleuteling op de **Parameters** blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c59-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="05c59-668">Selecteer het abonnement, resourcegroep locatie voor resourcegroep, juridische voorwaarden en overeenkomst en klik vervolgens op **maken** versleuteling op een nieuwe IaaS VM in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="05c59-669">Virtuele Linux-machines, kunt u versleuteling uitschakelen met behulp van de [uitschakelen van versleuteling op een actieve Linux VM](https://aka.ms/decrypt-linuxvm) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="05c59-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="05c59-670">De volgende tabel bevat de parameters van de Resource Manager-sjabloon voor het uitschakelen van versleuteling op een actieve IaaS VM:</span><span class="sxs-lookup"><span data-stu-id="05c59-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="05c59-671">Parameter</span><span class="sxs-lookup"><span data-stu-id="05c59-671">Parameter</span></span> | <span data-ttu-id="05c59-672">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05c59-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c59-673">vmName</span><span class="sxs-lookup"><span data-stu-id="05c59-673">vmName</span></span> | <span data-ttu-id="05c59-674">Naam van de virtuele machine die de versleutelingsbewerking op worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="05c59-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="05c59-675">volumeType</span></span> | <span data-ttu-id="05c59-676">Het type van het volume dat een ontsleutelingsbewerking wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="05c59-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="05c59-677">Geldige waarden zijn _OS_, _gegevens_, en _alle_.</span><span class="sxs-lookup"><span data-stu-id="05c59-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="05c59-678">U kunt versleuteling voor het uitvoeren van Windows IaaS VM OS/opstartvolume zonder versleuteling wordt uitgeschakeld op het niet uitschakelen de _gegevens_ volume.</span><span class="sxs-lookup"><span data-stu-id="05c59-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="05c59-679">Houd er ook rekening mee dat uitschakelen versleuteling op de schijf met het besturingssysteem is niet toegestaan voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="05c59-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="05c59-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="05c59-680">sequenceVersion</span></span> | <span data-ttu-id="05c59-681">De versie van de volgorde van de BitLocker-bewerking.</span><span class="sxs-lookup"><span data-stu-id="05c59-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="05c59-682">Dit versienummer verhoogd telkens wanneer een ontsleutelingsbewerking schijf op dezelfde virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="05c59-683">Schakel versleuteling in op een bestaande of actief IaaS VM</span><span class="sxs-lookup"><span data-stu-id="05c59-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="05c59-684">Zie voor informatie over het uitschakelen van versleuteling op een bestaande of actief IaaS-VM met behulp van de PowerShell-cmdlet [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="05c59-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="05c59-685">Deze cmdlet biedt ondersteuning voor Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="05c59-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="05c59-686">Schakel codering wordt een extensie geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="05c59-687">Als de _naam_ parameter niet is opgegeven, een uitbreiding met de standaardnaam _AzureDiskEncryption voor VM's van Windows_ wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05c59-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="05c59-688">Op Linux virtuele machines, wordt de AzureDiskEncryptionForLinux-uitbreiding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05c59-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="05c59-689">Deze cmdlet opnieuw opgestart voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="05c59-690">Schakel versleuteling in op vooraf zijn versleuteld IaaS VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="05c59-691">De Azure beheerd schijf ARM-sjabloon gebruiken om te maken van een versleutelde virtuele machine van een vooraf zijn versleuteld VHD met de ARM-sjabloon te vinden op</span><span class="sxs-lookup"><span data-stu-id="05c59-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="05c59-692">[Een nieuwe beheerde versleutelde schijf van een vooraf zijn versleuteld VHD/storage-blob maken] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="05c59-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="05c59-693">Schakel versleuteling in op een nieuwe Linux IaaS-VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="05c59-694">Met de Azure beheerd schijf ARM-sjabloon kunt u een nieuwe versleutelde Linux IaaS virtuele machine maken met de ARM-sjabloon te vinden op</span><span class="sxs-lookup"><span data-stu-id="05c59-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="05c59-695">[Implementatie RHEL 7.2 met volledige schijfversleuteling] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="05c59-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="05c59-696">Schakel versleuteling in op een nieuwe Windows IaaS-VM met beheerde Azure-schijf</span><span class="sxs-lookup"><span data-stu-id="05c59-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="05c59-697">Met de Azure beheerd schijf ARM-sjabloon kunt u een nieuwe versleutelde Linux IaaS virtuele machine maken met de ARM-sjabloon te vinden op</span><span class="sxs-lookup"><span data-stu-id="05c59-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="05c59-698">[Een nieuwe versleutelde Windows IaaS beheerd schijf virtuele machine maken van de afbeelding] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="05c59-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="05c59-699">Dit is verplicht op momentopname en/of back-up een beheerde schijven op basis van VM-instantie buiten en voordat u Azure Disk Encryption inschakelt.</span><span class="sxs-lookup"><span data-stu-id="05c59-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="05c59-700">Een momentopname van de beheerde schijf kan worden uitgevoerd vanuit de portal of Azure Backup kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05c59-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="05c59-701">Back-ups zorgen ervoor dat een hersteloptie mogelijk in het geval van een onverwachte fout opgetreden tijdens het versleutelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="05c59-702">Als u een back-up is gemaakt, kan de cmdlet Set-AzureRmVMDiskEncryptionExtension worden gebruikt voor het versleutelen van beheerde schijven door de parameter - skipVmBackup te geven.</span><span class="sxs-lookup"><span data-stu-id="05c59-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="05c59-703">Met deze opdracht uitvoeren tegen beheerde schijven op basis van de virtuele machine totdat een back-up is gemaakt en deze parameter is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="05c59-704">Versleutelingsinstellingen van een bestaande versleutelde niet premium virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="05c59-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="05c59-705">Gebruik de bestaande interfaces van de schijf van Azure-codering wordt ondersteund voor het uitvoeren van de virtuele machine [PS-cmdlets, CLI of ARM-sjablonen] de versleutelingsinstellingen bijwerken zoals AAD client-ID/geheime sleutel versleutelingssleutel [KEK] versleutelingssleutel BitLocker voor Windows-VM of de wachtwoordzin voor Linux-VM enz. De versleutelingsinstelling voor de update wordt alleen ondersteund voor virtuele machines die worden ondersteund door niet-premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="05c59-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="05c59-706">Het is NNOT ondersteund voor virtuele machines die worden ondersteund door de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="05c59-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="05c59-707">Bijlage</span><span class="sxs-lookup"><span data-stu-id="05c59-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="05c59-708">Verbinding maken met uw abonnement</span><span class="sxs-lookup"><span data-stu-id="05c59-708">Connect to your subscription</span></span>
<span data-ttu-id="05c59-709">Lees voordat u doorgaat, de *vereisten* sectie in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="05c59-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="05c59-710">Nadat u ervoor te zorgen dat aan alle vereisten is voldaan, kunt u verbinding met uw abonnement als volgt:</span><span class="sxs-lookup"><span data-stu-id="05c59-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="05c59-711">Start een Azure PowerShell-sessie en meld u aan bij uw Azure-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="05c59-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="05c59-712">Als u meerdere abonnementen hebt en opgeven dat een wilt om te gebruiken, typt u het volgende als u wilt zien van de abonnementen voor uw account:</span><span class="sxs-lookup"><span data-stu-id="05c59-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="05c59-713">Als u het abonnement dat u wilt gebruiken, typt u:</span><span class="sxs-lookup"><span data-stu-id="05c59-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="05c59-714">Om te controleren of het abonnement geconfigureerd juist is, typt u:</span><span class="sxs-lookup"><span data-stu-id="05c59-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="05c59-715">Om te bevestigen op dat de Azure Disk Encryption-cmdlets zijn geïnstalleerd, typt u:</span><span class="sxs-lookup"><span data-stu-id="05c59-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="05c59-716">De volgende voorbeelduitvoer bevestigt dat de installatie van Azure schijf versleuteling PowerShell:</span><span class="sxs-lookup"><span data-stu-id="05c59-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="05c59-717">Een vooraf zijn versleuteld Windows VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="05c59-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="05c59-718">De volgende secties zijn nodig voor het voorbereiden van een vooraf zijn versleuteld Windows VHD voor de implementatie als een gecodeerde VHD in Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="05c59-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="05c59-719">Gebruik de informatie voor het voorbereiden en een nieuwe Windows VM (VHD) op de Azure Site Recovery of Azure worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="05c59-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="05c59-720">Bijwerken van Groepsbeleid om toe te staan zonder TPM voor OS-beveiliging</span><span class="sxs-lookup"><span data-stu-id="05c59-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="05c59-721">De groepsbeleidsinstellingen voor BitLocker-instelling **BitLocker-stationsversleuteling**, die u vindt hier onder **lokaal computerbeleid** > **Computerconfiguratie**  >  **Beheersjablonen** > **Windows-onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="05c59-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="05c59-722">Deze instelling te wijzigen **besturingssysteem stations** > **aanvullende verificatie bij opstarten vereisen** > **BitLocker zonder een compatibele TPMtoestaan**, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="05c59-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="05c59-724">BitLocker-onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="05c59-724">Install BitLocker feature components</span></span>
<span data-ttu-id="05c59-725">Voor Windows Server 2012 en hoger, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="05c59-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="05c59-726">Gebruik de volgende opdracht voor Windows Server 2008 R2:</span><span class="sxs-lookup"><span data-stu-id="05c59-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="05c59-727">Het volume met het besturingssysteem voorbereiden voor BitLocker met behulp van`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="05c59-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="05c59-728">Voor het comprimeren van de partitie van het besturingssysteem en de machine voorbereiden voor BitLocker, voert u de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="05c59-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="05c59-729">Het besturingssysteemvolume beveiligen met behulp van BitLocker</span><span class="sxs-lookup"><span data-stu-id="05c59-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="05c59-730">Gebruik de [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) opdracht versleuteling op het opstartvolume met behulp van een externe sleutelbeveiliging in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="05c59-731">Ook de externe sleutel (.bek-bestand) op de externe schijf of volume plaatsen.</span><span class="sxs-lookup"><span data-stu-id="05c59-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="05c59-732">Versleuteling is ingeschakeld op het systeem/opstartvolume na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="05c59-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="05c59-733">De virtuele machine met een afzonderlijke gegevens/resource VHD voorbereiden voor het ophalen van de externe sleutel met BitLocker.</span><span class="sxs-lookup"><span data-stu-id="05c59-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="05c59-734">Versleutelen van een OS-station op een actieve Linux VM</span><span class="sxs-lookup"><span data-stu-id="05c59-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="05c59-735">Versleuteling van een OS-station op een actieve Linux VM wordt ondersteund door de volgende distributies:</span><span class="sxs-lookup"><span data-stu-id="05c59-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="05c59-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="05c59-736">RHEL 7.2</span></span>
* <span data-ttu-id="05c59-737">7.2 centOS</span><span class="sxs-lookup"><span data-stu-id="05c59-737">CentOS 7.2</span></span>
* <span data-ttu-id="05c59-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="05c59-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="05c59-739">Vereisten voor de OS-schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="05c59-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="05c59-740">De virtuele machine moet worden gemaakt vanuit de Marketplace-installatiekopie in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05c59-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="05c59-741">Azure virtuele machine met ten minste 4 GB aan RAM-geheugen (aanbevolen grootte is 7 GB).</span><span class="sxs-lookup"><span data-stu-id="05c59-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="05c59-742">(Voor RHEL en CentOS) SELinux uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="05c59-743">Zie '4.4.2 SELinux uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="05c59-744">Uitschakelen van SELinux' in de [SELinux van de gebruiker en de Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="05c59-745">Nadat u SELinux uitgeschakeld, start u de virtuele machine ten minste één keer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="05c59-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="05c59-746">Stappen</span><span class="sxs-lookup"><span data-stu-id="05c59-746">Steps</span></span>
1. <span data-ttu-id="05c59-747">Een virtuele machine maken met behulp van een van de verdelingen eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="05c59-748">Voor CentOS 7.2, OS schijfversleuteling ondersteund via een speciale installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="05c59-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="05c59-749">Geef voor het gebruik van deze installatiekopie '7.2n' als de SKU bij het maken van de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="05c59-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="05c59-750">De virtuele machine naar wens configureren.</span><span class="sxs-lookup"><span data-stu-id="05c59-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="05c59-751">Als u schijven voor het versleutelen van alle de (OS + gegevens), de gegevensstations moeten worden opgegeven en koppelbaar van /etc/fstab gaat.</span><span class="sxs-lookup"><span data-stu-id="05c59-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="05c59-752">Gebruik UUID =... om op te geven gegevensstations in/etc/fstab in plaats van de naam van het blok apparaat (bijvoorbeeld/dev/sdb1) opgeven.</span><span class="sxs-lookup"><span data-stu-id="05c59-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="05c59-753">Tijdens het versleutelen wijzigt de volgorde van de stations op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="05c59-754">Als uw virtuele machine afhankelijk van een specifieke volgorde van apparaten is, mislukt het koppel deze na versleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="05c59-755">Meld u af bij de SSH-sessies.</span><span class="sxs-lookup"><span data-stu-id="05c59-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="05c59-756">Geef voor het versleutelen van het besturingssysteem volumeType als **alle** of **OS** wanneer u [versleuteling inschakelen](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="05c59-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="05c59-757">Alle gebruikersruimte innemen processen die niet worden uitgevoerd als `systemd` services moeten worden afgesloten met een `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="05c59-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="05c59-758">Start opnieuw op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-758">Reboot the VM.</span></span> <span data-ttu-id="05c59-759">Wanneer u OS schijfversleuteling op een actieve virtuele machine inschakelt, plan op VM uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="05c59-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="05c59-760">Controleer regelmatig de voortgang van versleuteling met behulp van de instructies in de [volgende sectie](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="05c59-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="05c59-761">Nadat Get AzureRmVmDiskEncryptionStatus toont 'VMRestartPending', start u uw virtuele machine opnieuw aanmelden bij deze of via de portal, PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="05c59-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="05c59-762">Voordat u opnieuw opstart, wordt aangeraden dat u opslaat [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="05c59-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="05c59-763">OS-versleuteling voortgang controleren</span><span class="sxs-lookup"><span data-stu-id="05c59-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="05c59-764">U kunt voortgang OS versleuteling op drie manieren:</span><span class="sxs-lookup"><span data-stu-id="05c59-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="05c59-765">Gebruik de `Get-AzureRmVmDiskEncryptionStatus` cmdlet en controleer het veld ProgressMessage:</span><span class="sxs-lookup"><span data-stu-id="05c59-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="05c59-766">Nadat de virtuele machine bereikt 'OS schijfversleuteling gestart', duurt het ongeveer 40 tot 50 minuten back VM op een Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="05c59-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="05c59-767">Omdat [uitgeven #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` en `DataVolumesEncrypted` worden weergegeven als `Unknown` in een aantal distributies.</span><span class="sxs-lookup"><span data-stu-id="05c59-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="05c59-768">Met de versie 2.1.5 WALinuxAgent en later kunt dit probleem automatisch opgelost.</span><span class="sxs-lookup"><span data-stu-id="05c59-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="05c59-769">Als u ziet `Unknown` u kunt in de uitvoer schijfversleuteling status controleren met behulp van de Azure Resourceverkenner.</span><span class="sxs-lookup"><span data-stu-id="05c59-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="05c59-770">Ga naar [Azure Resource Explorer](https://resources.azure.com/), en vouw vervolgens deze hiërarchie in het deelvenster selectie op links:</span><span class="sxs-lookup"><span data-stu-id="05c59-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

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

 <span data-ttu-id="05c59-771">Ga in de InstanceView voor de versleutelingsstatus van uw schijven.</span><span class="sxs-lookup"><span data-stu-id="05c59-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![Instantieweergave van virtuele machine](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="05c59-773">Bekijk [opstarten diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="05c59-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="05c59-774">Berichten van de extensie ADE moeten worden voorafgegaan door `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="05c59-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="05c59-775">Aanmelden bij de virtuele machine via SSH en ophalen van het logboek voor uitbreiding van:</span><span class="sxs-lookup"><span data-stu-id="05c59-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="05c59-776">/var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="05c59-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="05c59-777">Het is raadzaam dat u niet met de virtuele machine aanmelden zich terwijl OS-versleuteling uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="05c59-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="05c59-778">Kopieer de logboeken alleen wanneer de twee methoden zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="05c59-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="05c59-779">Een vooraf zijn versleuteld Linux VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="05c59-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="05c59-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="05c59-780">Ubuntu 16</span></span>
<span data-ttu-id="05c59-781">Configureren van versleuteling tijdens de installatie van het distributiepunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="05c59-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="05c59-782">Selecteer **configureren van versleutelde volumes** wanneer u de schijven partitioneren.</span><span class="sxs-lookup"><span data-stu-id="05c59-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="05c59-784">Maak een afzonderlijke opstartstation, moet niet worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="05c59-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="05c59-785">Codeer uw basisstation.</span><span class="sxs-lookup"><span data-stu-id="05c59-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="05c59-787">Geef een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="05c59-787">Provide a passphrase.</span></span> <span data-ttu-id="05c59-788">Dit is de wachtwoordzin op die u naar de sleutelkluis uploadt.</span><span class="sxs-lookup"><span data-stu-id="05c59-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="05c59-790">Voltooi partitioneren.</span><span class="sxs-lookup"><span data-stu-id="05c59-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="05c59-792">Wanneer u de virtuele machine worden opgestart en wordt gevraagd een wachtwoordzin, gebruikt u de wachtwoordzin die u hebt opgegeven in stap 3.</span><span class="sxs-lookup"><span data-stu-id="05c59-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="05c59-794">De virtuele machine voorbereiden voor het uploaden naar Azure met behulp [deze instructies](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="05c59-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="05c59-795">Voer niet de laatste stap (de virtuele machine opheffen van inrichting) nog.</span><span class="sxs-lookup"><span data-stu-id="05c59-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="05c59-796">Codering met Azure werkt als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="05c59-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="05c59-797">Maak een bestand onder /usr/local/sbin/azure_crypt_key.sh, met de inhoud in het volgende script.</span><span class="sxs-lookup"><span data-stu-id="05c59-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="05c59-798">Let op de KeyFileName omdat deze de naam van het wachtwoordzin die wordt gebruikt door Azure.</span><span class="sxs-lookup"><span data-stu-id="05c59-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="05c59-799">Wijzig de configuratie crypt in */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="05c59-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="05c59-800">Dit ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="05c59-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="05c59-801">Als u wilt bewerken *azure_crypt_key.sh* in Windows en u gekopieerd naar Linux, voer `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="05c59-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="05c59-802">Uitvoerbare machtigingen toevoegen aan het script:</span><span class="sxs-lookup"><span data-stu-id="05c59-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="05c59-803">Bewerken */etc/initramfs-tools/modules* door regels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="05c59-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="05c59-804">Uitvoeren `update-initramfs -u -k all` bijwerken van de initramfs waarmee de `keyscript` te laten treden.</span><span class="sxs-lookup"><span data-stu-id="05c59-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="05c59-805">Nu u de virtuele machine kunt inrichting ervan ongedaan.</span><span class="sxs-lookup"><span data-stu-id="05c59-805">Now you can deprovision the VM.</span></span>

 ![Ubuntu 16.04 Setup](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="05c59-807">Doorgaan naar volgende stap en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="05c59-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="05c59-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="05c59-808">openSUSE 13.2</span></span>
<span data-ttu-id="05c59-809">Voor het configureren van versleuteling tijdens de installatie van het distributiepunt, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="05c59-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="05c59-810">Wanneer u de schijven partitioneren, selecteert u **versleutelen Volume groep**, en voer vervolgens een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="05c59-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="05c59-811">Dit is het wachtwoord dat u naar de sleutelkluis uploaden zult.</span><span class="sxs-lookup"><span data-stu-id="05c59-811">This is the password that you will upload to your key vault.</span></span>

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="05c59-813">Start de virtuele machine met het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="05c59-813">Boot the VM using your password.</span></span>

 ![openSUSE 13.2 instellen](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="05c59-815">De virtuele machine voorbereiden voor het uploaden naar Azure door de instructies in [een SLES of openSUSE virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="05c59-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="05c59-816">Voer niet de laatste stap (de virtuele machine opheffen van inrichting) nog.</span><span class="sxs-lookup"><span data-stu-id="05c59-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="05c59-817">Versleuteling werkt met Azure, kunt u het volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="05c59-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="05c59-818">Bewerk de /etc/dracut.conf, en voeg de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="05c59-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="05c59-819">Deze regels uitcommentariëren aan het einde van het bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="05c59-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="05c59-820">De volgende regel aan het begin van het bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:</span><span class="sxs-lookup"><span data-stu-id="05c59-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="05c59-821">En wijzig alle instanties van:</span><span class="sxs-lookup"><span data-stu-id="05c59-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="05c59-822">in:</span><span class="sxs-lookup"><span data-stu-id="05c59-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="05c59-823">Bewerk /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh en voegt deze toe aan '# Open LUKS apparaat':</span><span class="sxs-lookup"><span data-stu-id="05c59-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
5. <span data-ttu-id="05c59-824">Voer `/usr/sbin/dracut -f -v` de initrd bijwerken.</span><span class="sxs-lookup"><span data-stu-id="05c59-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="05c59-825">Nu u kunt inrichting ervan ongedaan maakt de virtuele machine en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="05c59-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="05c59-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="05c59-826">CentOS 7</span></span>
<span data-ttu-id="05c59-827">Voor het configureren van versleuteling tijdens de installatie van het distributiepunt, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="05c59-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="05c59-828">Selecteer **mijn gegevens versleutelen** wanneer u schijven partitioneren.</span><span class="sxs-lookup"><span data-stu-id="05c59-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="05c59-830">Zorg ervoor dat **versleutelen** is geselecteerd voor de basispartitie.</span><span class="sxs-lookup"><span data-stu-id="05c59-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="05c59-832">Geef een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="05c59-832">Provide a passphrase.</span></span> <span data-ttu-id="05c59-833">Dit is de wachtwoordzin op die u naar de sleutelkluis uploaden zult.</span><span class="sxs-lookup"><span data-stu-id="05c59-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="05c59-835">Wanneer u de virtuele machine worden opgestart en wordt gevraagd een wachtwoordzin, gebruikt u de wachtwoordzin die u hebt opgegeven in stap 3.</span><span class="sxs-lookup"><span data-stu-id="05c59-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="05c59-837">De virtuele machine voorbereiden voor het uploaden naar Azure met behulp van de 'CentOS 7.0 +'-instructies in [een CentOS-virtuele machine voorbereiden voor Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="05c59-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="05c59-838">Voer niet de laatste stap (de virtuele machine opheffen van inrichting) nog.</span><span class="sxs-lookup"><span data-stu-id="05c59-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="05c59-839">Nu u kunt inrichting ervan ongedaan maakt de virtuele machine en [uw VHD uploaden](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.</span><span class="sxs-lookup"><span data-stu-id="05c59-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="05c59-840">Versleuteling werkt met Azure, kunt u het volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="05c59-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="05c59-841">Bewerk de /etc/dracut.conf, en voeg de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="05c59-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="05c59-842">Deze regels uitcommentariëren aan het einde van het bestand /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="05c59-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="05c59-843">De volgende regel aan het begin van het bestand /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh toevoegen:</span><span class="sxs-lookup"><span data-stu-id="05c59-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="05c59-844">En wijzig alle instanties van:</span><span class="sxs-lookup"><span data-stu-id="05c59-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="05c59-845">tot</span><span class="sxs-lookup"><span data-stu-id="05c59-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="05c59-846">Bewerk /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh en dit toevoegen na de '# Open LUKS apparaat':</span><span class="sxs-lookup"><span data-stu-id="05c59-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
5. <span data-ttu-id="05c59-847">Voer de ' / usr/sbin/dracut - f - v ' de initrd bijwerken.</span><span class="sxs-lookup"><span data-stu-id="05c59-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![CentOS 7 Setup](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="05c59-849">Versleutelde harde schijf geüpload naar Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="05c59-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="05c59-850">Nadat BitLocker-versleuteling of DM-Crypt versleuteling is ingeschakeld, moet de lokale versleutelde VHD te uploaden naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="05c59-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="05c59-851">Uploaden van het geheim schijf-codering voor vooraf zijn versleuteld VM aan de sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="05c59-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="05c59-852">Het geheim voor schijf-codering die u hebt verkregen moet eerder worden geüpload als een geheim in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="05c59-853">De sleutelkluis moet beschikken over machtigingen die zijn ingeschakeld voor uw Azure AD-client en schijfversleuteling.</span><span class="sxs-lookup"><span data-stu-id="05c59-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="05c59-854">Schijf versleuteling geheim niet versleuteld met een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="05c59-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="05c59-855">Als u het geheim in de sleutelkluis instelt, gebruik [Set AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="05c59-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="05c59-856">Als u een virtuele Windows-computer hebt, het bek-bestand is gecodeerd als een base64-tekenreeks en vervolgens geüpload naar uw sleutelkluis met de `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05c59-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="05c59-857">De wachtwoordzin is voor Linux, gecodeerd als een base64-tekenreeks en vervolgens geüpload naar de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="05c59-858">Bovendien moet u ervoor dat de volgende codes zijn ingesteld bij het maken van het geheim in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="05c59-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="05c59-859">Gebruik de `$secretUrl` in de volgende stap voor [de OS-schijf koppelen zonder KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="05c59-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="05c59-860">Schijf versleuteling geheim is versleuteld met een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="05c59-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="05c59-861">Voordat u het geheim naar de sleutelkluis uploaden, kunt u deze desgewenst met een sleutel versleutelingssleutel coderen.</span><span class="sxs-lookup"><span data-stu-id="05c59-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="05c59-862">Gebruik de omloop [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) eerst het geheim met behulp van de versleutelingssleutel van de sleutel te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="05c59-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="05c59-863">De uitvoer van deze bewerking tekstterugloop is base64 gecodeerde URL string die u vervolgens uploaden als een geheim met behulp van kunt de [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05c59-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
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

<span data-ttu-id="05c59-864">Gebruik `$KeyEncryptionKey` en `$secretUrl` in de volgende stap voor [de OS-schijf met behulp van de KEK koppelen](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="05c59-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="05c59-865">Geef een geheime URL wanneer u een besturingssysteemschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="05c59-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="05c59-866">Zonder een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="05c59-866">Without using a KEK</span></span>
<span data-ttu-id="05c59-867">Terwijl u de schijf met het besturingssysteem toevoegen wilt, moet u doorgeven `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="05c59-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="05c59-868">De URL is in de sectie 'schijfversleuteling geheim niet versleuteld met een KEK' gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="05c59-869">Met behulp van een KEK-sleutel</span><span class="sxs-lookup"><span data-stu-id="05c59-869">Using a KEK</span></span>
<span data-ttu-id="05c59-870">Wanneer u de OS-schijf koppelen, `$KeyEncryptionKey` en `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="05c59-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="05c59-871">De URL is in de sectie 'schijfversleuteling geheim niet versleuteld met een KEK' gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="05c59-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="05c59-872">Download deze handleiding</span><span class="sxs-lookup"><span data-stu-id="05c59-872">Download this guide</span></span>
<span data-ttu-id="05c59-873">U kunt deze handleiding uit downloaden de [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="05c59-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="05c59-874">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="05c59-874">For more information</span></span>
[<span data-ttu-id="05c59-875">Verken Azure Disk Encryption met Azure PowerShell - deel 1</span><span class="sxs-lookup"><span data-stu-id="05c59-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="05c59-876">Azure Disk Encryption met Azure PowerShell - deel 2 verkennen</span><span class="sxs-lookup"><span data-stu-id="05c59-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
