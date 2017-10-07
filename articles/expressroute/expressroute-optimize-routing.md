---
title: 'ExpressRoute-routering optimaliseren: Azure | Microsoft Docs'
description: "Deze pagina bevat informatie over hoe toooptimize routering wanneer er meer dan één ExpressRoute-circuits die Microsoft verbinden met uw bedrijfsnetwerk."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>ExpressRoute-routering optimaliseren
Wanneer u meerdere ExpressRoute-circuits hebt, hebt u meer dan één pad tooconnect tooMicrosoft. Als gevolg hiervan suboptimale routering kan plaatsvinden - dat wil zeggen, het verkeer kan duren voordat een langer pad tooreach Microsoft, en Microsoft tooyour netwerk. Hallo langer Hallo netwerkpad, Hallo hogere Hallo latentie. Latentie heeft een directe invloed op toepassingsprestaties en gebruikerservaring. Dit artikel wordt dit probleem geïllustreerd en wordt uitgelegd hoe routering met toooptimize Hallo standaardrouteringstechnologieën.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Suboptimale routering van de klant tooMicrosoft
U gaat nu sluiten Hallo routeringsprobleem bekijken door een voorbeeld. Stel dat u hebt twee kantoren in Hallo VS, één in Los Angeles en één in New York. Uw kantoren zijn aangesloten op een Wide Area Network (WAN). Dit kan uw eigen backbone-netwerk zijn of het IP VPN van uw serviceprovider. U hebt twee ExpressRoute-circuits, één in VS-West en één in VS-Oost, die ook op Hallo WAN zijn verbonden. U hebt uiteraard twee paden tooconnect toohello Microsoft-netwerk. Stel nu dat u zowel in VS West als in VS Oost een Azure-implementatie hebt (bijvoorbeeld Azure App Service). Uw bedoeling is tooconnect uw gebruikers in Los Angeles tooAzure VS-West en uw gebruikers in New York tooAzure VS-Oost omdat uw servicebeheerder adverteert dat gebruikers in elke office access Hallo in de buurt van Azure services voor optimale ervaringen. Helaas werkt Hallo dit plan voor gebruikers van Hallo oostkust maar niet voor Hallo westkust gebruikers. Hallo is Hallo probleem te wijten aan Hallo volgende. Op elk ExpressRoute-circuit adverteren we tooyou zowel Hallo-voorvoegsel in Azure VS-Oost (23.100.0.0/16) en Hallo-voorvoegsel in Azure VS-West (13.100.0.0/16). Als u niet welk voorvoegsel bij welke regio hoort weet, bent u niet kunt tootreat deze anders. Uw WAN-netwerk kan denkt dat beide voorvoegsels Hallo zijn dichter tooUS Oost dan VS-West en daarom omgeleid beide office gebruikers toohello ExpressRoute-circuit in VS-Oost. Hallo-end hebt u veel ontevreden gebruikers in Hallo kantoor in Los Angeles.

