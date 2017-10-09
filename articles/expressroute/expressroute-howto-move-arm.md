---
title: 'ExpressRoute-circuits verplaatsen van klassieke tooResource Manager: PowerShell: Azure | Microsoft Docs'
description: Deze pagina wordt beschreven hoe toomove een klassieke circuit toohello Resource Manager deployment model met behulp van PowerShell.
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
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="6868c-103">ExpressRoute-circuits verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="6868c-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="6868c-104">toouse een ExpressRoute-circuit voor zowel klassieke Hallo als Resource Manager-implementatiemodel, moet u Hallo circuit toohello Resource Manager-implementatiemodel verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="6868c-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="6868c-105">Hallo volgende secties helpen u uw circuit verplaatsen met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6868c-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6868c-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6868c-106">Before you begin</span></span>

* <span data-ttu-id="6868c-107">Controleer of u de meest recente versie Hallo van hello Azure PowerShell-modules (ten minste versie 1.0).</span><span class="sxs-lookup"><span data-stu-id="6868c-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="6868c-108">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6868c-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6868c-109">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="6868c-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="6868c-110">Hallo-informatie die is opgegeven onder [een ExpressRoute-circuit verplaatsen van klassieke tooResource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="6868c-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="6868c-111">Zorg ervoor dat u volledig Hallo limieten en beperkingen begrijpt.</span><span class="sxs-lookup"><span data-stu-id="6868c-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="6868c-112">Controleer of Hallo circuit in het klassieke implementatiemodel Hallo volledig operationeel is.</span><span class="sxs-lookup"><span data-stu-id="6868c-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="6868c-113">Zorg ervoor dat u een resourcegroep die is gemaakt in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6868c-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="6868c-114">Een ExpressRoute-circuit verplaatsen</span><span class="sxs-lookup"><span data-stu-id="6868c-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="6868c-115">Stap 1: De details van het circuit vanuit het klassieke implementatiemodel Hallo verzamelen</span><span class="sxs-lookup"><span data-stu-id="6868c-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="6868c-116">Meld toohello klassieke Azure-omgeving en de servicesleutel Hallo verzamelen.</span><span class="sxs-lookup"><span data-stu-id="6868c-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="6868c-117">Meld u aan tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="6868c-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="6868c-118">Selecteer Hallo juiste Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6868c-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="6868c-119">Hallo PowerShell-modules importeren voor Azure en ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6868c-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="6868c-120">Gebruik onderstaande tooget Hallo service sleutels Hallo-cmdlet voor al uw ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="6868c-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="6868c-121">Na het Hallo-sleutels ophalen, kopiëren Hallo **servicesleutel** van Hallo-circuit dat u wilt dat toomove toohello Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6868c-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="6868c-122">Stap 2: Aanmelden en een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6868c-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="6868c-123">Meld u aan toohello Resource Manager-omgeving en een nieuwe resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="6868c-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="6868c-124">Meld u aan tooyour Azure Resource Manager-omgeving.</span><span class="sxs-lookup"><span data-stu-id="6868c-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="6868c-125">Selecteer Hallo juiste Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6868c-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="6868c-126">Hallo codefragment hieronder toocreate een nieuwe resourcegroep wijzigen als u nog een resourcegroep hebt.</span><span class="sxs-lookup"><span data-stu-id="6868c-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="6868c-127">Stap 3: Verplaats Hallo ExpressRoute-circuit toohello Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="6868c-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="6868c-128">U bent nu klaar toomove uw ExpressRoute-circuit vanuit Hallo classic deployment model toohello Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6868c-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="6868c-129">Controleer voordat u doorgaat, Hallo informatie in [een ExpressRoute-circuit verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="6868c-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="6868c-130">toomove uw circuit wijzigen en voer de volgende codefragment Hallo uit:</span><span class="sxs-lookup"><span data-stu-id="6868c-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="6868c-131">Nadat het Hallo verplaatsen is voltooid, worden nieuwe Hallo-naam die wordt vermeld in de vorige cmdlet Hallo gebruikte tooaddress Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="6868c-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="6868c-132">Hallo-circuit in wezen gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6868c-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="6868c-133">Circuit toegang wijzigen</span><span class="sxs-lookup"><span data-stu-id="6868c-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="6868c-134">ExpressRoute-circuit toegang voor beide implementatiemodellen tooenable</span><span class="sxs-lookup"><span data-stu-id="6868c-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="6868c-135">Na het verplaatsen van het klassieke ExpressRoute-circuit toohello Resource Manager-implementatiemodel, kunt u access tooboth implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="6868c-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="6868c-136">Voer Hallo tooboth implementatiemodellen voor cmdlets tooenable toegang te volgen:</span><span class="sxs-lookup"><span data-stu-id="6868c-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="6868c-137">Hallo circuit details ophalen.</span><span class="sxs-lookup"><span data-stu-id="6868c-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="6868c-138">'Klassieke bewerkingen toestaan' tooTRUE ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6868c-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="6868c-139">Hallo circuit bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6868c-139">Update hello circuit.</span></span> <span data-ttu-id="6868c-140">Nadat u deze bewerking is voltooid, kunt u zich kunt tooview Hallo circuit Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6868c-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="6868c-141">Hallo volgende cmdlet tooget Hallo details Hallo ExpressRoute-circuit worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6868c-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="6868c-142">U moet de sleutel kunnen toosee Hallo service vermeld zijn.</span><span class="sxs-lookup"><span data-stu-id="6868c-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="6868c-143">U kunt nu koppelingen toohello ExpressRoute-circuit met Hallo classic deployment model opdrachten voor klassieke vnet's en opdrachten voor Hallo-Resource Manager voor Resource Manager VNets beheren.</span><span class="sxs-lookup"><span data-stu-id="6868c-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="6868c-144">Hallo helpen volgende artikelen u bij het beheren van koppelingen toohello ExpressRoute-circuit:</span><span class="sxs-lookup"><span data-stu-id="6868c-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="6868c-145">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="6868c-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="6868c-146">Uw virtuele netwerk tooyour ExpressRoute-circuit in het klassieke implementatiemodel Hallo koppelen</span><span class="sxs-lookup"><span data-stu-id="6868c-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="6868c-147">toodisable ExpressRoute-circuit toegang toohello klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="6868c-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="6868c-148">Hallo na cmdlets toodisable toegang toohello klassieke implementatiemodel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6868c-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="6868c-149">Details van ExpressRoute-circuit Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="6868c-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="6868c-150">'Klassieke bewerkingen toestaan' tooFALSE ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6868c-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="6868c-151">Hallo circuit bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6868c-151">Update hello circuit.</span></span> <span data-ttu-id="6868c-152">Nadat u deze bewerking is voltooid, worden niet kunnen tooview Hallo circuit Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6868c-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="6868c-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6868c-153">Next steps</span></span>

* [<span data-ttu-id="6868c-154">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="6868c-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="6868c-155">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="6868c-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
