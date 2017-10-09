---
title: aaaReceive gebeurtenissen van Azure Event Hubs met behulp van standaard .NET | Microsoft Docs
description: Ontvangen van berichten Hello EventProcessorHost in .NET standaard aan de slag
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Ontvangen van berichten Hello Event Processor Host in .NET standaard aan de slag

> [!NOTE]
> Dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Deze zelfstudie laat zien hoe een .NET Core toowrite consoletoepassing die berichten ontvangt van een event hub met behulp van **EventProcessorHost**. U kunt uitvoeren Hallo [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) oplossing-Hallo tekenreeksen is vervangen door uw event hub en storage-account waarden. Of u kunt volgen Hallo stappen in deze zelfstudie toocreate zelf.

## <a name="prerequisites"></a>Vereisten

* [Microsoft Visual Studio 2015 of 2017](http://www.visualstudio.com). Hallo-voorbeelden in deze zelfstudie Gebruik Visual Studio 2017, maar Visual Studio 2015 wordt ook ondersteund.
* [.NET core Visual Studio 2015 of hulpprogramma's voor 2017](http://www.microsoft.com/net/core).
* Een Azure-abonnement.
* Een Azure Event Hubs-naamruimte.
* Een Azure Storage-account.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Een Event Hubs-naamruimte en een Event Hub maken  

de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte voor Hallo Event Hubs typt en beheerreferenties Hallo dat uw toepassing toocommunicate met Hallo event hub moet. toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), en vervolgens doorgaan met de Hallo stappen te volgen.  

## <a name="create-an-azure-storage-account"></a>Een Azure-opslagaccount maken  

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).  
2. Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **nieuw**, klikt u op **opslag**, en klik vervolgens op **Storage-Account**.  
3. Hallo-velden in de blade opslagaccount hello, en klik vervolgens op **maken**.

    ![Storage-account maken][1]

4. Nadat u Hallo Zie **implementaties is geslaagd** bericht wordt weergegeven, klikt u op naam van nieuw opslagaccount Hallo Hallo. In Hallo **Essentials** blade, klikt u op **Blobs**. Wanneer Hallo **Blob-service** blade wordt geopend, klikt u op **+ Container** Hallo bovenaan. Geef een naam op Hallo-container en sluit vervolgens Hallo **Blob-service** blade.  
5. Klik op **toegangssleutels** in het Hallo links blade en kopiëren Hallo van Hallo storage-container, Hallo storage-account en Hallo-waarde van **key1**. Deze waarden tooNotepad of andere tijdelijke locatie opslaan.  

## <a name="create-a-console-application"></a>Een consoletoepassing maken

Start Visual Studio. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**. Maak een consoletoepassing .NET Core.

![Nieuw project][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Hallo Event Hubs NuGet-pakket toevoegen

Hallo toevoegen [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) en [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET-bibliotheek NuGet-pakketten tooyour standaardproject met de volgende stappen: 

1. Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.
2. Klik op Hallo **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.EventHubs' en selecteer Hallo **Microsoft.Azure.EventHubs** pakket. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.
3. Herhaal stap 1 en 2 en installeer Hallo **Microsoft.Azure.EventHubs.Processor** pakket.

## <a name="implement-hello-ieventprocessor-interface"></a>Hallo IEventProcessor-interface implementeren

1. Klik in Solution Explorer met de rechtermuisknop op Hallo-project op **toevoegen**, en klik vervolgens op **klasse**. Naam nieuwe klasse Hallo **SimpleEventProcessor**.

2. Open Hallo bestand simpleeventprocessor.cs en voeg de volgende Hallo `using` instructies toohello boven in Hallo-bestand.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Implementeer Hallo `IEventProcessor` interface. Vervang de volledige inhoud Hallo Hallo `SimpleEventProcessor` klasse Hello code te volgen:

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Schrijven van een methode hoofdconsole die gebruikmaakt van hello SimpleEventProcessor klasse tooreceive-berichten

1. Voeg de volgende Hallo `using` instructies toohello boven aan het bestand Program.cs Hallo.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Toevoegen van constanten toohello `Program` klasse voor Hallo event hub-verbindingsreeks, naam event hub, container opslagaccountnaam, opslagaccountnaam en opslagaccountsleutel. Hallo code te volgen en Hallo tijdelijke aanduidingen vervangt met de bijbehorende waarden toevoegen.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Voeg een nieuwe methode met de naam `MainAsync` toohello `Program` klasse als volgt:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. Toevoegen van de volgende regel code toohello hello `Main` methode:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Zo zou het bestand Program.cs er moeten uitzien:

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.

Gefeliciteerd. U hebt nu berichten ontvangen van een event hub met behulp van Hallo Event Processor Host.

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
