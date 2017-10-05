---
title: Aangepaste scriptextensie op een virtuele machine van Windows | Microsoft Docs
description: Virtuele machine van Azure-configuratietaken automatiseren met behulp van de aangepaste scriptextensie PowerShell-scripts uitvoeren op een externe Windows-VM
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
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="5fbc4-103">Aangepast Script uitbreiding voor Windows met het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="5fbc4-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5fbc4-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5fbc4-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5fbc4-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5fbc4-107">Lees [meer informatie over het uitvoeren van deze stappen met het Resource Manager-model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5fbc4-108">De aangepaste Scriptextensie downloads en scripts op virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="5fbc4-109">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="5fbc4-110">Scripts kunnen worden gedownload van Azure storage of GitHub, of naar de Azure portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="5fbc4-111">De aangepaste scriptextensie kan worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met de Azure CLI, PowerShell, Azure-portal of de REST-API van Azure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="5fbc4-112">Dit document details over het gebruik van de aangepaste Scriptextensie met behulp van de Azure PowerShell-module, Azure Resource Manager-sjablonen en details stappen voor probleemoplossing in Windows-systemen.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fbc4-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5fbc4-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="5fbc4-114">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="5fbc4-114">Operating System</span></span>

<span data-ttu-id="5fbc4-115">De aangepaste Scriptextensie versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="5fbc4-116">De locatie van script</span><span class="sxs-lookup"><span data-stu-id="5fbc4-116">Script Location</span></span>

<span data-ttu-id="5fbc4-117">Het script moet worden opgeslagen in Azure-opslag of een andere locatie die toegankelijk zijn via een geldige URL.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="5fbc4-118">Verbinding met Internet</span><span class="sxs-lookup"><span data-stu-id="5fbc4-118">Internet Connectivity</span></span>

<span data-ttu-id="5fbc4-119">De aangepaste Script uitbreiding voor Windows is vereist dat de virtuele doelmachine is verbonden met internet.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="5fbc4-120">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="5fbc4-120">Extension schema</span></span>

<span data-ttu-id="5fbc4-121">De volgende JSON geeft het schema voor de aangepaste Scriptextensie.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="5fbc4-122">De extensie is vereist voor de locatie van een script (Azure Storage of een andere locatie met een geldige URL) en een opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="5fbc4-123">Als u Azure-opslag gebruikt als de scriptbron, wordt een Azure storage-account en -account sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="5fbc4-124">Deze items moeten worden behandeld als gevoelige gegevens en opgegeven in de configuratie van de instelling voor beveiligde uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="5fbc4-125">Azure VM-extensie beveiligde instellingsgegevens is versleuteld en alleen op de virtuele doelmachine worden ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="5fbc4-126">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="5fbc4-126">Property values</span></span>

| <span data-ttu-id="5fbc4-127">Naam</span><span class="sxs-lookup"><span data-stu-id="5fbc4-127">Name</span></span> | <span data-ttu-id="5fbc4-128">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5fbc4-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="5fbc4-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5fbc4-129">apiVersion</span></span> | <span data-ttu-id="5fbc4-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="5fbc4-130">2015-06-15</span></span> |
| <span data-ttu-id="5fbc4-131">Uitgever</span><span class="sxs-lookup"><span data-stu-id="5fbc4-131">publisher</span></span> | <span data-ttu-id="5fbc4-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="5fbc4-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="5fbc4-133">De extensie</span><span class="sxs-lookup"><span data-stu-id="5fbc4-133">extension</span></span> | <span data-ttu-id="5fbc4-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="5fbc4-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="5fbc4-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="5fbc4-135">typeHandlerVersion</span></span> | <span data-ttu-id="5fbc4-136">1.8</span><span class="sxs-lookup"><span data-stu-id="5fbc4-136">1.8</span></span> |
| <span data-ttu-id="5fbc4-137">fileUris (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="5fbc4-137">fileUris (e.g)</span></span> | <span data-ttu-id="5fbc4-138">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-sample-templates/master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="5fbc4-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="5fbc4-139">commandToExecute (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="5fbc4-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="5fbc4-140">PowerShell - ExecutionPolicy Unrestricted - bestand configureren muziek app.ps1</span><span class="sxs-lookup"><span data-stu-id="5fbc4-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="5fbc4-141">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="5fbc4-141">Template deployment</span></span>

<span data-ttu-id="5fbc4-142">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="5fbc4-143">De JSON-schema in de vorige sectie wordt beschreven, kan de aangepaste Scriptextensie uitvoeren tijdens de sjabloonimplementatie van een Azure Resource Manager-in een Azure Resource Manager-sjabloon worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="5fbc4-144">Een voorbeeldsjabloon met de aangepaste Scriptextensie vindt u hier, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="5fbc4-145">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="5fbc4-145">PowerShell deployment</span></span>

<span data-ttu-id="5fbc4-146">De `Set-AzureVMCustomScriptExtension` opdracht kan worden gebruikt voor de extensie voor aangepaste scripts toevoegen aan een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="5fbc4-147">Zie voor meer informatie [Set AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="5fbc4-148">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="5fbc4-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="5fbc4-149">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="5fbc4-149">Troubleshoot</span></span>

<span data-ttu-id="5fbc4-150">Gegevens over de status van extensie-implementaties kunnen worden opgehaald uit de Azure portal en met behulp van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="5fbc4-151">Overzicht van de implementatiestatus van uitbreidingen voor een bepaalde virtuele machine, voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="5fbc4-152">Uitvoering van de extensie uitvoer ons aangemeld bestanden gevonden in de volgende map op de virtuele doelmachine.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="5fbc4-153">Het script zelf is gedownload naar de volgende map op de virtuele doelmachine.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="5fbc4-154">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="5fbc4-154">Support</span></span>

<span data-ttu-id="5fbc4-155">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op de [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="5fbc4-156">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5fbc4-157">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="5fbc4-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="5fbc4-158">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="5fbc4-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>