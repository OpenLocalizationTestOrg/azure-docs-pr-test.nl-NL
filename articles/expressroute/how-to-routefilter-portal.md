---
title: 'Routefilters voor Azure ExpressRoute Microsoft-peering configureren: Portal | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooconfigure routefilters voor het gebruik van Microsoft-Peering hello Azure-portal
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Routefilters voor Microsoft-peering configureren

Routefilters zijn een manier tooconsume een subset van de ondersteunde services via Microsoft-peering. Hallo stappen in dit artikel helpen u te configureren en beheren van routefilters voor ExpressRoute-circuits.

Dynamics 365-services en Office 365-services zoals Exchange Online, SharePoint Online en Skype voor bedrijven, zijn toegankelijk via Hallo Microsoft-peering. Wanneer Microsoft-peering in een ExpressRoute-circuit is geconfigureerd, worden alle voorvoegsels gerelateerde toothese-services worden geadverteerd via Hallo BGP-sessies die zijn gemaakt. Een BGP-communitywaarde is aangesloten tooevery voorvoegsel tooidentify Hallo service die wordt aangeboden via Hallo voorvoegsel. Zie voor een lijst met Hallo BGP-Communitywaarden en deze worden toegewezen aan Hallo-services, [BGP-community's](expressroute-routing.md#bgp).

Als u connectiviteit tooall services vereist, wordt een groot aantal voorvoegsels worden geadverteerd via BGP. Dit aanzienlijk groter Hallo Hallo routetabellen onderhouden door routers in uw netwerk. Als u van plan tooconsume slechts een subset van services die worden aangeboden bent via Microsoft-peering, kunt u de grootte van uw routetabellen op twee manieren Hallo reduceren. U kunt:

- Filter ongewenste voorvoegsels door routefilters zijn toegepast op de BGP-community's. Dit is een standaardprocedure voor netwerken en meestal wordt gebruikt binnen meerdere netwerken.

- Routefilters definiëren en ze tooyour ExpressRoute-circuit toepassen. Een routefilter is een nieuwe resource dat u kunt aangeven Hallo lijst met services die u van plan bent tooconsume via Microsoft-peering. ExpressRoute-routers verzenden alleen Hallo lijst met voorvoegsels die deel uitmaken van toohello services in Hallo routefilter geïdentificeerd.

### <a name="about"></a>Over routefilters

Wanneer Microsoft-peering is geconfigureerd op uw ExpressRoute-circuit, opzetten Hallo Microsoft randrouters een combinatie van BGP-sessies met Hallo-randrouters (jouw e-mailadres of uw connectiviteitsprovider). Er is geen routes worden aangekondigd tooyour netwerk. tooenable route-advertisements tooyour netwerk, moet u een routefilter koppelen.

Een routefilter kunt u identificeren van de services die u wilt dat tooconsume via Microsoft-peering voor uw ExpressRoute-circuit. Het is in wezen een witte lijst van alle Hallo BGP-Communitywaarden. Wanneer een bron routeren filter wordt gedefinieerd en tooan ExpressRoute-circuit gekoppeld, zijn alle voorvoegsels die zijn toegewezen toohello BGP-Communitywaarden aangekondigd tooyour netwerk.

toobe kunnen tooattach routefilters met Office 365-services zich bevinden, moet u autorisatie tooconsume Office 365-services via ExpressRoute hebben. Als u geen geautoriseerde tooconsume Office 365-services via ExpressRoute bent, mislukt de Hallo bewerking tooattach routefilters. Zie voor meer informatie over het autorisatieproces Hallo [Azure ExpressRoute voor Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Connectiviteit tooDynamics 365 services is niet vereist voor alle toestemming.

> [!IMPORTANT]
> Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd. Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.
> 
> 

### <a name="workflow"></a>Werkstroom

toobe kunnen toosuccessfully tooservices verbinding via Microsoft-peering, moet u de volgende configuratiestappen Hallo uitvoeren:

- U moet een actief ExpressRoute-circuit met Microsoft-peering ingerichte hebben. U kunt deze taken Hallo tooaccomplish instructies te volgen:
  - [Maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.
  - [Microsoft-peering maken](expressroute-howto-routing-portal-resource-manager.md) als u rechtstreeks Hallo BGP-sessie beheren. Of vraag uw connectiviteitsprovider Microsoft-peering voor uw circuit inrichten.

-  U moet maken en configureren van een routefilter.
    - Identificeren Hallo services die u met tooconsume via Microsoft-peering
    - Lijst van BGP-Communitywaarden die zijn gekoppeld aan services Hallo Hallo identificeren
    - Maak een regel tooallow Hallo voorvoegsel lijst overeenkomende Hallo BGP-Communitywaarden

-  Hallo route filter toohello ExpressRoute-circuit, moet u koppelen.

## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint met de configuratie, zorg er dan voor dat u voldoet aan Hallo volgende criteria:

 - Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

 - U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.

 - U hebt een actieve Microsoft-peering. Volg de instructies op [maken en wijzigen van peeringconfiguratie](expressroute-howto-routing-portal-resource-manager.md)


## <a name="prefixes"></a>Stap 1. Een lijst met voorvoegsels en BGP-Communitywaarden ophalen

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Een lijst met waarden van BGP-community

BGP-Communitywaarden die zijn gekoppeld aan services toegankelijk zijn via Microsoft-peering is beschikbaar in Hallo [routeringsvereisten voor ExpressRoute](expressroute-routing.md) pagina.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Maak een lijst van Hallo waarden die u toouse wilt

Maak een lijst van BGP-Communitywaarden die u wilt dat toouse in Hallo routefilter. Hallo BGP-communitywaarde voor Dynamics 365 services is een voorbeeld: 12076:5040.

## <a name="filter"></a>Stap 2. Maak een routefilter en een filterregel

Een routefilter kan slechts één regel, en Hallo regel moet van het type 'Toestaan'. Deze regel kan een lijst met BGP-Communitywaarden die zijn gekoppeld hebben.

### <a name="1-create-a-route-filter"></a>1. Maken van een routefilter
U kunt een routefilter maken door het selecteren van Hallo optie toocreate een nieuwe resource. Klik op **nieuw** > **Networking** > **RouteFilter**, zoals weergegeven in Hallo installatiekopie te volgen:

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

U moet Hallo routefilter plaatsen in een resourcegroep. 

![Maken van een routefilter](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Een filterregel maken

U kunt toevoegen en updateregels door het selecteren van Hallo regel tabblad voor de routefilter beheren.

![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Hallo services gewenste tooconnect toofrom Hallo vervolgkeuzelijst en opslaan van de regel Hallo wanneer u klaar bent, kunt u selecteren.

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Stap 3. Hallo route filter tooan ExpressRoute-circuit koppelen

Hallo 'Circuit toevoegen' knop selecteren en ExpressRoute-circuit Hallo selecteren in de vervolgkeuzelijst Hallo kunt Hallo route filter tooa circuit koppelen.

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>tooget hello eigenschappen van een routefilter

U kunt de eigenschappen van een routefilter weergeven wanneer u Hallo resource in Hallo portal opent.

![Maken van een routefilter](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>tooupdate hello eigenschappen van een routefilter

U kunt Hallo-lijst van BGP-community waarden gekoppelde tooa circuit bijwerken door Hallo 'beheren regel' knop te selecteren.


![Maken van een routefilter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Maken van een routefilter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>een routefilter van een ExpressRoute-circuit toodetach

toodetach een circuit van Hallo route-filter, klik met de rechtermuisknop op Hallo circuit en klik op 'losgekoppeld'.

![Maken van een routefilter](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>een routefilter toodelete

Als u de knop verwijderen Hallo selecteert, kunt u een routefilter verwijderen. 

![Maken van een routefilter](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
