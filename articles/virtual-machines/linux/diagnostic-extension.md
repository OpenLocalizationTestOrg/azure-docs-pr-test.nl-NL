---
title: aaaAzure Compute - Linux-extensie voor diagnostische | Microsoft Docs
description: Hoe tooconfigure hello Azure Linux diagnostische extensie (LAD) toocollect metrische gegevens en gebeurtenissen van virtuele Linux-machines in Azure wordt uitgevoerd.
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="11b2d-103">Linux-extensie voor diagnostische toomonitor metrische gegevens en logboekbestanden gebruiken</span><span class="sxs-lookup"><span data-stu-id="11b2d-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="11b2d-104">Dit document beschrijft versie 3.0 en nieuwere Hallo diagnostische Linux-extensie.</span><span class="sxs-lookup"><span data-stu-id="11b2d-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11b2d-105">Zie voor meer informatie over versie 2.3 en oudere [dit document](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="11b2d-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="11b2d-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="11b2d-106">Introduction</span></span>

<span data-ttu-id="11b2d-107">Hallo Linux diagnostische uitbreiding kunt u een gebruiker controleprogramma Hallo de status van een Linux-VM uitgevoerd op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11b2d-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="11b2d-108">Er Hallo volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="11b2d-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="11b2d-109">Verzamelt systeemprestaties van Hallo VM en slaat ze op in een specifieke tabel in een aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="11b2d-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="11b2d-110">Logboekgebeurtenissen moeten worden opgehaald uit syslog en slaat ze op in een specifieke tabel in Hallo aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="11b2d-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="11b2d-111">Hiermee kunt gebruikers toocustomize Hallo gegevens metrische gegevens die zijn verzameld en worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="11b2d-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="11b2d-112">Kunnen gebruikers toocustomize Hallo syslog faciliteiten en niveaus van gebeurtenissen die worden verzameld en worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="11b2d-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="11b2d-113">Hiermee kunt gebruikers tooupload opgegeven logboek bestanden tooa aangewezen opslag tabel.</span><span class="sxs-lookup"><span data-stu-id="11b2d-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="11b2d-114">Ondersteunt het verzenden van metrische gegevens en logboekbestanden gebeurtenissen tooarbitrary EventHub eindpunten en blobs JSON-indeling in Hallo aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="11b2d-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="11b2d-115">Deze extensie werkt met beide Azure-implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="11b2d-116">Hallo-uitbreiding installeren in uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="11b2d-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="11b2d-117">U kunt deze uitbreiding inschakelen met behulp van hello Azure PowerShell-cmdlets, Azure CLI-scripts of sjablonen voor Azure-implementatie.</span><span class="sxs-lookup"><span data-stu-id="11b2d-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="11b2d-118">Zie voor meer informatie [extensies functies](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="11b2d-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="11b2d-119">Hello Azure-portal niet gebruikte tooenable of LAD 3.0 configureren.</span><span class="sxs-lookup"><span data-stu-id="11b2d-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="11b2d-120">In plaats daarvan installeert en configureert deze versie 2.3.</span><span class="sxs-lookup"><span data-stu-id="11b2d-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="11b2d-121">Azure portal grafieken en waarschuwingen werken met gegevens van beide versies van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="11b2d-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="11b2d-122">Deze installatie-instructies en een [downloadbare voorbeeldconfiguratie](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 te configureren:</span><span class="sxs-lookup"><span data-stu-id="11b2d-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="11b2d-123">Leg Hallo dezelfde metrische gegevens zijn verstrekt door LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="11b2d-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="11b2d-124">vastleggen van een handig set file system maatstaven voor nieuwe tooLAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="11b2d-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="11b2d-125">Hallo syslog standaardverzameling ingeschakeld door LAD 2.3; vastleggen</span><span class="sxs-lookup"><span data-stu-id="11b2d-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="11b2d-126">Schakel hello Azure portal ervaring voor grafieken en waarschuwen voor VM metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="11b2d-127">Hallo downloadbare configuratie is slechts een voorbeeld; Wijzig het toosuit uw eigen behoeften.</span><span class="sxs-lookup"><span data-stu-id="11b2d-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="11b2d-128">Vereisten</span><span class="sxs-lookup"><span data-stu-id="11b2d-128">Prerequisites</span></span>

