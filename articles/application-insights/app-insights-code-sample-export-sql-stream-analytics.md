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
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="1d845-103">Overzicht: TooSQL van Application Insights met Stream Analytics exporteren</span><span class="sxs-lookup"><span data-stu-id="1d845-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="1d845-104">Dit artikel laat zien hoe toomove de telemetriegegevens van [Azure Application Insights] [ start] in een Azure SQL database met behulp van [continue Export] [ export] en [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="1d845-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="1d845-105">Continue export verplaatst de telemetriegegevens naar Azure Storage in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1d845-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="1d845-106">We parseren Hallo JSON-objecten met behulp van Azure Stream Analytics en rijen in een databasetabel te maken.</span><span class="sxs-lookup"><span data-stu-id="1d845-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="1d845-107">(Meer in het algemeen Hallo manier toodo continue Export is uw eigen analyse Hallo telemetrie verzenden tooApplication Insights van uw apps.</span><span class="sxs-lookup"><span data-stu-id="1d845-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="1d845-108">U kan pas deze code voorbeeld toodo andere mogelijkheden met Hallo geëxporteerd telemetriegegevens, zoals aggregatie van gegevens.)</span><span class="sxs-lookup"><span data-stu-id="1d845-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="1d845-109">We beginnen met Hallo veronderstelling dat u al hebt Hallo-app die u wilt dat toomonitor.</span><span class="sxs-lookup"><span data-stu-id="1d845-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="1d845-110">In dit voorbeeld we paginaweergavegegevens hello gebruiken, maar hello hetzelfde patroon kan gemakkelijk worden uitgebreid tooother gegevenstypen zoals aangepaste gebeurtenissen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="1d845-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="1d845-111">Application Insights tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d845-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="1d845-112">tooget gestart:</span><span class="sxs-lookup"><span data-stu-id="1d845-112">tooget started:</span></span>

