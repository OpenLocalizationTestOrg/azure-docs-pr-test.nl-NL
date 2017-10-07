---
title: aaaExport logboekanalyse gegevens tooPower BI | Microsoft Docs
description: "Power BI is een cloudgebaseerde business analytics-service van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.  Log Analytics kunt continu gegevens exporteren vanuit Hallo OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.  Dit artikel wordt beschreven hoe tooconfigure query's in logboekanalyse die automatisch geëxporteerd tooPower BI met regelmatige tussenpozen."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Log Analytics gegevens tooPower BI exporteren

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens dit proces voor het exporteren van logboekanalyse gegevens tooPower BI niet meer werken.  Eventuele bestaande schema's die u hebt gemaakt voordat u de upgrade wordt uitgeschakeld. 
>
> Na de upgrade hello Azure Log Analytics gebruikt hetzelfde platform als Application Insights en gebruik van dezelfde tooexport Log Analytics-query's tooPower BI als verwerken Hallo [Hallo proces tooexport Application Insights tooPower BI query](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Kunt u met behulp van Hallo Analytics console zoals beschreven in dit artikel Hallo-query exporteren of kunt u Hallo **Power BI** knop Hallo boven aan het welkomstscherm in Hallo logboek Search-portal.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is een service in de cloud business analytics van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.  Log Analytics kunt automatisch gegevens exporteren vanuit Hallo OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.

Wanneer u Power BI met logboekanalyse configureert, maakt u log-query's die hun resultaten toocorresponding gegevenssets in Power BI exporteren.  blijft tooautomatically uitvoeren volgens een schema dat u tookeep Hallo gegevensset up toodate met de meest recente gegevens Hallo verzameld door logboekanalyse definiëren Hallo query en exporteren.

