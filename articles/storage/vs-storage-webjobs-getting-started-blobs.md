---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (webtaak projecten) | Microsoft Docs
description: Hoe tooget gestart met behulp van Blob-opslag in een project webtaak nadat u verbinding tooan Azure-opslag met Visual Studio hebt verbonden services.
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Aan de slag met Azure Blob storage en Visual Studio verbonden services (webtaak projecten)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Dit artikel vindt u C# code voorbeelden die tonen hoe tootrigger een proces wanneer een Azure-blob is gemaakt of bijgewerkt. Hallo-codevoorbeelden gebruiken Hallo [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versie 1.x. Wanneer u een project storage account tooa webtaak toevoegen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster Hallo juiste Azure Storage NuGet-pakket is geïnstalleerd, Hallo juiste .NET verwijzingen worden toegevoegd toohello Project en verbindingsreeksen voor Hallo storage-account worden bijgewerkt in Hallo App.config-bestand.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Hoe tootrigger een functie wanneer een blob is gemaakt of bijgewerkt
Deze sectie wordt beschreven hoe toouse hello **BlobTrigger** kenmerk.

 **Opmerking:** Hallo WebJobs SDK scans logboek bestanden toowatch voor nieuwe of gewijzigde blobs. Dit proces is inherent langzaam; een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat Hallo blob is gemaakt.  Als uw toepassing onmiddellijk tooprocess blobs moet, Hallo aanbevolen methode toocreate een wachtrijbericht is wanneer u Hallo blob maken en Hallo gebruiken [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) kenmerk in plaats van Hallo **BlobTrigger** -kenmerk op Hallo-functie die Hallo blob verwerkt.

### <a name="single-placeholder-for-blob-name-with-extension"></a>Één tijdelijke aanduiding voor blob-naam met de extensie
Hallo codevoorbeeld tekst blobs die worden weergegeven in kopieert Hallo *invoer* container toohello *uitvoer* container:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Hallo kenmerkconstructor tekenreeksparameter een die Hallo containernaam en een tijdelijke aanduiding voor Hallo blob-naam aangeeft. In dit voorbeeld als de naam van een blob *Blob1.txt* wordt gemaakt in Hallo *invoer* -container, Hallo-functie maakt een blob met de naam *Blob1.txt* in Hallo *uitvoer*  container.

Zoals wordt weergegeven in het volgende codevoorbeeld hello, kunt u een bestandsnaampatroon opgeven met de Hallo blob naam tijdelijke:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Deze code alleen blobs die namen die beginnen met 'oorspronkelijke--' hebt opgehaald. Bijvoorbeeld: *oorspronkelijke Blob1.txt* in Hallo *invoer* container te worden gekopieerd*kopie Blob1.txt* in Hallo *uitvoer* container.

Als u een bestandsnaampatroon toospecify voor blobnamen die accolades in Hallo naam hebben moet, dubbelklik Hallo accolades gebruiken. Bijvoorbeeld, als u wilt dat toofind blobs in Hallo *installatiekopieën* container met namen als volgt:

        {20140101}-soundfile.mp3

Gebruik deze optie voor het patroon:

        images/{{20140101}}-{name}

In voorbeeld Hallo Hallo *naam* aanduidingswaarde zou worden *soundfile.mp3*.

### <a name="separate-blob-name-and-extension-placeholders"></a>Afzonderlijke blob-naam en extensie voor tijdelijke aanduidingen
Hallo volgende code voorbeeld wijzigt Hallo bestandsextensie als blobs die worden weergegeven in Hallo gekopieerd *invoer* container toohello *uitvoer* container. Hallo code registreert Hallo extensie Hallo *invoer* blob en Hiermee stelt u de extensie Hallo Hallo *uitvoer* blob te*.txt*.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Typen dat kunt u tooblobs binden
U kunt Hallo **BlobTrigger** -kenmerk op Hallo volgende typen:

