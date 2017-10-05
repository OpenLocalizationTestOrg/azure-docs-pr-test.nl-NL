---
title: Azure Service Bus gebruiken met de WebJobs SDK
description: Informatie over het gebruik van Azure Service Bus-wachtrijen en onderwerpen met de WebJobs SDK.
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a>Azure Service Bus gebruiken met de WebJobs SDK
## <a name="overview"></a>Overzicht
Deze handleiding bevat C#-codevoorbeelden die laten hoe een proces wordt geactiveerd zien wanneer een Azure Service Bus-bericht wordt ontvangen. De code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.

De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md).

De codefragmenten alleen weergeven functies, niet de code die wordt gemaakt de `JobHost` object zoals in dit voorbeeld:

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

Een [volledige Service Bus-codevoorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in de azure-API-sdk-samples-opslagplaats op GitHub.com.

## <a id="prerequisites"></a>Vereisten
Werken met Service Bus die u hebt voor het installeren van de [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet-pakket naast de andere WebJobs SDK-pakketten. 

Hebt u ook de verbindingsreeks AzureWebJobsServiceBus naast de storage-verbindingsreeksen instellen.  U kunt dit doen het `connectionStrings` gedeelte van het bestand App.config, zoals wordt weergegeven in het volgende voorbeeld:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Zie voor een voorbeeldproject met de instelling voor de Service Bus-tekenreeks in het bestand App.config [Service Bus-voorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

De verbindingsreeksen kunnen ook worden ingesteld in de Azure runtimeomgeving, die vervolgens het App.config-instellingen worden genegeerd als de webtaak wordt uitgevoerd in Azure. Zie voor meer informatie [aan de slag met de WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Het activeren van een functie als een Service Bus-wachtrijbericht wordt ontvangen
Voor het schrijven van een functie waarmee de WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruik de `ServiceBusTrigger` kenmerk. De kenmerkconstructor heeft een parameter met de naam van de wachtrij om te pollen.

### <a name="how-servicebustrigger-works"></a>De werking van ServiceBusTrigger
De SDK ontvangt een bericht in `PeekLock` modus en aanroepen `Complete` op het bericht als de functie wordt voltooid of aanroepen `Abandon` als de functie is mislukt. Als de functie wordt uitgevoerd langer dan de `PeekLock` een time-out opgetreden, de vergrendeling wordt automatisch verlengd.

Service Bus omgaat met een eigen verontreinigd wachtrij die niet kunnen worden beheerd of geconfigureerd door de WebJobs SDK. 

### <a name="string-queue-message"></a>Tekenreeks wachtrijbericht
Het volgende codevoorbeeld leest een wachtrijbericht die een tekenreeks bevat en de tekenreeks naar het dashboard WebJobs SDK wordt geschreven.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Opmerking:** als u de berichten in wachtrij plaatsen in een toepassing die geen gebruik maakt van de WebJobs SDK maakt, controleert u of in te stellen [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) op 'text/plain'.

### <a name="poco-queue-message"></a>POCO wachtrijbericht
De SDK wordt automatisch een wachtrijbericht met JSON voor een POCO deserialiseren [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type. Het volgende codevoorbeeld leest het bericht van een wachtrij met een `BlobInformation` object waarvoor een `BlobName` eigenschap:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

Zie voor codevoorbeelden waarin wordt getoond hoe eigenschappen van de POCO gebruiken om te werken met blobs en tabellen in dezelfde functie, de [opslag wachtrijen versie van dit artikel](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Als uw code die het bericht uit de wachtrij maakt geen gebruik van de WebJobs SDK, moet u de code is vergelijkbaar met het volgende voorbeeld gebruiken:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Typen ServiceBusTrigger werkt met
Naast `string` en POCO-typen, kunt u de `ServiceBusTrigger` kenmerk met een bytematrix of een `BrokeredMessage` object.

## <a id="create"></a>Het maken van Service Bus-berichtenwachtrij-berichten
Schrijven van een functie die een nieuwe wachtrij bericht gebruik genereert de `ServiceBus` kenmerk en in de naam van de wachtrij voor de kenmerkconstructor. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Een enkel wachtrijbericht in een niet-async-functie maken
Het volgende codevoorbeeld maakt gebruik van een output-parameter voor het maken van een nieuw bericht in de wachtrij met de naam 'outputqueue' met dezelfde inhoud als het bericht ontvangen in de wachtrij met de naam 'inputqueue'.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

De output-parameter voor het maken van een enkel wachtrijbericht mag geen van de volgende typen:

* `string`
* `byte[]`
* `BrokeredMessage`
* Een serialiseerbare POCO-type dat u opgeeft. Automatisch geserialiseerd als JSON.

Voor de parameters van het type POCO, wordt een wachtrijbericht altijd gemaakt wanneer de functie wordt beëindigd. Als de parameter null is, maakt de SDK een wachtrijbericht dat null wordt geretourneerd wanneer het bericht wordt ontvangen en gedeserialiseerd. Voor andere typen als de parameter null is is geen wachtrijbericht gemaakt.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Maken van meerdere berichten in wachtrij plaatsen of in een async-functies
Gebruik voor het maken van meerdere berichten de `ServiceBus` met kenmerk `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende codevoorbeeld:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Het bericht voor elke wachtrij wordt onmiddellijk gemaakt wanneer de `Add` methode wordt aangeroepen.

## <a id="topics"></a>Werken met Service Bus-onderwerpen
Gebruik voor het schrijven van een functie die de SDK-aanroepen wanneer een bericht wordt ontvangen op een Service Bus-onderwerp, de `ServiceBusTrigger` kenmerk met de constructor die onderwerpnaam en de naam van het abonnement, zoals wordt weergegeven in het volgende codevoorbeeld:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

Gebruik voor het maken van een bericht over een onderwerp de `ServiceBus` kenmerk met de naam van een onderwerp dezelfde manier als u deze met de naam van een wachtrij gebruiken.

## <a name="features-added-in-release-11"></a>Functies die zijn toegevoegd in versie 1.1
De volgende functies zijn toegevoegd in versie 1.1:

* Toestaan grondige aanpassing van de berichtverwerking `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`biedt ondersteuning voor aanpassing van de Service Bus `MessagingFactory` en `NamespaceManager`.
* Een `MessageProcessor` strategiepatroon kunt u een processor per wachtrij/onderwerp opgeven.
* Verwerking gelijktijdigheid van bericht is standaard ondersteund. 
* Eenvoudige aanpassing van `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.
* Toestaan dat [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) moet worden opgegeven op `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (voor scenario's waarbij u mogelijk geen rechten beheren). Houd er rekening mee dat Azure WebJobs kan niet automatisch worden ingericht, niet-bestaande wachtrijen en onderwerpen zonder AccessRights beheren.

## <a id="queues"></a>Verwante onderwerpen de opslag wachtrijen how-to artikel vallen
Zie voor meer informatie over WebJobs SDK scenario's die niet specifiek zijn voor Service Bus [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Onderwerpen in dit artikel omvatten het volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken
* De SDK-verbindingsreeksen instellen in code
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Een functie handmatig activeren
* Schrijven Logboeken

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding is opgegeven codevoorbeelden die laten hoe algemene scenario's zien voor het werken met Azure Service Bus verwerkt. Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

