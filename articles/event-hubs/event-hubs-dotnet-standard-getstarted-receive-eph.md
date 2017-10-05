---
title: Ontvangen van gebeurtenissen van Azure Event Hubs met behulp van standaard .NET | Microsoft Docs
description: Ontvangen van berichten met de EventProcessorHost in .NET standaard aan de slag
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="e2663-103">Ontvangen van berichten met de Gebeurtenisprocessorhost in .NET standaard aan de slag</span><span class="sxs-lookup"><span data-stu-id="e2663-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="e2663-104">Dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="e2663-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="e2663-105">Deze zelfstudie laat zien hoe u schrijft een consoletoepassing .NET Core die berichten van een event hub met behulp van ontvangt **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="e2663-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="e2663-106">U kunt uitvoeren de [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) oplossing als-is, de tekenreeksen vervangen door uw event hub en storage account waarden.</span><span class="sxs-lookup"><span data-stu-id="e2663-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="e2663-107">Of u kunt de stappen in deze zelfstudie voor het maken van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="e2663-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2663-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2663-108">Prerequisites</span></span>

* <span data-ttu-id="e2663-109">[Microsoft Visual Studio 2015 of 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e2663-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="e2663-110">De voorbeelden in deze zelfstudie Gebruik Visual Studio 2017, maar de Visual Studio 2015 wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e2663-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="e2663-111">[.NET core Visual Studio 2015 of hulpprogramma's voor 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="e2663-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="e2663-112">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2663-112">An Azure subscription.</span></span>
* <span data-ttu-id="e2663-113">Een Azure Event Hubs-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="e2663-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="e2663-114">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="e2663-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="e2663-115">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="e2663-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="e2663-116">De eerste stap is het gebruik van de [Azure-portal](https://portal.azure.com) voor het maken van een naamruimte voor het type Event Hubs en beheerreferenties die uw toepassing moet communiceren met de event hub.</span><span class="sxs-lookup"><span data-stu-id="e2663-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="e2663-117">Volg de procedure in voor het maken van een naamruimte en event hub [in dit artikel](event-hubs-create.md), en vervolgens doorgaan met de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="e2663-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e2663-118">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="e2663-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="e2663-119">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2663-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="e2663-120">Klik in het linkernavigatievenster van de portal op **nieuw**, klikt u op **opslag**, en klik vervolgens op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="e2663-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="e2663-121">Vul de velden in de blade opslagaccount en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e2663-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Storage-account maken][1]

4. <span data-ttu-id="e2663-123">Nadat u de **implementaties is geslaagd** bericht wordt weergegeven, klikt u op de naam van het nieuwe opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e2663-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="e2663-124">In de **Essentials** blade, klikt u op **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="e2663-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="e2663-125">Wanneer de **Blob-service** blade wordt geopend, klikt u op **+ Container** aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="e2663-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="e2663-126">Geef een naam op voor de container en sluit vervolgens de **Blob-service** blade.</span><span class="sxs-lookup"><span data-stu-id="e2663-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="e2663-127">Klik op **toegangssleutels** in het linkerdeelvenster blade en kopieer de naam van de storage-container, het opslagaccount en de waarde van **key1**.</span><span class="sxs-lookup"><span data-stu-id="e2663-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="e2663-128">Deze waarden naar Kladblok of een andere tijdelijke locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="e2663-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="e2663-129">Een consoletoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e2663-129">Create a console application</span></span>

<span data-ttu-id="e2663-130">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2663-130">Start Visual Studio.</span></span> <span data-ttu-id="e2663-131">Klik in het menu **File** op **New** en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="e2663-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="e2663-132">Maak een consoletoepassing .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e2663-132">Create a .NET Core console application.</span></span>

![Nieuw project][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="e2663-134">Toevoegen van het Event Hubs NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="e2663-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="e2663-135">Voeg de [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) en [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET standaardbibliotheek NuGet-pakketten aan uw project met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e2663-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="e2663-136">Klik met de rechtermuisknop op het nieuwe project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="e2663-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e2663-137">Klik op de **Bladeren** tabblad, zoekt u naar 'Microsoft.Azure.EventHubs' en selecteer de **Microsoft.Azure.EventHubs** pakket.</span><span class="sxs-lookup"><span data-stu-id="e2663-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="e2663-138">Klik op **Installeren** om de installatie te voltooien en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e2663-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="e2663-139">Herhaal stap 1 en 2 en installeer de **Microsoft.Azure.EventHubs.Processor** pakket.</span><span class="sxs-lookup"><span data-stu-id="e2663-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="e2663-140">De IEventProcessor-interface implementeren</span><span class="sxs-lookup"><span data-stu-id="e2663-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="e2663-141">Klik in Solution Explorer met de rechtermuisknop op het project, klikt u op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="e2663-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="e2663-142">Naam van de nieuwe klasse **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="e2663-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="e2663-143">Open het bestand simpleeventprocessor.cs en voeg de volgende `using` instructies boven aan het bestand.</span><span class="sxs-lookup"><span data-stu-id="e2663-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="e2663-144">Implementeer de `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="e2663-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="e2663-145">Vervang de volledige inhoud van de `SimpleEventProcessor` klasse met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="e2663-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="e2663-146">Schrijven van een methode hoofdconsole die gebruikmaakt van de klasse SimpleEventProcessor om berichten te ontvangen</span><span class="sxs-lookup"><span data-stu-id="e2663-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="e2663-147">Voeg aan het begin van het bestand Program.cs de volgende `using`-instructies toe.</span><span class="sxs-lookup"><span data-stu-id="e2663-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="e2663-148">Constanten toevoegen de `Program` klasse voor de verbindingsreeks voor event hub, naam event hub container opslagaccountnaam, opslagaccountnaam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="e2663-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="e2663-149">Voeg de volgende code, vervang de tijdelijke aanduidingen door de bijbehorende waarden.</span><span class="sxs-lookup"><span data-stu-id="e2663-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="e2663-150">Voeg een nieuwe methode met de naam `MainAsync` naar de `Program` klasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="e2663-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="e2663-151">Voeg de volgende regel code aan de `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="e2663-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="e2663-152">Zo zou het bestand Program.cs er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="e2663-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="e2663-153">Voer het programma uit en controleer of er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="e2663-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="e2663-154">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="e2663-154">Congratulations!</span></span> <span data-ttu-id="e2663-155">U hebt nu berichten ontvangen van een event hub met behulp van de Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="e2663-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2663-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2663-156">Next steps</span></span>
<span data-ttu-id="e2663-157">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="e2663-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e2663-158">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="e2663-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e2663-159">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="e2663-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e2663-160">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e2663-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
