---
title: Azure Blob-opslag gebruiken met de WebJobs SDK
description: Informatie over het Azure blob storage gebruiken met de WebJobs SDK. Een proces wordt geactiveerd wanneer een nieuwe blob wordt weergegeven in een container en verwerken van verontreinigde BLOB's.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="726c3-104">Azure Blob-opslag gebruiken met de WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="726c3-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="726c3-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="726c3-105">Overview</span></span>
<span data-ttu-id="726c3-106">Deze handleiding bevat C#-codevoorbeelden die laten hoe een proces wordt geactiveerd zien wanneer een Azure-blob is gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="726c3-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="726c3-107">De code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="726c3-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="726c3-108">Zie voor codevoorbeelden die laten hoe zien u blobs, [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="726c3-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="726c3-109">De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md) of [meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="726c3-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="726c3-110"><a id="trigger"></a>Het activeren van een functie wanneer een blob is gemaakt of bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="726c3-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="726c3-111">Deze sectie wordt beschreven hoe u de `BlobTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="726c3-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="726c3-112">De WebJobs SDK scant logboekbestanden moeten worden gecontroleerd op nieuwe of gewijzigde blobs.</span><span class="sxs-lookup"><span data-stu-id="726c3-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="726c3-113">Dit proces is niet realtime; een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat de blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="726c3-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="726c3-114">Bovendien [opslag logboeken worden gemaakt op een 'best inspanningen'](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; er is geen garantie dat alle gebeurtenissen wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="726c3-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="726c3-115">Onder bepaalde omstandigheden kunnen een logboeken worden gemist.</span><span class="sxs-lookup"><span data-stu-id="726c3-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="726c3-116">Als de beperkingen snelheid en betrouwbaarheid van blob-triggers niet toegestaan voor uw toepassing zijn, de aanbevolen methode is het maken van een wachtrijbericht wanneer u de blob maken en gebruiken de [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) kenmerk in plaats van de `BlobTrigger` kenmerk voor de functie die de blob wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="726c3-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="726c3-117">Één tijdelijke aanduiding voor blob-naam met de extensie</span><span class="sxs-lookup"><span data-stu-id="726c3-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="726c3-118">Het volgende codevoorbeeld kopieert tekst blobs die worden weergegeven in de *invoer* container voor de *uitvoer* container:</span><span class="sxs-lookup"><span data-stu-id="726c3-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="726c3-119">De kenmerkconstructor tekenreeksparameter een waarin de containernaam van de en een tijdelijke aanduiding voor de blob-naam opgegeven.</span><span class="sxs-lookup"><span data-stu-id="726c3-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="726c3-120">In dit voorbeeld als de naam van een blob *Blob1.txt* wordt gemaakt in de *invoer* -container, de functie maakt een blob met de naam *Blob1.txt* in de *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="726c3-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="726c3-121">Zoals wordt weergegeven in het volgende codevoorbeeld, kunt u een bestandsnaampatroon opgeven met de tijdelijke aanduiding voor blob:</span><span class="sxs-lookup"><span data-stu-id="726c3-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="726c3-122">Deze code alleen blobs die namen die beginnen met 'oorspronkelijke--' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="726c3-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="726c3-123">Bijvoorbeeld: *oorspronkelijke Blob1.txt* in de *invoer* container wordt gekopieerd naar *kopie Blob1.txt* in de *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="726c3-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="726c3-124">Als u een naampatroon opgeven voor blob-namen die accolades hebben met de naam moet, dubbelklikt u accolades gebruiken.</span><span class="sxs-lookup"><span data-stu-id="726c3-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="726c3-125">Bijvoorbeeld, als u wilt zoeken blobs in de *installatiekopieën* container met namen als volgt:</span><span class="sxs-lookup"><span data-stu-id="726c3-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="726c3-126">Gebruik deze optie voor het patroon:</span><span class="sxs-lookup"><span data-stu-id="726c3-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="726c3-127">In het voorbeeld wordt de *naam* aanduidingswaarde zou worden *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="726c3-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="726c3-128">Afzonderlijke blob-naam en extensie voor tijdelijke aanduidingen</span><span class="sxs-lookup"><span data-stu-id="726c3-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="726c3-129">Het volgende codevoorbeeld de bestandsextensie wijzigt, zoals het gekopieerd blobs die worden weergegeven in de *invoer* container voor de *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="726c3-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="726c3-130">De code registreert de uitbreiding van de *invoer* blob en stelt u de uitbreiding van de *uitvoer* -blob naar *.txt*.</span><span class="sxs-lookup"><span data-stu-id="726c3-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="726c3-131"><a id="types"></a>Typen die u aan BLOB's koppelen kunt</span><span class="sxs-lookup"><span data-stu-id="726c3-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="726c3-132">U kunt de `BlobTrigger` -kenmerk op de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="726c3-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="726c3-133">Andere typen gedeserialiseerd door [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="726c3-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="726c3-134">Als u samenwerken met het Azure storage-account wilt, kunt u ook toevoegen een `CloudStorageAccount` -parameter voor de methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="726c3-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="726c3-135">Zie voor voorbeelden van de [blob-binding-code in de sdk van azure webjobs-opslagplaats op GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="726c3-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="726c3-136"><a id="string"></a>Ophalen van blob tekstinhoud door binding naar een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="726c3-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="726c3-137">Als tekst blobs worden verwacht, `BlobTrigger` kunnen worden toegepast op een `string` parameter.</span><span class="sxs-lookup"><span data-stu-id="726c3-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="726c3-138">Het volgende codevoorbeeld wordt gebonden een tekst-blob naar een `string` parameter met de naam `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="726c3-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="726c3-139">De functie wordt deze parameter de inhoud van de blob geschreven naar het dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="726c3-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="726c3-140"><a id="icbsb"></a>Ophalen van blob-inhoud geserialiseerd met behulp van ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="726c3-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="726c3-141">Het volgende codevoorbeeld maakt gebruik van een klasse die implementeert `ICloudBlobStreamBinder` zodat de `BlobTrigger` kenmerk binden van een blob naar de `WebImage` type.</span><span class="sxs-lookup"><span data-stu-id="726c3-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="726c3-142">De `WebImage` binding code is opgegeven een `WebImageBinder` klasse die is afgeleid van `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="726c3-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="726c3-143">Ophalen van de blobpad voor de activerende blob</span><span class="sxs-lookup"><span data-stu-id="726c3-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="726c3-144">Als u wilt ophalen van de naam van de container en de blob-naam van de blob die de functie is geactiveerd, bevatten een `blobTrigger` opgegeven parameter in de functiehandtekening.</span><span class="sxs-lookup"><span data-stu-id="726c3-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="726c3-145"><a id="poison"></a>Het verwerken van verontreinigde blobs</span><span class="sxs-lookup"><span data-stu-id="726c3-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="726c3-146">Wanneer een `BlobTrigger` functie mislukt, de SDK-aanroepen deze opnieuw als de fout is veroorzaakt door een tijdelijke fout.</span><span class="sxs-lookup"><span data-stu-id="726c3-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="726c3-147">Als de fout wordt veroorzaakt door de inhoud van de blob, mislukt de functie elke keer dat de blob wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="726c3-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="726c3-148">Standaard de SDK-aanroepen een functie maximaal 5 maal voor een opgegeven blob.</span><span class="sxs-lookup"><span data-stu-id="726c3-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="726c3-149">Als de vijfde mislukt probeert, wordt een bericht met de SDK toegevoegd aan een wachtrij met de naam *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="726c3-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="726c3-150">Het maximum aantal nieuwe pogingen kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="726c3-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="726c3-151">Dezelfde [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) instelling wordt gebruikt voor de verwerking van verontreinigde blob en wachtrij verontreinigd bericht verwerking.</span><span class="sxs-lookup"><span data-stu-id="726c3-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="726c3-152">Bericht uit de wachtrij voor verontreinigde blobs is een JSON-object met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="726c3-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="726c3-153">FunctionId (in de notatie *{naam van een webtaak}*. Functies. *{Functienaam}*, bijvoorbeeld: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="726c3-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="726c3-154">BlobType ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="726c3-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="726c3-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="726c3-155">ContainerName</span></span>
* <span data-ttu-id="726c3-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="726c3-156">BlobName</span></span>
* <span data-ttu-id="726c3-157">ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="726c3-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="726c3-158">In het volgende codevoorbeeld wordt de `CopyBlob` functie heeft code die ervoor zorgt dat mislukken telkens wanneer deze wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="726c3-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="726c3-159">Nadat de SDK voor het maximum aantal nieuwe pogingen aangeroepen, een bericht in de wachtrij verontreinigd blob gemaakt en dat bericht is verwerkt door de `LogPoisonBlob` functie.</span><span class="sxs-lookup"><span data-stu-id="726c3-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="726c3-160">De SDK deserializes automatisch het JSON-bericht.</span><span class="sxs-lookup"><span data-stu-id="726c3-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="726c3-161">Hier volgt de `PoisonBlobMessage` klasse:</span><span class="sxs-lookup"><span data-stu-id="726c3-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="726c3-162"><a id="polling"></a>BLOB polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="726c3-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="726c3-163">De WebJobs SDK scant alle containers die zijn opgegeven door `BlobTrigger` kenmerken aan begin van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="726c3-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="726c3-164">In een grote opslagaccount deze scan kan enige tijd duren, zodat dit mogelijk even voordat nieuwe blobs zijn gevonden en `BlobTrigger` functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="726c3-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="726c3-165">Om te detecteren nieuwe of gewijzigde blobs na het starten van toepassingsservices, leest de SDK periodiek uit de logboeken van de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="726c3-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="726c3-166">De logboeken van de blob zijn gebufferd en alleen fysiek elke 10 minuten weggeschreven of dus, dus er aanzienlijke vertraging optreden nadat een blob wordt gemaakt of voordat de bijbehorende bijgewerkt `BlobTrigger` functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="726c3-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="726c3-167">Er is een uitzondering voor blobs die u met behulp van maakt de `Blob` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="726c3-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="726c3-168">Wanneer de WebJobs SDK een nieuwe blob maakt, wordt de nieuwe blob onmiddellijk doorgegeven aan een overeenkomende `BlobTrigger` functies.</span><span class="sxs-lookup"><span data-stu-id="726c3-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="726c3-169">Daarom hebt u een keten van blob-invoer en uitvoer, kan de SDK verwerken efficiënt.</span><span class="sxs-lookup"><span data-stu-id="726c3-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="726c3-170">Maar als u wilt een lage latentie functies voor blobs die zijn gemaakt of bijgewerkt op een andere manier voor het verwerken van uw blob uitgevoerd, wordt u aangeraden `QueueTrigger` plaats `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="726c3-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="726c3-171"><a id="receipts"></a>BLOB ontvangstbevestigingen</span><span class="sxs-lookup"><span data-stu-id="726c3-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="726c3-172">De WebJobs SDK zorgt ervoor dat er geen `BlobTrigger` functie wordt meer dan één keer aangeroepen voor de dezelfde nieuwe of bijgewerkte blob.</span><span class="sxs-lookup"><span data-stu-id="726c3-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="726c3-173">Dit wordt uitgevoerd door het onderhouden van *blob ontvangstbevestigingen* om te bepalen of een versie van de opgegeven blob is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="726c3-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="726c3-174">BLOB ontvangstbevestigingen worden opgeslagen in een container met de naam *webjobs-azure-hosts* in de Azure storage-account dat is opgegeven door de verbindingsreeks AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="726c3-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="726c3-175">De ontvangst van een blob heeft de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="726c3-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="726c3-176">De functie die voor de blob is aangeroepen ('*{naam van een webtaak}*. Functies. *{Functienaam}*', bijvoorbeeld: 'WebJob1.Functions.CopyBlob')</span><span class="sxs-lookup"><span data-stu-id="726c3-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="726c3-177">De containernaam</span><span class="sxs-lookup"><span data-stu-id="726c3-177">The container name</span></span>
* <span data-ttu-id="726c3-178">Het blobtype ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="726c3-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="726c3-179">De blob-naam</span><span class="sxs-lookup"><span data-stu-id="726c3-179">The blob name</span></span>
* <span data-ttu-id="726c3-180">De ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="726c3-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="726c3-181">Als u afdwingen opnieuw verwerken van een blob wilt, kunt u handmatig de ontvangst van de blob voor blob uit verwijderen de *webjobs-azure-hosts* container.</span><span class="sxs-lookup"><span data-stu-id="726c3-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="726c3-182"><a id="queues"></a>Verwante onderwerpen gedekt door het artikel wachtrijen</span><span class="sxs-lookup"><span data-stu-id="726c3-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="726c3-183">Scenario's die niet specifiek zijn voor blob-verwerking, Zie voor meer informatie over het afhandelen van de blob-verwerking geactiveerd door een wachtrijbericht of voor WebJobs SDK [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="726c3-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="726c3-184">Verwante onderwerpen in dit artikel omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="726c3-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="726c3-185">Async-functies</span><span class="sxs-lookup"><span data-stu-id="726c3-185">Async functions</span></span>
* <span data-ttu-id="726c3-186">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="726c3-186">Multiple instances</span></span>
* <span data-ttu-id="726c3-187">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="726c3-187">Graceful shutdown</span></span>
* <span data-ttu-id="726c3-188">Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="726c3-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="726c3-189">De SDK-verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="726c3-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="726c3-190">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="726c3-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="726c3-191">Configureer `MaxDequeueCount` voor het verwerken van verontreinigde blob.</span><span class="sxs-lookup"><span data-stu-id="726c3-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="726c3-192">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="726c3-192">Trigger a function manually</span></span>
* <span data-ttu-id="726c3-193">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="726c3-193">Write logs</span></span>

## <span data-ttu-id="726c3-194"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="726c3-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="726c3-195">Deze handleiding is opgegeven codevoorbeelden die laten hoe algemene scenario's zien voor het werken met Azure blobs afhandelen.</span><span class="sxs-lookup"><span data-stu-id="726c3-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="726c3-196">Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="726c3-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

