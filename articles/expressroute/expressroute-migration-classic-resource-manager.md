---
title: 'Migreren van virtuele netwerken die zijn gekoppeld ExpressRoute van klassieke tooResource Manager: Azure: PowerShell | Microsoft Docs'
description: Deze pagina wordt beschreven hoe toomigrate virtuele netwerken tooResource Manager gekoppeld na het verplaatsen van het circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Migreren van virtuele netwerken die zijn gekoppeld ExpressRoute van klassieke tooResource Manager

Dit artikel wordt uitgelegd hoe toomigrate Azure ExpressRoute virtuele netwerken vanuit Hallo classic deployment model toohello Azure Resource Manager-implementatiemodel gekoppeld na het verplaatsen van uw ExpressRoute-circuit. 


## <a name="before-you-begin"></a>Voordat u begint
* Controleer of u de meest recente versie Hallo van hello Azure PowerShell-modules. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* Hallo-informatie die is opgegeven onder [een ExpressRoute-circuit verplaatsen van klassieke tooResource Manager](expressroute-move.md). Zorg ervoor dat u volledig Hallo limieten en beperkingen begrijpt.
* Controleer of Hallo circuit in het klassieke implementatiemodel Hallo volledig operationeel is.
* Zorg ervoor dat u een resourcegroep die is gemaakt in Hallo Resource Manager-implementatiemodel.
* Hallo resource migratiedocumentatie volgende bekijken:

    * [Migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Veelgestelde vragen: Platform ondersteund migratie van IaaS-resources van klassieke tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Bekijk meest voorkomende migratiefouten en oplossingen](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Ondersteunde en niet-ondersteunde scenario 's

* Een ExpressRoute-circuit kan worden verplaatst vanaf Hallo klassieke toohello Resource Manager-omgeving zonder uitvaltijd. U kunt elk ExpressRoute-circuit verplaatsen van Hallo klassieke toohello Resource Manager-omgeving zonder uitvaltijd. Volg de instructies in Hallo [ExpressRoute-circuits verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel met behulp van PowerShell](expressroute-howto-move-arm.md). Dit is een vereiste toomove bronnen verbonden toohello virtueel netwerk.
* Virtuele netwerken, gateways en bijbehorende implementaties binnen het virtuele netwerk Hallo die zijn aangesloten tooan ExpressRoute-circuit in Hallo hetzelfde abonnement kan worden gemigreerd toohello Resource Manager-omgeving zonder uitvaltijd. Hallo stappen beschreven hoger toomigrate resources, zoals virtuele netwerken, gateways en virtuele machines die in het virtuele netwerk Hallo is geïmplementeerd, kunt u volgen. U moet ervoor zorgen dat de virtuele netwerken Hallo juist zijn geconfigureerd voordat ze worden gemigreerd. 
* Virtuele netwerken, gateways en bijbehorende implementaties in Hallo virtuele netwerk die zich niet in Hallo hetzelfde abonnement als Hallo ExpressRoute-circuit sommige uitvaltijd toocomplete Hallo migratie is vereist. Hallo laatste sectie van Hallo document beschrijft Hallo stappen toobe gevolgd toomigrate resources.
* Een virtueel netwerk met zowel de ExpressRoute-Gateway en de VPN-Gateway kan niet worden gemigreerd.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Een ExpressRoute-circuit verplaatsen van klassieke tooResource Manager
U moet verplaatsen, een ExpressRoute-circuit vanuit het Hallo-classic toohello Resource Manager-omgeving voordat u probeert toomigrate resources die zijn gekoppeld toohello ExpressRoute-circuit. tooaccomplish dit taak Zie Hallo artikelen te volgen:

* Hallo-informatie die is opgegeven onder [een ExpressRoute-circuit verplaatsen van klassieke tooResource Manager](expressroute-move.md).
* [Een circuit verplaatsen van klassieke tooResource Manager met Azure PowerShell](expressroute-howto-move-arm.md).
* Hello Azure Service Management portal gebruiken. U kunt Hallo werkstroom te volgen[maken van nieuwe ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en selecteer de optie importeren Hallo. 

Deze bewerking leidt tot uitvaltijd. Tijdens het Hallo-migratie wordt uitgevoerd, kunt u gegevens tussen uw lokale en Microsoft tootransfer blijven.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migreren van virtuele netwerken, gateways en bijbehorende implementaties

Hallo stappen volgen van toomigrate afhankelijk van of uw resources in Hallo zijn hetzelfde abonnement en/of verschillende abonnementen behoren.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Migreren van virtuele netwerken, gateways en bijbehorende implementaties in hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit
Deze sectie beschrijft Hallo stappen toobe gevolgd toomigrate een virtueel netwerk, gateway en bijbehorende implementaties in hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit. Er is geen downtime gekoppeld aan deze migratie. U kunt toouse blijven alle resources via Hallo-migratieproces. Hallo management vlak is vergrendeld terwijl Hallo migratie uitgevoerd wordt. 

1. Zorg ervoor dat Hallo ExpressRoute-circuit is verplaatst uit Hallo klassieke toohello Resource Manager-omgeving.
2. Zorg ervoor dat Hallo virtuele netwerk op de juiste wijze is voorbereid voor Hallo-migratie.
3. Registreer uw abonnement voor de Resourcemigratie. tooregister uw abonnement voor Resourcemigratie gebruik Hallo PowerShell-codefragment te volgen:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Valideren, voorbereiden en migreren. toomove hello virtueel netwerk, gebruik Hallo PowerShell-codefragment te volgen:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Ook kunt u de migratie door het uitvoeren van de volgende PowerShell-cmdlet Hallo afbreken:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Volgende stappen
* [Migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Veelgestelde vragen: Platform ondersteund migratie van IaaS-resources van klassieke tooAzure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Bekijk meest voorkomende migratiefouten en oplossingen](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
