---
title: een Linux-VM met een VM-extensie aaaMonitoring | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Linux-extensie voor diagnostische toomonitor Hallo prestaties en diagnostische gegevens van een Linux-VM in Azure.
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
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="3c92f-103">Gebruik Hallo Linux-extensie voor diagnostische toomonitor Hallo prestaties en diagnostische gegevens van een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="3c92f-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="3c92f-104">Dit document beschrijft versie 2.3 Hallo diagnostische Linux-extensie.</span><span class="sxs-lookup"><span data-stu-id="3c92f-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c92f-105">Deze versie is afgeschaft en wordt niet gepubliceerd elk gewenst moment na 30 juni 2018.</span><span class="sxs-lookup"><span data-stu-id="3c92f-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="3c92f-106">Het is vervangen door versie 3.0.</span><span class="sxs-lookup"><span data-stu-id="3c92f-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="3c92f-107">Zie voor meer informatie, Hallo [documentatie voor versie 3.0 Hallo Linux diagnostische extensie](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3c92f-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="3c92f-108">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3c92f-108">Introduction</span></span>

<span data-ttu-id="3c92f-109">(**Opmerking**: Hallo diagnostische Linux-extensie is open source op [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) waarop Hallo meest actuele informatie over het Hallo-extensie voor het eerst wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="3c92f-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="3c92f-110">Kunt u toocheck hello [GitHub-pagina](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) eerste.)</span><span class="sxs-lookup"><span data-stu-id="3c92f-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="3c92f-111">Hallo Linux diagnostische uitbreiding kunt u een gebruiker monitor Hallo virtuele Linux-machines die worden uitgevoerd op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c92f-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="3c92f-112">Er Hallo volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="3c92f-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="3c92f-113">Verzamelt en uploadt Hallo informatie over de systeemprestaties van Hallo Linux VM toohello van gebruiker opslag tabel, met inbegrip van diagnose- en syslog-informatie.</span><span class="sxs-lookup"><span data-stu-id="3c92f-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="3c92f-114">Hiermee kunt gebruikers toocustomize Hallo gegevens metrische gegevens die worden verzameld en geüpload.</span><span class="sxs-lookup"><span data-stu-id="3c92f-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="3c92f-115">Hiermee kunt gebruikers tooupload opgegeven logboek bestanden tooa aangewezen opslag tabel.</span><span class="sxs-lookup"><span data-stu-id="3c92f-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="3c92f-116">In huidige versie Hallo 2.3 omvat Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="3c92f-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="3c92f-117">Alle Linux Rsyslog-Logboeken, met inbegrip van systeem, beveiliging en toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="3c92f-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="3c92f-118">Alle systeemgegevens die opgegeven op [Hallo System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3c92f-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="3c92f-119">Door gebruiker opgegeven logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="3c92f-119">User-specified log files.</span></span>

<span data-ttu-id="3c92f-120">Deze extensie werkt met zowel klassieke Hallo als Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3c92f-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="3c92f-121">Huidige versie van het Hallo-extensie en afschaffing van oude versies</span><span class="sxs-lookup"><span data-stu-id="3c92f-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="3c92f-122">meest recente versie van de uitbreiding Hallo Hallo is **2.3**, en **eventuele oude versies (2.0, 2.1 en 2.2) wordt afgeschaft en niet-gepubliceerde einde van dit jaar (2017)**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="3c92f-123">Als u Hallo Linux diagnose uitbreiding geïnstalleerd met automatische secundaire versie upgrade uitgeschakeld, het raadzaam dat u Hallo uitbreiding verwijderen en opnieuw installeren met de upgrade van secundaire versie automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3c92f-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="3c92f-124">Op klassieke virtuele machines (ASM), kunt u dit doen door op te geven '2.*' hello versie als u de extensie Hallo via Azure XPLAT CLI of Powershell installeert.</span><span class="sxs-lookup"><span data-stu-id="3c92f-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="3c92f-125">Op virtuele machines ARM, u kunt dit doen door op te nemen ' 'autoUpgradeMinorVersion': true' in hello VM-sjabloon voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c92f-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="3c92f-126">Ook hebt een nieuwe installatie van Hallo uitbreiding Hallo automatisch secundaire versie upgraden optie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3c92f-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="3c92f-127">Hallo-extensie inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c92f-127">Enable hello extension</span></span>

<span data-ttu-id="3c92f-128">U kunt deze uitbreiding inschakelen met behulp van Hallo [Azure-portal](https://portal.azure.com/#), Azure PowerShell of Azure CLI-scripts.</span><span class="sxs-lookup"><span data-stu-id="3c92f-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="3c92f-129">tooview en Hallo systeem configureren en rechtstreeks prestatiegegevens van hello Azure-portal, volg [deze stappen uit op Hallo Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="3c92f-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="3c92f-130">In dit artikel is gericht op het tooenable en Hallo-uitbreiding configureren met behulp van Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="3c92f-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="3c92f-131">Hiermee kunt u tooread en bekijkt hello-gegevens direct vanuit Hallo opslag tabel.</span><span class="sxs-lookup"><span data-stu-id="3c92f-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="3c92f-132">Houd er rekening mee dat Hallo configuratiemethoden die hier worden beschreven, niet voor hello Azure-portal werkt.</span><span class="sxs-lookup"><span data-stu-id="3c92f-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="3c92f-133">tooview en Hallo systeem- en -gegevens rechtstreeks vanuit hello Azure-portal configureren, Hallo-uitbreiding moet worden ingeschakeld via het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="3c92f-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c92f-134">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c92f-134">Prerequisites</span></span>

* <span data-ttu-id="3c92f-135">**Azure Linux Agent versie 2.0.6 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="3c92f-136">Opmerking dat de meeste Azure VM Linux-afbeeldingen versie 2.0.6 bevatten of hoger.</span><span class="sxs-lookup"><span data-stu-id="3c92f-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="3c92f-137">U kunt uitvoeren **WAAgent-versie** tooconfirm welke versie is geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="3c92f-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="3c92f-138">Als u een versie die ouder is dan 2.0.6 van Hallo VM wordt uitgevoerd, kunt u volgen [deze instructies op GitHub](https://github.com/Azure/WALinuxAgent "instructies") tooupdate deze.</span><span class="sxs-lookup"><span data-stu-id="3c92f-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="3c92f-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-139">**Azure CLI**.</span></span> <span data-ttu-id="3c92f-140">Ga als volgt [in deze richtlijnen voor het installeren van de CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI-omgeving op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3c92f-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="3c92f-141">Nadat u Azure CLI hebt geïnstalleerd, kunt u Hallo **azure** via de opdrachtregelinterface (Bash, Terminal of een opdrachtprompt) tooaccess hello Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="3c92f-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="3c92f-142">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3c92f-142">For example:</span></span>

  * <span data-ttu-id="3c92f-143">Voer **azure vm-extensie set--help** voor gedetailleerde help-informatie.</span><span class="sxs-lookup"><span data-stu-id="3c92f-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="3c92f-144">Voer **azure-aanmelding** toosign in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3c92f-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="3c92f-145">Voer **azure vm lijst** toolist alle virtuele machines die u op Azure hebt Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c92f-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="3c92f-146">Een storage account toostore Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c92f-146">A storage account toostore hello data.</span></span> <span data-ttu-id="3c92f-147">U moet de naam van een account dat eerder is gemaakt en een toegang tot belangrijke tooupload Hallo gegevens tooyour opslag.</span><span class="sxs-lookup"><span data-stu-id="3c92f-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="3c92f-148">Hello Azure CLI opdracht tooenable Hallo Linux diagnostische uitbreiding gebruiken</span><span class="sxs-lookup"><span data-stu-id="3c92f-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="3c92f-149">Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-149">Scenario 1.</span></span> <span data-ttu-id="3c92f-150">Hallo-extensie met Hallo standaardgegevensset inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c92f-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="3c92f-151">In versie 2.3 of hoger bevat de Hallo standaardgegevens die worden verzameld:</span><span class="sxs-lookup"><span data-stu-id="3c92f-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="3c92f-152">Alle Rsyslog gegevens (inclusief systeem, beveiliging en toepassingslogboeken).</span><span class="sxs-lookup"><span data-stu-id="3c92f-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="3c92f-153">Een kernset aan de basisgegevens van het systeem.</span><span class="sxs-lookup"><span data-stu-id="3c92f-153">A core set of basis system data.</span></span> <span data-ttu-id="3c92f-154">Let op Hallo van volledige gegevensset wordt beschreven op Hallo [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3c92f-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="3c92f-155">Als u wilt dat tooenable extra gegevens verder met Hallo stappen in scenario's 2 en 3.</span><span class="sxs-lookup"><span data-stu-id="3c92f-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="3c92f-156">Step 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-156">Step 1.</span></span> <span data-ttu-id="3c92f-157">Maak een bestand met de naam PrivateConfig.json Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="3c92f-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="3c92f-158">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="3c92f-158">Step 2.</span></span> <span data-ttu-id="3c92f-159">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --persoonlijke configuratiepad PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="3c92f-160">Scenario 2.</span><span class="sxs-lookup"><span data-stu-id="3c92f-160">Scenario 2.</span></span> <span data-ttu-id="3c92f-161">Maatstaven voor prestaties monitor Hallo aanpassen</span><span class="sxs-lookup"><span data-stu-id="3c92f-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="3c92f-162">Deze sectie beschrijft hoe toocustomize Hallo prestaties en diagnostische gegevenstabel.</span><span class="sxs-lookup"><span data-stu-id="3c92f-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="3c92f-163">Step 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-163">Step 1.</span></span> <span data-ttu-id="3c92f-164">Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3c92f-165">Ook een bestand met de naam PublicConfig.json maken.</span><span class="sxs-lookup"><span data-stu-id="3c92f-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="3c92f-166">Geef gegevens op bepaalde Hallo gewenste toocollect.</span><span class="sxs-lookup"><span data-stu-id="3c92f-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="3c92f-167">Voor alle ondersteunde providers en variabelen te verwijzen naar Hallo [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3c92f-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="3c92f-168">U kunt meerdere query's en deze opslaan op meerdere tabellen door meer query's toohello script toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3c92f-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="3c92f-169">Standaard wordt altijd Hallo Rsyslog gegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="3c92f-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="3c92f-170">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="3c92f-170">Step 2.</span></span> <span data-ttu-id="3c92f-171">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="3c92f-172">Scenario 3.</span><span class="sxs-lookup"><span data-stu-id="3c92f-172">Scenario 3.</span></span> <span data-ttu-id="3c92f-173">Uploaden van uw eigen logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="3c92f-173">Upload your own log files</span></span>

<span data-ttu-id="3c92f-174">Deze sectie beschrijft hoe toocollect en uploaden specifieke tooyour storage-account logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="3c92f-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="3c92f-175">U moet beide Hallo tooyour logboek bestands- en Hallo padnaam van Hallo tabel waar u toostore uw logboek toospecify.</span><span class="sxs-lookup"><span data-stu-id="3c92f-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="3c92f-176">U kunt meerdere logboekbestanden maken door meerdere toohello script van de tabel file/vermeldingen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3c92f-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="3c92f-177">Step 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-177">Step 1.</span></span> <span data-ttu-id="3c92f-178">Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3c92f-179">Maakt u een ander bestand met de naam PublicConfig.json met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="3c92f-179">Then create another file named PublicConfig.json with hello following content:</span></span>

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

<span data-ttu-id="3c92f-180">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="3c92f-180">Step 2.</span></span> <span data-ttu-id="3c92f-181">Voer `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json` uit.</span><span class="sxs-lookup"><span data-stu-id="3c92f-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="3c92f-182">Houd er rekening mee dat met deze instelling op Hallo extensie versies voorafgaande too2.3, alle logboeken geschreven te`/var/log/mysql.err` te kunnen worden gedupliceerd`/var/log/syslog` (of `/var/log/messages` , afhankelijk van Hallo Linux distro) ook.</span><span class="sxs-lookup"><span data-stu-id="3c92f-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="3c92f-183">Als u deze dubbele logboekregistratie tooavoid wilt, kunt u het vastleggen van uitsluiten `local6` faciliteit wordt geregistreerd in de configuratie van uw rsyslog.</span><span class="sxs-lookup"><span data-stu-id="3c92f-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="3c92f-184">Het Hallo Linux distro afhangt, maar op een systeem Ubuntu 14.04 Hallo bestand toomodify is `/etc/rsyslog.d/50-default.conf` en kunt u de regel Hallo vervangen `*.*;auth,authpriv.none -/var/log/syslog` te`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="3c92f-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="3c92f-185">Dit probleem is opgelost in Hallo nieuwste hotfix release van 2.3 (2.3.9007), dus als er Hallo extensie versie 2.3, dit probleem niet moet gebeuren.</span><span class="sxs-lookup"><span data-stu-id="3c92f-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="3c92f-186">Als dit wel nog steeds zelfs na het opnieuw opstarten van uw virtuele machine, contact met ons opnemen en help ons waarom Hallo nieuwste hotfixversie niet automatisch wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3c92f-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="3c92f-187">Scenario 4.</span><span class="sxs-lookup"><span data-stu-id="3c92f-187">Scenario 4.</span></span> <span data-ttu-id="3c92f-188">Hallo-extensie van de logboekbestanden verzamelen stoppen</span><span class="sxs-lookup"><span data-stu-id="3c92f-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="3c92f-189">Deze sectie beschrijft hoe toostop Hallo-extensie van het verzamelen van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="3c92f-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="3c92f-190">Let op: Hallo bewakingsproces agent wordt nog steeds actief en werkend worden zelfs met deze herconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="3c92f-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="3c92f-191">Als u toostop Hallo agentproces volledig bewaking wilt, kunt u dit doen door het uitschakelen van extensie is Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c92f-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="3c92f-192">Hallo opdracht toodisable Hallo extensie is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="3c92f-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="3c92f-193">Step 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-193">Step 1.</span></span> <span data-ttu-id="3c92f-194">Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1.</span><span class="sxs-lookup"><span data-stu-id="3c92f-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3c92f-195">Maak een ander bestand met de naam PublicConfig.json met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="3c92f-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="3c92f-196">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="3c92f-196">Step 2.</span></span> <span data-ttu-id="3c92f-197">Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3c92f-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="3c92f-198">Controleer uw gegevens</span><span class="sxs-lookup"><span data-stu-id="3c92f-198">Review your data</span></span>

<span data-ttu-id="3c92f-199">Hallo prestaties en diagnostische gegevens worden opgeslagen in een tabel met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3c92f-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="3c92f-200">Bekijk [hoe toouse Azure Table Storage met Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn tooaccess Hallo gegevens in de opslag van de Hallo tabel weergeven met behulp van Azure CLI-scripts.</span><span class="sxs-lookup"><span data-stu-id="3c92f-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="3c92f-201">Bovendien kunt u na UI extra tooaccess Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="3c92f-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="3c92f-202">Visual Studio Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="3c92f-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="3c92f-203">Ga tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="3c92f-203">Go tooyour storage account.</span></span> <span data-ttu-id="3c92f-204">Nadat het Hallo VM wordt uitgevoerd gedurende vijf minuten, ziet u vier Hallo standaardtabellen: 'LinuxCpu', 'LinuxDisk', 'LinuxMemory' en 'Linuxsyslog'.</span><span class="sxs-lookup"><span data-stu-id="3c92f-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="3c92f-205">Dubbelklik op Hallo namen tooview Hallo tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="3c92f-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="3c92f-206">[Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/ "Azure Opslagverkenner").</span><span class="sxs-lookup"><span data-stu-id="3c92f-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![Afbeelding](./media/diagnostic-extension/no1.png)

<span data-ttu-id="3c92f-208">Als u fileCfg of perfCfg (zoals beschreven in scenario's 2 en 3) hebt ingeschakeld, kunt u Visual Studio Server Explorer en Azure Storage Explorer tooview niet-standaard gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c92f-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3c92f-209">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="3c92f-209">Known issues</span></span>

* <span data-ttu-id="3c92f-210">Hallo Rsyslog informatie en logboekbestand klant opgegeven alleen toegankelijk via het uitvoeren van scripts.</span><span class="sxs-lookup"><span data-stu-id="3c92f-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
