---
title: Extensie van virtuele machine met Azure-netwerk-Watcher-Agent voor Windows | Microsoft Docs
description: De netwerk-Watcher-Agent op virtuele Windows-computer met de extensie van een virtuele machine implementeren.
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: b8d6a998bc86337b286a3434f44f762cca9b7e68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="b2fbe-103">De extensie van de virtuele machine Watcher-Agent voor Windows-netwerk</span><span class="sxs-lookup"><span data-stu-id="b2fbe-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="b2fbe-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b2fbe-104">Overview</span></span>

<span data-ttu-id="b2fbe-105">[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="b2fbe-106">De extensie van de Agent voor netwerk-Watcher-virtuele machine is vereist voor sommige van de netwerk-Watcher-functies op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="b2fbe-107">Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="b2fbe-108">In dit document worden de ondersteunde platforms en implementatie-opties voor de extensie van de Agent voor netwerk-Watcher-virtuele machine voor Windows.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2fbe-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b2fbe-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="b2fbe-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="b2fbe-110">Operating system</span></span>

<span data-ttu-id="b2fbe-111">De Agent voor netwerk-Watcher-extensie versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="b2fbe-112">Houd er rekening mee dat de Nano-Server niet wordt ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="b2fbe-113">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="b2fbe-113">Internet connectivity</span></span>

<span data-ttu-id="b2fbe-114">Sommige van de Agent voor netwerk-Watcher-functionaliteit is vereist dat de virtuele doelmachine worden verbonden met Internet.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="b2fbe-115">Zonder de mogelijkheid tot stand brengen van uitgaande verbindingen mogelijk enkele van de Agent voor netwerk-Watcher-functies niet goed of niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="b2fbe-116">Zie voor meer informatie de [netwerk-Watcher documentatie](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2fbe-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="b2fbe-117">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="b2fbe-117">Extension schema</span></span>

<span data-ttu-id="b2fbe-118">De volgende JSON vindt u het schema voor de Agent voor netwerk-Watcher-extensie.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="b2fbe-119">De extensie niet vereist, noch gebruiker opgegeven instellingen op dit moment ondersteunt en is afhankelijk van de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="b2fbe-120">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="b2fbe-120">Property values</span></span>

| <span data-ttu-id="b2fbe-121">Naam</span><span class="sxs-lookup"><span data-stu-id="b2fbe-121">Name</span></span> | <span data-ttu-id="b2fbe-122">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b2fbe-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="b2fbe-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b2fbe-123">apiVersion</span></span> | <span data-ttu-id="b2fbe-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="b2fbe-124">2015-06-15</span></span> |
| <span data-ttu-id="b2fbe-125">Uitgever</span><span class="sxs-lookup"><span data-stu-id="b2fbe-125">publisher</span></span> | <span data-ttu-id="b2fbe-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="b2fbe-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="b2fbe-127">type</span><span class="sxs-lookup"><span data-stu-id="b2fbe-127">type</span></span> | <span data-ttu-id="b2fbe-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="b2fbe-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="b2fbe-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="b2fbe-129">typeHandlerVersion</span></span> | <span data-ttu-id="b2fbe-130">1.4</span><span class="sxs-lookup"><span data-stu-id="b2fbe-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="b2fbe-131">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="b2fbe-131">Template deployment</span></span>

<span data-ttu-id="b2fbe-132">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="b2fbe-133">De JSON-schema in de vorige sectie wordt beschreven, kan de Agent voor netwerk-Watcher-extensie uitgevoerd tijdens de sjabloonimplementatie van een Azure Resource Manager-in een Azure Resource Manager-sjabloon worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="b2fbe-134">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="b2fbe-134">PowerShell deployment</span></span>

<span data-ttu-id="b2fbe-135">De `Set-AzureRmVMExtension` opdracht kan worden gebruikt voor het implementeren van de extensie van de Agent voor netwerk-Watcher-virtuele machine op een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="b2fbe-136">Problemen oplossen en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b2fbe-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="b2fbe-137">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b2fbe-137">Troubleshooting</span></span>

<span data-ttu-id="b2fbe-138">Gegevens over de status van extensie-implementaties kunnen worden opgehaald uit de Azure portal en met behulp van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="b2fbe-139">Overzicht van de implementatiestatus van uitbreidingen voor een bepaalde virtuele machine, voer de volgende opdracht met de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="b2fbe-140">De uitvoer van de extensie-uitvoering wordt vastgelegd in bestanden gevonden in de volgende map:</span><span class="sxs-lookup"><span data-stu-id="b2fbe-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="b2fbe-141">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b2fbe-141">Support</span></span>

<span data-ttu-id="b2fbe-142">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u Raadpleeg de gebruikershandleiding voor netwerk-Watcher-documentatie of neem contact op met de Azure deskundigen op het [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b2fbe-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="b2fbe-143">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b2fbe-144">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="b2fbe-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="b2fbe-145">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="b2fbe-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
