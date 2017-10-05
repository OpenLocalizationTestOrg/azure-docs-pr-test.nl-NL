---
title: Uw gegevens importeren in analyses in Azure Application Insights | Microsoft Docs
description: Statische gegevens samen te voegen met de app telemetrie importeren of een afzonderlijke gegevensstroom query met Analytics importeren.
services: application-insights
keywords: Open-schema, gegevens importeren
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="3e887-104">Gegevens importeren in Analytics</span><span class="sxs-lookup"><span data-stu-id="3e887-104">Import data into Analytics</span></span>

<span data-ttu-id="3e887-105">Importeer tabellaire gegevens in [Analytics](app-insights-analytics.md)om toe te voegen met een [Application Insights](app-insights-overview.md) telemetrie van uw app of dat u deze als een afzonderlijke stream kunt analyseren.</span><span class="sxs-lookup"><span data-stu-id="3e887-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="3e887-106">Analytics is een krachtige querytaal die geschikt is voor het analyseren van grote hoeveelheden voorzien van een tijdstempel streams telemetrie.</span><span class="sxs-lookup"><span data-stu-id="3e887-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="3e887-107">U kunt gegevens importeren in Analytics met uw eigen schema.</span><span class="sxs-lookup"><span data-stu-id="3e887-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="3e887-108">Heeft geen gebruik van de standaard Application Insights-schema's zoals aanvraag of trace.</span><span class="sxs-lookup"><span data-stu-id="3e887-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="3e887-109">U kunt importeren JSON of DSV (scheidingsteken gescheiden waarden - komma, puntkomma of tab) bestanden.</span><span class="sxs-lookup"><span data-stu-id="3e887-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="3e887-110">Er zijn drie situaties waarin u importeert in Analytics handig is:</span><span class="sxs-lookup"><span data-stu-id="3e887-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="3e887-111">**Voeg met app telemetrie.**</span><span class="sxs-lookup"><span data-stu-id="3e887-111">**Join with app telemetry.**</span></span> <span data-ttu-id="3e887-112">U kunt bijvoorbeeld een tabel met URL's van uw website wordt toegewezen aan beter leesbaar pagina's importeren.</span><span class="sxs-lookup"><span data-stu-id="3e887-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="3e887-113">In Analytics, kunt u een dashboard grafiekrapport de tien meest populaire pagina's in uw website.</span><span class="sxs-lookup"><span data-stu-id="3e887-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="3e887-114">Nu kunt deze pagina's in plaats van de URL's weergeven.</span><span class="sxs-lookup"><span data-stu-id="3e887-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="3e887-115">**Telemetrie van uw toepassing correleren** met andere bronnen zoals netwerkverkeer, server-gegevens of CDN logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="3e887-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="3e887-116">**Analyse van toepassing op een afzonderlijke gegevensstroom.**</span><span class="sxs-lookup"><span data-stu-id="3e887-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="3e887-117">Application Insights Analytics is een krachtig hulpprogramma dat goed samen met sparse, voorzien van een tijdstempel streams - veel beter dan SQL in veel gevallen werkt.</span><span class="sxs-lookup"><span data-stu-id="3e887-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="3e887-118">Als u een dergelijke stroom van een andere bron hebt, kunt u deze kunt analyseren met Analytics.</span><span class="sxs-lookup"><span data-stu-id="3e887-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="3e887-119">Verzenden van gegevens naar de gegevensbron is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="3e887-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="3e887-120">(Eenmaal) Definieer de planning van uw gegevens in een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3e887-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="3e887-121">(Periodiek) Uw gegevens uploaden naar Azure storage en de REST-API om contact met ons opnemen die nieuwe gegevens opname wacht aanroepen.</span><span class="sxs-lookup"><span data-stu-id="3e887-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="3e887-122">De gegevens zijn beschikbaar voor de query in Analytics binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3e887-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="3e887-123">De frequentie van het uploaden wordt gedefinieerd door u en hoe snel wilt u uw gegevens beschikbaar voor query's.</span><span class="sxs-lookup"><span data-stu-id="3e887-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="3e887-124">Het is efficiënter uploaden van gegevens in grotere segmenten, maar niet groter zijn dan 1GB.</span><span class="sxs-lookup"><span data-stu-id="3e887-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="3e887-125">*Hebt u veel gegevensbronnen analyseren?*</span><span class="sxs-lookup"><span data-stu-id="3e887-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="3e887-126">*Overweeg het gebruik van* logstash *voor het verzenden van uw gegevens naar Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="3e887-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="3e887-127">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3e887-127">Before you start</span></span>

