---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (webtaak projecten) | Microsoft Docs
description: Hoe tooget gestart met behulp van Blob-opslag in een project webtaak nadat u verbinding tooan Azure-opslag met Visual Studio hebt verbonden services.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="d46d1-103">Aan de slag met Azure Blob storage en Visual Studio verbonden services (webtaak projecten)</span><span class="sxs-lookup"><span data-stu-id="d46d1-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d46d1-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d46d1-104">Overview</span></span>
<span data-ttu-id="d46d1-105">Dit artikel vindt u C# code voorbeelden die tonen hoe tootrigger een proces wanneer een Azure-blob is gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d46d1-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="d46d1-106">Hallo-codevoorbeelden gebruiken Hallo [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="d46d1-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="d46d1-107">Wanneer u een project storage account tooa webtaak toevoegen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster Hallo juiste Azure Storage NuGet-pakket is geïnstalleerd, Hallo juiste .NET verwijzingen worden toegevoegd toohello Project en verbindingsreeksen voor Hallo storage-account worden bijgewerkt in Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="d46d1-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="d46d1-108">Hoe tootrigger een functie wanneer een blob is gemaakt of bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="d46d1-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="d46d1-109">Deze sectie wordt beschreven hoe toouse hello **BlobTrigger** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d46d1-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="d46d1-110">**Opmerking:** Hallo WebJobs SDK scans logboek bestanden toowatch voor nieuwe of gewijzigde blobs.</span><span class="sxs-lookup"><span data-stu-id="d46d1-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="d46d1-111">Dit proces is inherent langzaam; een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat Hallo blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d46d1-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="d46d1-112">Als uw toepassing onmiddellijk tooprocess blobs moet, Hallo aanbevolen methode toocreate een wachtrijbericht is wanneer u Hallo blob maken en Hallo gebruiken [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) kenmerk in plaats van Hallo **BlobTrigger** -kenmerk op Hallo-functie die Hallo blob verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d46d1-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="d46d1-113">Één tijdelijke aanduiding voor blob-naam met de extensie</span><span class="sxs-lookup"><span data-stu-id="d46d1-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="d46d1-114">Hallo codevoorbeeld tekst blobs die worden weergegeven in kopieert Hallo *invoer* container toohello *uitvoer* container:</span><span class="sxs-lookup"><span data-stu-id="d46d1-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="d46d1-115">Hallo kenmerkconstructor tekenreeksparameter een die Hallo containernaam en een tijdelijke aanduiding voor Hallo blob-naam aangeeft.</span><span class="sxs-lookup"><span data-stu-id="d46d1-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="d46d1-116">In dit voorbeeld als de naam van een blob *Blob1.txt* wordt gemaakt in Hallo *invoer* -container, Hallo-functie maakt een blob met de naam *Blob1.txt* in Hallo *uitvoer*  container.</span><span class="sxs-lookup"><span data-stu-id="d46d1-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="d46d1-117">Zoals wordt weergegeven in het volgende codevoorbeeld hello, kunt u een bestandsnaampatroon opgeven met de Hallo blob naam tijdelijke:</span><span class="sxs-lookup"><span data-stu-id="d46d1-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="d46d1-118">Deze code alleen blobs die namen die beginnen met 'oorspronkelijke--' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d46d1-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="d46d1-119">Bijvoorbeeld: *oorspronkelijke Blob1.txt* in Hallo *invoer* container te worden gekopieerd*kopie Blob1.txt* in Hallo *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="d46d1-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="d46d1-120">Als u een bestandsnaampatroon toospecify voor blobnamen die accolades in Hallo naam hebben moet, dubbelklik Hallo accolades gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d46d1-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="d46d1-121">Bijvoorbeeld, als u wilt dat toofind blobs in Hallo *installatiekopieën* container met namen als volgt:</span><span class="sxs-lookup"><span data-stu-id="d46d1-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="d46d1-122">Gebruik deze optie voor het patroon:</span><span class="sxs-lookup"><span data-stu-id="d46d1-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="d46d1-123">In voorbeeld Hallo Hallo *naam* aanduidingswaarde zou worden *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="d46d1-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="d46d1-124">Afzonderlijke blob-naam en extensie voor tijdelijke aanduidingen</span><span class="sxs-lookup"><span data-stu-id="d46d1-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="d46d1-125">Hallo volgende code voorbeeld wijzigt Hallo bestandsextensie als blobs die worden weergegeven in Hallo gekopieerd *invoer* container toohello *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="d46d1-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="d46d1-126">Hallo code registreert Hallo extensie Hallo *invoer* blob en Hiermee stelt u de extensie Hallo Hallo *uitvoer* blob te*.txt*.</span><span class="sxs-lookup"><span data-stu-id="d46d1-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="d46d1-127">Typen dat kunt u tooblobs binden</span><span class="sxs-lookup"><span data-stu-id="d46d1-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="d46d1-128">U kunt Hallo **BlobTrigger** -kenmerk op Hallo volgende typen:</span><span class="sxs-lookup"><span data-stu-id="d46d1-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="d46d1-129">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="d46d1-129">**string**</span></span>
* <span data-ttu-id="d46d1-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="d46d1-130">**TextReader**</span></span>
* <span data-ttu-id="d46d1-131">**Stroom**</span><span class="sxs-lookup"><span data-stu-id="d46d1-131">**Stream**</span></span>
* <span data-ttu-id="d46d1-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="d46d1-132">**ICloudBlob**</span></span>
* <span data-ttu-id="d46d1-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="d46d1-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="d46d1-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="d46d1-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="d46d1-135">Andere typen gedeserialiseerd door [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="d46d1-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="d46d1-136">Als u wilt dat toowork rechtstreeks met hello Azure storage-account, kunt u ook toevoegen een **CloudStorageAccount** parameter toohello methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="d46d1-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="d46d1-137">Tekst blob-inhoud opvragen door binding toostring</span><span class="sxs-lookup"><span data-stu-id="d46d1-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="d46d1-138">Als tekst blobs worden verwacht, **BlobTrigger** kunnen worden toegepast tooa **tekenreeks** parameter.</span><span class="sxs-lookup"><span data-stu-id="d46d1-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="d46d1-139">Hallo volgende codevoorbeeld wordt gebonden een blob tekst tooa **tekenreeks** parameter met de naam **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="d46d1-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="d46d1-140">Hallo-functie maakt gebruik van die inhoud parameter toowrite Hallo van Hallo blob toohello WebJobs SDK-dashboard.</span><span class="sxs-lookup"><span data-stu-id="d46d1-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="d46d1-141">Ophalen van blob-inhoud geserialiseerd met behulp van ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="d46d1-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="d46d1-142">Hallo volgende codevoorbeeld maakt gebruik van een klasse die implementeert **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** kenmerk toobind een blob-toohello **WebImage** type.</span><span class="sxs-lookup"><span data-stu-id="d46d1-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="d46d1-143">Hallo **WebImage** binding code is opgegeven een **WebImageBinder** klasse die is afgeleid van **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="d46d1-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="d46d1-144">Hoe toohandle poison blobs</span><span class="sxs-lookup"><span data-stu-id="d46d1-144">How toohandle poison blobs</span></span>
<span data-ttu-id="d46d1-145">Wanneer een **BlobTrigger** functie mislukt, Hallo SDK aangeroepen opnieuw, indien Hallo-fout is veroorzaakt door een tijdelijke fout.</span><span class="sxs-lookup"><span data-stu-id="d46d1-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="d46d1-146">Als Hallo fout wordt veroorzaakt door Hallo inhoud van de blob hello, mislukt de Hallo functie telkens wanneer wordt geprobeerd tooprocess Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="d46d1-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="d46d1-147">Standaard-Hallo SDK een functie van too5 tijden aanroepen voor een opgegeven blob.</span><span class="sxs-lookup"><span data-stu-id="d46d1-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="d46d1-148">Als de vijfde probeer Hallo mislukt, Hallo SDK wordt toegevoegd een berichtenwachtrij tooa met de naam *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="d46d1-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="d46d1-149">maximum aantal pogingen Hallo kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d46d1-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="d46d1-150">Hallo dezelfde [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) instelling wordt gebruikt voor de verwerking van verontreinigde blob en wachtrij verontreinigd bericht verwerking.</span><span class="sxs-lookup"><span data-stu-id="d46d1-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="d46d1-151">Hallo-bericht van wachtrij voor verontreinigde blobs is een JSON-object met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d46d1-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="d46d1-152">FunctionId (Hallo indeling *{naam van een webtaak}*. Functies. *{Functienaam}*, bijvoorbeeld: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="d46d1-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="d46d1-153">BlobType ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="d46d1-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="d46d1-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="d46d1-154">ContainerName</span></span>
* <span data-ttu-id="d46d1-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="d46d1-155">BlobName</span></span>
* <span data-ttu-id="d46d1-156">ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="d46d1-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="d46d1-157">In de volgende Hallo code voorbeeld hello **CopyBlob** functie heeft code die ervoor zorgt toofail dat telkens wanneer deze wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d46d1-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="d46d1-158">Nadat Hallo SDK voor Hallo kunt u het maximum aantal nieuwe pogingen aangeroepen, een bericht op Hallo verontreinigd blob wachtrij is gemaakt en dat bericht is verwerkt door Hallo **LogPoisonBlob** functie.</span><span class="sxs-lookup"><span data-stu-id="d46d1-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="d46d1-159">Hallo SDK deserializes automatisch JSON het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="d46d1-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="d46d1-160">Hier volgt Hallo **PoisonBlobMessage** klasse:</span><span class="sxs-lookup"><span data-stu-id="d46d1-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="d46d1-161">BLOB polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="d46d1-161">Blob polling algorithm</span></span>
<span data-ttu-id="d46d1-162">Hallo WebJobs SDK scant alle containers die zijn opgegeven door **BlobTrigger** kenmerken aan begin van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d46d1-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="d46d1-163">In een grote opslagaccount deze scan kan enige tijd duren, zodat dit mogelijk even voordat nieuwe blobs zijn gevonden en **BlobTrigger** functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d46d1-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="d46d1-164">toodetect blobs nieuw of gewijzigd na toepassing start, Hallo die SDK periodiek uit Hallo blob-opslag leest Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d46d1-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="d46d1-165">Hallo blob logboeken zijn gebufferd en alleen fysiek elke 10 minuten weggeschreven of dus, dus er aanzienlijke vertraging optreden nadat een blob wordt gemaakt of voordat het Hallo overeenkomt bijgewerkt **BlobTrigger** functie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d46d1-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="d46d1-166">Er is een uitzondering voor blobs die u maakt met behulp van Hallo **Blob** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d46d1-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="d46d1-167">Als Hallo WebJobs SDK wordt een nieuwe blob gemaakt, wordt de nieuwe blob Hallo onmiddellijk doorgegeven tooany overeenkomende **BlobTrigger** functies.</span><span class="sxs-lookup"><span data-stu-id="d46d1-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="d46d1-168">Daarom hebt u een keten van blob-invoer en uitvoer, kan Hallo SDK verwerken efficiënt.</span><span class="sxs-lookup"><span data-stu-id="d46d1-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="d46d1-169">Maar als u wilt een lage latentie functies voor blobs die zijn gemaakt of bijgewerkt op een andere manier voor het verwerken van uw blob uitgevoerd, wordt u aangeraden **QueueTrigger** plaats **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="d46d1-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="d46d1-170">BLOB ontvangstbevestigingen</span><span class="sxs-lookup"><span data-stu-id="d46d1-170">Blob receipts</span></span>
<span data-ttu-id="d46d1-171">Hallo WebJobs SDK zorgt ervoor dat er geen **BlobTrigger** functie wordt aangeroepen meer dan één keer voor Hallo dezelfde nieuw of bijgewerkt blob.</span><span class="sxs-lookup"><span data-stu-id="d46d1-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="d46d1-172">Dit wordt uitgevoerd door het onderhouden van *blob ontvangstbevestigingen* in volgorde toodetermine als een versie van de opgegeven blob is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d46d1-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="d46d1-173">BLOB ontvangstbevestigingen worden opgeslagen in een container met de naam *webjobs-azure-hosts* in hello Azure storage-account is opgegeven door Hallo AzureWebJobsStorage verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="d46d1-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="d46d1-174">De ontvangst van een blob heeft Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="d46d1-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="d46d1-175">de functie die is aangeroepen voor blob Hallo Hallo ('*{naam van een webtaak}*. Functies. *{Functienaam}*', bijvoorbeeld: 'WebJob1.Functions.CopyBlob')</span><span class="sxs-lookup"><span data-stu-id="d46d1-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="d46d1-176">Hallo-containernaam</span><span class="sxs-lookup"><span data-stu-id="d46d1-176">hello container name</span></span>
* <span data-ttu-id="d46d1-177">Hallo blobtype ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="d46d1-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="d46d1-178">Hallo blob-naam</span><span class="sxs-lookup"><span data-stu-id="d46d1-178">hello blob name</span></span>
* <span data-ttu-id="d46d1-179">Hallo ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="d46d1-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="d46d1-180">Als u tooforce opnieuw verwerken van een blob wilt, kunt u Hallo blob ontvangst voor blob handmatig verwijderen van Hallo *webjobs-azure-hosts* container.</span><span class="sxs-lookup"><span data-stu-id="d46d1-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="d46d1-181">Verwante onderwerpen Hallo wachtrijen artikel vallen</span><span class="sxs-lookup"><span data-stu-id="d46d1-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="d46d1-182">Zie voor informatie over hoe toohandle blob verwerking geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tooblob verwerking, [hoe toouse Azure queue storage Hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d46d1-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="d46d1-183">Verwante onderwerpen in dit artikel zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d46d1-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="d46d1-184">Async-functies</span><span class="sxs-lookup"><span data-stu-id="d46d1-184">Async functions</span></span>
* <span data-ttu-id="d46d1-185">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="d46d1-185">Multiple instances</span></span>
* <span data-ttu-id="d46d1-186">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="d46d1-186">Graceful shutdown</span></span>
* <span data-ttu-id="d46d1-187">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="d46d1-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="d46d1-188">Hallo SDK verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="d46d1-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="d46d1-189">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="d46d1-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="d46d1-190">Configureer **MaxDequeueCount** voor het verwerken van verontreinigde blob.</span><span class="sxs-lookup"><span data-stu-id="d46d1-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="d46d1-191">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="d46d1-191">Trigger a function manually</span></span>
* <span data-ttu-id="d46d1-192">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="d46d1-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="d46d1-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d46d1-193">Next steps</span></span>
<span data-ttu-id="d46d1-194">In dit artikel is opgegeven codevoorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="d46d1-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="d46d1-195">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d46d1-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

