---
title: aaaA rondleiding via Analytics in Azure Application Insights | Microsoft Docs
description: Korte voorbeelden van alle Hallo belangrijkste query's in Analytics, Hallo krachtige zoekfunctie van Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a>Een rondleiding van Analytics in Application Insights
[Analytics](app-insights-analytics.md) is Hallo krachtige zoekfunctie van [Application Insights](app-insights-overview.md). Deze pagina's worden de Log Analytics query language beschreven.

* **[Hallo inleidende video bekijken](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet nog gegevens tooApplication Insights verzendt.
* **[SQL-gebruikers cheats blad](https://aka.ms/sql-analytics)**  Hallo meest voorkomende idioms vertaalt.

U gaat nu een stapsgewijze beschrijving van enkele eenvoudige query tooget die u gestart.

## <a name="connect-tooyour-application-insights-data"></a>Verbinding maken met gegevens van de Application Insights tooyour
Analytics openen vanuit uw app [overzichtsblade](app-insights-dashboards.md) in Application Insights:

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Nemen](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n rijen weergeven
Gegevenspunten die zich gebruiker operations (meestal HTTP-aanvragen ontvangen door uw web-app aanmelden) worden opgeslagen in een tabel met de naam `requests`. Elke rij is een telemetrie gegevenspunt ontvangen van Hallo Application Insights-SDK in uw app.

Laten we beginnen vindt u een paar voorbeeld rijen van de tabel Hallo van:

![resultaten](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Plaats Hallo cursor ergens in de instructie Hallo voordat u klikt op Start. U kunt een instructie verdelen over meer dan één regel, maar geen lege regels plaatsen in een instructie. Lege regels zijn een handige manier tookeep verschillende query's in het venster Hallo scheiden.
>
>

Kolommen kiezen, sleept u deze groeperen op kolommen, en te filteren:

![Klik op de kolom selecteren in de rechterbovenhoek van de resultaten](./media/app-insights-analytics-tour/030.png)

Vouw een item toosee Hallo detail:

![Kies tabel en kolommen configureren gebruiken](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Klik op Hallo hoofd van een kolom toore volgorde Hallo resultaten-beschikbaar in de webbrowser Hallo. Maar houd er rekening mee dat voor een grote resultatenset Hallo aantal rijen gedownloade toohello browser is beperkt. Sorteren op deze manier wordt niet altijd weergegeven u Hallo werkelijke hoogste of laagste items. toosort items betrouwbare manier gebruik Hallo `top` of `sort` operator.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) en [sorteren](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`is handig tooget een snel voorbeeld van een resultaat, maar deze bevat rijen uit de tabel Hallo in willekeurige volgorde. gebruik van een geordende weergave tooget `top` (voor een voorbeeld) of `sort` (via de hele tabel Hallo).

Hallo eerste n rijen, geordend op een bepaalde kolom weergeven:

```AIQL

    requests | top 10 by timestamp desc
```

* *Syntaxis:* hebben de meeste operators sleutelwoord parameters, zoals `by`.
* `desc`aflopende volgorde = `asc` = oplopend.

![](./media/app-insights-analytics-tour/260.png)

`top...`is een manier meer zodat de melding `sort ... | take...`. We kunnen schrijven:

```AIQL

    requests | sort by timestamp desc | take 10
```

Hallo resultaat zou zijn Hallo dezelfde, maar deze zou iets langzamer uitgevoerd. (U kunt ook schrijven `order`, dit is een alias van `sort`.)

Hallo kolomkoppen in tabelweergave Hallo kunnen ook worden gebruikt toosort Hallo resultaten op het welkomstscherm. Maar natuurlijk, als u hebt gebruikt `take` of `top` tooretrieve alleen maar een deel van een tabel, moet u alleen opnieuw rangschikken Hallo records die u hebt opgehaald.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Waar](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): voor het filteren van een voorwaarde

Laten we zien alleen aanvragen die een bepaalde resultaatcode geretourneerd:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Hallo `where` operator werkt met een Boole-expressie. Hier volgen enkele belangrijke punten hierover:

* `and`, `or`: Booleaanse operators
* `==`, `<>`, `!=` : gelijk en niet gelijk aan
* `=~`, `!~` : niet-hoofdlettergevoelige tekenreeks gelijk en niet gelijk zijn. Er zijn veel meer tekenreeks vergelijkingsoperators.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Het juiste type Hallo
Mislukte aanvragen zoeken:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Time

Uw query's zijn standaard beperkte toohello afgelopen 24 uur. Maar u kunt dit bereik wijzigen:

![](./media/app-insights-analytics-tour/change-time-range.png)

Hallo tijdsbereik overschrijven door een query noemt schrijven `timestamp` in een component where. Bijvoorbeeld:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

Hallo tijd bereik functie is gelijkwaardig tooa 'where' component ingevoegd na elke vermelding van een van de brontabellen Hallo.

`ago(3d)`betekent 'drie dagen geleden'. Andere tijdseenheden uren bevatten (`2h`, `2.5h`), minuten (`25m`), en seconden (`10s`).

Andere voorbeelden:

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

[Datums en tijden verwijzing](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selecteren en de namen van kolommen berekenen
Gebruik [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick uit net Hallo kolommen die u wilt:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

U kunt ook wijzigen van kolommen en definiëren van nieuwe:

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![Resultaat](./media/app-insights-analytics-tour/270.png)

* Kolomnamen kunnen spaties bevatten of symbolen als ze zijn tussen zoals deze: `['...']` of`["..."]`
* `%`Hallo is gebruikelijke modulo operator.
* `1d`(die wordt een cijfer, en vervolgens een had') is een letterlijke timespan wat betekent dat één dag. Hier volgen enkele meer timespan literals: `12h`, `30m`, `10s`, `0.01s`.
* `floor`(alias `bin`) Rondt een waarde omlaag toohello dichtstbijzijnde meervoud van basiswaarde Hallo u opgeeft. Dus `floor(aTime, 1s)` Rondt tegelijk omlaag toohello dichtstbijzijnde seconde.

Expressies kunnen bevatten alle Hallo gebruikelijke operators (`+`, `-`,...), en er is een aantal handige functies.

## <a name="extend"></a>Breid uit
Als u alleen tooadd kolommen toohello bestaande toepassingsgroepen wilt, gebruikt u [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Met behulp van [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is minder uitgebreid dan [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) als u wilt dat tookeep Hallo alle bestaande kolommen.

### <a name="convert-toolocal-time"></a>Toolocal tijd converteren

Tijdstempels worden altijd in UTC. Dus als u bijvoorbeeld op Hallo ons Pacific westkust winter is, kunt u als volgt uit:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Overzicht van](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): cumulatieve groepen rijen
`Summarize`van toepassing is een opgegeven *aggregatiefunctie* via Rijgroepen koppelen.

Bijvoorbeeld, Hallo duurt voordat uw web-app toorespond tooa aanvraag wordt gerapporteerd in het veld Hallo `duration`. Gemiddelde reactietijd van Hallo gaan we kijken tijd tooall aanvragen:

![](./media/app-insights-analytics-tour/410.png)

Of we Hallo resultaat kan verdelen in aanvragen van verschillende namen:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`verzamelt gegevenspunten in de stroom Hallo Hallo in groepen voor welke Hallo `by` component evenveel evalueert. Elke waarde in Hallo `by` - elke bewerkingsnaam in Hallo boven de voorbeeld - expressie resulteert in een rij in de resultaattabel Hallo.

Of we kan resultaten groeperen op tijd van de dag:

![](./media/app-insights-analytics-tour/430.png)

U ziet hoe we maken gebruik van Hallo `bin` functie (aka `floor`). Als we zojuist gebruikt `by timestamp`, elke rij invoer in een eigen weinig groep zou eindigen. Voor een continue scalaire like tijden of getallen, hebben we toobreak Hallo continue reeks in een beheersbare aantal discrete waarden. `bin`-Dit is slechts Hallo bekend afronden naar beneden `floor` werken - is de eenvoudigste manier toodo Hallo die.

We kunnen gebruiken dezelfde techniek tooreduce bereiken met tekenreeksen Hallo:

![](./media/app-insights-analytics-tour/440.png)

Merk op dat u kunt `name=` tooset Hallo-naam van een resultaatkolom in Hallo statistische expressies of Hallo door component.

## <a name="counting-sampled-data"></a>Voorbeeldgegevens tellen
`sum(itemCount)`is Hallo aanbevolen aggregatie toocount gebeurtenissen. In veel gevallen itemCount == 1, zodat het Hallo-functie gewoon een aantal rijen in de groep Hallo Hallo telt. Maar wanneer [steekproeven](app-insights-sampling.md) is uitgevoerd, alleen een fractie van de oorspronkelijke gebeurtenissen Hallo blijven behouden als gegevenspunten in Application Insights, zodat er zijn voor elk gegevenspunt u ziet, `itemCount` gebeurtenissen.

Bijvoorbeeld, als steekproeven 75% van de oorspronkelijke gebeurtenissen Hallo vervolgens itemCount negeert == 4 in Hallo bewaard records - dat wil zeggen, voor elke record behouden, zijn er vier oorspronkelijke records.

Adaptieve steekproeven zorgt ervoor dat itemCount toobe hogere tijdens perioden wanneer uw toepassing veel wordt gebruikt.

Berekening van het itemCount daarom resulteert in een goede indicatie van de oorspronkelijke aantal Hallo van gebeurtenissen.

![](./media/app-insights-analytics-tour/510.png)

Er is ook een `count()` aggregatie (en een aantal bewerking) voor gevallen waarin u echt toocount Hallo aantal rijen in een groep wilt.

Er is een bereik van [aggregatiefuncties](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Voor grafieken Hallo resultaten
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Standaard worden de resultaten weergegeven als een tabel:

![](./media/app-insights-analytics-tour/225.png)

We kunt beter dan Hallo tabelweergave doen. Bekijk Hallo resulteert in een diagramweergave Hallo in met de Hallo verticale balk optie:

![Klik op grafiek, kiest u verticaal staafdiagram en toewijzen x en y assen](./media/app-insights-analytics-tour/230.png)

U ziet dat hoewel we niet sorteren Hallo resultaten tijd (zoals u ziet in Hallo tabel weergave), datum/tijd Hallo grafiekweergave altijd weergegeven in de juiste volgorde.


## <a name="timecharts"></a>Timecharts
Weergeven hoeveel gebeurtenissen er elk uur zijn:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Selecteer optie Hallo grafiek:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Meerdere reeksen
Meerdere expressies in Hallo `summarize` component maakt meerdere kolommen.

Meerdere expressies in Hallo `by` component maakt meerdere rijen, één voor elke combinatie van waarden.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabel met aanvragen per uur en locatie](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Een grafiek segmenteren door dimensies
Als u een tabel met een tekenreekskolom en een numerieke kolom Hallo tekenreeks grafiek gebruikte toosplit Hallo numerieke gegevens in afzonderlijke reeks punten zijn kan. Als er meer dan een kolom met tekenreeksen, kunt u welke toouse kolom als Hallo-discriminator.

![Een grafiek met segmenteren](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Stuiteren snelheid

Een boolean tooa tekenreeks toouse converteren als discriminator:

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a>Meerdere metrische gegevens weergeven
Als u een tabel met meer dan een numerieke kolom, in aanvulling toohello tijdstempel grafiek, kunt u een combinatie van beide weergeven.

![Een grafiek met segmenteren](./media/app-insights-analytics-tour/110.png)

U moet selecteren **niet splitsen** voordat u kunt meerdere numerieke kolommen selecteren. U kunt niet splitsen door een kolom met tekenreeksen op Hallo dezelfde tijd als meer dan een numerieke kolom om weer te geven.

## <a name="daily-average-cycle"></a>Dagelijkse gemiddelde cyclus
Hoe informatie over het gebruik variëren op Hallo gemiddelde dag?

Aantal aanvragen door Hallo tijd modulo één dag voor binned in uren:

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Lijndiagram van uren in een gemiddelde dag](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> U ziet dat momenteel we tooconvert tijdsduur toodatetimes in volgorde toodisplay in een lijndiagram hebben.
>
>

## <a name="compare-multiple-daily-series"></a>Meerdere dagelijkse reeksen vergelijken
Hoe informatie over het gebruik variëren na verloop van tijd van de dag Hallo in andere landen?

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Gesplitste door client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a>Tekenen van een distributiepunt
Hoeveel sessies zijn er van verschillende lengtes?

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

de laatste regel Hallo is vereist tooconvert toodatetime. Momenteel wordt Hallo x-as van een grafiek weergegeven als een scalaire alleen als het een datum/tijd.

Hallo `where` component eindresultaat sessies worden uitgesloten (sessionDuration == 0) en stelt de lengte van de x-as Hallo Hallo.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Percentielen](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Welke bereiken van duur hebben betrekking op verschillende percentages van sessies?

Hallo hierboven query gebruiken, maar vervang Hallo laatste regel:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

We ook verwijderd Hallo bovengrens in Hallo waar component, in volgorde tooget cijfers inclusief alle sessies met meer dan één verzoek corrigeren:

![Resultaat](./media/app-insights-analytics-tour/180.png)

Waaruit zien we dat:

* 5% van sessies hebben een duur van minder dan 3 minuten 34s;
* 50% van sessies laatste minder dan 36 minuten;
* 5% van sessies laatste meer dan 7 dagen

tooget een afzonderlijke verdeling voor elk land, we hebben zojuist toobring hello client_CountryOrRegion kolom afzonderlijk via beide geven een overzicht van operators:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a>Koppelen
We hebben toegang tot tooseveral tabellen, inclusief aanvragen en uitzonderingen.

toofind hello uitzonderingen gerelateerde tooa aanvraag die foutantwoord geretourneerd, kunnen we Hallo tabellen samenvoegen op `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


Het is raadzaam om toouse `project` tooselect alleen Hallo kolommen we voordat u uitvoert moeten Hallo join.
In Hallo dezelfde componenten we Hallo timestamp-kolom wijzigen.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Laat](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): een resultaat tooa variabele toewijzen

Gebruik `let` tooseparate Hallo delen van vorige Hallo-expressie. Hallo resultaten zijn niet gewijzigd:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> Plaats geen lege regels tussen de onderdelen van Hallo query Hallo Hallo Analytics-client. Zorg ervoor dat tooexecute hiervan.
>

Gebruik `toscalar` tooconvert één tabel tooa celwaarde:

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a>Functies

Gebruik *laten* toodefine een functie:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Het openen van geneste objecten
Geneste objecten gemakkelijk toegankelijk. Bijvoorbeeld in Hallo uitzonderingen stroom ziet u gestructureerde objecten als volgt:

![Resultaat](./media/app-insights-analytics-tour/520.png)

U kunt deze afvlakken door te kiezen Hallo eigenschappen die u geïnteresseerd bent in:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Houd er rekening mee dat u nodig hebt toocast hello toohello juiste resultaattype.


## <a name="custom-properties-and-measurements"></a>Aangepaste eigenschappen en metingen
Als uw toepassing koppelt [aangepaste dimensies (eigenschappen) en aangepaste metingen](app-insights-api-custom-events-metrics.md#properties) tooevents en vervolgens worden deze weergegeven in Hallo `customDimensions` en `customMeasurements` objecten.

Bijvoorbeeld, als uw app bevat:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract deze waarden in Analytics:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify of een aangepaste dimensie is van een bepaald type:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Dashboards
U kunt uw resultaten tooa dashboard in volgorde toobring samen vastmaken uw belangrijkste grafieken en tabellen.

* [Azure gedeelde dashboard](app-insights-dashboards.md#share-dashboards): klik op het Punaisepictogram Hallo. Voordat u dit doet, moet u een gedeelde dashboard hebben. Open in hello Azure-portal, of een dashboard maken en klikt u op delen.
* [Power BI-dashboard](app-insights-export-power-bi.md): klik op exporteren, Power BI Query. Een voordeel van dit alternatief is dat u uw query samen met andere resultaten van een breed scala van gegevensbronnen kunt weergeven.

## <a name="combine-with-imported-data"></a>Gecombineerd met de geïmporteerde gegevens

Analytics-rapporten perfect op Hallo dashboard, maar soms wilt u tootranslate Hallo gegevens tooa meer digestible formulier. Stel bijvoorbeeld dat uw geverifieerde gebruikers worden geïdentificeerd in Hallo telemetrie door een alias. U wilt de namen van hun real tooshow in de resultaten. toodo, moet u een CSV-bestand dat kan worden toegewezen uit Hallo aliassen toohello echte namen.

U kunt een bestand importeren en gebruiken net als standaardtabellen hello (aanvragen, uitzonderingen, enzovoort). U kunt deze query uitvoeren op een eigen of deel hieraan met andere tabellen. Bijvoorbeeld, als u een tabel met de naam usermap hebt en er kolommen `realName` en `userId`, kunt u deze tootranslate hello `user_AuthenticatedId` veld Hallo-aanvraagtelemetrie:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

een tabel, Hallo Schema blade tooimport onder **andere gegevensbronnen**, volg Hallo instructies tooadd een nieuwe gegevensbron door het uploaden van een steekproef van uw gegevens. Vervolgens kunt u deze definitie tooupload tabellen.

Hallo import-functie is momenteel in preview zodat aanvankelijk ziet u een koppeling 'Contact met ons opnemen' onder "Andere gegevensbronnen." Gebruik deze toosign toohello preview-programma en Hallo koppeling vervolgens worden vervangen door een knop 'Een nieuwe gegevensbron toevoegen'.


## <a name="tables"></a>Tabellen
Hallo-stroom ontvangen van uw app telemetrie is toegankelijk via verschillende tabellen. Hallo-schema van de eigenschappen die beschikbaar zijn voor elke tabel is Hallo links in Hallo-venster zichtbaar.

### <a name="requests-table"></a>Tabel aanvragen
Aantal HTTP-aanvragen tooyour web-app en het segment met de paginanaam:

![Aantal aanvragen gesegmenteerd op naam](./media/app-insights-analytics-tour/analytics-count-requests.png)

Hallo-aanvragen die niet voldoen aan de meeste zoeken:

![Aantal aanvragen gesegmenteerd op naam](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Aangepaste gebeurtenissentabel
Als u [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend uw eigen gebeurtenissen, kunt u ze lezen uit deze tabel.

We nemen een voorbeeld waarin uw app-code deze regels bevat:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Hallo frequentie van deze gebeurtenissen worden weergegeven:

![Aantal aangepaste gebeurtenissen weergeven](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Pak metingen en dimensies van Hallo gebeurtenissen:

![Aantal aangepaste gebeurtenissen weergeven](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Tabel met aangepaste metrische gegevens
Als u [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend uw eigen metrische waarden vindt u de resultaten in Hallo **customMetrics** stroom. Bijvoorbeeld:  

![Aangepaste metrische gegevens in Application Insights analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> In [Metrics Explorer](app-insights-metrics-explorer.md), alle aangepaste metingen gekoppelde tooany type telemetrie samen voorkomen in Hallo metrische gegevens blade samen met metrische gegevens die zijn verzonden met behulp van `TrackMetric()`. Maar in Analytics, aangepaste metingen zijn nog steeds gekoppeld toowhichever type telemetrie ze werden uitgevoerd op - gebeurtenissen of aanvragen, enzovoort -terwijl metrische gegevens die zijn verzonden door TrackMetric worden weergegeven in hun eigen stroom.
>
>

### <a name="performance-counters-table"></a>Prestaties tellers tabel
[Prestatiemeteritems](app-insights-performance-counters.md) u basissysteem metrische gegevens voor uw app, zoals CPU, geheugen, weergeven en netwerkgebruik. U kunt Hallo SDK toosend aanvullende prestatiemeteritems, met inbegrip van uw eigen aangepaste items configureren.

Hallo **performanceCounters** schema beschrijft Hallo `category`, `counter` naam, en `instance` naam van elk prestatiemeteritem. Namen van exemplaren zijn alleen van toepassing toosome prestatiemeteritems en geven doorgaans aan Hallo naam van het Hallo proces toowhich Hallo aantal is gekoppeld. Hallo telemetrie voor elke toepassing ziet u alleen Hallo items voor die toepassing. Bijvoorbeeld: toosee welke items zijn beschikbaar:

![Prestatiemeters in Application Insights analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

een grafiek van het beschikbare geheugen over Hallo tooget periode geselecteerd:

![Geheugen timechart in Application Insights analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

Zoals u andere telemetrie **performanceCounters** heeft ook een kolom `cloud_RoleInstance` die aangeeft dat de identiteit Hallo van Hallo hostcomputer waarop uw app wordt uitgevoerd. Bijvoorbeeld: toocompare Hallo prestaties van uw app op verschillende computers Hallo:

![Prestaties gesegmenteerd op rolinstantie in Application Insights analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Uitzonderingentabel
[Uitzonderingen die zijn gerapporteerd door uw app](app-insights-asp-net-exceptions.md) zijn beschikbaar in deze tabel.

toofind Hallo HTTP-aanvraag die uw app is verwerkt wanneer Hallo uitzondering is gegenereerd, operation_Id koppelen:

![Uitzonderingen met aanvragen operation_Id koppelen](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Browser tijdsinstellingen tabel
`browserTimings`toont de pagina laden gegevens verzameld in browsers van uw gebruikers.

[Instellen van uw app voor clientzijde telemetrie](app-insights-javascript.md) in volgorde toosee deze metrische gegevens.

Hallo-schema bevat [metrische gegevens die wijzen op Hallo lengten van verschillende fasen van Hallo pagina laadproces](app-insights-javascript.md#page-load-performance). (Ze niet duiden op Hallo tijdsduur die uw gebruikers een pagina lezen.)  

Hallo popularities van verschillende pagina's weergeven en tijden voor elke pagina te laden:

![Laadtijden voor pagina's in Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Tabel met resultaten beschikbaarheid
`availabilityResults`toont Hallo resultaten van uw [webtests](app-insights-monitor-web-app-availability.md). Elke uitvoering van uw tests vanaf elke testlocatie wordt afzonderlijk gerapporteerd.

![Laadtijden voor pagina's in Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Afhankelijkheden tabel
Resultaten van aanroepen bevat dat uw app toodatabases en REST-API's en andere maakt tooTrackDependency() aanroept. Tevens AJAX-aanroepen vanuit de browser Hallo.

AJAX-aanroepen vanuit de browser Hallo:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Afhankelijkheidsaanroepen van Hallo-server:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Serverzijde afhankelijkheid resultaten altijd weergeven `success==False` als hello Application Insights-Agent niet is geïnstalleerd. Echter zijn hello andere gegevens juist.

### <a name="traces-table"></a>Traceringen tabel
Hallo telemetrie verzonden door uw app met TrackTrace(), bevat of [andere frameworks voor logboekregistratie](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Video 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Geavanceerde query's:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Volgende stappen
* [Naslaggids voor Analytics](app-insights-analytics-reference.md)
* [SQL-gebruikers cheats blad](https://aka.ms/sql-analytics) Hallo meest voorkomende idioms vertaalt.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
