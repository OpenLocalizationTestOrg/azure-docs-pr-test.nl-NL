---
title: aaaOMS uitbreiding van de virtuele machine van Azure voor Windows | Microsoft Docs
description: Hallo OMS-agent op de Windows virtuele machine met de extensie van een virtuele machine implementeren.
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
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="3a1d6-103">OMS de extensie van de virtuele machine voor Windows</span><span class="sxs-lookup"><span data-stu-id="3a1d6-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="3a1d6-104">Operations Management Suite (OMS) biedt mogelijkheden voor bewaking, waarschuwingen en waarschuwing herstel tussen cloud en on-premises activa.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="3a1d6-105">Hallo OMS-Agent de extensie van de virtuele machine voor Windows is gepubliceerd en ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="3a1d6-106">Hallo-extensie Hallo OMS-agent is geïnstalleerd op virtuele machines in Azure en virtuele machines in een bestaande OMS-werkruimte inschrijft.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="3a1d6-107">Dit document details Hallo ondersteund platforms, configuraties en implementatie-opties voor Hallo extensie OMS-virtuele machine voor Windows.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a1d6-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a1d6-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="3a1d6-109">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="3a1d6-109">Operating system</span></span>
<span data-ttu-id="3a1d6-110">Hallo-extensie OMS-Agent versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="3a1d6-111">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="3a1d6-111">Internet connectivity</span></span>
<span data-ttu-id="3a1d6-112">uitbreiding van de OMS-Agent voor Windows Hello is vereist dat Hallo doel-virtuele machine is verbonden toohello internet.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="3a1d6-113">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="3a1d6-113">Extension schema</span></span>

<span data-ttu-id="3a1d6-114">Hallo toont volgende JSON Hallo-schema voor Hallo OMS-Agent-extensie.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="3a1d6-115">Hallo-uitbreiding vereist Hallo werkruimte-Id en werkruimte sleutel uit Hallo doel OMS-werkruimte, deze vindt u in Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="3a1d6-116">Omdat Hallo werkruimtesleutel moet worden behandeld als gevoelige gegevens, moet deze worden opgeslagen in de configuratie van een beveiligde instelling.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="3a1d6-117">Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="3a1d6-118">Houd er rekening mee dat **workspaceId** en **workspaceKey** zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="3a1d6-119">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="3a1d6-119">Property values</span></span>

| <span data-ttu-id="3a1d6-120">Naam</span><span class="sxs-lookup"><span data-stu-id="3a1d6-120">Name</span></span> | <span data-ttu-id="3a1d6-121">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3a1d6-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="3a1d6-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a1d6-122">apiVersion</span></span> | <span data-ttu-id="3a1d6-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="3a1d6-123">2015-06-15</span></span> |
| <span data-ttu-id="3a1d6-124">Uitgever</span><span class="sxs-lookup"><span data-stu-id="3a1d6-124">publisher</span></span> | <span data-ttu-id="3a1d6-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="3a1d6-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="3a1d6-126">type</span><span class="sxs-lookup"><span data-stu-id="3a1d6-126">type</span></span> | <span data-ttu-id="3a1d6-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="3a1d6-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="3a1d6-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="3a1d6-128">typeHandlerVersion</span></span> | <span data-ttu-id="3a1d6-129">1.0</span><span class="sxs-lookup"><span data-stu-id="3a1d6-129">1.0</span></span> |
| <span data-ttu-id="3a1d6-130">workspaceId (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="3a1d6-130">workspaceId (e.g)</span></span> | <span data-ttu-id="3a1d6-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="3a1d6-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="3a1d6-132">workspaceKey (bijvoorbeeld)</span><span class="sxs-lookup"><span data-stu-id="3a1d6-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="3a1d6-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="3a1d6-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="3a1d6-134">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="3a1d6-134">Template deployment</span></span>

<span data-ttu-id="3a1d6-135">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="3a1d6-136">Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo OMS-Agent extensie tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="3a1d6-137">Een voorbeeldsjabloon met Hallo OMS-Agent VM-extensie vindt u op Hallo [galerie van Azure Quick Start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="3a1d6-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="3a1d6-138">Hallo JSON voor de extensie van een virtuele machine worden genest in de bron van de virtuele machine Hallo of geplaatst op Hallo bovenste niveau van een Resource Manager JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="3a1d6-139">Hallo plaatsing van Hallo JSON is van invloed op Hallo-waarde van Hallo resourcenaam en het type.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="3a1d6-140">Zie voor meer informatie [naam en type voor de onderliggende resources instellen](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3a1d6-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="3a1d6-141">Hallo volgende voorbeeld wordt ervan uitgegaan Hallo OMS-extensie is genest binnen de bron van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="3a1d6-142">Wanneer het nesten van Hallo extensie resource Hallo JSON wordt geplaatst in Hallo `"resources": []` object van het Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


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

<span data-ttu-id="3a1d6-143">Bij het plaatsen van Hallo extensie JSON aan Hallo basis van sjabloon hello, Hallo Resourcenaam bevat een verwijzing toohello bovenliggende virtuele machine en Hallo type reflecteert Hallo geneste configuratie.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="3a1d6-144">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="3a1d6-144">PowerShell deployment</span></span>

<span data-ttu-id="3a1d6-145">Hallo `Set-AzureRmVMExtension` opdracht gebruikte toodeploy Hallo OMS-Agent virtuele machine extensie tooan bestaande virtuele machine kan worden.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="3a1d6-146">Voordat u Hallo-opdracht, moeten de openbare en persoonlijke configuraties Hallo toobe opgeslagen in een PowerShell-hash-tabel.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="3a1d6-147">Oplossen van problemen en ondersteunen</span><span class="sxs-lookup"><span data-stu-id="3a1d6-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="3a1d6-148">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3a1d6-148">Troubleshoot</span></span>

<span data-ttu-id="3a1d6-149">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="3a1d6-150">Implementatiestatus van toosee Hallo van uitbreidingen voor een opgegeven virtuele machine, Voer Hallo na gebruik van de opdracht hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="3a1d6-151">Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:</span><span class="sxs-lookup"><span data-stu-id="3a1d6-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="3a1d6-152">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="3a1d6-152">Support</span></span>

<span data-ttu-id="3a1d6-153">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3a1d6-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="3a1d6-154">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3a1d6-155">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="3a1d6-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="3a1d6-156">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3a1d6-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
