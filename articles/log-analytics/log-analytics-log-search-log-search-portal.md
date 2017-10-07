---
title: aaaUsing hello logboek zoeken portal in Azure Log Analytics | Microsoft Docs
description: Dit artikel bevat een zelfstudie waarin wordt beschreven hoe toocreate Meld u zoekopdrachten en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse met Hallo logboek zoeken portal.  Hallo-zelfstudie bevat enkele eenvoudige query's uitgevoerd tooreturn verschillende soorten gegevens en analyseren van resultaten.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Logboek zoekacties in de Azure-logboekanalyse met Hallo logboek zoeken portal maken

> [!NOTE]
> Dit artikel wordt beschreven in Azure-logboekanalyse met behulp van de nieuwe querytaal Hallo Hallo logboek zoeken-portal.  U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).  
>
> Als uw werkruimte niet bijgewerkte toohello nieuwe querytaal is, raadpleegt u te[vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) voor meer informatie over de huidige versie Hallo van Hallo logboek zoeken portal.

Dit artikel bevat een zelfstudie waarin wordt beschreven hoe toocreate Meld u zoekopdrachten en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse met Hallo logboek zoeken portal.  Hallo-zelfstudie bevat enkele eenvoudige query's uitgevoerd tooreturn verschillende soorten gegevens en analyseren van resultaten.  Dit artikel gaat over functies in Hallo logboek zoeken portal voor Hallo query te wijzigen in plaats van rechtstreeks wijzigen.  Zie voor informatie over het Hallo-query rechtstreeks te bewerken, Hallo [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).

