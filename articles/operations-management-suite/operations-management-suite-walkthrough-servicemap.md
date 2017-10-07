---
title: aaaService kaart oplossing zelf eigen tempo demo | Microsoft Docs
description: Serviceoverzicht is een oplossing in Operations Management Suite (OMS) die automatisch de onderdelen van toepassing op Windows detecteert en Linux-systemen en maps Hallo communicatie tussen services.  Dit is een self in uw eigen tempo demo die doorloopt met Serviceoverzicht tooidentify en onderzoeken van een gesimuleerde probleem in een webtoepassing.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>OMS-demo (Operations Management Suited-demo) in eigen tempo - Serviceoverzicht
Dit is een self in uw eigen tempo demo die helpt bij het gebruik van Hallo [Serviceoverzicht oplossing](operations-management-suite-service-map.md) in tooidentify Operations Management Suite (OMS) en onderzoeken van een gesimuleerde probleem in een webtoepassing.  Serviceoverzicht detecteert automatisch de onderdelen van toepassing op Windows-en Linux- en maps Hallo communicatie tussen services.  Ook worden gegevens verzameld door andere services OMS tooassist samengevoegd u in de prestaties analyseren en te identificeren van problemen.  Gebruikt u ook de [zoekopdrachten aanmelden met logboekanalyse](../log-analytics/log-analytics-log-searches.md) toodrill af van de verzamelde gegevens in de volgorde tooidentify Hallo hoofdoorzaak van het probleem.


## <a name="scenario-description"></a>Scenariobeschrijving
U hebt zojuist een melding dat Hallo Top Customer Portal toepassing prestatieproblemen heeft ontvangen.  Hallo enige informatie die u hebt, is dat deze problemen ongeveer 4:00 am PST Vandaag gestart.  U niet helemaal zeker van alle onderdelen die Hallo die Hallo-portal is afhankelijk van behalve een set van webservers.  

