---
title: De extensie Azure aangepaste scripts voor Windows | Microsoft Docs
description: Configuratietaken voor Windows-VM automatiseren met behulp van de aangepaste scriptextensie
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: a6f417ea6575b81258998ae3b31c10e9df59b603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="cca0f-103">Extensie voor aangepaste scripts voor Windows</span><span class="sxs-lookup"><span data-stu-id="cca0f-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="cca0f-104">De aangepaste Scriptextensie downloads en scripts op virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cca0f-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="cca0f-105">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="cca0f-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="cca0f-106">Scripts kunnen worden gedownload van Azure storage of GitHub, of naar de Azure portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="cca0f-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="cca0f-107">De aangepaste scriptextensie kan worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met de Azure CLI, PowerShell, Azure-portal of de REST-API van Azure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="cca0f-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="cca0f-108">Dit document details over het gebruik van de aangepaste Scriptextensie met behulp van de Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="cca0f-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cca0f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cca0f-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="cca0f-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="cca0f-110">Operating System</span></span>

<span data-ttu-id="cca0f-111">De aangepaste Scriptextensie versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="cca0f-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="cca0f-112">De locatie van script</span><span class="sxs-lookup"><span data-stu-id="cca0f-112">Script Location</span></span>

<span data-ttu-id="cca0f-113">Het script moet worden opgeslagen in Azure Blob-opslag of een andere locatie die toegankelijk zijn via een geldige URL.</span><span class="sxs-lookup"><span data-stu-id="cca0f-113">The script needs to be stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="cca0f-114">Verbinding met Internet</span><span class="sxs-lookup"><span data-stu-id="cca0f-114">Internet Connectivity</span></span>

<span data-ttu-id="cca0f-115">De aangepaste Script uitbreiding voor Windows is vereist dat de virtuele doelmachine is verbonden met internet.</span><span class="sxs-lookup"><span data-stu-id="cca0f-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="cca0f-116">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="cca0f-116">Extension schema</span></span>

<span data-ttu-id="cca0f-117">De volgende JSON geeft het schema voor de aangepaste Scriptextensie.</span><span class="sxs-lookup"><span data-stu-id="cca0f-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="cca0f-118">De extensie is vereist voor de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cca0f-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="cca0f-119">Als u Azure-opslag gebruikt als de scriptbron, wordt een Azure storage-account en -account sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="cca0f-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="cca0f-120">Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in de configuratie van de instelling voor beveiligde uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="cca0f-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="cca0f-121">Azure VM-extensie beveiligde instellingsgegevens is versleuteld en alleen op de virtuele doelmachine worden ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="cca0f-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="cca0f-122">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="cca0f-122">Property values</span></span>

