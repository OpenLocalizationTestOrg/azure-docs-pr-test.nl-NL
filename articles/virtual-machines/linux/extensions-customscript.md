---
title: aangepaste scripts aaaRun op Linux VM's in Azure | Microsoft Docs
description: Configuratietaken voor Linux-VM automatiseren met behulp van aangepaste Scriptextensie Hallo
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="1b85a-103">Hello Azure-extensie voor aangepaste scripts gebruiken met Linux virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="1b85a-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="1b85a-104">Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b85a-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="1b85a-105">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="1b85a-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="1b85a-106">Scripts kunnen worden gedownload van Azure storage of andere toegankelijke internetlocatie, of toohello extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="1b85a-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="1b85a-107">Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.</span><span class="sxs-lookup"><span data-stu-id="1b85a-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="1b85a-108">De Documentdetails van dit hoe toouse aangepaste Scriptextensie van Hallo hello Azure CLI en een Azure Resource Manager-sjabloon en details stappen voor probleemoplossing in Linux-systemen.</span><span class="sxs-lookup"><span data-stu-id="1b85a-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="1b85a-109">Configuratie voor uitbreiding</span><span class="sxs-lookup"><span data-stu-id="1b85a-109">Extension Configuration</span></span>
<span data-ttu-id="1b85a-110">configuratie van de aangepaste Scriptextensie Hallo geeft bijvoorbeeld de locatie van script en Hallo opdracht toobe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1b85a-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="1b85a-111">Deze configuratie kan worden opgeslagen in de configuratiebestanden, op Hallo vanaf de opdrachtregel of in een Azure Resource Manager-sjabloon opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b85a-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="1b85a-112">Gevoelige gegevens kunnen worden opgeslagen in een beveiligde configuratie die is versleuteld en worden alleen ontsleuteld in Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1b85a-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="1b85a-113">Hallo is beveiligde handig wanneer Hallo uitvoering opdracht geheimen zoals een wachtwoord bevat.</span><span class="sxs-lookup"><span data-stu-id="1b85a-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="1b85a-114">De openbare configuratie</span><span class="sxs-lookup"><span data-stu-id="1b85a-114">Public Configuration</span></span>
<span data-ttu-id="1b85a-115">Schema:</span><span class="sxs-lookup"><span data-stu-id="1b85a-115">Schema:</span></span>

<span data-ttu-id="1b85a-116">**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="1b85a-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="1b85a-117">Hallo-namen gebruiken, zoals hieronder tooavoid implementatieproblemen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b85a-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="1b85a-118">**commandToExecute**: (vereist, string) vermelding punt script tooexecute Hallo</span><span class="sxs-lookup"><span data-stu-id="1b85a-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="1b85a-119">**fileUris**: (optioneel, string array) Hallo-URL's voor bestanden toobe gedownload.</span><span class="sxs-lookup"><span data-stu-id="1b85a-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="1b85a-120">**tijdstempel** (optioneel, geheel getal) dit veld alleen tootrigger een opnieuw uitvoeren van script hello gebruiken door de waarde van dit veld te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1b85a-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="1b85a-121">Beveiligde configuratie</span><span class="sxs-lookup"><span data-stu-id="1b85a-121">Protected Configuration</span></span>
<span data-ttu-id="1b85a-122">Schema:</span><span class="sxs-lookup"><span data-stu-id="1b85a-122">Schema:</span></span>

