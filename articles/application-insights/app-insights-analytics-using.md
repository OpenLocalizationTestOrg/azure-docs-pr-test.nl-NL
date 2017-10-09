---
title: aaaUsing Analytics - Hallo krachtige zoekfunctie van Azure Application Insights | Microsoft Docs
description: 'Met behulp van Hallo Analytics, Hallo diagnostische gegevens doorzoeken krachtige hulpprogramma van Application Insights. '
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Door middel van analyses in Application Insights
[Analytics](app-insights-analytics.md) is Hallo krachtige zoekfunctie van [Application Insights](app-insights-overview.md). Deze pagina's worden de Log Analytics query language beschreven.

* **[Hallo inleidende video bekijken](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet nog gegevens tooApplication Insights verzendt.

## <a name="open-analytics"></a>Open Analytics
Klik op Analytics van uw app thuis resource in Application Insights.

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics-using/001.png)

Hallo inline-zelfstudie hebt u enkele ideeën over wat u kunt doen.

Er is een [hier uitgebreider rondleiding](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Uw telemetrie query
### <a name="write-a-query"></a>Een query schrijven
![Schema weergeven](./media/app-insights-analytics-using/150.png)

Beginnen met de namen van elk van de vermelde aan de linkerkant Hallo Hallo-tabellen hello (of Hallo [bereik](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) of [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators). Gebruik `|` toocreate een pijplijn met [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense vraagt u met de Hallo operators en Hallo expressie-elementen die u kunt gebruiken. Klik op het informatiepictogram hello (of druk op CTRL + SPATIEBALK) tooget een langere beschrijving en voorbeelden van hoe toouse elk element.

Zie Hallo [Analytics taal rondleiding](app-insights-analytics-tour.md) en [taalreferentie](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Een query uitvoeren
![Een query uit te voeren](./media/app-insights-analytics-using/130.png)

1. U kunt één regeleinden gebruiken in een query.
2. Plaats de cursor Hallo binnen of aan Hallo einde van de gewenste toorun Hallo-query.
3. Controleer de tijdsbereik Hallo van uw query. (U kunt deze wijzigen of deze door uw eigen overschrijven [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) -component in uw query.)
3. Klik op Go toorun Hallo query.
4. Lege regels niet in uw query worden geplaatst. U kunt meerdere gescheiden query's in één query tabblad houden door deze te scheiden met een lege regels. Alleen Hallo query's met de Hallo cursor wordt uitgevoerd.

### <a name="save-a-query"></a>Een query opslaan
![Opslaan van een query](./media/app-insights-analytics-using/140.png)

1. Hallo huidige query-bestand opslaan.
2. Open een opgeslagen query-bestand.
3. Maak een nieuwe querybestand.

## <a name="see-hello-details"></a>Zie Hallo-details
De volledige lijst met eigenschappen voor elke rij in Hallo resultaten toosee uitbreiden. U kunt verder uitbreiden in elke eigenschap die is bijvoorbeeld een gestructureerde waarde -, aangepaste dimensies of Hallo stack aanbieding in een uitzondering.

![Vouw een rij](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Hallo resultaten ordenen
U kunt sorteren, filteren, pagineren en groep Hallo resultaten van uw query.

> [!NOTE]
> Sorteren, groeperen en filteren in de browser Hallo niet Voer de query opnieuw uit. Ze alleen Hallo resultaten die zijn geretourneerd door de laatste query opnieuw te rangschikken. 
> 
> tooperform deze taken in het Hallo-server voordat Hallo resultaten worden geretourneerd, schrijft u uw query met Hallo [sorteren](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [samenvatten](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) en [waar](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.
> 
> 

Hallo-kolommen die u wilt kiezen zoals toosee, sleept u kolom headers toorearrange en formaat kolommen te slepen.

![Kolommen rangschikken](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Items sorteren en filteren
Uw resultaten sorteren door te klikken op Hallo hoofd van een kolom. Klik opnieuw toosort Hallo andere manier en klikt u op een derde keer toorevert toohello oorspronkelijke ordening geretourneerd door de query.

Gebruik Hallo pictogram toonarrow uw zoekopdracht filteren.

![Kolommen sorteren en filteren](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Items groeperen
toosort groeperen door meer dan een kolom te gebruiken. Deze eerst inschakelen en sleep de kolomkoppen in Hallo ruimte boven Hallo tabel.

![Groep](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Ontbreken er bepaalde resultaten?

Als u denkt dat u alle verwachte Hallo-resultaten niet ziet, moet u er een aantal mogelijke redenen zijn.

* **Filter tijdsbereik**. Standaard worden alleen er resultaten van Hallo afgelopen 24 uur. Er is een automatische filter dat verkleint Hallo bereik van de resultaten die zijn opgehaald uit de brontabellen Hallo. 

    U kunt echter wijzigen Hallo tijdsbereik filteren met behulp van de vervolgkeuzelijst Hallo.

    Of u kunt automatische bereik Hallo vervangen door uw eigen [ `where  ... timestamp ...` component](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) in uw query. Bijvoorbeeld:

    `requests | where timestamp > ago('2d')`

* **Resultaten limiet**. Er is een limiet van ongeveer 10 k rijen op Hallo resultaten geretourneerd door het Hallo-portal. Een waarschuwing bevat als u gaan Hallo overschreden. Als dat gebeurt, sorteren van de resultaten in de tabel Hallo won't altijd u alle Hallo werkelijke eerste of laatste resultaten weergeven. 

    Het is raadzaam om tooavoid roept Hallo limiet. Filter tijdsbereik hello gebruiken, of gebruik operators, zoals:

  * [Top 100 volgens de timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [100 duren](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [samenvatten](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [waar tijdstempel > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(Meer dan 10 k rijen wilt? Overweeg het gebruik van [continue Export](app-insights-export-telemetry.md) in plaats daarvan. Analytics is ontworpen voor analyse, in plaats van onbewerkte gegevens op te halen.)

## <a name="diagrams"></a>Diagrammen
Hallo type diagram dat u wilt selecteren:

![Selecteer een diagramtype](./media/app-insights-analytics-using/230.png)

Als u meerdere kolommen van de juiste typen Hallo hebt, kunt u Hallo x en y-as en een kolom met de dimensies toosplit Hallo resultaten op.

Standaard resultaten in eerste instantie worden weergegeven als een tabel, en u Hallo diagram handmatig selecteren. Maar u kunt Hallo [renderen richtlijn](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) aan Hallo einde van een query tooselect een diagram.

### <a name="analytics-diagnostics"></a>Analytics diagnostische gegevens


Op een timechart als er een plotselinge piek of de stap in uw gegevens, ziet u mogelijk een gemarkeerde punt op Hallo lijn. Hiermee wordt aangegeven dat Analytics Diagnostics een combinatie van eigenschappen die Hallo plotselinge verandering uitfilteren is geïdentificeerd. Klik op Hallo punt tooget meer informatie over het Hallo-filter en toosee Hallo gefilterde versie. Hiermee kunt u bepalen welke veroorzaakt Hallo wijzigen. 

[Meer informatie over diagnostische gegevens Analytics](app-insights-analytics-diagnostics.md)


![Analytics diagnostische gegevens](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Pincode toodashboard
U kunt vastmaken een diagram of tabel tooone van uw [dashboards gedeeld](app-insights-dashboards.md) -Hallo pincode klikt u op. (U moet mogelijk te[upgrade pakket de prijzen van uw app](app-insights-pricing.md) tooturn over deze functie.) 

![Klik op Hallo pincode](./media/app-insights-analytics-using/pin-01.png)

Dit betekent dat, wanneer u een dashboard toohelp u Hallo prestaties of het gebruik van uw webservices bewaken samenstellen, u erg complexe analyse naast Hallo andere metrische gegevens opnemen kunt. 

Als er vier of minder kolommen, kunt u een tabel toohello-dashboard vastmaken. Alleen Hallo bovenste zeven rijen worden weergegeven.

### <a name="dashboard-refresh"></a>Dashboard vernieuwen
Hallo grafiek vastgemaakt toohello dashboard wordt automatisch vernieuwd door Hallo query opnieuw ongeveer elk uur wordt uitgevoerd. U kunt ook klikken op de knop Vernieuwen Hallo.

### <a name="automatic-simplifications"></a>Automatische vereenvoudigen

Bepaalde vereenvoudigen zijn toegepaste tooa grafiek wanneer u deze tooa dashboard vastmaken.

**Tijd van de beperking:** query's zijn automatisch beperkt toohello afgelopen 14 dagen. Hallo effect is Hallo dezelfde als de query bevat `where timestamp > ago(14d)`.

**Aantal beperking bin:** als u een grafiek die een groot aantal afzonderlijke opslaglocaties (meestal een staafdiagram weergeven heeft) minder ingevuld opslaglocaties automatisch gegroepeerd in een enkele 'anderen' hello opslaglocatie. Bijvoorbeeld: deze query:

    requests | summarize count_search = count() by client_CountryOrRegion

Analytics weergegeven als volgt:

![Grafiek met lange staart](./media/app-insights-analytics-using/pin-07.png)

maar wanneer u deze tooa dashboard vastmaken als volgt uitziet:

![Grafiek met beperkte opslaglocaties](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>TooExcel exporteren
Nadat u een query uitvoert hebt, kunt u een CSV-bestand downloaden. Klik op **exporteren, Excel**.

## <a name="export-toopower-bi"></a>TooPower BI exporteren
Hallo cursor plaatsen in een query en kies **exporteren, Power BI**.

![Exporteren van Analytics tooPower BI](./media/app-insights-analytics-using/240.png)

U uitvoeren Hallo query in Power BI. U kunt deze toorefresh, instellen op een planning.

U kunt dashboards die samenbrengen van gegevens uit een groot aantal bronnen maken met Power BI.

[Meer informatie over export tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Dieptekoppeling

Een koppeling onder **uitvoer, koppeling van de Share** kunt u tooanother gebruiker verzenden. Opgegeven Hallo gebruiker heeft [toegang tooyour resourcegroep](app-insights-resources-roles-access-control.md), Hallo query wordt geopend in Hallo Analytics gebruikersinterface.

(In Hallo-koppeling Hallo querytekst wordt weergegeven na '? q = ' gzip gecomprimeerd en base 64-codering. U kunt code toogenerate dieptekoppelingen schrijven toousers op te geven. Hallo wordt echter aanbevolen manier toorun Analytics van code is via Hallo [REST-API](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automatisering

Gebruik Hallo [REST-API van Data Access](https://dev.applicationinsights.io/) toorun analysequery's. [Bijvoorbeeld](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (met PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

In tegenstelling tot Hallo Analytics UI, geeft Hallo REST-API tijdstempel beperking tooyour query's niet automatisch toegevoegd. Houd er rekening mee tooadd uw eigen where-component, tooavoid grote antwoorden ophalen.



## <a name="import-data"></a>Gegevens importeren

U kunt gegevens importeren uit een CSV-bestand. Standaardgebruik zijn tooimport statische gegevens die u kunt deelnemen aan met tabellen uit uw telemetrie. 

Als de geverifieerde gebruikers worden geïdentificeerd in uw telemetrie met een alias of een verborgen-id, kunt u bijvoorbeeld een tabel die is toegewezen aliassen tooreal namen importeren. Door een join op Hallo-aanvraagtelemetrie uitvoert, kunt u gebruikers identificeren met hun echte namen in Hallo Analytics-rapporten.

### <a name="define-your-data-schema"></a>Het gegevensschema van uw definiëren

1. Klik op **instellingen** (op linksboven) en vervolgens **gegevensbronnen**. 
2. Toevoegen van een gegevensbron, Hallo instructies te volgen. U bent toosupply gevraagd een steekproef van Hallo gegevens, die ten minste tien rijen bevatten. Corrigeer Hallo schema.

Hiermee definieert u een gegevensbron, klikt u vervolgens u kunt afzonderlijke tabellen tooimport gebruiken.

### <a name="import-a-table"></a>Een tabel importeren

1. Definitie van de gegevensbron uit de lijst Hallo openen.
2. Klik op 'Uploaden' en volg Hallo instructies tooupload Hallo tabel. Hiervoor moet een aanroep tooa REST-API en het is daarom gemakkelijk tooautomate. 

De tabel is nu beschikbaar voor gebruik in Analytics query's. Deze wordt weergegeven in Analytics 

### <a name="use-hello-table"></a>Gebruik tabel Hallo

Stel de definitie van de gegevensbron wordt aangeroepen `usermap`, en dat er twee velden `realName` en `user_AuthenticatedId`. Hallo `requests` tabel heeft ook een veld met de naam `user_AuthenticatedId`, zodat u eenvoudig toojoin ze:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
Hallo resulterende tabel van aanvragen is een extra kolom `realName`.

### <a name="import-from-logstash"></a>Importeren uit LogStash

Als u [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), kunt u Analytics tooquery uw Logboeken. Gebruik Hallo [invoegtoepassing die gegevens doorgesluisd naar Analytics](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

