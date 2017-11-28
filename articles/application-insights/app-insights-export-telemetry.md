---
title: aaaContinuous exporteren van telemetrie in Application Insights | Microsoft Docs
description: Diagnostische en gebruiksgegevens gegevens toostorage in Microsoft Azure exporteren en dit van daaruit te downloaden.
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="f1da8-103">Exporteren van telemetrie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f1da8-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="f1da8-104">Wilt u tookeep uw telemetrie langer dan de standaard bewaarperiode Hallo?</span><span class="sxs-lookup"><span data-stu-id="f1da8-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="f1da8-105">Of op een speciale wijze worden verwerkt?</span><span class="sxs-lookup"><span data-stu-id="f1da8-105">Or process it in some specialized way?</span></span> <span data-ttu-id="f1da8-106">Continue Export is ideaal voor dit.</span><span class="sxs-lookup"><span data-stu-id="f1da8-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="f1da8-107">u in de Application Insights-portal Hallo ziet Hallo-gebeurtenissen kunnen worden geëxporteerde toostorage in Microsoft Azure in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="f1da8-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="f1da8-108">Daar kunt u downloaden van uw gegevens en wat u code schrijven tooprocess moet het.</span><span class="sxs-lookup"><span data-stu-id="f1da8-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="f1da8-109">Met behulp van continue Export mogelijk extra kosten in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="f1da8-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="f1da8-110">Controleer uw [prijzen model](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="f1da8-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="f1da8-111">Voordat u de continue export instelt, zijn er enkele alternatieven kunt u tooconsider:</span><span class="sxs-lookup"><span data-stu-id="f1da8-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="f1da8-112">Hallo Export knop Hallo boven aan een blade metrische gegevens of zoeken kunt u tabellen en grafieken tooan Excel-spreadsheet overdragen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="f1da8-113">[Analytics](app-insights-analytics.md) biedt een krachtige querytaal voor telemetrie.</span><span class="sxs-lookup"><span data-stu-id="f1da8-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="f1da8-114">Het kan ook resultaten exporteren.</span><span class="sxs-lookup"><span data-stu-id="f1da8-114">It can also export results.</span></span>
* <span data-ttu-id="f1da8-115">Als u op zoek bent te[Verken uw gegevens in Power BI](app-insights-export-power-bi.md), kunt u dat doen zonder gebruik van continue Export.</span><span class="sxs-lookup"><span data-stu-id="f1da8-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="f1da8-116">Hallo [REST-API toegang tot de gegevens](https://dev.applicationinsights.io/) kunt u programmatisch toegang krijgen tot uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="f1da8-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="f1da8-117">Nadat uw gegevens toostorage (waar het kunt blijven voor als u wilt) continue Export zijn gekopieerd, is het nog steeds beschikbaar in Application Insights voor Hallo gebruikelijke [bewaarperiode](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="f1da8-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="f1da8-118"><a name="setup"></a>Maken van een continue Export</span><span class="sxs-lookup"><span data-stu-id="f1da8-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="f1da8-119">Open continue Export in Hallo Application Insights-resource voor uw app, en kies **toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="f1da8-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Schuif naar beneden en klik op de continue Export](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="f1da8-121">Kies Hallo telemetrie gegevenstypen gewenste tooexport.</span><span class="sxs-lookup"><span data-stu-id="f1da8-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="f1da8-122">Maak of Selecteer een [Azure storage-account](../storage/common/storage-introduction.md) waar u toostore Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1da8-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="f1da8-123">Hallo-opslaglocatie zal worden standaard toohello dezelfde geografische regio als uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="f1da8-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="f1da8-124">Als u in een andere regio opslaat, u mogelijk ook wijzigingskosten overdracht.</span><span class="sxs-lookup"><span data-stu-id="f1da8-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Klik op toevoegen, exporteren bestemming Storage-account en maakt een nieuwe winkel of kies een bestaand archief](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="f1da8-126">Maak of Selecteer een container in Hallo opslag:</span><span class="sxs-lookup"><span data-stu-id="f1da8-126">Create or select a container in hello storage:</span></span>

    ![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="f1da8-128">Als u uw export hebt gemaakt, wordt er gestart gaan.</span><span class="sxs-lookup"><span data-stu-id="f1da8-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="f1da8-129">U alleen ophalen gegevens die na het maken van Hallo export aankomt.</span><span class="sxs-lookup"><span data-stu-id="f1da8-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="f1da8-130">Er is een vertraging van ongeveer een uur voordat gegevens worden weergegeven in het Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="f1da8-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="f1da8-131">continue export tooedit</span><span class="sxs-lookup"><span data-stu-id="f1da8-131">tooedit continuous export</span></span>

<span data-ttu-id="f1da8-132">Als u wilt dat toochange Hallo gebeurtenistypen later, net Hallo export bewerken:</span><span class="sxs-lookup"><span data-stu-id="f1da8-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Klik op de typen gebeurtenissen kiezen](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="f1da8-134">continue export toostop</span><span class="sxs-lookup"><span data-stu-id="f1da8-134">toostop continuous export</span></span>

<span data-ttu-id="f1da8-135">toostop hello exporteren, klikt u op uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="f1da8-136">Als u opnieuw inschakelen op, kunnen Hallo exporteren wordt opnieuw opgestart met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1da8-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="f1da8-137">U won't Hallo gegevens dat is ontvangen in de portal Hallo terwijl export is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f1da8-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="f1da8-138">toostop hello exporteren, deze permanent verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="f1da8-139">In dat geval verwijdert niet de gegevens van opslag.</span><span class="sxs-lookup"><span data-stu-id="f1da8-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="f1da8-140">Kan niet toevoegen of wijzigen van een exporteren?</span><span class="sxs-lookup"><span data-stu-id="f1da8-140">Can't add or change an export?</span></span>
* <span data-ttu-id="f1da8-141">de uitvoer tooadd of wijzigen, moet u eigenaar, bijdrager of Application Insights Inzender toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="f1da8-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="f1da8-142">[Meer informatie over functies][roles].</span><span class="sxs-lookup"><span data-stu-id="f1da8-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="f1da8-143"><a name="analyze"></a>Welke gebeurtenissen krijgt u?</span><span class="sxs-lookup"><span data-stu-id="f1da8-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="f1da8-144">Hallo is geëxporteerde gegevens Hallo onbewerkte telemetrie die we van uw toepassing ontvangen, behalve dat we locatiegegevens waarmee de berekening van Hallo client-IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="f1da8-145">Gegevens die zijn genegeerd door [steekproeven](app-insights-sampling.md) is niet opgenomen in Hallo geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1da8-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="f1da8-146">Andere berekende waarden zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="f1da8-147">Bijvoorbeeld: gemiddelde CPU-gebruik niet worden geëxporteerd, maar we Exporteer Hallo onbewerkte telemetrie waaruit Hallo gemiddelde wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="f1da8-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="f1da8-148">Hallo gegevens omvatten ook Hallo resultaten van een [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) die u hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f1da8-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="f1da8-149">**Een steekproef.**</span><span class="sxs-lookup"><span data-stu-id="f1da8-149">**Sampling.**</span></span> <span data-ttu-id="f1da8-150">Als uw toepassing grote hoeveelheden gegevens verzendt, wordt Hallo steekproeven functie werkt en wordt alleen een fractie van Hallo gegenereerd telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="f1da8-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="f1da8-151">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="f1da8-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="f1da8-152"><a name="get"></a>Hallo gegevens controleren</span><span class="sxs-lookup"><span data-stu-id="f1da8-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="f1da8-153">U kunt inspecteren Hallo opslag rechtstreeks in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f1da8-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="f1da8-154">Klik op **Bladeren**, selecteer uw storage-account en open vervolgens **Containers**.</span><span class="sxs-lookup"><span data-stu-id="f1da8-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="f1da8-155">tooinspect Azure-opslag in Visual Studio openen **weergave**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f1da8-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="f1da8-156">(Als u deze menuopdracht niet hebt, moet u tooinstall hello Azure SDK: Open Hallo **nieuw Project** dialoogvenster Vouw Visual C# / Cloud en kies **ophalen van Microsoft Azure SDK voor .NET**.)</span><span class="sxs-lookup"><span data-stu-id="f1da8-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="f1da8-157">Wanneer u uw bloblarchief opent, ziet u een container met een set van blob-bestanden.</span><span class="sxs-lookup"><span data-stu-id="f1da8-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="f1da8-158">Hallo-URI van elk bestand dat is afgeleid van de naam van uw Application Insights-resource, de instrumentatiesleutel, telemetrie-type/datum/tijd.</span><span class="sxs-lookup"><span data-stu-id="f1da8-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="f1da8-159">(Hallo resourcenaam is alleen kleine letters bevatten, en de instrumentatiesleutel Hallo streepjes worden weggelaten.)</span><span class="sxs-lookup"><span data-stu-id="f1da8-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Hallo blob-opslag met een geschikt hulpprogramma controleren](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="f1da8-161">Hallo-datum en tijd UTC zijn en zijn wanneer Hallo telemetrie is gedeponeerd in Hallo store - niet Hallo tijd is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f1da8-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="f1da8-162">Als u code toodownload Hallo gegevens schrijft, het verplaatsen lineair Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1da8-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="f1da8-163">Hier volgt Hallo vorm van Hallo-pad:</span><span class="sxs-lookup"><span data-stu-id="f1da8-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="f1da8-164">waar</span><span class="sxs-lookup"><span data-stu-id="f1da8-164">Where</span></span>

* <span data-ttu-id="f1da8-165">`blobCreationTimeUtc`tijdstip waarop blob is gemaakt in Hallo interne is staging-opslag</span><span class="sxs-lookup"><span data-stu-id="f1da8-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="f1da8-166">`blobDeliveryTimeUtc`Hallo keer is dat wanneer blob gekopieerde toohello export-doelopslag is</span><span class="sxs-lookup"><span data-stu-id="f1da8-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="f1da8-167"><a name="format"></a>Indeling van gegevens</span><span class="sxs-lookup"><span data-stu-id="f1da8-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="f1da8-168">Elke blob is een tekstbestand dat meerdere bevat ' \n'-separated rijen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="f1da8-169">Het bevat Hallo telemetrie gedurende een periode van ongeveer een halve minuut is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f1da8-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="f1da8-170">Elke rij vertegenwoordigt een gegevenspunt telemetrie zoals een aanvraag of een pagina weergave.</span><span class="sxs-lookup"><span data-stu-id="f1da8-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="f1da8-171">Elke rij is een niet-opgemaakte JSON-document.</span><span class="sxs-lookup"><span data-stu-id="f1da8-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="f1da8-172">Als u toosit wilt en op het staart, opent u het in Visual Studio en kies bewerken, Geavanceerd indelingsbestand:</span><span class="sxs-lookup"><span data-stu-id="f1da8-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Telemetrie van paginaweergaven Hallo met een geschikt hulpprogramma](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="f1da8-174">Tijdsduren zijn in ticks, waarbij 10 000 bedraagt ticks = 1ms.</span><span class="sxs-lookup"><span data-stu-id="f1da8-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="f1da8-175">Bijvoorbeeld: deze waarden weergeven voor een periode van 1ms toosend een aanvraag van Hallo browser, 3 MS tooreceive en 1.8s tooprocess Hallo pagina in de browser Hallo:</span><span class="sxs-lookup"><span data-stu-id="f1da8-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="f1da8-176">Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="f1da8-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="f1da8-177">Hallo verwerken van gegevens</span><span class="sxs-lookup"><span data-stu-id="f1da8-177">Processing hello data</span></span>
<span data-ttu-id="f1da8-178">Op kleine schaal, kunt u sommige code toopull elkaar uw gegevens te schrijven, lezen in een werkblad, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f1da8-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="f1da8-179">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f1da8-179">For example:</span></span>

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

<span data-ttu-id="f1da8-180">Zie voor een grotere codevoorbeeld [met behulp van een werkrol][exportasa].</span><span class="sxs-lookup"><span data-stu-id="f1da8-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="f1da8-181"><a name="delete"></a>Uw oude gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="f1da8-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="f1da8-182">Houd er rekening mee dat u zelf verantwoordelijk bent voor het beheren van uw opslagcapaciteit en het verwijderen van oude gegevens Hallo indien nodig.</span><span class="sxs-lookup"><span data-stu-id="f1da8-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="f1da8-183">Als u uw opslagsleutel opnieuw genereren...</span><span class="sxs-lookup"><span data-stu-id="f1da8-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="f1da8-184">Als u Hallo sleutel tooyour opslag wijzigt, wordt continue export niet meer.</span><span class="sxs-lookup"><span data-stu-id="f1da8-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="f1da8-185">U ziet een melding in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f1da8-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="f1da8-186">Hallo continue Export blade openen en bewerken van het exporteren.</span><span class="sxs-lookup"><span data-stu-id="f1da8-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="f1da8-187">Hallo exporteren bestemming bewerken, maar stelt u Hallo dezelfde opslag geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f1da8-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="f1da8-188">Klik op OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="f1da8-188">Click OK tooconfirm.</span></span>

![Bewerken Hallo continue exporteren, openen en sluiten thee exportbestemming.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="f1da8-190">Hallo continue export wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="f1da8-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="f1da8-191">Exporteren van voorbeelden</span><span class="sxs-lookup"><span data-stu-id="f1da8-191">Export samples</span></span>

* <span data-ttu-id="f1da8-192">[Met Stream Analytics tooSQL exporteren][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f1da8-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f1da8-193">Stream Analytics voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="f1da8-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="f1da8-194">Overweeg op grotere schaal [HDInsight](https://azure.microsoft.com/services/hdinsight/) -Hadoop-clusters in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="f1da8-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="f1da8-195">HDInsight biedt een reeks technologieën voor het beheren en analyseren van grote gegevens en u tooprocess gegevens die zijn geëxporteerd uit de Application Insights kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1da8-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="f1da8-196">Vragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="f1da8-196">Q & A</span></span>
* <span data-ttu-id="f1da8-197">*Maar alle gewenste is een eenmalige download van een grafiek.*</span><span class="sxs-lookup"><span data-stu-id="f1da8-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="f1da8-198">Ja, kunt u dat doen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-198">Yes, you can do that.</span></span> <span data-ttu-id="f1da8-199">Klik boven Hallo van Hallo-blade op **gegevens exporteren**.</span><span class="sxs-lookup"><span data-stu-id="f1da8-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="f1da8-200">*Ik heb een export ingesteld, maar er zijn geen gegevens in de winkel.*</span><span class="sxs-lookup"><span data-stu-id="f1da8-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="f1da8-201">Heeft Application Insights ontvangen alle telemetrie van uw app omdat u Hallo export instellen?</span><span class="sxs-lookup"><span data-stu-id="f1da8-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="f1da8-202">U ontvangt alleen nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1da8-202">You'll only receive new data.</span></span>
* <span data-ttu-id="f1da8-203">*Tooset up exporteren van een geprobeerd, maar is toegang geweigerd*</span><span class="sxs-lookup"><span data-stu-id="f1da8-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="f1da8-204">Als Hallo account eigendom is van uw organisatie, hebt u toobe lid is van Hallo eigenaars of inzenders groepen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="f1da8-205">*Kan ik rechte toomy eigen lokale store exporteren?*</span><span class="sxs-lookup"><span data-stu-id="f1da8-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="f1da8-206">Nee, momenteel.</span><span class="sxs-lookup"><span data-stu-id="f1da8-206">No, sorry.</span></span> <span data-ttu-id="f1da8-207">De engine voor het exporteren wordt momenteel alleen ondersteund met Azure storage op dit moment.</span><span class="sxs-lookup"><span data-stu-id="f1da8-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="f1da8-208">*Is er limiet toohello hoeveelheid gegevens die u in Mijn archief plaatsen?*</span><span class="sxs-lookup"><span data-stu-id="f1da8-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="f1da8-209">Nee.</span><span class="sxs-lookup"><span data-stu-id="f1da8-209">No.</span></span> <span data-ttu-id="f1da8-210">We je houden gegevens worden gepusht totdat u Hallo export verwijdert.</span><span class="sxs-lookup"><span data-stu-id="f1da8-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="f1da8-211">We stopt als wij Hallo buitenste limieten voor blob-opslag bereikt, maar dat is heel groot.</span><span class="sxs-lookup"><span data-stu-id="f1da8-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="f1da8-212">Is tooyou toocontrol hoeveel opslagruimte die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f1da8-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="f1da8-213">*Hoeveel blobs moet ik Zie in Hallo storage?*</span><span class="sxs-lookup"><span data-stu-id="f1da8-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="f1da8-214">Voor elk gegevenstype u wordt geselecteerde tooexport, een nieuwe blob elke minuut gemaakt (als de gegevens beschikbaar is).</span><span class="sxs-lookup"><span data-stu-id="f1da8-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="f1da8-215">Bovendien voor toepassingen met intensief verkeer moet extra partitie eenheden zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="f1da8-216">Elke eenheid maakt een blob in dit geval elke minuut.</span><span class="sxs-lookup"><span data-stu-id="f1da8-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="f1da8-217">*Ik Hallo sleutel toomy opslag opnieuw gegenereerd of Hallo-naam van de container Hallo gewijzigd en nu Hallo export niet werkt.*</span><span class="sxs-lookup"><span data-stu-id="f1da8-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="f1da8-218">Hallo export bewerken blade en open Hallo export bestemming.</span><span class="sxs-lookup"><span data-stu-id="f1da8-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="f1da8-219">Laat Hallo dezelfde opslag als voorheen geselecteerd en klik op OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="f1da8-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="f1da8-220">Exporteren wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="f1da8-220">Export will restart.</span></span> <span data-ttu-id="f1da8-221">Als Hallo wijzigen binnen Hallo afgelopen paar dagen was, geen gegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="f1da8-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="f1da8-222">*Kan ik Hallo export onderbreken?*</span><span class="sxs-lookup"><span data-stu-id="f1da8-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="f1da8-223">Ja.</span><span class="sxs-lookup"><span data-stu-id="f1da8-223">Yes.</span></span> <span data-ttu-id="f1da8-224">Klik op uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1da8-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="f1da8-225">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="f1da8-225">Code samples</span></span>

* [<span data-ttu-id="f1da8-226">Stream Analytics-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f1da8-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="f1da8-227">[Met Stream Analytics tooSQL exporteren][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f1da8-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f1da8-228">Gedetailleerde gegevens model verwijzing voor Hallo eigenschaptypen en waarden.</span><span class="sxs-lookup"><span data-stu-id="f1da8-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
