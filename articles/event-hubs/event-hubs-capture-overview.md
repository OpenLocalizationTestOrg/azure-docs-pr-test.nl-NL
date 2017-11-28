---
title: aaaOverview van het vastleggen van Azure Event Hubs | Microsoft Docs
description: Vastleggen van telemetriegegevens met Event Hubs vastleggen
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="711a9-103">Azure Event Hubs vastleggen</span><span class="sxs-lookup"><span data-stu-id="711a9-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="711a9-104">Vastleggen van Azure Event Hubs kunt u tooautomatically afleveren Hallo gegevensstromen in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) of [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account van uw keuze, hello flexibiliteit toegevoegd voor het opgeven van een interval van tijd of grootte.</span><span class="sxs-lookup"><span data-stu-id="711a9-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="711a9-105">Het instellen van het vastleggen is snel, zijn er geen administratieve kosten toorun en deze schaalt automatisch met Event Hubs [doorvoereenheden](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="711a9-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="711a9-106">Vastleggen van Event Hubs is Hallo gemakkelijkste manier tooload gegevensstromen in Azure, en kunt u toofocus op gegevensverwerking in plaats van op het opnemen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="711a9-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="711a9-107">Vastleggen van Event Hubs kunt u realtime tooprocess en pijplijnen op basis van batch op Hallo dezelfde stroom.</span><span class="sxs-lookup"><span data-stu-id="711a9-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="711a9-108">Dit betekent dat u kunt oplossingen bouwt die groeien met uw behoeften gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="711a9-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="711a9-109">Of u bij het bouwen van batch-systemen vandaag nog met het oog op toekomstige realtime verwerking of u wilt dat tooadd een efficiënte koude pad tooan bestaande realtime-oplossing, is het vastleggen van Event Hubs werken met gegevensstromen eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="711a9-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="711a9-110">Event Hubs vastleggen werking</span><span class="sxs-lookup"><span data-stu-id="711a9-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="711a9-111">Event Hubs is een duurzame buffer tijd bewaren voor telemetrie inkomend, vergelijkbare tooa gedistribueerde logboek.</span><span class="sxs-lookup"><span data-stu-id="711a9-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="711a9-112">Hallo sleutel tooscaling in Event Hubs is Hallo [gepartitioneerde consumer model](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="711a9-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="711a9-113">Elke partitie is een onafhankelijke segment van gegevens en onafhankelijk is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="711a9-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="711a9-114">Na verloop van tijd die deze gegevens van jaar uitschakelen op basis van Hallo configureerbare bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="711a9-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="711a9-115">Als gevolg hiervan een bepaalde gebeurtenis hub nooit ' te vol raakt. "</span><span class="sxs-lookup"><span data-stu-id="711a9-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="711a9-116">U toospecify vastleggen van Event Hubs worden kunt uw eigen Azure Blob storage-account en een container of een Azure Data Lake Store-account, de gebruikte toostore Hallo vastgelegd gegevens.</span><span class="sxs-lookup"><span data-stu-id="711a9-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="711a9-117">Deze accounts kunnen zich in Hallo dezelfde regio als uw event hub of in een andere regio, toohello flexibiliteit van Event Hubs vastleggen Hallo-functie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="711a9-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="711a9-118">Gegevensopname is geschreven in [Apache Avro] [ Apache Avro] indeling: een compact, snelle, binaire indeling die uitgebreide gegevensstructuren inlineschema biedt.</span><span class="sxs-lookup"><span data-stu-id="711a9-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="711a9-119">Deze indeling wordt veel gebruikt in de Hadoop-ecosysteem hello, Stream Analytics en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="711a9-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="711a9-120">Meer informatie over het werken met Avro vindt verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="711a9-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="711a9-121">Windowing vastleggen</span><span class="sxs-lookup"><span data-stu-id="711a9-121">Capture windowing</span></span>

<span data-ttu-id="711a9-122">Vastleggen van Event Hubs kunnen tooset van een venster toocontrol vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="711a9-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="711a9-123">Dit venster is een minimale grootte en de configuratie van de tijd met een 'eerste WINS-beleid,' wat betekent dat Hallo eerste trigger is aangetroffen, wordt een capture-bewerking.</span><span class="sxs-lookup"><span data-stu-id="711a9-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="711a9-124">Als u hebt een vijftien minuten, 100 MB venster vastleggen en 1 MB per seconde Hallo grootte venster triggers voordat Hallo tijdvenster.</span><span class="sxs-lookup"><span data-stu-id="711a9-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="711a9-125">Elke partitie afzonderlijk vastgelegd en schrijft een voltooide blok-blob gelijktijdig Hallo met vastleggen, met de naam van Hallo tijd op welke Hallo vastleggen interval is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="711a9-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="711a9-126">Hallo opslag naamconventie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="711a9-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="711a9-127">Toothroughput eenheden schalen</span><span class="sxs-lookup"><span data-stu-id="711a9-127">Scaling toothroughput units</span></span>

<span data-ttu-id="711a9-128">Event Hubs-verkeer wordt beheerd door [doorvoereenheden](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="711a9-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="711a9-129">Eén doorvoereenheid kunt 1 MB per seconde of 1000 gebeurtenissen per seconde van inkomende en twee keer de omvang van uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="711a9-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="711a9-130">Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden en u kunt meer aanschaffen bij een quotum verhogen [ondersteuningsaanvraag][support request].</span><span class="sxs-lookup"><span data-stu-id="711a9-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="711a9-131">Gebruik dat buiten uw aangeschafte doorvoereenheden wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="711a9-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="711a9-132">Event Hubs vastleggen kopieert gegevens rechtstreeks vanuit Hallo interne Event Hubs opslag voor het overslaan van doorvoer eenheid uitgaande quota en opslaan van uw uitgaande voor andere lezers verwerking zoals Stream Analytics of Spark.</span><span class="sxs-lookup"><span data-stu-id="711a9-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="711a9-133">Na de configuratie vastleggen van Event Hubs wordt automatisch uitgevoerd wanneer u uw eerste gebeurtenis verzenden en wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="711a9-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="711a9-134">toomake het eenvoudiger voor de downstreamverwerking-tooknow die Hallo-proces werkt, Event Hubs lege bestanden schrijft wanneer er geen gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="711a9-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="711a9-135">Deze procedure biedt een voorspelbare uitgebracht en de markering die kan worden ingevoerd uw batch-processors.</span><span class="sxs-lookup"><span data-stu-id="711a9-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="711a9-136">Instellen van het vastleggen van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="711a9-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="711a9-137">U kunt vastleggen configureren tijdens het Hallo event hub maken met behulp van Hallo [Azure-portal](https://portal.azure.com), of met behulp van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="711a9-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="711a9-138">Zie voor meer informatie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="711a9-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="711a9-139">Inschakelen van Event Hubs vastleggen met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="711a9-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="711a9-140">Maken van een naamruimte Event Hubs met een event hub en vastleggen met behulp van een Azure Resource Manager-sjabloon inschakelen</span><span class="sxs-lookup"><span data-stu-id="711a9-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="711a9-141">Hallo vastgelegd bestanden verkennen en werken met Avro</span><span class="sxs-lookup"><span data-stu-id="711a9-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="711a9-142">Vastleggen van Event Hubs maakt bestanden in de Avro-indeling die is opgegeven op het tijdvenster Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="711a9-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="711a9-143">U kunt deze bestanden weergeven in een hulpprogramma zoals [Azure Opslagverkenner][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="711a9-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="711a9-144">U kunt downloaden Hallo bestanden lokaal toowork erop.</span><span class="sxs-lookup"><span data-stu-id="711a9-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="711a9-145">Hallo-bestanden die zijn geproduceerd door het vastleggen van Event Hubs hebben Hallo Avro-schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="711a9-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="711a9-146">Een eenvoudige manier tooexplore Avro-bestanden worden met behulp van Hallo [Avro extra] [ Avro Tools] jar van Apache.</span><span class="sxs-lookup"><span data-stu-id="711a9-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="711a9-147">Na het downloaden van dit jar, ziet u door het uitvoeren van de volgende opdracht Hallo Hallo-schema van een specifiek Avro-bestand:</span><span class="sxs-lookup"><span data-stu-id="711a9-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="711a9-148">Met deze opdracht retourneert</span><span class="sxs-lookup"><span data-stu-id="711a9-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="711a9-149">U kunt ook gebruik van hulpprogramma's voor Avro tooconvert hello tooJSON indeling en andere bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="711a9-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="711a9-150">tooperform meer geavanceerde verwerken, downloaden en installeren van Avro voor uw keuze van platform.</span><span class="sxs-lookup"><span data-stu-id="711a9-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="711a9-151">Hallo er bij uitvoering van dit artikel, zijn implementaties beschikbaar voor C, C++, C\#, Java, NodeJS, Perl, PHP, Python en Ruby.</span><span class="sxs-lookup"><span data-stu-id="711a9-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="711a9-152">Apache Avro is voltooid aan de slag-handleidingen voor [Java] [ Java] en [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="711a9-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="711a9-153">U kunt ook lezen Hallo [aan de slag met Event Hubs vastleggen](event-hubs-capture-python.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="711a9-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="711a9-154">Hoe Event Hubs vastleggen wordt in rekening gebracht</span><span class="sxs-lookup"><span data-stu-id="711a9-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="711a9-155">Vastleggen van Event Hubs wordt gemeten op dezelfde manier toothroughput eenheden: als een per uur kosten.</span><span class="sxs-lookup"><span data-stu-id="711a9-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="711a9-156">Hallo kosten is rechtstreeks evenredig toohello getal voor Hallo naamruimte aangeschafte doorvoereenheden.</span><span class="sxs-lookup"><span data-stu-id="711a9-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="711a9-157">Als doorvoereenheden worden verhoogd of verlaagd, worden de meters Event Hubs vastleggen verhogen en tooprovide die overeenkomt met de prestaties afnemen.</span><span class="sxs-lookup"><span data-stu-id="711a9-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="711a9-158">Hallo meters optreden in combinatie.</span><span class="sxs-lookup"><span data-stu-id="711a9-158">hello meters occur in tandem.</span></span> <span data-ttu-id="711a9-159">Zie voor prijsinformatie, [prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="711a9-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="711a9-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="711a9-160">Next steps</span></span>

<span data-ttu-id="711a9-161">Vastleggen van Event Hubs zijn Hallo gemakkelijkste manier tooget gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="711a9-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="711a9-162">Met Azure Data Lake en Azure Data Factory Azure HDInsight kunt u batchverwerking uitvoeren en andere analyses met behulp van bekende hulpprogramma's en platforms van uw keuze op elke schaal moet u.</span><span class="sxs-lookup"><span data-stu-id="711a9-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="711a9-163">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="711a9-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="711a9-164">Aan de slag verzenden en ontvangen van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="711a9-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="711a9-165">Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="711a9-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="711a9-166">[Event Hubs-overzicht][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="711a9-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