<span data-ttu-id="3e887-128">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="3e887-128">You need:</span></span>

1. <span data-ttu-id="3e887-129">Een Application Insights-resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e887-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="3e887-130">Als u wilt analyseren van uw gegevens afzonderlijk van andere telemetrie [Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3e887-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="3e887-131">Als u lid worden van of uw gegevens met de telemetrie van een app die al is ingesteld met Application Insights vergelijken, kunt u de bron voor die app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e887-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="3e887-132">Inzender of eigenaar toegang tot deze resource.</span><span class="sxs-lookup"><span data-stu-id="3e887-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="3e887-133">Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="3e887-133">Azure storage.</span></span> <span data-ttu-id="3e887-134">U kunt uploaden naar Azure storage en Analytics uw gegevens ontvangt van daaruit.</span><span class="sxs-lookup"><span data-stu-id="3e887-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="3e887-135">U wordt aangeraden dat u een speciale storage-account maken voor uw blobs.</span><span class="sxs-lookup"><span data-stu-id="3e887-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="3e887-136">Als uw blobs worden gedeeld met andere processen, duurt het langer voor onze processen uw blobs te lezen.</span><span class="sxs-lookup"><span data-stu-id="3e887-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="3e887-137">Uw schema definiëren</span><span class="sxs-lookup"><span data-stu-id="3e887-137">Define your schema</span></span>

<span data-ttu-id="3e887-138">Voordat u gegevens importeren kunt, moet u een *gegevensbron* waarmee het schema van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="3e887-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="3e887-139">U kunt maximaal 50 gegevensbronnen in een enkele Application Insights-bron hebben</span><span class="sxs-lookup"><span data-stu-id="3e887-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="3e887-140">Start de wizard gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3e887-140">Start the data source wizard.</span></span> <span data-ttu-id="3e887-141">Gebruik de knop 'Een nieuwe gegevensbron toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="3e887-141">Use "Add new data source" button.</span></span> <span data-ttu-id="3e887-142">U kunt ook - klikt u op de knop instellingen in rechts bovenhoek en kies 'Gegevensbronnen' in het vervolgkeuzemenu.</span><span class="sxs-lookup"><span data-stu-id="3e887-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="3e887-144">Geef een naam voor de nieuwe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3e887-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="3e887-145">Definieer de indeling van de bestanden die u zult uploaden.</span><span class="sxs-lookup"><span data-stu-id="3e887-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="3e887-146">U kunt de indeling handmatig definiëren of u een voorbeeld-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="3e887-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="3e887-147">Als de gegevens zich in de CSV-indeling, zijn de eerste rij van de voorbeeld-kolomkoppen.</span><span class="sxs-lookup"><span data-stu-id="3e887-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="3e887-148">U kunt de veldnamen in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3e887-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="3e887-149">Het voorbeeld moet ten minste 10 rijen of records van de gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="3e887-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="3e887-150">Kolom- of veldnamen moeten alfanumeriek namen (zonder spaties of leestekens) hebben.</span><span class="sxs-lookup"><span data-stu-id="3e887-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Een voorbeeld-bestand uploaden](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="3e887-152">Controleer het schema die is verkregen met de wizard.</span><span class="sxs-lookup"><span data-stu-id="3e887-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="3e887-153">Als deze de typen van een voorbeeld van een afgeleid, moet u mogelijk de afgeleide typen van de kolommen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3e887-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Bekijk de afgeleid schema](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="3e887-155">(Optioneel.) Upload een schemadefinitie.</span><span class="sxs-lookup"><span data-stu-id="3e887-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="3e887-156">Zie de onderstaande notatie.</span><span class="sxs-lookup"><span data-stu-id="3e887-156">See the format below.</span></span>

 * <span data-ttu-id="3e887-157">Selecteer een tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="3e887-157">Select a Timestamp.</span></span> <span data-ttu-id="3e887-158">Alle gegevens in Analytics moet beschikken over een tijdstempelveld.</span><span class="sxs-lookup"><span data-stu-id="3e887-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="3e887-159">Type moet hebben `datetime`, maar heeft geen naam 'tijdstempel'.</span><span class="sxs-lookup"><span data-stu-id="3e887-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="3e887-160">Als uw gegevens een kolom met een datum en tijd in de ISO-indeling heeft, kies deze optie als de timestamp-kolom.</span><span class="sxs-lookup"><span data-stu-id="3e887-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="3e887-161">Kies anders 'als gegevens ontvangen' en het importproces een timestamp-veld wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3e887-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="3e887-162">De gegevensbron maken.</span><span class="sxs-lookup"><span data-stu-id="3e887-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="3e887-163">Bestandsindeling van pakketdefinities schema</span><span class="sxs-lookup"><span data-stu-id="3e887-163">Schema definition file format</span></span>

<span data-ttu-id="3e887-164">In plaats van het schema in de gebruikersinterface bewerkt, kunt u de schemadefinitie laden uit een bestand.</span><span class="sxs-lookup"><span data-stu-id="3e887-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="3e887-165">De indeling van de definitie schema is als volgt:</span><span class="sxs-lookup"><span data-stu-id="3e887-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="3e887-166">Gescheiden indeling</span><span class="sxs-lookup"><span data-stu-id="3e887-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="3e887-167">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="3e887-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="3e887-168">Elke kolom wordt geïdentificeerd door de locatie, de naam en het type.</span><span class="sxs-lookup"><span data-stu-id="3e887-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="3e887-169">Locatie – is voor het bestand met scheidingstekens hiervan de positie van de toegewezen waarde.</span><span class="sxs-lookup"><span data-stu-id="3e887-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="3e887-170">Voor JSON-indeling is de jpath van de toegewezen sleutel.</span><span class="sxs-lookup"><span data-stu-id="3e887-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="3e887-171">Naam: de naam van de kolom die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3e887-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="3e887-172">Type: het gegevenstype van die kolom.</span><span class="sxs-lookup"><span data-stu-id="3e887-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="3e887-173">Als een voorbeeldgegevens gebruikt en bestandsindeling worden gescheiden, moet de schemadefinitie alle kolommen toewijzen en nieuwe kolommen toevoegen aan het einde.</span><span class="sxs-lookup"><span data-stu-id="3e887-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="3e887-174">JSON staat gedeeltelijke toewijzing van de gegevens, dus de schemadefinitie van JSON-indeling heeft geen elke sleutel die is gevonden in een voorbeeldgegevens toewijzen.</span><span class="sxs-lookup"><span data-stu-id="3e887-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="3e887-175">Deze kolommen die geen deel uitmaken van de voorbeeldgegevens kan ook worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3e887-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="3e887-176">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="3e887-176">Import data</span></span>

<span data-ttu-id="3e887-177">Om gegevens te importeren, uploaden naar Azure storage, een toegangssleutel voor het maken en breng een REST-API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="3e887-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="3e887-179">U kunt het volgende proces handmatig uitvoeren of een geautomatiseerde systeem instellen om dat te doen met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="3e887-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="3e887-180">U moet als volgt te werk voor elk blok van gegevens die u wilt importeren.</span><span class="sxs-lookup"><span data-stu-id="3e887-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="3e887-181">De gegevens te uploaden [Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3e887-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="3e887-182">BLOBs kunnen worden elke maximaal 1GB ongecomprimeerde omvang.</span><span class="sxs-lookup"><span data-stu-id="3e887-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="3e887-183">Grote blobs honderden MB zijn ideaal vanuit het oogpunt van prestaties van.</span><span class="sxs-lookup"><span data-stu-id="3e887-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="3e887-184">U kunt het comprimeren met Gzip uploadtijd en de latentie voor de gegevens beschikbaar zijn voor de query te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="3e887-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="3e887-185">Gebruik de `.gz` bestandsnaamextensie.</span><span class="sxs-lookup"><span data-stu-id="3e887-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="3e887-186">Het is raadzaam een afzonderlijke opslagaccount voor dit doel gebruiken om te voorkomen dat verzoeken van andere services prestaties te vertragen.</span><span class="sxs-lookup"><span data-stu-id="3e887-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="3e887-187">Tijdens het verzenden van gegevens met hoge frequentie, om de paar seconden het verdient aanbeveling gebruik van meer dan één opslagaccount, voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="3e887-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="3e887-188">[Maak een Shared Access Signature-sleutel voor de blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="3e887-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="3e887-189">De sleutel moet een vervalperiode van één dag hebben en leestoegang te bieden.</span><span class="sxs-lookup"><span data-stu-id="3e887-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="3e887-190">Een REST-aanroep op de hoogte van Application Insights die wacht op de gegevens wilt maken.</span><span class="sxs-lookup"><span data-stu-id="3e887-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="3e887-191">Eindpunt:`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="3e887-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="3e887-192">HTTP-methode: POST</span><span class="sxs-lookup"><span data-stu-id="3e887-192">HTTP method: POST</span></span>
 * <span data-ttu-id="3e887-193">De nettolading van:</span><span class="sxs-lookup"><span data-stu-id="3e887-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="3e887-194">De tijdelijke aanduidingen zijn:</span><span class="sxs-lookup"><span data-stu-id="3e887-194">The placeholders are:</span></span>

* <span data-ttu-id="3e887-195">`Blob URI with Shared Access Key`: U krijgt deze van de procedure voor het maken van een sleutel.</span><span class="sxs-lookup"><span data-stu-id="3e887-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="3e887-196">Het is specifiek voor de blob.</span><span class="sxs-lookup"><span data-stu-id="3e887-196">It is specific to the blob.</span></span>
* <span data-ttu-id="3e887-197">`Schema ID`: De schema-ID gegenereerd voor uw gedefinieerd schema.</span><span class="sxs-lookup"><span data-stu-id="3e887-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="3e887-198">De gegevens in deze blob moeten voldoen aan het schema.</span><span class="sxs-lookup"><span data-stu-id="3e887-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="3e887-199">`DateTime`: De UTC-tijd waarop de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="3e887-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="3e887-200">We accepteren van deze indelingen: ISO8601 (zoals ' 01-01-2016 13:45:01 '); RFC822 (' Wed, 14 december 16 14:57:01 + 0000 '); RFC850 ("woensdag, 14-december-16 14:57:00 UTC"); RFC1123 (' Wed 14 december 2016 14:57:00 + 0000 ').</span><span class="sxs-lookup"><span data-stu-id="3e887-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="3e887-201">`Instrumentation key`van uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="3e887-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="3e887-202">De gegevens zijn beschikbaar in Analytics na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3e887-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="3e887-203">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="3e887-203">Error responses</span></span>

* <span data-ttu-id="3e887-204">**400 onjuiste aanvraag**: geeft aan dat de nettolading van de aanvraag ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="3e887-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="3e887-205">Controleren:</span><span class="sxs-lookup"><span data-stu-id="3e887-205">Check:</span></span>
 * <span data-ttu-id="3e887-206">Juiste instrumentatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="3e887-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="3e887-207">Geldige tijd-waarde.</span><span class="sxs-lookup"><span data-stu-id="3e887-207">Valid time value.</span></span> <span data-ttu-id="3e887-208">Deze moet de tijd nu in UTC.</span><span class="sxs-lookup"><span data-stu-id="3e887-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="3e887-209">De JSON van de gebeurtenis voldoet aan het schema.</span><span class="sxs-lookup"><span data-stu-id="3e887-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="3e887-210">**403-verboden**: de blob die u hebt verzonden, is niet toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="3e887-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="3e887-211">Zorg ervoor dat de gedeelde toegangssleutel geldig is en niet is verlopen.</span><span class="sxs-lookup"><span data-stu-id="3e887-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="3e887-212">**404 niet gevonden**:</span><span class="sxs-lookup"><span data-stu-id="3e887-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="3e887-213">De blob bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="3e887-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="3e887-214">De bron-id is onjuist.</span><span class="sxs-lookup"><span data-stu-id="3e887-214">The sourceId is wrong.</span></span>

<span data-ttu-id="3e887-215">Meer gedetailleerde informatie is beschikbaar in het antwoordbericht van de fout.</span><span class="sxs-lookup"><span data-stu-id="3e887-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="3e887-216">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="3e887-216">Sample code</span></span>

<span data-ttu-id="3e887-217">Deze code gebruikt de [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="3e887-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="3e887-218">Klassen</span><span class="sxs-lookup"><span data-stu-id="3e887-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="3e887-219">Gegevens opnemen</span><span class="sxs-lookup"><span data-stu-id="3e887-219">Ingest data</span></span>

<span data-ttu-id="3e887-220">Deze code gebruiken voor elke blob.</span><span class="sxs-lookup"><span data-stu-id="3e887-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="3e887-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e887-221">Next steps</span></span>

* [<span data-ttu-id="3e887-222">Rondleiding van de querytaal Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3e887-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="3e887-223">Gebruik *Logstash* om gegevens te verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="3e887-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
