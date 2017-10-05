---
title: Extensie van virtuele machine met Azure-netwerk-Watcher-Agent voor Linux | Microsoft Docs
description: Implementeer de netwerk-Watcher-Agent op Linux virtuele machine met de extensie van een virtuele machine.
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="684fe-103">De extensie van de virtuele machine Watcher-Agent voor Linux-netwerk</span><span class="sxs-lookup"><span data-stu-id="684fe-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="684fe-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="684fe-104">Overview</span></span>

<span data-ttu-id="684fe-105">[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="684fe-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="684fe-106">De extensie van de Agent voor netwerk-Watcher-virtuele machine is vereist voor sommige van de netwerk-Watcher-functies op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="684fe-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="684fe-107">Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="684fe-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="684fe-108">In dit document worden de ondersteunde platforms en implementatie-opties voor de extensie van de Agent voor netwerk-Watcher-virtuele machine voor Linux.</span><span class="sxs-lookup"><span data-stu-id="684fe-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="684fe-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="684fe-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="684fe-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="684fe-110">Operating system</span></span>

<span data-ttu-id="684fe-111">De extensie van de netwerk-Watcher-Agent kan worden uitgevoerd tegen deze Linux-distributies:</span><span class="sxs-lookup"><span data-stu-id="684fe-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="684fe-112">Distributie</span><span class="sxs-lookup"><span data-stu-id="684fe-112">Distribution</span></span> | <span data-ttu-id="684fe-113">Versie</span><span class="sxs-lookup"><span data-stu-id="684fe-113">Version</span></span> |
|---|---|
| <span data-ttu-id="684fe-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="684fe-114">Ubuntu</span></span> | <span data-ttu-id="684fe-115">16.04 TNS, 14.04 TNS en 12.04 TNS</span><span class="sxs-lookup"><span data-stu-id="684fe-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="684fe-116">Debian</span><span class="sxs-lookup"><span data-stu-id="684fe-116">Debian</span></span> | <span data-ttu-id="684fe-117">7 en 8</span><span class="sxs-lookup"><span data-stu-id="684fe-117">7 and 8</span></span> |
| <span data-ttu-id="684fe-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="684fe-118">RedHat</span></span> | <span data-ttu-id="684fe-119">6.x en 7.x</span><span class="sxs-lookup"><span data-stu-id="684fe-119">6.x and 7.x</span></span> |
| <span data-ttu-id="684fe-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="684fe-120">Oracle Linux</span></span> | <span data-ttu-id="684fe-121">7 x</span><span class="sxs-lookup"><span data-stu-id="684fe-121">7x</span></span> |
| <span data-ttu-id="684fe-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="684fe-122">Suse</span></span> | <span data-ttu-id="684fe-123">11 en 12</span><span class="sxs-lookup"><span data-stu-id="684fe-123">11 and 12</span></span> |
| <span data-ttu-id="684fe-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="684fe-124">OpenSuse</span></span> | <span data-ttu-id="684fe-125">7.0</span><span class="sxs-lookup"><span data-stu-id="684fe-125">7.0</span></span> |
| <span data-ttu-id="684fe-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="684fe-126">CentOS</span></span> | <span data-ttu-id="684fe-127">7.0</span><span class="sxs-lookup"><span data-stu-id="684fe-127">7.0</span></span> |

<span data-ttu-id="684fe-128">Houd er rekening mee dat virtuele CoreOS op dit moment niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="684fe-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="684fe-129">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="684fe-129">Internet connectivity</span></span>

<span data-ttu-id="684fe-130">Sommige van de Agent voor netwerk-Watcher-functionaliteit is vereist dat de virtuele doelmachine worden verbonden met Internet.</span><span class="sxs-lookup"><span data-stu-id="684fe-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="684fe-131">Zonder de mogelijkheid tot stand brengen van uitgaande verbindingen mogelijk enkele van de Agent voor netwerk-Watcher-functies niet goed of niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="684fe-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="684fe-132">Zie voor meer informatie de [netwerk-Watcher documentatie](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="684fe-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="684fe-133">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="684fe-133">Extension schema</span></span>

<span data-ttu-id="684fe-134">De volgende JSON vindt u het schema voor de Agent voor netwerk-Watcher-extensie.</span><span class="sxs-lookup"><span data-stu-id="684fe-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="684fe-135">De extensie niet vereist, noch gebruiker opgegeven instellingen op dit moment ondersteunt en is afhankelijk van de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="684fe-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="684fe-136">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="684fe-136">Property values</span></span>

| <span data-ttu-id="684fe-137">Naam</span><span class="sxs-lookup"><span data-stu-id="684fe-137">Name</span></span> | <span data-ttu-id="684fe-138">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="684fe-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="684fe-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="684fe-139">apiVersion</span></span> | <span data-ttu-id="684fe-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="684fe-140">2015-06-15</span></span> |
| <span data-ttu-id="684fe-141">Uitgever</span><span class="sxs-lookup"><span data-stu-id="684fe-141">publisher</span></span> | <span data-ttu-id="684fe-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="684fe-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="684fe-143">type</span><span class="sxs-lookup"><span data-stu-id="684fe-143">type</span></span> | <span data-ttu-id="684fe-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="684fe-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="684fe-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="684fe-145">typeHandlerVersion</span></span> | <span data-ttu-id="684fe-146">1.4</span><span class="sxs-lookup"><span data-stu-id="684fe-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="684fe-147">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="684fe-147">Template deployment</span></span>

<span data-ttu-id="684fe-148">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="684fe-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="684fe-149">De JSON-schema in de vorige sectie wordt beschreven, kan de Agent voor netwerk-Watcher-extensie uitgevoerd tijdens de sjabloonimplementatie van een Azure Resource Manager-in een Azure Resource Manager-sjabloon worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="684fe-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="684fe-150">Azure CLI-implementatie</span><span class="sxs-lookup"><span data-stu-id="684fe-150">Azure CLI deployment</span></span>

<span data-ttu-id="684fe-151">De Azure CLI kan worden gebruikt voor het implementeren van de netwerk-Watcher Agent VM-extensie op een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="684fe-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="684fe-152">Problemen oplossen en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="684fe-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="684fe-153">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="684fe-153">Troubleshooting</span></span>

<span data-ttu-id="684fe-154">Gegevens over de status van extensie-implementaties kunnen worden opgehaald uit de Azure portal en met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="684fe-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="684fe-155">Overzicht van de implementatiestatus van uitbreidingen voor een bepaalde virtuele machine, voer de volgende opdracht met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="684fe-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="684fe-156">De uitvoer van de extensie-uitvoering wordt vastgelegd in bestanden gevonden in de volgende map:</span><span class="sxs-lookup"><span data-stu-id="684fe-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="684fe-157">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="684fe-157">Support</span></span>

<span data-ttu-id="684fe-158">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u verwijzen naar de netwerk-Watcher-documentatie of neem contact op met de Azure deskundigen op het [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="684fe-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="684fe-159">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="684fe-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="684fe-160">Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="684fe-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="684fe-161">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="684fe-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
