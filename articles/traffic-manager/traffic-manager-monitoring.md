---
title: aaaAzure Traffic Manager-eindpuntcontrole | Microsoft Docs
description: In dit artikel vindt u informatie over hoe Traffic Manager gebruikt voor eindpuntcontrole en automatische eindpunt failover toohelp Azure klanten hoge beschikbaarheid toepassingen implementeren
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Eindpuntcontrole van Traffic Manager

Azure Traffic Manager omvat ingebouwde eindpuntcontrole en automatische eindpunt failover. Deze functie kunt u hoge beschikbaarheid toepassingen leveren die robuuste tooendpoint mislukt, waaronder Azure-regio fouten.

## <a name="configure-endpoint-monitoring"></a>Eindpunt bewaking configureren

tooconfigure eindpuntcontrole, moet u de volgende instellingen op uw Traffic Manager-profiel Hallo opgeven:

* **Protocol**. Kies HTTP, HTTPS of TCP als Hallo-protocol dat Traffic Manager wordt gebruikt bij het scannen van uw eindpunt toocheck de status. HTTPS-bewaking niet gecontroleerd of uw SSL-certificaat geldig is--alleen wordt gecontroleerd dat Hallo certificaat aanwezig is.
* **Poort**. Kies Hallo poort Hallo aanvraag gebruikt.
* **Pad**. Deze configuratieinstelling is alleen geldig voor Hallo HTTP en HTTPS-protocollen, waarvoor opgeven Hallo padinstelling vereist is. Het bieden van deze instelling voor Hallo TCP-protocol controleresultaten in een fout. Voor TCP-protocol geeft Hallo relatief pad en de naam van de Hallo Hallo webpagina of het Hallo-bestand dat toegang geeft tot bewaking Hallo. Een slash (/) is een geldige invoer voor Hallo relatief pad. Deze waarde geeft aan dat Hallo-bestand is in de hoofdmap hello (standaard).
* **Probing Interval**. Deze waarde geeft aan hoe vaak een eindpunt voor de status van een zoek Traffic Manager-agent wordt gecontroleerd. U kunt hier twee waarden opgeven: 30 seconden (normaal zoeken) en 10 seconden (snel zoeken). Als geen waarden zijn opgegeven, wordt Hallo profiel tooa standaardwaarde van 30 seconden. Ga naar Hallo [Traffic Manager prijzen](https://azure.microsoft.com/pricing/details/traffic-manager) pagina toolearn meer over snel Zoek prijzen.
* **Aantal mislukte verdragen**. Deze waarde bepaalt hoeveel mislukte maximaal een zoek Traffic Manager-agent wordt toegestaan voordat dat eindpunt als beschadigd gemarkeerd. De waarde ervan kan variëren tussen 0 en 9. Een waarde 0 betekent dat één bewaking fout kan leiden tot dat eindpunt toobe als beschadigd gemarkeerd. Als geen waarde opgeeft, wordt de standaardwaarde Hallo van 3.
* **Time-out voor bewaking**. Deze eigenschap geeft Hallo en de hoeveelheid tijd Hallo Traffic-Manager Zoek agent moet worden gewacht voordat het overwegen van een storing controleren wanneer een selectievakje health test toohello eindpunt wordt verzonden. Als Hallo die probing Interval is ingesteld too30 seconden, dan hebt u Hallo time-outwaarde tussen 5 en 10 seconden instellen kunt. Als geen waarde opgeeft, wordt een standaardwaarde van 10 seconden. Als Hallo die probing Interval is ingesteld too10 seconden, dan hebt u Hallo time-outwaarde tussen 5 en 9 seconden instellen kunt. Als er geen time-outwaarde is opgegeven, wordt een standaardwaarde van 9 seconden.

![Eindpuntcontrole van Traffic Manager](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Afbeelding 1: Traffic Manager-eindpuntcontrole**

## <a name="how-endpoint-monitoring-works"></a>Hoe eindpuntcontrole werkt

Als Hallo bewaking protocol is ingesteld als HTTP of HTTPS, kunt u Zoek Hallo Traffic Manager-agent een GET-aanvraag toohello-eindpunt met Hallo-protocol en poort opgegeven relatieve pad. Als er weer een antwoord 200 OK, is dat eindpunt in orde beschouwd. Als antwoord Hallo is een andere waarde, of als er geen reactie wordt ontvangen binnen de Hallo opgegeven time-outperiode, hello Traffic Manager-agent scannen probeert het dan opnieuw op basis van toohello aantal fouten verdragen instelling (geen probeert opnieuw worden uitgevoerd als deze instelling 0 is) . Als het aantal achtereenvolgende mislukte pogingen Hallo hoger dan Hallo aantal fouten verdragen instelling is, is dat eindpunt als beschadigd gemarkeerd. 

Als Hallo bewaking protocol TCP, initieert Zoek Hallo Traffic Manager-agent een TCP-verbindingsaanvraag Hallo poort opgegeven. Als het Hallo-eindpunt reageert toohello aanvraag met een antwoord tooestablish Hallo-verbinding dat statuscontrole is gemarkeerd als een is voltooid en zoek het Traffic Manager-agent Hallo Hallo TCP-verbinding wordt hersteld. Als het Hallo-antwoord is een andere waarde, of als er geen reactie wordt ontvangen binnen Hallo time-outperiode is opgegeven, Hallo Traffic Manager-agent scannen probeert opnieuw volgens toohello aantal fouten verdragen instelling (geen probeert opnieuw worden gemaakt als deze instelling 0 is). Als het aantal achtereenvolgende mislukte pogingen Hallo hoger dan Hallo aantal fouten verdragen instelling is, is dat eindpunt niet in orde gemarkeerd.

In alle gevallen Traffic Manager-tests vanaf meerdere locaties en Hallo opeenvolgende mislukte bepaling gebeurt er in elke regio. Dit betekent ook dat eindpunten statuscontroles van Traffic Manager met een hogere frequentie dan Hallo-instelling gebruikt voor het scannen van Interval ontvangen.

>[!NOTE]
>Voor HTTP of HTTPS-protocol bewaking, is een gangbare optie Hallo eindpunt zijde tooimplement een aangepaste pagina in uw toepassing - bijvoorbeeld /health.aspx. Dit pad gebruiken voor bewaking, kunt u toepassingsspecifieke controles, zoals prestatiemeteritems te controleren of de controle van de beschikbaarheid van de database uitvoeren. Op basis van deze aangepaste controles, retourneert Hallo pagina voor een juiste HTTP-statuscode.

Alle eindpunten in een Traffic Manager-profiel delen controle-instellingen. Als u toouse verschillende controle-instellingen voor verschillende eindpunten, kunt u [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Status endpoint en profiel

U kunt inschakelen en uitschakelen van Traffic Manager-profielen en eindpunten. Echter, een wijziging in de status van endpoint ook optreden als gevolg van Traffic Manager instellingen en processen geautomatiseerde.

### <a name="endpoint-status"></a>Status endpoint

U kunt in- of uitschakelen van een specifieke eindpunt. de onderliggende service Hello, die nog steeds mogelijk in orde, wordt niet beïnvloed. Veranderende Hallo eindpunt status besturingselementen Hallo beschikbaarheid van Hallo eindpunt in Hallo Traffic Manager-profiel. Wanneer de Eindpuntstatus van een is uitgeschakeld, Traffic Manager controleert de status niet en Hallo-eindpunt is niet opgenomen in een DNS-antwoord.

### <a name="profile-status"></a>Status van het profiel

Hallo profiel statusinstelling gebruikt, kunt u in- of uitschakelen van een bepaald profiel. Terwijl de status van endpoint invloed is op één eindpunt, beïnvloedt de status van het profiel Hallo volledige profiel, inclusief alle eindpunten. Wanneer u een profiel uitschakelt, Hallo eindpunten niet voor health worden gecontroleerd en er zijn geen eindpunten zijn opgenomen in een DNS-antwoord. Een [NXDOMAIN](https://tools.ietf.org/html/rfc2308) antwoordcode wordt geretourneerd voor Hallo DNS-query.

### <a name="endpoint-monitor-status"></a>Status van endpoint-monitor

Status van endpoint-monitor is een Traffic Manager gegenereerd waarde die Hallo status van het Hallo-eindpunt toont. U kunt geen deze instelling handmatig wijzigen. Hallo endpoint monitor-status is een combinatie van Hallo resultaten van eindpuntcontrole en Hallo geconfigureerd Eindpuntstatus. Hallo mogelijke waarden van de monitor status van endpoint worden weergegeven in de volgende tabel Hallo:

| Status van het profiel | Status endpoint | Status van endpoint-monitor | Opmerkingen |
| --- | --- | --- | --- |
| Uitgeschakeld |Ingeschakeld |Inactieve |Hallo-profiel is uitgeschakeld. Hoewel het Hallo-eindpunt is ingeschakeld, voorrang status van het profiel hello (uitgeschakeld). Eindpunten in uitgeschakelde profielen niet worden bewaakt. Een antwoord NXDOMAIN code wordt geretourneerd voor Hallo DNS-query. |
| &lt;alle&gt; |Uitgeschakeld |Uitgeschakeld |Hallo-eindpunt is uitgeschakeld. Uitgeschakelde eindpunten niet worden bewaakt. Hallo-eindpunt is niet opgenomen in de DNS-antwoorden, daarom wordt er geen verkeer ontvangen. |
| Ingeschakeld |Ingeschakeld |Online |Hallo-eindpunt wordt bewaakt en is in orde. Het is opgenomen in de DNS-antwoorden en verkeer kan ontvangen. |
| Ingeschakeld |Ingeschakeld |Gedegradeerd |Bewaking statuscontroles eindpunt mislukken. Hallo-eindpunt is niet opgenomen in de DNS-antwoorden en geen verkeer ontvangt. <br>Een uitzondering toothis is als alle eindpunten zijn gedegradeerd, in welk geval ze allemaal beschouwd als toobe geretourneerd in antwoord op Hallo query).</br>|
| Ingeschakeld |Ingeschakeld |CheckingEndpoint |Hallo-eindpunt wordt bewaakt, maar Hallo resultaten van de eerste test Hallo hebben nog niet ontvangen. CheckingEndpoint is een tijdelijke status dat meestal onmiddellijk na het toevoegen of een eindpunt in Hallo profiel inschakelen. Een eindpunt in deze status is opgenomen in de DNS-antwoorden en verkeer kan ontvangen. |
| Ingeschakeld |Ingeschakeld |Stopped |Hallo cloud service of web-app die Hallo eindpunt punten toois niet wordt uitgevoerd. Controleer Hallo cloud service of web-app-instellingen. Dit kan ook gebeuren als het Hallo-eindpunt is van geneste eindpunt typt en Hallo onderliggende profiel is uitgeschakeld of niet actief is. <br>Een eindpunt met de status gestopt wordt niet gecontroleerd. Het is niet opgenomen in de DNS-antwoorden en geen verkeer ontvangt. Een uitzondering toothis is als alle eindpunten zijn gedegradeerd, in welk geval ze allemaal beschouwd toobe in Hallo query-antwoord geretourneerd.</br>|

Zie voor meer informatie over hoe de status van endpoint-monitor wordt berekend voor geneste eindpunten [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Status van het profiel

monitor status van het Hallo profiel is een combinatie van de status van het profiel Hallo geconfigureerd en Hallo eindpunt monitor statuswaarden voor alle eindpunten. Hallo mogelijke waarden worden beschreven in de volgende tabel Hallo:

| Status van het profiel (zoals geconfigureerd) | Status van endpoint-monitor | Status van het profiel | Opmerkingen |
| --- | --- | --- | --- |
| Uitgeschakeld |&lt;eventuele&gt; of een profiel waarvoor geen eindpunten. |Uitgeschakeld |Hallo-profiel is uitgeschakeld. |
| Ingeschakeld |Hallo-status van ten minste één eindpunt is gedegradeerd. |Gedegradeerd |Bekijk Hallo afzonderlijke eindpunt status waarden toodetermine welke eindpunten meer aandacht vereisen. |
| Ingeschakeld |Hallo-status van ten minste één eindpunt is Online. Er zijn geen eindpunten hebben gedegradeerd status. |Online |Hallo-service wordt verkeer accepteert. Er is geen verdere actie vereist. |
| Ingeschakeld |Hallo-status van ten minste één eindpunt is CheckingEndpoint. Er zijn geen eindpunten status Online of gedegradeerd. |CheckingEndpoints |De status van deze overgang treedt op wanneer een profiel als gemaakt of ingeschakeld. Hallo eindpunt status wordt gecontroleerd op Hallo eerst. |
| Ingeschakeld |Hallo-status van alle eindpunten in Hallo profiel zijn uitgeschakeld of gestopt of Hallo profiel heeft geen eindpunten zijn gedefinieerd. |Inactieve |Er zijn geen eindpunten active, maar nog steeds Hallo-profiel is ingeschakeld. |

## <a name="endpoint-failover-and-recovery"></a>Eindpunt failovers en herstel

Traffic Manager controleert periodiek Hallo status van elk eindpunt, inclusief slecht eindpunten. Traffic Manager detecteert wanneer een eindpunt in orde wordt en deze terug naar worden gedraaid worden.

Een eindpunt is niet in orde als een Hallo volgende gebeurtenissen optreedt:
- Als bewaking protocol Hallo HTTP of HTTPS:
    - Er is een niet-200-antwoord ontvangen (met inbegrip van een andere 2xx-code of een 301/302-omleiding).
- Als Hallo protocol bewaking TCP is: 
    - Een antwoord verzonden andere dan ACK of SYN-ACK is ontvangen in het antwoord toohello synchronisatieverzoek door tooattempt Traffic Manager een verbinding tot stand brengen.
- Time-out. 
- Een andere verbindingsprobleem ertoe Hallo-eindpunt wordt niet bereikbaar.

Zie voor meer informatie over het oplossen van problemen mislukte controles [probleemoplossing gedegradeerd status op Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md). 

Hallo volgende tijdlijn in afbeelding 2 is een gedetailleerde beschrijving van Hallo bewakingsproces van Traffic Manager-eindpunt met Hallo volgende instellingen: HTTP protocol bewaking is, zoek-interval is 30 seconden, aantal verdragen fouten 3, time-outwaarde is is 10 seconden en DNS TTL is 30 seconden.

![Traffic Manager-eindpunt failover en failback-reeks](./media/traffic-manager-monitoring/timeline.png)

**Afbeelding 2: Traffic manager-eindpunt failovers en herstel reeks**

1. **OPHALEN VAN**. Voor elk eindpunt voert Hallo bewakingssysteem Traffic Manager een aanvraag voor ophalen op Hallo pad dat is opgegeven in Hallo controle-instellingen.
2. **200 OK**. Hallo bewakingssysteem verwacht een HTTP 200 OK-bericht toobe geretourneerd binnen 10 seconden. Wanneer deze dit antwoord ontvangt, herkent het dat Hallo service beschikbaar is.
3. **30 seconden tussen controles**. statuscontrole Hallo-eindpunt wordt herhaald elke 30 seconden.
4. **Service is niet beschikbaar**. Hallo-service niet meer beschikbaar. Traffic Manager weet niet tot de volgende statuscontrole Hallo.
5. **Pogingen tooaccess Hallo bewaking pad**. Hallo bewakingssysteem voert een GET-aanvraag, maar geen antwoord ontvangen binnen de time-outperiode Hallo van 10 seconden (u kunt ook een niet-200-respons kan worden ontvangen). Vervolgens wordt er meer driemaal geprobeerd met een interval van 30 seconden. Als een van de pogingen Hallo geslaagd is, klikt u vervolgens Hallo aantal pogingen wordt opnieuw ingesteld.
6. **De status ingesteld tooDegraded**. Na een vierde opeenvolgende mislukte markeert Hallo bewakingssysteem Hallo niet beschikbaar-Eindpuntstatus als gedegradeerd.
7. **Verkeer wordt omgereden tooother eindpunten**. Hallo Traffic Manager-DNS-naamservers worden bijgewerkt en Hallo eindpunt Traffic Manager niet meer geretourneerd in antwoord tooDNS query's. Nieuwe verbindingen zijn gerichte tooother, beschikbare eindpunten. Vorige DNS-antwoorden met dit eindpunt is echter nog steeds van cache recursieve DNS-servers en DNS-clients. Clients blijven toouse Hallo eindpunt totdat Hallo DNS-cache verloopt. Als Hallo DNS-cache is verlopen, kunnen clients nieuwe DNS-query's maken en gerichte toodifferent eindpunten. Hallo Cacheduur wordt bepaald door Hallo TTL-instelling in Hallo Traffic Manager-profiel, bijvoorbeeld: 30 seconden.
8. **Status controleert gaan**. Traffic Manager blijft toocheck Hallo status van het Hallo-eindpunt heeft de status gedegradeerd. Traffic Manager detecteert wanneer Hallo eindpunt toohealth retourneert.
9. **Service weer online wordt gezet**. Hallo-service beschikbaar. Hallo-eindpunt heeft de status gedegradeerd in Traffic Manager totdat Hallo bewakingssysteem de volgende statuscontrole voert.
10. **Verkeer tooservice hervat**. Traffic Manager een GET-aanvraag verzendt en ontvangt van een statusantwoord 200 OK. Hallo-service heeft de status in orde tooa geretourneerd. Hallo Traffic Manager-naamservers worden bijgewerkt en ze toohand Hallo-service DNS-naam in DNS-antwoorden beginnen. Verkeer retourneert toohello eindpunt, zoals in de cache DNS-antwoorden die andere eindpunten retourneren vervalt, en als de bestaande verbindingen tooother eindpunten zijn beëindigd.

    > [!NOTE]
    > Traffic Manager werkt op Hallo DNS-niveau en kan niet het bestaande verbindingen tooany eindpunt beïnvloeden. Wanneer het verkeer tussen de eindpunten (ofwel door gewijzigde profielinstellingen, of tijdens een failover en failback) wordt verwezen, is het Traffic Manager zorgt ervoor dat nieuwe verbindingen tooavailable eindpunten. Andere eindpunten mogelijk blijven echter tooreceive verkeer via bestaande verbindingen totdat deze sessies worden beëindigd. tooenable verkeer toodrain van bestaande verbindingen, toepassingen beperken Hallo sessieduur gebruikt met elk eindpunt.

## <a name="traffic-routing-methods"></a>Voor verkeersroutering methoden

Wanneer een eindpunt de status gedegradeerd heeft, wordt het niet langer geretourneerd in antwoord tooDNS query's. In plaats daarvan is een alternatieve eindpunt gekozen en geretourneerd. Hallo verkeersroutering methode is geconfigureerd in Hallo profiel bepaalt hoe alternatieve Hallo-eindpunt is gekozen.

* **Prioriteit**. Eindpunten vormen een geprioriteerde lijst. Hallo eerste beschikbare eindpunt op Hallo lijst wordt altijd geretourneerd. Als de Eindpuntstatus van een is gedegradeerd, wordt de volgende beschikbare eindpunt Hallo geretourneerd.
* **Gewogen**. Alle beschikbare eindpunt wordt gekozen in willekeurige volgorde op basis van hun toegewezen gewichten en gewicht Hallo Hallo andere beschikbare eindpunten.
* **Prestaties**. Hallo eindpunt dichtstbijzijnde toohello eindgebruiker wordt geretourneerd. Als dat eindpunt niet beschikbaar is, een eindpunt willekeurig wordt gekozen in alle andere beschikbare eindpunten Hallo. Het kiezen van een willekeurig eindpunt voorkomt een trapsgewijze fout die optreden kan wanneer de volgende dichtstbijzijnde eindpunt Hallo overbelast wordt. U kunt plannen voor het verkeer routeren alternatieve failover configureren met behulp van [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Geografische**. Hallo-eindpunt toegewezen tooserve Hallo geografische locatie op basis van de queryaanvraag Hallo die IP 's wordt geretourneerd. Als dat eindpunt niet beschikbaar is, een ander eindpunt niet worden geselecteerde toofailover, omdat een geografische locatie kan toegewezen alleen tooone eindpunt in een profiel (meer informatie vindt u in Hallo [Veelgestelde vragen over](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Als een best practice bij gebruik van geografische routering, wordt aangeraden klanten toouse genest Traffic Manager-profielen met meer dan één eindpunt als Hallo eindpunten van Hallo-profiel.

Zie voor meer informatie [Traffic Manager-verkeersroutering methoden](traffic-manager-routing-methods.md).

> [!NOTE]
> Een uitzondering toonormal traffic routing kan zich voordoen wanneer alle in aanmerking komende eindpunten een gedegradeerde status hebben. Traffic Manager wordt geprobeerd een 'best effort' en *reageert als alle Hallo gedegradeerd status eindpunten daadwerkelijk in een online status zijn*. Dit gedrag is beter toohello alternatieve die zijn toonot retourneert een willekeurig eindpunt in Hallo DNS-antwoord. Niet uitgeschakeld of gestopt eindpunten worden bewaakt, dus deze worden niet beschouwd als in aanmerking komen voor verkeer.
>
> Dit probleem wordt meestal veroorzaakt door onjuiste configuratie van Hallo-service, zoals:
>
> * Een toegangsbeheerlijst [] Hallo Traffic Manager-statuscontroles worden geblokkeerd.
> * Een onjuiste configuratie van Hallo bewaking poort of -protocol in Hallo Traffic manager-profiel.
>
> Hallo gevolg zijn van dit probleem is dat als statuscontroles Traffic Manager niet correct zijn geconfigureerd, lijkt het alsof van Hallo traffic routing alsof Traffic Manager *is* goed werkt. In dit geval kan niet eindpunt failover gebeurt echter algemene beschikbaarheid betrekking heeft. Het is belangrijk toocheck dat Hallo profiel ziet u een Online status, niet de status gedegradeerd. Een Online status geeft aan dat Hallo Traffic Manager health werkt controleert zoals verwacht.

Voor meer informatie over het oplossen van problemen mislukt statuscontroles, Zie [probleemoplossing gedegradeerd status op Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Volgende stappen

Meer informatie over [de werking van Traffic Manager](traffic-manager-how-traffic-manager-works.md)

Meer informatie over Hallo [verkeersroutering methoden](traffic-manager-routing-methods.md) ondersteund door Traffic Manager

Meer informatie over hoe te[een Traffic Manager-profiel maken](traffic-manager-manage-profiles.md)

[Problemen met de status gedegradeerd](traffic-manager-troubleshooting-degraded.md) op een Traffic Manager-eindpunt