1. <span data-ttu-id="1d845-113">[Application Insights instellen voor uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="1d845-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="1d845-114">(In dit voorbeeld we ligt de nadruk op paginaweergavegegevens van Hallo clientbrowsers verwerking, maar u kan Application Insights instellen voor de serverzijde Hallo van uw [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) proces en app-aanvraag afhankelijkheden en andere servertelemetrie.)</span><span class="sxs-lookup"><span data-stu-id="1d845-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="1d845-115">Uw app publiceren en bekijk de telemetrische gegevens verschijnen in uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="1d845-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="1d845-116">Maken van opslag in Azure</span><span class="sxs-lookup"><span data-stu-id="1d845-116">Create storage in Azure</span></span>
<span data-ttu-id="1d845-117">Continue export levert altijd gegevens tooan Azure Storage-account, dus u toocreate Hallo opslag eerst moet.</span><span class="sxs-lookup"><span data-stu-id="1d845-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="1d845-118">Een opslagaccount maken in uw abonnement in Hallo [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="1d845-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![Kies nieuw, gegevens, opslag in Azure-portal.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="1d845-122">Een container maken</span><span class="sxs-lookup"><span data-stu-id="1d845-122">Create a container</span></span>
   
    ![In de nieuwe opslag hello, Containers selecteren, klikt u op Hallo Containers tegel en klik vervolgens op toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="1d845-124">Hallo-toegangssleutel voor opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="1d845-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="1d845-125">U hebt deze nodig snel tooset up Hallo invoer toohello stream analytics-service.</span><span class="sxs-lookup"><span data-stu-id="1d845-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Instellingen, sleutels, open in Hallo opslag, en een kopie van de primaire toegangssleutel Hallo](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="1d845-127">Continue export tooAzure opslag starten</span><span class="sxs-lookup"><span data-stu-id="1d845-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="1d845-128">Blader in hello Azure-portal, Application Insights-resource toohello die u hebt gemaakt voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d845-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="1d845-130">Maak een continue export.</span><span class="sxs-lookup"><span data-stu-id="1d845-130">Create a continuous export.</span></span>
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="1d845-132">Selecteer Hallo-opslagaccount die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="1d845-132">Select hello storage account you created earlier:</span></span>

    ![Hallo exportbestemming instellen](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="1d845-134">Hallo gebeurtenistypen gewenste toosee instellen:</span><span class="sxs-lookup"><span data-stu-id="1d845-134">Set hello event types you want toosee:</span></span>

    ![Gebeurtenistypen kiezen](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="1d845-136">Laat een aantal gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="1d845-136">Let some data accumulate.</span></span> <span data-ttu-id="1d845-137">Terug zitten en toestaan dat uw toepassing een tijdje gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1d845-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="1d845-138">Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1d845-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="1d845-139">En ook Hallo gegevens tooyour opslag worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="1d845-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="1d845-140">Inspecteer Hallo geëxporteerd-gegevens in de portal Hallo - kiezen **Bladeren**, selecteer uw storage-account en vervolgens **Containers** - of in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d845-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="1d845-141">Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag.</span><span class="sxs-lookup"><span data-stu-id="1d845-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="1d845-142">(Als u deze optie niet hebt, moet u tooinstall hello Azure SDK: Open het dialoogvenster Nieuw Project Hallo en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)</span><span class="sxs-lookup"><span data-stu-id="1d845-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Open in Visual Studio Server Browser, Azure, opslag](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="1d845-144">Noteer Hallo deel van de padnaam hello, die is afgeleid van naam en instrumentation sleutel van Hallo van toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d845-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="1d845-145">Hallo-gebeurtenissen worden tooblob bestanden geschreven in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1d845-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="1d845-146">Elk bestand kan een of meer gebeurtenissen bevatten.</span><span class="sxs-lookup"><span data-stu-id="1d845-146">Each file may contain one or more events.</span></span> <span data-ttu-id="1d845-147">Dus willen we graag tooread Hallo gebeurtenisgegevens en filter Hallo velden die we willen.</span><span class="sxs-lookup"><span data-stu-id="1d845-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="1d845-148">Er zijn alle soorten wat die we met de Hallo gegevens kan doen, maar onze plan is vandaag de dag toouse Stream Analytics toomove Hallo gegevens tooa SQL-database.</span><span class="sxs-lookup"><span data-stu-id="1d845-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="1d845-149">Dat kunt u eenvoudig toorun veel interessante query's.</span><span class="sxs-lookup"><span data-stu-id="1d845-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="1d845-150">Een Azure SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="1d845-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="1d845-151">Opnieuw starten vanuit uw abonnement in [Azure-portal][portal], Hallo-database maken (en een nieuwe server, tenzij u er al hebt verkregen) toowhich schrijft u Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="1d845-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Nieuw, gegevens, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="1d845-153">Zorg ervoor dat databaseserver Hallo kan toegang tooAzure services:</span><span class="sxs-lookup"><span data-stu-id="1d845-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Bladeren, Servers, uw server, instellingen, Firewall, tooAzure toegang toestaan](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="1d845-155">Een tabel maken in Azure SQL DB</span><span class="sxs-lookup"><span data-stu-id="1d845-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="1d845-156">Verbinding maken met toohello-database die zijn gemaakt in de vorige sectie Hallo met het beheerprogramma van uw voorkeur.</span><span class="sxs-lookup"><span data-stu-id="1d845-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="1d845-157">In dit overzicht we gebruiken [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="1d845-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="1d845-158">Een nieuwe query maken en uitvoeren van de volgende T-SQL Hallo:</span><span class="sxs-lookup"><span data-stu-id="1d845-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="1d845-159">In dit voorbeeld gebruiken we gegevens van paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="1d845-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="1d845-160">toosee Hallo van andere gegevens die beschikbaar zijn, inspecteren van de JSON-uitvoer en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="1d845-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="1d845-161">Azure Stream Analytics-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="1d845-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="1d845-162">Van Hallo [klassieke Azure Portal](https://manage.windowsazure.com/)hello Azure Stream Analytics-service en selecteer een nieuwe Stream Analytics-taak maken:</span><span class="sxs-lookup"><span data-stu-id="1d845-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="1d845-163">Als de nieuwe taak Hallo is gemaakt, vouwt u de details ervan:</span><span class="sxs-lookup"><span data-stu-id="1d845-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="1d845-164">Locatie van de blob instellen</span><span class="sxs-lookup"><span data-stu-id="1d845-164">Set blob location</span></span>
<span data-ttu-id="1d845-165">Deze tootake invoer van uw blob continue Export instellen:</span><span class="sxs-lookup"><span data-stu-id="1d845-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="1d845-166">Nu moet u Hallo primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="1d845-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="1d845-167">Stel dit in als Hallo Opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="1d845-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="1d845-168">Set pad voorvoegselpatroon</span><span class="sxs-lookup"><span data-stu-id="1d845-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="1d845-169">Ervoor tooset Hallo datumnotatie te worden**jjjj-MM-DD** (met **streepjes**).</span><span class="sxs-lookup"><span data-stu-id="1d845-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="1d845-170">Hallo pad voorvoegsel patroon geeft aan hoe Stream Analytics Hallo invoerbestanden vindt in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="1d845-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="1d845-171">U moet tooset het toocorrespond toohow continue Export Hallo-gegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="1d845-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="1d845-172">Stel deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="1d845-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="1d845-173">In dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1d845-173">In this example:</span></span>

* <span data-ttu-id="1d845-174">`webapplication27`Hallo-naam van Hallo Application Insights-resource **allemaal in kleine letters**.</span><span class="sxs-lookup"><span data-stu-id="1d845-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="1d845-175">`1234...`de instrumentatiesleutel Hallo Hallo Application Insights-resource is **met streepjes verwijderd**.</span><span class="sxs-lookup"><span data-stu-id="1d845-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="1d845-176">`PageViews`Hallo-type van de gegevens die we willen tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="1d845-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="1d845-177">de beschikbare typen Hello, is afhankelijk van Hallo filter die u in de continue Export instellen.</span><span class="sxs-lookup"><span data-stu-id="1d845-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="1d845-178">Bekijk Hallo geëxporteerde gegevens toosee Hallo andere beschikbare typen en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="1d845-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="1d845-179">`/{date}/{time}`een patroon er wordt letterlijk geschreven.</span><span class="sxs-lookup"><span data-stu-id="1d845-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="1d845-180">tooget hello naam en sleutel van uw Application Insights-resource Essentials openen op de overzichtspagina of instellingen openen.</span><span class="sxs-lookup"><span data-stu-id="1d845-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="1d845-181">De eerste installatie voltooien</span><span class="sxs-lookup"><span data-stu-id="1d845-181">Finish initial setup</span></span>
<span data-ttu-id="1d845-182">Bevestig Hallo serialisatie-indeling:</span><span class="sxs-lookup"><span data-stu-id="1d845-182">Confirm hello serialization format:</span></span>

![Bevestigen en de wizard te sluiten](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="1d845-184">Hallo wizard te sluiten en wachten op Hallo setup toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1d845-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="1d845-185">Gebruik Hallo voorbeeld functie toocheck Hallo invoer pad correct ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1d845-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="1d845-186">Als dit mislukt: Controleer of er gegevens in de opslag Hallo voor Hallo voorbeeld-tijdsbereik u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="1d845-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="1d845-187">Hallo invoer definitie bewerken en controleer u Hallo storage-account, pad voorvoegsel ingesteld en datumnotatie correct.</span><span class="sxs-lookup"><span data-stu-id="1d845-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="1d845-188">Set-query</span><span class="sxs-lookup"><span data-stu-id="1d845-188">Set query</span></span>
<span data-ttu-id="1d845-189">Open gedeelte Hallo-query:</span><span class="sxs-lookup"><span data-stu-id="1d845-189">Open hello query section:</span></span>

![Selecteer in de stream analytics, Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="1d845-191">Vervang de standaardquery Hallo met:</span><span class="sxs-lookup"><span data-stu-id="1d845-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="1d845-192">U ziet dat Hallo eerst enkele eigenschappen zijn gegevens van specifieke toopage weergeven.</span><span class="sxs-lookup"><span data-stu-id="1d845-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="1d845-193">Uitvoer van andere typen telemetrie heeft andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1d845-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="1d845-194">Zie Hallo [gedetailleerde gegevens modelverwijzing voor Hallo eigenschaptypen en waarden.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="1d845-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="1d845-195">Uitvoer toodatabase instellen</span><span class="sxs-lookup"><span data-stu-id="1d845-195">Set up output toodatabase</span></span>
<span data-ttu-id="1d845-196">Selecteer SQL als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1d845-196">Select SQL as hello output.</span></span>

![Selecteer in de stream analytics, uitvoer](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="1d845-198">Geef Hallo SQL-database.</span><span class="sxs-lookup"><span data-stu-id="1d845-198">Specify hello SQL database.</span></span>

![Vul Hallo details van de database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="1d845-200">Hallo wizard te sluiten en wachten op een melding dat Hallo uitvoer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1d845-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="1d845-201">Verwerking starten</span><span class="sxs-lookup"><span data-stu-id="1d845-201">Start processing</span></span>
<span data-ttu-id="1d845-202">Hallo taak vanuit Hallo actiebalk starten:</span><span class="sxs-lookup"><span data-stu-id="1d845-202">Start hello job from hello action bar:</span></span>

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="1d845-204">U kunt kiezen of toostart verwerking Hallo gegevens vanaf nu of toostart met oudere gegevens.</span><span class="sxs-lookup"><span data-stu-id="1d845-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="1d845-205">Hallo laatste is handig als u hebt continue Export is al een tijdje wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1d845-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="1d845-207">Ga terug tooSQL Server-beheerprogramma's na een paar minuten en bekijkt hello gegevens stromende.</span><span class="sxs-lookup"><span data-stu-id="1d845-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="1d845-208">Gebruik bijvoorbeeld een query als volgt:</span><span class="sxs-lookup"><span data-stu-id="1d845-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="1d845-209">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="1d845-209">Related articles</span></span>
* [<span data-ttu-id="1d845-210">Met Stream Analytics tooPowerBI exporteren</span><span class="sxs-lookup"><span data-stu-id="1d845-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="1d845-211">Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="1d845-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="1d845-212">Continue Export in de Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d845-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="1d845-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d845-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

