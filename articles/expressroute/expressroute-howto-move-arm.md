---
title: 'ExpressRoute-circuits verplaatsen van klassiek naar Resource Manager: PowerShell: Azure | Microsoft Docs'
description: Deze pagina wordt beschreven hoe een klassieke circuit verplaatsen naar het Resource Manager-implementatiemodel met behulp van PowerShell.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="749ec-103">ExpressRoute-circuits verplaatsen van het klassieke naar het Resource Manager-implementatiemodel met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="749ec-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="749ec-104">Voor het gebruik van een ExpressRoute-circuit voor zowel het klassieke implementatiemodel van Resource Manager, moet u het circuit verplaatsen naar het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="749ec-105">De volgende secties helpen u uw circuit verplaatsen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="749ec-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="749ec-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="749ec-106">Before you begin</span></span>

* <span data-ttu-id="749ec-107">Controleer of u de nieuwste versie van de Azure PowerShell-modules (ten minste versie 1.0).</span><span class="sxs-lookup"><span data-stu-id="749ec-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="749ec-108">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="749ec-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="749ec-109">Zorg ervoor dat u hebt bekeken de [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="749ec-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="749ec-110">Lees de informatie die is opgegeven onder [een ExpressRoute-circuit verplaatsen van klassiek naar Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="749ec-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="749ec-111">Zorg ervoor dat u volledig limieten en beperkingen begrijpt.</span><span class="sxs-lookup"><span data-stu-id="749ec-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="749ec-112">Controleer of het circuit volledig operationeel is in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="749ec-113">Zorg ervoor dat u een resourcegroep die is gemaakt in het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="749ec-114">Een ExpressRoute-circuit verplaatsen</span><span class="sxs-lookup"><span data-stu-id="749ec-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="749ec-115">Stap 1: De details van het circuit vanuit het klassieke implementatiemodel verzamelen</span><span class="sxs-lookup"><span data-stu-id="749ec-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="749ec-116">Aanmelden bij de klassieke Azure-omgeving en de servicesleutel verzamelen.</span><span class="sxs-lookup"><span data-stu-id="749ec-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="749ec-117">Aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="749ec-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="749ec-118">Selecteer het juiste Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="749ec-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="749ec-119">Importeer de PowerShell-modules voor Azure en ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="749ec-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="749ec-120">De onderstaande cmdlet gebruiken om op te halen van de service-sleutels voor al uw ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="749ec-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="749ec-121">Bij het ophalen van de sleutels, kopieert u de **servicesleutel** van het circuit die u wilt verplaatsen naar het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="749ec-122">Stap 2: Aanmelden en een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="749ec-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="749ec-123">Aanmelden bij de Resource Manager-omgeving en maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="749ec-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="749ec-124">Aanmelden bij uw Azure Resource Manager-omgeving.</span><span class="sxs-lookup"><span data-stu-id="749ec-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="749ec-125">Selecteer het juiste Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="749ec-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="749ec-126">Wijzig het codefragment hieronder een nieuwe resourcegroep maken als u een resourcegroep nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="749ec-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="749ec-127">Stap 3: De ExpressRoute-circuit verplaatsen naar het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="749ec-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="749ec-128">U bent nu klaar voor het ExpressRoute-circuit verplaatsen van het klassieke implementatiemodel naar het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="749ec-129">Bekijk de informatie in voordat u doorgaat, [een ExpressRoute-circuit verplaatsen van het klassieke naar het Resource Manager-implementatiemodel](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="749ec-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="749ec-130">Uw circuit te verplaatsen, wijzigen en voer het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="749ec-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="749ec-131">Nadat de verplaatsing is voltooid, wordt de nieuwe naam die wordt vermeld in de vorige cmdlet gebruikt voor het oplossen van de resource.</span><span class="sxs-lookup"><span data-stu-id="749ec-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="749ec-132">In wezen het circuit gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="749ec-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="749ec-133">Circuit toegang wijzigen</span><span class="sxs-lookup"><span data-stu-id="749ec-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="749ec-134">ExpressRoute-circuit toegang voor beide implementatiemodellen inschakelen</span><span class="sxs-lookup"><span data-stu-id="749ec-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="749ec-135">Nadat u het klassieke ExpressRoute-circuit naar het Resource Manager-implementatiemodel, kunt u toegang tot beide implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="749ec-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="749ec-136">Voer de volgende cmdlets voor toegang tot beide implementatiemodellen:</span><span class="sxs-lookup"><span data-stu-id="749ec-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="749ec-137">De circuit-details ophalen.</span><span class="sxs-lookup"><span data-stu-id="749ec-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="749ec-138">Ingesteld op 'Klassieke bewerkingen toestaan' op TRUE.</span><span class="sxs-lookup"><span data-stu-id="749ec-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="749ec-139">Werk het circuit.</span><span class="sxs-lookup"><span data-stu-id="749ec-139">Update the circuit.</span></span> <span data-ttu-id="749ec-140">Nadat u deze bewerking is voltooid, kunt u zich kunt u het circuit in het klassieke implementatiemodel weergeven.</span><span class="sxs-lookup"><span data-stu-id="749ec-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="749ec-141">Voer de volgende cmdlet als u de details van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="749ec-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="749ec-142">U moet de servicesleutel vermeld zien.</span><span class="sxs-lookup"><span data-stu-id="749ec-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="749ec-143">U kunt nu koppelingen naar het ExpressRoute-circuit met de klassieke implementatie model-opdrachten voor klassieke vnet's en de Resource Manager-opdrachten voor Resource Manager VNets beheren.</span><span class="sxs-lookup"><span data-stu-id="749ec-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="749ec-144">De volgende artikelen kunnen u koppelingen naar het ExpressRoute-circuit beheren:</span><span class="sxs-lookup"><span data-stu-id="749ec-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="749ec-145">Het virtuele netwerk koppelen aan uw ExpressRoute-circuit in het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="749ec-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="749ec-146">Het virtuele netwerk koppelen aan uw ExpressRoute-circuit in het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="749ec-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="749ec-147">ExpressRoute-circuit toegang tot het klassieke implementatiemodel uitschakelen</span><span class="sxs-lookup"><span data-stu-id="749ec-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="749ec-148">Voer de volgende cmdlets voor toegang tot het klassieke implementatiemodel uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="749ec-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="749ec-149">Details van het ExpressRoute-circuit ophalen.</span><span class="sxs-lookup"><span data-stu-id="749ec-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="749ec-150">Ingesteld op 'Klassieke bewerkingen toestaan' op FALSE.</span><span class="sxs-lookup"><span data-stu-id="749ec-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="749ec-151">Werk het circuit.</span><span class="sxs-lookup"><span data-stu-id="749ec-151">Update the circuit.</span></span> <span data-ttu-id="749ec-152">Nadat u deze bewerking is voltooid, is het niet mogelijk het circuit weergeven in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="749ec-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="749ec-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="749ec-153">Next steps</span></span>

* [<span data-ttu-id="749ec-154">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="749ec-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="749ec-155">Het virtuele netwerk koppelen aan uw ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="749ec-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)