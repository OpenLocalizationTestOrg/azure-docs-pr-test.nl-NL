---
title: verkeersrouteringsmethoden voor Traffic Manager - aaaAzure | Microsoft Docs
description: Hiermee artikelen geeft die u inzicht in Hallo verschillende verkeersrouteringsmethoden gebruikt door Traffic Manager
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Methoden voor het doorsturen van Traffic Manager

Azure Traffic Manager ondersteunt vier verkeersroutering methoden toodetermine hoe tooroute netwerk verkeer toohello verschillende service-eindpunten. Traffic Manager is van toepassing hello verkeersroutering methode tooeach DNS-query die wordt ontvangen. Hallo verkeersroutering methode bepaalt welk eindpunt in Hallo DNS-antwoord geretourneerd.

Er zijn vier methoden voor het doorsturen van verkeer beschikbaar in Traffic Manager:

* **[Prioriteit](#priority):** Selecteer **prioriteit** als u wilt toouse een primaire service-eindpunt voor al het verkeer en back-ups bieden voor het geval Hallo primaire of back-up Hallo-eindpunten niet beschikbaar zijn.
* **[Gewogen](#weighted):** Selecteer **gewogen** als u wilt dat toodistribute verkeer van een set eindpunten, ofwel gelijkmatig of volgens tooweights die u definieert.
* **[Prestaties](#performance):** Selecteer **prestaties** wanneer u eindpunten op verschillende geografische locaties en u wilt dat eindgebruikers toouse Hallo 'dichtstbijzijnde' eindpunt in termen van de laagste netwerklatentie Hallo.
* **[Geografische](#geographic):** Selecteer **geografische** zodat gebruikers gerichte toospecific eindpunten (Azure, extern of geneste) op basis van welke geografische locatie hun DNS-query is afkomstig uit. Dit machtigt Traffic Manager klanten tooenable scenario's waarin de geografische regio van de gebruiker weet en routering toe op basis van die belangrijke. Voorbeelden zijn die voldoet aan gegevens onafhankelijkheid vereist, lokalisatie van inhoud & gebruiker ervaring en verkeer vanuit verschillende regio's te meten.

Alle Traffic Manager-profielen bevatten bewaking van endpoint-status- en eindpunt automatische failover. Zie voor meer informatie [Traffic Manager-eindpunt bewaking](traffic-manager-monitoring.md). Een enkele Traffic Manager-profiel kunt slechts één methode voor het doorsturen van verkeer. U kunt een andere verkeersrouteringsmethode selecteren voor uw profiel op elk gewenst moment. Wijzigingen worden toegepast binnen één minuut en er geen uitvaltijd is ontstaan. Voor verkeersroutering methoden kunnen worden gecombineerd met behulp van geneste Traffic Manager-profielen. Geneste kunt geavanceerde en flexibele verkeersroutering configuraties die behoeften van Hallo van grotere, complexe toepassingen. Zie voor meer informatie [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md).

## <a name = "priority"></a>Prioriteit voor verkeersroutering methode

Een organisatie wil vaak tooprovide betrouwbaarheid voor de services door het implementeren van een of meer back-services als hun primaire service uitvalt. Hallo 'Prioriteit' verkeersroutering methode Azure kunnen klanten tooeasily dit patroon failover implementeren.

![Azure Traffic Manager 'Prioriteit' verkeersroutering methode][1]

Hallo Traffic Manager-profiel bevat een geprioriteerde lijst van de service-eindpunten. Traffic Manager verzendt standaard alle verkeer toohello primaire (hoogste prioriteit) eindpunt. Als de primaire Hallo-eindpunt is niet beschikbaar, Hallo Traffic Manager routes verkeer toohello tweede eindpunt. Als beide Hallo primaire en secundaire eindpunten niet beschikbaar zijn, gaat het Hallo-verkeer toohello derde, enzovoort. Beschikbaarheid van het Hallo-eindpunt is gebaseerd op Hallo geconfigureerd status (ingeschakeld of uitgeschakeld) en Hallo lopende eindpuntcontrole.

### <a name="configuring-endpoints"></a>Eindpunten configureren

Met Azure Resource Manager u Hallo eindpuntprioriteit expliciet met behulp van de eigenschap 'prioriteit' Hallo voor elk eindpunt configureren. Deze eigenschap is een waarde tussen 1 en 1000. Lagere waarden vertegenwoordigen een hogere prioriteit. Eindpunten kunnen geen prioriteitswaarden delen. Hallo-eigenschap is optioneel. Wanneer u dit weglaat, wordt een standaardprioriteit op basis van Hallo eindpunt volgorde gebruikt.

##<a name = "weighted"></a>Gewogen verkeersroutering methode
Hallo 'Gewogen' verkeersroutering methode kunt u toodistribute verkeer gelijkmatig of een vooraf gedefinieerde weging toouse.

![Azure Traffic Manager-'Gewogen' methode verkeer routering][2]

In Hallo gewogen verkeersroutering methode, moet u een eindpunt van de tooeach gewicht in Hallo Traffic Manager-profielconfiguratie toewijzen. Hallo gewicht is een geheel getal tussen 1 too1000. Deze parameter is optioneel. Als u dit weglaat, wordt verkeer Managers een standaardgewicht van '1'.

Voor elke DNS-query heeft ontvangen, kiest de Traffic Manager willekeurig een beschikbare eindpunt. Hallo waarschijnlijkheid van het kiezen van een eindpunt is gebaseerd op Hallo gewichten tooall beschikbare eindpunten toegewezen. Hallo met hetzelfde gewicht over alle eindpunten resulteert in een zelfs distributie van verkeer. Met behulp van hogere of lagere gewichten op specifieke eindpunten zorgt ervoor dat deze eindpunten toobe meer of minder vaak in Hallo DNS-antwoorden worden geretourneerd.

Hallo gewogen maakt een nuttig scenario's:

* Upgrade van de toepassing geleidelijk: een percentage van het verkeer tooroute tooa nieuwe eindpunt toewijzen en Hallo verkeer geleidelijk te verhogen over tijd too100%.
* Toepassing migratie tooAzure: een profiel maken met Azure en externe eindpunten. Hallo-gewicht van Hallo eindpunten tooprefer Hallo nieuwe eindpunten aanpassen.
* Cloud sturen voor extra capaciteit: snel een on-premises implementatie naar cloud Hallo uitbreiden door de gegevens achter een Traffic Manager-profiel. Wanneer u extra capaciteit in de cloud hello, kunt u toevoegen of meer eindpunten inschakelen en geef op welk gedeelte van het verkeer gaat tooeach eindpunt.

Hello Azure Resource Manager-portal ondersteunt de configuratie van Hallo gewogen verkeer routering.  U kunt gewichten Hallo Resource Manager-versies van Azure PowerShell, CLI en Hallo REST-API's configureren.

Het is belangrijk toounderstand dat DNS-antwoorden in de cache zijn opgeslagen door clients en door Hallo recursieve DNS-servers die clients Hallo tooresolve DNS-namen gebruiken. Deze cache, kan een invloed hebben op gewogen verkeer distributies. Wanneer Hallo aantal clients en de recursieve DNS-servers groot is, wordt verkeer distributie werkt zoals verwacht. Echter, als Hallo aantal clients of recursieve DNS-servers klein is, caching kan aanzienlijk laten uitvallen Hallo verkeer distributie.

Algemene gebruiksvoorbeelden zijn onder andere:

* Ontwikkeling en testomgevingen
* Toepassingen communicatie
* Toepassingen die gericht is op een beperkte-gebruikersgroep die delen een gemeenschappelijke recursieve DNS-infrastructuur (bijvoorbeeld medewerkers van de bedrijfsportal verbinding maken via een proxy)

Deze DNS-cache-effecten zijn algemene tooall DNS-verkeer routeren systemen, niet alleen Azure Traffic Manager. In sommige gevallen kan expliciet wissen Hallo DNS-cache bieden een tijdelijke oplossing. In andere gevallen is zijn een alternatieve methode voor verkeersroutering geschikter.

## <a name = "performance"></a>Prestaties voor verkeersroutering methode

Eindpunten in twee of meer locaties implementeren via Hallo wereld kan Hallo reactiesnelheid van veel toepassingen met behulp van routing verkeer toohello locatie die is 'dichtstbijzijnde' tooyou verbeteren. Hallo 'Prestaties' verkeersroutering methode biedt deze mogelijkheid.

![Azure Traffic Manager 'Prestaties' verkeersroutering methode][3]

'dichtstbijzijnde' Hallo-eindpunt is niet noodzakelijkerwijs dichtstbijzijnde door geografische afstand wordt gemeten. In plaats daarvan bepaalt Hallo 'Prestaties' verkeersroutering methode Hallo dichtstbijzijnde eindpunt door te meten netwerklatentie. Traffic Manager onderhoudt een Internet latentie tabel tootrack Hallo round trip tijd tussen het IP-adresbereiken en elke Azure-datacenter.

Traffic Manager worden opgezocht Hallo IP-bronadres van Hallo inkomende DNS-aanvraag in Hallo Internet latentie tabel. Traffic Manager kiest een beschikbare eindpunt in hello Azure-datacenter die heeft de laagste latentie Hallo voor deze IP-adresbereik, en vervolgens dat eindpunt in Hallo DNS-antwoord geretourneerd.

Zoals uitgelegd in [hoe Traffic Manager werkt](traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager ontvangt geen DNS-query's rechtstreeks van clients. In plaats daarvan DNS-query's zijn afkomstig Hallo recursieve DNS-service dat Hallo-clients geconfigureerde toouse zijn. Daarom hello IP-adres dat wordt gebruikt toodetermine Hallo 'dichtstbijzijnde' eindpunt is niet van de client Hallo IP-adres, maar het Hallo IP-adres van Hallo recursieve DNS-service is. Dit IP-adres is in de praktijk kan een goede proxy voor Hallo-client.


Traffic Manager regelmatig updates Hallo Internet latentie tabel tooaccount voor wijzigingen in Hallo globale Internet en nieuwe Azure-regio's. Echter afhankelijk de prestaties van toepassingen van realtime variaties in load over Hallo Internet. Verkeer routeren bewaakt belasting van een bepaalde service-eindpunt niet. Echter, als een eindpunt niet beschikbaar is, Traffic Manager biedt niet opnemen in reacties op DNS-query's.


Toonote punten:

* Als uw profiel bevat meerdere eindpunten in dezelfde Azure-regio, Hallo vervolgens Traffic Manager verkeer gelijkmatig over Hallo beschikbare eindpunten in deze regio wordt. Als u liever een ander verkeer distributie binnen een regio, kunt u [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md).
* Als alle eindpunten in de dichtstbijzijnde Hallo ingeschakeld Azure-regio worden gedegradeerd, Traffic Manager wordt verplaatst als verkeer toohello eindpunten Hallo volgende dichtstbijzijnde Azure-regio. Als u een reeks voorkeur failover toodefine wilt, gebruikt [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md).
* Als u de verkeersrouteringsmethode prestaties Hallo met externe eindpunten of geneste eindpunten, moet u toospecify Hallo locatie van deze eindpunten. Kies hello Azure-regio die het dichtst tooyour implementatie. Deze locaties zijn Hallo waarden die worden ondersteund door Hallo Internet latentie tabel.
* Hallo-algoritme dat Hallo-eindpunt kiest is deterministisch. DNS-query's uit Hallo dezelfde client wordt omgeleid toohello herhaald hetzelfde eindpunt. Clients gebruiken doorgaans verschillende recursieve DNS-servers als onderweg. Hallo-client mogelijk gerouteerde tooa ander endpoint. Routering kan ook worden beïnvloed door updates toohello Internet latentie tabel. Daarom Hallo prestaties voor verkeersroutering methode wordt niet gegarandeerd dat een client altijd toohello gerouteerd hetzelfde eindpunt.
* Als de Hallo Internet latentie tabel verandert, merkt u wellicht dat sommige clients gerichte tooa eindpunt zijn. Deze wijziging routering is nauwkeuriger op basis van latentiegegevens van de huidige. Deze updates zijn essentieel toomaintain Hallo nauwkeurigheid van het verkeer routeren als Hallo die Internet voortdurend zich verder ontwikkelen.

## <a name = "geographic"></a>Geografische verkeersroutering methode

Traffic Manager-profielen kunnen geconfigureerde toouse Hallo geografisch routeringsmethode zodat gebruikers worden omgeleid toospecific eindpunten (Azure, extern of geneste) op basis van welke geografische locatie hun DNS-query afkomstig zijn. Dit machtigt Traffic Manager klanten tooenable scenario's waarin de geografische regio van de gebruiker weet en routering toe op basis van die belangrijke. Voorbeelden zijn die voldoet aan gegevens onafhankelijkheid vereist, lokalisatie van inhoud & gebruiker ervaring en verkeer vanuit verschillende regio's te meten.
Wanneer een profiel is geconfigureerd voor het doorsturen van geografische, elk eindpunt gekoppeld dat profiel toohave een reeks tooit geografische regio's die zijn toegewezen moet. Een geografische regio kan zich op de volgende detailniveaus 
- World – elke regio
- Regionale groepering – bijvoorbeeld Afrika Midden-Oosten, Australië/Pacific enzovoort. 
- Land/regio – bijvoorbeeld Ierland Peru, Hongkong SAR enzovoort. 
- Staat/provincie – bijvoorbeeld Verenigde Staten Californië, Australië-Queensland, Canada Alberta enz. (Opmerking: deze granulariteitsniveau wordt alleen ondersteund voor staten / provincies in Australië, Canada VK en Verenigde Staten).

Wanneer een regio of een set van regio's wordt toegewezen tooan eindpunt, haalt alle aanvragen van deze gebieden gerouteerde alleen toothat-eindpunt. Traffic Manager maakt gebruik van Hallo IP-bronadres van Hallo DNS-query toodetermine Hallo regio van waaruit het opvragen van een gebruiker uit – meestal is dit Hallo IP-adres van Hallo lokale DNS-resolver Hallo query namens de gebruiker Hallo doen.  

![Azure Traffic Manager-'Geografische' methode verkeer routering](./media/traffic-manager-routing-methods/geographic.png)

Traffic Manager leest Hallo IP-bronadres van Hallo DNS-query en besluit welke geografische regio die afkomstig van zijn is. Vervolgens controleert het toosee als er een eindpunt dat deze tooit geografische regio toegewezen heeft. Deze zoekactie begint bij laagste granulariteitsniveau hello (staat/provincie waar het wordt ondersteund, anders op Hallo land/regio niveau) en probeert alle Hallo manier toohello hoogste niveau, namelijk **World**. Hallo eerste overeenkomst gevonden met behulp van deze verandering is aangewezen als Hallo eindpunt tooreturn in Hallo query-antwoord. Als die overeenkomt met een eindpunt binnen die onderliggende profiel van een geneste type eindpunt wordt geretourneerd, gebaseerd op de routeringsmethode voor. Hallo volgende punten zijn van toepassing toothis gedrag:

- Een geografische regio kan toegewezen alleen tooone eindpunt in een Traffic Manager-profiel zijn wanneer Hallo routeringstype geografische routering is. Dit zorgt ervoor dat gebruikers routering deterministisch is en klanten scenario's waarvoor ondubbelzinnig geografische grenzen kunnen inschakelen.
- Als een gebruiker regio afkomstig zijn onder twee verschillende eindpunten geografische toewijzing, Traffic Manager Hallo-eindpunt met de laagste granulatie Hallo selecteert en houdt geen rekening routering aanvragen van die regio toohello andere eindpunt. Neem bijvoorbeeld een type routering voor geografische profiel met twee eindpunten - 1 en Endpoint2. 1 is geconfigureerd tooreceive verkeer van Ierland en Endpoint2 is geconfigureerd tooreceive verkeer van Europa. Als een aanvraag afkomstig uit Ierland is, maar het is altijd gerouteerde tooEndpoint1.
- Omdat een regio kan toegewezen alleen tooone eindpunt, wordt het in Traffic Manager retourneert ongeacht of Hallo-eindpunt al dan niet in orde is.

    >[!IMPORTANT]
    >Het is raadzaam dat klanten die gebruikmaken van de geografische routeringsmethode Hallo koppelen aan Hallo geneste type eindpunten die onderliggende profielen met ten minste twee eindpunten binnen elk heeft.
- Als een eindpunt overeenkomst is gevonden en is dat eindpunt in Hallo **gestopt** staat, Traffic Manager een GEENGEGEVENS antwoord geretourneerd. In dit geval geen verdere zoekacties bestaat hoger staan in de hiërarchie van Hallo geografische regio. Dit gedrag is ook van toepassing voor geneste eindpunttypen Hallo onderliggende profiel wordt in Hallo **gestopt** of **uitgeschakelde** status.
- Als een eindpunt wordt weergegeven in een **uitgeschakelde** status, het niet opgenomen in het Hallo-regio die overeenkomt met de proces. Dit gedrag is ook van toepassing op geneste eindpunttypen wanneer Hallo-eindpunt in Hallo is **uitgeschakelde** status.
- Als een query afkomstig is van een geografische regio die niet toegewezen in dit profiel is, retourneert Traffic Manager een antwoord GEENGEGEVENS. Daarom is het raadzaam dat klanten gebruiken geografische routering met één eindpunt, in het ideale geval van het type geneste met ten minste twee eindpunten binnen Hallo onderliggende profiel Hallo regio **World** tooit toegewezen. Dit zorgt er ook voor dat alle IP-adressen die niet zijn toegewezen tooa regio worden verwerkt.

Zoals uitgelegd in [hoe Traffic Manager werkt](traffic-manager-how-traffic-manager-works.md), Traffic Manager ontvangt geen DNS-query's rechtstreeks van clients. In plaats daarvan DNS-query's zijn afkomstig Hallo recursieve DNS-service dat Hallo-clients geconfigureerde toouse zijn. Hallo IP-adres dat wordt gebruikt toodetermine Hallo regio is daarom niet Hallo van client-IP-adres, maar het Hallo IP-adres van Hallo recursieve DNS-service is. Dit IP-adres is in de praktijk kan een goede proxy voor Hallo-client.


## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toodevelop hoge beschikbaarheid van toepassingen via [eindpuntcontrole Traffic Manager](traffic-manager-monitoring.md)

Meer informatie over hoe te[een Traffic Manager-profiel maken](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



