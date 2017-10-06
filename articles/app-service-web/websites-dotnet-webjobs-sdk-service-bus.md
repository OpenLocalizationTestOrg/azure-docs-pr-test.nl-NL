---
title: aaaHow toouse Azure Service Bus Hello WebJobs SDK
description: Meer informatie over hoe Hallo toouse Azure Service Bus-wachtrijen en onderwerpen met de WebJobs SDK.
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Hoe toouse Azure Service Bus met Hallo WebJobs SDK
## <a name="overview"></a>Overzicht
Deze handleiding bevat C# code voorbeelden die tonen hoe tootrigger een proces wanneer er wordt een Azure Service Bus-bericht ontvangen. Hallo code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.

Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md).

Hallo codefragmenten functies, alleen weergeven niet code die wordt gemaakt van Hallo Hallo `JobHost` object zoals in dit voorbeeld:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

Een [volledige Service Bus-codevoorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) in hello azure webjobs-sdk samples opslagplaats op GitHub.com is.

## <a id="prerequisites"></a>Vereisten
toowork met Service Bus hebt u tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pakket bovendien toohello andere pakketten WebJobs SDK. 

U hebt ook tooset hello AzureWebJobsServiceBus verbindingsreeks in toevoeging toohello storage-verbindingsreeksen.  U kunt dit doen in Hallo `connectionStrings` sectie van Hallo App.config-bestand, zoals wordt weergegeven in het volgende voorbeeld Hallo:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Zie voor een voorbeeldproject met Hallo Service Bus-verbindingsinstelling tekenreeks in Hallo App.config-bestand, [Service Bus-voorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

Hallo-verbindingsreeksen kunnen ook worden ingesteld in hello Azure runtime-omgeving, waarmee vervolgens Hallo App.config instellingen overschreven wanneer Hallo webtaak wordt uitgevoerd in Azure. Zie voor meer informatie [aan de slag met de WebJobs SDK Hallo](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Hoe tootrigger een functie als een Service Bus-wachtrij bericht wordt ontvangen
toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo `ServiceBusTrigger` kenmerk. Hallo kenmerkconstructor heeft een parameter met de naam Hallo van Hallo wachtrij toopoll.

### <a name="how-servicebustrigger-works"></a>De werking van ServiceBusTrigger
Hallo SDK een bericht ontvangt in `PeekLock` modus en aanroepen `Complete` op het Hallo-bericht als Hallo-functie wordt voltooid of aanroepen `Abandon` als Hallo-functie is mislukt. Als het Hallo-functie wordt uitgevoerd langer dan Hallo `PeekLock` time-out Hallo vergrendeling automatisch wordt vernieuwd.

Service Bus omgaat met een eigen verontreinigd wachtrij die niet kunnen worden beheerd of geconfigureerd door Hallo WebJobs SDK. 

### <a name="string-queue-message"></a>Tekenreeks wachtrijbericht
Hallo leest codevoorbeeld een wachtrijbericht die een tekenreeks bevat en schrijft Hallo tekenreeks toohello WebJobs SDK-dashboard.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Opmerking:** als u Hallo berichten in wachtrij plaatsen in een toepassing die geen gebruik maakt van Hallo WebJobs SDK maakt, moet u ervoor tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) te "text/plain'.

### <a name="poco-queue-message"></a>POCO wachtrijbericht
Hallo SDK wordt automatisch een wachtrijbericht met JSON voor een POCO deserialiseren [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type. Hallo codevoorbeeld leest het bericht van een wachtrij met een `BlobInformation` object waarvoor een `BlobName` eigenschap:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Codevoorbeelden die laat zien hoe toouse eigenschappen van Hallo POCO toowork met blobs en tabellen in dezelfde Hallo werkt, kunt u Hallo [opslag wachtrijen versie van dit artikel](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Als uw code die wachtrij het Hallo-bericht maakt geen gebruik maakt van Hallo WebJobs SDK, gebruikt u code vergelijkbare toohello voorbeeld te volgen:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Typen ServiceBusTrigger werkt met
Naast `string` en POCO-typen, kunt u Hallo `ServiceBusTrigger` kenmerk met een bytematrix of een `BrokeredMessage` object.

## <a id="create"></a>Hoe wachtrij toocreate Service Bus-berichten
toowrite een functie die een nieuwe wachtrijbericht maakt gebruik van Hallo `ServiceBus` kenmerk en Hallo wachtrij naam toohello kenmerkconstructor doorgeven. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Een enkel wachtrijbericht in een niet-async-functie maken
Hallo volgende codevoorbeeld maakt gebruik van een output-parameter toocreate een nieuw bericht in de wachtrij Hallo met de naam 'outputqueue' Hello dezelfde inhoud als bericht ontvangen in Hallo wachtrij met de naam 'inputqueue' Hallo.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

Hallo output-parameter voor het maken van een enkel wachtrijbericht mag geen van de volgende typen Hallo:

* `string`
* `byte[]`
* `BrokeredMessage`
* Een serialiseerbare POCO-type dat u opgeeft. Automatisch geserialiseerd als JSON.

Voor de parameters van het type POCO, een wachtrijbericht altijd gemaakt wanneer het Hallo-functie wordt beëindigd. Als Hallo parameter null is, maakt het Hallo SDK een wachtrijbericht dat null wordt geretourneerd wanneer het Hallo-bericht is ontvangen en gedeserialiseerd. Hallo voor andere typen, als Hallo parameter null is geen wachtrijbericht is gemaakt.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Maken van meerdere berichten in wachtrij plaatsen of in een async-functies
toocreate meerdere berichten gebruiken Hallo `ServiceBus` met kenmerk `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende codevoorbeeld Hallo:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Het bericht voor elke wachtrij wordt gemaakt bij direct hello `Add` methode wordt aangeroepen.

## <a id="topics"></a>Hoe toowork met Service Bus-onderwerpen
toowrite een functie die Hallo SDK-aanroepen wanneer een bericht wordt ontvangen op een Service Bus-onderwerp, gebruikt u Hallo `ServiceBusTrigger` kenmerk met de Hallo-constructor die onderwerpnaam en de naam van het abonnement, zoals wordt weergegeven in het volgende codevoorbeeld Hallo:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

een bericht op een onderwerp, gebruik Hallo toocreate `ServiceBus` kenmerk met een onderwerp naam Hallo dezelfde manier gebruiken met de naam van een wachtrij.

## <a name="features-added-in-release-11"></a>Functies die zijn toegevoegd in versie 1.1
Hallo volgende kenmerken zijn toegevoegd in versie 1.1:

* Toestaan grondige aanpassing van de berichtverwerking `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`biedt ondersteuning voor aanpassing van Service Bus Hallo `MessagingFactory` en `NamespaceManager`.
* Een `MessageProcessor` strategiepatroon kunt u toospecify een processor per wachtrij/onderwerp.
* Verwerking gelijktijdigheid van bericht is standaard ondersteund. 
* Eenvoudige aanpassing van `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.
* Toestaan dat [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe opgegeven op `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (voor scenario's waarbij u mogelijk geen rechten beheren). Houd er rekening mee dat Azure WebJobs niet kan tooautomatically inrichten niet-bestaande wachtrijen en onderwerpen zonder AccessRights beheren.

## <a id="queues"></a>Verwante onderwerpen Hallo opslag wachtrijen hoe tooarticle vallen
Zie voor informatie over WebJobs SDK scenario's niet specifiek tooService Bus, [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Onderwerpen in dit artikel zijn Hallo volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
* Hallo SDK verbindingsreeksen instellen in code
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Een functie handmatig activeren
* Schrijven Logboeken

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure Service Bus. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

