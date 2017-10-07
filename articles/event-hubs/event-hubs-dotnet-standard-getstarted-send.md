---
title: aaaSend gebeurtenissen tooAzure Event Hubs met behulp van standaard .NET | Microsoft Docs
description: Verzenden van gebeurtenissen tooEvent Hubs in .NET standaard aan de slag
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Verzenden van berichten tooAzure Event Hubs in .NET standaard aan de slag

> [!NOTE]
> Dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Deze zelfstudie laat zien hoe toowrite een consoletoepassing .NET Core waarmee een reeks verzonden berichten tooan event hub. U kunt uitvoeren Hallo [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) oplossing als-, vervangt Hallo `EhConnectionString` en `EhEntityPath` tekenreeksen met de waarden van uw event hub. Of u kunt volgen Hallo stappen in deze zelfstudie toocreate zelf.

## <a name="prerequisites"></a>Vereisten

* [Microsoft Visual Studio 2015 of 2017](http://www.visualstudio.com). Hallo-voorbeelden in deze zelfstudie Gebruik Visual Studio 2017, maar Visual Studio 2015 wordt ook ondersteund.
* [.NET core Visual Studio 2015 of hulpprogramma's voor 2017](http://www.microsoft.com/net/core).
* Een Azure-abonnement.
* Een event hub-naamruimte.

toosend berichten tooan event hub, gebruiken we toowrite Visual Studio een C#-consoletoepassing.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Een Event Hubs-naamruimte en een Event Hub maken

de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte voor Hallo event Hubtype en beheerreferenties Hallo dat uw toepassing toocommunicate met Hallo event hub moet. toocreate een naamruimte en een event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), en vervolgens doorgaan met de Hallo stappen te volgen.

## <a name="create-a-console-application"></a>Een consoletoepassing maken

Start Visual Studio. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**. Maak een consoletoepassing .NET Core.

![Nieuw project][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Hallo Event Hubs NuGet-pakket toevoegen

Hallo toevoegen [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET-bibliotheek NuGet-pakket tooyour standaardproject met de volgende stappen: 

1. Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.
2. Klik op Hallo **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.EventHubs' en selecteer Hallo **Microsoft.Azure.EventHubs** pakket. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Sommige code toosend berichten toohello event hub schrijven

1. Voeg de volgende Hallo `using` instructies toohello boven aan het bestand Program.cs Hallo.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Toevoegen van constanten toohello `Program` klasse voor Hallo Event Hubs tekenreeks en entiteit verbindingspad (afzonderlijke event hub-naam). Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo juiste waarden die zijn verkregen tijdens het maken van Hallo event hub.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Voeg een nieuwe methode met de naam `MainAsync` toohello `Program` klasse als volgt:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. Voeg een nieuwe methode met de naam `SendMessagesToEventHub` toohello `Program` klasse als volgt:

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. Hallo na code toohello toevoegen `Main` methode in Hallo `Program` klasse.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Zo zou het bestand Program.cs er moeten uitzien.

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.

Gefeliciteerd. U hebt nu verzonden berichten tooan event hub.

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Ontvangen van gebeurtenissen van Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
