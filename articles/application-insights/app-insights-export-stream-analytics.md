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
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="a3989-103">Gebruik Stream Analytics tooprocess geëxporteerde gegevens van Application Insights</span><span class="sxs-lookup"><span data-stu-id="a3989-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="a3989-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is ideaal Hallo-hulpprogramma voor het verwerken van gegevens [geëxporteerd uit de Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="a3989-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="a3989-105">Stream Analytics kunt ophalen van gegevens uit verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="a3989-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="a3989-106">U kunt transformeren en Hallo gegevens filteren en routeren vervolgens tooa diverse Put.</span><span class="sxs-lookup"><span data-stu-id="a3989-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="a3989-107">In dit voorbeeld maakt u een netwerkadapter die worden gegevens uit de Application Insights, naam en het doorgesluisd naar Power BI verwerkt aantal Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="a3989-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="a3989-108">Er zijn veel beter en eenvoudiger [aanbevolen manieren toodisplay Application Insights-gegevens in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a3989-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="a3989-109">Hallo pad hier geïllustreerd is slechts een voorbeeld tooillustrate hoe tooprocess geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="a3989-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagram voor exporteren via SA tooPBI blokkeren](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="a3989-111">Maken van opslag in Azure</span><span class="sxs-lookup"><span data-stu-id="a3989-111">Create storage in Azure</span></span>
<span data-ttu-id="a3989-112">Continue export levert altijd gegevens tooan Azure Storage-account, dus u toocreate Hallo opslag eerst moet.</span><span class="sxs-lookup"><span data-stu-id="a3989-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="a3989-113">Een 'klassiek' storage-account maken in uw abonnement in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3989-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![Kies nieuw, gegevens, opslag in Azure-portal](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="a3989-115">Een container maken</span><span class="sxs-lookup"><span data-stu-id="a3989-115">Create a container</span></span>
   
    ![In de nieuwe opslag hello, Containers selecteren, klikt u op Hallo Containers tegel en klik vervolgens op toevoegen](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="a3989-117">Hallo-toegangssleutel voor opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="a3989-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="a3989-118">U hebt deze nodig snel tooset up Hallo invoer toohello stream analytics-service.</span><span class="sxs-lookup"><span data-stu-id="a3989-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Instellingen, sleutels, open in Hallo opslag, en een kopie van de primaire toegangssleutel Hallo](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="a3989-120">Continue export tooAzure opslag starten</span><span class="sxs-lookup"><span data-stu-id="a3989-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="a3989-121">[Continue export](app-insights-export-telemetry.md) worden gegevens uit de Application Insights in Azure-opslag verplaatst.</span><span class="sxs-lookup"><span data-stu-id="a3989-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="a3989-122">Blader in hello Azure-portal, Application Insights-resource toohello die u hebt gemaakt voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3989-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="a3989-124">Maak een continue export.</span><span class="sxs-lookup"><span data-stu-id="a3989-124">Create a continuous export.</span></span>
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="a3989-126">Selecteer Hallo-opslagaccount die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="a3989-126">Select hello storage account you created earlier:</span></span>

    ![Hallo exportbestemming instellen](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="a3989-128">Hallo gebeurtenistypen gewenste toosee instellen:</span><span class="sxs-lookup"><span data-stu-id="a3989-128">Set hello event types you want toosee:</span></span>

    ![Gebeurtenistypen kiezen](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="a3989-130">Laat een aantal gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="a3989-130">Let some data accumulate.</span></span> <span data-ttu-id="a3989-131">Terug zitten en toestaan dat uw toepassing een tijdje gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a3989-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="a3989-132">Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a3989-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="a3989-133">En ook Hallo gegevens tooyour opslag worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="a3989-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="a3989-134">Hallo geëxporteerd gegevens te controleren.</span><span class="sxs-lookup"><span data-stu-id="a3989-134">Inspect hello exported data.</span></span> <span data-ttu-id="a3989-135">Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag.</span><span class="sxs-lookup"><span data-stu-id="a3989-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="a3989-136">(Als u deze optie niet hebt, moet u tooinstall hello Azure SDK: Open het dialoogvenster Nieuw Project Hallo en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)</span><span class="sxs-lookup"><span data-stu-id="a3989-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="a3989-137">Noteer Hallo deel van de padnaam hello, die is afgeleid van naam en instrumentation sleutel van Hallo van toepassing.</span><span class="sxs-lookup"><span data-stu-id="a3989-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="a3989-138">Hallo-gebeurtenissen worden tooblob bestanden geschreven in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a3989-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="a3989-139">Elk bestand kan een of meer gebeurtenissen bevatten.</span><span class="sxs-lookup"><span data-stu-id="a3989-139">Each file may contain one or more events.</span></span> <span data-ttu-id="a3989-140">Dus willen we graag tooread Hallo gebeurtenisgegevens en filter Hallo velden die we willen.</span><span class="sxs-lookup"><span data-stu-id="a3989-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="a3989-141">Er zijn alle soorten wat die we met de Hallo gegevens kan doen, maar onze plan is vandaag de dag toouse Stream Analytics toopipe Hallo gegevens tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="a3989-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="a3989-142">Azure Stream Analytics-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="a3989-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="a3989-143">Van Hallo [klassieke Azure Portal](https://manage.windowsazure.com/)hello Azure Stream Analytics-service en selecteer een nieuwe Stream Analytics-taak maken:</span><span class="sxs-lookup"><span data-stu-id="a3989-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="a3989-144">Als de nieuwe taak Hallo is gemaakt, vouwt u de details ervan:</span><span class="sxs-lookup"><span data-stu-id="a3989-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="a3989-145">Locatie van de blob instellen</span><span class="sxs-lookup"><span data-stu-id="a3989-145">Set blob location</span></span>
<span data-ttu-id="a3989-146">Deze tootake invoer van uw blob continue Export instellen:</span><span class="sxs-lookup"><span data-stu-id="a3989-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="a3989-147">Nu moet u Hallo primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="a3989-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="a3989-148">Stel dit in als Hallo Opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="a3989-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="a3989-149">Set pad voorvoegselpatroon</span><span class="sxs-lookup"><span data-stu-id="a3989-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="a3989-150">**Worden ervoor tooset Hallo datumnotatie tooYYYY-MM-DD (met streepjes).**</span><span class="sxs-lookup"><span data-stu-id="a3989-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="a3989-151">Hallo pad voorvoegsel patroon geeft aan waar Stream Analytics Hallo invoerbestanden vindt in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="a3989-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="a3989-152">U moet tooset het toocorrespond toohow continue Export Hallo-gegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="a3989-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="a3989-153">Stel deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="a3989-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="a3989-154">In dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a3989-154">In this example:</span></span>

* <span data-ttu-id="a3989-155">`webapplication27`Hallo-naam van Hallo Application Insights-resource **alle kleine letters**.</span><span class="sxs-lookup"><span data-stu-id="a3989-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="a3989-156">`1234...`de instrumentatiesleutel Hallo Hallo Application Insights-resource is **weglaten streepjes**.</span><span class="sxs-lookup"><span data-stu-id="a3989-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="a3989-157">`PageViews`Hallo type gegevens dat u wilt dat tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="a3989-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="a3989-158">de beschikbare typen Hello, is afhankelijk van Hallo filter die u in de continue Export instellen.</span><span class="sxs-lookup"><span data-stu-id="a3989-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="a3989-159">Bekijk Hallo geëxporteerde gegevens toosee Hallo andere beschikbare typen en Zie Hallo [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a3989-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="a3989-160">`/{date}/{time}`een patroon er wordt letterlijk geschreven.</span><span class="sxs-lookup"><span data-stu-id="a3989-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="a3989-161">Hallo opslag toomake zeker dat u direct Hallo pad controleren.</span><span class="sxs-lookup"><span data-stu-id="a3989-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="a3989-162">De eerste installatie voltooien</span><span class="sxs-lookup"><span data-stu-id="a3989-162">Finish initial setup</span></span>
<span data-ttu-id="a3989-163">Bevestig Hallo serialisatie-indeling:</span><span class="sxs-lookup"><span data-stu-id="a3989-163">Confirm hello serialization format:</span></span>

![Bevestigen en de wizard te sluiten](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="a3989-165">Hallo wizard te sluiten en wachten op Hallo setup toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a3989-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="a3989-166">Hallo voorbeeld opdracht toodownload sommige gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a3989-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="a3989-167">Houd het als een voorbeeld test toodebug uw query.</span><span class="sxs-lookup"><span data-stu-id="a3989-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="a3989-168">Set Hallo-uitvoer</span><span class="sxs-lookup"><span data-stu-id="a3989-168">Set hello output</span></span>
<span data-ttu-id="a3989-169">Nu uw taak selecteren en instellen van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a3989-169">Now select your job and set hello output.</span></span>

![Selecteer Nieuw kanaal hello, klikt u op de uitvoer, toevoegen, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="a3989-171">Geef uw **werk- of schoolaccount** tooauthorize Stream Analytics tooaccess uw Power BI-resource.</span><span class="sxs-lookup"><span data-stu-id="a3989-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="a3989-172">Vervolgens tot een naam voor uitvoer Hallo en voor Hallo doel Power BI gegevensset en tabel.</span><span class="sxs-lookup"><span data-stu-id="a3989-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Drie namen voorraad](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="a3989-174">Set Hallo query</span><span class="sxs-lookup"><span data-stu-id="a3989-174">Set hello query</span></span>
<span data-ttu-id="a3989-175">Hallo query beheerst Hallo vertaling van invoer toooutput.</span><span class="sxs-lookup"><span data-stu-id="a3989-175">hello query governs hello translation from input toooutput.</span></span>

![Hallo taak selecteren en klik op de Query.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="a3989-178">Hallo Test functie toocheck ophalen van de juiste uitvoer hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a3989-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="a3989-179">Geef het Hallo-voorbeeldgegevens die u hebt gemaakt van Hallo invoer pagina.</span><span class="sxs-lookup"><span data-stu-id="a3989-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="a3989-180">Query toodisplay tellingen van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="a3989-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="a3989-181">Plak deze query:</span><span class="sxs-lookup"><span data-stu-id="a3989-181">Paste this query:</span></span>

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

* <span data-ttu-id="a3989-182">export-invoer is Hallo alias gaven wij toohello Stroominvoer</span><span class="sxs-lookup"><span data-stu-id="a3989-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="a3989-183">pbi-uitvoer is Hallo uitvoeraliassen is gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="a3989-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="a3989-184">We gebruiken [buitenste toepassen GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) omdat Hallo gebeurtenisnaam zich in een geneste JSON arrray.</span><span class="sxs-lookup"><span data-stu-id="a3989-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="a3989-185">Selecteer uitgelicht Hallo Hallo vervolgens gebeurtenisnaam, samen met een telling van het aantal exemplaren met die naam aanwezig in Hallo periode Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3989-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="a3989-186">Hallo [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) component Hallo elementen gegroepeerd in perioden van 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="a3989-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="a3989-187">Query toodisplay metrische waarden</span><span class="sxs-lookup"><span data-stu-id="a3989-187">Query toodisplay metric values</span></span>
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

* <span data-ttu-id="a3989-188">Deze query ingezoomd in Hallo metrische gegevens telemetrie tooget Hallo gebeurtenistijd en Hallo metrische waarde.</span><span class="sxs-lookup"><span data-stu-id="a3989-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="a3989-189">Hallo metrische waarden zijn binnen een matrix, zodat we Hallo buitenste toepassen GetElements patroon tooextract Hallo rijen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a3989-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="a3989-190">'myMetric' hello naam is van Hallo metrische gegevens in dit geval.</span><span class="sxs-lookup"><span data-stu-id="a3989-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="a3989-191">Query tooinclude waarden van de dimensie-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a3989-191">Query tooinclude values of dimension properties</span></span>
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

* <span data-ttu-id="a3989-192">Deze query bevat de waarden van eigenschappen zonder dimensie afhankelijk van een bepaalde dimensie wordt op een vaste index in een matrix dimensie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3989-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="a3989-193">Hallo-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a3989-193">Run hello job</span></span>
<span data-ttu-id="a3989-194">U kunt een datum selecteren in Hallo toostart Hallo taak in het verleden.</span><span class="sxs-lookup"><span data-stu-id="a3989-194">You can select a date in hello past toostart hello job from.</span></span> 

![Hallo taak selecteren en klik op de Query.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="a3989-197">Wacht totdat het Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3989-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="a3989-198">Weergeven van resultaten in Power BI</span><span class="sxs-lookup"><span data-stu-id="a3989-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="a3989-199">Er zijn veel beter en eenvoudiger [aanbevolen manieren toodisplay Application Insights-gegevens in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a3989-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="a3989-200">Hallo pad hier geïllustreerd is slechts een voorbeeld tooillustrate hoe tooprocess geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="a3989-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="a3989-201">Power BI met uw werk of schoolaccount, en selecteer Hallo gegevensset en tabel die u hebt gedefinieerd als uitvoer van de Stream Analytics-taak Hallo Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="a3989-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="a3989-203">Nu kunt u deze gegevensset in rapporten en dashboards in [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a3989-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="a3989-205">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="a3989-205">No data?</span></span>
* <span data-ttu-id="a3989-206">Controleer dat u [set Hallo datumnotatie](#set-path-prefix-pattern) correct tooYYYY-MM-DD (met streepjes).</span><span class="sxs-lookup"><span data-stu-id="a3989-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="a3989-207">Video</span><span class="sxs-lookup"><span data-stu-id="a3989-207">Video</span></span>
<span data-ttu-id="a3989-208">Noam Ben Zeev ziet u hoe tooprocess gegevens met behulp van de Stream Analytics geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="a3989-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a3989-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3989-209">Next steps</span></span>
* [<span data-ttu-id="a3989-210">Continue export</span><span class="sxs-lookup"><span data-stu-id="a3989-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="a3989-211">Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="a3989-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="a3989-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a3989-212">Application Insights</span></span>](app-insights-overview.md)

