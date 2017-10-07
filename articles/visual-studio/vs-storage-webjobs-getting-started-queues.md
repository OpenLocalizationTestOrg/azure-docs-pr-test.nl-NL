---
title: aaaGetting gestart met de opslag van de wachtrij en Visual Studio verbonden services (webtaak projecten) | Microsoft Docs
description: Hoe tooget gestart met Azure Queue storage in een project webtaak nadat tooa storage-account met Visual Studio verbinding services verbonden.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Aan de slag met Azure Queue storage en Visual Studio verbonden services (webtaak projecten)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe de slag met Azure Queue storage in een project voor Visual Studio Azure webtaak nadat u hebt gemaakt of waarnaar wordt verwezen Azure storage-account met behulp van Visual Studio Hallo **verbonden Services toevoegen** in het dialoogvenster. Wanneer u een project storage account tooa webtaak toevoegen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster Hallo juiste Azure Storage NuGet-pakketten zijn geïnstalleerd, Hallo juiste .NET verwijzingen worden toegevoegd toohello Project en verbindingsreeksen voor Hallo storage-account worden bijgewerkt in Hallo App.config-bestand.  

Dit artikel vindt u C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure Queue storage-service.

Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten. Zie [aan de slag met Azure Queue Storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie. Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen
toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo **QueueTrigger** kenmerk. Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van Hallo wachtrij toopoll. toosee hoe tooset Hallo wachtrijnaam dynamisch, Bekijk [hoe tooset configuratieopties](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>String, Wachtrijberichten
Hallo voorbeeld te volgen, Hallo wachtrij bevat een Tekenreeksbericht voor de dus **QueueTrigger** toegepaste tooa tekenreeksparameter met de naam is **logMessage** die Hallo inhoud van de wachtrij het Hallo-bericht bevat. Hallo functie [schrijft een logboek bericht toohello Dashboard](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Naast **tekenreeks**, Hallo is mogelijk een bytematrix een **CloudQueueMessage** object of een POCO die u definieert.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
Hallo voorbeeld te volgen, wachtrij het Hallo-bericht bevat JSON voor een **BlobInformation** object waaronder een **BlobName** eigenschap. Hallo SDK deserializes automatisch Hallo-object.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten. Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Async-functies
Hallo async-functie na [schrijft een logboek toohello Dashboard](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals weergegeven in het volgende voorbeeld die een blob kopieert Hallo. (Voor een uitleg van Hallo **queueTrigger** tijdelijke aanduiding, Zie Hallo [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sectie.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Typen Hallo QueueTrigger kenmerk werkt met
U kunt **QueueTrigger** Hello volgende typen:

* **tekenreeks**
* Een POCO-type dat geserialiseerd als JSON
* **byte]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Polling-algoritme
Hallo SDK implementeert een willekeurige exponentiële back-off algoritme tooreduce Hallo effect van niet-actieve wachtrij polling op de opslagkosten voor transactie.  Wanneer een bericht is gevonden, Hallo SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen. Na meerdere mislukte pogingen tooget een wachtrijbericht, wachttijd Hallo tooincrease voortgezet totdat het Hallo maximale wachttijd, bereikt welke standaardwaarden tooone minuut. [Hallo maximale wachttijd is configureerbaar](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Meerdere exemplaren
Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaken uitvoert op elke machine en elke machine wordt gewacht op triggers en probeert toorun functies. In sommige gevallen die kan dit leiden toosome functies verwerken Hallo dezelfde gegevens tweemaal functies moeten dus van idempotent (zodat die herhaaldelijk aanroepen Hello dezelfde invoergegevens levert geen resultaten dubbele geschreven).  

## <a name="parallel-execution"></a>Parallelle uitvoering
Als er meerdere functies luistert naar verschillende wachtrijen, wordt Hallo SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.

Hallo geldt ook wanneer meerdere berichten worden ontvangen voor een enkele wachtrij. Standaard Hallo SDK een batch van 16 Wachtrijberichten tegelijk opgehaald en wordt uitgevoerd Hallo-functie die parallel worden verwerkt. [Hallo batchgrootte is configureerbaar](#how-to-set-configuration-options). Bij het ophalen van Hallo nummer wordt verwerkt omlaag toohalf van batchgrootte hello, hello SDK opgehaald van een andere batch- en begint met de verwerking van deze berichten. Maximum aantal gelijktijdige berichten worden verwerkt per functie Hallo is daarom een anderhalf maal Hallo batchgrootte. Deze beperking geldt afzonderlijk tooeach-functie die een **QueueTrigger** kenmerk. Als u niet dat parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, stelt u Hallo batch grootte too1.

## <a name="get-queue-or-queue-message-metadata"></a>Wachtrij of wachtrij bericht metagegevens ophalen
U kunt Hallo berichteigenschappen volgen door toe te voegen parameters toohello methodehandtekening krijgen:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **tekenreeks** queueTrigger (de berichttekst bevat)
* **tekenreeks** id
* **tekenreeks** popReceipt
* **int** dequeueCount

Als u wilt dat toowork rechtstreeks met hello Azure storage-API, u kunt ook toevoegen een **CloudStorageAccount** parameter.

Hallo volgende voorbeeld wordt geschreven alle deze metagegevens tooan INFO-toepassingslogboek. In voorbeeld Hallo bevatten zowel logMessage als queueTrigger Hallo inhoud van de wachtrij het Hallo-bericht.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Hier volgt een voorbeeld-logboekbestanden geschreven door de voorbeeldcode Hallo:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>Correct afsluiten
Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een **CancellationToken** parameter waarmee Hallo toonotify Hallo besturingssysteemfunctie wanneer hello webtaak is over toobe beëindigd. U kunt deze melding toomake ervoor Hallo-functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.

Hallo volgende voorbeeld wordt getoond hoe toocheck voor aanstaande webtaak beëindiging in een functie.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Opmerking:** Hallo Dashboard mogelijk niet correct weergegeven Hallo status en de uitvoer van de functies die zijn afgesloten.

Zie voor meer informatie [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht
een functie die u een nieuw wachtrijbericht, gebruik Hallo maakt toowrite **wachtrij** kenmerk. Zoals **QueueTrigger**, u doorgeeft in Hallo wachtrijnaam als een tekenreeks of kunt u [Hallo wachtrijnaam dynamisch ingesteld](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>String, Wachtrijberichten
een nieuwe wachtrijbericht in Hallo wachtrij met de naam 'outputqueue' maakt Hello na niet async-codevoorbeeld met dezelfde inhoud als wachtrij het Hallo-bericht in Hallo wachtrij met de naam 'inputqueue ontvangen' Hallo. (Gebruik voor asynchrone functies **IAsyncCollector<T>**  zoals later in deze sectie.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
toocreate een wachtrijbericht met een POCO in plaats van een tekenreeks, op te geven Hallo POCO typt als een output-parameter toohello **wachtrij** kenmerkconstructor.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Hallo SDK serialiseert automatisch Hallo object tooJSON. Een wachtrijbericht is altijd gemaakt, zelfs als het Hallo-object is null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Meerdere berichten maken of in een async-functies
toocreate meerdere berichten maken Hallo parametertype voor Hallo uitvoerwachtrij **ICollector<T>**  of **IAsyncCollector<T>**, zoals weergegeven in het volgende voorbeeld Hallo.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Het bericht voor elke wachtrij wordt gemaakt bij direct hello **toevoegen** methode wordt aangeroepen.

### <a name="types-that-hello-queue-attribute-works-with"></a>Typen Hallo wachtrij kenmerk werkt met
U kunt Hallo **wachtrij** -kenmerk op Hallo parametertypen te volgen:

* **uitgaand tekenreeks** (wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie Hallo eindigt)
* **uitgaand byte []** (werkt als **tekenreeks**)
* **uitgaand CloudQueueMessage** (werkt als **tekenreeks**)
* **uitgaand POCO** (een serialiseerbaar type, maakt u een bericht met een null-object als Hallo-parameter is null wanneer de functie Hallo eindigt)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (voor het handmatig maken van berichten met behulp van Hallo API van Azure Storage rechtstreeks)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
Als u toodo moet enkele werken in uw functie voordat u een kenmerk WebJobs SDK, zoals **wachtrij**, **Blob**, of **tabel**, kunt u Hallo **IBinder** interface.

Hallo volgende voorbeeld wordt een bericht invoerwachtrij en maakt u een nieuw bericht Hello dezelfde inhoud in een wachtrij voor de uitvoer. Hallo uitvoer wachtrijnaam is ingesteld door code in de hoofdtekst van de functie Hallo Hallo.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Hallo **IBinder** interface kan ook worden gebruikt met Hallo **tabel** en **Blob** kenmerken.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Hoe tooread en write-blobs en tabellen tijdens het verwerken van een wachtrijbericht
Hallo **Blob** en **tabel** kenmerken kunt u tooread en blobs en tabellen te schrijven. Hallo-voorbeelden in deze sectie tooblobs van toepassing. Zie voor codevoorbeelden die laten hoe tootrigger verwerkt zien wanneer BLOB's worden gemaakt of bijgewerkt, [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [hoe toouse Azure-tabel opslag Hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>String, Wachtrijberichten activering van blob-bewerkingen
Voor een wachtrijbericht met een tekenreeks **queueTrigger** is een tijdelijke aanduiding kunt u in Hallo **Blob** van het kenmerk **blobPath** parameter met inhoud van Hallo Hallo-bericht.

Hallo volgende voorbeeld wordt **stroom** tooread en write blobs objecten. wachtrij het Hallo-bericht is Hallo-naam van een blob die zich in Hallo textblobs container. Een kopie van de blob met Hallo '-nieuwe ' toegevoegde toohello naam wordt gemaakt in Hallo dezelfde container.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hallo **Blob** kenmerk constructor heeft een **blobPath** parameter waarmee Hallo-container en de blob-naam. Zie voor meer informatie over deze tijdelijke aanduiding [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Wanneer Hallo kenmerk wordt verfraaid een **stroom** object, een andere constructorparameter geeft u op Hallo **FileAccess** modus lezen, schrijven of lezen/schrijven.

Hallo volgende voorbeeld wordt een **CloudBlockBlob** toodelete een blob-object. wachtrij het Hallo-bericht is Hallo-naam van Hallo blob.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
Voor een POCO opgeslagen als JSON in wachtrij het Hallo-bericht, kunt u tijdelijke aanduidingen voor naam van de eigenschappen van het object in Hallo Hallo **wachtrij** van het kenmerk **blobPath** parameter. U kunt ook metagegevens-Eigenschapsnamen wachtrij gebruiken als tijdelijke aanduidingen. Zie [wachtrij of wachtrij bericht metagegevens ophalen](#get-queue-or-queue-message-metadata).

Hallo volgende voorbeeld wordt gekopieerd een blob tooa nieuwe blob met een andere extensie. wachtrij het Hallo-bericht is een **BlobInformation** -object met **BlobName** en **BlobNameWithoutExtension** eigenschappen. eigenschapnamen Hello worden gebruikt als tijdelijke aanduidingen in Hallo blobpad voor Hallo **Blob** kenmerken.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten. Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Als u toodo werken sommige in de functie moet voor het binden van een blob tooan-object, kunt u Hallo kenmerk in de hoofdtekst Hallo van Hallo-functie, zoals wordt weergegeven in [WebJobs SDK gebruiken kenmerken in de hoofdtekst van een functie Hallo](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Blob-kenmerk met de Hallo kunnen worden gebruikt
Hallo **Blob** kenmerk kan worden gebruikt met de volgende typen Hallo:

* **Stroom** (lezen of schrijven, opgegeven met behulp van Hallo FileAccess constructorparameter)
* **TextReader**
* **TextWriter**
* **tekenreeks** (gelezen)
* **uitgaand tekenreeks** (schrijven, maakt u een blob alleen als Hallo tekenreeksparameter niet-null is bij het Hallo-functie retourneert)
* POCO (lezen)
* uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer Hallo functie retourneert)
* **CloudBlobStream** (schrijven)
* **ICloudBlob** (lezen of schrijven)
* **CloudBlockBlob** (lezen of schrijven)
* **CloudPageBlob** (lezen of schrijven)

## <a name="how-toohandle-poison-messages"></a>Hoe toohandle poison berichten
Berichten waarvan de inhoud zorgt ervoor een functie toofail dat worden genoemd *berichten poison*. Hallo-functie is mislukt, wachtrij het Hallo-bericht is niet verwijderd als uiteindelijk wordt opgehaald, waardoor Hallo cyclus toobe herhaald. Hallo SDK kan automatisch Hallo cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.

### <a name="automatic-poison-message-handling"></a>Verwerken van verontreinigde berichten automatische
Hallo SDK zal een functie van too5 keren tooprocess een wachtrijbericht aanroepen. Als de vijfde probeer Hallo mislukt, is het Hallo-bericht verplaatste tooa verontreinigd wachtrij. U kunt zien hoe tooconfigure maximum aantal pogingen in Hallo [hoe configuratieopties tooset](#how-to-set-configuration-options).

Hallo verontreinigd wachtrij heet *{originalqueuename}*-verontreinigd. U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is.

In het volgende voorbeeld Hallo Hallo **CopyBlob** functie mislukken wanneer er een wachtrijbericht bevat Hallo-naam van een blob die niet bestaat. Wanneer dit gebeurt, wordt het Hallo-bericht wordt verplaatst van Hallo copyblobqueue wachtrij toohello copyblobqueue poison wachtrij. Hallo **ProcessPoisonMessage** vervolgens logboeken Hallo verontreinigd bericht.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Hallo volgende afbeelding ziet u console-uitvoer van deze functies bij het verwerken van een poison-bericht.

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Verwerken van verontreinigde berichten handmatige
U krijgt Hallo aantal keren dat een bericht opgepikt voor verwerking door toe te voegen een **int** parameter met de naam **dequeueCount** tooyour-functie. U kunt vervolgens het selectievakje hello telling in functiecode in wachtrij- en uw eigen verontreinigd bericht verwerkt wanneer Hallo nummer een drempelwaarde overschrijdt, zoals wordt weergegeven in het volgende voorbeeld Hallo uitvoeren.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a>Hoe tooset configuratieopties
U kunt Hallo **JobHostConfiguration** type tooset Hallo volgende configuratieopties:

* Hallo SDK verbindingsreeksen in code instellen.
* Configureer **QueueTrigger** instellingen zoals het maximum aantal in wachtrij.
* Wachtrijnamen van de ophalen van configuratie.

### <a name="set-sdk-connection-strings-in-code"></a>SDK-verbindingsreeksen instellen in code
Hallo SDK-verbindingsreeksen instellen in de code kunt u toouse uw eigen namen van de tekenreeks verbindingen in configuratiebestanden of omgevingsvariabelen, zoals wordt weergegeven in Hallo voorbeeld te volgen.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a>QueueTrigger instellingen configureren
U kunt Hallo instellingen die van toepassing toohello wachtrij berichtverwerking volgende configureren:

* maximum aantal berichten die tegelijkertijd toobe parallel uitgevoerd worden opgepikt Hallo (de standaardwaarde is 16).
* Hallo maximum aantal pogingen voordat een wachtrijbericht tooa poison-wachtrij worden verzonden (de standaardwaarde is 5).
* Hallo maximale wachttijd voordat opnieuw polling wanneer een wachtrij leeg is (de standaardwaarde is 1 minuut).

Hallo volgende voorbeeld wordt getoond hoe tooconfigure deze instellingen:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Waarden instellen voor de WebJobs SDK constructorparameters in code
Soms wilt u toospecify een wachtrijnaam, een blob-naam of de container of een tabel naam in de code in plaats van harde-code. U kunt bijvoorbeeld toospecify Hallo wachtrijnaam voor **QueueTrigger** in een configuratie-bestand of de omgeving variabele.

U kunt dit doen door doorgeven in een **NameResolver** object toohello **JobHostConfiguration** type. U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw **NameResolver** code geeft Hallo werkelijke waarden toobe gebruikt in plaats van de tijdelijke aanduidingen.

Bijvoorbeeld, Stel dat u wilt dat toouse een wachtrij met de naam logqueuetest in de testomgeving Hallo en één met de naam logqueueprod in productie. In plaats van een vastgelegde wachtrijnaam, die u wilt toospecify Hallo-naam van een vermelding in Hallo **appSettings** verzameling die de werkelijke wachtrijnaam Hallo zou hebben. Als hello **appSettings** sleutel logqueue is, de functie eruit als Hallo voorbeeld te volgen.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Uw **NameResolver** klasse kan vervolgens ophalen Hallo wachtrijnaam van **appSettings** zoals weergegeven in Hallo voorbeeld te volgen:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

U geeft Hallo **NameResolver** klasse in toohello **JobHost** zoals weergegeven in het volgende voorbeeld Hallo-object.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer het Hallo-toepassing wordt gestart. U kunt de naam van de blob-container niet wijzigen terwijl Hallo-taak wordt uitgevoerd.

## <a name="how-tootrigger-a-function-manually"></a>Hoe een functie tootrigger handmatig
een functie tootrigger handmatig hello gebruiken **aanroepen** of **CallAsync** methode op Hallo **JobHost** object en Hallo **NoAutomaticTrigger** het kenmerk op Hallo-functie, zoals wordt weergegeven in Hallo voorbeeld te volgen.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a>Hoe toowrite registreert
Hallo Dashboard ziet u Logboeken op twee plaatsen: Hallo-pagina voor Hallo webtaak en Hallo-pagina voor een specifieke webtaak-aanroep.

![Logboeken in webtaak pagina](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

De uitvoer van de Console-methoden die u in een functie of Hallo aanroepen **Main()** wordt weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet in Hallo-pagina voor een bepaalde methodeaanroep. Uitvoer van Hallo TextWriter object die u via een parameter in de methodehandtekening weergegeven in de dashboardpagina Hallo voor een methodeaanroep.

Console-uitvoer kan niet worden bepaald gekoppelde tooa de methodeaanroep omdat Hallo Console één thread, terwijl veel functies kunnen worden uitgevoerd op Hallo hetzelfde moment. Daarom is Hallo SDK biedt elke functieaanroep met een eigen unieke logboek writer-object.

toowrite [logboeken voor tracering van toepassing](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik **Console.Out** (maakt logboeken die zijn gemarkeerd als INFO) en **Console.Error** (logboeken die zijn gemarkeerd als fout maakt). Een alternatief is toouse [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)en waarmee u uitgebreid, waarschuwing, kritiek niveaus in de toevoeging tooInfo en de fout. Logboeken voor tracering van toepassing worden weergegeven in Hallo web app-logboekbestanden, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren. Geldt voor alle Console-uitvoer, Hallo meest recente 100-toepassingslogboeken ook worden weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet Hallo pagina voor een functie-aanroep.

Console-uitvoer wordt weergegeven in Hallo Dashboard alleen als Hallo programma wordt uitgevoerd in een Azure-webtaak niet als Hallo programma lokaal wordt uitgevoerd of in sommige andere omgeving.

U kunt logboekregistratie uitschakelen door in te stellen Hallo Dashboard connection string toonull. Zie voor meer informatie [hoe tooset configuratieopties](#how-to-set-configuration-options).

Hallo volgende voorbeeld ziet u op verschillende manieren toowrite Logboeken:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Hallo in Hallo WebJobs SDK-Dashboard, uitvoer van Hallo **TextWriter** object wordt wanneer u toohello pagina voor een bepaalde gaat functie aanroepen en selecteer **wisselknop uitvoer**:

![Het aanroepen van koppeling](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

In Hallo WebJobs SDK-Dashboard, Hallo meest recente 100 regels van de Console uitvoer weergeven van wanneer u toohello pagina voor Hallo webtaak (niet voor functie-aanroep Hallo gaat) en selecteer **wisselknop uitvoer**.

![Uitvoer van de in-of uitschakelen](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in Hallo web-app-bestandssysteem.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

In een Azure blob-toepassing hello logboeken moeten uitzien: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,

En in een Azure-tabel Hallo **Console.Out** en **Console.Error** logboeken moeten uitzien:

![Logboek van de gegevens in de tabel](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Foutenlogboek in tabel](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure wachtrijen. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

