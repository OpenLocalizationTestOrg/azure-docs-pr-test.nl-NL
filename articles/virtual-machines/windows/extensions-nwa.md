---
title: aaaAzure netwerk-Watcher-Agent de extensie van de virtuele machine voor Windows | Microsoft Docs
description: Hallo netwerk-Watcher-Agent op de Windows virtuele machine met de extensie van een virtuele machine implementeren.
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
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="6b412-103">De extensie van de virtuele machine Watcher-Agent voor Windows-netwerk</span><span class="sxs-lookup"><span data-stu-id="6b412-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="6b412-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6b412-104">Overview</span></span>

<span data-ttu-id="6b412-105">[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="6b412-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="6b412-106">Hallo-extensie van de virtuele machine netwerk-Watcher-Agent is een vereiste voor een aantal functies van de netwerk-Watcher Hallo op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b412-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="6b412-107">Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="6b412-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="6b412-108">Dit document details Hallo ondersteund platforms en implementatie-opties voor Hallo extensie van de virtuele machine netwerk-Watcher-Agent voor Windows.</span><span class="sxs-lookup"><span data-stu-id="6b412-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b412-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b412-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="6b412-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="6b412-110">Operating system</span></span>

<span data-ttu-id="6b412-111">Hallo uitbreiding van de netwerk-Watcher-Agent versies voor Windows kan worden uitgevoerd op basis van Windows Server 2008 R2, 2012, 2012 R2 en 2016.</span><span class="sxs-lookup"><span data-stu-id="6b412-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="6b412-112">Houd er rekening mee dat Hallo die nano Server wordt niet ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="6b412-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="6b412-113">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="6b412-113">Internet connectivity</span></span>

<span data-ttu-id="6b412-114">Aantal Hallo Agent voor netwerk-Watcher-functionaliteit is vereist dat Hallo doel-virtuele machine verbonden toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="6b412-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="6b412-115">Zonder Hallo mogelijkheid tooestablish uitgaande verbindingen mogelijk enkele Hallo Network Watcher Agent functies niet goed of niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="6b412-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="6b412-116">Zie voor meer informatie Hallo [netwerk-Watcher documentatie](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b412-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="6b412-117">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="6b412-117">Extension schema</span></span>

<span data-ttu-id="6b412-118">Hallo toont volgende JSON Hallo-schema voor Hallo Agent voor netwerk-Watcher-extensie.</span><span class="sxs-lookup"><span data-stu-id="6b412-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="6b412-119">Hallo-uitbreiding geen van beide vereist, noch de gebruiker opgegeven instellingen op dit moment ondersteunt en is afhankelijk van de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="6b412-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="6b412-120">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="6b412-120">Property values</span></span>

| <span data-ttu-id="6b412-121">Naam</span><span class="sxs-lookup"><span data-stu-id="6b412-121">Name</span></span> | <span data-ttu-id="6b412-122">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="6b412-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="6b412-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6b412-123">apiVersion</span></span> | <span data-ttu-id="6b412-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="6b412-124">2015-06-15</span></span> |
| <span data-ttu-id="6b412-125">Uitgever</span><span class="sxs-lookup"><span data-stu-id="6b412-125">publisher</span></span> | <span data-ttu-id="6b412-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="6b412-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="6b412-127">type</span><span class="sxs-lookup"><span data-stu-id="6b412-127">type</span></span> | <span data-ttu-id="6b412-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="6b412-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="6b412-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="6b412-129">typeHandlerVersion</span></span> | <span data-ttu-id="6b412-130">1.4</span><span class="sxs-lookup"><span data-stu-id="6b412-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="6b412-131">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="6b412-131">Template deployment</span></span>

<span data-ttu-id="6b412-132">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6b412-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="6b412-133">Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo uitbreiding van de netwerk-Watcher Agent tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b412-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="6b412-134">PowerShell-implementatie</span><span class="sxs-lookup"><span data-stu-id="6b412-134">PowerShell deployment</span></span>

<span data-ttu-id="6b412-135">Hallo `Set-AzureRmVMExtension` opdracht gebruikte toodeploy Hallo Network Watcher Agent virtuele machine extensie tooan bestaande virtuele machine kan worden.</span><span class="sxs-lookup"><span data-stu-id="6b412-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="6b412-136">Problemen oplossen en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="6b412-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="6b412-137">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6b412-137">Troubleshooting</span></span>

<span data-ttu-id="6b412-138">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="6b412-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="6b412-139">Implementatiestatus van toosee Hallo van uitbreidingen voor een opgegeven virtuele machine, Voer Hallo na gebruik van de opdracht hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="6b412-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="6b412-140">Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:</span><span class="sxs-lookup"><span data-stu-id="6b412-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="6b412-141">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="6b412-141">Support</span></span>

<span data-ttu-id="6b412-142">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u verwijzen toohello gebruikershandleiding voor netwerk-Watcher-documentatie of neem contact op met hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6b412-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="6b412-143">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="6b412-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6b412-144">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="6b412-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="6b412-145">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="6b412-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
