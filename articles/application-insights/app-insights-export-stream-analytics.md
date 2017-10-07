---
title: aaaExport met Stream Analytics uit Azure Application Insights | Microsoft Docs
description: Stream Analytics kunt continu transformeren, filter en route Hallo gegevens exporteren uit de Application Insights.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Gebruik Stream Analytics tooprocess geëxporteerde gegevens van Application Insights
[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is ideaal Hallo-hulpprogramma voor het verwerken van gegevens [geëxporteerd uit de Application Insights](app-insights-export-telemetry.md). Stream Analytics kunt ophalen van gegevens uit verschillende bronnen. U kunt transformeren en Hallo gegevens filteren en routeren vervolgens tooa diverse Put.

In dit voorbeeld maakt u een netwerkadapter die worden gegevens uit de Application Insights, naam en het doorgesluisd naar Power BI verwerkt aantal Hallo velden.

> [!WARNING]
> Er zijn veel beter en eenvoudiger [aanbevolen manieren toodisplay Application Insights-gegevens in Power BI](app-insights-export-power-bi.md). Hallo pad hier geïllustreerd is slechts een voorbeeld tooillustrate hoe tooprocess geëxporteerde gegevens.
> 
> 

![Diagram voor exporteren via SA tooPBI blokkeren](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Maken van opslag in Azure
Continue export levert altijd gegevens tooan Azure Storage-account, dus u toocreate Hallo opslag eerst moet.

1. Een 'klassiek' storage-account maken in uw abonnement in Hallo [Azure-portal](https://portal.azure.com).
   
   ![Kies nieuw, gegevens, opslag in Azure-portal](./media/app-insights-export-stream-analytics/030.png)
2. Een container maken
   
    ![In de nieuwe opslag hello, Containers selecteren, klikt u op Hallo Containers tegel en klik vervolgens op toevoegen](./media/app-insights-export-stream-analytics/040.png)
3. Hallo-toegangssleutel voor opslag kopiëren
   
    U hebt deze nodig snel tooset up Hallo invoer toohello stream analytics-service.
   
    ![Instellingen, sleutels, open in Hallo opslag, en een kopie van de primaire toegangssleutel Hallo](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Continue export tooAzure opslag starten
[Continue export](app-insights-export-telemetry.md) worden gegevens uit de Application Insights in Azure-opslag verplaatst.

1. Blader in hello Azure-portal, Application Insights-resource toohello die u hebt gemaakt voor uw toepassing.
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-export-stream-analytics/050.png)
2. Maak een continue export.
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-export-stream-analytics/060.png)

    Selecteer Hallo-opslagaccount die u eerder hebt gemaakt:

    ![Hallo exportbestemming instellen](./media/app-insights-export-stream-analytics/070.png)

    Hallo gebeurtenistypen gewenste toosee instellen:

    ![Gebeurtenistypen kiezen](./media/app-insights-export-stream-analytics/080.png)

1. Laat een aantal gegevens worden verzameld. Terug zitten en toestaan dat uw toepassing een tijdje gebruiken. Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md). 
   
    En ook Hallo gegevens tooyour opslag worden geëxporteerd. 
2. Hallo geëxporteerd gegevens te controleren. Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag. (Als u deze optie niet hebt, moet u tooinstall hello Azure SDK: Open het dialoogvenster Nieuw Project Hallo en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Noteer Hallo deel van de padnaam hello, die is afgeleid van naam en instrumentation sleutel van Hallo van toepassing. 

Hallo-gebeurtenissen worden tooblob bestanden geschreven in JSON-indeling. Elk bestand kan een of meer gebeurtenissen bevatten. Dus willen we graag tooread Hallo gebeurtenisgegevens en filter Hallo velden die we willen. Er zijn alle soorten wat die we met de Hallo gegevens kan doen, maar onze plan is vandaag de dag toouse Stream Analytics toopipe Hallo gegevens tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Azure Stream Analytics-exemplaar maken
Van Hallo [klassieke Azure Portal](https://manage.windowsazure.com/)hello Azure Stream Analytics-service en selecteer een nieuwe Stream Analytics-taak maken:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Als de nieuwe taak Hallo is gemaakt, vouwt u de details ervan:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Locatie van de blob instellen
Deze tootake invoer van uw blob continue Export instellen:

![](./media/app-insights-export-stream-analytics/120.png)

Nu moet u Hallo primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd. Stel dit in als Hallo Opslagaccountsleutel.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Set pad voorvoegselpatroon
![](./media/app-insights-export-stream-analytics/140.png)

**Worden ervoor tooset Hallo datumnotatie tooYYYY-MM-DD (met streepjes).**

Hallo pad voorvoegsel patroon geeft aan waar Stream Analytics Hallo invoerbestanden vindt in Hallo-opslag. U moet tooset het toocorrespond toohow continue Export Hallo-gegevens opslaat. Stel deze als volgt:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

In dit voorbeeld:

* `webapplication27`Hallo-naam van Hallo Application Insights-resource **alle kleine letters**.
* `1234...`de instrumentatiesleutel Hallo Hallo Application Insights-resource is **weglaten streepjes**. 
* `PageViews`Hallo type gegevens dat u wilt dat tooanalyze. de beschikbare typen Hello, is afhankelijk van Hallo filter die u in de continue Export instellen. Bekijk Hallo geëxporteerde gegevens toosee Hallo andere beschikbare typen en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).
* `/{date}/{time}`een patroon er wordt letterlijk geschreven.

> [!NOTE]
> Hallo opslag toomake zeker dat u direct Hallo pad controleren.
> 
> 

### <a name="finish-initial-setup"></a>De eerste installatie voltooien
Bevestig Hallo serialisatie-indeling:

![Bevestigen en de wizard te sluiten](./media/app-insights-export-stream-analytics/150.png)

Hallo wizard te sluiten en wachten op Hallo setup toocomplete.

> [!TIP]
> Hallo voorbeeld opdracht toodownload sommige gegevens gebruikt. Houd het als een voorbeeld test toodebug uw query.
> 
> 

## <a name="set-hello-output"></a>Set Hallo-uitvoer
Nu uw taak selecteren en instellen van Hallo uitvoer.

![Selecteer Nieuw kanaal hello, klikt u op de uitvoer, toevoegen, Power BI](./media/app-insights-export-stream-analytics/160.png)

Geef uw **werk- of schoolaccount** tooauthorize Stream Analytics tooaccess uw Power BI-resource. Vervolgens tot een naam voor uitvoer Hallo en voor Hallo doel Power BI gegevensset en tabel.

![Drie namen voorraad](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Set Hallo query
Hallo query beheerst Hallo vertaling van invoer toooutput.

![Hallo taak selecteren en klik op de Query. Plak Hallo voorbeeld hieronder.](./media/app-insights-export-stream-analytics/180.png)

Hallo Test functie toocheck ophalen van de juiste uitvoer hello gebruiken. Geef het Hallo-voorbeeldgegevens die u hebt gemaakt van Hallo invoer pagina. 

### <a name="query-toodisplay-counts-of-events"></a>Query toodisplay tellingen van gebeurtenissen
Plak deze query:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* export-invoer is Hallo alias gaven wij toohello Stroominvoer
* pbi-uitvoer is Hallo uitvoeraliassen is gedefinieerd
* We gebruiken [buitenste toepassen GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) omdat Hallo gebeurtenisnaam zich in een geneste JSON arrray. Selecteer uitgelicht Hallo Hallo vervolgens gebeurtenisnaam, samen met een telling van het aantal exemplaren met die naam aanwezig in Hallo periode Hallo. Hallo [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) component Hallo elementen gegroepeerd in perioden van 1 minuut.

### <a name="query-toodisplay-metric-values"></a>Query toodisplay metrische waarden
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Deze query ingezoomd in Hallo metrische gegevens telemetrie tooget Hallo gebeurtenistijd en Hallo metrische waarde. Hallo metrische waarden zijn binnen een matrix, zodat we Hallo buitenste toepassen GetElements patroon tooextract Hallo rijen gebruiken. 'myMetric' hello naam is van Hallo metrische gegevens in dit geval. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Query tooinclude waarden van de dimensie-eigenschappen
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Deze query bevat de waarden van eigenschappen zonder dimensie afhankelijk van een bepaalde dimensie wordt op een vaste index in een matrix dimensie Hallo Hallo.

## <a name="run-hello-job"></a>Hallo-taak uitvoeren
U kunt een datum selecteren in Hallo toostart Hallo taak in het verleden. 

![Hallo taak selecteren en klik op de Query. Plak Hallo voorbeeld hieronder.](./media/app-insights-export-stream-analytics/190.png)

Wacht totdat het Hallo-taak wordt uitgevoerd.

## <a name="see-results-in-power-bi"></a>Weergeven van resultaten in Power BI
> [!WARNING]
> Er zijn veel beter en eenvoudiger [aanbevolen manieren toodisplay Application Insights-gegevens in Power BI](app-insights-export-power-bi.md). Hallo pad hier geïllustreerd is slechts een voorbeeld tooillustrate hoe tooprocess geëxporteerde gegevens.
> 
> 

Power BI met uw werk of schoolaccount, en selecteer Hallo gegevensset en tabel die u hebt gedefinieerd als uitvoer van de Stream Analytics-taak Hallo Hallo openen.

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/200.png)

Nu kunt u deze gegevensset in rapporten en dashboards in [Power BI](https://powerbi.microsoft.com).

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Zijn er geen gegevens?
* Controleer dat u [set Hallo datumnotatie](#set-path-prefix-pattern) correct tooYYYY-MM-DD (met streepjes).

## <a name="video"></a>Video
Noam Ben Zeev ziet u hoe tooprocess gegevens met behulp van de Stream Analytics geëxporteerd.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Continue export](app-insights-export-telemetry.md)
* [Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

