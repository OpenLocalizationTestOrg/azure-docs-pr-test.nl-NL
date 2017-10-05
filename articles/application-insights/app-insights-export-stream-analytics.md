---
title: Exporteren met behulp van de Stream Analytics uit Azure Application Insights | Microsoft Docs
description: Stream Analytics kunt continu transformeren, filteren en doorsturen van de gegevens die u uit de Application Insights exporteren.
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
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="fb84c-103">Gebruik van Stream Analytics voor het verwerken van de geëxporteerde gegevens van Application Insights</span><span class="sxs-lookup"><span data-stu-id="fb84c-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="fb84c-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is het ideaal hulpprogramma voor het verwerken van gegevens [geëxporteerd uit de Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="fb84c-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="fb84c-105">Stream Analytics kunt ophalen van gegevens uit verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="fb84c-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="fb84c-106">U kunt transformeren en filter de gegevens en vervolgens doorsturen naar een groot aantal Put.</span><span class="sxs-lookup"><span data-stu-id="fb84c-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="fb84c-107">In dit voorbeeld maakt u een netwerkadapter die worden gegevens uit de Application Insights, naam en het doorgesluisd naar Power BI sommige velden worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="fb84c-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="fb84c-108">Er zijn veel beter en eenvoudiger [aanbevolen manieren Application Insights-gegevens weergeven in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="fb84c-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="fb84c-109">Het pad hier geïllustreerd is slechts een voorbeeld ter illustratie van de geëxporteerde gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="fb84c-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Diagram voor exporteren via SA naar PBI blokkeren](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="fb84c-111">Maken van opslag in Azure</span><span class="sxs-lookup"><span data-stu-id="fb84c-111">Create storage in Azure</span></span>
<span data-ttu-id="fb84c-112">Continue export levert altijd gegevens aan een Azure Storage-account, dus u moet de opslag om eerst te maken.</span><span class="sxs-lookup"><span data-stu-id="fb84c-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="fb84c-113">Een 'klassiek' storage-account maken in uw abonnement in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb84c-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![Kies nieuw, gegevens, opslag in Azure-portal](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="fb84c-115">Een container maken</span><span class="sxs-lookup"><span data-stu-id="fb84c-115">Create a container</span></span>
   
    ![In de nieuwe opslag Containers selecteren, klikt u op de tegel Containers en toevoegen](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="fb84c-117">De toegangssleutel voor opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="fb84c-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="fb84c-118">U moet deze snel voor het instellen van de invoer van de stream analytics-service.</span><span class="sxs-lookup"><span data-stu-id="fb84c-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Instellingen, sleutels, open in de opslag, en een kopie van de primaire toegangssleutel](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="fb84c-120">Start de continue export naar Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="fb84c-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="fb84c-121">[Continue export](app-insights-export-telemetry.md) worden gegevens uit de Application Insights in Azure-opslag verplaatst.</span><span class="sxs-lookup"><span data-stu-id="fb84c-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="fb84c-122">Blader naar de Application Insights-resource die u hebt gemaakt voor uw toepassing in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fb84c-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="fb84c-124">Maak een continue export.</span><span class="sxs-lookup"><span data-stu-id="fb84c-124">Create a continuous export.</span></span>
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="fb84c-126">Selecteer het opslagaccount dat u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="fb84c-126">Select the storage account you created earlier:</span></span>

    ![Stel de doelserver exporteren](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="fb84c-128">Stel de typen gebeurtenissen die u wilt zien:</span><span class="sxs-lookup"><span data-stu-id="fb84c-128">Set the event types you want to see:</span></span>

    ![Gebeurtenistypen kiezen](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="fb84c-130">Laat een aantal gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="fb84c-130">Let some data accumulate.</span></span> <span data-ttu-id="fb84c-131">Terug zitten en toestaan dat uw toepassing een tijdje gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fb84c-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="fb84c-132">Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="fb84c-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="fb84c-133">En ook de gegevens worden geëxporteerd naar uw opslag.</span><span class="sxs-lookup"><span data-stu-id="fb84c-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="fb84c-134">Inspecteer de geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="fb84c-134">Inspect the exported data.</span></span> <span data-ttu-id="fb84c-135">Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag.</span><span class="sxs-lookup"><span data-stu-id="fb84c-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="fb84c-136">(Als u deze optie niet hebt, moet u de Azure SDK installeren: Open het dialoogvenster New Project en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)</span><span class="sxs-lookup"><span data-stu-id="fb84c-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="fb84c-137">Noteer het algemene gedeelte van de padnaam die is afgeleid van de sleutel voor naam en instrumentatie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="fb84c-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="fb84c-138">De gebeurtenissen worden geschreven naar de blob-bestanden in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="fb84c-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="fb84c-139">Elk bestand kan een of meer gebeurtenissen bevatten.</span><span class="sxs-lookup"><span data-stu-id="fb84c-139">Each file may contain one or more events.</span></span> <span data-ttu-id="fb84c-140">Dus willen we gelezen gegevens van de gebeurtenis en de velden die we wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="fb84c-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="fb84c-141">Er zijn alle soorten wat die we met de gegevens doen kan, maar onze plan is vandaag de dag Stream Analytics gebruiken naar de gegevens met Power BI pipe.</span><span class="sxs-lookup"><span data-stu-id="fb84c-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="fb84c-142">Azure Stream Analytics-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="fb84c-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="fb84c-143">Van de [klassieke Azure Portal](https://manage.windowsazure.com/), selecteer de Azure Stream Analytics-service en een nieuwe Stream Analytics-taak maken:</span><span class="sxs-lookup"><span data-stu-id="fb84c-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="fb84c-144">Als de nieuwe taak is gemaakt, vouwt u de details ervan:</span><span class="sxs-lookup"><span data-stu-id="fb84c-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="fb84c-145">Locatie van de blob instellen</span><span class="sxs-lookup"><span data-stu-id="fb84c-145">Set blob location</span></span>
<span data-ttu-id="fb84c-146">Stel deze in op invoer van uw blob continue Export nemen:</span><span class="sxs-lookup"><span data-stu-id="fb84c-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="fb84c-147">Nu moet u de primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="fb84c-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="fb84c-148">Stel dit in als de sleutel van het Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fb84c-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="fb84c-149">Set pad voorvoegselpatroon</span><span class="sxs-lookup"><span data-stu-id="fb84c-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="fb84c-150">**Zorg ervoor dat de datumnotatie ingesteld op jjjj-MM-DD (met streepjes).**</span><span class="sxs-lookup"><span data-stu-id="fb84c-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="fb84c-151">Het pad naar het voorvoegsel patroon geeft aan waar de invoerbestanden in Stream Analytics worden gevonden in de opslag.</span><span class="sxs-lookup"><span data-stu-id="fb84c-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="fb84c-152">U moet worden ingesteld in overeenstemming met continue Export hoe de gegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="fb84c-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="fb84c-153">Stel deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb84c-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="fb84c-154">In dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fb84c-154">In this example:</span></span>

* <span data-ttu-id="fb84c-155">`webapplication27`de naam van de Application Insights-resource **alle kleine letters**.</span><span class="sxs-lookup"><span data-stu-id="fb84c-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="fb84c-156">`1234...`de instrumentatiesleutel van de Application Insights-resource is **weglaten streepjes**.</span><span class="sxs-lookup"><span data-stu-id="fb84c-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="fb84c-157">`PageViews`is het type gegevens dat u wilt analyseren.</span><span class="sxs-lookup"><span data-stu-id="fb84c-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="fb84c-158">De beschikbare typen, is afhankelijk van het filter dat u in de continue Export instellen.</span><span class="sxs-lookup"><span data-stu-id="fb84c-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="fb84c-159">De geëxporteerde gegevens om de beschikbare typen Zie en bekijk de [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="fb84c-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="fb84c-160">`/{date}/{time}`een patroon er wordt letterlijk geschreven.</span><span class="sxs-lookup"><span data-stu-id="fb84c-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="fb84c-161">Inspecteer de opslag om ervoor te zorgen dat u het pad naar rechts.</span><span class="sxs-lookup"><span data-stu-id="fb84c-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="fb84c-162">De eerste installatie voltooien</span><span class="sxs-lookup"><span data-stu-id="fb84c-162">Finish initial setup</span></span>
<span data-ttu-id="fb84c-163">Bevestig de serialisatie-indeling:</span><span class="sxs-lookup"><span data-stu-id="fb84c-163">Confirm the serialization format:</span></span>

![Bevestigen en de wizard te sluiten](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="fb84c-165">De wizard te sluiten en wacht totdat de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="fb84c-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="fb84c-166">De voorbeeld-opdracht gebruiken om bepaalde gegevens te downloaden.</span><span class="sxs-lookup"><span data-stu-id="fb84c-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="fb84c-167">Houd het als een voorbeeld van de test voor foutopsporing van uw query.</span><span class="sxs-lookup"><span data-stu-id="fb84c-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="fb84c-168">Stel de uitvoer</span><span class="sxs-lookup"><span data-stu-id="fb84c-168">Set the output</span></span>
<span data-ttu-id="fb84c-169">Nu uw taak selecteren en instellen van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="fb84c-169">Now select your job and set the output.</span></span>

![Selecteer het nieuwe kanaal, klikt u op de uitvoer, toevoegen, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="fb84c-171">Geef uw **werk- of schoolaccount** voor het autoriseren van Stream Analytics voor toegang tot uw Power BI-bron.</span><span class="sxs-lookup"><span data-stu-id="fb84c-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="fb84c-172">Vervolgens tot een naam voor de uitvoer en voor de Power BI-gegevensset doel en de tabel.</span><span class="sxs-lookup"><span data-stu-id="fb84c-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Drie namen voorraad](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="fb84c-174">Instellen van de query</span><span class="sxs-lookup"><span data-stu-id="fb84c-174">Set the query</span></span>
<span data-ttu-id="fb84c-175">De query bepaalt de vertaling van invoer om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fb84c-175">The query governs the translation from input to output.</span></span>

![De taak te selecteren en klik op de Query.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="fb84c-178">Gebruik de functie Test om te controleren dat u de uitvoer van de juiste krijgt.</span><span class="sxs-lookup"><span data-stu-id="fb84c-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="fb84c-179">Geef deze de voorbeeldgegevens die u hebt gemaakt van de invoer-pagina.</span><span class="sxs-lookup"><span data-stu-id="fb84c-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="fb84c-180">Query voor het aantal gebeurtenissen weergeven</span><span class="sxs-lookup"><span data-stu-id="fb84c-180">Query to display counts of events</span></span>
<span data-ttu-id="fb84c-181">Plak deze query:</span><span class="sxs-lookup"><span data-stu-id="fb84c-181">Paste this query:</span></span>

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

* <span data-ttu-id="fb84c-182">export-invoer is de alias die wordt gestuurd naar de stroom invoer</span><span class="sxs-lookup"><span data-stu-id="fb84c-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="fb84c-183">pbi-uitvoer is de uitvoeralias die is gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="fb84c-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="fb84c-184">We gebruiken [buitenste toepassen GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) omdat de gebeurtenisnaam van de in een geneste JSON arrray is.</span><span class="sxs-lookup"><span data-stu-id="fb84c-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="fb84c-185">Selecteer hervat vervolgens de naam van de gebeurtenis, samen met een telling van het aantal exemplaren met die naam aanwezig in de periode.</span><span class="sxs-lookup"><span data-stu-id="fb84c-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="fb84c-186">De [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) component elementen gegroepeerd in perioden van 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="fb84c-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="fb84c-187">Query voor metrische waarden weergeven</span><span class="sxs-lookup"><span data-stu-id="fb84c-187">Query to display metric values</span></span>
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

* <span data-ttu-id="fb84c-188">Deze query ingezoomd in de telemetrie van de metrische gegevens ophalen van de tijd van de gebeurtenis en de metrische waarde.</span><span class="sxs-lookup"><span data-stu-id="fb84c-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="fb84c-189">De metrische waarden zijn binnen een matrix, zodat we het buitenste toepassen GetElements-patroon gebruiken om op te halen van de rijen.</span><span class="sxs-lookup"><span data-stu-id="fb84c-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="fb84c-190">'myMetric' is de naam van de metrische gegevens in dit geval.</span><span class="sxs-lookup"><span data-stu-id="fb84c-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="fb84c-191">Query voor het opnemen van waarden van de dimensie-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="fb84c-191">Query to include values of dimension properties</span></span>
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

* <span data-ttu-id="fb84c-192">Deze query bevat de waarden van de dimensie-eigenschappen zonder afhankelijk van een bepaalde dimensie wordt op een vaste index in de dimensiematrix.</span><span class="sxs-lookup"><span data-stu-id="fb84c-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="fb84c-193">De taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fb84c-193">Run the job</span></span>
<span data-ttu-id="fb84c-194">U kunt een datum selecteren in het verleden om de taak uit te starten.</span><span class="sxs-lookup"><span data-stu-id="fb84c-194">You can select a date in the past to start the job from.</span></span> 

![De taak te selecteren en klik op de Query.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="fb84c-197">Wacht totdat de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fb84c-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="fb84c-198">Weergeven van resultaten in Power BI</span><span class="sxs-lookup"><span data-stu-id="fb84c-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="fb84c-199">Er zijn veel beter en eenvoudiger [aanbevolen manieren Application Insights-gegevens weergeven in Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="fb84c-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="fb84c-200">Het pad hier geïllustreerd is slechts een voorbeeld ter illustratie van de geëxporteerde gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="fb84c-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="fb84c-201">Power BI openen met uw werk of school-account en selecteer de gegevensset en de tabel die u hebt gedefinieerd als de uitvoer van de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="fb84c-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="fb84c-203">Nu kunt u deze gegevensset in rapporten en dashboards in [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fb84c-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Selecteer uw gegevensset en de velden in Power BI.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="fb84c-205">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="fb84c-205">No data?</span></span>
* <span data-ttu-id="fb84c-206">Controleer dat u [datumnotatie instellen](#set-path-prefix-pattern) correct naar jjjj-MM-DD (met streepjes).</span><span class="sxs-lookup"><span data-stu-id="fb84c-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="fb84c-207">Video</span><span class="sxs-lookup"><span data-stu-id="fb84c-207">Video</span></span>
<span data-ttu-id="fb84c-208">Noam Ben Zeev laat zien hoe geëxporteerde gegevens met behulp van de Stream Analytics verwerken.</span><span class="sxs-lookup"><span data-stu-id="fb84c-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fb84c-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb84c-209">Next steps</span></span>
* [<span data-ttu-id="fb84c-210">Continue export</span><span class="sxs-lookup"><span data-stu-id="fb84c-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="fb84c-211">Gedetailleerde gegevens model verwijzing voor de eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="fb84c-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="fb84c-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="fb84c-212">Application Insights</span></span>](app-insights-overview.md)

