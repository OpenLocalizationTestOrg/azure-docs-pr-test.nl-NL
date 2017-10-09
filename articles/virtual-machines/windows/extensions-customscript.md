---
title: aaaAzure aangepast Script uitbreiding voor Windows | Microsoft Docs
description: Configuratietaken voor Windows-VM automatiseren met behulp van Hallo aangepaste scriptextensie
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
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="81ee7-103">Extensie voor aangepaste scripts voor Windows</span><span class="sxs-lookup"><span data-stu-id="81ee7-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="81ee7-104">Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="81ee7-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="81ee7-105">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="81ee7-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="81ee7-106">Scripts kunnen worden gedownload van Azure storage of GitHub, of toohello Azure-portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="81ee7-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="81ee7-107">Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.</span><span class="sxs-lookup"><span data-stu-id="81ee7-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="81ee7-108">Dit document beschrijft hoe toouse Hallo extensie voor aangepaste scripts gebruiken hello Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="81ee7-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ee7-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81ee7-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="81ee7-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="81ee7-110">Operating System</span></span>

<span data-ttu-id="81ee7-111">Hallo-extensie voor aangepaste scripts voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016 versies.</span><span class="sxs-lookup"><span data-stu-id="81ee7-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="81ee7-112">De locatie van script</span><span class="sxs-lookup"><span data-stu-id="81ee7-112">Script Location</span></span>

<span data-ttu-id="81ee7-113">Hallo script moet toobe opgeslagen in Azure Blob-opslag of een andere locatie die toegankelijk zijn via een geldige URL.</span><span class="sxs-lookup"><span data-stu-id="81ee7-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="81ee7-114">Verbinding met Internet</span><span class="sxs-lookup"><span data-stu-id="81ee7-114">Internet Connectivity</span></span>

<span data-ttu-id="81ee7-115">Hallo aangepast Script uitbreiding voor Windows is vereist dat Hallo doel-virtuele machine is verbonden toohello internet.</span><span class="sxs-lookup"><span data-stu-id="81ee7-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="81ee7-116">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="81ee7-116">Extension schema</span></span>

<span data-ttu-id="81ee7-117">Hallo toont volgende JSON Hallo-schema voor de aangepaste Scriptextensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="81ee7-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="81ee7-118">Hallo-uitbreiding vereist de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht tooexecute.</span><span class="sxs-lookup"><span data-stu-id="81ee7-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="81ee7-119">Een Azure storage-account en -account sleutel is vereist als voor informatie over het gebruik van Azure Storage als Hallo van de scriptbron.</span><span class="sxs-lookup"><span data-stu-id="81ee7-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="81ee7-120">Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in configuratie van de beveiligde instelling Hallo-extensies.</span><span class="sxs-lookup"><span data-stu-id="81ee7-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="81ee7-121">Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="81ee7-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="81ee7-122">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="81ee7-122">Property values</span></span>

