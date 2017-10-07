---
title: Traffic Manager-profielen aaaNested | Microsoft Docs
description: Dit artikel wordt uitgelegd Hallo 'Geneste profielen' functie van Azure Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Geneste Traffic Manager-profielen

Traffic Manager bevat een reeks verkeersroutering methoden waarmee u toocontrol hoe Traffic Manager kiest welk eindpunt verkeer van elke gebruiker ontvangt. Zie voor meer informatie [Traffic Manager-verkeersroutering methoden](traffic-manager-routing-methods.md).

Elke Traffic Manager-profiel geeft één verkeersroutering methode. Er zijn echter scenario's waarvoor meer geavanceerde voor verkeersroutering dan Hallo routering geleverd door een enkele Traffic Manager-profiel. U kunt het Traffic Manager profielen toocombine Hallo voordelen van meer dan één methode voor verkeersroutering nesten. Geneste profielen kunnen u toooverride Hallo standaard Traffic Manager gedrag toosupport grotere en complexere implementaties van toepassingen.

Hallo volgen voorbeelden laten zien hoe toouse genest Traffic Manager-profielen in verschillende scenario's.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Voorbeeld 1: Combineren 'Prestaties' en 'Gewogen' voor verkeersroutering

Stel dat u een toepassing in Azure-regio's te volgen Hallo geïmplementeerd: VS-West, West-Europa en Oost-Azië. U gebruikt de Traffic Manager 'Prestaties' verkeersroutering methode toodistribute verkeer toohello regio dichtstbijzijnde toohello gebruiker.

![Één Traffic Manager-profiel][4]

Stel nu dat u wenst tootest een update tooyour service voordat u veel meer rolling. Wilt u toouse Hallo 'gewogen' verkeersroutering methode toodirect een laag percentage verkeer tooyour testimplementatie. U instellen Hallo testimplementatie naast de bestaande productie-implementatie Hallo in West-Europa.

Beide 'gewogen' kan niet worden gecombineerd en '-verkeer routeren in één profiel. toosupport dit scenario maakt u een Traffic Manager-profiel met behulp van twee Hallo West-Europa eindpunten en Hallo 'Gewogen' verkeersroutering methode. Vervolgens voegt u dit profiel 'onderliggend item' als een eindpunt toohello 'parent'-profiel. Hallo bovenliggende profiel nog steeds gebruik van prestaties voor verkeersroutering methode Hallo en bevat Hallo andere algemene implementaties als eindpunten.

Hallo volgende diagram illustreert het volgende voorbeeld:

![Geneste Traffic Manager-profielen][2]

In deze configuratie is wordt omgeleid via Hallo bovenliggende profiel verkeer verkeer tussen regio's normaal. In West-Europa distribueert hello geneste profiel verkeer toohello productie- en eindpunten volgens toohello gewicht is toegewezen.

Als Hallo bovenliggende profiel Hallo 'Prestaties' verkeersroutering methode gebruikt, moet elk eindpunt een locatie worden toegewezen. Hallo-locatie wordt toegewezen wanneer u Hallo-eindpunt configureren. Kies hello Azure-regio die het dichtst tooyour implementatie. Hello zijn Azure-regio's Hallo locatie waarden die worden ondersteund door Hallo Internet latentie tabel. Zie voor meer informatie [Traffic Manager 'Prestaties' verkeersroutering methode](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Voorbeeld 2: Eindpuntcontrole in geneste profielen

