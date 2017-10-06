---
title: aaaHow toouse Azure queue storage met Hallo WebJobs SDK
description: Meer informatie over hoe toouse Azure queue storage Hello WebJobs SDK. Maken en verwijderen van wachtrijen; invoegen, inspecteren, ophalen en verwijderen van Wachtrijberichten en meer.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Hoe toouse Azure queue storage Hello WebJobs SDK
## <a name="overview"></a>Overzicht
Deze handleiding bevat C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure queue storage-service.

Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md) of te[meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Hallo codefragmenten de meeste functies, alleen weergeven niet code die wordt gemaakt van Hallo Hallo `JobHost` object zoals in dit voorbeeld:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Hallo handleiding bevat de volgende onderwerpen Hallo:

* [Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen](#trigger)
  * String, Wachtrijberichten
  * POCO-berichtenwachtrij-berichten
  * Async-functies
  * Typen Hallo QueueTrigger kenmerk werkt met
  * Polling-algoritme
  * Meerdere exemplaren
  * Parallelle uitvoering
  * Wachtrij of wachtrij bericht metagegevens ophalen
  * Correct afsluiten
* [Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht](#createqueue)
  * String, Wachtrijberichten
  * POCO-berichtenwachtrij-berichten
  * Meerdere berichten maken of in een async-functies
  * Typen Hallo wachtrij kenmerk werkt met
  * Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
* [Hoe tooread en write blobs tijdens het verwerken van een wachtrijbericht](#blobs)
  * String, Wachtrijberichten
  * POCO-berichtenwachtrij-berichten
  * Typen Hallo Blob kenmerk werkt met
* [Hoe toohandle poison berichten](#poison)
  * Verwerken van verontreinigde berichten automatische
  * Verwerken van verontreinigde berichten handmatige
* [Hoe tooset configuratieopties](#config)
  * SDK-verbindingsreeksen instellen in code
  * QueueTrigger instellingen configureren
  * Waarden instellen voor de WebJobs SDK constructorparameters in code
* [Hoe een functie tootrigger handmatig](#manual)
* [Hoe toowrite registreert](#logs)
* [Hoe toohandle fouten en time-outs configureren](#errors)
* [Volgende stappen](#nextsteps)

## <a id="trigger"></a>Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen
toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo `QueueTrigger` kenmerk. Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van Hallo wachtrij toopoll. U kunt ook [Hallo wachtrijnaam dynamisch ingesteld](#config).

### <a name="string-queue-messages"></a>String, Wachtrijberichten
Hallo voorbeeld te volgen, Hallo wachtrij bevat een Tekenreeksbericht voor de dus `QueueTrigger` toegepaste tooa tekenreeksparameter met de naam is `logMessage` die Hallo inhoud van de wachtrij het Hallo-bericht bevat. Hallo functie [schrijft een logboek bericht toohello Dashboard](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Naast `string`, Hallo is mogelijk een bytematrix een `CloudQueueMessage` object of een POCO die u definieert.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
Hallo voorbeeld te volgen, wachtrij het Hallo-bericht bevat JSON voor een `BlobInformation` object waaronder een `BlobName` eigenschap. Hallo SDK deserializes automatisch Hallo-object.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten. Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Async-functies
Hallo async-functie na [schrijft een logboek toohello Dashboard](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals weergegeven in het volgende voorbeeld die een blob kopieert Hallo. (Voor een uitleg van Hallo `queueTrigger` tijdelijke aanduiding, Zie Hallo [Blobs](#blobs) sectie.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Typen Hallo QueueTrigger kenmerk werkt met
U kunt `QueueTrigger` Hello volgende typen:

* `string`
* Een POCO-type dat geserialiseerd als JSON
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a>Polling-algoritme
Hallo SDK implementeert een willekeurige exponentiële back-off algoritme tooreduce Hallo effect van niet-actieve wachtrij polling op de opslagkosten voor transactie.  Wanneer een bericht is gevonden, Hallo SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen. Na meerdere mislukte pogingen tooget een wachtrijbericht, wachttijd Hallo tooincrease voortgezet totdat het Hallo maximale wachttijd, bereikt welke standaardwaarden tooone minuut. [Hallo maximale wachttijd is configureerbaar](#config).

### <a id="instances"></a>Meerdere exemplaren
Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaak wordt uitgevoerd op elke computer en elke machine wordt gewacht op triggers en probeert toorun functies. Hallo WebJobs SDK wachtrij trigger automatisch wordt voorkomen dat een functie verwerken van een wachtrijbericht meerdere keren; functies hoeft geen toobe toobe idempotent geschreven. Echter, als u wilt dat tooensure dat slechts één exemplaar van een functie wordt uitgevoerd zelfs als er meerdere exemplaren van Hallo host web-app, kunt u Hallo `Singleton` kenmerk.

### <a id="parallel"></a>Parallelle uitvoering
Als er meerdere functies luistert naar verschillende wachtrijen, wordt Hallo SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.

Hallo geldt ook wanneer meerdere berichten worden ontvangen voor een enkele wachtrij. Standaard Hallo SDK een batch van 16 Wachtrijberichten tegelijk opgehaald en wordt uitgevoerd Hallo-functie die parallel worden verwerkt. [Hallo batchgrootte is configureerbaar](#config). Bij het ophalen van Hallo nummer wordt verwerkt omlaag toohalf van batchgrootte hello, hello SDK opgehaald van een andere batch- en begint met de verwerking van deze berichten. Maximum aantal gelijktijdige berichten worden verwerkt per functie Hallo is daarom een anderhalf maal Hallo batchgrootte. Deze beperking geldt afzonderlijk tooeach-functie die een `QueueTrigger` kenmerk.

Als u geen parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, kunt u Hallo batch grootte too1 instellen. Zie ook **meer controle over de verwerking van de wachtrij** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).

### <a id="queuemetadata"></a>Wachtrij of wachtrij bericht metagegevens ophalen
U kunt Hallo berichteigenschappen volgen door toe te voegen parameters toohello methodehandtekening krijgen:

* `DateTimeOffset`expirationTime
* `DateTimeOffset`insertionTime
* `DateTimeOffset`nextVisibleTime
* `string`queueTrigger (de berichttekst bevat)
* `string`ID
* `string`popReceipt
* `int`dequeueCount

Als u wilt dat toowork rechtstreeks met hello Azure storage-API, u kunt ook toevoegen een `CloudStorageAccount` parameter.

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

### <a id="graceful"></a>Correct afsluiten
Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een `CancellationToken` parameter waarmee Hallo toonotify Hallo besturingssysteemfunctie wanneer hello webtaak is over toobe beëindigd. U kunt deze melding toomake ervoor Hallo-functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.

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

## <a id="createqueue"></a>Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht
een functie die u een nieuw wachtrijbericht, gebruik Hallo maakt toowrite `Queue` kenmerk. Zoals `QueueTrigger`, u doorgeeft in Hallo wachtrijnaam als een tekenreeks of kunt u [Hallo wachtrijnaam dynamisch ingesteld](#config).

### <a name="string-queue-messages"></a>String, Wachtrijberichten
een nieuwe wachtrijbericht in Hallo wachtrij met de naam 'outputqueue' maakt Hello na niet async-codevoorbeeld met dezelfde inhoud als wachtrij het Hallo-bericht in Hallo wachtrij met de naam 'inputqueue ontvangen' Hallo. (Gebruik voor asynchrone functies `IAsyncCollector<T>` zoals later in deze sectie.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
toocreate een wachtrijbericht met een POCO in plaats van een tekenreeks, op te geven Hallo POCO typt als een output-parameter toohello `Queue` kenmerkconstructor.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Hallo SDK serialiseert automatisch Hallo object tooJSON. Een wachtrijbericht is altijd gemaakt, zelfs als het Hallo-object is null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Meerdere berichten maken of in een async-functies
toocreate meerdere berichten maken Hallo parametertype voor Hallo uitvoerwachtrij `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende voorbeeld Hallo.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Het bericht voor elke wachtrij wordt gemaakt bij direct hello `Add` methode wordt aangeroepen.

### <a name="types-that-hello-queue-attribute-works-with"></a>Typen Hallo wachtrij kenmerk werkt met
U kunt Hallo `Queue` -kenmerk op Hallo parametertypen te volgen:

* `out string`(wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie Hallo eindigt)
* `out byte[]`(werkt als `string`)
* `out CloudQueueMessage`(werkt als `string`)
* `out POCO`(een serialiseerbaar type, maakt u een bericht met een null-object als Hallo-parameter is null wanneer de functie Hallo eindigt)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(voor het maken van berichten handmatig rechtstreeks met Hallo API van Azure Storage)

### <a id="ibinder"></a>Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
Als u toodo moet enkele werken in uw functie voordat u een kenmerk WebJobs SDK, zoals `Queue`, `Blob`, of `Table`, kunt u Hallo `IBinder` interface.

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

Hallo `IBinder` interface kan ook worden gebruikt met Hallo `Table` en `Blob` kenmerken.

## <a id="blobs"></a>Hoe tooread en write-blobs en tabellen tijdens het verwerken van een wachtrijbericht
Hallo `Blob` en `Table` kenmerken kunt u tooread en blobs en tabellen te schrijven. Hallo-voorbeelden in deze sectie tooblobs van toepassing. Zie voor codevoorbeelden die laten hoe tootrigger verwerkt zien wanneer BLOB's worden gemaakt of bijgewerkt, [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [hoe toouse Azure-tabel opslag Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>String, Wachtrijberichten activering van blob-bewerkingen
Voor een wachtrijbericht met een tekenreeks `queueTrigger` is een tijdelijke aanduiding kunt u in Hallo `Blob` van het kenmerk `blobPath` parameter dat Hallo inhoud van het Hallo-bericht bevat.

Hallo volgende voorbeeld wordt `Stream` tooread en write blobs objecten. wachtrij het Hallo-bericht is Hallo-naam van een blob die zich in Hallo textblobs container. Een kopie van de blob met Hallo '-nieuwe ' toegevoegde toohello naam wordt gemaakt in Hallo dezelfde container.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hallo `Blob` kenmerk constructor heeft een `blobPath` parameter waarmee Hallo-container en de blob-naam. Zie voor meer informatie over deze tijdelijke aanduiding [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Wanneer Hallo kenmerk wordt verfraaid een `Stream` object, een andere constructorparameter geeft u op Hallo `FileAccess` modus lezen, schrijven of lezen/schrijven.

Hallo volgende voorbeeld wordt een `CloudBlockBlob` toodelete een blob-object. wachtrij het Hallo-bericht is Hallo-naam van Hallo blob.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij
Voor een POCO opgeslagen als JSON in wachtrij het Hallo-bericht, kunt u tijdelijke aanduidingen voor naam van de eigenschappen van het object in Hallo Hallo `Queue` van het kenmerk `blobPath` parameter. U kunt ook [eigenschapnamen metagegevens in de wachtrij](#queuemetadata) als tijdelijke aanduidingen.

Hallo volgende voorbeeld wordt gekopieerd een blob tooa nieuwe blob met een andere extensie. wachtrij het Hallo-bericht is een `BlobInformation` -object met `BlobName` en `BlobNameWithoutExtension` eigenschappen. eigenschapnamen Hello worden gebruikt als tijdelijke aanduidingen in Hallo blobpad voor Hallo `Blob` kenmerken.

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

Als u toodo werken sommige in de functie moet voor het binden van een blob tooan-object, kunt u Hallo-kenmerk in Hallo hoofdtekst van de functie Hallo [zoals eerder besproken voor Hallo wachtrij kenmerk](#ibinder).

### <a id="blobattributetypes"></a>Blob-kenmerk met de Hallo kunnen worden gebruikt
Hallo `Blob` kenmerk kan worden gebruikt met de volgende typen Hallo:

* `Stream`(lezen of schrijven, opgegeven met behulp van Hallo FileAccess constructorparameter)
* `TextReader`
* `TextWriter`
* `string`(gelezen)
* `out string`(schrijven, maakt u een blob alleen als Hallo tekenreeksparameter niet-null is bij het Hallo-functie retourneert)
* POCO (lezen)
* uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer Hallo functie retourneert)
* `CloudBlobStream`(schrijven)
* `ICloudBlob`(Lees- of schrijfbewerking)
* `CloudBlockBlob`(Lees- of schrijfbewerking)
* `CloudPageBlob`(Lees- of schrijfbewerking)

## <a id="poison"></a>Hoe toohandle poison berichten
Berichten waarvan de inhoud zorgt ervoor een functie toofail dat worden genoemd *berichten poison*. Hallo-functie is mislukt, wachtrij het Hallo-bericht is niet verwijderd als uiteindelijk wordt opgehaald, waardoor Hallo cyclus toobe herhaald. Hallo SDK kan automatisch Hallo cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.

### <a name="automatic-poison-message-handling"></a>Verwerken van verontreinigde berichten automatische
Hallo SDK zal een functie van too5 keren tooprocess een wachtrijbericht aanroepen. Als de vijfde probeer Hallo mislukt, is het Hallo-bericht verplaatste tooa verontreinigd wachtrij. [Hallo kunt u het maximum aantal pogingen is configureerbaar](#config).

Hallo verontreinigd wachtrij heet *{originalqueuename}*-verontreinigd. U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is.

In het volgende voorbeeld Hallo Hallo `CopyBlob` functie mislukken wanneer er een wachtrijbericht bevat Hallo-naam van een blob die niet bestaat. Wanneer dit gebeurt, wordt het Hallo-bericht wordt verplaatst van Hallo copyblobqueue wachtrij toohello copyblobqueue poison wachtrij. Hallo `ProcessPoisonMessage` vervolgens logboeken Hallo verontreinigd bericht.

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

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>Verwerken van verontreinigde berichten handmatige
U krijgt Hallo aantal keren dat een bericht opgepikt voor verwerking door toe te voegen een `int` parameter met de naam `dequeueCount` tooyour-functie. U kunt vervolgens het selectievakje hello telling in functiecode in wachtrij- en uw eigen verontreinigd bericht verwerkt wanneer Hallo nummer een drempelwaarde overschrijdt, zoals wordt weergegeven in het volgende voorbeeld Hallo uitvoeren.

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

## <a id="config"></a>Hoe tooset configuratieopties
U kunt Hallo `JobHostConfiguration` type tooset Hallo volgende configuratieopties:

* Hallo SDK verbindingsreeksen in code instellen.
* Configureer `QueueTrigger` instellingen zoals het maximum aantal in wachtrij.
* Wachtrijnamen van de ophalen van configuratie.

### <a id="setconnstr"></a>SDK-verbindingsreeksen instellen in code
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

### <a id="configqueue"></a>QueueTrigger instellingen configureren
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

### <a id="setnamesincode"></a>Waarden instellen voor de WebJobs SDK constructorparameters in code
Soms wilt u toospecify een wachtrijnaam, een blob-naam of de container of een tabel naam in de code in plaats van harde-code. U kunt bijvoorbeeld toospecify Hallo wachtrijnaam voor `QueueTrigger` in een configuratie-bestand of de omgeving variabele.

U kunt dit doen door doorgeven in een `NameResolver` toohello object `JobHostConfiguration` type. U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw `NameResolver` code geeft Hallo werkelijke waarden toobe gebruikt in plaats van de tijdelijke aanduidingen.

Bijvoorbeeld, Stel dat u wilt dat toouse een wachtrij met de naam logqueuetest in de testomgeving Hallo en één met de naam logqueueprod in productie. In plaats van een vastgelegde wachtrijnaam, die u wilt toospecify Hallo-naam van een vermelding in Hallo `appSettings` verzameling die de werkelijke wachtrijnaam Hallo zou hebben. Als hello `appSettings` sleutel logqueue is, de functie eruit als Hallo voorbeeld te volgen.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Uw `NameResolver` klasse kan vervolgens ophalen Hallo wachtrijnaam van `appSettings` zoals weergegeven in Hallo voorbeeld te volgen:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

U geeft Hallo `NameResolver` klasse in toohello `JobHost` zoals weergegeven in het volgende voorbeeld Hallo-object.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer het Hallo-toepassing wordt gestart. U kunt de naam van de blob-container niet wijzigen terwijl Hallo-taak wordt uitgevoerd.

## <a id="manual"></a>Hoe een functie tootrigger handmatig
een functie tootrigger handmatig hello gebruiken `Call` of `CallAsync` methode op Hallo `JobHost` object en Hallo `NoAutomaticTrigger` kenmerk op Hallo-functie, zoals wordt weergegeven in het volgende voorbeeld Hallo.

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

## <a id="logs"></a>Hoe toowrite registreert
Hallo Dashboard ziet u Logboeken op twee plaatsen: Hallo-pagina voor Hallo webtaak en Hallo-pagina voor een specifieke webtaak-aanroep.

![Logboeken in webtaak pagina](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

De uitvoer van de Console-methoden die u in een functie of Hallo aanroepen `Main()` wordt weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet in Hallo-pagina voor een bepaalde methodeaanroep. Uitvoer van Hallo TextWriter object die u via een parameter in de methodehandtekening weergegeven in de dashboardpagina Hallo voor een methodeaanroep.

Console-uitvoer kan niet worden bepaald gekoppelde tooa de methodeaanroep omdat Hallo Console één thread, terwijl veel functies kunnen worden uitgevoerd op Hallo hetzelfde moment. Daarom is Hallo SDK biedt elke functieaanroep met een eigen unieke logboek writer-object.

toowrite [logboeken voor tracering van toepassing](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik `Console.Out` (maakt logboeken die zijn gemarkeerd als INFO) en `Console.Error` (logboeken die zijn gemarkeerd als fout maakt). Een alternatief is toouse [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)en waarmee u uitgebreid, waarschuwing, kritiek niveaus in de toevoeging tooInfo en de fout. Logboeken voor tracering van toepassing worden weergegeven in Hallo web app-logboekbestanden, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren. Geldt voor alle Console-uitvoer, Hallo meest recente 100-toepassingslogboeken ook worden weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet Hallo pagina voor een functie-aanroep.

Console-uitvoer wordt weergegeven in Hallo Dashboard alleen als Hallo programma wordt uitgevoerd in een Azure-webtaak niet als Hallo programma lokaal wordt uitgevoerd of in sommige andere omgeving.

Dashboard logboekregistratie voor scenario's met hoge doorvoer uitschakelen. Standaard Hallo SDK schrijft logboeken toostorage en deze activiteit kan de prestaties nadelig beïnvloeden tijdens de verwerking van veel berichten. toodisable logboekregistratie instellen Hallo dashboard connection string toonull zoals in Hallo voorbeeld te volgen.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

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

Hallo in Hallo WebJobs SDK-Dashboard, uitvoer van Hallo `TextWriter` object wordt wanneer u toohello pagina voor een bepaalde gaat functie aanroepen en klik op **wisselknop uitvoer**:

![Klik op de koppeling van de functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

In Hallo WebJobs SDK-Dashboard, Hallo meest recente 100 regels van de Console uitvoer weergeven van wanneer u toohello pagina voor Hallo webtaak (niet voor functie-aanroep Hallo gaat) en klik op **wisselknop uitvoer**.

![Klik op de uitvoer in-of uitschakelen](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in Hallo web-app-bestandssysteem.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

In een Azure blob-toepassing hello logboeken moeten uitzien: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,

En in een Azure-tabel Hallo `Console.Out` en `Console.Error` logboeken moeten uitzien:

![Logboek van de gegevens in de tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Foutenlogboek in tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Als u tooplug in uw eigen berichtenlogboek wilt, Zie [in dit voorbeeld](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>Hoe toohandle fouten en time-outs configureren
Hallo WebJobs SDK bevat ook een [time-out](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) kenmerk waarmee u een functie toobe geannuleerd kunt als toocause niet voltooid binnen een opgegeven tijdsduur. En als u tooraise een waarschuwing wilt als er te veel fouten optreden binnen een opgegeven periode, kunt u Hallo `ErrorTrigger` kenmerk. Hier volgt een [ErrorTrigger voorbeeld](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

U kunt ook dynamisch uitschakelen en inschakelen van functies toocontrol of ze kunnen worden geactiveerd, door middel van een configuratieswitch die een app-instelling of de naam van omgevingsvariabele kan worden. Zie voor voorbeeldcode Hallo `Disable` kenmerk in [hello WebJobs SDK voorbeelden opslagplaats](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure wachtrijen. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).
