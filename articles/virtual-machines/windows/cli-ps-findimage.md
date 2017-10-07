---
title: "installatiekopieën van aaaSelect virtuele Windows-machine in Azure | Microsoft Docs"
description: "Meer informatie over hoe toouse Azure PowerSHell toodetermine Hallo uitgever, aanbieding, SKU en versie voor Marketplace-VM-installatiekopieën."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="54eef-103">Hoe toofind Windows VM installatiekopieën in hello Azure Marketplace met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54eef-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="54eef-104">Dit onderwerp wordt beschreven hoe toouse Azure PowerShell toofind VM installatiekopieën in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="54eef-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="54eef-105">Gebruik deze informatie toospecify een Marketplace-installatiekopie bij het maken van een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="54eef-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="54eef-106">Zorg ervoor dat u geïnstalleerd en geconfigureerd Hallo nieuwste [Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="54eef-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="54eef-107">Tabel met veelgebruikte Windows-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="54eef-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="54eef-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="54eef-108">PublisherName</span></span> | <span data-ttu-id="54eef-109">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="54eef-109">Offer</span></span> | <span data-ttu-id="54eef-110">Sku</span><span class="sxs-lookup"><span data-stu-id="54eef-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54eef-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-112">WindowsServer</span></span> |<span data-ttu-id="54eef-113">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="54eef-113">2016-Datacenter</span></span> |
| <span data-ttu-id="54eef-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-115">WindowsServer</span></span> |<span data-ttu-id="54eef-116">2016 Datacenter-Server Core</span><span class="sxs-lookup"><span data-stu-id="54eef-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="54eef-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-118">WindowsServer</span></span> |<span data-ttu-id="54eef-119">2016 Datacenter met Containers</span><span class="sxs-lookup"><span data-stu-id="54eef-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="54eef-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-121">WindowsServer</span></span> |<span data-ttu-id="54eef-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="54eef-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="54eef-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-124">WindowsServer</span></span> |<span data-ttu-id="54eef-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="54eef-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="54eef-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54eef-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54eef-127">WindowsServer</span></span> |<span data-ttu-id="54eef-128">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="54eef-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="54eef-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="54eef-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="54eef-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="54eef-130">DynamicsNAV</span></span> |<span data-ttu-id="54eef-131">2017</span><span class="sxs-lookup"><span data-stu-id="54eef-131">2017</span></span> |
| <span data-ttu-id="54eef-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="54eef-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="54eef-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="54eef-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="54eef-134">2016</span><span class="sxs-lookup"><span data-stu-id="54eef-134">2016</span></span> |
| <span data-ttu-id="54eef-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="54eef-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="54eef-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="54eef-136">SQL2016-WS2016</span></span> |<span data-ttu-id="54eef-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="54eef-137">Enterprise</span></span> |
| <span data-ttu-id="54eef-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="54eef-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="54eef-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="54eef-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="54eef-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="54eef-140">Enterprise</span></span> |
| <span data-ttu-id="54eef-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="54eef-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="54eef-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="54eef-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="54eef-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="54eef-143">2012R2</span></span> |
| <span data-ttu-id="54eef-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54eef-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="54eef-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54eef-145">WindowsServerEssentials</span></span> |<span data-ttu-id="54eef-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54eef-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="54eef-147">Specifieke installatiekopieën zoeken</span><span class="sxs-lookup"><span data-stu-id="54eef-147">Find specific images</span></span>


<span data-ttu-id="54eef-148">Wanneer u een nieuwe virtuele machine maakt met Azure Resource Manager, in sommige gevallen moet u toospecify een afbeelding met Hallo combinatie van Hallo eigenschappen van de installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="54eef-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="54eef-149">Uitgever</span><span class="sxs-lookup"><span data-stu-id="54eef-149">Publisher</span></span>
* <span data-ttu-id="54eef-150">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="54eef-150">Offer</span></span>
* <span data-ttu-id="54eef-151">SKU</span><span class="sxs-lookup"><span data-stu-id="54eef-151">SKU</span></span>

<span data-ttu-id="54eef-152">Gebruik bijvoorbeeld deze waarden met Hallo [Set AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell-cmdlet of met een resource groep sjabloon waarin u Hallo type VM toobe gemaakt moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="54eef-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="54eef-153">Als u deze waarden nodig toodetermine hebt, kunt u Hallo uitvoeren [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), en [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="54eef-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="54eef-154">U bepalen deze waarden:</span><span class="sxs-lookup"><span data-stu-id="54eef-154">You determine these values:</span></span>

1. <span data-ttu-id="54eef-155">Lijst Hallo installatiekopie uitgevers.</span><span class="sxs-lookup"><span data-stu-id="54eef-155">List hello image publishers.</span></span>
2. <span data-ttu-id="54eef-156">Geef de aanbiedingen voor een bepaalde uitgever weer.</span><span class="sxs-lookup"><span data-stu-id="54eef-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="54eef-157">Geef de SKU's voor een bepaalde aanbieding weer.</span><span class="sxs-lookup"><span data-stu-id="54eef-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="54eef-158">Lijst eerst Hallo uitgevers Hello volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="54eef-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="54eef-159">Vul de naam van uw gekozen publisher en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="54eef-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="54eef-160">Vul de aanbiedingsnaam van uw gekozen en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="54eef-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="54eef-161">Uit de uitvoer Hallo Hallo `Get-AzureRMVMImageSku` uitvoert, en u alle Hallo informatie u toospecify Hallo installatiekopie voor een nieuwe virtuele machine nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="54eef-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="54eef-162">Hallo hieronder vindt u een voorbeeld van een volledige:</span><span class="sxs-lookup"><span data-stu-id="54eef-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="54eef-163">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="54eef-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="54eef-164">Hallo 'Legitieme Microsoft Windows Server' Publisher:</span><span class="sxs-lookup"><span data-stu-id="54eef-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="54eef-165">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="54eef-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="54eef-166">Voor Windows ' Server' hello bieden:</span><span class="sxs-lookup"><span data-stu-id="54eef-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="54eef-167">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="54eef-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="54eef-168">In deze lijst kopiëren Hallo gekozen SKU-naam, en hebt u alle Hallo-informatie voor Hallo `Set-AzureRMVMSourceImage` PowerShell-cmdlet of voor een resource group-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="54eef-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54eef-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54eef-169">Next steps</span></span>
<span data-ttu-id="54eef-170">Nu kunt u precies Hallo installatiekopie wilt toouse.</span><span class="sxs-lookup"><span data-stu-id="54eef-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="54eef-171">toocreate een virtuele machine snel met behulp van de installatiekopiegegevens hello, die u zojuist hebt gevonden, Zie [virtuele Windows-machine maken met PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="54eef-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