Traffic Manager controleert actief Hallo status van elke service-eindpunt. Als een eindpunt beschadigd is, stuurt Traffic Manager gebruikers tooalternative eindpunten toopreserve Hallo beschikbaarheid van uw service. Deze controle en failover eindpuntgedrag geldt tooall verkeersroutering methoden. Zie voor meer informatie [Traffic Manager-eindpunt bewaking](traffic-manager-monitoring.md). Eindpuntcontrole werkt anders voor geneste profielen. Met geneste profielen uitvoeren Hallo bovenliggende profiel niet statuscontroles op Hallo onderliggende rechtstreeks. In plaats daarvan de status van de Hallo Hallo onderliggende profiel eindpunten gebruikte toocalculate is Hallo algemene status van Hallo onderliggende profiel. Deze informatie wordt doorgegeven Hallo genest profiel hiërarchie. Hallo bovenliggende profiel gebruikt deze toodetermine geaggregeerde status of toodirect verkeer toohello onderliggende profiel. Zie Hallo [Veelgestelde vragen over](traffic-manager-FAQs.md#traffic-manager-nested-profiles) voor volledige informatie over de statuscontrole van geneste profielen.

Retourneert het vorige voorbeeld toohello, stel Hallo productie-implementatie in West-Europa is mislukt. Standaard Hallo 'onderliggend item' profiel zorgt ervoor dat alle verkeer toohello testimplementatie op servers. Als de testimplementatie Hallo ook mislukt, wordt in Hallo bovenliggende profiel bepaalt dat Hallo onderliggende profiel niet moeten verkeer verschijnen zou omdat alle onderliggende eindpunten slecht zijn. Vervolgens distribueert Hallo bovenliggende profiel verkeer toohello andere regio's.

![Geneste profiel failover (standaardinstelling)][3]

Het is mogelijk dat u tevreden met deze benadering. Of u mogelijk betrokken al het verkeer voor West-Europa gaat nu toohello testimplementatie in plaats van een beperkte subset-verkeer. Ongeacht Hallo health Hallo implementatie testen, kunt u toofail via toohello andere regio's als Hallo productie-implementatie in West-Europa is mislukt. tooenable deze failover, kunt u Hallo 'MinChildEndpoints' parameter opgeven wanneer u Hallo onderliggende profiel configureert als een eindpunt in Hallo bovenliggende profiel. Hallo parameter bepaalt Hallo minimum aantal beschikbare eindpunten in Hallo onderliggende profiel. Hallo-standaardwaarde is '1'. Voor dit scenario stelt u Hallo MinChildEndpoints waarde too2. Onder deze drempelwaarde, Hallo bovenliggende profiel Hallo hele onderliggende profiel toobe niet beschikbaar beschouwt en zorgt ervoor dat verkeer toohello andere eindpunten.

Hallo volgende afbeelding ziet u deze configuratie:

![Profiel failover met 'MinChildEndpoints' genest = 2][4]

> [!NOTE]
> Hallo 'Prioriteit' verkeersroutering methode distribueert alle verkeer tooa één eindpunt. Er is dus weinig doel in een instelling voor MinChildEndpoints dan '1' voor een onderliggende-profiel.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Voorbeeld 3: Prioriteit failover gebieden in 'Prestaties' voor verkeersroutering

Hallo standaardgedrag voor Hallo 'Prestaties' verkeersroutering methode is ontworpen tooavoid laden hello te veel naast dichtstbijzijnde eindpunt en een trapsgewijze reeks fouten veroorzaken. Wanneer een eindpunt is mislukt, al het verkeer dat zou hebben is omgeleid toothat eindpunt gelijkmatig wordt verdeeld toohello andere eindpunten in alle regio's.

!['Prestaties'-verkeer met standaard failover-routering][5]

Stel u liever Hallo West-Europa verkeer failover tooWest ons en verkeer tooother regio's alleen directe wanneer beide eindpunten niet beschikbaar zijn. U kunt deze oplossing met behulp van een profiel voor een onderliggende Hello 'Prioriteit' verkeersroutering methode maken.

!['Prestaties'-verkeer met speciale failover-routering][6]

Aangezien Hallo West-Europa eindpunt heeft een hogere prioriteit dan Hallo VS-West eindpunt, wordt alle verkeer toohello West-Europa eindpunt verzonden wanneer beide eindpunten online zijn. Als West-Europa mislukt, is het verkeer gerichte tooWest VS. Hallo genest profiel is verkeer gerichte tooEast Azië alleen als zowel West-Europa en VS-West mislukken.

U kunt dit patroon herhalen voor alle regio's. Vervang alle drie eindpunten in Hallo bovenliggende profiel door drie onderliggende profielen elk voor een reeks prioriteit failover.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Voorbeeld 4: Beheren 'Prestaties'-verkeer routeren tussen meerdere eindpunten in Hallo dezelfde regio

Stel Hallo prestaties voor verkeersroutering methode wordt gebruikt in een profiel dat meer dan één eindpunt in een bepaald gebied is. Standaard verkeer omgeleid toothat regio gelijkmatig wordt verdeeld over alle beschikbare eindpunten in deze regio.

!['Prestaties' verkeer distributie van routering regio-verkeer (standaardinstelling)][7]

In plaats van meerdere eindpunten in West-Europa, worden deze eindpunten zijn ingesloten in een afzonderlijke onderliggende profiel. Hallo onderliggende profiel wordt toohello bovenliggende toegevoegd als Hallo alleen eindpunt in West-Europa. Hallo-instellingen op Hallo onderliggende profiel kunnen Hallo verkeer distributie met West-Europa beheren door in te schakelen op basis van prioriteit of gewogen verkeersroutering binnen deze regio.

![Routering met aangepaste regio-verkeer distributie 'Prestaties'-verkeer][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Voorbeeld 5: Per eindpunt controle-instellingen

Stel dat u migreren Traffic Manager toosmoothly verkeer van een verouderde on-premises website tooa nieuwe Cloud-gebaseerde versie gehost in Azure. Voor de oude site hello wilt u toouse Hallo startpagina URI toomonitor sitestatus. Maar voor Hallo nieuwe Cloud-gebaseerde versie, implementeert u een aangepaste pagina (pad ' / monitor.aspx') die worden extra controles uitgevoerd.

![Traffic Manager-eindpunt monitoring (standaardinstelling)][9]

Hallo controle-instellingen in een Traffic Manager-profiel toepassing tooall eindpunten binnen één profiel. Voor geneste profielen gebruikt u een andere onderliggende profiel per site toodefine verschillende controle-instellingen.

![Bewaking met de eindpuntinstellingen per Traffic Manager-eindpunt][10]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [Traffic Manager-profielen](traffic-manager-overview.md)

Meer informatie over hoe te[een Traffic Manager-profiel maken](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
