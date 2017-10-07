---
title: gebruik van de gegevens aaaAnalyze in Log Analytics | Microsoft Docs
description: Gebruik Hallo gebruik dashboard in logboekanalyse tooview hoeveel gegevens toohello Log Analytics-service worden verzonden en waarom grote hoeveelheden gegevens worden verzonden.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Gegevensgebruik analyseren in Log Analytics
Log Analytics bevat informatie over Hallo hoeveelheid gegevens die zijn verzameld, die computers verzonden hello gegevens en Hallo verschillende soorten gegevens die worden verzonden.  Gebruik Hallo **Log Analytics gebruik** dashboard toosee Hallo hoeveelheid gegevens verzonden toohello Log Analytics-service. Hallo-dashboard ziet hoeveel gegevens worden verzameld door elke oplossing en hoeveel gegevens u uw computers om berichten te verzenden.

## <a name="understand-hello-usage-dashboard"></a>Hallo gebruik dashboard begrijpen
Hallo **logboekanalyse gebruik** dashboard toont de Hallo volgende informatie:

- Gegevensvolume
    - Gegevensvolume gedurende een bepaalde periode (op basis van uw huidige tijdsbereik)
    - Gegevensvolume per oplossing
    - Gegevens die niet zijn gekoppeld aan een computer
- Computers
    - Computers waarmee gegevens worden verzonden
    - Computers zonder gegevens in de afgelopen 24 uur
- Aanbiedingen
    - Knooppunten voor Insight en Analytics
    - Knooppunten voor automatisering en beheer
    - Knooppunten voor beveiliging
- Prestaties
    - Tijd toocollect en index
- Lijst met query's

![gebruiksdashboard](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork met gebruiksgegevens
1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com) met behulp van uw Azure-abonnement.
2. Op Hallo **Hub** menu, klikt u op **meer services** en typt u in de lijst met resources Hallo **logboekanalyse**. Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Klik op **Log Analytics**.  
    ![Azure-hub](./media/log-analytics-usage/hub.png)
3. Hallo **logboekanalyse** dashboard bevat een overzicht van uw werkruimten. Selecteer een werkruimte.
4. In Hallo *werkruimte* dashboard, klikt u op **logboekanalyse gebruik**.
5. Op Hallo **Log Analytics gebruik** dashboard, klikt u op **tijd: afgelopen 24 uur** toochange Hallo tijdsinterval.  
    ![tijdsinterval](./media/log-analytics-usage/time.png)
6. Weergave Hallo gebruik categorie bladen die gebieden weergeven u geïnteresseerd bent in. Kies een blade en klik vervolgens op een item in het tooview meer details in [logboek zoeken](log-analytics-log-searches.md).  
    ![voorbeeld van blade voor gegevensgebruik](./media/log-analytics-usage/blade.png)
