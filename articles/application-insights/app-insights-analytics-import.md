---
title: aaaImport uw tooAnalytics gegevens in Azure Application Insights | Microsoft Docs
description: Statische gegevens toojoin met app telemetrie importeren, of een afzonderlijke gegevensstroom tooquery met Analytics importeren.
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="c3981-104">Gegevens importeren in Analytics</span><span class="sxs-lookup"><span data-stu-id="c3981-104">Import data into Analytics</span></span>

<span data-ttu-id="c3981-105">Importeer tabellaire gegevens in [Analytics](app-insights-analytics.md), ofwel toojoin met [Application Insights](app-insights-overview.md) telemetrie van uw app, of dat u deze als een afzonderlijke stream kunt analyseren.</span><span class="sxs-lookup"><span data-stu-id="c3981-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="c3981-106">Analytics is een krachtige query language geschikt tooanalyzing hoog volume voorzien van een tijdstempel streams telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c3981-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="c3981-107">U kunt gegevens importeren in Analytics met uw eigen schema.</span><span class="sxs-lookup"><span data-stu-id="c3981-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="c3981-108">Heeft geen toouse Hallo standaard Application Insights-schema's zoals aanvraag of trace.</span><span class="sxs-lookup"><span data-stu-id="c3981-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="c3981-109">U kunt importeren JSON of DSV (scheidingsteken gescheiden waarden - komma, puntkomma of tab) bestanden.</span><span class="sxs-lookup"><span data-stu-id="c3981-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="c3981-110">Er zijn drie situaties waarin tooAnalytics importeren handig is:</span><span class="sxs-lookup"><span data-stu-id="c3981-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="c3981-111">**Voeg met app telemetrie.**</span><span class="sxs-lookup"><span data-stu-id="c3981-111">**Join with app telemetry.**</span></span> <span data-ttu-id="c3981-112">U kunt bijvoorbeeld een tabel die is toegewezen URL's van uw website toomore gelezen pagina's importeren.</span><span class="sxs-lookup"><span data-stu-id="c3981-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="c3981-113">In Analytics, kunt u een dashboard grafiekrapport Hallo tien meest populaire pagina's in uw website.</span><span class="sxs-lookup"><span data-stu-id="c3981-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="c3981-114">Nu kan worden weergegeven waarop Hallo pagina's in plaats van Hallo URL's.</span><span class="sxs-lookup"><span data-stu-id="c3981-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="c3981-115">**Telemetrie van uw toepassing correleren** met andere bronnen zoals netwerkverkeer, server-gegevens of CDN logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="c3981-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="c3981-116">**Toepassing Analytics tooa afzonderlijke gegevensstroom.**</span><span class="sxs-lookup"><span data-stu-id="c3981-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="c3981-117">Application Insights Analytics is een krachtig hulpprogramma dat goed samen met sparse, voorzien van een tijdstempel streams - veel beter dan SQL in veel gevallen werkt.</span><span class="sxs-lookup"><span data-stu-id="c3981-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="c3981-118">Als u een dergelijke stroom van een andere bron hebt, kunt u deze kunt analyseren met Analytics.</span><span class="sxs-lookup"><span data-stu-id="c3981-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="c3981-119">Verzenden de tooyour-gegevensbron is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="c3981-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="c3981-120">(Eenmaal) Hallo-schema van uw gegevens in een gegevensbron definiëren.</span><span class="sxs-lookup"><span data-stu-id="c3981-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="c3981-121">(Periodiek) Uploaden van uw gegevens tooAzure opslag en Hallo REST-API toonotify ons die nieuwe gegevens opname wacht te bellen.</span><span class="sxs-lookup"><span data-stu-id="c3981-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="c3981-122">Binnen een paar minuten is Hallo gegevens beschikbaar voor query's in Analytics.</span><span class="sxs-lookup"><span data-stu-id="c3981-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="c3981-123">Hello frequentie van Hallo uploaden is door u gedefinieerde en hoe snel wilt u uw gegevens toobe beschikbaar voor query's.</span><span class="sxs-lookup"><span data-stu-id="c3981-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="c3981-124">Het is efficiënter tooupload gegevens in grotere segmenten, maar niet groter zijn dan 1GB.</span><span class="sxs-lookup"><span data-stu-id="c3981-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="c3981-125">*Hebt u veel gegevensbronnen tooanalyze?*</span><span class="sxs-lookup"><span data-stu-id="c3981-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="c3981-126">*Overweeg het gebruik van* logstash *tooship uw gegevens in Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="c3981-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="c3981-127">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c3981-127">Before you start</span></span>