![Log Analytics tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Power BI-schema 's
Een *Power BI planning* bevat een logboek zoekopdracht die een set gegevens exporteert van Hallo OMS-opslagplaats tooa bijbehorende gegevensset in Power BI en een planning die definieert hoe vaak deze zoekopdracht tookeep Hallo gegevensset huidige wordt uitgevoerd.

Hallo velden in de gegevensset Hallo komt overeen met de Hallo eigenschappen van Hallo records geretourneerd door Hallo logboek zoeken.  Als Hallo search records van verschillende typen retourneert en vervolgens Hallo gegevensset alle bevat opgenomen eigenschappen van elk van de Hallo Hallo recordtypen.  

> [!NOTE]
> Het is een best practice toouse een zoekquery logboek die onbewerkte gegevens retourneert als tegengestelde tooperforming een consolidatie met opdrachten zoals [meting](log-analytics-search-reference.md#measure).  U kunt een aggregatie en berekeningen in Power BI van ruwe gegevens Hallo uitvoeren.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Verbinding maken met OMS-werkruimte tooPower BI
Voordat u van logboekanalyse tooPower BI exporteren kunt, moet u verbinding maken met uw OMS werkruimte tooyour Power BI-account met Hallo procedure te volgen.  

1. Klik in Hallo OMS-console op Hallo **instellingen** tegel.
2. Selecteer **Accounts**.
3. In Hallo **werkruimte** sectie Klik **tooPower BI-Account verbinding**.
4. Geef Hallo referenties voor uw Power BI-account.

## <a name="create-a-power-bi-schedule"></a>Maak een planning van Power BI
Maak een Power BI-schema voor elke gegevensset met Hallo procedure te volgen.

1. Klik in Hallo OMS-console op Hallo **logboek zoeken** tegel.
2. Typ in een nieuwe query of Selecteer een opgeslagen zoekopdracht dat retourneert gegevens dat u wilt dat tooexport te Hallo**Power BI**.  
3. Klik op Hallo **Power BI** knop bovenaan Hallo Hallo pagina tooopen hello **Power BI** dialoogvenster.
4. Geef informatie op Hallo in Hallo hieronder tabel en klik **opslaan**.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Naam |Naam tooidentify Hallo plannen wanneer u Hallo lijst met Power BI-schema's weergeven. |
| Opgeslagen zoekopdracht |Hallo logboek zoeken toorun.  Selecteer de huidige query Hallo of Selecteer een bestaande opgeslagen zoekopdracht uit de vervolgkeuzelijst Hallo. |
| Planning |Hoe vaak toorun Hallo opgeslagen zoeken en te exporteren toohello Power BI-gegevensset.  Hallo-waarde moet tussen 15 minuten en 24 uur. |
| De naam van de gegevensset |Hallo-naam van de gegevensset Hallo in Power BI.  Deze wordt gemaakt als deze niet bestaat en wordt bijgewerkt als het bestand bestaat. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Weergeven en verwijderen van Power BI-schema 's
Hallo-lijst weergeven van de bestaande planningen van Power BI Hello procedure te volgen.

1. Klik in Hallo OMS-console op Hallo **instellingen** tegel.
2. Selecteer **Power BI**.

Bovendien toohello details van Hallo plannen, Hallo aantal keren dat planning Hallo afgelopen week in Hallo is uitgevoerd en Hallo status van de laatste synchronisatie Hallo worden weergegeven.  Hallo-synchronisatie aangetroffen fouten, u kunt klikken op Hallo koppeling toorun logboek zoekt records met details van Hallo-fout.

U kunt een schema verwijderen door te klikken op Hallo **X** in Hallo **verwijderen kolom**.  U kunt een planning uitschakelen door het selecteren van **uit**.  toomodify een schema moet u deze verwijderen en maak deze opnieuw met de nieuwe instellingen Hallo.

![Power BI-schema 's](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Voorbeeld-overzicht
Hallo volgende sectie wordt uitgelegd een voorbeeld van een Power BI-schema maken en gebruiken van de gegevensset toocreate een eenvoudig rapport.  In dit voorbeeld alle prestatiegegevens voor een set computers is geëxporteerde tooPower BI en vervolgens een lijngrafiek toodisplay processorgebruik is gemaakt.

### <a name="create-log-search"></a>Logboek zoekopdracht maken
Begin met het maken van een zoekopdracht logboek voor Hallo gegevens willen we toosend toohello gegevensset.  In dit voorbeeld gebruiken we een query alle prestatiegegevens voor computers met een naam die begint retourneert met *srv*.  

![Power BI-schema 's](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Zoeken met Power BI maken
We klikt u op Hallo **Power BI** tooopen Hallo Power BI dialoogvenster knop en Hallo vereist informatie te bieden.  We wilt dat deze zoekopdracht toorun één keer per uur en maken van een gegevensset met de naam *Contoso Perf*.  Aangezien we Hallo zoeken openen die Hallo gegevens we willen maakt al hebt, wij houden Hallo standaardwaarde *huidige zoekquery gebruiken* voor **opgeslagen zoekopdrachten**.

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Controleer of zoeken met Power BI
tooverify dat we Hallo planning correct hebt gemaakt, we Hallo lijst weergeven met Power BI zoekopdrachten onder Hallo **instellingen** -tegel in Hallo OMS-dashboard.  Er wacht een paar minuten en vernieuw deze weergave totdat deze rapporteert dat Hallo synchronisatie is uitgevoerd.

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Controleer of de gegevensset Hallo in Power BI
We Meld u aan bij onze account bij [powerbi.microsoft.com](http://powerbi.microsoft.com/) en schuif te**gegevenssets** Hallo onder het linkerdeelvenster Hallo aan.  Zien we dat Hallo *Contoso Perf* gegevensset wordt vermeld die aangeeft dat de export is uitgevoerd.

![Power BI-gegevensset](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Maken op basis van gegevensset
U selecteert Hallo **Contoso Perf** gegevensset en klik vervolgens op **resultaten** in Hallo **velden** deelvenster op Hallo rechts tooview Hallo velden die deel van deze dataset uitmaken.  toocreate een processorgebruik regel grafiek weergeven voor elke computer, we Hallo van de volgende activiteiten uitvoeren.

1. Selecteert u grafiekweergave Hallo-regel.
2. Sleep **ObjectName** te**rapport niveau filter** en Controleer **Processor**.
3. Sleep **CounterName** te**rapport niveau filter** en Controleer **percentage processortijd**.
4. Sleep **tegenwaarde** te**waarden**.
5. Sleep **Computer** te**legenda**.
6. Sleep **TimeGenerated** te**as**.

U ziet dat Hallo resulterende lijngrafiek met Hallo gegevens van onze gegevensset wordt weergegeven.

![Power BI-lijndiagram](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Hallo rapport opslaan
We opslaan Hallo rapport door te klikken op Hallo knop Hallo boven aan het welkomstscherm opslaan en het is nu opgenomen in Hallo rapporten sectie in het linkerdeelvenster Hallo valideren.

![Power BI-rapporten](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toobuild-query's die kunnen worden geëxporteerd tooPower BI.
* Meer informatie over [Power BI](http://powerbi.microsoft.com) toobuild visualisaties op basis van logboekanalyse uitvoer.
