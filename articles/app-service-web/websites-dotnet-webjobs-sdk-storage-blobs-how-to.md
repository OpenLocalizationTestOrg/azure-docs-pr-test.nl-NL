---
title: aaaHow toouse Azure blob storage met Hallo WebJobs SDK
description: Meer informatie over hoe toouse Azure blob-opslag met Hallo WebJobs SDK. Een proces wordt geactiveerd wanneer een nieuwe blob wordt weergegeven in een container en verwerken van verontreinigde BLOB's.
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
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="8ff38-104">Hoe toouse Azure blob-opslag met Hallo WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="8ff38-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="8ff38-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8ff38-105">Overview</span></span>
<span data-ttu-id="8ff38-106">Deze handleiding bevat C# code voorbeelden die tonen hoe tootrigger een proces wanneer een Azure-blob is gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8ff38-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="8ff38-107">Hallo code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="8ff38-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="8ff38-108">Zie voor codevoorbeelden die laten zien hoe toocreate blobs [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8ff38-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="8ff38-109">Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md) of te[meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8ff38-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="8ff38-110"><a id="trigger"></a>Hoe tootrigger een functie wanneer een blob is gemaakt of bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="8ff38-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="8ff38-111">Deze sectie wordt beschreven hoe toouse hello `BlobTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8ff38-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="8ff38-112">Hallo WebJobs SDK scans logboek bestanden toowatch voor nieuwe of gewijzigde blobs.</span><span class="sxs-lookup"><span data-stu-id="8ff38-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="8ff38-113">Dit proces is niet realtime; een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat Hallo blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ff38-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="8ff38-114">Bovendien [opslag logboeken worden gemaakt op een 'best inspanningen'](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; er is geen garantie dat alle gebeurtenissen wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="8ff38-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="8ff38-115">Onder bepaalde omstandigheden kunnen een logboeken worden gemist.</span><span class="sxs-lookup"><span data-stu-id="8ff38-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="8ff38-116">Als de snelheid en betrouwbaarheid beperkingen Hallo van blob-triggers niet toegestaan voor uw toepassing zijn, Hallo aanbevolen methode toocreate een wachtrijbericht is wanneer u Hallo blob maken en Hallo gebruiken [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) in plaats van het kenmerk Hallo `BlobTrigger` -kenmerk op Hallo-functie die Hallo blob verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8ff38-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="8ff38-117">Één tijdelijke aanduiding voor blob-naam met de extensie</span><span class="sxs-lookup"><span data-stu-id="8ff38-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="8ff38-118">Hallo codevoorbeeld tekst blobs die worden weergegeven in kopieert Hallo *invoer* container toohello *uitvoer* container:</span><span class="sxs-lookup"><span data-stu-id="8ff38-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="8ff38-119">Hallo kenmerkconstructor tekenreeksparameter een die Hallo containernaam en een tijdelijke aanduiding voor Hallo blob-naam aangeeft.</span><span class="sxs-lookup"><span data-stu-id="8ff38-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="8ff38-120">In dit voorbeeld als de naam van een blob *Blob1.txt* wordt gemaakt in Hallo *invoer* -container, Hallo-functie maakt een blob met de naam *Blob1.txt* in Hallo *uitvoer*  container.</span><span class="sxs-lookup"><span data-stu-id="8ff38-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="8ff38-121">Zoals wordt weergegeven in het volgende codevoorbeeld hello, kunt u een bestandsnaampatroon opgeven met de Hallo blob naam tijdelijke:</span><span class="sxs-lookup"><span data-stu-id="8ff38-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="8ff38-122">Deze code alleen blobs die namen die beginnen met 'oorspronkelijke--' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8ff38-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="8ff38-123">Bijvoorbeeld: *oorspronkelijke Blob1.txt* in Hallo *invoer* container te worden gekopieerd*kopie Blob1.txt* in Hallo *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="8ff38-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="8ff38-124">Als u een bestandsnaampatroon toospecify voor blobnamen die accolades in Hallo naam hebben moet, dubbelklik Hallo accolades gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ff38-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="8ff38-125">Bijvoorbeeld, als u wilt dat toofind blobs in Hallo *installatiekopieën* container met namen als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ff38-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="8ff38-126">Gebruik deze optie voor het patroon:</span><span class="sxs-lookup"><span data-stu-id="8ff38-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="8ff38-127">In voorbeeld Hallo Hallo *naam* aanduidingswaarde zou worden *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="8ff38-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="8ff38-128">Afzonderlijke blob-naam en extensie voor tijdelijke aanduidingen</span><span class="sxs-lookup"><span data-stu-id="8ff38-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="8ff38-129">Hallo volgende code voorbeeld wijzigt Hallo bestandsextensie als blobs die worden weergegeven in Hallo gekopieerd *invoer* container toohello *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="8ff38-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="8ff38-130">Hallo code registreert Hallo extensie Hallo *invoer* blob en Hiermee stelt u de extensie Hallo Hallo *uitvoer* blob te*.txt*.</span><span class="sxs-lookup"><span data-stu-id="8ff38-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <span data-ttu-id="8ff38-131"><a id="types"></a>Typen dat kunt u tooblobs binden</span><span class="sxs-lookup"><span data-stu-id="8ff38-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="8ff38-132">U kunt Hallo `BlobTrigger` -kenmerk op Hallo volgende typen:</span><span class="sxs-lookup"><span data-stu-id="8ff38-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

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
* <span data-ttu-id="8ff38-133">Andere typen gedeserialiseerd door [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="8ff38-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="8ff38-134">Als u wilt dat toowork rechtstreeks met hello Azure storage-account, kunt u ook toevoegen een `CloudStorageAccount` parameter toohello methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="8ff38-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="8ff38-135">Zie voor voorbeelden Hallo [blob-code van de binding in Hallo sdk van azure webjobs opslagplaats op GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8ff38-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="8ff38-136"><a id="string"></a>Tekst blob-inhoud opvragen door binding toostring</span><span class="sxs-lookup"><span data-stu-id="8ff38-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="8ff38-137">Als tekst blobs worden verwacht, `BlobTrigger` kunnen worden toegepast tooa `string` parameter.</span><span class="sxs-lookup"><span data-stu-id="8ff38-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="8ff38-138">Hallo volgende codevoorbeeld wordt gebonden een blob tekst tooa `string` parameter met de naam `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="8ff38-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="8ff38-139">Hallo-functie maakt gebruik van die inhoud parameter toowrite Hallo van Hallo blob toohello WebJobs SDK-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8ff38-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="8ff38-140"><a id="icbsb"></a>Ophalen van blob-inhoud geserialiseerd met behulp van ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="8ff38-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="8ff38-141">Hallo volgende codevoorbeeld maakt gebruik van een klasse die implementeert `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind een blob-toohello kenmerk `WebImage` type.</span><span class="sxs-lookup"><span data-stu-id="8ff38-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

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

<span data-ttu-id="8ff38-142">Hallo `WebImage` binding code is opgegeven een `WebImageBinder` klasse die is afgeleid van `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="8ff38-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="8ff38-143">Hallo blobpad ophalen voor activering van blob Hallo</span><span class="sxs-lookup"><span data-stu-id="8ff38-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="8ff38-144">Hallo-containernaam tooget en blob-naam van de blob Hallo die Hallo-functie is geactiveerd bevatten een `blobTrigger` tekenreeksparameter in Hallo functiehandtekening.</span><span class="sxs-lookup"><span data-stu-id="8ff38-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="8ff38-145"><a id="poison"></a>Hoe toohandle poison blobs</span><span class="sxs-lookup"><span data-stu-id="8ff38-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="8ff38-146">Wanneer een `BlobTrigger` functie mislukt, Hallo SDK aangeroepen opnieuw, indien Hallo-fout is veroorzaakt door een tijdelijke fout.</span><span class="sxs-lookup"><span data-stu-id="8ff38-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="8ff38-147">Als Hallo fout wordt veroorzaakt door Hallo inhoud van de blob hello, mislukt de Hallo functie telkens wanneer wordt geprobeerd tooprocess Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="8ff38-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="8ff38-148">Standaard-Hallo SDK een functie van too5 tijden aanroepen voor een opgegeven blob.</span><span class="sxs-lookup"><span data-stu-id="8ff38-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="8ff38-149">Als de vijfde probeer Hallo mislukt, Hallo SDK wordt toegevoegd een berichtenwachtrij tooa met de naam *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="8ff38-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="8ff38-150">maximum aantal pogingen Hallo kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8ff38-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="8ff38-151">Hallo dezelfde [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) instelling wordt gebruikt voor de verwerking van verontreinigde blob en wachtrij verontreinigd bericht verwerking.</span><span class="sxs-lookup"><span data-stu-id="8ff38-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="8ff38-152">Hallo-bericht van wachtrij voor verontreinigde blobs is een JSON-object met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8ff38-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="8ff38-153">FunctionId (Hallo indeling *{naam van een webtaak}*. Functies. *{Functienaam}*, bijvoorbeeld: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="8ff38-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="8ff38-154">BlobType ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="8ff38-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="8ff38-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="8ff38-155">ContainerName</span></span>
* <span data-ttu-id="8ff38-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="8ff38-156">BlobName</span></span>
* <span data-ttu-id="8ff38-157">ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="8ff38-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="8ff38-158">In de volgende Hallo code voorbeeld hello `CopyBlob` functie heeft code die ervoor zorgt toofail dat telkens wanneer deze wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8ff38-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="8ff38-159">Nadat Hallo SDK voor Hallo kunt u het maximum aantal nieuwe pogingen aangeroepen, een bericht op Hallo verontreinigd blob wachtrij is gemaakt en dat bericht is verwerkt door Hallo `LogPoisonBlob` functie.</span><span class="sxs-lookup"><span data-stu-id="8ff38-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="8ff38-160">Hallo SDK deserializes automatisch JSON het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="8ff38-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="8ff38-161">Hier volgt Hallo `PoisonBlobMessage` klasse:</span><span class="sxs-lookup"><span data-stu-id="8ff38-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="8ff38-162"><a id="polling"></a>BLOB polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="8ff38-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="8ff38-163">Hallo WebJobs SDK scant alle containers die zijn opgegeven door `BlobTrigger` kenmerken aan begin van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ff38-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="8ff38-164">In een grote opslagaccount deze scan kan enige tijd duren, zodat dit mogelijk even voordat nieuwe blobs zijn gevonden en `BlobTrigger` functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ff38-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="8ff38-165">toodetect blobs nieuw of gewijzigd na toepassing start, Hallo die SDK periodiek uit Hallo blob-opslag leest Logboeken.</span><span class="sxs-lookup"><span data-stu-id="8ff38-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="8ff38-166">Hallo blob logboeken zijn gebufferd en alleen fysiek elke 10 minuten weggeschreven of dus, dus er aanzienlijke vertraging optreden nadat een blob wordt gemaakt of voordat het Hallo overeenkomt bijgewerkt `BlobTrigger` functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ff38-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="8ff38-167">Er is een uitzondering voor blobs die u maakt met behulp van Hallo `Blob` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8ff38-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="8ff38-168">Als Hallo WebJobs SDK wordt een nieuwe blob gemaakt, wordt de nieuwe blob Hallo onmiddellijk doorgegeven tooany overeenkomende `BlobTrigger` functies.</span><span class="sxs-lookup"><span data-stu-id="8ff38-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="8ff38-169">Daarom hebt u een keten van blob-invoer en uitvoer, kan Hallo SDK verwerken efficiënt.</span><span class="sxs-lookup"><span data-stu-id="8ff38-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="8ff38-170">Maar als u wilt een lage latentie functies voor blobs die zijn gemaakt of bijgewerkt op een andere manier voor het verwerken van uw blob uitgevoerd, wordt u aangeraden `QueueTrigger` plaats `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="8ff38-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="8ff38-171"><a id="receipts"></a>BLOB ontvangstbevestigingen</span><span class="sxs-lookup"><span data-stu-id="8ff38-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="8ff38-172">Hallo WebJobs SDK zorgt ervoor dat er geen `BlobTrigger` functie wordt aangeroepen meer dan één keer voor Hallo dezelfde nieuw of bijgewerkt blob.</span><span class="sxs-lookup"><span data-stu-id="8ff38-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="8ff38-173">Dit wordt uitgevoerd door het onderhouden van *blob ontvangstbevestigingen* in volgorde toodetermine als een versie van de opgegeven blob is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8ff38-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="8ff38-174">BLOB ontvangstbevestigingen worden opgeslagen in een container met de naam *webjobs-azure-hosts* in hello Azure storage-account is opgegeven door Hallo AzureWebJobsStorage verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="8ff38-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="8ff38-175">De ontvangst van een blob heeft Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8ff38-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="8ff38-176">de functie die is aangeroepen voor blob Hallo Hallo ('*{naam van een webtaak}*. Functies. *{Functienaam}*', bijvoorbeeld: 'WebJob1.Functions.CopyBlob')</span><span class="sxs-lookup"><span data-stu-id="8ff38-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="8ff38-177">Hallo-containernaam</span><span class="sxs-lookup"><span data-stu-id="8ff38-177">hello container name</span></span>
* <span data-ttu-id="8ff38-178">Hallo blobtype ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="8ff38-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="8ff38-179">Hallo blob-naam</span><span class="sxs-lookup"><span data-stu-id="8ff38-179">hello blob name</span></span>
* <span data-ttu-id="8ff38-180">Hallo ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="8ff38-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="8ff38-181">Als u tooforce opnieuw verwerken van een blob wilt, kunt u Hallo blob ontvangst voor blob handmatig verwijderen van Hallo *webjobs-azure-hosts* container.</span><span class="sxs-lookup"><span data-stu-id="8ff38-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="8ff38-182"><a id="queues"></a>Verwante onderwerpen Hallo wachtrijen artikel vallen</span><span class="sxs-lookup"><span data-stu-id="8ff38-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="8ff38-183">Zie voor informatie over hoe toohandle blob verwerking geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tooblob verwerking, [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8ff38-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="8ff38-184">Verwante onderwerpen in dit artikel zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8ff38-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="8ff38-185">Async-functies</span><span class="sxs-lookup"><span data-stu-id="8ff38-185">Async functions</span></span>
* <span data-ttu-id="8ff38-186">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="8ff38-186">Multiple instances</span></span>
* <span data-ttu-id="8ff38-187">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="8ff38-187">Graceful shutdown</span></span>
* <span data-ttu-id="8ff38-188">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="8ff38-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="8ff38-189">Hallo SDK verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="8ff38-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="8ff38-190">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="8ff38-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="8ff38-191">Configureer `MaxDequeueCount` voor het verwerken van verontreinigde blob.</span><span class="sxs-lookup"><span data-stu-id="8ff38-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="8ff38-192">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="8ff38-192">Trigger a function manually</span></span>
* <span data-ttu-id="8ff38-193">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="8ff38-193">Write logs</span></span>

## <span data-ttu-id="8ff38-194"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ff38-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="8ff38-195">Deze handleiding is opgegeven codevoorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="8ff38-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="8ff38-196">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="8ff38-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

