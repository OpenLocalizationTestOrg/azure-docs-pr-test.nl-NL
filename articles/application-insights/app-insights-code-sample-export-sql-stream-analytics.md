---
title: Exporteren naar SQL van Azure Application Insights | Microsoft Docs
description: Continu Application Insights gegevens exporteren naar SQL met Stream Analytics.
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
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="00a6a-103">Overzicht: Exporteren naar SQL van Application Insights met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00a6a-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="00a6a-104">Dit artikel laat zien hoe u verplaatst uw telemetriegegevens van [Azure Application Insights] [ start] in een Azure SQL database met behulp van [continue Export] [ export] en [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="00a6a-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="00a6a-105">Continue export verplaatst de telemetriegegevens naar Azure Storage in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="00a6a-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="00a6a-106">We parseren van de JSON-objecten met behulp van Azure Stream Analytics en rijen in een databasetabel te maken.</span><span class="sxs-lookup"><span data-stu-id="00a6a-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="00a6a-107">(Meer in het algemeen continue Export is de manier om uw eigen analyse van de telemetrie die uw apps naar Application Insights verzenden.</span><span class="sxs-lookup"><span data-stu-id="00a6a-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="00a6a-108">U kunt dit codevoorbeeld hiervoor andere mogelijkheden met de geëxporteerde telemetriegegevens, zoals aggregatie van gegevens worden aanpassen.)</span><span class="sxs-lookup"><span data-stu-id="00a6a-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="00a6a-109">We beginnen met de veronderstelling dat u al hebt de app die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="00a6a-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="00a6a-110">We gebruiken de gegevens van de pagina in dit voorbeeld, maar dit patroon kan gemakkelijk worden uitgebreid naar andere gegevenstypen zoals aangepaste gebeurtenissen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="00a6a-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="00a6a-111">Application Insights toevoegen aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="00a6a-111">Add Application Insights to your application</span></span>
<span data-ttu-id="00a6a-112">Aan de slag:</span><span class="sxs-lookup"><span data-stu-id="00a6a-112">To get started:</span></span>