## <a name="components-and-features-used"></a>Gebruikte onderdelen en functies
- [Oplossing Serviceoverzicht](operations-management-suite-service-map.md)
- [Zoeken in logboeken van Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Overzicht

### <a name="1-connect-toohello-oms-experience-center"></a>1. Verbinding maken met toohello OMS ervaring Center
Hallo maakt gebruik van deze doorloop [Operations Management Suite ervaring Center](https://experience.mms.microsoft.com/) waarmee u een volledige OMS-omgeving met voorbeeldgegevens. Start met behulp van deze link, Geef uw informatie op en selecteer vervolgens Hallo **inzicht en analyse** scenario.


### <a name="2-start-service-map"></a>2. Serviceoverzicht starten
Hallo Serviceoverzicht oplossing starten door te klikken op Hallo **Serviceoverzicht** tegel.

![Tegel Serviceoverzicht](media/operations-management-suite-walkthrough-servicemap/tile.png)

Hallo Serviceoverzicht console wordt weergegeven.  Hallo is linkerdeelvenster een lijst met computers in uw omgeving waarop Hallo Serviceoverzicht agent is geïnstalleerd.  Selecteert u Hallo-computer die u tooview uit deze lijst wilt.

![Lijst met computers](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Computer weergeven
We weten dat Hallo webservers heten AcmeWFE001 en AcmeWFE002, zodat dit een redelijke plaats toostart lijkt.  Klik op **AcmeWFE001**.  Hallo-kaart voor AcmeWFE001 en alle bijbehorende afhankelijkheden worden weergegeven.  U kunt zien welke processen worden uitgevoerd op de geselecteerde computer Hallo en die ze met communiceren externe-services.

![Webserver](media/operations-management-suite-walkthrough-servicemap/web-server.png)

We zorgen maakt over Hallo prestaties van onze webservices toepassing dus klikt u op Hallo **AcmeAppPool (IIS-toepassingen)** proces.  Dit Hallo worden details weergegeven voor dit proces en markeert u de afhankelijkheden ervan.  

![Pool van toepassingen](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Tijdvenster wijzigen

We gehoord dat Hallo probleem dus laten we om 4:00 A.M. gestart hieronder nader bekeken wat op dat moment is gebeurt. Klik op **tijdsbereik** en wijzig Hallo tijd too4: 00 AM PST (houden Hallo huidige datum en aanpassen voor uw lokale tijdzone) met een duur van 20 minuten.

![Tijdkiezer](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Waarschuwing weergeven

Nu zien we dat Hallo **acmetomcat** afhankelijkheid heeft een waarschuwing wordt weergegeven, zodat die onze potentiële problemen.  Klik op het waarschuwingspictogram Hallo in **acmetomcat** tooshow Hallo details voor Hallo waarschuwing.  U ziet dat het CPU-gebruik kritiek is en daarom gaat u dit gegeven uitbreiden voor meer details.  Dit is waarschijnlijk de oorzaak van de slechte prestaties. 

![Waarschuwing](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Prestaties weergeven

U gaat **acmetomcat** nader bekijken.  Klik in het Hallo bovenste rechts van **acmetomcat** en selecteer **Load Server kaart** tooshow Hallo detail en afhankelijkheden voor deze machine. We kunnen vervolgens bekijken wat in deze items prestaties tooverify onze vermoeden.  Selecteer Hallo **prestaties** tabblad toodisplay hello [prestatiemeteritems worden verzameld door logboekanalyse](../log-analytics/log-analytics-data-sources-performance-counters.md) via Hallo tijdsbereik.  U ziet dat er periodieke pieken in het Hallo-processor en geheugen voorbereidingen.

![Prestaties](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Wijzigingen bijhouden weergeven
Nu gaat u uitzoeken waardoor deze pieken in het gebruik worden veroorzaakt.  Klik op Hallo **samenvatting** tabblad.  Op deze manier kan de informatie die OMS verzameld van Hallo computer, zoals niet-verbindingen, kritieke waarschuwingen en wijzigingen in de software.  Secties met informatie die interessant recente al worden uitgebreid en u kunt andere secties tooinspect informatie die ze bevatten uitbreiden.


Vouw **Wijzigingen bijhouden** open als dit nog niet is gebeurd.  De weergegeven informatie verzameld door Hallo [bijhouden oplossing](../log-analytics/log-analytics-change-tracking.md).  Het lijkt erop dat er in dit tijdvenster een softwarewijziging heeft plaatsgevonden.  Klik op **Software** tooget details.  Een back-upproces is toegevoegd toohello machine direct na 4:00 uur, zodat deze wordt weergegeven toobe Hallo stackpad voor Hallo overmatig gebruik van bronnen worden verbruikt.

![Wijzigingen bijhouden](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Details weergeven in Zoeken in logboeken
We kunnen dit verder verifiëren door te kijken Hallo gedetailleerde prestatiegegevens verzameld in Hallo Log Analytics-opslagplaats.  Klik op Hallo **waarschuwingen** opnieuw tabblad en klik vervolgens op de Hallo **intensief CPU** waarschuwingen.  Klik op **Weergeven in Zoeken in logboeken**.  Hiermee opent u een venster van Hallo logboek zoeken waar u kunt uitvoeren [Meld zoekopdrachten](../log-analytics/log-analytics-log-searches.md) op basis van gegevens die zijn opgeslagen in de opslagplaats Hallo.  Serviceoverzicht een queriy al ingevuld voor ons tooretrieve Hallo waarschuwing we geïnteresseerd bent in.  

![Zoekopdrachten in logboeken](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Opgeslagen zoekopdracht openen
Laten we zien als we kunnen sommige nader ophalen op Hallo prestatieverzameling die deze waarschuwing is gegenereerd en controleren van onze vermoeden bestaat dat Hallo problemen worden veroorzaakt door deze back-upproces.  Hallo tijdsbereik ook wijzigen**6 uur**.  Klik vervolgens op **Favorieten** en schuif omlaag toohello opgeslagen zoekopdrachten voor **Serviceoverzicht**.  Dit zijn query's die specifiek voor deze analyse zijn gemaakt.  Klik op **Top 5 Processes by CPU for acmetomcat**.

![Opgeslagen zoekopdracht](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Deze query retourneert een lijst met Hallo top 5 processen processor verbruikt op **acmetomcat**.  U kunt inspecteren Hallo query tooget een inleiding toohello querytaal gebruikt voor zoekopdrachten logboek.  Als u geïnteresseerd in Hallo processen op andere computers, kan u Hallo query tooretrieve die informatie wijzigen.

In dit geval ziet u dat back-upproces Hallo consistent ongeveer 60% van de Hallo appserver CPU verbruikt.  Het is duidelijk dat dit nieuwe proces verantwoordelijk is voor het prestatieprobleem.  De oplossing is natuurlijk tooremove dit nieuwe back-upsoftware Hallo application server afmelden.  We kunnen daadwerkelijk gebruikmaken van Desired State Configuration (DSC) worden beheerd door Azure Automation toodefine beleidsregels die zorg ervoor dat dit proces wordt nooit uitgevoerd op deze kritieke systemen.


## <a name="summary-points"></a>Overzichtspunten
- [Serviceoverzicht](operations-management-suite-service-map.md) geeft een beeld van de gehele toepassing, zelfs als u niet alle servers en afhankelijkheden kent.
- Serviceoverzicht geeft gegevens weer die worden verzameld door andere oplossingen OMS toohelp u problemen met uw toepassing en de onderliggende infrastructuur.
- [Meld u zoekopdrachten](../log-analytics/log-analytics-log-searches.md) kunt u toodrill omlaag in specifieke gegevens verzameld in Hallo Log Analytics-opslagplaats.    

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [Serviceoverzicht](operations-management-suite-service-map.md).
- Serviceoverzicht [implementeren en configureren](operations-management-suite-service-map-configure.md).
- Meer informatie over [Log Analytics](../log-analytics/log-analytics-overview.md), dat is vereist voor Serviceoverzicht en dat de operationele gegevens bewaart die door agents zijn opgeslagen.