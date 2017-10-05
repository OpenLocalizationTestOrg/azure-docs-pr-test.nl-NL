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
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a>Azure Blob-opslag gebruiken met de WebJobs SDK
## <a name="overview"></a>Overzicht
Deze handleiding bevat C#-codevoorbeelden die laten hoe een proces wordt geactiveerd zien wanneer een Azure-blob is gemaakt of bijgewerkt. De code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.

Zie voor codevoorbeelden die laten hoe zien u blobs, [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md) of [meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Het activeren van een functie wanneer een blob is gemaakt of bijgewerkt
Deze sectie wordt beschreven hoe u de `BlobTrigger` kenmerk. 

> [!NOTE]
> De WebJobs SDK scant logboekbestanden moeten worden gecontroleerd op nieuwe of gewijzigde blobs. Dit proces is niet realtime; een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat de blob is gemaakt. Bovendien [opslag logboeken worden gemaakt op een 'best inspanningen'](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; er is geen garantie dat alle gebeurtenissen wordt vastgelegd. Onder bepaalde omstandigheden kunnen een logboeken worden gemist. Als de beperkingen snelheid en betrouwbaarheid van blob-triggers niet toegestaan voor uw toepassing zijn, de aanbevolen methode is het maken van een wachtrijbericht wanneer u de blob maken en gebruiken de [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) kenmerk in plaats van de `BlobTrigger` kenmerk voor de functie die de blob wordt verwerkt.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Één tijdelijke aanduiding voor blob-naam met de extensie
Het volgende codevoorbeeld kopieert tekst blobs die worden weergegeven in de *invoer* container voor de *uitvoer* container:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

De kenmerkconstructor tekenreeksparameter een waarin de containernaam van de en een tijdelijke aanduiding voor de blob-naam opgegeven. In dit voorbeeld als de naam van een blob *Blob1.txt* wordt gemaakt in de *invoer* -container, de functie maakt een blob met de naam *Blob1.txt* in de *uitvoer* container. 

Zoals wordt weergegeven in het volgende codevoorbeeld, kunt u een bestandsnaampatroon opgeven met de tijdelijke aanduiding voor blob:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Deze code alleen blobs die namen die beginnen met 'oorspronkelijke--' hebt opgehaald. Bijvoorbeeld: *oorspronkelijke Blob1.txt* in de *invoer* container wordt gekopieerd naar *kopie Blob1.txt* in de *uitvoer* container.

Als u een naampatroon opgeven voor blob-namen die accolades hebben met de naam moet, dubbelklikt u accolades gebruiken. Bijvoorbeeld, als u wilt zoeken blobs in de *installatiekopieën* container met namen als volgt:

        {20140101}-soundfile.mp3

Gebruik deze optie voor het patroon:

        images/{{20140101}}-{name}

In het voorbeeld wordt de *naam* aanduidingswaarde zou worden *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Afzonderlijke blob-naam en extensie voor tijdelijke aanduidingen
Het volgende codevoorbeeld de bestandsextensie wijzigt, zoals het gekopieerd blobs die worden weergegeven in de *invoer* container voor de *uitvoer* container. De code registreert de uitbreiding van de *invoer* blob en stelt u de uitbreiding van de *uitvoer* -blob naar *.txt*.

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

## <a id="types"></a>Typen die u aan BLOB's koppelen kunt
U kunt de `BlobTrigger` -kenmerk op de volgende typen:

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
* Andere typen gedeserialiseerd door [ICloudBlobStreamBinder](#icbsb) 

Als u samenwerken met het Azure storage-account wilt, kunt u ook toevoegen een `CloudStorageAccount` -parameter voor de methodehandtekening.

Zie voor voorbeelden van de [blob-binding-code in de sdk van azure webjobs-opslagplaats op GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Ophalen van blob tekstinhoud door binding naar een tekenreeks
Als tekst blobs worden verwacht, `BlobTrigger` kunnen worden toegepast op een `string` parameter. Het volgende codevoorbeeld wordt gebonden een tekst-blob naar een `string` parameter met de naam `logMessage`. De functie wordt deze parameter de inhoud van de blob geschreven naar het dashboard WebJobs SDK. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a>Ophalen van blob-inhoud geserialiseerd met behulp van ICloudBlobStreamBinder
Het volgende codevoorbeeld maakt gebruik van een klasse die implementeert `ICloudBlobStreamBinder` zodat de `BlobTrigger` kenmerk binden van een blob naar de `WebImage` type.

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

De `WebImage` binding code is opgegeven een `WebImageBinder` klasse die is afgeleid van `ICloudBlobStreamBinder`.

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a>Ophalen van de blobpad voor de activerende blob
Als u wilt ophalen van de naam van de container en de blob-naam van de blob die de functie is geactiveerd, bevatten een `blobTrigger` opgegeven parameter in de functiehandtekening.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Het verwerken van verontreinigde blobs
Wanneer een `BlobTrigger` functie mislukt, de SDK-aanroepen deze opnieuw als de fout is veroorzaakt door een tijdelijke fout. Als de fout wordt veroorzaakt door de inhoud van de blob, mislukt de functie elke keer dat de blob wordt verwerkt. Standaard de SDK-aanroepen een functie maximaal 5 maal voor een opgegeven blob. Als de vijfde mislukt probeert, wordt een bericht met de SDK toegevoegd aan een wachtrij met de naam *webjobs-blobtrigger-poison*.

Het maximum aantal nieuwe pogingen kan worden geconfigureerd. Dezelfde [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) instelling wordt gebruikt voor de verwerking van verontreinigde blob en wachtrij verontreinigd bericht verwerking. 

Bericht uit de wachtrij voor verontreinigde blobs is een JSON-object met de volgende eigenschappen:

* FunctionId (in de notatie *{naam van een webtaak}*. Functies. *{Functienaam}*, bijvoorbeeld: WebJob1.Functions.CopyBlob)
* BlobType ('BlockBlob' of 'PageBlob')
* ContainerName
* BlobName
* ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

In het volgende codevoorbeeld wordt de `CopyBlob` functie heeft code die ervoor zorgt dat mislukken telkens wanneer deze wordt aangeroepen. Nadat de SDK voor het maximum aantal nieuwe pogingen aangeroepen, een bericht in de wachtrij verontreinigd blob gemaakt en dat bericht is verwerkt door de `LogPoisonBlob` functie. 

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

De SDK deserializes automatisch het JSON-bericht. Hier volgt de `PoisonBlobMessage` klasse: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a>BLOB polling-algoritme
De WebJobs SDK scant alle containers die zijn opgegeven door `BlobTrigger` kenmerken aan begin van de toepassing. In een grote opslagaccount deze scan kan enige tijd duren, zodat dit mogelijk even voordat nieuwe blobs zijn gevonden en `BlobTrigger` functies worden uitgevoerd.

Om te detecteren nieuwe of gewijzigde blobs na het starten van toepassingsservices, leest de SDK periodiek uit de logboeken van de blob-opslag. De logboeken van de blob zijn gebufferd en alleen fysiek elke 10 minuten weggeschreven of dus, dus er aanzienlijke vertraging optreden nadat een blob wordt gemaakt of voordat de bijbehorende bijgewerkt `BlobTrigger` functie wordt uitgevoerd. 

Er is een uitzondering voor blobs die u met behulp van maakt de `Blob` kenmerk. Wanneer de WebJobs SDK een nieuwe blob maakt, wordt de nieuwe blob onmiddellijk doorgegeven aan een overeenkomende `BlobTrigger` functies. Daarom hebt u een keten van blob-invoer en uitvoer, kan de SDK verwerken efficiënt. Maar als u wilt een lage latentie functies voor blobs die zijn gemaakt of bijgewerkt op een andere manier voor het verwerken van uw blob uitgevoerd, wordt u aangeraden `QueueTrigger` plaats `BlobTrigger`.

### <a id="receipts"></a>BLOB ontvangstbevestigingen
De WebJobs SDK zorgt ervoor dat er geen `BlobTrigger` functie wordt meer dan één keer aangeroepen voor de dezelfde nieuwe of bijgewerkte blob. Dit wordt uitgevoerd door het onderhouden van *blob ontvangstbevestigingen* om te bepalen of een versie van de opgegeven blob is verwerkt.

BLOB ontvangstbevestigingen worden opgeslagen in een container met de naam *webjobs-azure-hosts* in de Azure storage-account dat is opgegeven door de verbindingsreeks AzureWebJobsStorage. De ontvangst van een blob heeft de volgende informatie:

* De functie die voor de blob is aangeroepen ('*{naam van een webtaak}*. Functies. *{Functienaam}*', bijvoorbeeld: 'WebJob1.Functions.CopyBlob')
* De containernaam
* Het blobtype ('BlockBlob' of 'PageBlob')
* De blob-naam
* De ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

Als u afdwingen opnieuw verwerken van een blob wilt, kunt u handmatig de ontvangst van de blob voor blob uit verwijderen de *webjobs-azure-hosts* container.

## <a id="queues"></a>Verwante onderwerpen gedekt door het artikel wachtrijen
Scenario's die niet specifiek zijn voor blob-verwerking, Zie voor meer informatie over het afhandelen van de blob-verwerking geactiveerd door een wachtrijbericht of voor WebJobs SDK [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Verwante onderwerpen in dit artikel omvatten het volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken
* De SDK-verbindingsreeksen in code instellen.
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Configureer `MaxDequeueCount` voor het verwerken van verontreinigde blob.
* Een functie handmatig activeren
* Schrijven Logboeken

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding is opgegeven codevoorbeelden die laten hoe algemene scenario's zien voor het werken met Azure blobs afhandelen. Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