1. <span data-ttu-id="00a6a-113">[Application Insights instellen voor uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="00a6a-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="00a6a-114">(In dit voorbeeld we ligt de nadruk op gegevens van de pagina weergeven in de clientbrowsers verwerking, maar u kunt Application Insights instellen voor de serverkant van uw [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) -app en verwerking van aanvragen, afhankelijkheden en andere servertelemetrie.)</span><span class="sxs-lookup"><span data-stu-id="00a6a-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="00a6a-115">Uw app publiceren en bekijk de telemetrische gegevens verschijnen in uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="00a6a-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="00a6a-116">Maken van opslag in Azure</span><span class="sxs-lookup"><span data-stu-id="00a6a-116">Create storage in Azure</span></span>
<span data-ttu-id="00a6a-117">Continue export levert altijd gegevens aan een Azure Storage-account, dus u moet de opslag om eerst te maken.</span><span class="sxs-lookup"><span data-stu-id="00a6a-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="00a6a-118">Een opslagaccount maken in uw abonnement in de [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="00a6a-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![Kies nieuw, gegevens, opslag in Azure-portal.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="00a6a-122">Een container maken</span><span class="sxs-lookup"><span data-stu-id="00a6a-122">Create a container</span></span>
   
    ![In de nieuwe opslag Containers selecteren, klikt u op de tegel Containers en toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="00a6a-124">De toegangssleutel voor opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="00a6a-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="00a6a-125">U moet deze snel voor het instellen van de invoer van de stream analytics-service.</span><span class="sxs-lookup"><span data-stu-id="00a6a-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Instellingen, sleutels, open in de opslag, en een kopie van de primaire toegangssleutel](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="00a6a-127">Start de continue export naar Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="00a6a-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="00a6a-128">Blader naar de Application Insights-resource die u hebt gemaakt voor uw toepassing in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="00a6a-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Kies Bladeren, Application Insights uw toepassing](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="00a6a-130">Maak een continue export.</span><span class="sxs-lookup"><span data-stu-id="00a6a-130">Create a continuous export.</span></span>
   
    ![Instellingen voor continue Export toevoegen](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="00a6a-132">Selecteer het opslagaccount dat u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="00a6a-132">Select the storage account you created earlier:</span></span>

    ![Stel de doelserver exporteren](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="00a6a-134">Stel de typen gebeurtenissen die u wilt zien:</span><span class="sxs-lookup"><span data-stu-id="00a6a-134">Set the event types you want to see:</span></span>

    ![Gebeurtenistypen kiezen](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="00a6a-136">Laat een aantal gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="00a6a-136">Let some data accumulate.</span></span> <span data-ttu-id="00a6a-137">Terug zitten en toestaan dat uw toepassing een tijdje gebruiken.</span><span class="sxs-lookup"><span data-stu-id="00a6a-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="00a6a-138">Telemetrie wordt geleverd in en ziet u statistische grafieken in [metrische explorer](app-insights-metrics-explorer.md) en afzonderlijke gebeurtenissen in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="00a6a-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="00a6a-139">En ook de gegevens worden geëxporteerd naar uw opslag.</span><span class="sxs-lookup"><span data-stu-id="00a6a-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="00a6a-140">Inspecteer de geëxporteerde gegevens in de portal - kiezen **Bladeren**, selecteer uw storage-account en vervolgens **Containers** - of in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00a6a-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="00a6a-141">Kies in Visual Studio **weergeven / Cloud Explorer**, en open Azure / opslag.</span><span class="sxs-lookup"><span data-stu-id="00a6a-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="00a6a-142">(Als u deze optie niet hebt, moet u de Azure SDK installeren: Open het dialoogvenster New Project en Visual C# / Cloud / ophalen van Microsoft Azure SDK voor .NET.)</span><span class="sxs-lookup"><span data-stu-id="00a6a-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Open in Visual Studio Server Browser, Azure, opslag](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="00a6a-144">Noteer het algemene gedeelte van de padnaam die is afgeleid van de sleutel voor naam en instrumentatie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="00a6a-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="00a6a-145">De gebeurtenissen worden geschreven naar de blob-bestanden in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="00a6a-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="00a6a-146">Elk bestand kan een of meer gebeurtenissen bevatten.</span><span class="sxs-lookup"><span data-stu-id="00a6a-146">Each file may contain one or more events.</span></span> <span data-ttu-id="00a6a-147">Dus willen we gelezen gegevens van de gebeurtenis en de velden die we wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="00a6a-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="00a6a-148">Er zijn alle soorten wat die we met de gegevens doen kan, maar onze plan is vandaag de dag Stream Analytics gebruiken de gegevens worden verplaatst naar een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="00a6a-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="00a6a-149">Die wordt maakt het eenvoudig om uit te voeren veel interessante query's.</span><span class="sxs-lookup"><span data-stu-id="00a6a-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="00a6a-150">Een Azure SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="00a6a-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="00a6a-151">Opnieuw starten vanuit uw abonnement in [Azure-portal][portal], de database maken (en een nieuwe server, tenzij u er al hebt verkregen) die u gaat het om gegevens te schrijven.</span><span class="sxs-lookup"><span data-stu-id="00a6a-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Nieuw, gegevens, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="00a6a-153">Zorg ervoor dat de database-server staat de toegang tot Azure-services:</span><span class="sxs-lookup"><span data-stu-id="00a6a-153">Make sure that the database server allows access to Azure services:</span></span>

![Bladeren, Servers, uw server, instellingen, Firewall, toegang tot Azure toestaan](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="00a6a-155">Een tabel maken in Azure SQL DB</span><span class="sxs-lookup"><span data-stu-id="00a6a-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="00a6a-156">Verbinding maken met de database gemaakt in de vorige sectie met het beheerprogramma van uw voorkeur.</span><span class="sxs-lookup"><span data-stu-id="00a6a-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="00a6a-157">In dit overzicht we gebruiken [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="00a6a-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="00a6a-158">Een nieuwe query maken en uitvoeren van de volgende T-SQL:</span><span class="sxs-lookup"><span data-stu-id="00a6a-158">Create a new query, and execute the following T-SQL:</span></span>

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

<span data-ttu-id="00a6a-159">In dit voorbeeld gebruiken we gegevens van paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="00a6a-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="00a6a-160">Overzicht van de gegevens beschikbaar Inspecteer de JSON-uitvoer en Zie de [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="00a6a-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="00a6a-161">Azure Stream Analytics-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="00a6a-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="00a6a-162">Van de [klassieke Azure Portal](https://manage.windowsazure.com/), selecteer de Azure Stream Analytics-service en een nieuwe Stream Analytics-taak maken:</span><span class="sxs-lookup"><span data-stu-id="00a6a-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="00a6a-163">Als de nieuwe taak is gemaakt, vouwt u de details ervan:</span><span class="sxs-lookup"><span data-stu-id="00a6a-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="00a6a-164">Locatie van de blob instellen</span><span class="sxs-lookup"><span data-stu-id="00a6a-164">Set blob location</span></span>
<span data-ttu-id="00a6a-165">Stel deze in op invoer van uw blob continue Export nemen:</span><span class="sxs-lookup"><span data-stu-id="00a6a-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="00a6a-166">Nu moet u de primaire toegangssleutel van uw Opslagaccount die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="00a6a-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="00a6a-167">Stel dit in als de sleutel van het Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="00a6a-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="00a6a-168">Set pad voorvoegselpatroon</span><span class="sxs-lookup"><span data-stu-id="00a6a-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="00a6a-169">Zorg ervoor dat de datumnotatie instellen op **jjjj-MM-DD** (met **streepjes**).</span><span class="sxs-lookup"><span data-stu-id="00a6a-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="00a6a-170">Het pad naar het voorvoegsel patroon geeft aan hoe de invoerbestanden in Stream Analytics worden gevonden in de opslag.</span><span class="sxs-lookup"><span data-stu-id="00a6a-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="00a6a-171">U moet worden ingesteld in overeenstemming met continue Export hoe de gegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="00a6a-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="00a6a-172">Stel deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="00a6a-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="00a6a-173">In dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="00a6a-173">In this example:</span></span>

* <span data-ttu-id="00a6a-174">`webapplication27`de naam van de Application Insights-resource **allemaal in kleine letters**.</span><span class="sxs-lookup"><span data-stu-id="00a6a-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="00a6a-175">`1234...`de instrumentatiesleutel van de Application Insights-resource is **met streepjes verwijderd**.</span><span class="sxs-lookup"><span data-stu-id="00a6a-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="00a6a-176">`PageViews`is het type gegevens wilt analyseren.</span><span class="sxs-lookup"><span data-stu-id="00a6a-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="00a6a-177">De beschikbare typen, is afhankelijk van het filter dat u in de continue Export instellen.</span><span class="sxs-lookup"><span data-stu-id="00a6a-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="00a6a-178">De geëxporteerde gegevens om de beschikbare typen Zie en bekijk de [exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="00a6a-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="00a6a-179">`/{date}/{time}`een patroon er wordt letterlijk geschreven.</span><span class="sxs-lookup"><span data-stu-id="00a6a-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="00a6a-180">Als u de naam en sleutel van uw Application Insights-resource, Essentials open op de overzichtspagina, of instellingen.</span><span class="sxs-lookup"><span data-stu-id="00a6a-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="00a6a-181">De eerste installatie voltooien</span><span class="sxs-lookup"><span data-stu-id="00a6a-181">Finish initial setup</span></span>
<span data-ttu-id="00a6a-182">Bevestig de serialisatie-indeling:</span><span class="sxs-lookup"><span data-stu-id="00a6a-182">Confirm the serialization format:</span></span>

![Bevestigen en de wizard te sluiten](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="00a6a-184">De wizard te sluiten en wacht totdat de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="00a6a-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="00a6a-185">De voorbeeld-functie gebruiken om te controleren of u het ingevoerde pad correct hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="00a6a-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="00a6a-186">Als dit mislukt: Controleer of er gegevens in de opslag voor de voorbeeld-periode die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="00a6a-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="00a6a-187">Bewerk de definitie van de invoer en controleer u de storage-account, het pad voorvoegsel ingesteld en datumnotatie correct.</span><span class="sxs-lookup"><span data-stu-id="00a6a-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="00a6a-188">Set-query</span><span class="sxs-lookup"><span data-stu-id="00a6a-188">Set query</span></span>
<span data-ttu-id="00a6a-189">Open de querysectie:</span><span class="sxs-lookup"><span data-stu-id="00a6a-189">Open the query section:</span></span>

![Selecteer in de stream analytics, Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="00a6a-191">Vervang de standaardquery met:</span><span class="sxs-lookup"><span data-stu-id="00a6a-191">Replace the default query with:</span></span>

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

<span data-ttu-id="00a6a-192">U ziet dat de eerste enkele eigenschappen specifiek voor paginaweergavegegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="00a6a-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="00a6a-193">Uitvoer van andere typen telemetrie heeft andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="00a6a-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="00a6a-194">Zie de [gedetailleerde gegevens modelverwijzing voor de eigenschaptypen en waarden.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="00a6a-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="00a6a-195">Instellen van uitvoer naar de database</span><span class="sxs-lookup"><span data-stu-id="00a6a-195">Set up output to database</span></span>
<span data-ttu-id="00a6a-196">Selecteer SQL als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="00a6a-196">Select SQL as the output.</span></span>

![Selecteer in de stream analytics, uitvoer](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="00a6a-198">Geef de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="00a6a-198">Specify the SQL database.</span></span>

![Vul de details van de database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="00a6a-200">De wizard te sluiten en wachten op een melding dat de uitvoer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="00a6a-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="00a6a-201">Verwerking starten</span><span class="sxs-lookup"><span data-stu-id="00a6a-201">Start processing</span></span>
<span data-ttu-id="00a6a-202">Start de taak van de actiebalk:</span><span class="sxs-lookup"><span data-stu-id="00a6a-202">Start the job from the action bar:</span></span>

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="00a6a-204">U kunt kiezen of verwerken van de gegevens vanaf nu of beginnen met oudere gegevens wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="00a6a-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="00a6a-205">De laatste is handig als u hebt continue Export is al een tijdje wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="00a6a-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![Klik op Start in de stream analytics,](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="00a6a-207">Ga terug naar SQL Server-beheerprogramma's na een paar minuten en bekijk de gegevens die.</span><span class="sxs-lookup"><span data-stu-id="00a6a-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="00a6a-208">Gebruik bijvoorbeeld een query als volgt:</span><span class="sxs-lookup"><span data-stu-id="00a6a-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="00a6a-209">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="00a6a-209">Related articles</span></span>
* [<span data-ttu-id="00a6a-210">Exporteren naar Power BI met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00a6a-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="00a6a-211">Gedetailleerde gegevens model verwijzing voor de eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="00a6a-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="00a6a-212">Continue Export in de Application Insights</span><span class="sxs-lookup"><span data-stu-id="00a6a-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="00a6a-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="00a6a-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

