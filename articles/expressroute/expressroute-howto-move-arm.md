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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>ExpressRoute-circuits verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel met behulp van PowerShell

toouse een ExpressRoute-circuit voor zowel klassieke Hallo als Resource Manager-implementatiemodel, moet u Hallo circuit toohello Resource Manager-implementatiemodel verplaatsen. Hallo volgende secties helpen u uw circuit verplaatsen met behulp van PowerShell.

## <a name="before-you-begin"></a>Voordat u begint

* Controleer of u de meest recente versie Hallo van hello Azure PowerShell-modules (ten minste versie 1.0). Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* Hallo-informatie die is opgegeven onder [een ExpressRoute-circuit verplaatsen van klassieke tooResource Manager](expressroute-move.md). Zorg ervoor dat u volledig Hallo limieten en beperkingen begrijpt.
* Controleer of Hallo circuit in het klassieke implementatiemodel Hallo volledig operationeel is.
* Zorg ervoor dat u een resourcegroep die is gemaakt in Hallo Resource Manager-implementatiemodel.

## <a name="move-an-expressroute-circuit"></a>Een ExpressRoute-circuit verplaatsen

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Stap 1: De details van het circuit vanuit het klassieke implementatiemodel Hallo verzamelen

Meld toohello klassieke Azure-omgeving en de servicesleutel Hallo verzamelen.

1. Meld u aan tooyour Azure-account.

  ```powershell
  Add-AzureAccount
  ```

2. Selecteer Hallo juiste Azure-abonnement.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Hallo PowerShell-modules importeren voor Azure en ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Gebruik onderstaande tooget Hallo service sleutels Hallo-cmdlet voor al uw ExpressRoute-circuits. Na het Hallo-sleutels ophalen, kopiëren Hallo **servicesleutel** van Hallo-circuit dat u wilt dat toomove toohello Resource Manager-implementatiemodel.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Stap 2: Aanmelden en een resourcegroep maken

Meld u aan toohello Resource Manager-omgeving en een nieuwe resourcegroep maken.

1. Meld u aan tooyour Azure Resource Manager-omgeving.

  ```powershell
  Login-AzureRmAccount
  ```

2. Selecteer Hallo juiste Azure-abonnement.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Hallo codefragment hieronder toocreate een nieuwe resourcegroep wijzigen als u nog een resourcegroep hebt.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Stap 3: Verplaats Hallo ExpressRoute-circuit toohello Resource Manager-implementatiemodel

U bent nu klaar toomove uw ExpressRoute-circuit vanuit Hallo classic deployment model toohello Resource Manager-implementatiemodel. Controleer voordat u doorgaat, Hallo informatie in [een ExpressRoute-circuit verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-move.md).

toomove uw circuit wijzigen en voer de volgende codefragment Hallo uit:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Nadat het Hallo verplaatsen is voltooid, worden nieuwe Hallo-naam die wordt vermeld in de vorige cmdlet Hallo gebruikte tooaddress Hallo resource. Hallo-circuit in wezen gewijzigd.
> 

## <a name="modify-circuit-access"></a>Circuit toegang wijzigen

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>ExpressRoute-circuit toegang voor beide implementatiemodellen tooenable

Na het verplaatsen van het klassieke ExpressRoute-circuit toohello Resource Manager-implementatiemodel, kunt u access tooboth implementatiemodellen. Voer Hallo tooboth implementatiemodellen voor cmdlets tooenable toegang te volgen:

1. Hallo circuit details ophalen.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. 'Klassieke bewerkingen toestaan' tooTRUE ingesteld.

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Hallo circuit bijwerken. Nadat u deze bewerking is voltooid, kunt u zich kunt tooview Hallo circuit Hallo klassieke implementatiemodel.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Hallo volgende cmdlet tooget Hallo details Hallo ExpressRoute-circuit worden uitgevoerd. U moet de sleutel kunnen toosee Hallo service vermeld zijn.

  ```powershell
  get-azurededicatedcircuit
  ```

5. U kunt nu koppelingen toohello ExpressRoute-circuit met Hallo classic deployment model opdrachten voor klassieke vnet's en opdrachten voor Hallo-Resource Manager voor Resource Manager VNets beheren. Hallo helpen volgende artikelen u bij het beheren van koppelingen toohello ExpressRoute-circuit:

    * [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel](expressroute-howto-linkvnet-arm.md)
    * [Uw virtuele netwerk tooyour ExpressRoute-circuit in het klassieke implementatiemodel Hallo koppelen](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute-circuit toegang toohello klassieke implementatiemodel

Hallo na cmdlets toodisable toegang toohello klassieke implementatiemodel worden uitgevoerd.

1. Details van ExpressRoute-circuit Hallo ophalen.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. 'Klassieke bewerkingen toestaan' tooFALSE ingesteld.

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Hallo circuit bijwerken. Nadat u deze bewerking is voltooid, worden niet kunnen tooview Hallo circuit Hallo klassieke implementatiemodel.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Volgende stappen

* [Maken en aanpassen van routering voor ExpressRoute-circuit](expressroute-howto-routing-arm.md)
* [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)