<span data-ttu-id="c3981-128">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="c3981-128">You need:</span></span>

1. <span data-ttu-id="c3981-129">Een Application Insights-resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c3981-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="c3981-130">Als u uw gegevens afzonderlijk van andere telemetrie tooanalyze wilt [Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c3981-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="c3981-131">Als u lid worden van of uw gegevens met de telemetrie van een app die al is ingesteld met Application Insights vergelijken, kunt u Hallo resource voor die app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c3981-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="c3981-132">Inzender of eigenaar toegang toothat resource.</span><span class="sxs-lookup"><span data-stu-id="c3981-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="c3981-133">Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="c3981-133">Azure storage.</span></span> <span data-ttu-id="c3981-134">Uploaden van tooAzure opslag en Analytics uw gegevens ontvangt van daaruit.</span><span class="sxs-lookup"><span data-stu-id="c3981-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="c3981-135">U wordt aangeraden dat u een speciale storage-account maken voor uw blobs.</span><span class="sxs-lookup"><span data-stu-id="c3981-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="c3981-136">Als uw blobs worden gedeeld met andere processen, duurt het langer voor onze tooread processen uw blobs.</span><span class="sxs-lookup"><span data-stu-id="c3981-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="c3981-137">Uw schema definiëren</span><span class="sxs-lookup"><span data-stu-id="c3981-137">Define your schema</span></span>

<span data-ttu-id="c3981-138">Voordat u gegevens importeren kunt, moet u een *gegevensbron* waarmee Hallo-schema van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="c3981-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="c3981-139">U kunt hebben van de gegevensbronnen too50 in één Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="c3981-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="c3981-140">Start de wizard Gegevensbron Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3981-140">Start hello data source wizard.</span></span> <span data-ttu-id="c3981-141">Gebruik de knop 'Een nieuwe gegevensbron toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="c3981-141">Use "Add new data source" button.</span></span> <span data-ttu-id="c3981-142">U kunt ook - klikt u op de knop instellingen in rechts bovenhoek en kies 'Gegevensbronnen' in het vervolgkeuzemenu.</span><span class="sxs-lookup"><span data-stu-id="c3981-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="c3981-144">Geef een naam voor de nieuwe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="c3981-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="c3981-145">Definieer de indeling van Hallo-bestanden die u zult uploaden.</span><span class="sxs-lookup"><span data-stu-id="c3981-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="c3981-146">U kunt Hallo indeling handmatig opgeven of u een voorbeeldbestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="c3981-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="c3981-147">Als Hallo gegevens zich in de CSV-indeling, zijn de eerste rij Hallo van Hallo voorbeeld kolomkoppen.</span><span class="sxs-lookup"><span data-stu-id="c3981-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="c3981-148">Hallo-veldnamen in de volgende stap hello, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3981-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="c3981-149">Hallo-voorbeeld moet ten minste 10 rijen of records van de gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="c3981-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="c3981-150">Kolom- of veldnamen moeten alfanumeriek namen (zonder spaties of leestekens) hebben.</span><span class="sxs-lookup"><span data-stu-id="c3981-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Een voorbeeld-bestand uploaden](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="c3981-152">Bekijk Hallo schema dat wizard Hallo heeft is.</span><span class="sxs-lookup"><span data-stu-id="c3981-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="c3981-153">Als het Hallo-typen uit een voorbeeld van een afgeleid, moet u mogelijk tooadjust Hallo afgeleid typen Hallo kolommen.</span><span class="sxs-lookup"><span data-stu-id="c3981-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Bekijk Hallo afgeleid schema](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="c3981-155">(Optioneel.) Upload een schemadefinitie.</span><span class="sxs-lookup"><span data-stu-id="c3981-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="c3981-156">Zie de onderstaande Hallo-notatie.</span><span class="sxs-lookup"><span data-stu-id="c3981-156">See hello format below.</span></span>

 * <span data-ttu-id="c3981-157">Selecteer een tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="c3981-157">Select a Timestamp.</span></span> <span data-ttu-id="c3981-158">Alle gegevens in Analytics moet beschikken over een tijdstempelveld.</span><span class="sxs-lookup"><span data-stu-id="c3981-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="c3981-159">Type moet hebben `datetime`, maar heeft geen toobe met de naam 'tijdstempel'.</span><span class="sxs-lookup"><span data-stu-id="c3981-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="c3981-160">Als uw gegevens een kolom met een datum en tijd in de ISO-indeling heeft, kies deze optie als Hallo timestamp-kolom.</span><span class="sxs-lookup"><span data-stu-id="c3981-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="c3981-161">Kies anders 'als gegevens ontvangen' en Hallo importproces een timestamp-veld wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c3981-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="c3981-162">Hallo-gegevensbron maken.</span><span class="sxs-lookup"><span data-stu-id="c3981-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="c3981-163">Bestandsindeling van pakketdefinities schema</span><span class="sxs-lookup"><span data-stu-id="c3981-163">Schema definition file format</span></span>

<span data-ttu-id="c3981-164">In plaats van het Hallo-schema in de gebruikersinterface bewerkt, kunt u de schemadefinitie Hallo laden uit een bestand.</span><span class="sxs-lookup"><span data-stu-id="c3981-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="c3981-165">Hallo schema definitie-indeling is als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3981-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="c3981-166">Gescheiden indeling</span><span class="sxs-lookup"><span data-stu-id="c3981-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="c3981-167">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="c3981-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="c3981-168">Elke kolom wordt geïdentificeerd door Hallo locatie, naam en type.</span><span class="sxs-lookup"><span data-stu-id="c3981-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="c3981-169">Locatie – is voor het bestand met scheidingstekens formatteert u het Hallo-positie van Hallo toegewezen waarde.</span><span class="sxs-lookup"><span data-stu-id="c3981-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="c3981-170">Voor JSON-indeling is het Hallo jpath van Hallo toegewezen sleutel.</span><span class="sxs-lookup"><span data-stu-id="c3981-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="c3981-171">Naam: Hallo weergegeven naam van Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="c3981-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="c3981-172">Type: Hallo-gegevenstype van die kolom.</span><span class="sxs-lookup"><span data-stu-id="c3981-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="c3981-173">Als een voorbeeldgegevens gebruikt en bestandsindeling worden gescheiden, moet Hallo schemadefinitie alle kolommen toewijzen en nieuwe kolommen toevoegen aan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="c3981-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="c3981-174">JSON staat gedeeltelijke Hallo gegevens worden toegewezen, daarom hello schemadefinitie van JSON-indeling heeft geen toomap elke sleutel die is gevonden in een voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="c3981-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="c3981-175">Deze kunt kolommen die geen deel uitmaken van de voorbeeldgegevens Hallo ook toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c3981-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="c3981-176">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="c3981-176">Import data</span></span>

<span data-ttu-id="c3981-177">tooimport gegevens, tooAzure opslag te uploaden, een toegangssleutel voor het maken en breng vervolgens een REST-API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="c3981-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Nieuwe gegevensbron toevoegen](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="c3981-179">U kunt Hallo na handmatig uitvoeren of instellen van een toodo automatisch deze met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="c3981-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="c3981-180">U moet toofollow deze stappen voor elk gegevensblok tooimport gewenste.</span><span class="sxs-lookup"><span data-stu-id="c3981-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="c3981-181">Hallo-gegevens te uploaden[Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c3981-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="c3981-182">BLOBs kunnen elke grootte van niet-gecomprimeerd too1GB zijn.</span><span class="sxs-lookup"><span data-stu-id="c3981-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="c3981-183">Grote blobs honderden MB zijn ideaal vanuit het oogpunt van prestaties van.</span><span class="sxs-lookup"><span data-stu-id="c3981-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="c3981-184">U kunt het comprimeren met Gzip tooimprove uploadtijd en de latentie voor Hallo gegevens toobe beschikbaar voor query.</span><span class="sxs-lookup"><span data-stu-id="c3981-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="c3981-185">Gebruik Hallo `.gz` bestandsnaamextensie.</span><span class="sxs-lookup"><span data-stu-id="c3981-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="c3981-186">Is het beste toouse een afzonderlijke opslagaccount voor dit doel, tooavoid aanroepen vanuit verschillende services prestaties te vertragen.</span><span class="sxs-lookup"><span data-stu-id="c3981-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="c3981-187">Tijdens het verzenden van gegevens met hoge frequentie, om de paar seconden verdient toouse meer dan één opslagaccount opgeven voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="c3981-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="c3981-188">[Maak een Shared Access Signature-sleutel voor Hallo blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="c3981-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="c3981-189">Hallo-sleutel moet een vervalperiode van één dag hebben en geef leestoegang.</span><span class="sxs-lookup"><span data-stu-id="c3981-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="c3981-190">Controleer een REST-aanroep toonotify Application Insights dat gegevens wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="c3981-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="c3981-191">Eindpunt:`https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="c3981-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="c3981-192">HTTP-methode: POST</span><span class="sxs-lookup"><span data-stu-id="c3981-192">HTTP method: POST</span></span>
 * <span data-ttu-id="c3981-193">De nettolading van:</span><span class="sxs-lookup"><span data-stu-id="c3981-193">Payload:</span></span>

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

<span data-ttu-id="c3981-194">Hallo tijdelijke aanduidingen zijn:</span><span class="sxs-lookup"><span data-stu-id="c3981-194">hello placeholders are:</span></span>

* <span data-ttu-id="c3981-195">`Blob URI with Shared Access Key`: U krijgt deze van Hallo procedure voor het maken van een sleutel.</span><span class="sxs-lookup"><span data-stu-id="c3981-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="c3981-196">Het is specifieke toohello blob.</span><span class="sxs-lookup"><span data-stu-id="c3981-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="c3981-197">`Schema ID`: Hallo schema-ID gegenereerd voor uw gedefinieerd schema.</span><span class="sxs-lookup"><span data-stu-id="c3981-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="c3981-198">Hallo-gegevens in deze blob moet toohello schema voldoen.</span><span class="sxs-lookup"><span data-stu-id="c3981-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="c3981-199">`DateTime`: Hallo UTC-tijd van aanvraag is verzonden op welke hello,.</span><span class="sxs-lookup"><span data-stu-id="c3981-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="c3981-200">We accepteren van deze indelingen: ISO8601 (zoals ' 01-01-2016 13:45:01 '); RFC822 (' Wed, 14 december 16 14:57:01 + 0000 '); RFC850 ("woensdag, 14-december-16 14:57:00 UTC"); RFC1123 (' Wed 14 december 2016 14:57:00 + 0000 ').</span><span class="sxs-lookup"><span data-stu-id="c3981-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="c3981-201">`Instrumentation key`van uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="c3981-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="c3981-202">Hallo-gegevens zijn beschikbaar in Analytics na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="c3981-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="c3981-203">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="c3981-203">Error responses</span></span>

* <span data-ttu-id="c3981-204">**400 onjuiste aanvraag**: geeft aan dat verzoek Hallo nettolading is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="c3981-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="c3981-205">Controleren:</span><span class="sxs-lookup"><span data-stu-id="c3981-205">Check:</span></span>
 * <span data-ttu-id="c3981-206">Juiste instrumentatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="c3981-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="c3981-207">Geldige tijd-waarde.</span><span class="sxs-lookup"><span data-stu-id="c3981-207">Valid time value.</span></span> <span data-ttu-id="c3981-208">Hallo UTC-tijd nu moeten worden.</span><span class="sxs-lookup"><span data-stu-id="c3981-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="c3981-209">De JSON van de gebeurtenis Hallo voldoet toohello schema.</span><span class="sxs-lookup"><span data-stu-id="c3981-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="c3981-210">**403-verboden**: Hallo blob die u hebt verzonden, is niet toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="c3981-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="c3981-211">Zorg ervoor dat Hallo gedeelde toegangssleutel is geldig en niet is verlopen.</span><span class="sxs-lookup"><span data-stu-id="c3981-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="c3981-212">**404 niet gevonden**:</span><span class="sxs-lookup"><span data-stu-id="c3981-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="c3981-213">Hallo blob bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="c3981-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="c3981-214">Hallo sourceId is onjuist.</span><span class="sxs-lookup"><span data-stu-id="c3981-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="c3981-215">Meer gedetailleerde informatie is beschikbaar in het foutbericht Hallo-antwoord.</span><span class="sxs-lookup"><span data-stu-id="c3981-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="c3981-216">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="c3981-216">Sample code</span></span>

<span data-ttu-id="c3981-217">Deze code gebruikt Hallo [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="c3981-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="c3981-218">Klassen</span><span class="sxs-lookup"><span data-stu-id="c3981-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="c3981-219">Gegevens opnemen</span><span class="sxs-lookup"><span data-stu-id="c3981-219">Ingest data</span></span>

<span data-ttu-id="c3981-220">Deze code gebruiken voor elke blob.</span><span class="sxs-lookup"><span data-stu-id="c3981-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="c3981-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3981-221">Next steps</span></span>

* [<span data-ttu-id="c3981-222">Rondleiding Hallo querytaal Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c3981-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="c3981-223">Gebruik *Logstash* toosend gegevens tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="c3981-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