| <span data-ttu-id="cca0f-123">Naam</span><span class="sxs-lookup"><span data-stu-id="cca0f-123">Name</span></span> | <span data-ttu-id="cca0f-124">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cca0f-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="cca0f-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="cca0f-125">apiVersion</span></span> | <span data-ttu-id="cca0f-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="cca0f-126">2015-06-15</span></span> |
| <span data-ttu-id="cca0f-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="cca0f-127">publisher</span></span> | <span data-ttu-id="cca0f-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="cca0f-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="cca0f-129">type</span><span class="sxs-lookup"><span data-stu-id="cca0f-129">type</span></span> | <span data-ttu-id="cca0f-130">Uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="cca0f-130">extensions</span></span> |
| <span data-ttu-id="cca0f-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="cca0f-131">typeHandlerVersion</span></span> | <span data-ttu-id="cca0f-132">1.9</span><span class="sxs-lookup"><span data-stu-id="cca0f-132">1.9</span></span> |
| <span data-ttu-id="cca0f-133">fileUris (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="cca0f-133">fileUris (e.g)</span></span> | <span data-ttu-id="cca0f-134">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="cca0f-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="cca0f-135">commandToExecute (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="cca0f-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="cca0f-136">PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1</span><span class="sxs-lookup"><span data-stu-id="cca0f-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="cca0f-137">storageAccountName (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="cca0f-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="cca0f-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="cca0f-138">examplestorageacct</span></span> |
| <span data-ttu-id="cca0f-139">storageAccountKey (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="cca0f-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="cca0f-140">TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg ==</span><span class="sxs-lookup"><span data-stu-id="cca0f-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="cca0f-141">**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="cca0f-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="cca0f-142">Gebruik de namen zoals hierboven om te voorkomen dat problemen bij de implementatie.</span><span class="sxs-lookup"><span data-stu-id="cca0f-142">Use the names as seen above to avoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="cca0f-143">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="cca0f-143">Template deployment</span></span>

<span data-ttu-id="cca0f-144">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="cca0f-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="cca0f-145">De JSON-schema in de vorige sectie wordt beschreven, kan de aangepaste Scriptextensie uitvoeren tijdens de sjabloonimplementatie van een Azure Resource Manager-in een Azure Resource Manager-sjabloon worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cca0f-145">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="cca0f-146">Een voorbeeldsjabloon met de aangepaste Scriptextensie vindt u hier, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="cca0f-146">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="cca0f-147">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="cca0f-147">PowerShell deployment</span></span>

<span data-ttu-id="cca0f-148">De `Set-AzureRmVMCustomScriptExtension` opdracht kan worden gebruikt voor de extensie voor aangepaste scripts toevoegen aan een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cca0f-148">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="cca0f-149">Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="cca0f-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="cca0f-150">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="cca0f-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="cca0f-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cca0f-151">Troubleshoot</span></span>

<span data-ttu-id="cca0f-152">Gegevens over de status van extensie-implementaties kunnen worden opgehaald uit de Azure portal en met behulp van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="cca0f-152">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="cca0f-153">Overzicht van de implementatiestatus van uitbreidingen voor een bepaalde virtuele machine, voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="cca0f-153">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="cca0f-154">De uitvoer van de extensie-uitvoering is geregistreerd in bestanden gevonden in de volgende map op de virtuele doelmachine.</span><span class="sxs-lookup"><span data-stu-id="cca0f-154">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="cca0f-155">De opgegeven bestanden zijn gedownload naar de volgende map op de virtuele doelmachine.</span><span class="sxs-lookup"><span data-stu-id="cca0f-155">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="cca0f-156">waar `<n>` is een decimal integer die tussen uitvoeringen van de uitbreiding mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cca0f-156">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="cca0f-157">De `1.*` waarde komt overeen met de werkelijke, huidige `typeHandlerVersion` waarde van de extensie.</span><span class="sxs-lookup"><span data-stu-id="cca0f-157">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="cca0f-158">Bijvoorbeeld: de werkelijke map kan niet `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="cca0f-158">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="cca0f-159">Bij het uitvoeren van de `commandToExecute` opdracht, de uitbreiding voor deze map hebt ingesteld (bijvoorbeeld `...\Downloads\2`) als de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="cca0f-159">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="cca0f-160">Dit maakt het gebruik van relatieve paden te vinden van de bestanden gedownload de `fileURIs` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cca0f-160">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="cca0f-161">Zie de onderstaande tabel voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="cca0f-161">See the table below for examples.</span></span>

<span data-ttu-id="cca0f-162">Omdat het absolute downloadpad na verloop van tijd variëren kan, is het beter om te kiezen voor relatieve scriptbestand paden in de `commandToExecute` tekenreeks, indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="cca0f-162">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="cca0f-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cca0f-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="cca0f-164">Informatie over het pad na het eerste segment van de URI wordt bewaard voor bestanden die worden gedownload de `fileUris` eigenschappenlijst.</span><span class="sxs-lookup"><span data-stu-id="cca0f-164">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="cca0f-165">Zoals u in de onderstaande tabel, gedownloade bestanden zijn toegewezen in submappen downloaden in overeenstemming met de structuur van de `fileUris` waarden.</span><span class="sxs-lookup"><span data-stu-id="cca0f-165">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="cca0f-166">Voorbeelden van gedownloade bestanden</span><span class="sxs-lookup"><span data-stu-id="cca0f-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="cca0f-167">URI in fileUris</span><span class="sxs-lookup"><span data-stu-id="cca0f-167">URI in fileUris</span></span> | <span data-ttu-id="cca0f-168">Relatieve locatie voor gedownloade</span><span class="sxs-lookup"><span data-stu-id="cca0f-168">Relative downloaded location</span></span> | <span data-ttu-id="cca0f-169">Absolute locatie gedownload *</span><span class="sxs-lookup"><span data-stu-id="cca0f-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="cca0f-170">\*Als verandert hierboven, de absolute paden gedurende de levensduur van de virtuele machine, maar niet binnen één uitvoering van de extensie CustomScript.</span><span class="sxs-lookup"><span data-stu-id="cca0f-170">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="cca0f-171">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="cca0f-171">Support</span></span>

<span data-ttu-id="cca0f-172">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts in de [MSDN Azure en Stack Overflow forums] raadplegen (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="cca0f-172">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="cca0f-173">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="cca0f-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="cca0f-174">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="cca0f-174">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="cca0f-175">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="cca0f-175">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
