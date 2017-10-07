---
title: aaaMoving ExpressRoute-circuits van klassieke tooResource Manager | Microsoft Docs
description: Deze pagina bevat een overzicht van wat u moet tooknow over het overbruggen van Hallo-classic en Hallo Resource Manager-implementatiemodel.
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>ExpressRoute-circuits verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel
Dit artikel bevat een overzicht van wat het betekent toomove een Azure ExpressRoute-circuit vanuit het Hallo-classic toohello Azure Resource Manager-implementatiemodel.

U kunt een enkel ExpressRoute-circuit tooconnect toovirtual netwerken die zijn geïmplementeerd in de klassieke Hallo en Hallo Resource Manager-implementatiemodel. Een ExpressRoute-circuit, ongeacht de manier waarop deze is gemaakt, kan nu toovirtual netwerken via beide implementatiemodellen koppelen.

![Een ExpressRoute-circuit die is gekoppeld aan toovirtual netwerken via beide implementatiemodellen](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>ExpressRoute-circuits die zijn gemaakt in het klassieke implementatiemodel Hallo
ExpressRoute-circuits die zijn gemaakt in het klassieke implementatiemodel Hallo moeten toobe verplaatst toohello Resource Manager deployment model eerste tooenable connectiviteit tooboth Hallo klassieke en het Hallo Resource Manager implementatiemodellen. Er is geen connectiviteitsonderbreking of -verlies wanneer een verbinding wordt verplaatst. Alle netwerkkoppelingen van circuit naar virtueel in het klassieke implementatiemodel hello (Hallo binnen hetzelfde abonnement en overlappend abonnement) blijven behouden.

Nadat Hallo verplaatsing is is voltooid, Hallo ExpressRoute-circuit zoekt, wordt uitgevoerd en werkt precies zoals een ExpressRoute-circuit dat is gemaakt in Hallo Resource Manager-implementatiemodel. U kunt nu verbindingen toovirtual netwerken maken in Hallo Resource Manager-implementatiemodel.

Nadat een ExpressRoute-circuit verplaatst toohello Resource Manager-implementatiemodel is, kunt u de levenscyclus Hallo Hallo ExpressRoute-circuit alleen met behulp van de Resource Manager-implementatiemodel Hallo beheren. Dit betekent dat u bewerkingen zoals het toevoegen/verwijderen van peerings, het bijwerken van circuiteigenschappen (zoals bandbreedte, SKU en factureringstype) en het verwijderen van circuits alleen in Hallo Resource Manager-implementatiemodel kunt uitvoeren. Raadpleeg onderstaande toohello sectie over circuits die zijn gemaakt in het Resource Manager-implementatiemodel Hallo voor meer informatie over hoe u toegang tooboth implementatiemodellen kunt beheren.

U beschikt niet over tooinvolve uw connectiviteit provider tooperform Hallo verplaatsen.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>ExpressRoute-circuits die zijn gemaakt in Hallo Resource Manager-implementatiemodel
U kunt ExpressRoute-circuits die zijn gemaakt in Hallo Resource Manager deployment model toobe toegankelijk vanuit beide implementatiemodellen kunt inschakelen. Elk ExpressRoute-circuit in uw abonnement kan worden ingeschakeld toobe toegankelijk vanuit beide implementatiemodellen.

* ExpressRoute-circuits die zijn gemaakt in Hallo Resource Manager-implementatiemodel hebt geen toegang tot toohello klassieke implementatiemodel standaard.
* ExpressRoute-circuits die zijn verplaatst van Hallo classic deployment model toohello Resource manager-implementatiemodel zijn toegankelijk vanuit beide implementatiemodellen standaard.
* Een ExpressRoute-circuit heeft altijd toegang toohello Resource Manager-implementatiemodel, ongeacht of deze is gemaakt in Hallo Resource Manager- of klassieke implementatiemodel. Dit betekent dat kunt u verbindingen toovirtual netwerken die zijn gemaakt in Hallo resourcemanager-implementatiemodel door de volgende instructies op [hoe virtuele netwerken toolink](expressroute-howto-linkvnet-arm.md).
* Toegang toohello klassieke implementatiemodel wordt gecontroleerd door Hallo **allowClassicOperations** parameter in Hallo ExpressRoute-circuit.

> [!IMPORTANT]
> Alle quota die zijn beschreven op Hallo [Servicelimieten](../azure-subscription-service-limits.md) pagina van toepassing. Als u bijvoorbeeld kunt een standaard circuit maximaal 10 virtuele netwerkkoppelingen /-verbindingen voor zowel klassieke Hallo als Hallo Resource Manager-implementatiemodel hebben.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Toegang toohello klassieke implementatiemodel beheren
U kunt een enkel ExpressRoute-circuit toolink toovirtual netwerken in beide implementatiemodellen inschakelen door de instelling Hallo **allowClassicOperations** parameter Hallo ExpressRoute-circuit.

Instelling **allowClassicOperations** tooTRUE kunt u toolink virtuele netwerken vanuit beide implementatie modellen toohello ExpressRoute-circuit. U kunt toovirtual netwerken in het klassieke implementatiemodel Hallo koppelen door de volgende richtlijnen op [hoe toolink virtuele netwerken in het klassieke implementatiemodel Hallo](expressroute-howto-linkvnet-classic.md). U kunt toovirtual netwerken in Hallo Resource Manager-implementatiemodel door de volgende richtlijnen te koppelen op [hoe toolink virtuele netwerken in Resource Manager-implementatiemodel Hallo](expressroute-howto-linkvnet-arm.md).

Instelling **allowClassicOperations** tooFALSE toegang blokkeert toohello circuit Hallo klassieke implementatiemodel. Alle koppelingen met virtuele netwerken in het klassieke implementatiemodel Hallo blijven echter behouden. In dit geval is Hallo ExpressRoute-circuit niet zichtbaar in het klassieke implementatiemodel Hallo.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Ondersteunde bewerkingen in het klassieke implementatiemodel Hallo
Hallo volgende klassieke bewerkingen worden ondersteund in een ExpressRoute circuit als **allowClassicOperations** tooTRUE is ingesteld:

* ExpressRoute-circuitgegevens verkrijgen
* Virtueel netwerk maken, bijwerken, verkrijgen/verwijderen koppelingen tooclassic virtuele netwerken
* Autorisaties voor koppelingen met virtuele netwerken voor abonnementoverschrijdende connectiviteit maken, bijwerken, verkrijgen en verwijderen

U kunt Hallo volgende klassieke bewerkingen niet uitvoeren wanneer **allowClassicOperations** tooTRUE is ingesteld:

* BGP-peerings (Border Gateway Protocol) maken, bijwerken, verkrijgen of verwijderen voor persoonlijke of openbare Azure-peerings en Microsoft-peerings
* ExpressRoute-circuits verwijderen

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Communicatie tussen Hallo-classic en Hallo Resource Manager-implementatiemodel
Hallo ExpressRoute-circuit fungeert als een brug tussen Hallo-classic en Hallo Resource Manager-implementatiemodel. Verkeer tussen virtuele machines in virtuele netwerken in het klassieke implementatiemodel Hallo en die in virtuele netwerken in Hallo Resource Manager-implementatiemodel stroomt via ExpressRoute als beide virtuele netwerken gekoppeld toohello zijn hetzelfde ExpressRoute-circuit.

Cumulatieve doorvoer wordt beperkt door Hallo doorvoercapaciteit van de virtuele netwerkgateway Hallo. Verkeer komt niet Hallo connectiviteitsprovider netwerken of uw netwerken in dergelijke gevallen invoeren. Verkeer tussen Hallo virtuele netwerken vindt volledig plaats in Hallo Microsoft-netwerk.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Toegang tooAzure openbare en Microsoft-peering bronnen
U kunt tooaccess resources die doorgaans toegankelijk zijn via openbare Azure-peering en Microsoft-peering zonder onderbreking blijven.  

## <a name="whats-supported"></a>Wat wordt er ondersteund
In deze sectie wordt beschreven wat er wordt ondersteund voor ExpressRoute-circuits:

* U kunt een enkel ExpressRoute-circuit tooaccess virtuele netwerken die zijn geïmplementeerd in Hallo-classic en Hallo Resource Manager-implementatiemodel.
* U kunt een ExpressRoute-circuit verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel. Nadat deze is verplaatst, Hallo ExpressRoute-circuit lijkt werkt en voert zoals elk ander ExpressRoute-circuit dat is gemaakt in Hallo Resource Manager-implementatiemodel.
* U kunt alleen Hallo ExpressRoute-circuit verplaatsen. Met deze bewerking kunt u geen circuitkoppelingen, virtuele netwerken of VPN-gateways verplaatsen.
* Nadat een ExpressRoute-circuit verplaatst toohello Resource Manager-implementatiemodel is, kunt u de levenscyclus Hallo Hallo ExpressRoute-circuit alleen met behulp van de Resource Manager-implementatiemodel Hallo beheren. Dit betekent dat u bewerkingen zoals het toevoegen/verwijderen van peerings, het bijwerken van circuiteigenschappen (zoals bandbreedte, SKU en factureringstype) en het verwijderen van circuits alleen in Hallo Resource Manager-implementatiemodel kunt uitvoeren.
* Hallo ExpressRoute-circuit fungeert als een brug tussen Hallo-classic en Hallo Resource Manager-implementatiemodel. Verkeer tussen virtuele machines in virtuele netwerken in het klassieke implementatiemodel Hallo en die in virtuele netwerken in Hallo Resource Manager-implementatiemodel stroomt via ExpressRoute als beide virtuele netwerken gekoppeld toohello zijn hetzelfde ExpressRoute-circuit.
* Abonnementoverschrijdende connectiviteit wordt ondersteund in zowel klassieke Hallo en Hallo Resource Manager-implementatiemodel.
* Nadat u een ExpressRoute-circuit van Hallo klassieke model toohello Azure Resource Manager-model verplaatsen, kunt u [migreren Hallo virtuele netwerken gekoppelde toohello ExpressRoute-circuit](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Wat wordt er niet ondersteund
In deze sectie wordt beschreven wat er niet wordt ondersteund voor ExpressRoute-circuits:

* Hallo levenscyclus van een ExpressRoute-circuit vanuit het klassieke implementatiemodel Hallo beheren.
* Op rollen gebaseerde toegangsbeheer (RBAC) ondersteuning voor het klassieke implementatiemodel Hallo. U kunt RBAC besturingselementen tooa circuit niet uitvoeren in het klassieke implementatiemodel Hallo. Een beheerder/CO van Hallo abonnement kunt koppelen aan of ontkoppelen van virtuele netwerken toohello circuit.

## <a name="configuration"></a>Configuratie
Hallo instructies die worden beschreven in [een ExpressRoute-circuit verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Volgende stappen
* [Hallo virtuele netwerken gekoppelde toohello ExpressRoute-circuit migreren van Hallo klassieke model toohello Azure Resource Manager-model](expressroute-migration-classic-resource-manager.md)
* Voor informatie over werkstromen raadpleegt u [ExpressRoute circuit provisioning workflows and circuit states](expressroute-workflows.md) (Werkstromen voor de inrichting van ExpressRoute-circuits en circuittoestanden).
* tooconfigure uw ExpressRoute-verbinding:
  
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-arm.md)
  * [Routering configureren](expressroute-howto-routing-arm.md)
  * [Koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)