| <span data-ttu-id="81ee7-123">Naam</span><span class="sxs-lookup"><span data-stu-id="81ee7-123">Name</span></span> | <span data-ttu-id="81ee7-124">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="81ee7-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="81ee7-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ee7-125">apiVersion</span></span> | <span data-ttu-id="81ee7-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="81ee7-126">2015-06-15</span></span> |
| <span data-ttu-id="81ee7-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="81ee7-127">publisher</span></span> | <span data-ttu-id="81ee7-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="81ee7-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="81ee7-129">type</span><span class="sxs-lookup"><span data-stu-id="81ee7-129">type</span></span> | <span data-ttu-id="81ee7-130">Uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="81ee7-130">extensions</span></span> |
| <span data-ttu-id="81ee7-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="81ee7-131">typeHandlerVersion</span></span> | <span data-ttu-id="81ee7-132">1.9</span><span class="sxs-lookup"><span data-stu-id="81ee7-132">1.9</span></span> |
| <span data-ttu-id="81ee7-133">fileUris (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="81ee7-133">fileUris (e.g)</span></span> | <span data-ttu-id="81ee7-134">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="81ee7-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="81ee7-135">commandToExecute (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="81ee7-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="81ee7-136">PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1</span><span class="sxs-lookup"><span data-stu-id="81ee7-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="81ee7-137">storageAccountName (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="81ee7-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="81ee7-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="81ee7-138">examplestorageacct</span></span> |
| <span data-ttu-id="81ee7-139">storageAccountKey (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="81ee7-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="81ee7-140">TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg ==</span><span class="sxs-lookup"><span data-stu-id="81ee7-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="81ee7-141">**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="81ee7-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="81ee7-142">Hallo namen gebruiken zoals hierboven tooavoid implementatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="81ee7-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="81ee7-143">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="81ee7-143">Template deployment</span></span>

<span data-ttu-id="81ee7-144">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="81ee7-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="81ee7-145">Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo aangepaste Scriptextensie tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="81ee7-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="81ee7-146">Een voorbeeldsjabloon waarin de aangepaste Scriptextensie u hier vindt, Hallo [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="81ee7-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="81ee7-147">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="81ee7-147">PowerShell deployment</span></span>

<span data-ttu-id="81ee7-148">Hallo `Set-AzureRmVMCustomScriptExtension` opdracht gebruikte tooadd Hallo aangepast Script extensie tooan bestaande virtuele machine kan worden.</span><span class="sxs-lookup"><span data-stu-id="81ee7-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="81ee7-149">Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="81ee7-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="81ee7-150">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="81ee7-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="81ee7-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="81ee7-151">Troubleshoot</span></span>

<span data-ttu-id="81ee7-152">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="81ee7-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="81ee7-153">Hallo Implementatiestatus toosee van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="81ee7-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="81ee7-154">Uitvoering van de extensie uitvoer geregistreerde toofiles gevonden onder Hallo volgt directory op Hallo doel-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="81ee7-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="81ee7-155">Hallo opgegeven bestanden zijn gedownload naar de volgende map op de virtuele doelmachine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="81ee7-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="81ee7-156">waar `<n>` is een decimal integer die kan worden gewijzigd tussen uitvoeringen van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="81ee7-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="81ee7-157">Hallo `1.*` waarde overeenkomt met de werkelijke, huidige Hallo `typeHandlerVersion` waarde van de Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="81ee7-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="81ee7-158">Hallo werkelijke directory kan bijvoorbeeld `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="81ee7-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="81ee7-159">Bij het uitvoeren van Hallo `commandToExecute` opdracht Hallo extensie deze map hebt ingesteld (bijvoorbeeld `...\Downloads\2`) als de huidige werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="81ee7-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="81ee7-160">Dit kunnen Hallo-gebruik van relatieve paden toolocate Hallo bestanden gedownload via Hallo `fileURIs` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="81ee7-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="81ee7-161">Zie onderstaande Hallo tabel voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="81ee7-161">See hello table below for examples.</span></span>

<span data-ttu-id="81ee7-162">Omdat Hallo absolute downloadpad na verloop van tijd verschillen kan, is het beter tooopt voor relatieve scriptbestand paden in Hallo `commandToExecute` tekenreeks, indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="81ee7-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="81ee7-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="81ee7-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="81ee7-164">Informatie over het pad na eerste Hallo-URI-segment wordt bewaard voor bestanden gedownload via Hallo `fileUris` eigenschappenlijst.</span><span class="sxs-lookup"><span data-stu-id="81ee7-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="81ee7-165">Zoals u in onderstaande tabel voor hello, gedownloade bestanden zijn toegewezen in downloaden submappen tooreflect Hallo structuur Hallo `fileUris` waarden.</span><span class="sxs-lookup"><span data-stu-id="81ee7-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="81ee7-166">Voorbeelden van gedownloade bestanden</span><span class="sxs-lookup"><span data-stu-id="81ee7-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="81ee7-167">URI in fileUris</span><span class="sxs-lookup"><span data-stu-id="81ee7-167">URI in fileUris</span></span> | <span data-ttu-id="81ee7-168">Relatieve locatie voor gedownloade</span><span class="sxs-lookup"><span data-stu-id="81ee7-168">Relative downloaded location</span></span> | <span data-ttu-id="81ee7-169">Absolute locatie gedownload *</span><span class="sxs-lookup"><span data-stu-id="81ee7-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="81ee7-170">\*Als verandert hierboven, Hallo absolute mappaden gedurende de levensduur Hallo Hallo VM, maar niet binnen één uitvoering van de extensie CustomScript Hallo.</span><span class="sxs-lookup"><span data-stu-id="81ee7-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="81ee7-171">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="81ee7-171">Support</span></span>

<span data-ttu-id="81ee7-172">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="81ee7-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="81ee7-173">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="81ee7-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="81ee7-174">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="81ee7-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="81ee7-175">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="81ee7-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
