---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Resource Manager: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Maken en wijzigen van de peering voor een ExpressRoute-circuit

In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met hello Azure-portal. U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit. Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:


## <a name="configuration-prerequisites"></a>Configuratievereisten

* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets in de volgende secties Hallo.
* Als u van plan toouse een gedeelde sleutel/MD5-hash bent, worden toouse ervoor dat dit aan beide zijden van Hallo tunnel- en limit Hallo aantal tekens tooa maximaal 25.

Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden. Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u. 

> [!IMPORTANT]
> We momenteel doen nog geen peerings geconfigureerd door serviceproviders via Hallo service management portal. Deze mogelijkheid zal binnenkort worden ingeschakeld. Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.
> 
> 

U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren. U kunt peerings configureren in elke gewenste volgorde. Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.

## <a name="azure-private-peering"></a>Persoonlijke Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-private-peering"></a>toocreate persoonlijke Azure-peering

1. Hallo ExpressRoute-circuit configureren. Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u doorgaat.

  ![lijst](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configureer persoonlijke Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:

  * Een/30 subnet voor de primaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een/30 subnet voor de secundaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken. U kunt een persoonlijk AS-nummer voor deze peering gebruiken. Zorg dat u niet 65515 gebruikt.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.
3. Selecteer Hallo persoonlijke Azure rij voor peering, zoals weergegeven in het volgende voorbeeld Hallo:

  ![Persoonlijke](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Configureer persoonlijke Azure-peering. Hallo volgende afbeelding toont een configuratievoorbeeld van een:

  ![Configureer persoonlijke peering](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven. Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello voorbeeld te volgen:

  ![persoonlijke peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure persoonlijke peering details

U kunt weergeven Hallo eigenschappen van persoonlijke Azure-peering door Hallo peering te selecteren.

![persoonlijke peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure configuratie van persoonlijke peering

U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.

![persoonlijke peering bijwerken](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete persoonlijke Azure-peering

U kunt een peeringconfiguratie verwijderen door het verwijderingspictogram Hallo, zoals weergegeven in Hallo installatiekopie te volgen:

![persoonlijke peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Openbare Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-public-peering"></a>toocreate openbare Azure-peering

1. Configureer het ExpressRoute-circuit. Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u verder.

  ![openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configureer openbare Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:

  * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.
3. Selecteer hello Azure rij voor openbare peering, zoals wordt weergegeven in Hallo installatiekopie te volgen:

  ![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Configureer openbare Azure-peering. Hallo volgende afbeelding toont een configuratievoorbeeld van een:

  ![Configureer openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven. Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello voorbeeld te volgen:

  ![Configuratie van openbare peering opslaan](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure openbare peering details

U kunt weergeven Hallo eigenschappen van openbare Azure-peering door Hallo peering te selecteren.

![de eigenschappen van openbare peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>configuratie van openbare peering Azure tooupdate

U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.

![Selecteer de rij voor openbare peering](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete openbare Azure-peering

U kunt de peeringconfiguratie verwijderen door het verwijderingspictogram hello, zoals wordt weergegeven in het volgende voorbeeld Hallo:

![openbare peering verwijderen](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Microsoft-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.

> [!IMPORTANT]
> Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd. Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit. Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft-peering

1. Configureer het ExpressRoute-circuit. Zorg ervoor dat Hallo circuit volledig is ingericht door de connectiviteitsprovider Hallo voordat u verder.

  ![Microsoft-peering weergeven](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configureer Microsoft-peering voor Hallo circuit. Zorg ervoor dat er Hallo volgende informatie voordat u verder.

  * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
  * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
  * Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie. Alleen openbare IP-adresvoorvoegsels worden geaccepteerd. Als u een reeks voorvoegsels toosend plant, kunt u een door komma's gescheiden lijst verzenden. Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.
  * **Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn ingeschreven toohello peering als getal, kunt u Hallo opgeven als getal toowhich ze zijn geregistreerd.
  * Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.
3. U kunt selecteren Hallo peering tooconfigure gewenst, zoals wordt weergegeven in de volgende Hallo voorbeeld. Selecteer Hallo rij voor Microsoft-peering.

  ![Selecteer de rij voor Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Configureer Microsoft-peering. Hallo volgende afbeelding toont een configuratievoorbeeld van een:

  ![Configureer Microsoft-peering](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Hallo-configuratie op te slaan wanneer u alle parameters hebt opgegeven.

  Als het circuit tooa 'Validatie nodig' status (zoals in afbeelding Hallo), moet u een bewijs van eigendom van Hallo voorvoegsels tooour ondersteuningsteam ondersteuning ticket tooshow openen.

  ![Microsoft-peeringconfiguratie opslaan](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  U kunt een ondersteuningsticket openen rechtstreeks vanuit de portal hello, zoals wordt weergegeven in Hallo voorbeeld te volgen:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Nadat het Hallo-configuratie is geaccepteerd, ziet u iets dergelijks toohello installatiekopie te volgen:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>details van tooview Microsoft-peering

U kunt weergeven Hallo eigenschappen van openbare Azure-peering door Hallo peering te selecteren.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>configuratie van tooupdate Microsoft-peering

U kunt Hallo rij voor peering selecteren en aanpassen van eigenschappen Hallo-peering.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft-peering

U kunt een peeringconfiguratie verwijderen door het verwijderingspictogram Hallo, zoals weergegeven in Hallo installatiekopie te volgen:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Volgende stappen

Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md)
* Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).
* Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).
* Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.
