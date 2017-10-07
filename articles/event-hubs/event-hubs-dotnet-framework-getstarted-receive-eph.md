---
title: aaaReceive gebeurtenissen van Azure Event Hubs met behulp van .NET Framework Hallo | Microsoft Docs
description: Volg deze zelfstudie tooreceive gebeurtenissen van Azure Event Hubs met behulp van Hallo .NET Framework.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="b934e-103">Ontvangen van gebeurtenissen van Azure Event Hubs met behulp van Hallo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b934e-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="b934e-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="b934e-104">Introduction</span></span>

<span data-ttu-id="b934e-105">Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b934e-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="b934e-106">Nadat u gegevens in Event Hubs hebt verzameld, kunt u Hallo gegevensopslag met behulp van een opslagcluster of transformeren met een realtime analytics-provider.</span><span class="sxs-lookup"><span data-stu-id="b934e-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="b934e-107">Deze gebeurtenis grootschalige verzamelen en verwerken mogelijkheid is een belangrijk onderdeel van moderne toepassingsarchitecturen inclusief Hallo Internet der dingen (IoT).</span><span class="sxs-lookup"><span data-stu-id="b934e-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="b934e-108">Deze zelfstudie laat zien hoe een .NET Framework toowrite consoletoepassing die berichten ontvangt van een event hub met Hallo  **[Gebeurtenisprocessorhost][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="b934e-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="b934e-109">toosend gebeurtenissen met Hallo .NET Framework, Zie Hallo [gebeurtenissen verzenden tooAzure Event Hubs met behulp van .NET Framework Hallo](event-hubs-dotnet-framework-getstarted-send.md) artikel, of klik op de juiste Hallo verzenden taal in Hallo links inhoudsopgave.</span><span class="sxs-lookup"><span data-stu-id="b934e-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="b934e-110">Hallo [Gebeurtenisprocessorhost] [ EventProcessorHost] is een .NET-klasse die de ontvangende gebeurtenissen van event hubs vereenvoudigt door permanente controlepunten beheren en parallelle ontvangst van deze event hubs.</span><span class="sxs-lookup"><span data-stu-id="b934e-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="b934e-111">Met behulp van Hallo [Gebeurtenisprocessorhost][Event Processor Host], kunt u gebeurtenissen splitsen over meerdere ontvangers, zelfs wanneer deze wordt gehost in verschillende knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b934e-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="b934e-112">Dit voorbeeld ziet u hoe toouse hello [Gebeurtenisprocessorhost] [ EventProcessorHost] voor één ontvanger.</span><span class="sxs-lookup"><span data-stu-id="b934e-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="b934e-113">Hallo [Scale-out gebeurtenisverwerking] [ Scale out Event Processing with Event Hubs] voorbeeld toont hoe toouse hello [Gebeurtenisprocessorhost] [ EventProcessorHost] met meerdere ontvangers.</span><span class="sxs-lookup"><span data-stu-id="b934e-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b934e-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b934e-114">Prerequisites</span></span>

<span data-ttu-id="b934e-115">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="b934e-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="b934e-116">[Microsoft Visual Studio 2015 of hoger](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b934e-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="b934e-117">Hallo schermopnamen in deze zelfstudie gebruiken Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b934e-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="b934e-118">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b934e-118">An active Azure account.</span></span> <span data-ttu-id="b934e-119">Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="b934e-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b934e-120">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b934e-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="b934e-121">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="b934e-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="b934e-122">de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte van Event Hubs typt en beheerreferenties Hallo uw toepassing moet toocommunicate met Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="b934e-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="b934e-123">toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), gaat u verder met de Hallo stappen in deze zelfstudie te volgen.</span><span class="sxs-lookup"><span data-stu-id="b934e-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b934e-124">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="b934e-124">Create an Azure Storage account</span></span>

