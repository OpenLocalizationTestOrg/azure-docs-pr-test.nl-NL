---
title: De extensie OMS Azure virtuele machine voor Windows | Microsoft Docs
description: Implementeer de OMS-agent op virtuele Windows-computer met de extensie van een virtuele machine.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="bfc5e-103">OMS de extensie van de virtuele machine voor Windows</span><span class="sxs-lookup"><span data-stu-id="bfc5e-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="bfc5e-104">Operations Management Suite (OMS) biedt mogelijkheden voor bewaking, waarschuwingen en waarschuwing herstel tussen cloud en on-premises activa.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="bfc5e-105">De extensie voor de OMS-Agent van een virtuele machine voor Windows is gepubliceerd en ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="bfc5e-106">De extensie wordt de OMS-agent geïnstalleerd op virtuele machines in Azure, en virtuele machines in een bestaande OMS-werkruimte schrijft.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="bfc5e-107">In dit document worden de ondersteunde platforms, configuraties en implementatie-opties voor de extensie van de OMS-virtuele machine voor Windows.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfc5e-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bfc5e-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="bfc5e-109">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="bfc5e-109">Operating system</span></span>
<span data-ttu-id="bfc5e-110">De extensie OMS-Agent versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="bfc5e-111">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="bfc5e-111">Internet connectivity</span></span>
<span data-ttu-id="bfc5e-112">De extensie OMS-Agent voor Windows is vereist dat de virtuele doelmachine is verbonden met internet.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="bfc5e-113">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="bfc5e-113">Extension schema</span></span>

<span data-ttu-id="bfc5e-114">De volgende JSON ziet u het schema voor de uitbreiding OMS-Agent.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="bfc5e-115">De extensie moet u de werkruimte-Id en werkruimtesleutel uit de doel-OMS-werkruimte, kunnen deze worden gevonden in de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="bfc5e-116">Omdat de werkruimtesleutel moet worden behandeld als gevoelige gegevens, moet deze worden opgeslagen in de configuratie van een beveiligde instelling.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="bfc5e-117">Azure VM-extensie beveiligde instellingsgegevens is versleuteld en alleen op de virtuele doelmachine worden ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="bfc5e-118">Houd er rekening mee dat **workspaceId** en **workspaceKey** zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="bfc5e-119">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="bfc5e-119">Property values</span></span>

| <span data-ttu-id="bfc5e-120">Naam</span><span class="sxs-lookup"><span data-stu-id="bfc5e-120">Name</span></span> | <span data-ttu-id="bfc5e-121">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bfc5e-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="bfc5e-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="bfc5e-122">apiVersion</span></span> | <span data-ttu-id="bfc5e-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="bfc5e-123">2015-06-15</span></span> |
| <span data-ttu-id="bfc5e-124">Uitgever</span><span class="sxs-lookup"><span data-stu-id="bfc5e-124">publisher</span></span> | <span data-ttu-id="bfc5e-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="bfc5e-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="bfc5e-126">type</span><span class="sxs-lookup"><span data-stu-id="bfc5e-126">type</span></span> | <span data-ttu-id="bfc5e-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="bfc5e-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="bfc5e-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="bfc5e-128">typeHandlerVersion</span></span> | <span data-ttu-id="bfc5e-129">1.0</span><span class="sxs-lookup"><span data-stu-id="bfc5e-129">1.0</span></span> |
| <span data-ttu-id="bfc5e-130">workspaceId (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="bfc5e-130">workspaceId (e.g)</span></span> | <span data-ttu-id="bfc5e-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="bfc5e-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="bfc5e-132">workspaceKey (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="bfc5e-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="bfc5e-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="bfc5e-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="bfc5e-134">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="bfc5e-134">Template deployment</span></span>

<span data-ttu-id="bfc5e-135">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="bfc5e-136">De JSON-schema in de vorige sectie beschreven kan worden gebruikt in een Azure Resource Manager-sjabloon voor de uitbreiding OMS-Agent wordt uitgevoerd tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="bfc5e-137">Een voorbeeldsjabloon met de OMS-Agent VM-extensie vindt u op de [galerie van Azure Quick Start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="bfc5e-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="bfc5e-138">De JSON voor de extensie van een virtuele machine worden genest in de bron van de virtuele machine, of aan de basis- of bovenste niveau van een Resource Manager JSON-sjabloon geplaatst.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="bfc5e-139">De plaatsing van de JSON van invloed op de waarde van de resourcenaam en het type.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="bfc5e-140">Zie voor meer informatie [naam en type voor de onderliggende resources instellen](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bfc5e-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="bfc5e-141">Het volgende voorbeeld wordt ervan uitgegaan dat de OMS-extensie is genest binnen de bron van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="bfc5e-142">Wanneer het nesten van de extensie-resource, de JSON wordt geplaatst in de `"resources": []` object van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="bfc5e-143">Bij het plaatsen van de JSON-extensie in de hoofdmap van de sjabloon, de naam van de bron bevat een verwijzing naar de bovenliggende virtuele machine en het type reflecteert de geneste configuratie.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="bfc5e-144">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="bfc5e-144">PowerShell deployment</span></span>

<span data-ttu-id="bfc5e-145">De `Set-AzureRmVMExtension` opdracht kan worden gebruikt voor het implementeren van de extensie van de virtuele machine OMS-Agent op een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="bfc5e-146">Voordat u de opdracht uitvoert, moeten de openbare en persoonlijke configuraties worden opgeslagen in een PowerShell-hash-tabel.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="bfc5e-147">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="bfc5e-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="bfc5e-148">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="bfc5e-148">Troubleshoot</span></span>

<span data-ttu-id="bfc5e-149">Gegevens over de status van extensie-implementaties kunnen worden opgehaald uit de Azure portal en met behulp van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="bfc5e-150">Overzicht van de implementatiestatus van uitbreidingen voor een bepaalde virtuele machine, voer de volgende opdracht met de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="bfc5e-151">De uitvoer van de extensie-uitvoering wordt vastgelegd in bestanden gevonden in de volgende map:</span><span class="sxs-lookup"><span data-stu-id="bfc5e-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="bfc5e-152">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="bfc5e-152">Support</span></span>

<span data-ttu-id="bfc5e-153">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op de [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="bfc5e-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="bfc5e-154">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bfc5e-155">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="bfc5e-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="bfc5e-156">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="bfc5e-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