* <span data-ttu-id="11b2d-129">**Azure Linux Agent versie 2.2.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="11b2d-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="11b2d-130">De meeste Azure VM Linux galerie met installatiekopieën zijn inclusief versie 2.2.7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="11b2d-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="11b2d-131">Voer `/usr/sbin/waagent -version` tooconfirm Hallo versie is geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="11b2d-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="11b2d-132">Als Hallo VM is een oudere versie van de guest-agent hello, volgt u [deze instructies](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate deze.</span><span class="sxs-lookup"><span data-stu-id="11b2d-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="11b2d-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="11b2d-133">**Azure CLI**.</span></span> <span data-ttu-id="11b2d-134">[Instellen van Azure CLI 2.0 Hallo](https://docs.microsoft.com/cli/azure/install-azure-cli) omgeving op uw computer.</span><span class="sxs-lookup"><span data-stu-id="11b2d-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="11b2d-135">Hallo wget-opdracht als u dit nog niet hebt: Voer `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="11b2d-136">Een bestaande Azure-abonnement en een bestaande opslag account binnen het toostore Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="11b2d-137">Voorbeeld-installatie</span><span class="sxs-lookup"><span data-stu-id="11b2d-137">Sample installation</span></span>

<span data-ttu-id="11b2d-138">Vul in de juiste parameters op Hallo Hallo eerste drie regels en voer dit script als hoofdmap:</span><span class="sxs-lookup"><span data-stu-id="11b2d-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="11b2d-139">Hallo-URL voor de voorbeeldconfiguratie Hallo en de inhoud ervan zijn onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="11b2d-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="11b2d-140">Download een exemplaar van Hallo portalinstellingen JSON-bestand en aanpassen voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="11b2d-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="11b2d-141">Alle sjablonen of automation die u samenstellen moet uw eigen exemplaar, in plaats van telkens te downloaden die URL te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="11b2d-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="11b2d-142">Hallo-extensie-instellingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="11b2d-142">Updating hello extension settings</span></span>

<span data-ttu-id="11b2d-143">Nadat u uw beveiligde of openbare instellingen hebt gewijzigd, deze implementeren toohello VM door te voeren dezelfde opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="11b2d-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="11b2d-144">Als alles in het Hallo-instellingen hebt gewijzigd, worden bijgewerkt Hallo instellingen toohello extensie verzonden.</span><span class="sxs-lookup"><span data-stu-id="11b2d-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="11b2d-145">LAD Hallo-configuratie wordt opnieuw geladen en zelf opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="11b2d-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="11b2d-146">Migratie van eerdere versies van Hallo-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="11b2d-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="11b2d-147">meest recente versie van de uitbreiding Hallo Hallo is **3.0**.</span><span class="sxs-lookup"><span data-stu-id="11b2d-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="11b2d-148">**Eventuele oude versies (2.x) zijn afgeschaft en is mogelijk niet-gepubliceerde op of na 31 juli 2018**.</span><span class="sxs-lookup"><span data-stu-id="11b2d-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11b2d-149">Deze extensie introduceert recente wijzigingen toohello configuratie van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="11b2d-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="11b2d-150">Een dergelijke wijziging is aangebracht tooimprove Hallo beveiliging van Hallo-extensie. Als gevolg hiervan kan achterwaartse compatibiliteit met 2.x niet worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="11b2d-151">Hallo-extensie Publisher voor deze extensie is ook anders dan Hallo publisher voor Hallo 2.x-versies.</span><span class="sxs-lookup"><span data-stu-id="11b2d-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="11b2d-152">toomigrate van 2.x toothis nieuwe versie van Hallo-extensie, moet u oude Hallo-extensie (onder Hallo oude naam van uitgever) en vervolgens installeren versie 3 van Hallo uitbreiding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="11b2d-153">Aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-153">Recommendations:</span></span>

* <span data-ttu-id="11b2d-154">Hallo-uitbreiding te installeren met de upgrade van secundaire versie automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="11b2d-155">Geef op klassieke implementatiemodel VMs '3.*' hello versie als u de extensie Hallo via Azure XPLAT CLI of Powershell installeert.</span><span class="sxs-lookup"><span data-stu-id="11b2d-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="11b2d-156">Op Azure Resource Manager deployment model VM's, bevatten ' 'autoUpgradeMinorVersion': true' in hello VM-sjabloon voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="11b2d-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="11b2d-157">Gebruik een nieuwe/verschillende storage-account voor LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="11b2d-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="11b2d-158">Er zijn enkele kleine compatibiliteitsproblemen tussen LAD 2.3 en LAD 3.0 waardoor een account lastige delen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="11b2d-159">LAD 3.0 slaat syslog-gebeurtenissen in een tabel met een andere naam.</span><span class="sxs-lookup"><span data-stu-id="11b2d-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="11b2d-160">Hallo counterSpecifier tekenreeksen voor `builtin` metrische gegevens verschillen LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="11b2d-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="11b2d-161">Beveiligde instellingen</span><span class="sxs-lookup"><span data-stu-id="11b2d-161">Protected settings</span></span>

<span data-ttu-id="11b2d-162">Deze reeks configuratiegegevens gevoelige informatie bevat die moet worden beschermd tegen openbare weergave, bijvoorbeeld storage-referenties.</span><span class="sxs-lookup"><span data-stu-id="11b2d-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="11b2d-163">Deze instellingen zijn verzonden tooand door Hallo-uitbreiding in versleutelde vorm opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="11b2d-164">Naam</span><span class="sxs-lookup"><span data-stu-id="11b2d-164">Name</span></span> | <span data-ttu-id="11b2d-165">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-165">Value</span></span>
---- | -----
<span data-ttu-id="11b2d-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="11b2d-166">storageAccountName</span></span> | <span data-ttu-id="11b2d-167">Hallo-naam van Hallo storage-account waarin gegevens worden geschreven door Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="11b2d-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="11b2d-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="11b2d-168">storageAccountEndPoint</span></span> | <span data-ttu-id="11b2d-169">(optioneel) Hallo-eindpunt te identificeren in welke Hallo storage-account bestaat Hallo-cloud.</span><span class="sxs-lookup"><span data-stu-id="11b2d-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="11b2d-170">Als u deze instelling niet aanwezig is, LAD toohello openbare Azure-cloud, standaard `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="11b2d-171">Deze waarde in een opslagaccount in de Duitse Azure, Azure Government of Azure China toouse dienovereenkomstig instellen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="11b2d-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="11b2d-172">storageAccountSasToken</span></span> | <span data-ttu-id="11b2d-173">Een [Account-SAS-token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) voor Blob- en -services (`ss='bt'`), van toepassing toocontainers en objecten (`srt='co'`), welke verleent toevoegen, maken, weergeven, bijwerken en schrijfmachtigingen (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="11b2d-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="11b2d-174">Voer *niet* Hallo voorloopspaties vraagteken (?) bevatten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="11b2d-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="11b2d-175">mdsdHttpProxy</span></span> | <span data-ttu-id="11b2d-176">(optioneel) HTTP-proxy informatie die nodig is tooenable Hallo extensie tooconnect toohello opgegeven storage-account en -eindpunt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="11b2d-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="11b2d-177">sinksConfig</span></span> | <span data-ttu-id="11b2d-178">(optioneel) Details van alternatieve doelen toowhich metrische gegevens en gebeurtenissen kunnen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="11b2d-179">Hallo specifieke details van elke gegevens sink ondersteund door Hallo extension worden behandeld in Hallo secties die volgen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="11b2d-180">U kunt eenvoudig hello vereist SAS-token via hello Azure-portal opstellen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="11b2d-181">Hallo opslagaccounts voor algemeen gebruik account toowhich gewenste Hallo extensie toowrite selecteren</span><span class="sxs-lookup"><span data-stu-id="11b2d-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="11b2d-182">Selecteer "Shared access signature' hello instellingen deel van Hallo linkermenu</span><span class="sxs-lookup"><span data-stu-id="11b2d-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="11b2d-183">Controleer de toepasselijke rubrieken Hallo zoals eerder beschreven</span><span class="sxs-lookup"><span data-stu-id="11b2d-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="11b2d-184">Klik op Hallo 'SAS genereren'.</span><span class="sxs-lookup"><span data-stu-id="11b2d-184">Click hello "Generate SAS" button.</span></span>

