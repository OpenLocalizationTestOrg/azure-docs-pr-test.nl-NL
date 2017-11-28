---
title: Netwerk-Watcher-Agent de extensie van de virtuele machine voor Linux aaaAzure | Microsoft Docs
description: Hallo netwerk-Watcher-Agent op Linux virtuele machine met de extensie van een virtuele machine implementeren.
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="896f0-103">De extensie van de virtuele machine Watcher-Agent voor Linux-netwerk</span><span class="sxs-lookup"><span data-stu-id="896f0-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="896f0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="896f0-104">Overview</span></span>

<span data-ttu-id="896f0-105">[Azure-netwerk-Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is een prestaties bewaken, diagnose en analyse netwerkservice waarmee u bewaking voor Azure-netwerken.</span><span class="sxs-lookup"><span data-stu-id="896f0-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="896f0-106">Hallo-extensie van de virtuele machine netwerk-Watcher-Agent is een vereiste voor een aantal functies van de netwerk-Watcher Hallo op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="896f0-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="896f0-107">Dit omvat het vastleggen van netwerkverkeer op aanvraag en andere geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="896f0-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="896f0-108">Dit document details Hallo ondersteund platforms en implementatie-opties voor Hallo extensie van de virtuele machine netwerk-Watcher-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="896f0-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="896f0-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="896f0-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="896f0-110">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="896f0-110">Operating system</span></span>

<span data-ttu-id="896f0-111">Hallo uitbreiding van de netwerk-Watcher-Agent kan worden uitgevoerd op basis van deze Linux-distributies:</span><span class="sxs-lookup"><span data-stu-id="896f0-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="896f0-112">Distributie</span><span class="sxs-lookup"><span data-stu-id="896f0-112">Distribution</span></span> | <span data-ttu-id="896f0-113">Versie</span><span class="sxs-lookup"><span data-stu-id="896f0-113">Version</span></span> |
|---|---|
| <span data-ttu-id="896f0-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="896f0-114">Ubuntu</span></span> | <span data-ttu-id="896f0-115">16.04 TNS, 14.04 TNS en 12.04 TNS</span><span class="sxs-lookup"><span data-stu-id="896f0-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="896f0-116">Debian</span><span class="sxs-lookup"><span data-stu-id="896f0-116">Debian</span></span> | <span data-ttu-id="896f0-117">7 en 8</span><span class="sxs-lookup"><span data-stu-id="896f0-117">7 and 8</span></span> |
| <span data-ttu-id="896f0-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="896f0-118">RedHat</span></span> | <span data-ttu-id="896f0-119">6.x en 7.x</span><span class="sxs-lookup"><span data-stu-id="896f0-119">6.x and 7.x</span></span> |
| <span data-ttu-id="896f0-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="896f0-120">Oracle Linux</span></span> | <span data-ttu-id="896f0-121">7 x</span><span class="sxs-lookup"><span data-stu-id="896f0-121">7x</span></span> |
| <span data-ttu-id="896f0-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="896f0-122">Suse</span></span> | <span data-ttu-id="896f0-123">11 en 12</span><span class="sxs-lookup"><span data-stu-id="896f0-123">11 and 12</span></span> |
| <span data-ttu-id="896f0-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="896f0-124">OpenSuse</span></span> | <span data-ttu-id="896f0-125">7.0</span><span class="sxs-lookup"><span data-stu-id="896f0-125">7.0</span></span> |
| <span data-ttu-id="896f0-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="896f0-126">CentOS</span></span> | <span data-ttu-id="896f0-127">7.0</span><span class="sxs-lookup"><span data-stu-id="896f0-127">7.0</span></span> |

<span data-ttu-id="896f0-128">Houd er rekening mee dat virtuele CoreOS op dit moment niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="896f0-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="896f0-129">Internetconnectiviteit</span><span class="sxs-lookup"><span data-stu-id="896f0-129">Internet connectivity</span></span>

<span data-ttu-id="896f0-130">Aantal Hallo Agent voor netwerk-Watcher-functionaliteit is vereist dat Hallo doel-virtuele machine verbonden toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="896f0-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="896f0-131">Zonder Hallo mogelijkheid tooestablish uitgaande verbindingen mogelijk enkele Hallo Network Watcher Agent functies niet goed of niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="896f0-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="896f0-132">Zie voor meer informatie Hallo [netwerk-Watcher documentatie](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="896f0-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="896f0-133">Uitbreidingsschema</span><span class="sxs-lookup"><span data-stu-id="896f0-133">Extension schema</span></span>

<span data-ttu-id="896f0-134">Hallo toont volgende JSON Hallo-schema voor Hallo Agent voor netwerk-Watcher-extensie.</span><span class="sxs-lookup"><span data-stu-id="896f0-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="896f0-135">Hallo-uitbreiding geen van beide vereist, noch de gebruiker opgegeven instellingen op dit moment ondersteunt en is afhankelijk van de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="896f0-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="896f0-136">Eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="896f0-136">Property values</span></span>

| <span data-ttu-id="896f0-137">Naam</span><span class="sxs-lookup"><span data-stu-id="896f0-137">Name</span></span> | <span data-ttu-id="896f0-138">Waarde / voorbeeld</span><span class="sxs-lookup"><span data-stu-id="896f0-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="896f0-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="896f0-139">apiVersion</span></span> | <span data-ttu-id="896f0-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="896f0-140">2015-06-15</span></span> |
| <span data-ttu-id="896f0-141">Uitgever</span><span class="sxs-lookup"><span data-stu-id="896f0-141">publisher</span></span> | <span data-ttu-id="896f0-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="896f0-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="896f0-143">type</span><span class="sxs-lookup"><span data-stu-id="896f0-143">type</span></span> | <span data-ttu-id="896f0-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="896f0-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="896f0-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="896f0-145">typeHandlerVersion</span></span> | <span data-ttu-id="896f0-146">1.4</span><span class="sxs-lookup"><span data-stu-id="896f0-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="896f0-147">Sjabloonimplementatie</span><span class="sxs-lookup"><span data-stu-id="896f0-147">Template deployment</span></span>

<span data-ttu-id="896f0-148">Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="896f0-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="896f0-149">Hallo JSON-schema in de vorige sectie Hallo gedetailleerde kan worden gebruikt in een Azure Resource Manager sjabloon toorun Hallo uitbreiding van de netwerk-Watcher Agent tijdens de sjabloonimplementatie van een Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="896f0-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="896f0-150">Azure CLI-implementatie</span><span class="sxs-lookup"><span data-stu-id="896f0-150">Azure CLI deployment</span></span>

<span data-ttu-id="896f0-151">Hello Azure CLI mag gebruikte toodeploy Hallo netwerk-Watcher Agent VM-extensie tooan bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="896f0-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="896f0-152">Problemen oplossen en ondersteuning</span><span class="sxs-lookup"><span data-stu-id="896f0-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="896f0-153">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="896f0-153">Troubleshooting</span></span>

<span data-ttu-id="896f0-154">Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="896f0-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="896f0-155">Implementatiestatus van toosee Hallo van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="896f0-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="896f0-156">Uitvoering van de extensie uitvoer volgt geregistreerde toofiles gevonden in Hallo directory:</span><span class="sxs-lookup"><span data-stu-id="896f0-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="896f0-157">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="896f0-157">Support</span></span>

<span data-ttu-id="896f0-158">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u verwijzen toohello netwerk-Watcher-documentatie of neem contact op met hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="896f0-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="896f0-159">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="896f0-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="896f0-160">Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="896f0-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="896f0-161">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="896f0-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