<span data-ttu-id="1b85a-123">**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="1b85a-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="1b85a-124">Hallo-namen gebruiken, zoals hieronder tooavoid implementatieproblemen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b85a-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="1b85a-125">**commandToExecute**: (optioneel, string) vermelding punt script tooexecute Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b85a-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="1b85a-126">Dit veld in plaats daarvan gebruiken als uw opdracht geheimen zoals wachtwoorden bevat.</span><span class="sxs-lookup"><span data-stu-id="1b85a-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="1b85a-127">**storageAccountName**: (optioneel, string) Hallo-naam van de storage-account.</span><span class="sxs-lookup"><span data-stu-id="1b85a-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="1b85a-128">Als u de storage-referenties opgeeft, moet alle fileUris URL's voor Azure Blobs.</span><span class="sxs-lookup"><span data-stu-id="1b85a-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="1b85a-129">**storageAccountKey**: (optioneel, string) Hallo toegangssleutel van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1b85a-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="1b85a-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b85a-130">Azure CLI</span></span>
<span data-ttu-id="1b85a-131">Wanneer u hello Azure CLI toorun Hallo extensie voor aangepaste scripts, een configuratiebestand of bestanden met minimale Hallo bestands-uri en Hallo uitvoering scriptopdracht maken.</span><span class="sxs-lookup"><span data-stu-id="1b85a-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="1b85a-132">Hallo-instellingen kunnen eventueel worden opgegeven in Hallo opdracht als een tekenreeks JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1b85a-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="1b85a-133">Hierdoor Hallo configuratie toobe tijdens de uitvoering en zonder een afzonderlijk configuratiebestand opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b85a-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="1b85a-134">Voorbeelden van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b85a-134">Azure CLI Examples</span></span>

<span data-ttu-id="1b85a-135">**Voorbeeld 1** -openbare configuratie met een scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="1b85a-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="1b85a-136">Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1b85a-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="1b85a-137">**Voorbeeld 2** -openbare configuratie zonder script een bestand.</span><span class="sxs-lookup"><span data-stu-id="1b85a-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="1b85a-138">Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1b85a-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="1b85a-139">**Voorbeeld 3** - een openbare-configuratiebestand is gebruikte toospecify Hallo-scriptbestand URI en een beveiligde configuratiebestand is gebruikte toospecify Hallo opdracht toobe uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1b85a-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="1b85a-140">De openbare configuratie voor bestand:</span><span class="sxs-lookup"><span data-stu-id="1b85a-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="1b85a-141">Beveiligde configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="1b85a-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="1b85a-142">Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1b85a-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="1b85a-143">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="1b85a-143">Resource Manager Template</span></span>
<span data-ttu-id="1b85a-144">Hello Azure-extensie voor aangepaste scripts kan worden uitgevoerd tijdens de virtuele Machine implementatie met een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1b85a-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="1b85a-145">toodo toevoegen dus juist opgemaakte JSON toohello-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="1b85a-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="1b85a-146">Voorbeelden van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b85a-146">Resource Manager Examples</span></span>
<span data-ttu-id="1b85a-147">**Voorbeeld 1** -openbare configuratie.</span><span class="sxs-lookup"><span data-stu-id="1b85a-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="1b85a-148">**Voorbeeld 2** -opdracht kan worden uitgevoerd in beveiligde configuratie.</span><span class="sxs-lookup"><span data-stu-id="1b85a-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="1b85a-149">Zie Hallo .net Core muziek Store Demo voor een compleet voorbeeld - [muziek Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="1b85a-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1b85a-150">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="1b85a-150">Troubleshooting</span></span>
<span data-ttu-id="1b85a-151">Wanneer Hallo aangepaste Scriptextensie wordt uitgevoerd, wordt de Hallo script gemaakt of gedownload naar een map vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="1b85a-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="1b85a-152">Hallo-opdrachtuitvoer wordt ook opgeslagen in deze map in `stdout` en `stderr` bestand.</span><span class="sxs-lookup"><span data-stu-id="1b85a-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="1b85a-153">Hello Azure Scriptextensie produceert een logboek u hier vindt.</span><span class="sxs-lookup"><span data-stu-id="1b85a-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="1b85a-154">de uitvoeringsstatus Hallo Hallo aangepaste Scriptextensie kan ook worden opgehaald met hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1b85a-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="1b85a-155">Hallo-uitvoer ziet er Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="1b85a-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="1b85a-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b85a-156">Next Steps</span></span>
<span data-ttu-id="1b85a-157">Zie voor meer informatie over andere VM-extensies voor Script [overzicht van de uitbreiding van de Azure-Script voor Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b85a-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

