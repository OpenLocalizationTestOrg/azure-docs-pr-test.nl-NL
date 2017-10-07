---
title: TooSQL exporteren uit Azure Application Insights | Microsoft Docs
description: Application Insights gegevens tooSQL met Stream Analytics continu exporteren.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Overzicht: TooSQL van Application Insights met Stream Analytics exporteren
Dit artikel laat zien hoe toomove de telemetriegegevens van [Azure Application Insights] [ start] in een Azure SQL database met behulp van [continue Export] [ export] en [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). 

Continue export verplaatst de telemetriegegevens naar Azure Storage in JSON-indeling. We parseren Hallo JSON-objecten met behulp van Azure Stream Analytics en rijen in een databasetabel te maken.

(Meer in het algemeen Hallo manier toodo continue Export is uw eigen analyse Hallo telemetrie verzenden tooApplication Insights van uw apps. U kan pas deze code voorbeeld toodo andere mogelijkheden met Hallo geëxporteerd telemetriegegevens, zoals aggregatie van gegevens.)

We beginnen met Hallo veronderstelling dat u al hebt Hallo-app die u wilt dat toomonitor.

In dit voorbeeld we paginaweergavegegevens hello gebruiken, maar hello hetzelfde patroon kan gemakkelijk worden uitgebreid tooother gegevenstypen zoals aangepaste gebeurtenissen en uitzonderingen. 

## <a name="add-application-insights-tooyour-application"></a>Application Insights tooyour toepassing toevoegen
tooget gestart:

