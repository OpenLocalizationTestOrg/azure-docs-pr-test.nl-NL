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
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="948cb-103">Azure Service Bus gebruiken met de WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="948cb-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="948cb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="948cb-104">Overview</span></span>
<span data-ttu-id="948cb-105">Deze handleiding bevat C#-codevoorbeelden die laten hoe een proces wordt geactiveerd zien wanneer een Azure Service Bus-bericht wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="948cb-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="948cb-106">De code voorbeelden gebruik [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="948cb-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="948cb-107">De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="948cb-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="948cb-108">De codefragmenten alleen weergeven functies, niet de code die wordt gemaakt de `JobHost` object zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="948cb-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="948cb-109">Een [volledige Service Bus-codevoorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in de azure-API-sdk-samples-opslagplaats op GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="948cb-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="948cb-110"><a id="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="948cb-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="948cb-111">Werken met Service Bus die u hebt voor het installeren van de [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet-pakket naast de andere WebJobs SDK-pakketten.</span><span class="sxs-lookup"><span data-stu-id="948cb-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="948cb-112">Hebt u ook de verbindingsreeks AzureWebJobsServiceBus naast de storage-verbindingsreeksen instellen.</span><span class="sxs-lookup"><span data-stu-id="948cb-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="948cb-113">U kunt dit doen het `connectionStrings` gedeelte van het bestand App.config, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="948cb-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="948cb-114">Zie voor een voorbeeldproject met de instelling voor de Service Bus-tekenreeks in het bestand App.config [Service Bus-voorbeeld](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="948cb-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="948cb-115">De verbindingsreeksen kunnen ook worden ingesteld in de Azure runtimeomgeving, die vervolgens het App.config-instellingen worden genegeerd als de webtaak wordt uitgevoerd in Azure. Zie voor meer informatie [aan de slag met de WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="948cb-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="948cb-116"><a id="trigger"></a>Het activeren van een functie als een Service Bus-wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="948cb-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="948cb-117">Voor het schrijven van een functie waarmee de WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruik de `ServiceBusTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="948cb-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="948cb-118">De kenmerkconstructor heeft een parameter met de naam van de wachtrij om te pollen.</span><span class="sxs-lookup"><span data-stu-id="948cb-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="948cb-119">De werking van ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="948cb-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="948cb-120">De SDK ontvangt een bericht in `PeekLock` modus en aanroepen `Complete` op het bericht als de functie wordt voltooid of aanroepen `Abandon` als de functie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="948cb-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="948cb-121">Als de functie wordt uitgevoerd langer dan de `PeekLock` een time-out opgetreden, de vergrendeling wordt automatisch verlengd.</span><span class="sxs-lookup"><span data-stu-id="948cb-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="948cb-122">Service Bus omgaat met een eigen verontreinigd wachtrij die niet kunnen worden beheerd of geconfigureerd door de WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="948cb-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="948cb-123">Tekenreeks wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="948cb-123">String queue message</span></span>
<span data-ttu-id="948cb-124">Het volgende codevoorbeeld leest een wachtrijbericht die een tekenreeks bevat en de tekenreeks naar het dashboard WebJobs SDK wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="948cb-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="948cb-125">**Opmerking:** als u de berichten in wachtrij plaatsen in een toepassing die geen gebruik maakt van de WebJobs SDK maakt, controleert u of in te stellen [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) op 'text/plain'.</span><span class="sxs-lookup"><span data-stu-id="948cb-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="948cb-126">POCO wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="948cb-126">POCO queue message</span></span>
<span data-ttu-id="948cb-127">De SDK wordt automatisch een wachtrijbericht met JSON voor een POCO deserialiseren [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span><span class="sxs-lookup"><span data-stu-id="948cb-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="948cb-128">Het volgende codevoorbeeld leest het bericht van een wachtrij met een `BlobInformation` object waarvoor een `BlobName` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="948cb-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="948cb-129">Zie voor codevoorbeelden waarin wordt getoond hoe eigenschappen van de POCO gebruiken om te werken met blobs en tabellen in dezelfde functie, de [opslag wachtrijen versie van dit artikel](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="948cb-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="948cb-130">Als uw code die het bericht uit de wachtrij maakt geen gebruik van de WebJobs SDK, moet u de code is vergelijkbaar met het volgende voorbeeld gebruiken:</span><span class="sxs-lookup"><span data-stu-id="948cb-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="948cb-131">Typen ServiceBusTrigger werkt met</span><span class="sxs-lookup"><span data-stu-id="948cb-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="948cb-132">Naast `string` en POCO-typen, kunt u de `ServiceBusTrigger` kenmerk met een bytematrix of een `BrokeredMessage` object.</span><span class="sxs-lookup"><span data-stu-id="948cb-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="948cb-133"><a id="create"></a>Het maken van Service Bus-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="948cb-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="948cb-134">Schrijven van een functie die een nieuwe wachtrij bericht gebruik genereert de `ServiceBus` kenmerk en in de naam van de wachtrij voor de kenmerkconstructor.</span><span class="sxs-lookup"><span data-stu-id="948cb-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="948cb-135">Een enkel wachtrijbericht in een niet-async-functie maken</span><span class="sxs-lookup"><span data-stu-id="948cb-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="948cb-136">Het volgende codevoorbeeld maakt gebruik van een output-parameter voor het maken van een nieuw bericht in de wachtrij met de naam 'outputqueue' met dezelfde inhoud als het bericht ontvangen in de wachtrij met de naam 'inputqueue'.</span><span class="sxs-lookup"><span data-stu-id="948cb-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="948cb-137">De output-parameter voor het maken van een enkel wachtrijbericht mag geen van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="948cb-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="948cb-138">Een serialiseerbare POCO-type dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="948cb-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="948cb-139">Automatisch geserialiseerd als JSON.</span><span class="sxs-lookup"><span data-stu-id="948cb-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="948cb-140">Voor de parameters van het type POCO, wordt een wachtrijbericht altijd gemaakt wanneer de functie wordt beëindigd. Als de parameter null is, maakt de SDK een wachtrijbericht dat null wordt geretourneerd wanneer het bericht wordt ontvangen en gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="948cb-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="948cb-141">Voor andere typen als de parameter null is is geen wachtrijbericht gemaakt.</span><span class="sxs-lookup"><span data-stu-id="948cb-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="948cb-142">Maken van meerdere berichten in wachtrij plaatsen of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="948cb-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="948cb-143">Gebruik voor het maken van meerdere berichten de `ServiceBus` met kenmerk `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="948cb-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="948cb-144">Het bericht voor elke wachtrij wordt onmiddellijk gemaakt wanneer de `Add` methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="948cb-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="948cb-145"><a id="topics"></a>Werken met Service Bus-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="948cb-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="948cb-146">Gebruik voor het schrijven van een functie die de SDK-aanroepen wanneer een bericht wordt ontvangen op een Service Bus-onderwerp, de `ServiceBusTrigger` kenmerk met de constructor die onderwerpnaam en de naam van het abonnement, zoals wordt weergegeven in het volgende codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="948cb-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="948cb-147">Gebruik voor het maken van een bericht over een onderwerp de `ServiceBus` kenmerk met de naam van een onderwerp dezelfde manier als u deze met de naam van een wachtrij gebruiken.</span><span class="sxs-lookup"><span data-stu-id="948cb-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="948cb-148">Functies die zijn toegevoegd in versie 1.1</span><span class="sxs-lookup"><span data-stu-id="948cb-148">Features added in release 1.1</span></span>
<span data-ttu-id="948cb-149">De volgende functies zijn toegevoegd in versie 1.1:</span><span class="sxs-lookup"><span data-stu-id="948cb-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="948cb-150">Toestaan grondige aanpassing van de berichtverwerking `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="948cb-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="948cb-151">`MessagingProvider`biedt ondersteuning voor aanpassing van de Service Bus `MessagingFactory` en `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="948cb-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="948cb-152">Een `MessageProcessor` strategiepatroon kunt u een processor per wachtrij/onderwerp opgeven.</span><span class="sxs-lookup"><span data-stu-id="948cb-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="948cb-153">Verwerking gelijktijdigheid van bericht is standaard ondersteund.</span><span class="sxs-lookup"><span data-stu-id="948cb-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="948cb-154">Eenvoudige aanpassing van `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="948cb-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="948cb-155">Toestaan dat [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) moet worden opgegeven op `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (voor scenario's waarbij u mogelijk geen rechten beheren).</span><span class="sxs-lookup"><span data-stu-id="948cb-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="948cb-156">Houd er rekening mee dat Azure WebJobs kan niet automatisch worden ingericht, niet-bestaande wachtrijen en onderwerpen zonder AccessRights beheren.</span><span class="sxs-lookup"><span data-stu-id="948cb-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="948cb-157"><a id="queues"></a>Verwante onderwerpen de opslag wachtrijen how-to artikel vallen</span><span class="sxs-lookup"><span data-stu-id="948cb-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="948cb-158">Zie voor meer informatie over WebJobs SDK scenario's die niet specifiek zijn voor Service Bus [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="948cb-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="948cb-159">Onderwerpen in dit artikel omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="948cb-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="948cb-160">Async-functies</span><span class="sxs-lookup"><span data-stu-id="948cb-160">Async functions</span></span>
* <span data-ttu-id="948cb-161">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="948cb-161">Multiple instances</span></span>
* <span data-ttu-id="948cb-162">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="948cb-162">Graceful shutdown</span></span>
* <span data-ttu-id="948cb-163">Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="948cb-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="948cb-164">De SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="948cb-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="948cb-165">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="948cb-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="948cb-166">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="948cb-166">Trigger a function manually</span></span>
* <span data-ttu-id="948cb-167">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="948cb-167">Write logs</span></span>

## <span data-ttu-id="948cb-168"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="948cb-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="948cb-169">Deze handleiding is opgegeven codevoorbeelden die laten hoe algemene scenario's zien voor het werken met Azure Service Bus verwerkt.</span><span class="sxs-lookup"><span data-stu-id="948cb-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="948cb-170">Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="948cb-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

