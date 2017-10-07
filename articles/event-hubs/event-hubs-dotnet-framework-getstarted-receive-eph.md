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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Ontvangen van gebeurtenissen van Azure Event Hubs met behulp van Hallo .NET Framework

## <a name="introduction"></a>Inleiding

Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt. Nadat u gegevens in Event Hubs hebt verzameld, kunt u Hallo gegevensopslag met behulp van een opslagcluster of transformeren met een realtime analytics-provider. Deze gebeurtenis grootschalige verzamelen en verwerken mogelijkheid is een belangrijk onderdeel van moderne toepassingsarchitecturen inclusief Hallo Internet der dingen (IoT).

Deze zelfstudie laat zien hoe een .NET Framework toowrite consoletoepassing die berichten ontvangt van een event hub met Hallo  **[Gebeurtenisprocessorhost][EventProcessorHost]**. toosend gebeurtenissen met Hallo .NET Framework, Zie Hallo [gebeurtenissen verzenden tooAzure Event Hubs met behulp van .NET Framework Hallo](event-hubs-dotnet-framework-getstarted-send.md) artikel, of klik op de juiste Hallo verzenden taal in Hallo links inhoudsopgave.

Hallo [Gebeurtenisprocessorhost] [ EventProcessorHost] is een .NET-klasse die de ontvangende gebeurtenissen van event hubs vereenvoudigt door permanente controlepunten beheren en parallelle ontvangst van deze event hubs. Met behulp van Hallo [Gebeurtenisprocessorhost][Event Processor Host], kunt u gebeurtenissen splitsen over meerdere ontvangers, zelfs wanneer deze wordt gehost in verschillende knooppunten. Dit voorbeeld ziet u hoe toouse hello [Gebeurtenisprocessorhost] [ EventProcessorHost] voor één ontvanger. Hallo [Scale-out gebeurtenisverwerking] [ Scale out Event Processing with Event Hubs] voorbeeld toont hoe toouse hello [Gebeurtenisprocessorhost] [ EventProcessorHost] met meerdere ontvangers.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* [Microsoft Visual Studio 2015 of hoger](http://visualstudio.com). Hallo schermopnamen in deze zelfstudie gebruiken Visual Studio 2017.
* Een actief Azure-account. Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Een Event Hubs-naamruimte en een Event Hub maken

de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte van Event Hubs typt en beheerreferenties Hallo uw toepassing moet toocommunicate met Hallo event hub. toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), gaat u verder met de Hallo stappen in deze zelfstudie te volgen.

## <a name="create-an-azure-storage-account"></a>Een Azure Storage-account maken

Hallo toouse [Gebeurtenisprocessorhost][EventProcessorHost], hebt u een [Azure Storage-account][Azure Storage account]:

1. Meld u aan toohello [Azure-portal][Azure portal], en klik op **nieuw** op Hallo linksboven welkomstscherm.
2. Klik op **Opslag** en klik vervolgens op **Opslagaccount**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. In Hallo **storage-account maken** blade een naam voor het Hallo-opslagaccount. Een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource. Klik vervolgens op **Maken**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. In de lijst van de Hallo met storage-accounts, klikt u op Hallo nieuw opslagaccount gemaakt.
5. Klik in de blade opslagaccount hello **toegangssleutels**. Hallo-waarde van kopiëren **key1** toouse verderop in deze zelfstudie.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Een consoletoepassing voor ontvangers maken

1. Maak in Visual Studio een nieuw Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **ontvanger**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **ontvanger** project en klik vervolgens op **NuGet-pakketten beheren voor oplossing**.
3. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio downloadt, installeert en voegt u een verwijzing toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), inclusief alle afhankelijkheden ervan.
4. Klik met de rechtermuisknop Hallo **ontvanger** project, klikt u op **toevoegen**, en klik vervolgens op **klasse**. Naam nieuwe klasse Hallo **SimpleEventProcessor**, en klik vervolgens op **toevoegen** toocreate Hallo-klasse.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Hallo instructies Hallo boven aan het bestand simpleeventprocessor.cs Hallo volgende toevoegen:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Vervang vervolgens, na de code voor de instantie van klasse Hallo HALLO hallo:
    
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
    
  Deze klasse wordt aangeroepen door Hallo **EventProcessorHost** tooprocess gebeurtenissen ontvangen van Hallo event hub. Hallo `SimpleEventProcessor` klasse gebruikt een stopwatch tooperiodically aanroep Hallo controlepuntmethode op Hallo **EventProcessorHost** context. Deze verwerking zorgt ervoor dat, als de ontvanger Hallo opnieuw wordt opgestart, niet meer dan vijf minuten verliest van de verwerking van werkitems.
6. In Hallo **programma** klasse, voeg de volgende Hallo `using` instructie Hallo boven aan het Hallo-bestand:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Vervang vervolgens Hallo `Main` methode in Hallo `Program` klasse met de volgende code Hallo, vervangen door de naam van Hallo event hub en Hallo naamruimteniveau verbinding tekenreeks die u eerder hebt opgeslagen en storage-account en de sleutel die u hebt gekopieerd in Hallo Hallo vorige secties. 
    
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

7. Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.
  
Gefeliciteerd. U hebt nu berichten ontvangen van een event hub met Hallo Event Processor Host.


> [!NOTE]
> In deze zelfstudie wordt één exemplaar van [EventProcessorHost][EventProcessorHost] gebruikt. tooincrease doorvoer, het wordt aanbevolen dat u meerdere exemplaren van [EventProcessorHost][EventProcessorHost], zoals weergegeven in Hallo [schaal uit de verwerking van gebeurtenissen] [schaal uit de verwerking van gebeurtenissen] voorbeeld. In deze gevallen hello verschillende exemplaren samen automatisch met elkaar tooload saldo Hallo ontvangen gebeurtenissen. Als u wilt dat meerdere ontvangers tooeach proces *alle* Hallo gebeurtenissen, moet u Hallo **ConsumerGroup** concept. Wanneer u gebeurtenissen ontvangen van andere computers, komt dit mogelijk handig toospecify namen voor [EventProcessorHost] [ EventProcessorHost] exemplaren op basis van het Hallo-machines (of rollen) in dat ze zijn geïmplementeerd. Zie voor meer informatie over deze onderwerpen Hallo [overzicht van Event Hubs] [ Event Hubs overview] en Hallo [Programmeerhandleiding voor Event Hubs] [ Event Hubs Programming Guide] onderwerpen.
> 
> 

## <a name="next-steps"></a>Volgende stappen

Nu dat u een werkende toepassing die een event hub maakt en gegevens verzendt en ontvangt hebt gemaakt, kunt u meer informatie via Hallo koppelingen te volgen:

* [EventProcessorHost][Event Processor Host]
* [Event Hubs-overzicht][Event Hubs overview]
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

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