toocreate zoekopdrachten in Hallo Advanced Analytics-portal in plaats van Hallo logboek zoeken portal, Zie [aan de slag met Hallo Analytics-Portal](https://go.microsoft.com/fwlink/?linkid=856587).  Beide portals hello gebruiken dezelfde query language tooaccess dezelfde gegevens in de werkruimte voor logboekanalyse Hallo Hallo.

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie wordt ervan uitgegaan dat u hebt al een werkruimte voor logboekanalyse met ten minste één verbonden bron die gegevens voor Hallo query's tooanalyze genereert.  

- Als u een werkruimte geen hebt, kunt u een gratis account maken met behulp van de procedure Hallo op [aan de slag met een werkruimte voor logboekanalyse](log-analytics-get-started.md).
- Verbinding maken met ten minste één [Windows-agent](log-analytics-windows-agents.md) of één [Linux-agent](log-analytics-linux-agents.md) toohello werkruimte.  

## <a name="open-hello-log-search-portal"></a>Open Hallo logboek zoeken portal
Starten door het Hallo logboek zoeken portal te openen.  U kunt openen in hello Azure-portal of Hallo OMS-portal.

1. Open hello Azure-portal.
2. Navigeer tooLog Analytics en selecteer uw werkruimte.
3. Selecteer **logboek zoeken** toostay in Azure portal of starten Hallo OMS-portal door te selecteren Hallo **OMS-Portal** Hallo logboek zoekknop te klikken.

![Meld u knop Zoeken](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Maken van een eenvoudige zoekopdrachten
de snelste manier tooretrieve Hallo sommige gegevens toowork met is een eenvoudige query waarin alle records in de tabel retourneert.  Als u een Windows- of Linux-clients verbonden tooyour werkruimte hebt, hebt u gegevens in ofwel Hallo gebeurtenis (Windows) of Syslog (Linux) tabel.

Typ een Hallo query's in het zoekvak hello te volgen en klik op Hallo zoeken.  

```
Event
```
```
Syslog
```

Gegevens worden geretourneerd in de lijst Standaardweergave Hallo en kunt u zien hoeveel totale records geretourneerd.

![Eenvoudige query](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Alleen hello eerste enkele eigenschappen van elke record worden weergegeven.  Klik op **meer** toodisplay alle eigenschappen voor een bepaalde record.

![Details van de records](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Hallo tijd bereik instellen
Elke record die is verzameld door Log Analytics is een **TimeGenerated** eigenschap met de Hallo datum en tijd die Hallo-record is gemaakt.  Een query in Hallo logboek zoeken portal retourneert alleen records met een **TimeGenerated** binnen Hallo tijd bereik dat wordt weergegeven op Hallo linkerkant van het welkomstscherm.  

U kunt Hallo tijdfilter wijzigen door het Hallo vervolgkeuzelijst selecteren of door het wijzigen van de schuifregelaar Hallo.  Hallo schuifregelaar wordt een staafdiagram waarin de relatieve aantal records voor elk segment tijd binnen het bereik van Hallo Hallo weergegeven.  Hallo-bereik is afhankelijk van dit segment.

Hallo tijd standaardbereik is **1 dag**.  Deze waarde te wijzigen**7 dagen**, en het totale aantal records Hallo moet verhogen.

![Datum tijd bereik](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Resultaten van Hallo query filteren
Op Hallo is links in het welkomstscherm Hallo filterdeelvenster waarmee u tooadd toohello query filteren zonder te rechtstreeks wijzigen.  Verschillende eigenschappen van Hallo records geretourneerd worden met de top tien waarden met hun aantal records weergegeven.

Als u met werkt **gebeurtenis**, selecteer Hallo selectievakje in naast te**fout** onder **EVENTLEVELNAME**.   Als u met werkt **Syslog**, selecteer Hallo selectievakje in naast te**err** onder **FOUTCODE**.  Hiermee wijzigt u Hallo query tooone na toolimit Hallo Hallo resulteert tooerror gebeurtenissen.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Add eigenschappen toohello filterdeelvenster door te selecteren **toofilters toevoegen** in Hallo eigenschap menu op een van de Hallo records.

![Toofilter menu toevoegen](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

U kunt instellen Hallo dezelfde door te selecteren filteren **Filter** van Hallo eigenschap menu naar een record met Hallo-waarde die u wilt toofilter.  

U hoeft alleen Hallo **Filter** optie voor eigenschappen met de naam in blauw.  Dit zijn *doorzoekbare* velden die zijn geïndexeerd voor voorwaarden zoeken.  Velden grijs zijn *vrije tekst doorzoekbare* velden waarvoor alleen Hallo **verwijzingen** optie.  Deze optie retourneert records die deze waarde in een eigenschap.

![Filtermenu](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

U kunt Hallo resultaten op één eigenschap groeperen op Hallo selecteren **groeperen op** optie in het menu Hallo-record.  Hiermee voegt u toe een [samenvatten](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query die Hallo resultaten in een grafiek weergegeven.  U kunt groeperen op meer dan één eigenschap, maar moet u tooedit Hallo query rechtstreeks.  Selecteer Hallo record menu volgende Hallo Hallo **Computer** eigenschap en selecteer **groeperen op 'Computer'**.  

![Groeperen op computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Werken met resultaten
Hallo logboek zoeken portal heeft een aantal functies voor het werken met Hallo resultaten van een query.  U kunt sorteren en filteren en groeperen resulteert tooanalyze Hallo gegevens zonder Hallo werkelijke query te wijzigen.  Resultaten van een query worden niet standaard gesorteerd.

tooview hello gegevens in tabelvorm, wat zorgt voor extra opties voor filteren en sorteren, klikt u op **tabel**.  

![Tabelweergave](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Klik op Hallo pijl door een record tooview Hallo details voor deze record.

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Sorteren op elk veld door te klikken op de kolomkop.

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Hallo resultaten op een specifieke waarde in kolom Hallo door te klikken op de knop filteren Hallo en het leveren van een filtervoorwaarde filteren.

![Resultaten filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Groeperen op een kolom door de kolom header toohello bovenaan Hallo resultaten te slepen.  U kunt meerdere velden groeperen door meerdere kolommen toohello boven te slepen.

![Resultaten van Groepsbeleid](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Werken met prestatiegegevens
Prestatiegegevens voor Windows- en Linux-agents wordt opgeslagen in de werkruimte voor logboekanalyse Hallo maken in Hallo **Perf** tabel.  Prestatiegegevens net als elke andere record zoeken en we een eenvoudige query waarin retourneert dat alle records van de prestaties op dezelfde manier als met gebeurtenissen kunt schrijven.

```
Perf
```

![Prestatiegegevens](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Hoewel miljoenen records voor alle prestatieobjecten en prestatiemeteritems retourneren is niet erg nuttig.  Query uitvoeren op dezelfde methoden die u gebruikte boven toofilter Hallo gegevens of alleen typt u de volgende Hallo Hallo kunt u rechtstreeks in het zoekvak Hallo-logboek.  Hiermee wordt alleen processor gebruik records voor zowel Windows- en Linux-computers.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Processorgebruik](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Dit beperkt Hallo gegevens tooa bepaald item, maar deze nog niet plaatsen in een formulier dat is bijzonder nuttig.  U kunt Hallo gegevens weergeven in een lijndiagram, maar moet u eerst de toogroup door de Computer en TimeGenerated.  toogroup op meerdere velden, moet u toomodify Hallo query rechtstreeks Hallo query toohello volgende zodanig te wijzigen.  Dit maakt gebruik van Hallo [Gem](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) functie op Hallo **tegenwaarde** eigenschap toocalculate Hallo gemiddelde waarde over elk uur.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Prestaties van een grafiek gegevensbron](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Nu dat Hallo gegevens worden naar behoren gegroepeerd, kunt u deze weergeven in een grafiek visual door toe te voegen Hallo [renderen](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Lijndiagram](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over Hallo Log Analytics-querytaal op [aan de slag met Hallo Analytics-Portal](https://go.microsoft.com/fwlink/?linkid=856079).
- Een zelfstudie met Hallo doorlopen [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587) waarmee u toorun Hallo dezelfde query's en toegang tot dezelfde gegevens als Hallo logboek zoeken portal Hallo.