![ExpressRoute geval 1 probleem - suboptimale routering van de klant tooMicrosoft](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Oplossing: gebruik BGP-community's
toooptimize routering voor gebruikers van beide kantoren, moet u tooknow welk voorvoegsel van Azure VS-West en die van Azure VS-Oost is. Deze informatie wordt versleuteld met [BGP-communitywaarden](expressroute-routing.md). We hebt een unieke BGP-Community waarde tooeach Azure-regio, bijvoorbeeld toegewezen '12076:51004' voor VS Oost en '12076:51006' voor VS West. Nu u weet welk voorvoegsel bij welke Azure-regio hoort, kunt u configureren welk ExpressRoute-circuit de voorkeur heeft. Omdat we BGP-tooexchange routeringsinformatie hello gebruiken, kunt u BGP van lokale-voorkeurswaarde tooinfluence routering. In ons voorbeeld kunt u een hogere lokale-voorkeurswaarde waarde too13.100.0.0/16 in VS-West dan in VS-Oost, en in een hogere lokale-voorkeurswaarde waarde too23.100.0.0/16 in VS-Oost dan in VS-West toewijzen. Deze configuratie zorgt ervoor dat, wanneer beide tooMicrosoft paden beschikbaar zijn, uw gebruikers in Los Angeles Hallo ExpressRoute-circuit in VS-West tooconnect tooAzure VS-West duurt dat uw gebruikers in New York Hallo ExpressRoute in VS-Oost tooAzure VS-Oost nemen . Routering is nu aan beide zijden geoptimaliseerd. 

![Oplossing Expressroute casus 1: BGP-community's gebruiken](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Hallo dezelfde techniek, met behulp van de lokale voorkeur, toegepaste toorouting van klant tooAzure virtueel netwerk kan worden. We coderen BGP-Community waarde toohello voorvoegsels die worden geadverteerd vanuit Azure tooyour netwerk niet. Echter, omdat u welke van uw implementatie van het virtuele netwerk sluiten toowhich van uw kantoor is weet, kunt u uw routers configureren dienovereenkomstig tooprefer één ExpressRoute-circuit tooanother.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Suboptimale routering van Microsoft toocustomer
Hier volgt een voorbeeld waarin verbindingen van Microsoft een langer pad tooreach uw netwerk nemen. In dit geval maakt u gebruik van on-premises Exchange-servers en Exchange Online in een [hybride omgeving](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Uw kantoren zijn verbonden tooa WAN. U adverteert de voorvoegsels Hallo van uw on-premises servers in beide uw kantoren tooMicrosoft via Hallo twee ExpressRoute-circuits. Start Exchange Online verbindingen toohello lokale servers in bijvoorbeeld postvakmigratie. Hallo verbinding tooyour kantoor in Los Angeles is helaas gerouteerde toohello ExpressRoute-circuit in VS-Oost voordat Hallo gehele continent back toohello westkust passeert. Hallo Hallo probleem wordt veroorzaakt vergelijkbare toohello eerst een. Zonder aanwijzingen weet Hallo Microsoft-netwerk niet welk klantvoorvoegsel sluiten tooUS Oost is en welke tooUS West sluiten. Dit gebeurt toopick Hallo Onjuiste padindeling tooyour kantoor in Los Angeles.

![ExpressRoute-voorbeeld 2 - suboptimale routering van Microsoft toocustomer](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Oplossing: AS-padtoevoeging
Er zijn twee oplossingen toohello probleem. Hallo eerst is een dat u gewoon uw on-premises voorvoegsel voor uw kantoor in Los Angeles, 177.2.0.0/31, op Hallo ExpressRoute-circuit in VS-West adverteert en uw on-premises voorvoegsel voor uw kantoor in New York, 177.2.0.2/31, op Hallo ExpressRoute-circuit in VS-Oost. Als gevolg hiervan is er slechts één pad voor Microsoft tooconnect tooeach kantoren. Er is geen dubbelzinnigheid en routering is geoptimaliseerd. Bij dit ontwerp moet u toothink over uw failoverstrategie voor. In Hallo gebeurtenis die Hallo pad tooMicrosoft via ExpressRoute wordt verbroken, moet u ervoor dat Exchange Online kunt nog steeds verbinding tooyour lokale servers toomake. 

de tweede oplossing Hallo is dat u doorgaan met tooadvertise van Hallo voorvoegsels op beide ExpressRoute-circuits en Daarnaast geeft u een hint welk voorvoegsel sluiten toowhich kantoren is. Omdat we BGP AS-padtoevoeging ondersteunen, kunt u Hallo AS-pad voor uw voorvoegsel tooinfluence routering configureren. U kunt in dit voorbeeld Hallo AS-pad voor 172.2.0.0/31 in VS-Oost verlengen zodat we wordt de voorkeur aan Hallo ExpressRoute-circuit in VS-West voor verkeer dat is bestemd voor dit voorvoegsel (omdat ons netwerk Hallo pad toothis voorvoegsel is korter in Hallo westen dat). U kunt ook Hallo AS-pad voor 172.2.0.2/31 in VS-West verlengen zodat we je liever Hallo ExpressRoute-circuit in VS-Oost. Routering is geoptimaliseerd voor beide kantoren. Als bij dit ontwerp één ExpressRoute-circuit wordt verbroken, kan Exchange Online u nog steeds bereiken via een ander ExpressRoute-circuit en uw WAN. 

> [!IMPORTANT]
> We verwijderen persoonlijke als getallen in Hallo AS-pad voor voorvoegsels Hallo op Microsoft-Peering ontvangen. U moet tooappend openbare AS-nummers in het Hallo AS-pad tooinfluence routering voor Microsoft-Peering.
> 
> 

![Oplossing ExpressRoute casus 2: Toevoeging van AS PATH gebruiken](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Hoewel Hallo voorbeelden hier opgegeven voor Microsoft- en openbare peerings, bieden we ondersteuning Hallo dezelfde mogelijkheden voor Hallo persoonlijke peering. Hallo AS-padtoevoeging werkt ook binnen een enkel ExpressRoute-circuit, tooinfluence Hallo selectie van de primaire en secundaire paden Hallo.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Suboptimale routering tussen virtuele netwerken
Met ExpressRoute, kunt u het virtuele netwerk tooVirtual netwerk (ook wel bekend als 'VNet') inschakelen communicatie door deze te koppelen tooan ExpressRoute-circuit. Wanneer u ze toomultiple ExpressRoute-circuits koppelen kan suboptimale routering gebeuren tussen Hallo VNets. Een voorbeeld. U hebt twee ExpressRoute-circuits, één in VS West en één in VS Oost. In elke regio hebt u twee VNets. Uw webservers zijn geïmplementeerd in een VNet en toepassingsservers in andere Hallo. Voor de redundantie, u koppeling Hallo twee VNets in elke regio tooboth Hallo lokale ExpressRoute-circuit en Hallo externe ExpressRoute-circuit. Zoals u hieronder kunt zien, uit elke VNet zijn er twee paden toohello andere VNet. Hallo VNets weet niet welk ExpressRoute-circuit is lokaal en welke regel is extern. Als gevolg daarvan als gelijk-kosten-Multi-Path (ECMP) routering tooload saldo inter VNet-verkeer, sommige verkeersstromen duurt langer pad Hallo en ophalen doorgestuurd op Hallo externe ExpressRoute-circuit.

![Probleem ExpressRoute casus 3: Suboptimale routering tussen virtuele netwerken](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Oplossing: een hoog gewicht toolocal verbinding toewijzen
Hallo-oplossing is eenvoudig. Omdat u waar de vnet's en Hallo circuits Hallo weet, u kunt laat ons weten welk pad voor elk VNet voorkeuren. Speciaal voor dit voorbeeld u een hogere gewicht toohello lokale verbinding dan verbinding met extern toohello toewijzen (Zie Hallo configuratievoorbeeld [hier](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Wanneer een VNet Hallo voorvoegsel Hallo ontvangt andere VNet op meerdere verbindingen deze wordt de voorkeur aan Hallo verbinding met de Hallo hoogste gewicht toosend verkeer dat is bestemd voor voorvoegsel.

![Oplossing voor ExpressRoute geval 3 - toewijzen hoog gewicht toolocal verbinding](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> U kunt ook de routering van VNet tooyour on-premises netwerk, als u meerdere ExpressRoute-circuits hebt met het gewicht van een verbinding in plaats van het toepassen van de AS-pad prepending, een techniek die wordt beschreven in het tweede scenario Hallo bovenstaande Hallo configureren beïnvloeden. Voor elke voorvoegsel altijd kijken we Hallo verbinding gewicht voordat Hallo AS padlengte bij het bepalen hoe toosend verkeer.
>
>
