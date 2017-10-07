---
title: aaaWorkflows voor het configureren van een ExpressRoute-circuit | Microsoft Docs
description: Deze pagina wordt u begeleid bij Hallo werkstromen voor het configureren van ExpressRoute-circuit en -peerings
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>ExpressRoute-werkstromen voor circuitinrichting en -statussen
Deze pagina wordt u begeleid Hallo service-inrichting en routering configuration werkstroom op hoog niveau.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Hallo volgende afbeelding en de bijbehorende stappen Hallo taken weergeven dat moet u een ExpressRoute-circuit ingerichte end-to-end in de volgorde toohave volgen. 

1. Gebruik PowerShell tooconfigure een ExpressRoute-circuit. Volg de instructies Hallo in Hallo [maken ExpressRoute-circuits](expressroute-howto-circuit-classic.md) artikel voor meer informatie.
2. De verbinding van de volgorde van Hallo-provider. Dit proces is. Neem contact op met uw connectiviteitsprovider voor meer informatie over het tooorder connectiviteit.
3. Zorg ervoor dat Hallo circuit is ingericht met succes gecontroleerd of ExpressRoute-circuit Hallo Inrichtingsstatus via PowerShell. 
4. Configureer Routeringsdomeinen. Als uw connectiviteitsprovider beheert de Layer 3 voor u, zal ze configureren voor uw circuit routering. Als uw connectiviteitsprovider alleen Layer 2-services biedt, moet u routering per richtlijnen die worden beschreven in Hallo [routeringsvereisten](expressroute-routing.md) en [routeringsconfiguratie](expressroute-howto-routing-classic.md) pagina's.
   
   * Inschakelen van persoonlijke Azure-peering - u moet deze peering tooconnect tooVMs inschakelen / cloudservices geïmplementeerd in virtuele netwerken.
   * Inschakelen van openbare Azure-peering - u openbare Azure-peering moet inschakelen indien u wenst dat tooconnect tooAzure services die worden gehost op openbare IP-adressen. Dit is een vereiste tooaccess Azure-resources als u ervoor tooenable standaardroutering gekozen hebt voor persoonlijke Azure-peering.
   * Schakel Microsoft-peering - u moet deze tooaccess Office 365 en Dynamics 365 inschakelen. 
     
     > [!IMPORTANT]
     > U moet ervoor zorgen dat u een afzonderlijke proxy gebruiken / edge tooconnect tooMicrosoft dan het account dat u gebruikt voor Hallo Hallo Internet. Hallo dezelfde rand voor ExpressRoute- en Hallo Internet wordt veroorzaken asymmetrische Routering en connectiviteit uitval voor uw netwerk worden gebruikt.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Koppelen van virtuele netwerken tooExpressRoute circuits - kunt u virtuele netwerken tooyour ExpressRoute-circuit koppelen. Volg de instructies [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit. Deze VNets kan zijn in dezelfde Azure-abonnement als Hallo ExpressRoute-circuit Hallo of kunnen zich in een ander abonnement.

## <a name="expressroute-circuit-provisioning-states"></a>ExpressRoute-circuit inrichtingstatuswaarden
Elk ExpressRoute-circuit heeft twee statussen:

* Serviceprovider Inrichtingsstatus
* Status

Status vertegenwoordigt van Microsoft-Inrichtingsstatus. Deze eigenschap wordt tooEnabled ingesteld wanneer u een Expressroute-circuit maken

Hallo connectiviteit provider Inrichtingsstatus vertegenwoordigt de status Hallo Hallo connectiviteit van de provider-zijde. Het kan zijn *NotProvisioned*, *inrichten*, of *ingericht*. Hallo ExpressRoute-circuit moet worden ingericht voor u toobe kunnen toouse deze.

### <a name="possible-states-of-an-expressroute-circuit"></a>Mogelijke statussen van een ExpressRoute-circuit
Deze sectie vindt u uit Hallo mogelijke statussen voor een ExpressRoute-circuit.

**Tijdens het maken**

Hier ziet u Hallo ExpressRoute-circuit in Hallo zodra u de status na Hallo PowerShell cmdlet toocreate hello ExpressRoute-circuit worden uitgevoerd.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Wanneer de connectiviteitsprovider in Hallo-proces voor het leveren van Hallo circuit is**

U ziet Hallo ExpressRoute-circuit in Hallo zodra u de status na sleutel toohello Hallo-connectiviteit serviceprovider doorgeven en ze Hallo inrichtingsproces hebt gestart.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Wanneer de connectiviteitsprovider Hallo inrichtingsproces is voltooid**

U ziet Hallo ExpressRoute-circuit in Hallo status volgen als u de connectiviteitsprovider Hallo Hallo inrichtingsproces is voltooid.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Ingericht en ingeschakeld is Hallo status Hallo circuit kan slechts voor u toobe kunnen toouse deze worden. Als u een Layer 2-provider gebruikt, kunt u configureren routering voor uw circuit alleen wanneer deze status heeft.

**Wanneer de connectiviteitsprovider Hallo circuit is laagsjabloon**

Als u Hallo serviceprovider toodeprovision hello ExpressRoute-circuit is aangevraagd, ziet u Hallo circuit ingesteld toohello status te volgen nadat het Hallo-serviceprovider Hallo opheffen van inrichting proces is voltooid.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


U kunt toore inschakelen als, of de PowerShell-cmdlets uitvoeren toodelete Hallo circuit.  

> [!IMPORTANT]
> Als u mislukt Hallo PowerShell cmdlet toodelete Hallo circuit wanneer Hallo ServiceProviderProvisioningState Provisioning of ingericht Hallo-bewerking is. Neem contact op met uw netwerkverbinding provider toodeprovision hello ExpressRoute-circuit eerst en verwijder vervolgens Hallo circuit. Microsoft blijft toobill Hallo circuit totdat u Hallo PowerShell cmdlet toodelete Hallo circuit uitvoert.
> 
> 

## <a name="routing-session-configuration-state"></a>Configuratie van routering sessiestatus
Hallo BGP Inrichtingsstatus laat u weten als Hallo BGP-sessie op de Microsoft edge Hallo is ingeschakeld. Hallo staat moet zijn ingeschakeld voor u toobe kunnen toouse hello peering.

Het is belangrijk toocheck Hallo BGP-sessiestatus met name voor Microsoft-peering. Toevoeging toohello BGP inrichting status heeft, wordt een andere status aangeroepen *aangekondigde openbare voorvoegsels status*. Hallo aangekondigde openbare voorvoegsels status moet *geconfigureerd* state, zowel voor Hallo BGP-sessie toobe omhoog als voor de routering toowork end-to-end. 

Als Hallo aangekondigd openbaar voorvoegsel status ingesteld op tooa *validatie nodig* staat, Hallo BGP-sessie niet is ingeschakeld, Hallo geadverteerde voorvoegsels komt niet overeen met de Hallo AS-nummer in een Hallo routeringsregisters. 

> [!IMPORTANT]
> Als Hallo openbare voorvoegsels status aangekondigde is in *handmatige validatie* staat, moet u een ondersteuningsticket met openen [Microsoft ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en bewijzen dat u Hallo IP-adressen bezit langs aangekondigd Hello autonoom systeemnummer die is gekoppeld.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Configureer uw ExpressRoute-verbinding.
  
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-arm.md)
  * [Routering configureren](expressroute-howto-routing-arm.md)
  * [Koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)