1. [Application Insights instellen voor uw webpagina's](app-insights-javascript.md). 
   
    (In dit voorbeeld we ligt de nadruk op paginaweergavegegevens van Hallo clientbrowsers verwerking, maar u kan Application Insights instellen voor de serverzijde Hallo van uw [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) proces en app-aanvraag afhankelijkheden en andere servertelemetrie.)
2. Uw app publiceren en bekijk de telemetrische gegevens verschijnen in uw Application Insights-resource.

## <a name="create-storage-in-azure"></a>Maken van opslag in Azure
Continue export levert altijd gegevens tooan Azure Storage-account, dus u toocreate Hallo opslag eerst moet.

1. Een opslagaccount maken in uw abonnement in Hallo [Azure-portal][portal].
   
    ![Kies nieuw, gegevens, opslag in Azure-portal. Klassieke selecteert, kiest u maken. Geef een opslagnaam.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Een container maken
   
    ![In de nieuwe opslag hello, Containers selecteren, klikt u op Hallo Containers tegel en klik vervolgens op toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Hallo-toegangssleutel voor opslag kopiëren
   
    U hebt deze nodig snel tooset up Hallo invoer toohello stream analytics-service.
   
    ![Instellingen, sleutels, open in Hallo opslag, en een kopie van de primaire toegangssleutel Hallo](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Continue export tooAzure opslag starten
1. Blader in hello Azure-portal, Application Insights-resource toohello die u hebt gemaakt voor uw toepassing.
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Maak een continue export.
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Selecteer Hallo-opslagaccount die u eerder hebt gemaakt:

    ![Hallo exportbestemming instellen](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Hallo gebeurtenistypen gewenste toosee instellen:

    ![Gebeurtenistypen kiezen](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Laat een aantal gegevens worden verzameld. Terug zitten en toestaan dat uw toepassing een tijdje gebruiken. Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md). 
   
    En ook Hallo gegevens tooyour opslag worden geëxporteerd. 
2. Inspecteer Hallo geëxporteerd-gegevens in de portal Hallo - kiezen **Bladeren**, selecteer uw storage-account en vervolgens **Containers** - of in Visual Studio. Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag. (Als u deze optie niet hebt, moet u tooinstall hello Azure SDK: Open het dialoogvenster Nieuw Project Hallo en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)
   
    ![Open in Visual Studio Server Browser, Azure, opslag](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Noteer Hallo deel van de padnaam hello, die is afgeleid van naam en instrumentation sleutel van Hallo van toepassing. 

Hallo-gebeurtenissen worden tooblob bestanden geschreven in JSON-indeling. Elk bestand kan een of meer gebeurtenissen bevatten. Dus willen we graag tooread Hallo gebeurtenisgegevens en filter Hallo velden die we willen. Er zijn alle soorten wat die we met de Hallo gegevens kan doen, maar onze plan is vandaag de dag toouse Stream Analytics toomove Hallo gegevens tooa SQL-database. Dat kunt u eenvoudig toorun veel interessante query's.

## <a name="create-an-azure-sql-database"></a>Een Azure SQL-Database maken
Opnieuw starten vanuit uw abonnement in [Azure-portal][portal], Hallo-database maken (en een nieuwe server, tenzij u er al hebt verkregen) toowhich schrijft u Hallo gegevens.

![Nieuw, gegevens, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Zorg ervoor dat databaseserver Hallo kan toegang tooAzure services:

![Bladeren, Servers, uw server, instellingen, Firewall, tooAzure toegang toestaan](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Een tabel maken in Azure SQL DB
Verbinding maken met toohello-database die zijn gemaakt in de vorige sectie Hallo met het beheerprogramma van uw voorkeur. In dit overzicht we gebruiken [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Een nieuwe query maken en uitvoeren van de volgende T-SQL Hallo:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

In dit voorbeeld gebruiken we gegevens van paginaweergaven. toosee Hallo van andere gegevens die beschikbaar zijn, inspecteren van de JSON-uitvoer en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Azure Stream Analytics-exemplaar maken
Van Hallo [klassieke Azure Portal](https://manage.windowsazure.com/)hello Azure Stream Analytics-service en selecteer een nieuwe Stream Analytics-taak maken:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Als de nieuwe taak Hallo is gemaakt, vouwt u de details ervan:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Locatie van de blob instellen
Deze tootake invoer van uw blob continue Export instellen:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Nu moet u Hallo primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd. Stel dit in als Hallo Opslagaccountsleutel.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Set pad voorvoegselpatroon
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Ervoor tooset Hallo datumnotatie te worden**jjjj-MM-DD** (met **streepjes**).

Hallo pad voorvoegsel patroon geeft aan hoe Stream Analytics Hallo invoerbestanden vindt in Hallo-opslag. U moet tooset het toocorrespond toohow continue Export Hallo-gegevens opslaat. Stel deze als volgt:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

In dit voorbeeld:

* `webapplication27`Hallo-naam van Hallo Application Insights-resource **allemaal in kleine letters**. 
* `1234...`de instrumentatiesleutel Hallo Hallo Application Insights-resource is **met streepjes verwijderd**. 
* `PageViews`Hallo-type van de gegevens die we willen tooanalyze. de beschikbare typen Hello, is afhankelijk van Hallo filter die u in de continue Export instellen. Bekijk Hallo geëxporteerde gegevens toosee Hallo andere beschikbare typen en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).
* `/{date}/{time}`een patroon er wordt letterlijk geschreven.

tooget hello naam en sleutel van uw Application Insights-resource Essentials openen op de overzichtspagina of instellingen openen.

#### <a name="finish-initial-setup"></a>De eerste installatie voltooien
Bevestig Hallo serialisatie-indeling:

![Bevestigen en de wizard te sluiten](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Hallo wizard te sluiten en wachten op Hallo setup toocomplete.

> [!TIP]
> Gebruik Hallo voorbeeld functie toocheck Hallo invoer pad correct ingesteld. Als dit mislukt: Controleer of er gegevens in de opslag Hallo voor Hallo voorbeeld-tijdsbereik u hebt gekozen. Hallo invoer definitie bewerken en controleer u Hallo storage-account, pad voorvoegsel ingesteld en datumnotatie correct.
> 
> 

## <a name="set-query"></a>Set-query
Open gedeelte Hallo-query:

![Selecteer in de stream analytics, Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Vervang de standaardquery Hallo met:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

U ziet dat Hallo eerst enkele eigenschappen zijn gegevens van specifieke toopage weergeven. Uitvoer van andere typen telemetrie heeft andere eigenschappen. Zie Hallo [gedetailleerde gegevens modelverwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Uitvoer toodatabase instellen
Selecteer SQL als Hallo uitvoer.

![Selecteer in de stream analytics, uitvoer](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Geef Hallo SQL-database.

![Vul Hallo details van de database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Hallo wizard te sluiten en wachten op een melding dat Hallo uitvoer is ingesteld.

## <a name="start-processing"></a>Verwerking starten
Hallo taak vanuit Hallo actiebalk starten:

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

U kunt kiezen of toostart verwerking Hallo gegevens vanaf nu of toostart met oudere gegevens. Hallo laatste is handig als u hebt continue Export is al een tijdje wordt uitgevoerd.

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Ga terug tooSQL Server-beheerprogramma's na een paar minuten en bekijkt hello gegevens stromende. Gebruik bijvoorbeeld een query als volgt:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Verwante artikelen:
* [Met Stream Analytics tooPowerBI exporteren](app-insights-export-power-bi.md)
* [Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)
* [Continue Export in de Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