* **tekenreeks**
* **TextReader**
* **Stroom**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Andere typen gedeserialiseerd door [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Als u wilt dat toowork rechtstreeks met hello Azure storage-account, kunt u ook toevoegen een **CloudStorageAccount** parameter toohello methodehandtekening.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Tekst blob-inhoud opvragen door binding toostring
Als tekst blobs worden verwacht, **BlobTrigger** kunnen worden toegepast tooa **tekenreeks** parameter. Hallo volgende codevoorbeeld wordt gebonden een blob tekst tooa **tekenreeks** parameter met de naam **logMessage**. Hallo-functie maakt gebruik van die inhoud parameter toowrite Hallo van Hallo blob toohello WebJobs SDK-dashboard.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Ophalen van blob-inhoud geserialiseerd met behulp van ICloudBlobStreamBinder
Hallo volgende codevoorbeeld maakt gebruik van een klasse die implementeert **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** kenmerk toobind een blob-toohello **WebImage** type.

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

Hallo **WebImage** binding code is opgegeven een **WebImageBinder** klasse die is afgeleid van **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Hoe toohandle poison blobs
Wanneer een **BlobTrigger** functie mislukt, Hallo SDK aangeroepen opnieuw, indien Hallo-fout is veroorzaakt door een tijdelijke fout. Als Hallo fout wordt veroorzaakt door Hallo inhoud van de blob hello, mislukt de Hallo functie telkens wanneer wordt geprobeerd tooprocess Hallo blob. Standaard-Hallo SDK een functie van too5 tijden aanroepen voor een opgegeven blob. Als de vijfde probeer Hallo mislukt, Hallo SDK wordt toegevoegd een berichtenwachtrij tooa met de naam *webjobs-blobtrigger-poison*.

maximum aantal pogingen Hallo kan worden geconfigureerd. Hallo dezelfde [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) instelling wordt gebruikt voor de verwerking van verontreinigde blob en wachtrij verontreinigd bericht verwerking.

Hallo-bericht van wachtrij voor verontreinigde blobs is een JSON-object met Hallo volgende eigenschappen:

* FunctionId (Hallo indeling *{naam van een webtaak}*. Functies. *{Functienaam}*, bijvoorbeeld: WebJob1.Functions.CopyBlob)
* BlobType ('BlockBlob' of 'PageBlob')
* ContainerName
* BlobName
* ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

In de volgende Hallo code voorbeeld hello **CopyBlob** functie heeft code die ervoor zorgt toofail dat telkens wanneer deze wordt aangeroepen. Nadat Hallo SDK voor Hallo kunt u het maximum aantal nieuwe pogingen aangeroepen, een bericht op Hallo verontreinigd blob wachtrij is gemaakt en dat bericht is verwerkt door Hallo **LogPoisonBlob** functie.

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

Hallo SDK deserializes automatisch JSON het Hallo-bericht. Hier volgt Hallo **PoisonBlobMessage** klasse:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>BLOB polling-algoritme
Hallo WebJobs SDK scant alle containers die zijn opgegeven door **BlobTrigger** kenmerken aan begin van de toepassing. In een grote opslagaccount deze scan kan enige tijd duren, zodat dit mogelijk even voordat nieuwe blobs zijn gevonden en **BlobTrigger** functies worden uitgevoerd.

toodetect blobs nieuw of gewijzigd na toepassing start, Hallo die SDK periodiek uit Hallo blob-opslag leest Logboeken. Hallo blob logboeken zijn gebufferd en alleen fysiek elke 10 minuten weggeschreven of dus, dus er aanzienlijke vertraging optreden nadat een blob wordt gemaakt of voordat het Hallo overeenkomt bijgewerkt **BlobTrigger** functie wordt uitgevoerd.

Er is een uitzondering voor blobs die u maakt met behulp van Hallo **Blob** kenmerk. Als Hallo WebJobs SDK wordt een nieuwe blob gemaakt, wordt de nieuwe blob Hallo onmiddellijk doorgegeven tooany overeenkomende **BlobTrigger** functies. Daarom hebt u een keten van blob-invoer en uitvoer, kan Hallo SDK verwerken efficiënt. Maar als u wilt een lage latentie functies voor blobs die zijn gemaakt of bijgewerkt op een andere manier voor het verwerken van uw blob uitgevoerd, wordt u aangeraden **QueueTrigger** plaats **BlobTrigger**.

### <a name="blob-receipts"></a>BLOB ontvangstbevestigingen
Hallo WebJobs SDK zorgt ervoor dat er geen **BlobTrigger** functie wordt aangeroepen meer dan één keer voor Hallo dezelfde nieuw of bijgewerkt blob. Dit wordt uitgevoerd door het onderhouden van *blob ontvangstbevestigingen* in volgorde toodetermine als een versie van de opgegeven blob is verwerkt.

BLOB ontvangstbevestigingen worden opgeslagen in een container met de naam *webjobs-azure-hosts* in hello Azure storage-account is opgegeven door Hallo AzureWebJobsStorage verbindingsreeks. De ontvangst van een blob heeft Hallo volgende informatie:

* de functie die is aangeroepen voor blob Hallo Hallo ('*{naam van een webtaak}*. Functies. *{Functienaam}*', bijvoorbeeld: 'WebJob1.Functions.CopyBlob')
* Hallo-containernaam
* Hallo blobtype ('BlockBlob' of 'PageBlob')
* Hallo blob-naam
* Hallo ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

Als u tooforce opnieuw verwerken van een blob wilt, kunt u Hallo blob ontvangst voor blob handmatig verwijderen van Hallo *webjobs-azure-hosts* container.

## <a name="related-topics-covered-by-hello-queues-article"></a>Verwante onderwerpen Hallo wachtrijen artikel vallen
Zie voor informatie over hoe toohandle blob verwerking geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tooblob verwerking, [hoe toouse Azure queue storage Hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Verwante onderwerpen in dit artikel zijn Hallo volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
* Hallo SDK verbindingsreeksen in code instellen.
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Configureer **MaxDequeueCount** voor het verwerken van verontreinigde blob.
* Een functie handmatig activeren
* Schrijven Logboeken

## <a name="next-steps"></a>Volgende stappen
In dit artikel is opgegeven codevoorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure blobs. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

