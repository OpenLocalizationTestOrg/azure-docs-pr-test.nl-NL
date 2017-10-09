---
title: Statusconfiguratie voor een overzicht van Azure aaaDesired | Microsoft Docs
description: Overzicht voor het gebruik van Hallo Microsoft Azure-extensie-handler voor PowerShell Desired State Configuration. Vereisten, architectuur, cmdlets zoals..
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="71a7d-104">Inleiding toohello Azure Desired State Configuration-extensie-handler</span><span class="sxs-lookup"><span data-stu-id="71a7d-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="71a7d-105">Hello Azure VM-Agent en de bijbehorende extensies uitmaken deel van Hallo Microsoft Azure Infrastructure Services.</span><span class="sxs-lookup"><span data-stu-id="71a7d-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="71a7d-106">VM-extensies zijn softwareonderdelen die Hallo VM-functionaliteit uitbreiden en verschillende bewerkingen VM vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="71a7d-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="71a7d-107">Bijvoorbeeld, Hallo VMAccess-extensie worden gebruikte tooreset een beheerderswachtwoord of aangepast Script Hallo extensie gebruikte tooexecute een script op Hallo VM kan worden.</span><span class="sxs-lookup"><span data-stu-id="71a7d-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="71a7d-108">Dit artikel bevat Hallo PowerShell Desired State Configuration (DSC)-extensie voor Azure Virtual machines als onderdeel van hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="71a7d-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="71a7d-109">U kunt nieuwe cmdlets tooupload gebruiken en een PowerShell DSC-configuratie toepassen op een Azure-VM met Hallo PowerShell DSC-extensie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="71a7d-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="71a7d-110">Hallo PowerShell DSC-uitbreiding aanroepen in PowerShell DSC tooenact Hallo ontvangen DSC-configuratie op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="71a7d-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="71a7d-111">Deze functionaliteit is ook beschikbaar via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="71a7d-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71a7d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="71a7d-112">Prerequisites</span></span>
<span data-ttu-id="71a7d-113">**Lokale machine** toointeract met Hallo Azure VM-extensie, of u kunt toouse beide hello Azure-portal hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="71a7d-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="71a7d-114">**Gastagent** hello Azure VM die is geconfigureerd door Hallo DSC-configuratie moet toobe een besturingssysteem dat ondersteuning biedt voor Windows Management Framework (WMF) 4.0 ofwel 5.0.</span><span class="sxs-lookup"><span data-stu-id="71a7d-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="71a7d-115">Hallo volledige lijst met ondersteunde versies van het besturingssysteem kan worden gevonden op Hallo [versiegeschiedenis van DSC-uitbreiding](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="71a7d-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="71a7d-116">Termen en begrippen</span><span class="sxs-lookup"><span data-stu-id="71a7d-116">Terms and concepts</span></span>
<span data-ttu-id="71a7d-117">Deze handleiding wordt ervan uitgegaan bekend bent met de volgende concepten Hallo:</span><span class="sxs-lookup"><span data-stu-id="71a7d-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="71a7d-118">Configuratie: een document DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="71a7d-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="71a7d-119">Knooppunt - doel voor een DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="71a7d-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="71a7d-120">In dit document verwijst 'knooppunt' altijd tooan Azure VM.</span><span class="sxs-lookup"><span data-stu-id="71a7d-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="71a7d-121">Configuratie - een .psd1 gegevensbestand met milieu gegevens voor een configuratie</span><span class="sxs-lookup"><span data-stu-id="71a7d-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="71a7d-122">Overzicht van architectuur</span><span class="sxs-lookup"><span data-stu-id="71a7d-122">Architectural overview</span></span>
<span data-ttu-id="71a7d-123">Hello Azure DSC-uitbreiding gebruikt hello Azure VM-Agent framework toodeliver, nemen en een rapport over DSC-configuraties die zijn uitgevoerd op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="71a7d-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="71a7d-124">Hallo DSC-extensie verwacht een ZIP-bestand met ten minste een configuratie-document en een aantal parameters opgegeven via Hallo-SDK van Azure PowerShell of via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="71a7d-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="71a7d-125">Als het Hallo-extensie is aangeroepen voor Hallo eerst, voert deze een installatieproces.</span><span class="sxs-lookup"><span data-stu-id="71a7d-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="71a7d-126">Dit proces wordt een versie van Windows Management Framework (WMF) Hallo Hallo logica te volgen met geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="71a7d-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="71a7d-127">Als hello Azure VM besturingssysteem Windows Server 2016 is, wordt geen actie ondernomen.</span><span class="sxs-lookup"><span data-stu-id="71a7d-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="71a7d-128">Windows Server 2016 heeft al Hallo meest recente versie van PowerShell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="71a7d-129">Als hello `wmfVersion` eigenschap is opgegeven, die versie van Hallo WMF is geïnstalleerd, tenzij deze is niet compatibel met OS Hallo van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="71a7d-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="71a7d-130">Als er geen `wmfVersion` eigenschap is opgegeven, Hallo meest toepasselijke versie Hallo WMF is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="71a7d-131">Installatie van Hallo WMF moet opnieuw worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="71a7d-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="71a7d-132">Na opnieuw opstarten, Hallo uitbreiding downloadt Hallo ZIP-bestand is opgegeven in Hallo `modulesUrl` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="71a7d-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="71a7d-133">Als deze locatie zich in Azure blob-opslag, een SAS-token kan worden opgegeven in Hallo `sasToken` eigenschap tooaccess Hallo bestand.</span><span class="sxs-lookup"><span data-stu-id="71a7d-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="71a7d-134">Nadat Hallo .zip is gedownload en uitgepakt, de functie van de configuratie is gedefinieerd in Hallo `configurationFunction` toogenerate Hallo MOF-bestand wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="71a7d-135">Hallo-extensie voert `Start-DscConfiguration -Force` op Hallo gegenereerd MOF-bestand.</span><span class="sxs-lookup"><span data-stu-id="71a7d-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="71a7d-136">Hallo-extensie uitvoer vastgelegd en schrijft deze weer uit toohello Azure Status kanaal.</span><span class="sxs-lookup"><span data-stu-id="71a7d-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="71a7d-137">Vanaf dit punt op Hallo verwerkt DSC LCM bewaking en correctie als normaal.</span><span class="sxs-lookup"><span data-stu-id="71a7d-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="71a7d-138">PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="71a7d-138">PowerShell cmdlets</span></span>
<span data-ttu-id="71a7d-139">PowerShell-cmdlets kunnen worden gebruikt met Azure Resource Manager of Hallo-classic deployment model toopackage, publiceren en DSC-extensie-implementaties controleren.</span><span class="sxs-lookup"><span data-stu-id="71a7d-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="71a7d-140">Hallo volgende cmdlets die vermeld zijn Hallo-modules voor klassieke implementatie, maar 'Azure' kan worden vervangen door "AzureRm" toouse hello Azure Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="71a7d-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="71a7d-141">Bijvoorbeeld: `Publish-AzureVMDscConfiguration` gebruikt Hallo klassieke implementatiemodel, waarbij `Publish-AzureRmVMDscConfiguration` maakt gebruik van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71a7d-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="71a7d-142">`Publish-AzureVMDscConfiguration`wordt in een configuratiebestand, voor afhankelijke DSC-resources wordt gescand en maakt een ZIP-bestand met Hallo-configuratie en DSC-resources nodig tooenact Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="71a7d-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="71a7d-143">Daarnaast kunnen er Hallo pakket lokaal via Hallo `-ConfigurationArchivePath` parameter.</span><span class="sxs-lookup"><span data-stu-id="71a7d-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="71a7d-144">Het publiceert Hallo ZIP-bestand tooAzure blob-opslag en beveiligt het met een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="71a7d-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="71a7d-145">Hallo ZIP-bestand gemaakt met deze cmdlet heeft Hallo .ps1-configuratiescript op Hallo hoofdmap van de archiefmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="71a7d-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="71a7d-146">Bronnen hebben Hallo modulemap geplaatst in de archiefmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="71a7d-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="71a7d-147">`Set-AzureVMDscExtension`injects hello vereiste instellingen voor Hallo PowerShell DSC-uitbreiding in een VM-configuratie-object.</span><span class="sxs-lookup"><span data-stu-id="71a7d-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="71a7d-148">Hallo VM wijzigingen moet in het klassieke implementatiemodel hello, toegepaste tooan virtuele machine van Azure met `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="71a7d-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="71a7d-149">`Get-AzureVMDscExtension`haalt status van Hallo DSC-extensie van een bepaalde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="71a7d-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="71a7d-150">`Get-AzureVMDscExtensionStatus`haalt status Hallo van Hallo DSC-configuratie door de handler voor Hallo DSC-uitbreiding van kracht.</span><span class="sxs-lookup"><span data-stu-id="71a7d-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="71a7d-151">Deze actie kan worden uitgevoerd op een enkele virtuele machine of een groep VM's.</span><span class="sxs-lookup"><span data-stu-id="71a7d-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="71a7d-152">`Remove-AzureVMDscExtension`Hallo-extensie handler verwijdert uit een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="71a7d-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="71a7d-153">Deze cmdlet biedt **niet** Hallo-configuratie verwijderen, Hallo WMF verwijderen of wijzigen van Hallo toegepast op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="71a7d-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="71a7d-154">Hallo-extensie handler worden alleen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="71a7d-155">**Belangrijke verschillen in ASM en Azure Resource Manager-cmdlets**</span><span class="sxs-lookup"><span data-stu-id="71a7d-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="71a7d-156">Azure Resource Manager-cmdlets worden synchroon.</span><span class="sxs-lookup"><span data-stu-id="71a7d-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="71a7d-157">ASM-cmdlets zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="71a7d-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="71a7d-158">ResourceGroupName, VMName ArchiveStorageAccountName, versie en locatie zijn alle vereiste parameters in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71a7d-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="71a7d-159">ArchiveResourceGroupName is een nieuwe optionele parameter voor Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71a7d-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="71a7d-160">U kunt deze parameter opgeven wanneer uw storage-account hoort tooa andere resourcegroep dan Hallo een waar Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71a7d-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="71a7d-161">ConfigurationArchive wordt ArchiveBlobName aangeroepen in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71a7d-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="71a7d-162">ContainerName wordt ArchiveContainerName aangeroepen in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71a7d-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="71a7d-163">StorageEndpointSuffix wordt ArchiveStorageEndpointSuffix aangeroepen in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71a7d-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="71a7d-164">Hallo AutoUpdate switch is tooAzure Resource Manager tooenable automatische updates van Hallo extensie handler toohello meest recente versie als en wanneer deze beschikbaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="71a7d-165">Houd er rekening mee dat deze parameter heeft Hallo potentiële toocause herstarts op Hallo VM wanneer een nieuwe versie van WMF is vrijgegeven Hallo.</span><span class="sxs-lookup"><span data-stu-id="71a7d-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="71a7d-166">Azure portal-functionaliteit</span><span class="sxs-lookup"><span data-stu-id="71a7d-166">Azure portal functionality</span></span>
<span data-ttu-id="71a7d-167">Blader tooa VM.</span><span class="sxs-lookup"><span data-stu-id="71a7d-167">Browse tooa VM.</span></span> <span data-ttu-id="71a7d-168">-Onder Instellingen > Algemeen klik "-extensies."</span><span class="sxs-lookup"><span data-stu-id="71a7d-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="71a7d-169">Een nieuw deelvenster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71a7d-169">A new pane is created.</span></span> <span data-ttu-id="71a7d-170">Klik op "Toevoegen" en selecteer PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="71a7d-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="71a7d-171">Hallo-portal moet invoer.</span><span class="sxs-lookup"><span data-stu-id="71a7d-171">hello portal needs input.</span></span>
<span data-ttu-id="71a7d-172">**Configuratie-Modules of Script**: dit veld is verplicht.</span><span class="sxs-lookup"><span data-stu-id="71a7d-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="71a7d-173">Vereist een .ps1-bestand met een configuratiescript of een ZIP-bestand met een .ps1-configuratiescript in Hallo-hoofdmap en alle afhankelijke resources in mappen van de module binnen Hallo .zip.</span><span class="sxs-lookup"><span data-stu-id="71a7d-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="71a7d-174">Het kan worden gemaakt met de Hallo `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` opgenomen in het Hallo-SDK van Azure PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71a7d-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="71a7d-175">Hallo ZIP-bestand is geüpload naar de gebruiker blob-opslag beveiligd door een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="71a7d-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="71a7d-176">**Bestand met configuratiegegevens PSD1**: dit veld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="71a7d-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="71a7d-177">Als uw configuratie een configuratiebestand voor de gegevens in .psd1 vereist, gebruikt u dit veld tooselect deze en upload het tooyour gebruiker blob-opslag, waar deze wordt beveiligd door een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="71a7d-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="71a7d-178">**Naam van configuratie Modulegekwalificeerde**: .ps1-bestanden kunnen meerdere functies van de configuratie hebben.</span><span class="sxs-lookup"><span data-stu-id="71a7d-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="71a7d-179">Voer de naam Hallo van Hallo .ps1 configuratiescript gevolgd door een '\' en Hallo-naam van Hallo configuratie functie.</span><span class="sxs-lookup"><span data-stu-id="71a7d-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="71a7d-180">Bijvoorbeeld, als uw script .ps1 heeft configuration.ps1' hello naam' en Hallo configuratie 'IisInstall' is, dus voert u:`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="71a7d-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="71a7d-181">**Configuratie argumenten**: als Hallo configuratie functie argumenten aanneemt, deze hier in Hallo-indeling invoeren `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="71a7d-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="71a7d-182">Opmerking: deze indeling is een andere indeling dan hoe configuratie argumenten via PowerShell-cmdlets of de Resource Manager-sjablonen worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="71a7d-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="71a7d-183">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="71a7d-183">Getting started</span></span>
<span data-ttu-id="71a7d-184">Hello Azure DSC-extensie neemt in documenten van DSC-configuratie en ze enacts op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="71a7d-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="71a7d-185">Hier volgt een eenvoudig voorbeeld van een configuratie.</span><span class="sxs-lookup"><span data-stu-id="71a7d-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="71a7d-186">Dit lokaal opslaan als 'IisInstall.ps1':</span><span class="sxs-lookup"><span data-stu-id="71a7d-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="71a7d-187">volgende stappen plaats Hallo IisInstall.ps1 script op Hallo Hallo opgegeven VM, Hallo configuratie uitvoeren en rapporteren over de status.</span><span class="sxs-lookup"><span data-stu-id="71a7d-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="71a7d-188">Klassieke model</span><span class="sxs-lookup"><span data-stu-id="71a7d-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="71a7d-189">Azure Resource Manager-model</span><span class="sxs-lookup"><span data-stu-id="71a7d-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="71a7d-190">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="71a7d-190">Logging</span></span>
<span data-ttu-id="71a7d-191">Logboekbestanden worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="71a7d-191">Logs are placed in:</span></span>

<span data-ttu-id="71a7d-192">C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[versienummer]</span><span class="sxs-lookup"><span data-stu-id="71a7d-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="71a7d-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71a7d-193">Next steps</span></span>
<span data-ttu-id="71a7d-194">Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="71a7d-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="71a7d-195">Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71a7d-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="71a7d-196">toofind aanvullende functionaliteit die u met PowerShell DSC beheren kunt [bladeren Hallo PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) voor meer DSC-resources.</span><span class="sxs-lookup"><span data-stu-id="71a7d-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="71a7d-197">Zie voor meer informatie over gevoelige parameters doorgeven in configuraties [beheren van referenties veilig met Hallo DSC-uitbreiding handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71a7d-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

