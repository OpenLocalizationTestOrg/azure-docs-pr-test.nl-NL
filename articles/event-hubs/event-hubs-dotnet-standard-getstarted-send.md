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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="ad319-103">Verzenden van berichten tooAzure Event Hubs in .NET standaard aan de slag</span><span class="sxs-lookup"><span data-stu-id="ad319-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="ad319-104">Dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="ad319-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="ad319-105">Deze zelfstudie laat zien hoe toowrite een consoletoepassing .NET Core waarmee een reeks verzonden berichten tooan event hub.</span><span class="sxs-lookup"><span data-stu-id="ad319-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="ad319-106">U kunt uitvoeren Hallo [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) oplossing als-, vervangt Hallo `EhConnectionString` en `EhEntityPath` tekenreeksen met de waarden van uw event hub.</span><span class="sxs-lookup"><span data-stu-id="ad319-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="ad319-107">Of u kunt volgen Hallo stappen in deze zelfstudie toocreate zelf.</span><span class="sxs-lookup"><span data-stu-id="ad319-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad319-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad319-108">Prerequisites</span></span>

* <span data-ttu-id="ad319-109">[Microsoft Visual Studio 2015 of 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ad319-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="ad319-110">Hallo-voorbeelden in deze zelfstudie Gebruik Visual Studio 2017, maar Visual Studio 2015 wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ad319-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="ad319-111">[.NET core Visual Studio 2015 of hulpprogramma's voor 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="ad319-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="ad319-112">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ad319-112">An Azure subscription.</span></span>
* <span data-ttu-id="ad319-113">Een event hub-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="ad319-113">An event hub namespace.</span></span>

<span data-ttu-id="ad319-114">toosend berichten tooan event hub, gebruiken we toowrite Visual Studio een C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="ad319-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="ad319-115">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="ad319-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="ad319-116">de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte voor Hallo event Hubtype en beheerreferenties Hallo dat uw toepassing toocommunicate met Hallo event hub moet.</span><span class="sxs-lookup"><span data-stu-id="ad319-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="ad319-117">toocreate een naamruimte en een event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), en vervolgens doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="ad319-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="ad319-118">Een consoletoepassing maken</span><span class="sxs-lookup"><span data-stu-id="ad319-118">Create a console application</span></span>

<span data-ttu-id="ad319-119">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad319-119">Start Visual Studio.</span></span> <span data-ttu-id="ad319-120">Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="ad319-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="ad319-121">Maak een consoletoepassing .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ad319-121">Create a .NET Core console application.</span></span>

![Nieuw project][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="ad319-123">Hallo Event Hubs NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="ad319-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="ad319-124">Hallo toevoegen [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET-bibliotheek NuGet-pakket tooyour standaardproject met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="ad319-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="ad319-125">Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="ad319-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ad319-126">Klik op Hallo **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.EventHubs' en selecteer Hallo **Microsoft.Azure.EventHubs** pakket.</span><span class="sxs-lookup"><span data-stu-id="ad319-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="ad319-127">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad319-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="ad319-128">Sommige code toosend berichten toohello event hub schrijven</span><span class="sxs-lookup"><span data-stu-id="ad319-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="ad319-129">Voeg de volgende Hallo `using` instructies toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad319-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="ad319-130">Toevoegen van constanten toohello `Program` klasse voor Hallo Event Hubs tekenreeks en entiteit verbindingspad (afzonderlijke event hub-naam).</span><span class="sxs-lookup"><span data-stu-id="ad319-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="ad319-131">Tijdelijke aanduidingen Hallo haakjes vervangen door Hallo juiste waarden die zijn verkregen tijdens het maken van Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="ad319-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="ad319-132">Voeg een nieuwe methode met de naam `MainAsync` toohello `Program` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="ad319-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

4. <span data-ttu-id="ad319-133">Voeg een nieuwe methode met de naam `SendMessagesToEventHub` toohello `Program` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="ad319-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

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

5. <span data-ttu-id="ad319-134">Hallo na code toohello toevoegen `Main` methode in Hallo `Program` klasse.</span><span class="sxs-lookup"><span data-stu-id="ad319-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="ad319-135">Zo zou het bestand Program.cs er moeten uitzien.</span><span class="sxs-lookup"><span data-stu-id="ad319-135">Here is what your Program.cs should look like.</span></span>

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

6. <span data-ttu-id="ad319-136">Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="ad319-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="ad319-137">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="ad319-137">Congratulations!</span></span> <span data-ttu-id="ad319-138">U hebt nu verzonden berichten tooan event hub.</span><span class="sxs-lookup"><span data-stu-id="ad319-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad319-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad319-139">Next steps</span></span>
<span data-ttu-id="ad319-140">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad319-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="ad319-141">Ontvangen van gebeurtenissen van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ad319-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="ad319-142">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="ad319-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ad319-143">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="ad319-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ad319-144">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ad319-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