![Afbeelding](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="11b2d-186">Kopiëren Hallo SAS gegenereerd in Hallo storageAccountSasToken veld; Hallo voorloopspaties vraagteken verwijderen ('? ').</span><span class="sxs-lookup"><span data-stu-id="11b2d-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="11b2d-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="11b2d-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="11b2d-188">Deze optionele secties bevatten aanvullende bestemmingen toowhich Hallo extensie stuurt Hallo-gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="11b2d-189">Hallo 'sink'-matrix bevat een object voor elke aanvullende gegevens sink.</span><span class="sxs-lookup"><span data-stu-id="11b2d-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="11b2d-190">Hallo bepaalt van kenmerk 'type' Hallo andere kenmerken in Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="11b2d-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="11b2d-191">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-191">Element</span></span> | <span data-ttu-id="11b2d-192">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-192">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-193">naam</span><span class="sxs-lookup"><span data-stu-id="11b2d-193">name</span></span> | <span data-ttu-id="11b2d-194">Een tekenreeks toorefer toothis sink elders in de configuratie van de uitbreiding Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="11b2d-195">type</span><span class="sxs-lookup"><span data-stu-id="11b2d-195">type</span></span> | <span data-ttu-id="11b2d-196">Hallo type sink wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-196">hello type of sink being defined.</span></span> <span data-ttu-id="11b2d-197">Hiermee bepaalt u andere waarden Hallo (indien aanwezig) in exemplaren van dit type.</span><span class="sxs-lookup"><span data-stu-id="11b2d-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="11b2d-198">Versie 3.0 Hallo Linux diagnostische uitbreiding ondersteunt twee typen van de sink: EventHub en JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="11b2d-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="11b2d-199">Hallo EventHub sink</span><span class="sxs-lookup"><span data-stu-id="11b2d-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="11b2d-200">Hallo 'sasURL' invoer bevat Hallo volledige URL, met inbegrip van SAS-token voor Hallo Event Hub toowhich gegevens moet worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="11b2d-201">LAD vereist een SAS naamgeving van een beleid waarmee Hallo verzenden claim.</span><span class="sxs-lookup"><span data-stu-id="11b2d-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="11b2d-202">Een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11b2d-202">An example:</span></span>

* <span data-ttu-id="11b2d-203">Een aangeroepen Event Hubs-naamruimte maken`contosohub`</span><span class="sxs-lookup"><span data-stu-id="11b2d-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="11b2d-204">Een Event Hub maken in de naamruimte van Hallo aangeroepen`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="11b2d-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="11b2d-205">Een gedeeld toegangsbeleid maken op Hallo Event Hub met de naam `writer` dat Hiermee Hallo claim verzenden</span><span class="sxs-lookup"><span data-stu-id="11b2d-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="11b2d-206">Als u hebt gemaakt een SAS goede tot middernacht UTC op 1 januari 2018, mogelijk Hallo sasURL waarde:</span><span class="sxs-lookup"><span data-stu-id="11b2d-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="11b2d-207">Zie voor meer informatie over het genereren van SAS-tokens voor Event Hubs [deze webpagina](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11b2d-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="11b2d-208">Hallo JsonBlob sink</span><span class="sxs-lookup"><span data-stu-id="11b2d-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="11b2d-209">Gegevens omgeleid tooa JsonBlob sink is opgeslagen in blobs in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="11b2d-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="11b2d-210">Elk exemplaar van LAD een blob elk uur wordt gemaakt voor elke naam sink.</span><span class="sxs-lookup"><span data-stu-id="11b2d-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="11b2d-211">Elke blob bevat altijd een ongeldige syntaxis JSON-matrix van object.</span><span class="sxs-lookup"><span data-stu-id="11b2d-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="11b2d-212">Nieuwe vermeldingen moment toohello matrix toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="11b2d-213">BLOBs worden opgeslagen in een container met dezelfde naam als sink Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="11b2d-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="11b2d-214">Hallo Azure storage-regels voor namen van de blob-containers toohello namen van JsonBlob put toepassen: tussen 3 en 63 kleine alfanumerieke ASCII-tekens of streepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="11b2d-215">Instellingen voor openbare</span><span class="sxs-lookup"><span data-stu-id="11b2d-215">Public settings</span></span>

<span data-ttu-id="11b2d-216">Deze structuur bevat verschillende blokken met instellingen die Hallo verzamelde Hallo-uitbreiding bepalen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="11b2d-217">Elke instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="11b2d-217">Each setting is optional.</span></span> <span data-ttu-id="11b2d-218">Als u opgeeft `ladCfg`, moet u ook opgeven `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="11b2d-219">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-219">Element</span></span> | <span data-ttu-id="11b2d-220">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-220">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="11b2d-221">StorageAccount</span></span> | <span data-ttu-id="11b2d-222">Hallo-naam van Hallo storage-account waarin gegevens worden geschreven door Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="11b2d-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="11b2d-223">Moet dezelfde naam, zoals is opgegeven in Hallo Hallo [beveiligde instellingen](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="11b2d-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="11b2d-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="11b2d-224">mdsdHttpProxy</span></span> | <span data-ttu-id="11b2d-225">(optioneel) Hetzelfde als in Hallo [beveiligde instellingen](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="11b2d-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="11b2d-226">Hallo openbare waarde wordt overschreven door persoonlijke Hallo-waarde als ingesteld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="11b2d-227">Proxyinstellingen met een geheim, zoals een wachtwoord, in Hallo plaatsen [beveiligde instellingen](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="11b2d-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="11b2d-228">Hallo resterende elementen zijn beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="11b2d-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="11b2d-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="11b2d-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="11b2d-230">Deze optionele structuur besturingselementen Hallo verzamelen van metrische gegevens en logboeken voor levering toohello Azure-service en tooother gegevens Put.</span><span class="sxs-lookup"><span data-stu-id="11b2d-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="11b2d-231">U moet ofwel opgeven `performanceCounters` of `syslogEvents` of beide.</span><span class="sxs-lookup"><span data-stu-id="11b2d-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="11b2d-232">U moet opgeven Hallo `metrics` structuur.</span><span class="sxs-lookup"><span data-stu-id="11b2d-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="11b2d-233">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-233">Element</span></span> | <span data-ttu-id="11b2d-234">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-234">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="11b2d-235">eventVolume</span></span> | <span data-ttu-id="11b2d-236">(optioneel) Besturingselementen Hallo aantal partities binnen Hallo opslag tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="11b2d-237">Moet een van `"Large"`, `"Medium"`, of `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="11b2d-238">Als niet wordt opgegeven, wordt de standaardwaarde Hallo `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="11b2d-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="11b2d-239">sampleRateInSeconds</span></span> | <span data-ttu-id="11b2d-240">(optioneel) Hallo standaardinterval tussen verzameling maatstaven voor onbewerkte (unaggregated).</span><span class="sxs-lookup"><span data-stu-id="11b2d-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="11b2d-241">Hallo kleinste ondersteund samplefrequentie is 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="11b2d-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="11b2d-242">Als niet wordt opgegeven, wordt de standaardwaarde Hallo `15`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="11b2d-243">metrics</span><span class="sxs-lookup"><span data-stu-id="11b2d-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="11b2d-244">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-244">Element</span></span> | <span data-ttu-id="11b2d-245">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-245">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="11b2d-246">resourceId</span></span> | <span data-ttu-id="11b2d-247">Hello Azure Resource Manager resource-ID van het Hallo VM of van virtuele-machineschaalset Hallo ingesteld toowhich Hallo die virtuele machine deel uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="11b2d-248">Deze instelling moet ook worden opgegeven als een JsonBlob sink is gebruikt in de Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="11b2d-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="11b2d-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="11b2d-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="11b2d-250">Hallo frequentie waarmee cumulatieve metrische gegevens toobe zijn berekend en tooAzure metrische gegevens, uitgedrukt als een tijdsinterval 8601 IS overgedragen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="11b2d-251">Hallo kleinste overdracht periode is 60 seconden, dat wil zeggen, PT1M.</span><span class="sxs-lookup"><span data-stu-id="11b2d-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="11b2d-252">U moet ten minste één scheduledTransferPeriod opgeven.</span><span class="sxs-lookup"><span data-stu-id="11b2d-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="11b2d-253">Voorbeelden van Hallo metrische gegevens die zijn opgegeven in Hallo performanceCounters sectie elke 15 seconden worden verzameld of op Hallo samplefrequentie expliciet is gedefinieerd voor Hallo teller.</span><span class="sxs-lookup"><span data-stu-id="11b2d-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="11b2d-254">Als meerdere scheduledTransferPeriod frequenties wordt weergegeven (zoals in Hallo voorbeeld), wordt elke aggregatie wordt afzonderlijk berekend.</span><span class="sxs-lookup"><span data-stu-id="11b2d-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="11b2d-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="11b2d-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="11b2d-256">Deze optionele sectie bepaalt Hallo-verzameling van metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="11b2d-257">Onbewerkte voorbeelden worden samengevoegd voor elk [scheduledTransferPeriod](#metrics) tooproduce deze waarden:</span><span class="sxs-lookup"><span data-stu-id="11b2d-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="11b2d-258">gemiddelde</span><span class="sxs-lookup"><span data-stu-id="11b2d-258">mean</span></span>
* <span data-ttu-id="11b2d-259">minimale</span><span class="sxs-lookup"><span data-stu-id="11b2d-259">minimum</span></span>
* <span data-ttu-id="11b2d-260">Maximum</span><span class="sxs-lookup"><span data-stu-id="11b2d-260">maximum</span></span>
* <span data-ttu-id="11b2d-261">laatste verzameld waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-261">last-collected value</span></span>
* <span data-ttu-id="11b2d-262">aantal steekproeven onbewerkte toocompute Hallo statistische functie gebruikt</span><span class="sxs-lookup"><span data-stu-id="11b2d-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="11b2d-263">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-263">Element</span></span> | <span data-ttu-id="11b2d-264">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-264">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-265">Put</span><span class="sxs-lookup"><span data-stu-id="11b2d-265">sinks</span></span> | <span data-ttu-id="11b2d-266">(optioneel) Een door komma's gescheiden lijst met namen van de sinks toowhich die LAD samengevoegde metrische resultaten verzendt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="11b2d-267">Alle samengevoegde metrische gegevens zijn gepubliceerde tooeach vermeld sink.</span><span class="sxs-lookup"><span data-stu-id="11b2d-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="11b2d-268">Zie [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="11b2d-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="11b2d-269">Voorbeeld: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="11b2d-270">type</span><span class="sxs-lookup"><span data-stu-id="11b2d-270">type</span></span> | <span data-ttu-id="11b2d-271">Werkelijke Hallo-provider van Hallo metriek identificeert.</span><span class="sxs-lookup"><span data-stu-id="11b2d-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="11b2d-272">Klasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-272">class</span></span> | <span data-ttu-id="11b2d-273">Identificeert samen met 'teller' hello specifieke metrische gegevens in de naamruimte Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="11b2d-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="11b2d-274">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-274">counter</span></span> | <span data-ttu-id="11b2d-275">Identificeert samen met 'class' hello specifieke metrische gegevens in de naamruimte Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="11b2d-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="11b2d-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="11b2d-276">counterSpecifier</span></span> | <span data-ttu-id="11b2d-277">Hallo specifieke metrische gegevens binnen hello Azure metrische gegevens naamruimte identificeert.</span><span class="sxs-lookup"><span data-stu-id="11b2d-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="11b2d-278">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-278">condition</span></span> | <span data-ttu-id="11b2d-279">(optioneel) Van toepassing selecteert een specifiek exemplaar van Hallo object toowhich Hallo metriek of selecteert Hallo aggregatie over alle exemplaren van dat object.</span><span class="sxs-lookup"><span data-stu-id="11b2d-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="11b2d-280">Zie voor meer informatie, Hallo [ `builtin` metrische definities](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="11b2d-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="11b2d-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="11b2d-281">sampleRate</span></span> | <span data-ttu-id="11b2d-282">IS 8601 interval dat ingesteld Hallo snelheid waarmee onbewerkte voorbeelden voor deze metrische gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="11b2d-283">Als niet is ingesteld, Hallo-interval voor gegevensverzameling is ingesteld door de waarde van Hallo [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="11b2d-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="11b2d-284">Hallo kortste ondersteunde-samplefrequentie is 15 seconden (PT15S).</span><span class="sxs-lookup"><span data-stu-id="11b2d-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="11b2d-285">eenheid</span><span class="sxs-lookup"><span data-stu-id="11b2d-285">unit</span></span> | <span data-ttu-id="11b2d-286">Moet een van deze tekenreeksen: 'Count', 'Bytes', 'Seconden', 'Percentage', 'CountPerSecond', 'BytesPerSecond', 'Milliseconde'.</span><span class="sxs-lookup"><span data-stu-id="11b2d-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="11b2d-287">Hallo-eenheid voor Hallo metriek definieert.</span><span class="sxs-lookup"><span data-stu-id="11b2d-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="11b2d-288">Gegevensgebruikers Hallo verzameld verwachten Hallo verzamelde gegevens waarden toomatch deze eenheid.</span><span class="sxs-lookup"><span data-stu-id="11b2d-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="11b2d-289">LAD negeert dit veld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-289">LAD ignores this field.</span></span>
<span data-ttu-id="11b2d-290">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="11b2d-290">displayName</span></span> | <span data-ttu-id="11b2d-291">Hallo label (in de taal Hallo Hallo gekoppeld landinstelling instellen) toobe gekoppeld toothis gegevens in Azure metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="11b2d-292">LAD negeert dit veld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-292">LAD ignores this field.</span></span>

<span data-ttu-id="11b2d-293">Hallo counterSpecifier is een identifier.</span><span class="sxs-lookup"><span data-stu-id="11b2d-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="11b2d-294">CounterSpecifier consumenten van metrische gegevens, zoals hello Azure portal voor grafieken en waarschuwingen van de functie, gebruiken als Hallo 'sleutel', waarmee een waarde of een exemplaar van een metriek.</span><span class="sxs-lookup"><span data-stu-id="11b2d-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="11b2d-295">Voor `builtin` metrische gegevens, wordt aangeraden gebruik van counterSpecifier-waarden die met beginnen `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="11b2d-296">Als u een specifiek exemplaar van een metriek verzamelt, raden wij dat u Hallo-id van Hallo exemplaar toohello counterSpecifier waarde koppelen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="11b2d-297">Enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="11b2d-297">Some examples:</span></span>

* <span data-ttu-id="11b2d-298">`/builtin/Processor/PercentIdleTime`-Niet-actieve tijd met een gemiddelde van alle kernen</span><span class="sxs-lookup"><span data-stu-id="11b2d-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="11b2d-299">`/builtin/Disk/FreeSpace(/mnt)`-Vrije ruimte voor Hallo mnt bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="11b2d-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="11b2d-300">`/builtin/Disk/FreeSpace`-Vrije ruimte met een gemiddelde van alle gekoppelde bestandssystemen</span><span class="sxs-lookup"><span data-stu-id="11b2d-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="11b2d-301">Verwacht Hallo counterSpecifier waarde toomatch een patroon LAD noch hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="11b2d-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="11b2d-302">In de manier waarop u counterSpecifier waarden samenstelt consistent zijn.</span><span class="sxs-lookup"><span data-stu-id="11b2d-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="11b2d-303">Wanneer u opgeeft `performanceCounters`, tooa gegevenstabel LAD altijd geschreven in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="11b2d-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="11b2d-304">U kunt hebben Hallo dezelfde gegevens die zijn geschreven tooJSON blobs en/of Event Hubs, maar u kunt opslag tooa gegevenstabel niet uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="11b2d-305">Alle exemplaren van Hallo diagnostische uitbreiding geconfigureerd toouse Hallo hetzelfde opslagaccount naam- en eindpunt toevoegen hun toohello metrische gegevens en Logboeken dezelfde tabel.</span><span class="sxs-lookup"><span data-stu-id="11b2d-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="11b2d-306">Als er te veel virtuele machines schrijft schrijft toohello partitie in dezelfde tabel, Azure kunt beperken toothat partitie.</span><span class="sxs-lookup"><span data-stu-id="11b2d-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="11b2d-307">Hallo eventVolume oorzaken vermeldingen toobe instelling verdeeld over 1 (klein), 10 (gemiddeld) of 100 (groot) verschillende partities.</span><span class="sxs-lookup"><span data-stu-id="11b2d-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="11b2d-308">'Gemiddeld' is meestal voldoende tooensure verkeer niet wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="11b2d-309">Hallo metrische gegevens voor Azure-functie van hello Azure-portal gebruikt Hallo-gegevens in deze tabel tooproduce grafieken of tootrigger waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="11b2d-310">Hallo-tabelnaam is Hallo samenvoeging van deze tekenreeksen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="11b2d-311">Hallo 'scheduledTransferPeriod' voor Hallo geaggregeerd waarden die zijn opgeslagen in de tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="11b2d-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="11b2d-312">Een datum in formulier Hallo 'JJJJMMDD", wijzigingen van elke 10 dagen</span><span class="sxs-lookup"><span data-stu-id="11b2d-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="11b2d-313">Voorbeelden zijn onder meer `WADMetricsPT1HP10DV2S20170410` en `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="11b2d-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="11b2d-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="11b2d-315">Deze optionele sectie bepaalt Hallo-verzameling van gebeurtenissen van syslog.</span><span class="sxs-lookup"><span data-stu-id="11b2d-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="11b2d-316">Als de sectie hello wordt weggelaten, worden helemaal syslog-gebeurtenissen niet vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="11b2d-317">Hallo syslogEventConfiguration verzameling heeft een vermelding voor elke syslog-faciliteit van belang.</span><span class="sxs-lookup"><span data-stu-id="11b2d-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="11b2d-318">Als minSeverity 'NONE' voor een bepaalde opslagruimte, of als faciliteit niet wordt weergegeven in het element Hallo helemaal, worden er zijn geen gebeurtenissen van de faciliteit vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="11b2d-319">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-319">Element</span></span> | <span data-ttu-id="11b2d-320">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-320">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-321">Put</span><span class="sxs-lookup"><span data-stu-id="11b2d-321">sinks</span></span> | <span data-ttu-id="11b2d-322">Een door komma's gescheiden lijst met namen van de sinks toowhich afzonderlijk logboek gebeurtenissen worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="11b2d-323">Alle gebeurtenissen die overeenkomt met de Hallo beperkingen in syslogEventConfiguration zijn gepubliceerde tooeach vermeld sink.</span><span class="sxs-lookup"><span data-stu-id="11b2d-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="11b2d-324">Voorbeeld: 'EHforsyslog'</span><span class="sxs-lookup"><span data-stu-id="11b2d-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="11b2d-325">voorziening %{facilityname/</span><span class="sxs-lookup"><span data-stu-id="11b2d-325">facilityName</span></span> | <span data-ttu-id="11b2d-326">De naam van een syslog-faciliteit (zoals ' logboek\_gebruiker ' of ' LOG\_LOCAL0 ').</span><span class="sxs-lookup"><span data-stu-id="11b2d-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="11b2d-327">Zie sectie van de Hallo 'faciliteit' Hallo [syslog man pagina](http://man7.org/linux/man-pages/man3/syslog.3.html) voor Hallo volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="11b2d-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="11b2d-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="11b2d-328">minSeverity</span></span> | <span data-ttu-id="11b2d-329">Een urgentieniveau syslog (zoals ' logboek\_fout ' of ' LOG\_INFO ').</span><span class="sxs-lookup"><span data-stu-id="11b2d-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="11b2d-330">Zie sectie van de Hallo 'niveau' Hallo [syslog man pagina](http://man7.org/linux/man-pages/man3/syslog.3.html) voor Hallo volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="11b2d-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="11b2d-331">Hallo-extensie bevat gebeurtenissen die worden verzonden toohello faciliteit op of boven Hallo opgegeven niveau.</span><span class="sxs-lookup"><span data-stu-id="11b2d-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="11b2d-332">Wanneer u opgeeft `syslogEvents`, tooa gegevenstabel LAD altijd geschreven in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="11b2d-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="11b2d-333">U kunt hebben Hallo dezelfde gegevens die zijn geschreven tooJSON blobs en/of Event Hubs, maar u kunt opslag tooa gegevenstabel niet uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="11b2d-334">Hallo partitioneren gedrag voor deze tabel wordt beschreven voor Hallo `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="11b2d-335">Hallo-tabelnaam is Hallo samenvoeging van deze tekenreeksen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="11b2d-336">Een datum in formulier Hallo 'JJJJMMDD", wijzigingen van elke 10 dagen</span><span class="sxs-lookup"><span data-stu-id="11b2d-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="11b2d-337">Voorbeelden zijn onder meer `LinuxSyslog20170410` en `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="11b2d-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="11b2d-338">perfCfg</span></span>

<span data-ttu-id="11b2d-339">Deze optionele sectie bepaalt de uitvoering van willekeurige [OMI](https://github.com/Microsoft/omi) query's.</span><span class="sxs-lookup"><span data-stu-id="11b2d-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="11b2d-340">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-340">Element</span></span> | <span data-ttu-id="11b2d-341">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-341">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-342">naamruimte</span><span class="sxs-lookup"><span data-stu-id="11b2d-342">namespace</span></span> | <span data-ttu-id="11b2d-343">(optioneel) Hallo OMI naamruimte in welke Hallo query moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="11b2d-344">Als u niets opgeeft, Hallo standaardwaarde is "root/scx', geïmplementeerd door Hallo [System Center platformoverschrijdende Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="11b2d-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="11b2d-345">query</span><span class="sxs-lookup"><span data-stu-id="11b2d-345">query</span></span> | <span data-ttu-id="11b2d-346">Hallo OMI query toobe uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="11b2d-347">Tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-347">table</span></span> | <span data-ttu-id="11b2d-348">(optioneel) hello Azure storage-tabel, in Hallo aangewezen storage-account (Zie [beveiligde instellingen](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="11b2d-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="11b2d-349">frequency</span><span class="sxs-lookup"><span data-stu-id="11b2d-349">frequency</span></span> | <span data-ttu-id="11b2d-350">(optioneel) Hallo aantal seconden tussen het uitvoeren van query Hallo.</span><span class="sxs-lookup"><span data-stu-id="11b2d-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="11b2d-351">Standaardwaarde is 300 (5 minuten); minimumwaarde is 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="11b2d-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="11b2d-352">Put</span><span class="sxs-lookup"><span data-stu-id="11b2d-352">sinks</span></span> | <span data-ttu-id="11b2d-353">(optioneel) Een door komma's gescheiden lijst met namen van aanvullende put toowhich onbewerkte metrische voorbeeldresultaten moet worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="11b2d-354">Er is geen aggregatie van deze voorbeelden onbewerkte wordt berekend door Hallo-extensie of Azure metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="11b2d-355">Een 'tabel' of 'sinks', of beide moeten worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="11b2d-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="11b2d-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="11b2d-356">fileLogs</span></span>

<span data-ttu-id="11b2d-357">Besturingselementen Hallo vastleggen van logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="11b2d-357">Controls hello capture of log files.</span></span> <span data-ttu-id="11b2d-358">LAD nieuwe tekstregels vastgelegd als ze zijn toohello bestand geschreven en schrijft deze tootable rijen en/of alle opgegeven Put (JsonBlob of EventHub).</span><span class="sxs-lookup"><span data-stu-id="11b2d-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="11b2d-359">Element</span><span class="sxs-lookup"><span data-stu-id="11b2d-359">Element</span></span> | <span data-ttu-id="11b2d-360">Waarde</span><span class="sxs-lookup"><span data-stu-id="11b2d-360">Value</span></span>
------- | -----
<span data-ttu-id="11b2d-361">Bestand</span><span class="sxs-lookup"><span data-stu-id="11b2d-361">file</span></span> | <span data-ttu-id="11b2d-362">volledige padnaam op Hallo van Hallo log-bestand toobe gecontroleerd en vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="11b2d-363">Hallo padnaam moet één bestand; de naam Deze kan niet de naam van een map of jokertekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="11b2d-364">Tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-364">table</span></span> | <span data-ttu-id="11b2d-365">(optioneel) hello Azure storage tabel in Hallo aangewezen opslag account (zoals opgegeven in configuratie Hallo beveiligd), in welke nieuwe lijnen van Hallo 'staart' Hallo-bestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="11b2d-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="11b2d-366">Put</span><span class="sxs-lookup"><span data-stu-id="11b2d-366">sinks</span></span> | <span data-ttu-id="11b2d-367">(optioneel) Een door komma's gescheiden lijst met namen van aanvullende put toowhich logboek regels verzonden.</span><span class="sxs-lookup"><span data-stu-id="11b2d-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="11b2d-368">Een 'tabel' of 'sinks', of beide moeten worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="11b2d-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="11b2d-369">Metrische gegevens die worden ondersteund door Hallo builtin provider</span><span class="sxs-lookup"><span data-stu-id="11b2d-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="11b2d-370">Hallo builtin metrische provider is een bron van de metrische gegevens meest interessante tooa uitgebreide set met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="11b2d-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="11b2d-371">Deze metrische gegevens kunnen worden onderverdeeld in vijf brede klassen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="11b2d-372">Processor</span><span class="sxs-lookup"><span data-stu-id="11b2d-372">Processor</span></span>
* <span data-ttu-id="11b2d-373">Geheugen</span><span class="sxs-lookup"><span data-stu-id="11b2d-373">Memory</span></span>
* <span data-ttu-id="11b2d-374">Netwerk</span><span class="sxs-lookup"><span data-stu-id="11b2d-374">Network</span></span>
* <span data-ttu-id="11b2d-375">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="11b2d-375">Filesystem</span></span>
* <span data-ttu-id="11b2d-376">Schijf</span><span class="sxs-lookup"><span data-stu-id="11b2d-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="11b2d-377">ingebouwde metrische gegevens voor Hallo Processor-klasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="11b2d-378">Hallo Processorklasse van metrische gegevens biedt informatie over het processorgebruik in Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="11b2d-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="11b2d-379">Bij het samenvoegen van percentages is Hallo resultaat Hallo gemiddelde over alle CPU's.</span><span class="sxs-lookup"><span data-stu-id="11b2d-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="11b2d-380">In een twee belangrijkste VM als één kern 100% bezig was en andere Hallo 100% niet-actief, Hallo gerapporteerd dat percentidletime zou dit 50.</span><span class="sxs-lookup"><span data-stu-id="11b2d-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="11b2d-381">Als elke core is 50% bezig voor Hallo dezelfde periode, Hallo gerapporteerde resultaat zou ook 50.</span><span class="sxs-lookup"><span data-stu-id="11b2d-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="11b2d-382">In een vier core VM, met één kern 100% bezet en Hallo andere niet-actief, Hallo gerapporteerd dat percentidletime 75 zou zijn.</span><span class="sxs-lookup"><span data-stu-id="11b2d-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="11b2d-383">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-383">counter</span></span> | <span data-ttu-id="11b2d-384">Betekenis</span><span class="sxs-lookup"><span data-stu-id="11b2d-384">Meaning</span></span>
------- | -------
<span data-ttu-id="11b2d-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-385">PercentIdleTime</span></span> | <span data-ttu-id="11b2d-386">Percentage tijd tijdens Hallo aggregatie venster dat processors zijn worden gebruikt voor het uitvoeren van niet-actieve Hallo kernel-lus</span><span class="sxs-lookup"><span data-stu-id="11b2d-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="11b2d-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-387">PercentProcessorTime</span></span> | <span data-ttu-id="11b2d-388">Percentage tijd dat een niet-actieve thread wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="11b2d-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="11b2d-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-389">PercentIOWaitTime</span></span> | <span data-ttu-id="11b2d-390">Percentage tijd wachten toocomplete voor i/o-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="11b2d-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="11b2d-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-391">PercentInterruptTime</span></span> | <span data-ttu-id="11b2d-392">Percentage tijd hardware/software-interrupts en DPC's (uitgestelde procedureaanroepen) wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="11b2d-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="11b2d-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-393">PercentUserTime</span></span> | <span data-ttu-id="11b2d-394">Niet-actieve tijd databaseprestaties aggregatie Hallo Hallo percentage tijd besteed aan in het dialoogvenster gebruiker meer met normale prioriteit</span><span class="sxs-lookup"><span data-stu-id="11b2d-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="11b2d-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-395">PercentNiceTime</span></span> | <span data-ttu-id="11b2d-396">Niet-actieve tijd Hallo percentages verlaagde (nice) prioriteit</span><span class="sxs-lookup"><span data-stu-id="11b2d-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="11b2d-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="11b2d-398">Niet-actieve tijd Hallo percentages in de beschermde (kernel) modus</span><span class="sxs-lookup"><span data-stu-id="11b2d-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="11b2d-399">Hallo moeten eerste vier items optellen too100%.</span><span class="sxs-lookup"><span data-stu-id="11b2d-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="11b2d-400">Hallo laatste prestatiemeteritems drie ook som too100%; ze Verdeel Hallo som van PercentProcessorTime PercentIOWaitTime en PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="11b2d-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="11b2d-401">instellen van een enkele metrische gegevens geaggregeerd tot alle processors tooobtain `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="11b2d-402">tooobtain een waarde voor een specifieke processor, zoals Hallo tweede logische processor van een vier VM, core ingesteld `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="11b2d-403">De logische processor-nummers zijn in Hallo bereik `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="11b2d-404">ingebouwde metrische gegevens voor Hallo geheugen-klasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="11b2d-405">Hallo geheugen klasse van metrische gegevens bevat informatie over geheugengebruik, paginering en wisselen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="11b2d-406">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-406">counter</span></span> | <span data-ttu-id="11b2d-407">Betekenis</span><span class="sxs-lookup"><span data-stu-id="11b2d-407">Meaning</span></span>
------- | -------
<span data-ttu-id="11b2d-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="11b2d-408">AvailableMemory</span></span> | <span data-ttu-id="11b2d-409">Beschikbaar fysiek geheugen in MiB</span><span class="sxs-lookup"><span data-stu-id="11b2d-409">Available physical memory in MiB</span></span>
<span data-ttu-id="11b2d-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="11b2d-410">PercentAvailableMemory</span></span> | <span data-ttu-id="11b2d-411">Beschikbaar fysiek geheugen als percentage van het totale geheugen</span><span class="sxs-lookup"><span data-stu-id="11b2d-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="11b2d-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="11b2d-412">UsedMemory</span></span> | <span data-ttu-id="11b2d-413">Gebruik fysiek geheugen (MiB)</span><span class="sxs-lookup"><span data-stu-id="11b2d-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="11b2d-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="11b2d-414">PercentUsedMemory</span></span> | <span data-ttu-id="11b2d-415">Fysiek geheugen in gebruik als een percentage van het totale geheugen</span><span class="sxs-lookup"><span data-stu-id="11b2d-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="11b2d-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="11b2d-416">PagesPerSec</span></span> | <span data-ttu-id="11b2d-417">Totaal aantal paginering (lezen/schrijven)</span><span class="sxs-lookup"><span data-stu-id="11b2d-417">Total paging (read/write)</span></span>
<span data-ttu-id="11b2d-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="11b2d-418">PagesReadPerSec</span></span> | <span data-ttu-id="11b2d-419">Pagina's lezen uit een back-up store (wisselbestand, programmabestand, toegewezen bestand, enz.)</span><span class="sxs-lookup"><span data-stu-id="11b2d-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="11b2d-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="11b2d-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="11b2d-421">Toobacking geschreven pagina's opslaan (wisselbestand, toegewezen bestand, enz.)</span><span class="sxs-lookup"><span data-stu-id="11b2d-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="11b2d-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="11b2d-422">AvailableSwap</span></span> | <span data-ttu-id="11b2d-423">Niet-gebruikte wisselruimte (MiB)</span><span class="sxs-lookup"><span data-stu-id="11b2d-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="11b2d-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="11b2d-424">PercentAvailableSwap</span></span> | <span data-ttu-id="11b2d-425">Niet-gebruikte wisselruimte als percentage van de totale wisselruimte</span><span class="sxs-lookup"><span data-stu-id="11b2d-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="11b2d-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="11b2d-426">UsedSwap</span></span> | <span data-ttu-id="11b2d-427">Gebruik wisselruimte (MiB)</span><span class="sxs-lookup"><span data-stu-id="11b2d-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="11b2d-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="11b2d-428">PercentUsedSwap</span></span> | <span data-ttu-id="11b2d-429">In gebruik wisselruimte als percentage van de totale wisselruimte</span><span class="sxs-lookup"><span data-stu-id="11b2d-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="11b2d-430">Deze klasse van metrische gegevens heeft slechts één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="11b2d-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="11b2d-431">Hallo 'voorwaarde'-kenmerk heeft geen nuttig instellingen en moet worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="11b2d-432">ingebouwde metrische gegevens voor Hallo netwerkklasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="11b2d-433">Hallo netwerkklasse van metrische gegevens bevat informatie over activiteit op het netwerk op een afzonderlijke netwerkinterfaces sinds het opstarten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="11b2d-434">LAD maakt geen metrische gegevens bandbreedte, die worden opgehaald van de host metrische gegevens beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="11b2d-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="11b2d-435">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-435">counter</span></span> | <span data-ttu-id="11b2d-436">Betekenis</span><span class="sxs-lookup"><span data-stu-id="11b2d-436">Meaning</span></span>
------- | -------
<span data-ttu-id="11b2d-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="11b2d-437">BytesTransmitted</span></span> | <span data-ttu-id="11b2d-438">Totaal aantal bytes dat is verzonden sinds het opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-438">Total bytes sent since boot</span></span>
<span data-ttu-id="11b2d-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="11b2d-439">BytesReceived</span></span> | <span data-ttu-id="11b2d-440">Totaal aantal bytes dat is ontvangen sinds het opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-440">Total bytes received since boot</span></span>
<span data-ttu-id="11b2d-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="11b2d-441">BytesTotal</span></span> | <span data-ttu-id="11b2d-442">Totaal aantal bytes verzonden of ontvangen sinds het opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="11b2d-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="11b2d-443">PacketsTransmitted</span></span> | <span data-ttu-id="11b2d-444">Totale aantal pakketten dat is verzonden sinds opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-444">Total packets sent since boot</span></span>
<span data-ttu-id="11b2d-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="11b2d-445">PacketsReceived</span></span> | <span data-ttu-id="11b2d-446">Totale aantal pakketten ontvangen sinds het opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-446">Total packets received since boot</span></span>
<span data-ttu-id="11b2d-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="11b2d-447">TotalRxErrors</span></span> | <span data-ttu-id="11b2d-448">Aantal ontvangen fouten sinds opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-448">Number of receive errors since boot</span></span>
<span data-ttu-id="11b2d-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="11b2d-449">TotalTxErrors</span></span> | <span data-ttu-id="11b2d-450">Aantal verzonden fouten sinds opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="11b2d-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="11b2d-451">TotalCollisions</span></span> | <span data-ttu-id="11b2d-452">Aantal conflicten die zijn gerapporteerd door Hallo netwerkpoorten sinds opstarten</span><span class="sxs-lookup"><span data-stu-id="11b2d-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="11b2d-453">Hoewel deze klasse wordt verwezen, is LAD ondersteunt geen vastleggen netwerk metrische gegevens die worden getotaliseerd over alle netwerkapparaten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="11b2d-454">Stel tooobtain Hallo metrische gegevens voor een specifieke interface, zoals eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="11b2d-455">ingebouwde metrische gegevens voor Hallo Filesystem-klasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="11b2d-456">Hallo Filesystem-klasse van metrische gegevens bevat informatie over het gebruik van het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="11b2d-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="11b2d-457">Absolute en het percentage waarden worden gerapporteerd als ze weergegeven tooan gewone gebruiker (geen hoofdmap worden zouden).</span><span class="sxs-lookup"><span data-stu-id="11b2d-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="11b2d-458">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-458">counter</span></span> | <span data-ttu-id="11b2d-459">Betekenis</span><span class="sxs-lookup"><span data-stu-id="11b2d-459">Meaning</span></span>
------- | -------
<span data-ttu-id="11b2d-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="11b2d-460">FreeSpace</span></span> | <span data-ttu-id="11b2d-461">Beschikbare schijfruimte in bytes</span><span class="sxs-lookup"><span data-stu-id="11b2d-461">Available disk space in bytes</span></span>
<span data-ttu-id="11b2d-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="11b2d-462">UsedSpace</span></span> | <span data-ttu-id="11b2d-463">Gebruikte schijfruimte in bytes</span><span class="sxs-lookup"><span data-stu-id="11b2d-463">Used disk space in bytes</span></span>
<span data-ttu-id="11b2d-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="11b2d-464">PercentFreeSpace</span></span> | <span data-ttu-id="11b2d-465">Percentage vrije ruimte</span><span class="sxs-lookup"><span data-stu-id="11b2d-465">Percentage free space</span></span>
<span data-ttu-id="11b2d-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="11b2d-466">PercentUsedSpace</span></span> | <span data-ttu-id="11b2d-467">Percentage gebruikte ruimte</span><span class="sxs-lookup"><span data-stu-id="11b2d-467">Percentage used space</span></span>
<span data-ttu-id="11b2d-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="11b2d-468">PercentFreeInodes</span></span> | <span data-ttu-id="11b2d-469">Percentage van de niet-gebruikte inodes</span><span class="sxs-lookup"><span data-stu-id="11b2d-469">Percentage of unused inodes</span></span>
<span data-ttu-id="11b2d-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="11b2d-470">PercentUsedInodes</span></span> | <span data-ttu-id="11b2d-471">Percentage van toegewezen (in gebruik) inodes getotaliseerd over alle bestandssystemen</span><span class="sxs-lookup"><span data-stu-id="11b2d-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="11b2d-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-472">BytesReadPerSecond</span></span> | <span data-ttu-id="11b2d-473">Gelezen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-473">Bytes read per second</span></span>
<span data-ttu-id="11b2d-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="11b2d-475">Bytes per seconde geschreven</span><span class="sxs-lookup"><span data-stu-id="11b2d-475">Bytes written per second</span></span>
<span data-ttu-id="11b2d-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-476">BytesPerSecond</span></span> | <span data-ttu-id="11b2d-477">Bytes lezen of schrijven per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-477">Bytes read or written per second</span></span>
<span data-ttu-id="11b2d-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-478">ReadsPerSecond</span></span> | <span data-ttu-id="11b2d-479">Leesbewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-479">Read operations per second</span></span>
<span data-ttu-id="11b2d-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-480">WritesPerSecond</span></span> | <span data-ttu-id="11b2d-481">Schrijfbewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-481">Write operations per second</span></span>
<span data-ttu-id="11b2d-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-482">TransfersPerSecond</span></span> | <span data-ttu-id="11b2d-483">Lees- of schrijfbewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-483">Read or write operations per second</span></span>

<span data-ttu-id="11b2d-484">Geaggregeerde waarden in alle bestandssystemen kunnen worden verkregen door het instellen van `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="11b2d-485">Waarden voor een specifieke gekoppelde bestandssysteem, zoals ' / mnt ', kan worden verkregen door het instellen van `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="11b2d-486">ingebouwde metrische gegevens voor Hallo schijf klasse</span><span class="sxs-lookup"><span data-stu-id="11b2d-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="11b2d-487">Hallo schijf klasse van metrische gegevens bevat informatie over schijfgebruik van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="11b2d-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="11b2d-488">Deze statistieken van toepassing toohello hele station.</span><span class="sxs-lookup"><span data-stu-id="11b2d-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="11b2d-489">Als er meerdere bestandssystemen op een apparaat, zijn Hallo tellers voor dat apparaat in feite getotaliseerd over alle mappen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="11b2d-490">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="11b2d-490">counter</span></span> | <span data-ttu-id="11b2d-491">Betekenis</span><span class="sxs-lookup"><span data-stu-id="11b2d-491">Meaning</span></span>
------- | -------
<span data-ttu-id="11b2d-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-492">ReadsPerSecond</span></span> | <span data-ttu-id="11b2d-493">Leesbewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-493">Read operations per second</span></span>
<span data-ttu-id="11b2d-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-494">WritesPerSecond</span></span> | <span data-ttu-id="11b2d-495">Schrijfbewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-495">Write operations per second</span></span>
<span data-ttu-id="11b2d-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-496">TransfersPerSecond</span></span> | <span data-ttu-id="11b2d-497">Totaal aantal bewerkingen per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-497">Total operations per second</span></span>
<span data-ttu-id="11b2d-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-498">AverageReadTime</span></span> | <span data-ttu-id="11b2d-499">Gemiddeld aantal seconden per leesbewerking</span><span class="sxs-lookup"><span data-stu-id="11b2d-499">Average seconds per read operation</span></span>
<span data-ttu-id="11b2d-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-500">AverageWriteTime</span></span> | <span data-ttu-id="11b2d-501">Gemiddeld aantal seconden per schrijfbewerking</span><span class="sxs-lookup"><span data-stu-id="11b2d-501">Average seconds per write operation</span></span>
<span data-ttu-id="11b2d-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="11b2d-502">AverageTransferTime</span></span> | <span data-ttu-id="11b2d-503">Gemiddeld aantal seconden per bewerking</span><span class="sxs-lookup"><span data-stu-id="11b2d-503">Average seconds per operation</span></span>
<span data-ttu-id="11b2d-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="11b2d-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="11b2d-505">Gemiddeld aantal bewerkingen in de wachtrij schijven</span><span class="sxs-lookup"><span data-stu-id="11b2d-505">Average number of queued disk operations</span></span>
<span data-ttu-id="11b2d-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="11b2d-507">Aantal gelezen bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-507">Number of bytes read per second</span></span>
<span data-ttu-id="11b2d-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="11b2d-509">Aantal bytes per seconde geschreven</span><span class="sxs-lookup"><span data-stu-id="11b2d-509">Number of bytes written per second</span></span>
<span data-ttu-id="11b2d-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="11b2d-510">BytesPerSecond</span></span> | <span data-ttu-id="11b2d-511">Aantal bytes gelezen of geschreven per seconde</span><span class="sxs-lookup"><span data-stu-id="11b2d-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="11b2d-512">Geaggregeerde waarden over alle schijven kunnen worden verkregen door het instellen van `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="11b2d-513">informatie voor een specifiek apparaat (bijvoorbeeld/dev/sdf1), tooget ingesteld `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="11b2d-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="11b2d-514">Installeren en configureren van LAD 3.0 via CLI</span><span class="sxs-lookup"><span data-stu-id="11b2d-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="11b2d-515">Ervan uitgaande dat uw beveiligde instellingen zijn in Hallo bestand PrivateConfig.json en uw openbare configuratiegegevens PublicConfig.json, deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="11b2d-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="11b2d-516">Hallo-opdracht wordt ervan uitgegaan dat u hello Azure Resource Management-modus (arm) van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="11b2d-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="11b2d-517">tooconfigure LAD voor de implementatie van het klassieke model (ASM) virtuele machines, te schakelen 'asm'-modus (`azure config mode asm`) en Hallo Resourcegroepnaam in Hallo opdracht weglaten.</span><span class="sxs-lookup"><span data-stu-id="11b2d-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="11b2d-518">Zie voor meer informatie, Hallo [platformoverschrijdende CLI documentatie](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="11b2d-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="11b2d-519">Een voorbeeldconfiguratie LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="11b2d-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="11b2d-520">Op basis van de voorgaande definities, hier van een configuratie voor uitbreiding LAD 3.0 voorbeeld met een verklaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="11b2d-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="11b2d-521">tooapply dit geval tooyour, u moet de naam van uw eigen opslagaccount gebruiken, account-SAS-token en EventHubs SAS-tokens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="11b2d-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="11b2d-522">PrivateConfig.json</span></span>

<span data-ttu-id="11b2d-523">Deze persoonlijke instellingen configureren:</span><span class="sxs-lookup"><span data-stu-id="11b2d-523">These private settings configure:</span></span>

* <span data-ttu-id="11b2d-524">een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="11b2d-524">a storage account</span></span>
* <span data-ttu-id="11b2d-525">een overeenkomende account-SAS-token</span><span class="sxs-lookup"><span data-stu-id="11b2d-525">a matching account SAS token</span></span>
* <span data-ttu-id="11b2d-526">verschillende Put (JsonBlob of EventHubs met SAS-tokens)</span><span class="sxs-lookup"><span data-stu-id="11b2d-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="11b2d-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="11b2d-527">PublicConfig.json</span></span>

<span data-ttu-id="11b2d-528">Deze instellingen voor openbare veroorzaken LAD naar:</span><span class="sxs-lookup"><span data-stu-id="11b2d-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="11b2d-529">Percentage processortijd en gebruikte schijfruimte metrische gegevens toohello uploaden `WADMetrics*` tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="11b2d-530">Uploaden van berichten van syslog-faciliteit 'gebruiker' en de ernst 'info' toohello `LinuxSyslog*` tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="11b2d-531">Uploaden van onbewerkte OMI query resultaten (PercentProcessorTime en PercentIdleTime) toohello met de naam `LinuxCPU` tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="11b2d-532">Toegevoegde regels in bestand uploaden `/var/log/myladtestlog` toohello `MyLadTestLog` tabel</span><span class="sxs-lookup"><span data-stu-id="11b2d-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="11b2d-533">In elk geval gegevens ook naar geüpload:</span><span class="sxs-lookup"><span data-stu-id="11b2d-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="11b2d-534">Azure Blob-opslag (containernaam is zoals gedefinieerd in Hallo JsonBlob sink)</span><span class="sxs-lookup"><span data-stu-id="11b2d-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="11b2d-535">EventHubs-eindpunt (zoals opgegeven in Hallo EventHubs sink)</span><span class="sxs-lookup"><span data-stu-id="11b2d-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="11b2d-536">Hallo `resourceId` Hallo configuratie overeenkomt met dat van Hallo VM of Hallo virtuele-machineschaalset ingesteld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="11b2d-537">Azure-platform metrische gegevens voor grafieken en waarschuwingen kent Hallo resourceId Hallo VM waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="11b2d-538">Deze verwacht toofind Hallo gegevens voor uw virtuele machine met behulp van Hallo resourceId Hallo zoeksleutel.</span><span class="sxs-lookup"><span data-stu-id="11b2d-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="11b2d-539">Als u Azure automatisch schalen, Hallo resourceId in Hallo automatisch schalen configuratie, moet overeenkomen met Hallo resourceId door LAD gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11b2d-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="11b2d-540">Hallo resourceId is ingebouwd in Hallo namen van JsonBlobs door LAD geschreven.</span><span class="sxs-lookup"><span data-stu-id="11b2d-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="11b2d-541">Bekijk uw gegevens</span><span class="sxs-lookup"><span data-stu-id="11b2d-541">View your data</span></span>

<span data-ttu-id="11b2d-542">Prestatiegegevens van de Azure portal tooview hello gebruiken of waarschuwingen instellen:</span><span class="sxs-lookup"><span data-stu-id="11b2d-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![Afbeelding](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="11b2d-544">Hallo `performanceCounters` gegevens altijd worden opgeslagen in een tabel met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="11b2d-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="11b2d-545">Azure Storage-API's zijn beschikbaar voor veel talen en platforms.</span><span class="sxs-lookup"><span data-stu-id="11b2d-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="11b2d-546">Gegevens die worden verzonden tooJsonBlob put wordt opgeslagen in blobs in Hallo storage-account met de naam in Hallo [beveiligde instellingen](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="11b2d-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="11b2d-547">U kunt Hallo blob-gegevens met behulp van een Azure Blob Storage-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="11b2d-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="11b2d-548">Bovendien kunt u deze gebruikersinterface extra tooaccess Hallo gegevens in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="11b2d-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="11b2d-549">Visual Studio Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="11b2d-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="11b2d-550">[Microsoft Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/ "Azure Opslagverkenner").</span><span class="sxs-lookup"><span data-stu-id="11b2d-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="11b2d-551">Deze momentopname van een sessie van Microsoft Azure Storage Explorer toont hello Azure Storage-tabellen en containers gegenereerd vanuit een juist geconfigureerde LAD 3.0-extensie op een virtuele testmachine.</span><span class="sxs-lookup"><span data-stu-id="11b2d-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="11b2d-552">Hallo installatiekopie komt niet overeen met exact met Hallo [LAD 3.0 voorbeeldconfiguratie](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="11b2d-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Afbeelding](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="11b2d-554">Zie de relevante Hallo [EventHubs-documentatie](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn hoe tooconsume berichten tooan EventHubs eindpunt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="11b2d-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11b2d-555">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11b2d-555">Next steps</span></span>

* <span data-ttu-id="11b2d-556">Maken van metrische waarschuwingen in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) van Hallo metrische gegevens die u hebt verzameld.</span><span class="sxs-lookup"><span data-stu-id="11b2d-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="11b2d-557">Maak [grafieken bewaking](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) voor uw metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11b2d-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="11b2d-558">Meer informatie over hoe te[maken van een virtuele-machineschaalset](/azure/virtual-machines/linux/tutorial-create-vmss) met behulp van de metrische gegevens toocontrol automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="11b2d-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