7. Controleer op Hallo logboek zoeken dashboard Hallo resultaten die zijn geretourneerd vanuit Hallo zoekopdracht.  
    ![voorbeeld van gebruik van zoeken in logboeken](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Een waarschuwing instellen wanneer de gegevensverzameling groter is dan verwacht
Deze sectie wordt beschreven hoe toocreate een waarschuwing als:
- Het gegevensvolume groter is dan een opgegeven hoeveelheid.
- Gegevensvolume is voorspelde tooexceed het opgegeven tijdsbestek.

[Waarschuwingen](log-analytics-alerts-creating.md) van Log Analytics maken gebruik van zoekquery’s. Hallo heeft volgende query een resultaat wanneer er meer dan 100 GB aan gegevens verzameld in Hallo afgelopen 24 uur:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Hallo volgende query gebruikt een eenvoudige formule toopredict wanneer meer dan 100 GB aan gegevens in een dag wordt verzonden: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert op een andere gegevensvolume wijziging Hallo 100 in Hallo query's toohello aantal GB op het gewenste tooalert.

Gebruik Hallo stappen wordt beschreven in [een waarschuwingsregel maakt](log-analytics-alerts-creating.md#create-an-alert-rule) toobe gewaarschuwd wanneer gegevensverzameling hoger is dan verwacht.

Bij het Hallo-waarschuwing voor de eerste query Hallo--maken wanneer er meer dan 100 GB aan gegevens in 24 uur, stel de:
- **Naam** te*gegevensvolume op dat groter is dan 100 GB in 24 uur*
- **Ernst** te*waarschuwing*
- **Zoekopdracht** te`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Tijdvenster** te*24 uur*.
- **Waarschuwing frequentie** toobe één uur nadat Hallo gebruiksgegevens updates slechts één keer per uur.
- **Op basis van de waarschuwing wordt gegenereerd** toobe *aantal resultaten*
- **Aantal resultaten** toobe *groter dan 0*

Gebruik Hallo stappen wordt beschreven in [acties tooalert regels toevoegen](log-analytics-alerts-actions.md) e-mail, webhook of runbook actie voor het Hallo-waarschuwingsregel configureren.

Wanneer maken Hallo-waarschuwing voor de tweede query Hallo--wanneer deze wordt voorspeld dat er meer dan 100 GB aan gegevens in 24 uur worden instellen de:
- **Naam** te*gegevensvolume verwacht toogreater dan 100 GB in 24 uur*
- **Ernst** te*waarschuwing*
- **Zoekopdracht** te`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Tijdvenster** te*drie uur*.
- **Waarschuwing frequentie** toobe één uur nadat Hallo gebruiksgegevens updates slechts één keer per uur.
- **Op basis van de waarschuwing wordt gegenereerd** toobe *aantal resultaten*
- **Aantal resultaten** toobe *groter dan 0*

Wanneer u een waarschuwing ontvangt, voert u Hallo stappen in Hallo volgende sectie tootroubleshoot waarom gebruik hoger is dan verwacht.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Het oplossen van problemen met een hoger gebruik dan verwacht
Hallo gebruik dashboard kunt u tooidentify waarom gebruik (en dus kosten) is groter dan u verwacht.

Hoger gebruik wordt veroorzaakt door een of beide volgende oorzaken:
- Meer gegevens dan verwacht tooLog Analytics wordt verzonden
- Meer knooppunten dan verwacht voor het verzenden van gegevens tooLog Analytics

### <a name="check-if-there-is-more-data-than-expected"></a>Controleren of er meer gegevens zijn dan verwacht 
Er zijn twee belangrijke secties van Hallo gebruikspagina waarmee u achterhalen wat de oorzaak van Hallo toobe voor de meeste gegevens worden verzameld.

Hallo *gegevensvolume gedurende een bepaalde periode* diagram toont Hallo totale hoeveelheid gegevens die worden verzonden en Hallo computers verzenden de meeste gegevens Hallo. Hallo grafiek Hallo boven kunt u toosee, als uw gebruik van algemene gegevens groeiende resterende stabiele of afneemt. Hallo-lijst met computers geeft Hallo 10-computers Hallo de meeste gegevens worden verzonden.

Hallo *gegevensvolume per oplossing* diagram toont Hallo hoeveelheid gegevens die worden verzonden door elke oplossing en Hallo oplossingen Hallo de meeste gegevens worden verzonden. Hallo diagram Hallo boven toont Hallo totale hoeveelheid gegevens die worden verzonden door elke oplossing na verloop van tijd. Deze informatie kunt u tooidentify of een oplossing wordt meer gegevens verzendt, over Hallo dezelfde bedrag van gegevens of minder gegevens gedurende een bepaalde periode. Hallo-lijst met oplossingen toont Hallo 10 oplossingen Hallo de meeste gegevens worden verzonden. 

Deze twee grafieken geven alle gegevens weer. Sommige gegevens zijn betaald, andere gegevens zijn gratis. toofocus op gegevens die factureerbare pas Hallo query op Hallo zoeken pagina tooinclude `IsBillable=true`.  

![gegevensvolumediagrammen](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Bekijkt hello *gegevensvolume gedurende een bepaalde periode* grafiek. toosee hello oplossingen en gegevenstypen die u de meeste gegevens voor een specifieke computer Hallo verzendt Klik op Hallo-naam van Hallo-computer. Klik op het Hallo-naam van de eerste computer Hallo in Hallo-lijst.

Hallo in Hallo schermafbeelding te volgen, *Log-beheer / Perf* gegevenstype Hallo de meeste gegevens verzendt voor Hallo-computer. 

![gegevensvolume voor een computer](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Vervolgens gaat u terug toohello *gebruik* dashboard en bekijkt hello *gegevensvolume per oplossing* grafiek. toosee hello computers Hallo de meeste gegevens voor een oplossing te verzenden, klik op Hallo-naam van de oplossing in de lijst Hallo Hallo. Klik op het Hallo-naam van de eerste oplossing Hallo in Hallo lijst. 

In Hallo schermafbeelding te volgen, is Hiermee bevestigd dat Hallo *acmetomcat* computer Hallo de meeste gegevens verzendt voor Hallo logboek-beheeroplossing.

![gegevensvolume voor een oplossing](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Indien nodig aanvullende analyse tooidentify grote volumes in een oplossing of het type uitvoeren. Voorbeelden van query's zijn:

+ **Beveiligingsoplossing**
  - `Type=SecurityEvent | measure count() by EventID`
+ **Logboekbeheeroplossing**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ **Perf-gegevenstype**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ **Gebeurtenisgegevenstype**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ **Syslog-gegevenstype**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ **AzureDiagnostics**-gegevenstype
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Volgende stappen tooreduce Hallo volume van logboekbestanden verzameld hello gebruiken:

| Bron van hoog gegevensvolume | Hoe tooreduce gegevensvolume |
| -------------------------- | ------------------------- |
| Beveiligingsgebeurtenissen            | Selecteer [normale of minimale beveiligingsgebeurtenissen](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) <br> Hallo beleid toocollect alleen nodig beveiligingscontrolegebeurtenissen wijzigen. Controleer in het bijzonder Hallo nodig toocollect gebeurtenissen voor <br> - [filterplatform controleren](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [register controleren](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [bestandssysteem controleren](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [kernel-object controleren](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [greepbewerking controleren](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [verwijderbare opslag controleren](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Prestatiemeteritems       | Wijzig de [Prestatiemeteritemconfiguratie](log-analytics-data-sources-performance-counters.md) in: <br> -Verminderen Hallo frequentie van verzamelen <br> - Aantal prestatiemeteritems beperken |
| Gebeurtenislogboeken                 | Wijzig [Configuratie van gebeurtenislogboek](log-analytics-data-sources-windows-events.md) in: <br> -Verlaag Hallo van gebeurtenislogboeken verzameld <br> - Alleen vereiste gebeurtenisniveaus verzamelen. Bijvoorbeeld, gebeurtenissen op *informatie*niveau niet verzamelen |
| Syslog                     | Wijzig de [syslog-configuratie](log-analytics-data-sources-syslog.md) in: <br> -Verlaag Hallo faciliteiten verzameld <br> - Alleen vereiste gebeurtenisniveaus verzamelen. Bijvoorbeeld, gebeurtenissen op *informatie*- en *foutopsporings*niveau niet verzamelen |
| AzureDiagnostics           | Wijzig de resourcelogboekverzameling om: <br> -Het aantal resources verzenden logboeken tooLog Analytics Hallo verminderen <br> - Alleen vereiste logboeken te verzamelen |
| Gegevens van computers die niet Hallo oplossing hoeven oplossing | Gebruik [oplossing targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gegevens van alleen de vereiste groepen van computers. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Controleren of er meer knooppunten zijn dan verwacht
Als u op Hallo *per knooppunt (OMS)* prijscategorie, wordt u in rekening gebracht op basis van Hallo aantal knooppunten en oplossingen die u gebruikt. U kunt zien hoeveel knooppunten van elke aanbieding in hello worden gebruikt *aanbiedingen* sectie van Hallo gebruik dashboard.

![gebruiksdashboard](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Klik op **alle...**  tooview Hallo volledige lijst met computers verzenden van gegevens voor de geselecteerde aanbieding Hallo.

Gebruik [oplossing targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gegevens van alleen de vereiste groepen van computers.


## <a name="next-steps"></a>Volgende stappen
* Zie [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) toolearn hoe toouse Hallo taal zoeken. Op Hallo gebruiksgegevens kunt u zoeken query's tooperform aanvullende analyse.
* Gebruik Hallo stappen wordt beschreven in [een waarschuwingsregel maakt](log-analytics-alerts-creating.md#create-an-alert-rule) toobe gewaarschuwd wanneer een zoekcriteria wordt voldaan
* Gebruik [oplossing targeting](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gegevens van alleen de vereiste groepen van computers
* Selecteer [normale of minimale beveiligingsgebeurtenissen](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)
* Wijzig de [prestatiemeteritemconfiguratie](log-analytics-data-sources-performance-counters.md)
* Wijzig de [gebeurtenislogboekconfiguratie](log-analytics-data-sources-windows-events.md)
* Wijzig de [syslog-configuratie](log-analytics-data-sources-syslog.md)
