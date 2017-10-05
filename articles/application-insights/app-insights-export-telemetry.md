---
title: Continue export van telemetrie in Application Insights | Microsoft Docs
description: Diagnostische gegevens en gebruiksgegevens exporteren naar opslag in Microsoft Azure en download deze vanaf daar.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="c46fc-103">Exporteren van telemetrie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="c46fc-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="c46fc-104">Wilt u uw telemetrie langer dan de standaard bewaarperiode houden?</span><span class="sxs-lookup"><span data-stu-id="c46fc-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="c46fc-105">Of op een speciale wijze worden verwerkt?</span><span class="sxs-lookup"><span data-stu-id="c46fc-105">Or process it in some specialized way?</span></span> <span data-ttu-id="c46fc-106">Continue Export is ideaal voor dit.</span><span class="sxs-lookup"><span data-stu-id="c46fc-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="c46fc-107">De gebeurtenissen die u in de Application Insights-portal ziet kunnen worden geëxporteerd naar JSON-indeling in Microsoft Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="c46fc-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="c46fc-108">Daar kunt u downloaden van uw gegevens en wat u code schrijven moet verwerken.</span><span class="sxs-lookup"><span data-stu-id="c46fc-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="c46fc-109">Met behulp van continue Export mogelijk extra kosten in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="c46fc-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="c46fc-110">Controleer uw [prijzen model](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c46fc-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="c46fc-111">Voordat u de continue export instelt, zijn er enkele alternatieven die kunt u overwegen:</span><span class="sxs-lookup"><span data-stu-id="c46fc-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="c46fc-112">De knop exporteren boven aan een blade metrische gegevens of zoeken kunt u transfer tabellen en grafieken met een Excel-werkblad.</span><span class="sxs-lookup"><span data-stu-id="c46fc-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="c46fc-113">[Analytics](app-insights-analytics.md) biedt een krachtige querytaal voor telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c46fc-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="c46fc-114">Het kan ook resultaten exporteren.</span><span class="sxs-lookup"><span data-stu-id="c46fc-114">It can also export results.</span></span>
* <span data-ttu-id="c46fc-115">Als u op zoek bent naar [Verken uw gegevens in Power BI](app-insights-export-power-bi.md), kunt u dat doen zonder gebruik van continue Export.</span><span class="sxs-lookup"><span data-stu-id="c46fc-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="c46fc-116">De [REST-API toegang tot de gegevens](https://dev.applicationinsights.io/) kunt u programmatisch toegang krijgen tot uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c46fc-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="c46fc-117">Nadat de continue Export uw gegevens worden gekopieerd naar opslag (waar het kunt blijven voor als u wilt), is het nog steeds beschikbaar in Application Insights voor de gebruikelijke [bewaarperiode](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="c46fc-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="c46fc-118"><a name="setup"></a>Maken van een continue Export</span><span class="sxs-lookup"><span data-stu-id="c46fc-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="c46fc-119">Open continue Export in de Application Insights-resource voor uw app en kies **toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="c46fc-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Schuif naar beneden en klik op de continue Export](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="c46fc-121">Kies de telemetrie-gegevenstypen die u wilt exporteren.</span><span class="sxs-lookup"><span data-stu-id="c46fc-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="c46fc-122">Maak of Selecteer een [Azure storage-account](../storage/common/storage-introduction.md) waar u de gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="c46fc-123">Standaard wordt de locatie voor de opslag worden ingesteld op dezelfde geografische regio als uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="c46fc-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="c46fc-124">Als u in een andere regio opslaat, u mogelijk ook wijzigingskosten overdracht.</span><span class="sxs-lookup"><span data-stu-id="c46fc-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Klik op toevoegen, exporteren bestemming Storage-account en maakt een nieuwe winkel of kies een bestaand archief](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="c46fc-126">Maak of Selecteer een container in de opslag:</span><span class="sxs-lookup"><span data-stu-id="c46fc-126">Create or select a container in the storage:</span></span>

    ![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="c46fc-128">Als u uw export hebt gemaakt, wordt er gestart gaan.</span><span class="sxs-lookup"><span data-stu-id="c46fc-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="c46fc-129">U alleen ophalen gegevens waarvoor binnenkomt nadat u de export hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c46fc-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="c46fc-130">Kan er een vertraging van ongeveer een uur voordat gegevens worden weergegeven in de opslag zijn.</span><span class="sxs-lookup"><span data-stu-id="c46fc-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="c46fc-131">Continue export bewerken</span><span class="sxs-lookup"><span data-stu-id="c46fc-131">To edit continuous export</span></span>

<span data-ttu-id="c46fc-132">Als u de gebeurtenistypen later wijzigen wilt, bewerkt u gewoon het exporteren:</span><span class="sxs-lookup"><span data-stu-id="c46fc-132">If you want to change the event types later, just edit the export:</span></span>

![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="c46fc-134">Continue export stoppen</span><span class="sxs-lookup"><span data-stu-id="c46fc-134">To stop continuous export</span></span>

<span data-ttu-id="c46fc-135">Als u wilt stoppen met het exporteren, klikt u op uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-135">To stop the export, click Disable.</span></span> <span data-ttu-id="c46fc-136">Als u opnieuw inschakelen op, kan de export wordt opnieuw opgestart met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="c46fc-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="c46fc-137">U kunt de gegevens die tijdens het exporteren is uitgeschakeld in de portal is aangekomen won't ophalen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="c46fc-138">Als u wilt de export permanent stoppen, moet u deze verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="c46fc-139">In dat geval verwijdert niet de gegevens van opslag.</span><span class="sxs-lookup"><span data-stu-id="c46fc-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="c46fc-140">Kan niet toevoegen of wijzigen van een exporteren?</span><span class="sxs-lookup"><span data-stu-id="c46fc-140">Can't add or change an export?</span></span>
* <span data-ttu-id="c46fc-141">Als u wilt toevoegen of wijzigen van de uitvoer, moet u de eigenaar, bijdrager of Application Insights Inzender toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="c46fc-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="c46fc-142">[Meer informatie over functies][roles].</span><span class="sxs-lookup"><span data-stu-id="c46fc-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="c46fc-143"><a name="analyze"></a>Welke gebeurtenissen krijgt u?</span><span class="sxs-lookup"><span data-stu-id="c46fc-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="c46fc-144">De geëxporteerde gegevens is de onbewerkte telemetrie die we van uw toepassing ontvangen, behalve dat we locatiegegevens op die we berekenen van de client-IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="c46fc-145">Gegevens die zijn genegeerd door [steekproeven](app-insights-sampling.md) is niet opgenomen in de geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="c46fc-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="c46fc-146">Andere berekende waarden zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="c46fc-147">Bijvoorbeeld: gemiddelde CPU-gebruik niet worden geëxporteerd, maar we Exporteer de onbewerkte telemetrie van waaruit het gemiddelde wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="c46fc-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="c46fc-148">De gegevens omvatten ook de resultaten van een [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c46fc-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="c46fc-149">**Een steekproef.**</span><span class="sxs-lookup"><span data-stu-id="c46fc-149">**Sampling.**</span></span> <span data-ttu-id="c46fc-150">Als uw toepassing grote hoeveelheden gegevens verzendt, wordt de functie steekproeven werkt en wordt alleen een fractie van de gegenereerde telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="c46fc-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="c46fc-151">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="c46fc-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="c46fc-152"><a name="get"></a>De gegevens controleren</span><span class="sxs-lookup"><span data-stu-id="c46fc-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="c46fc-153">U kunt de opslag rechtstreeks in de portal inspecteren.</span><span class="sxs-lookup"><span data-stu-id="c46fc-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="c46fc-154">Klik op **Bladeren**, selecteer uw storage-account en open vervolgens **Containers**.</span><span class="sxs-lookup"><span data-stu-id="c46fc-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="c46fc-155">Om te controleren op Azure-opslag in Visual Studio, open **weergave**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c46fc-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="c46fc-156">(Als u deze menuopdracht niet hebt, moet u de Azure SDK installeren: Open de **nieuw Project** dialoogvenster Vouw Visual C# / Cloud en kies **ophalen van Microsoft Azure SDK voor .NET**.)</span><span class="sxs-lookup"><span data-stu-id="c46fc-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="c46fc-157">Wanneer u uw bloblarchief opent, ziet u een container met een set van blob-bestanden.</span><span class="sxs-lookup"><span data-stu-id="c46fc-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="c46fc-158">De URI van elk bestand dat is afgeleid van de naam van uw Application Insights-resource, de instrumentatiesleutel, telemetrie-type/datum/tijd.</span><span class="sxs-lookup"><span data-stu-id="c46fc-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="c46fc-159">(De resourcenaam is alleen kleine letters en streepjes bevatten de instrumentatiesleutel wordt weggelaten.)</span><span class="sxs-lookup"><span data-stu-id="c46fc-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Inspecteer de blob-opslag met een geschikt hulpprogramma](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="c46fc-161">De datum en tijd UTC zijn en zijn wanneer de telemetrie is in de store - gedeponeerd niet de tijd die is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c46fc-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="c46fc-162">Dus als u code schrijven om te downloaden van de gegevens, kunt het verplaatsen lineair via de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c46fc-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="c46fc-163">Hier volgt de vorm van het pad:</span><span class="sxs-lookup"><span data-stu-id="c46fc-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="c46fc-164">waar</span><span class="sxs-lookup"><span data-stu-id="c46fc-164">Where</span></span>

* <span data-ttu-id="c46fc-165">`blobCreationTimeUtc`tijdstip waarop de blob is gemaakt in het interne is staging-opslag</span><span class="sxs-lookup"><span data-stu-id="c46fc-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="c46fc-166">`blobDeliveryTimeUtc`is de tijd wanneer de blob wordt gekopieerd naar het doelopslagaccount exporteren</span><span class="sxs-lookup"><span data-stu-id="c46fc-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="c46fc-167"><a name="format"></a>Indeling van gegevens</span><span class="sxs-lookup"><span data-stu-id="c46fc-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="c46fc-168">Elke blob is een tekstbestand dat meerdere bevat ' \n'-separated rijen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="c46fc-169">Het bevat de telemetrie die gedurende een periode van ongeveer een halve minuut is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c46fc-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="c46fc-170">Elke rij vertegenwoordigt een gegevenspunt telemetrie zoals een aanvraag of een pagina weergave.</span><span class="sxs-lookup"><span data-stu-id="c46fc-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="c46fc-171">Elke rij is een niet-opgemaakte JSON-document.</span><span class="sxs-lookup"><span data-stu-id="c46fc-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="c46fc-172">Als u wilt plaatsen en staart op het, opent u het in Visual Studio en kiest u bewerken en Geavanceerd indelingsbestand:</span><span class="sxs-lookup"><span data-stu-id="c46fc-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![De telemetrie met een geschikt hulpprogramma weergeven](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="c46fc-174">Tijdsduren zijn in ticks, waarbij 10 000 bedraagt ticks = 1ms.</span><span class="sxs-lookup"><span data-stu-id="c46fc-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="c46fc-175">Deze waarden wordt bijvoorbeeld een tijd van 1ms een aanvraag te verzenden vanuit de browser, 3 MS te ontvangen en 1.8s voor het verwerken van de pagina in de browser weergeven:</span><span class="sxs-lookup"><span data-stu-id="c46fc-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="c46fc-176">Gedetailleerde gegevens model verwijzing voor de eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="c46fc-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="c46fc-177">Verwerken van de gegevens</span><span class="sxs-lookup"><span data-stu-id="c46fc-177">Processing the data</span></span>
<span data-ttu-id="c46fc-178">Op kleine schaal, kunt u bepaalde code kunt u gegevens uit elkaar, in een werkblad kunnen lezen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c46fc-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="c46fc-179">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c46fc-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="c46fc-180">Zie voor een grotere codevoorbeeld [met behulp van een werkrol][exportasa].</span><span class="sxs-lookup"><span data-stu-id="c46fc-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="c46fc-181"><a name="delete"></a>Uw oude gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46fc-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="c46fc-182">Houd er rekening mee dat u zelf verantwoordelijk bent voor het beheren van uw opslagcapaciteit en het verwijderen van de oude gegevens zo nodig.</span><span class="sxs-lookup"><span data-stu-id="c46fc-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="c46fc-183">Als u uw opslagsleutel opnieuw genereren...</span><span class="sxs-lookup"><span data-stu-id="c46fc-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="c46fc-184">Als u de sleutel naar uw opslag wijzigt, wordt continue export niet meer.</span><span class="sxs-lookup"><span data-stu-id="c46fc-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="c46fc-185">U ziet een melding in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c46fc-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="c46fc-186">Open de blade continue Export en uw export bewerken.</span><span class="sxs-lookup"><span data-stu-id="c46fc-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="c46fc-187">De bestemming exporteren bewerken, maar stelt u de dezelfde opslag die is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c46fc-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="c46fc-188">Klik op OK om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-188">Click OK to confirm.</span></span>

![Bewerk de continue export openen en sluiten thee bestemming voor exporteren.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="c46fc-190">De continue export wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="c46fc-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="c46fc-191">Exporteren van voorbeelden</span><span class="sxs-lookup"><span data-stu-id="c46fc-191">Export samples</span></span>

* <span data-ttu-id="c46fc-192">[Exporteren naar SQL met Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="c46fc-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="c46fc-193">Stream Analytics voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="c46fc-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="c46fc-194">Overweeg op grotere schaal [HDInsight](https://azure.microsoft.com/services/hdinsight/) -Hadoop-clusters in de cloud.</span><span class="sxs-lookup"><span data-stu-id="c46fc-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="c46fc-195">HDInsight biedt een reeks technologieën voor het beheren en analyseren van grote gegevens en u deze kunt gebruiken om gegevens die zijn geëxporteerd uit de Application Insights te verwerken.</span><span class="sxs-lookup"><span data-stu-id="c46fc-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="c46fc-196">Vragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="c46fc-196">Q & A</span></span>
* <span data-ttu-id="c46fc-197">*Maar alle gewenste is een eenmalige download van een grafiek.*</span><span class="sxs-lookup"><span data-stu-id="c46fc-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="c46fc-198">Ja, kunt u dat doen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-198">Yes, you can do that.</span></span> <span data-ttu-id="c46fc-199">Klik boven aan de blade op **gegevens exporteren**.</span><span class="sxs-lookup"><span data-stu-id="c46fc-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="c46fc-200">*Ik heb een export ingesteld, maar er zijn geen gegevens in de winkel.*</span><span class="sxs-lookup"><span data-stu-id="c46fc-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="c46fc-201">Heeft Application Insights ontvangen alle telemetrie van uw app omdat u de export instellen?</span><span class="sxs-lookup"><span data-stu-id="c46fc-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="c46fc-202">U ontvangt alleen nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="c46fc-202">You'll only receive new data.</span></span>
* <span data-ttu-id="c46fc-203">*Geprobeerd een export instellen, maar is toegang geweigerd*</span><span class="sxs-lookup"><span data-stu-id="c46fc-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="c46fc-204">Als het account eigendom is van uw organisatie, moet u lid zijn van de groepen eigenaars of medewerkers.</span><span class="sxs-lookup"><span data-stu-id="c46fc-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="c46fc-205">*Kan ik meteen naar mijn eigen winkel lokale exporteren?*</span><span class="sxs-lookup"><span data-stu-id="c46fc-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="c46fc-206">Nee, momenteel.</span><span class="sxs-lookup"><span data-stu-id="c46fc-206">No, sorry.</span></span> <span data-ttu-id="c46fc-207">De engine voor het exporteren wordt momenteel alleen ondersteund met Azure storage op dit moment.</span><span class="sxs-lookup"><span data-stu-id="c46fc-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="c46fc-208">*Is er een limiet voor de hoeveelheid gegevens die u in Mijn archief plaatsen?*</span><span class="sxs-lookup"><span data-stu-id="c46fc-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="c46fc-209">Nee.</span><span class="sxs-lookup"><span data-stu-id="c46fc-209">No.</span></span> <span data-ttu-id="c46fc-210">We je houden gegevens worden gepusht totdat u de export verwijdert.</span><span class="sxs-lookup"><span data-stu-id="c46fc-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="c46fc-211">We stopt als we de buitenste limieten voor blob-opslag bereikt, maar dat heel groot is.</span><span class="sxs-lookup"><span data-stu-id="c46fc-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="c46fc-212">Het is aan u om te bepalen hoeveel opslagruimte die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c46fc-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="c46fc-213">*Hoeveel blobs moet ik Zie in de opslag?*</span><span class="sxs-lookup"><span data-stu-id="c46fc-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="c46fc-214">Voor elk gegevenstype dat u hebt geselecteerd om te exporteren, wordt een nieuwe blob elke minuut gemaakt (als de gegevens beschikbaar is).</span><span class="sxs-lookup"><span data-stu-id="c46fc-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="c46fc-215">Bovendien voor toepassingen met intensief verkeer moet extra partitie eenheden zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="c46fc-216">Elke eenheid maakt een blob in dit geval elke minuut.</span><span class="sxs-lookup"><span data-stu-id="c46fc-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="c46fc-217">*Ik heb de sleutel wordt opnieuw gegenereerd met mijn opslag of de naam van de container gewijzigd en nu de export niet werkt.*</span><span class="sxs-lookup"><span data-stu-id="c46fc-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="c46fc-218">De export bewerken en open de blade van de bestemming exporteren.</span><span class="sxs-lookup"><span data-stu-id="c46fc-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="c46fc-219">Laat dezelfde opslag als voorheen geselecteerd en klik op OK om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="c46fc-220">Exporteren wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="c46fc-220">Export will restart.</span></span> <span data-ttu-id="c46fc-221">Als de wijziging in de afgelopen paar dagen was, geen gegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="c46fc-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="c46fc-222">*Kan ik de export onderbreken?*</span><span class="sxs-lookup"><span data-stu-id="c46fc-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="c46fc-223">Ja.</span><span class="sxs-lookup"><span data-stu-id="c46fc-223">Yes.</span></span> <span data-ttu-id="c46fc-224">Klik op uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c46fc-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="c46fc-225">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="c46fc-225">Code samples</span></span>

* [<span data-ttu-id="c46fc-226">Stream Analytics-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c46fc-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="c46fc-227">[Exporteren naar SQL met Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="c46fc-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="c46fc-228">Gedetailleerde gegevens model verwijzing voor de eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="c46fc-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