<span data-ttu-id="b934e-125">Hallo toouse [Gebeurtenisprocessorhost][EventProcessorHost], hebt u een [Azure Storage-account][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="b934e-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="b934e-126">Meld u aan toohello [Azure-portal][Azure portal], en klik op **nieuw** op Hallo linksboven welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="b934e-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="b934e-127">Klik op **Opslag** en klik vervolgens op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="b934e-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="b934e-128">In Hallo **storage-account maken** blade een naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b934e-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="b934e-129">Een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="b934e-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="b934e-130">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="b934e-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="b934e-131">In de lijst van de Hallo met storage-accounts, klikt u op Hallo nieuw opslagaccount gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b934e-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="b934e-132">Klik in de blade opslagaccount hello **toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="b934e-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="b934e-133">Hallo-waarde van kopiëren **key1** toouse verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b934e-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="b934e-134">Een consoletoepassing voor ontvangers maken</span><span class="sxs-lookup"><span data-stu-id="b934e-134">Create a receiver console application</span></span>

1. <span data-ttu-id="b934e-135">Maak in Visual Studio een nieuw Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="b934e-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="b934e-136">Naam Hallo project **ontvanger**.</span><span class="sxs-lookup"><span data-stu-id="b934e-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="b934e-137">Klik in Solution Explorer met de rechtermuisknop op Hallo **ontvanger** project en klik vervolgens op **NuGet-pakketten beheren voor oplossing**.</span><span class="sxs-lookup"><span data-stu-id="b934e-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="b934e-138">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="b934e-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="b934e-139">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="b934e-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="b934e-140">Visual Studio downloadt, installeert en voegt u een verwijzing toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), inclusief alle afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="b934e-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="b934e-141">Klik met de rechtermuisknop Hallo **ontvanger** project, klikt u op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="b934e-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="b934e-142">Naam nieuwe klasse Hallo **SimpleEventProcessor**, en klik vervolgens op **toevoegen** toocreate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="b934e-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="b934e-143">Hallo instructies Hallo boven aan het bestand simpleeventprocessor.cs Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b934e-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="b934e-144">Vervang vervolgens, na de code voor de instantie van klasse Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="b934e-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="b934e-145">Deze klasse wordt aangeroepen door Hallo **EventProcessorHost** tooprocess gebeurtenissen ontvangen van Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="b934e-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="b934e-146">Hallo `SimpleEventProcessor` klasse gebruikt een stopwatch tooperiodically aanroep Hallo controlepuntmethode op Hallo **EventProcessorHost** context.</span><span class="sxs-lookup"><span data-stu-id="b934e-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="b934e-147">Deze verwerking zorgt ervoor dat, als de ontvanger Hallo opnieuw wordt opgestart, niet meer dan vijf minuten verliest van de verwerking van werkitems.</span><span class="sxs-lookup"><span data-stu-id="b934e-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="b934e-148">In Hallo **programma** klasse, voeg de volgende Hallo `using` instructie Hallo boven aan het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="b934e-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="b934e-149">Vervang vervolgens Hallo `Main` methode in Hallo `Program` klasse met de volgende code Hallo, vervangen door de naam van Hallo event hub en Hallo naamruimteniveau verbinding tekenreeks die u eerder hebt opgeslagen en storage-account en de sleutel die u hebt gekopieerd in Hallo Hallo vorige secties.</span><span class="sxs-lookup"><span data-stu-id="b934e-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="b934e-150">Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="b934e-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="b934e-151">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b934e-151">Congratulations!</span></span> <span data-ttu-id="b934e-152">U hebt nu berichten ontvangen van een event hub met Hallo Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="b934e-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="b934e-153">In deze zelfstudie wordt één exemplaar van [EventProcessorHost][EventProcessorHost] gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b934e-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="b934e-154">tooincrease doorvoer, het wordt aanbevolen dat u meerdere exemplaren van [EventProcessorHost][EventProcessorHost], zoals weergegeven in Hallo [schaal uit de verwerking van gebeurtenissen] [schaal uit de verwerking van gebeurtenissen] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b934e-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="b934e-155">In deze gevallen hello verschillende exemplaren samen automatisch met elkaar tooload saldo Hallo ontvangen gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b934e-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="b934e-156">Als u wilt dat meerdere ontvangers tooeach proces *alle* Hallo gebeurtenissen, moet u Hallo **ConsumerGroup** concept.</span><span class="sxs-lookup"><span data-stu-id="b934e-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="b934e-157">Wanneer u gebeurtenissen ontvangen van andere computers, komt dit mogelijk handig toospecify namen voor [EventProcessorHost] [ EventProcessorHost] exemplaren op basis van het Hallo-machines (of rollen) in dat ze zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b934e-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="b934e-158">Zie voor meer informatie over deze onderwerpen Hallo [overzicht van Event Hubs] [ Event Hubs overview] en Hallo [Programmeerhandleiding voor Event Hubs] [ Event Hubs Programming Guide] onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b934e-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b934e-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b934e-159">Next steps</span></span>

<span data-ttu-id="b934e-160">Nu dat u een werkende toepassing die een event hub maakt en gegevens verzendt en ontvangt hebt gemaakt, kunt u meer informatie via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b934e-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="b934e-161">[EventProcessorHost][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="b934e-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="b934e-162">[Event Hubs-overzicht][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="b934e-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="b934e-163">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b934e-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
