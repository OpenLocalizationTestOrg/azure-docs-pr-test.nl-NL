---
title: aaaPerformance overwegingen voor Azure Traffic Manager | Microsoft Docs
description: Inzicht in prestaties op Traffic Manager en hoe tootest prestaties van uw website bij gebruik van Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Prestatieoverwegingen voor Traffic Manager

Deze pagina wordt uitgelegd Prestatieoverwegingen met Traffic Manager. Houd rekening met Hallo scenario te volgen:

U hebt de exemplaren van uw website in Hallo WestUS en Oost-Aziatische regio's. Een van de exemplaren Hallo is Hallo Statuscontrole voor de Hallo traffic manager-test mislukt. Verkeer van de toepassing is in orde gerichte toohello-regio. Deze failover wordt verwacht, maar prestaties op basis van Hallo latentie van Hallo verkeer nu tooa verafgelegen regio problematisch kan zijn.

## <a name="performance-considerations-for-traffic-manager"></a>Prestatieoverwegingen voor Traffic Manager

Hallo alleen invloed op de prestaties die Traffic Manager op uw website hebben kan is Hallo eerste DNS-zoekactie. Een DNS-aanvraag voor Hallo-naam van uw Traffic Manager-profiel wordt verwerkt door Hallo Microsoft DNS-basisserver die hosts Hallo trafficmanager.net zone. Traffic Manager gevuld en regelmatig van Hallo Microsoft DNS-hoofdmap servers op basis van Hallo Traffic Manager-beleid en Hallo test resultaten. Dus zelfs tijdens Hallo eerste DNS-zoekactie, worden er geen DNS-query's tooTraffic Manager verzonden.

Traffic Manager bestaat uit verschillende onderdelen: DNS-naam servers, een API-service, Hallo opslaglaag en een eindpunt bewaking van de service. Als een serviceonderdeel Traffic Manager is mislukt, heeft dit geen effect op Hallo DNS-naam die is gekoppeld aan uw Traffic Manager-profiel. Hallo-records in de Microsoft DNS-servers Hallo blijven ongewijzigd. Eindpuntcontrole en bijwerken van de DNS-echter niet gebeuren. Traffic Manager is daarom niet kunnen tooupdate DNS-toopoint tooyour failoversite wanneer uw primaire site uitvalt.

DNS-naamomzetting is snel en resultaten in de cache zijn opgeslagen. Hallo snelheid van het eerste DNS-zoekopdracht hello, is afhankelijk van Hallo DNS-servers Hallo client voor naamomzetting gebruikt. Een client kan normaal gesproken een DNS-zoekopdracht binnen ~ 50 ms voltooid. Hallo-resultaten van Hallo lookup in cache zijn opgeslagen voor de duur van Hallo Hallo DNS Time-to-live (TTL). Hallo standaard TTL-waarde voor Traffic Manager is 300 seconden.

Verkeer wordt niet uitgebreid via Traffic Manager. Zodra Hallo DNS-zoekopdracht is voltooid, heeft Hallo-client een IP-adres voor een exemplaar van uw website. Hallo client rechtstreeks verbinding maakt toothat adres en geeft niet via het Traffic Manager. Hallo Traffic Manager-beleid u heeft geen invloed op de Hallo DNS-prestaties. Een prestaties routering-methode kan echter nadelig Hallo toepassingservaring. Bijvoorbeeld, als uw beleid verkeer van Noord-Amerika tooan exemplaar gehost in Azië omleidingen, mogelijk Hallo netwerklatentie voor deze sessies een prestatieprobleem.

## <a name="measuring-traffic-manager-performance"></a>Meten van de prestaties van Traffic Manager

Er zijn meerdere websites kunt u toounderstand Hallo prestaties en het gedrag van een Traffic Manager-profiel. Veel van deze sites zijn gratis maar mogelijk beperkingen. Sommige sites bieden uitgebreide bewaking en rapportage voor een vast bedrag.

Hallo-hulpprogramma's op deze sites meten DNS latenties en weergave Hallo IP-adressen voor clientlocaties Hallo wereld opgelost. De meeste van deze hulpprogramma's niet opslaan in cache Hallo DNS-resultaten. Daarom weergeven Hallo extra Hallo volledige DNS-zoekopdracht telkens wanneer die een test wordt uitgevoerd. Wanneer u uw eigen client hebt getest, alleen ervaren Hallo volledige DNS-lookup prestaties één keer tijdens de duur van de TTL Hallo.

## <a name="sample-tools-toomeasure-dns-performance"></a>Voorbeeld extra toomeasure DNS-prestaties

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS biedt veel prestatiehulpprogramma's. Hallo vergelijking van de DNS-hulpprogramma kunt u zien hoe lang duurt het tooresolve uw DNS-naam en hoe die tooother DNS-serviceproviders worden vergeleken.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Een van de eenvoudigste tools Hallo is WebSitePulse. DNS-omzettingstijd voor Hallo URL toosee, eerste Byte, laatste Byte en andere prestatiestatistieken invoeren. U kunt kiezen uit drie verschillende testlocaties. In dit voorbeeld ziet u dat de eerste uitvoering Hallo blijkt dat DNS-lookup 0.204 per seconde heeft.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Omdat resultaten in cache zijn opgeslagen, Hallo Hallo tweede test voor dezelfde Traffic Manager-eindpunt Hallo DNS-zoekopdracht Hallo duurt 0.002 per seconde.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA-App synthetische Monitor](https://asm.ca.com/en/checkit.php)

    Deze site voorheen bekend als Hallo Watchmouse selectievakje Website hulpprogramma, ziet u Hallo DNS-omzetting tijd tegelijkertijd uit meerdere geografische regio's. Voer Hallo URL toosee DNS-omzettingstijd, verbindingstijd en snelheid van verschillende geografische locaties. Gebruik deze test toosee welke gehoste service is geretourneerd voor verschillende locaties Hallo wereld.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Dit hulpprogramma biedt prestatiestatistieken weer voor elk element van een webpagina. Hallo analyse van de pagina tabblad toont Hallo percentage tijd op de DNS-zoekactie.

* [Wat is mijn DNS?](http://www.whatsmydns.net/)

    Deze site heeft een DNS-zoekopdracht vanaf verschillende locaties 20 en Hallo resultaten weergeven op een kaart.

* [Kennis van Web-Interface](http://www.digwebinterface.com)

    Deze site geeft dat meer gedetailleerde DNS-informatie, met inbegrip van CNAMEs en A-records. Zorg ervoor dat u Hallo 'vullen met kleur uitvoer' en 'Statistieken' onder opties controleren en selecteert 'All' onder Nameservers.

## <a name="next-steps"></a>Volgende stappen

[Over verkeersrouteringsmethoden voor Traffic Manager](traffic-manager-routing-methods.md)

[Testen van uw Traffic Manager-instellingen](traffic-manager-testing-settings.md)

[Bewerkingen op Traffic Manager (REST API-referentiemateriaal)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager-Cmdlets](http://go.microsoft.com/fwlink/p/?LinkId=400769)

