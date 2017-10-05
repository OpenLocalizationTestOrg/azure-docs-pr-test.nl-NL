---
title: Bewaking van een Linux-VM met een VM-extensie | Microsoft Docs
description: Informatie over het gebruik van de diagnostische Linux-extensie voor het bewaken van de prestaties en diagnostische gegevens van een Linux-VM in Azure.
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="f96f0-103">De diagnostische Linux-extensie gebruiken voor het controleren van de prestaties en diagnostische gegevens van een Linux VM</span><span class="sxs-lookup"><span data-stu-id="f96f0-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="f96f0-104">Dit document beschrijft versie 2.3 van de diagnostische Linux-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="f96f0-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f96f0-105">Deze versie is afgeschaft en wordt niet gepubliceerd elk gewenst moment na 30 juni 2018.</span><span class="sxs-lookup"><span data-stu-id="f96f0-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="f96f0-106">Het is vervangen door versie 3.0.</span><span class="sxs-lookup"><span data-stu-id="f96f0-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="f96f0-107">Zie voor meer informatie de [documentatie voor versie 3.0 van de Linux-extensie voor diagnostische](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f96f0-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="f96f0-108">Inleiding</span><span class="sxs-lookup"><span data-stu-id="f96f0-108">Introduction</span></span>

<span data-ttu-id="f96f0-109">(**Opmerking**: de diagnostische Linux-uitbreiding is open source op [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) waarop de meest actuele informatie over de uitbreiding voor het eerst wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="f96f0-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="f96f0-110">U wilt controleren de [GitHub-pagina](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) eerste.)</span><span class="sxs-lookup"><span data-stu-id="f96f0-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="f96f0-111">De Linux-extensie voor diagnostische helpt de monitor van een gebruiker de Linux-virtuele machines die worden uitgevoerd op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f96f0-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="f96f0-112">Deze heeft de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="f96f0-112">It has the following capabilities:</span></span>

* <span data-ttu-id="f96f0-113">Verzamelt en uploadt de informatie over de systeemprestaties van de Linux-VM aan de gebruiker opslag tabel, met inbegrip van diagnose- en syslog-informatie.</span><span class="sxs-lookup"><span data-stu-id="f96f0-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="f96f0-114">Hiermee kunnen gebruikers de gegevens metrische gegevens die worden verzameld en geüpload aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f96f0-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="f96f0-115">Hiermee kunnen gebruikers opgegeven logboekbestanden uploaden naar een tabel aangewezen opslag.</span><span class="sxs-lookup"><span data-stu-id="f96f0-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="f96f0-116">In de huidige versie 2.3 omvatten de gegevens:</span><span class="sxs-lookup"><span data-stu-id="f96f0-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="f96f0-117">Alle Linux Rsyslog-Logboeken, met inbegrip van systeem, beveiliging en toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="f96f0-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="f96f0-118">Alle systeemgegevens die opgegeven op [de site van System Center Cross-Platform oplossingen](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="f96f0-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="f96f0-119">Door gebruiker opgegeven logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="f96f0-119">User-specified log files.</span></span>

<span data-ttu-id="f96f0-120">Deze extensie werkt met zowel het klassieke als Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f96f0-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="f96f0-121">Huidige versie van de extensie en afschaffing van oude versies</span><span class="sxs-lookup"><span data-stu-id="f96f0-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="f96f0-122">De meest recente versie van de uitbreiding is **2.3**, en **eventuele oude versies (2.0, 2.1 en 2.2) wordt afgeschaft en niet-gepubliceerde einde van dit jaar (2017)**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="f96f0-123">Als u de extensie Linux diagnose met secundaire versie van Automatische upgrade uitgeschakeld hebt geïnstalleerd, het raadzaam dat u de uitbreiding verwijderen en opnieuw installeren met de upgrade van secundaire versie automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f96f0-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="f96f0-124">Op klassieke virtuele machines (ASM), kunt u dit doen door op te geven '2.*' als de versie, als u de uitbreiding via Azure XPLAT CLI of Powershell installeert.</span><span class="sxs-lookup"><span data-stu-id="f96f0-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="f96f0-125">Op virtuele machines ARM, u kunt dit doen door op te nemen ' 'autoUpgradeMinorVersion': true' in de VM-sjabloon voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="f96f0-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="f96f0-126">Een nieuwe installatie van de extensie, moeten ook moet de secundaire versie van Automatische upgrade-optie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f96f0-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="f96f0-127">De uitbreiding inschakelen</span><span class="sxs-lookup"><span data-stu-id="f96f0-127">Enable the extension</span></span>

<span data-ttu-id="f96f0-128">U kunt deze uitbreiding inschakelen met behulp van de [Azure-portal](https://portal.azure.com/#), Azure PowerShell of Azure CLI-scripts.</span><span class="sxs-lookup"><span data-stu-id="f96f0-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="f96f0-129">Als u wilt weergeven en configureren van de systeem- en gegevens rechtstreeks vanuit de Azure portal, volg [deze stappen uit op de Azure-blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="f96f0-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="f96f0-130">Dit artikel is gericht op het inschakelen en configureren van de uitbreiding met behulp van Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f96f0-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="f96f0-131">Hiermee kunt u om te lezen en de gegevens rechtstreeks vanuit de tabel voor opslag weergeven.</span><span class="sxs-lookup"><span data-stu-id="f96f0-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="f96f0-132">Houd er rekening mee dat de configuratiemethoden die hier worden beschreven, niet voor de Azure-portal werkt.</span><span class="sxs-lookup"><span data-stu-id="f96f0-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="f96f0-133">Als u wilt weergeven en configureren van de systeem- en gegevens rechtstreeks vanuit de Azure portal, moet de extensie worden ingeschakeld via de portal.</span><span class="sxs-lookup"><span data-stu-id="f96f0-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f96f0-134">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f96f0-134">Prerequisites</span></span>

* <span data-ttu-id="f96f0-135">**Azure Linux Agent versie 2.0.6 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="f96f0-136">Opmerking dat de meeste Azure VM Linux-afbeeldingen versie 2.0.6 bevatten of hoger.</span><span class="sxs-lookup"><span data-stu-id="f96f0-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="f96f0-137">U kunt uitvoeren **WAAgent-versie** om te controleren welke versie is geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f96f0-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="f96f0-138">Als u een versie die ouder is dan 2.0.6 van de virtuele machine wordt uitgevoerd, kunt u volgen [deze instructies op GitHub](https://github.com/Azure/WALinuxAgent "instructies") bij te werken.</span><span class="sxs-lookup"><span data-stu-id="f96f0-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="f96f0-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-139">**Azure CLI**.</span></span> <span data-ttu-id="f96f0-140">Ga als volgt [in deze richtlijnen voor het installeren van de CLI](../../../cli-install-nodejs.md) voor het instellen van de Azure CLI-omgeving op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f96f0-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="f96f0-141">Nadat u Azure CLI hebt geïnstalleerd, kunt u de **azure** via de opdrachtregelinterface (Bash, Terminal of een opdrachtprompt) voor toegang tot de Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f96f0-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="f96f0-142">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f96f0-142">For example:</span></span>

  * <span data-ttu-id="f96f0-143">Voer **azure vm-extensie set--help** voor gedetailleerde help-informatie.</span><span class="sxs-lookup"><span data-stu-id="f96f0-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="f96f0-144">Voer **azure-aanmelding** aan te melden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="f96f0-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="f96f0-145">Voer **azure vm lijst** voor een lijst met alle virtuele machines die u op Azure hebt.</span><span class="sxs-lookup"><span data-stu-id="f96f0-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="f96f0-146">Een opslagaccount voor het opslaan van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="f96f0-146">A storage account to store the data.</span></span> <span data-ttu-id="f96f0-147">U moet de naam van een account dat eerder is gemaakt en een toegangssleutel voor het uploaden van de gegevens naar uw opslag.</span><span class="sxs-lookup"><span data-stu-id="f96f0-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="f96f0-148">Gebruik de Azure CLI-opdracht voor het Linux-extensie voor diagnostische inschakelen</span><span class="sxs-lookup"><span data-stu-id="f96f0-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="f96f0-149">Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-149">Scenario 1.</span></span> <span data-ttu-id="f96f0-150">De uitbreiding met de standaardgegevensset inschakelen</span><span class="sxs-lookup"><span data-stu-id="f96f0-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="f96f0-151">In versie 2.3 of hoger bevat de gegevens die worden verzameld:</span><span class="sxs-lookup"><span data-stu-id="f96f0-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="f96f0-152">Alle Rsyslog gegevens (inclusief systeem, beveiliging en toepassingslogboeken).</span><span class="sxs-lookup"><span data-stu-id="f96f0-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="f96f0-153">Een kernset aan de basisgegevens van het systeem.</span><span class="sxs-lookup"><span data-stu-id="f96f0-153">A core set of basis system data.</span></span> <span data-ttu-id="f96f0-154">Let op: de volledige gegevensset wordt beschreven op de [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="f96f0-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="f96f0-155">Als u extra gegevens inschakelen wilt, gaat u verder met de stappen in scenario's 2 en 3.</span><span class="sxs-lookup"><span data-stu-id="f96f0-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="f96f0-156">Step 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-156">Step 1.</span></span> <span data-ttu-id="f96f0-157">Maak een bestand met de naam PrivateConfig.json met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f96f0-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="f96f0-158">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="f96f0-158">Step 2.</span></span> <span data-ttu-id="f96f0-159">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --persoonlijke configuratiepad PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="f96f0-160">Scenario 2.</span><span class="sxs-lookup"><span data-stu-id="f96f0-160">Scenario 2.</span></span> <span data-ttu-id="f96f0-161">Aanpassen van de monitor maatstaven voor prestaties</span><span class="sxs-lookup"><span data-stu-id="f96f0-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="f96f0-162">Deze sectie beschrijft het aanpassen van de prestaties en diagnostische gegevenstabel.</span><span class="sxs-lookup"><span data-stu-id="f96f0-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="f96f0-163">Step 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-163">Step 1.</span></span> <span data-ttu-id="f96f0-164">Maak een bestand met de naam PrivateConfig.json met de inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="f96f0-165">Ook een bestand met de naam PublicConfig.json maken.</span><span class="sxs-lookup"><span data-stu-id="f96f0-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="f96f0-166">Geef de specifieke gegevens die u wenst te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="f96f0-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="f96f0-167">Voor alle ondersteunde providers en variabelen te verwijzen naar de [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="f96f0-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="f96f0-168">U kunt meerdere query's en deze opslaan op meerdere tabellen door meer query's naar het script toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f96f0-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="f96f0-169">Standaard wordt altijd de Rsyslog gegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="f96f0-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="f96f0-170">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="f96f0-170">Step 2.</span></span> <span data-ttu-id="f96f0-171">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="f96f0-172">Scenario 3.</span><span class="sxs-lookup"><span data-stu-id="f96f0-172">Scenario 3.</span></span> <span data-ttu-id="f96f0-173">Uploaden van uw eigen logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="f96f0-173">Upload your own log files</span></span>

<span data-ttu-id="f96f0-174">Deze sectie wordt beschreven hoe verzamelen en specifieke logboekbestanden uploaden naar uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="f96f0-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="f96f0-175">U moet zowel het pad naar het logboekbestand en de naam van de tabel waar u wilt opslaan van uw logboek opgeven.</span><span class="sxs-lookup"><span data-stu-id="f96f0-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="f96f0-176">U kunt meerdere logboekbestanden maken door meerdere bestandstabel/vermeldingen toe te voegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="f96f0-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="f96f0-177">Step 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-177">Step 1.</span></span> <span data-ttu-id="f96f0-178">Maak een bestand met de naam PrivateConfig.json met de inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="f96f0-179">Maak een ander bestand met de naam PublicConfig.json met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f96f0-179">Then create another file named PublicConfig.json with the following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="f96f0-180">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="f96f0-180">Step 2.</span></span> <span data-ttu-id="f96f0-181">Voer `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json` uit.</span><span class="sxs-lookup"><span data-stu-id="f96f0-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="f96f0-182">Houd er rekening mee dat met deze instelling op de extensie versies voorafgaand aan 2.3 alle logboeken geschreven naar `/var/log/mysql.err` om te kunnen worden gedupliceerd `/var/log/syslog` (of `/var/log/messages` , afhankelijk van de Linux-distro) ook.</span><span class="sxs-lookup"><span data-stu-id="f96f0-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="f96f0-183">Als u voorkomen dat deze dubbele logboekregistratie wilt, kunt u het vastleggen van uitsluiten `local6` faciliteit wordt geregistreerd in de configuratie van uw rsyslog.</span><span class="sxs-lookup"><span data-stu-id="f96f0-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="f96f0-184">Dit is afhankelijk van de Linux-distro, maar op een systeem Ubuntu 14.04 het bestand te wijzigen is `/etc/rsyslog.d/50-default.conf` en kunt u de regel vervangen `*.*;auth,authpriv.none -/var/log/syslog` naar `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="f96f0-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="f96f0-185">Dit probleem is opgelost in de nieuwste versie van de hotfix van 2.3 (2.3.9007), dus als u de versie van de uitbreiding 2.3 hebt, dit probleem niet moet gebeuren.</span><span class="sxs-lookup"><span data-stu-id="f96f0-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="f96f0-186">Als dit wel nog steeds zelfs na het opnieuw opstarten van uw virtuele machine, contact met ons opnemen en help ons waarom de meest recente hotfixversie niet automatisch wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f96f0-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="f96f0-187">Scenario 4.</span><span class="sxs-lookup"><span data-stu-id="f96f0-187">Scenario 4.</span></span> <span data-ttu-id="f96f0-188">De extensie van de logboekbestanden verzamelen stoppen</span><span class="sxs-lookup"><span data-stu-id="f96f0-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="f96f0-189">Deze sectie beschrijft hoe u de uitbreiding van het verzamelen van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f96f0-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="f96f0-190">Houd er rekening mee dat het bewakingsproces van de agent wordt nog steeds actief en werkend zelfs met deze herconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f96f0-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="f96f0-191">Als u het bewakingsproces van agent volledig worden gestopt wilt, kunt u dit doen door de uitbreiding uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="f96f0-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="f96f0-192">De opdracht de uitbreiding uitschakelen is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="f96f0-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="f96f0-193">Step 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-193">Step 1.</span></span> <span data-ttu-id="f96f0-194">Maak een bestand met de naam PrivateConfig.json met de inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="f96f0-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="f96f0-195">Maak een ander bestand met de naam PublicConfig.json met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f96f0-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="f96f0-196">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="f96f0-196">Step 2.</span></span> <span data-ttu-id="f96f0-197">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="f96f0-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="f96f0-198">Controleer uw gegevens</span><span class="sxs-lookup"><span data-stu-id="f96f0-198">Review your data</span></span>

<span data-ttu-id="f96f0-199">De prestaties en diagnostische gegevens worden opgeslagen in een tabel met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f96f0-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="f96f0-200">Bekijk [hoe Azure Table Storage gebruiken met Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) voor meer informatie over hoe u toegang tot de gegevens in de tabel opslag met behulp van Azure CLI-scripts.</span><span class="sxs-lookup"><span data-stu-id="f96f0-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="f96f0-201">U kunt bovendien na UI-hulpprogramma's gebruiken voor toegang tot de gegevens:</span><span class="sxs-lookup"><span data-stu-id="f96f0-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="f96f0-202">Visual Studio Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="f96f0-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="f96f0-203">Ga naar uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="f96f0-203">Go to your storage account.</span></span> <span data-ttu-id="f96f0-204">Nadat de virtuele machine is uitgevoerd gedurende vijf minuten, ziet u de tabellen vier standaard: 'LinuxCpu', 'LinuxDisk', 'LinuxMemory' en 'Linuxsyslog'.</span><span class="sxs-lookup"><span data-stu-id="f96f0-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="f96f0-205">Dubbelklik op de tabelnamen om de gegevens weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f96f0-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="f96f0-206">[Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/ "Azure Opslagverkenner").</span><span class="sxs-lookup"><span data-stu-id="f96f0-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![Afbeelding](./media/diagnostic-extension/no1.png)

<span data-ttu-id="f96f0-208">Als u fileCfg of perfCfg (zoals beschreven in scenario's 2 en 3) hebt ingeschakeld, kunt u Visual Studio Server Explorer en Azure Storage Explorer gebruiken om niet-standaard gegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f96f0-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f96f0-209">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="f96f0-209">Known issues</span></span>

* <span data-ttu-id="f96f0-210">De Rsyslog informatie en de klant opgegeven logboekbestand kunnen alleen worden benaderd via scripts.</span><span class="sxs-lookup"><span data-stu-id="f96f0-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
