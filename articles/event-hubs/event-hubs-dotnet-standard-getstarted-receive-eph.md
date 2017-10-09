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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="92ec3-103">Ontvangen van berichten Hello Event Processor Host in .NET standaard aan de slag</span><span class="sxs-lookup"><span data-stu-id="92ec3-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="92ec3-104">Dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="92ec3-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="92ec3-105">Deze zelfstudie laat zien hoe een .NET Core toowrite consoletoepassing die berichten ontvangt van een event hub met behulp van **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="92ec3-106">U kunt uitvoeren Hallo [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) oplossing-Hallo tekenreeksen is vervangen door uw event hub en storage-account waarden.</span><span class="sxs-lookup"><span data-stu-id="92ec3-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="92ec3-107">Of u kunt volgen Hallo stappen in deze zelfstudie toocreate zelf.</span><span class="sxs-lookup"><span data-stu-id="92ec3-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92ec3-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92ec3-108">Prerequisites</span></span>

* <span data-ttu-id="92ec3-109">[Microsoft Visual Studio 2015 of 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="92ec3-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="92ec3-110">Hallo-voorbeelden in deze zelfstudie Gebruik Visual Studio 2017, maar Visual Studio 2015 wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="92ec3-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="92ec3-111">[.NET core Visual Studio 2015 of hulpprogramma's voor 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="92ec3-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="92ec3-112">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="92ec3-112">An Azure subscription.</span></span>
* <span data-ttu-id="92ec3-113">Een Azure Event Hubs-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="92ec3-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="92ec3-114">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="92ec3-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="92ec3-115">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="92ec3-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="92ec3-116">de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte voor Hallo Event Hubs typt en beheerreferenties Hallo dat uw toepassing toocommunicate met Hallo event hub moet.</span><span class="sxs-lookup"><span data-stu-id="92ec3-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="92ec3-117">toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), en vervolgens doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="92ec3-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="92ec3-118">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="92ec3-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="92ec3-119">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92ec3-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="92ec3-120">Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **nieuw**, klikt u op **opslag**, en klik vervolgens op **Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="92ec3-121">Hallo-velden in de blade opslagaccount hello, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Storage-account maken][1]

4. <span data-ttu-id="92ec3-123">Nadat u Hallo Zie **implementaties is geslaagd** bericht wordt weergegeven, klikt u op naam van nieuw opslagaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="92ec3-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="92ec3-124">In Hallo **Essentials** blade, klikt u op **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="92ec3-125">Wanneer Hallo **Blob-service** blade wordt geopend, klikt u op **+ Container** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="92ec3-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="92ec3-126">Geef een naam op Hallo-container en sluit vervolgens Hallo **Blob-service** blade.</span><span class="sxs-lookup"><span data-stu-id="92ec3-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="92ec3-127">Klik op **toegangssleutels** in het Hallo links blade en kopiëren Hallo van Hallo storage-container, Hallo storage-account en Hallo-waarde van **key1**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="92ec3-128">Deze waarden tooNotepad of andere tijdelijke locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="92ec3-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="92ec3-129">Een consoletoepassing maken</span><span class="sxs-lookup"><span data-stu-id="92ec3-129">Create a console application</span></span>

<span data-ttu-id="92ec3-130">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92ec3-130">Start Visual Studio.</span></span> <span data-ttu-id="92ec3-131">Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="92ec3-132">Maak een consoletoepassing .NET Core.</span><span class="sxs-lookup"><span data-stu-id="92ec3-132">Create a .NET Core console application.</span></span>

![Nieuw project][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="92ec3-134">Hallo Event Hubs NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="92ec3-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="92ec3-135">Hallo toevoegen [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) en [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET-bibliotheek NuGet-pakketten tooyour standaardproject met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="92ec3-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="92ec3-136">Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="92ec3-137">Klik op Hallo **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.EventHubs' en selecteer Hallo **Microsoft.Azure.EventHubs** pakket.</span><span class="sxs-lookup"><span data-stu-id="92ec3-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="92ec3-138">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92ec3-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="92ec3-139">Herhaal stap 1 en 2 en installeer Hallo **Microsoft.Azure.EventHubs.Processor** pakket.</span><span class="sxs-lookup"><span data-stu-id="92ec3-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="92ec3-140">Hallo IEventProcessor-interface implementeren</span><span class="sxs-lookup"><span data-stu-id="92ec3-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="92ec3-141">Klik in Solution Explorer met de rechtermuisknop op Hallo-project op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="92ec3-142">Naam nieuwe klasse Hallo **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="92ec3-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="92ec3-143">Open Hallo bestand simpleeventprocessor.cs en voeg de volgende Hallo `using` instructies toohello boven in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="92ec3-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="92ec3-144">Implementeer Hallo `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="92ec3-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="92ec3-145">Vervang de volledige inhoud Hallo Hallo `SimpleEventProcessor` klasse Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="92ec3-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="92ec3-146">Schrijven van een methode hoofdconsole die gebruikmaakt van hello SimpleEventProcessor klasse tooreceive-berichten</span><span class="sxs-lookup"><span data-stu-id="92ec3-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="92ec3-147">Voeg de volgende Hallo `using` instructies toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="92ec3-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="92ec3-148">Toevoegen van constanten toohello `Program` klasse voor Hallo event hub-verbindingsreeks, naam event hub, container opslagaccountnaam, opslagaccountnaam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="92ec3-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="92ec3-149">Hallo code te volgen en Hallo tijdelijke aanduidingen vervangt met de bijbehorende waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="92ec3-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="92ec3-150">Voeg een nieuwe methode met de naam `MainAsync` toohello `Program` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="92ec3-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

3. <span data-ttu-id="92ec3-151">Toevoegen van de volgende regel code toohello hello `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="92ec3-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="92ec3-152">Zo zou het bestand Program.cs er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="92ec3-152">Here is what your Program.cs file should look like:</span></span>

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

4. <span data-ttu-id="92ec3-153">Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="92ec3-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="92ec3-154">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="92ec3-154">Congratulations!</span></span> <span data-ttu-id="92ec3-155">U hebt nu berichten ontvangen van een event hub met behulp van Hallo Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="92ec3-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92ec3-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92ec3-156">Next steps</span></span>
<span data-ttu-id="92ec3-157">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92ec3-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="92ec3-158">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="92ec3-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="92ec3-159">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="92ec3-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="92ec3-160">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="92ec3-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
