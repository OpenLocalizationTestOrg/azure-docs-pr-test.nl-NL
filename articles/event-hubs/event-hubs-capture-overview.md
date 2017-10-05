---
title: Overzicht van Azure Event Hubs vastleggen | Microsoft Docs
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
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="6417d-103">Azure Event Hubs vastleggen</span><span class="sxs-lookup"><span data-stu-id="6417d-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="6417d-104">Azure Event Hubs vastleggen, kunt u automatisch de streaminggegevens in Event Hubs te leveren een [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) of [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) -account van uw keuze, met de extra flexibiliteit het opgeven van een interval van tijd of grootte.</span><span class="sxs-lookup"><span data-stu-id="6417d-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="6417d-105">Het instellen van het vastleggen is snel, er zijn geen administratieve kosten uit te voeren en wordt automatisch geschaald met Event Hubs [doorvoereenheden](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="6417d-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="6417d-106">Event Hubs vastleggen is de eenvoudigste manier om te streamen gegevens laden in Azure, en kunt u zich kunt richten op het verwerken van gegevens in plaats van op het opnemen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6417d-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="6417d-107">Event Hubs vastleggen, kunt u in real-time en op basis van batch pijplijnen op de dezelfde stroom verwerken.</span><span class="sxs-lookup"><span data-stu-id="6417d-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="6417d-108">Dit betekent dat u kunt oplossingen bouwt die groeien met uw behoeften gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="6417d-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="6417d-109">Of u bij het bouwen van batch-systemen vandaag nog met het oog op toekomstige realtime verwerking of u wilt een efficiënte koude pad toevoegen aan een bestaande realtime oplossing, is het vastleggen van Event Hubs werken met gegevensstromen eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="6417d-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="6417d-110">Event Hubs vastleggen werking</span><span class="sxs-lookup"><span data-stu-id="6417d-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="6417d-111">Event Hubs is een duurzame buffer tijd bewaren voor telemetrie inkomend, vergelijkbaar met een gedistribueerde logboek.</span><span class="sxs-lookup"><span data-stu-id="6417d-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="6417d-112">De sleutel voor schaling in Event Hubs is de [gepartitioneerde consumer model](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="6417d-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="6417d-113">Elke partitie is een onafhankelijke segment van gegevens en onafhankelijk is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="6417d-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="6417d-114">Na verloop van tijd deze gegevens van jaar uit, op basis van de configureerbare bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="6417d-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="6417d-115">Als gevolg hiervan een bepaalde gebeurtenis hub nooit ' te vol raakt. "</span><span class="sxs-lookup"><span data-stu-id="6417d-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="6417d-116">Event Hubs vastleggen, kunt u uw eigen Azure Blob storage-account en een container of een Azure Data Lake Store-account worden gebruikt voor het opslaan van de vastgelegde gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="6417d-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="6417d-117">Deze accounts kunnen zich in dezelfde regio bevinden als uw event hub of in een andere regio, toe te voegen aan de flexibiliteit van de functie voor het vastleggen van Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="6417d-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="6417d-118">Gegevensopname is geschreven in [Apache Avro] [ Apache Avro] indeling: een compact, snelle, binaire indeling die uitgebreide gegevensstructuren inlineschema biedt.</span><span class="sxs-lookup"><span data-stu-id="6417d-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="6417d-119">Deze indeling wordt veel gebruikt in de Hadoop-ecosysteem, Stream Analytics en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6417d-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="6417d-120">Meer informatie over het werken met Avro vindt verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6417d-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="6417d-121">Windowing vastleggen</span><span class="sxs-lookup"><span data-stu-id="6417d-121">Capture windowing</span></span>

<span data-ttu-id="6417d-122">Event Hubs vastleggen, kunt u een venster instellen om te bepalen vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="6417d-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="6417d-123">Dit venster is een minimale grootte en de configuratie van de tijd met een 'eerste WINS-beleid,' wat betekent dat de eerste trigger is aangetroffen, een capture-bewerking wordt.</span><span class="sxs-lookup"><span data-stu-id="6417d-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="6417d-124">Als u een vijftien minuten hebt, is 100 MB venster vastleggen en verzenden van 1 MB per seconde, de grootte van venster triggers voordat het tijdvenster.</span><span class="sxs-lookup"><span data-stu-id="6417d-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="6417d-125">Elke partitie afzonderlijk vastgelegd en schrijft een voltooide blok-blob op het moment van vastleggen, met de naam van de tijd waarop de capture-interval is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="6417d-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="6417d-126">De naamconventie voor opslag is als volgt:</span><span class="sxs-lookup"><span data-stu-id="6417d-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="6417d-127">Doorvoereenheden schalen</span><span class="sxs-lookup"><span data-stu-id="6417d-127">Scaling to throughput units</span></span>

<span data-ttu-id="6417d-128">Event Hubs-verkeer wordt beheerd door [doorvoereenheden](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="6417d-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="6417d-129">Eén doorvoereenheid kunt 1 MB per seconde of 1000 gebeurtenissen per seconde van inkomende en twee keer de omvang van uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="6417d-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="6417d-130">Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden en u kunt meer aanschaffen bij een quotum verhogen [ondersteuningsaanvraag][support request].</span><span class="sxs-lookup"><span data-stu-id="6417d-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="6417d-131">Gebruik dat buiten uw aangeschafte doorvoereenheden wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="6417d-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="6417d-132">Event Hubs vastleggen kopieert gegevens rechtstreeks vanuit de interne opslag van de Event Hubs het overslaan van doorvoer eenheid uitgaande quota en opslaan van uw uitgaande voor andere lezers verwerking zoals Stream Analytics of Spark.</span><span class="sxs-lookup"><span data-stu-id="6417d-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="6417d-133">Na de configuratie vastleggen van Event Hubs wordt automatisch uitgevoerd wanneer u uw eerste gebeurtenis verzenden en wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="6417d-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="6417d-134">Event Hubs schrijft lege bestanden voor de downstreamverwerking te weten dat het proces werkt te vereenvoudigen, wanneer er geen gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="6417d-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="6417d-135">Deze procedure biedt een voorspelbare uitgebracht en de markering die kan worden ingevoerd uw batch-processors.</span><span class="sxs-lookup"><span data-stu-id="6417d-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="6417d-136">Instellen van het vastleggen van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6417d-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="6417d-137">U kunt vastleggen configureren op de event hub maken tijd met behulp van de [Azure-portal](https://portal.azure.com), of met behulp van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6417d-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="6417d-138">Raadpleeg voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="6417d-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="6417d-139">Inschakelen van Event Hubs vastleggen met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6417d-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="6417d-140">Maken van een naamruimte Event Hubs met een event hub en vastleggen met behulp van een Azure Resource Manager-sjabloon inschakelen</span><span class="sxs-lookup"><span data-stu-id="6417d-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="6417d-141">De vastgelegde bestanden verkennen en werken met Avro</span><span class="sxs-lookup"><span data-stu-id="6417d-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="6417d-142">Vastleggen van Event Hubs maakt bestanden in de Avro-indeling die is opgegeven op de geconfigureerde periode.</span><span class="sxs-lookup"><span data-stu-id="6417d-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="6417d-143">U kunt deze bestanden weergeven in een hulpprogramma zoals [Azure Opslagverkenner][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="6417d-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="6417d-144">U kunt downloaden de bestanden lokaal te werken.</span><span class="sxs-lookup"><span data-stu-id="6417d-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="6417d-145">De bestanden die wordt geproduceerd door het vastleggen van Event Hubs hebben de volgende Avro-schema:</span><span class="sxs-lookup"><span data-stu-id="6417d-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="6417d-146">Een eenvoudige manier om te verkennen Avro-bestanden is via de [Avro extra] [ Avro Tools] jar van Apache.</span><span class="sxs-lookup"><span data-stu-id="6417d-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="6417d-147">Na het downloaden van dit jar, ziet u het schema van een specifiek Avro-bestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6417d-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="6417d-148">Met deze opdracht retourneert</span><span class="sxs-lookup"><span data-stu-id="6417d-148">This command returns</span></span>

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

<span data-ttu-id="6417d-149">U kunt ook de Avro-hulpprogramma's gebruiken voor het bestand converteren naar JSON-indeling en andere bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6417d-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="6417d-150">Als u meer geavanceerde verwerken, downloaden en installeren van Avro voor uw keuze van platform.</span><span class="sxs-lookup"><span data-stu-id="6417d-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="6417d-151">Op het moment van schrijven van dit er implementaties beschikbaar zijn voor C, C++, C\#, Java, NodeJS, Perl, PHP, Python en Ruby.</span><span class="sxs-lookup"><span data-stu-id="6417d-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="6417d-152">Apache Avro is voltooid aan de slag-handleidingen voor [Java] [ Java] en [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="6417d-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="6417d-153">U kunt ook lezen de [aan de slag met Event Hubs vastleggen](event-hubs-capture-python.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="6417d-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="6417d-154">Hoe Event Hubs vastleggen wordt in rekening gebracht</span><span class="sxs-lookup"><span data-stu-id="6417d-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="6417d-155">Event Hubs vastleggen datalimiet geldt ook voor doorvoereenheden: als een per uur kosten.</span><span class="sxs-lookup"><span data-stu-id="6417d-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="6417d-156">De kosten is rechtstreeks evenredig met het aantal doorvoereenheden hebt aangeschaft voor de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="6417d-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="6417d-157">Als doorvoereenheden worden verhoogd of verlaagd, wordt Event Hubs vastleggen meters verhogen en minder overeenkomende prestaties bieden.</span><span class="sxs-lookup"><span data-stu-id="6417d-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="6417d-158">De meters optreden in combinatie.</span><span class="sxs-lookup"><span data-stu-id="6417d-158">The meters occur in tandem.</span></span> <span data-ttu-id="6417d-159">Zie voor prijsinformatie, [prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="6417d-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6417d-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6417d-160">Next steps</span></span>

<span data-ttu-id="6417d-161">Event Hubs vastleggen is de eenvoudigste manier om gegevens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="6417d-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="6417d-162">Met Azure Data Lake en Azure Data Factory Azure HDInsight kunt u batchverwerking uitvoeren en andere analyses met behulp van bekende hulpprogramma's en platforms van uw keuze op elke schaal moet u.</span><span class="sxs-lookup"><span data-stu-id="6417d-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="6417d-163">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="6417d-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="6417d-164">Aan de slag verzenden en ontvangen van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="6417d-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="6417d-165">Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="6417d-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="6417d-166">[Event Hubs-overzicht][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="6417d-166">[Event Hubs overview][Event Hubs overview]</span></span>

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
