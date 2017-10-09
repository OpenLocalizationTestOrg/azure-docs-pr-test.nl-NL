---
title: aaaCustom scriptextensie op een virtuele machine van Windows | Microsoft Docs
description: Virtuele machine van Azure-configuratietaken automatiseren met behulp van Hallo aangepast Script extensie toorun PowerShell-scripts op een externe Windows-VM
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="f864d-103">Aangepast Script uitbreiding voor Windows met het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="f864d-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f864d-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f864d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f864d-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f864d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f864d-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f864d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f864d-107">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f864d-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f864d-108">Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="f864d-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="f864d-109">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="f864d-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f864d-110">Scripts kunnen worden gedownload van Azure storage of GitHub, of toohello Azure-portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="f864d-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="f864d-111">Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.</span><span class="sxs-lookup"><span data-stu-id="f864d-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f864d-112">Dit document beschrijft hoe toouse Hallo extensie voor aangepaste scripts gebruiken hello Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="f864d-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f864d-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f864d-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f864d-114">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="f864d-114">Operating System</span></span>

<span data-ttu-id="f864d-115">Hallo-extensie voor aangepaste scripts voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016 versies.</span><span class="sxs-lookup"><span data-stu-id="f864d-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="f864d-116">De locatie van script</span><span class="sxs-lookup"><span data-stu-id="f864d-116">Script Location</span></span>

<span data-ttu-id="f864d-117">Hallo script moet toobe opgeslagen in Azure-opslag of een andere locatie die toegankelijk zijn via een geldige URL.</span><span class="sxs-lookup"><span data-stu-id="f864d-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f864d-118">Verbinding met Internet</span><span class="sxs-lookup"><span data-stu-id="f864d-118">Internet Connectivity</span></span>

<span data-ttu-id="f864d-119">Hallo aangepast Script uitbreiding voor Windows is vereist dat Hallo doel-virtuele machine is verbonden toohello internet.</span><span class="sxs-lookup"><span data-stu-id="f864d-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="f864d-120">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="f864d-120">Extension schema</span></span>

<span data-ttu-id="f864d-121">Hallo toont volgende JSON Hallo-schema voor de aangepaste Scriptextensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f864d-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="f864d-122">Hallo-uitbreiding vereist de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht tooexecute.</span><span class="sxs-lookup"><span data-stu-id="f864d-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="f864d-123">Een Azure storage-account en -account sleutel is vereist als voor informatie over het gebruik van Azure Storage als Hallo van de scriptbron.</span><span class="sxs-lookup"><span data-stu-id="f864d-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="f864d-124">Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in configuratie van de beveiligde instelling Hallo-extensies.</span><span class="sxs-lookup"><span data-stu-id="f864d-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="f864d-125">Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="f864d-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="f864d-126">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="f864d-126">Property values</span></span>

| <span data-ttu-id="f864d-127">Naam</span><span class="sxs-lookup"><span data-stu-id="f864d-127">Name</span></span> | <span data-ttu-id="f864d-128">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f864d-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f864d-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f864d-129">apiVersion</span></span> | <span data-ttu-id="f864d-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f864d-130">2015-06-15</span></span> |
| <span data-ttu-id="f864d-131">Uitgever</span><span class="sxs-lookup"><span data-stu-id="f864d-131">publisher</span></span> | <span data-ttu-id="f864d-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="f864d-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="f864d-133">De extensie</span><span class="sxs-lookup"><span data-stu-id="f864d-133">extension</span></span> | <span data-ttu-id="f864d-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="f864d-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="f864d-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f864d-135">typeHandlerVersion</span></span> | <span data-ttu-id="f864d-136">1.8</span><span class="sxs-lookup"><span data-stu-id="f864d-136">1.8</span></span> |
| <span data-ttu-id="f864d-137">fileUris (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="f864d-137">fileUris (e.g)</span></span> | <span data-ttu-id="f864d-138">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="f864d-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="f864d-139">commandToExecute (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="f864d-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="f864d-140">PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1</span><span class="sxs-lookup"><span data-stu-id="f864d-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="f864d-141">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="f864d-141">Template deployment</span></span>

<span data-ttu-id="f864d-142">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f864d-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f864d-143">Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo aangepaste Scriptextensie tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f864d-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="f864d-144">Een voorbeeldsjabloon waarin de aangepaste Scriptextensie u hier vindt, Hallo [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="f864d-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="f864d-145">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="f864d-145">PowerShell deployment</span></span>

<span data-ttu-id="f864d-146">Hallo `Set-AzureVMCustomScriptExtension` opdracht gebruikte tooadd Hallo aangepast Script extensie tooan bestaande virtuele machine kan worden.</span><span class="sxs-lookup"><span data-stu-id="f864d-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="f864d-147">Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="f864d-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="f864d-148">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="f864d-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="f864d-149">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f864d-149">Troubleshoot</span></span>

<span data-ttu-id="f864d-150">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="f864d-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="f864d-151">Hallo Implementatiestatus toosee van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f864d-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="f864d-152">Uitvoering van de extensie uitvoer ons geregistreerde toofiles gevonden in de volgende map op de virtuele doelmachine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f864d-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="f864d-153">Hallo script zelf is gedownload naar de volgende map op de virtuele doelmachine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f864d-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="f864d-154">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="f864d-154">Support</span></span>

<span data-ttu-id="f864d-155">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f864d-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f864d-156">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="f864d-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f864d-157">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="f864d-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f864d-158">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f864d-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
