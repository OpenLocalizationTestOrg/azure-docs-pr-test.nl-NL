---
title: Ontvangen van gebeurtenissen van Azure Event Hubs met behulp van Java | Microsoft Docs
description: Aan de slag ontvangen van Event Hubs met behulp van Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="032af-103">Ontvangen van gebeurtenissen van Azure Event Hubs met Java</span><span class="sxs-lookup"><span data-stu-id="032af-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="032af-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="032af-104">Introduction</span></span>
<span data-ttu-id="032af-105">Event Hubs is een zeer schaalbaar systeem die kan worden miljoenen gebeurtenissen per seconde opnemen voor het inschakelen van een toepassing te verwerken en analyseren van de enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="032af-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="032af-106">Als ze eenmaal in Event Hubs zijn verzameld, kunt u de gegevens omzetten en opslaan met een realtime analytics-provider of opslagcluster.</span><span class="sxs-lookup"><span data-stu-id="032af-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="032af-107">Zie voor meer informatie de [overzicht van Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="032af-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="032af-108">Deze zelfstudie laat zien hoe gebeurtenissen ontvangen in een event hub met een consoletoepassing die is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="032af-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="032af-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="032af-109">Prerequisites</span></span>

<span data-ttu-id="032af-110">Om deze zelfstudie hebt voltooid, moet u de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="032af-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="032af-111">Een Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="032af-111">A Java development environment.</span></span> <span data-ttu-id="032af-112">Voor deze zelfstudie gaan we ervan uit [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="032af-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="032af-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="032af-113">An active Azure account.</span></span> <br/><span data-ttu-id="032af-114">Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="032af-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="032af-115">Zie <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="032af-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="032af-116">Berichten ontvangen met EventProcessorHost in Java</span><span class="sxs-lookup"><span data-stu-id="032af-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="032af-117">**EventProcessorHost** is een Javaklasse die ontvangen van gebeurtenissen van Event Hubs vereenvoudigt door permanente controlepunten beheren en parallelle ontvangst van deze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="032af-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="032af-118">EventProcessorHost gebruikt, splitsen u gebeurtenissen over meerdere ontvangers, zelfs wanneer deze wordt gehost in verschillende knooppunten.</span><span class="sxs-lookup"><span data-stu-id="032af-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="032af-119">In dit voorbeeld wordt het gebruik van EventProcessorHost gedemonstreerd voor één ontvanger.</span><span class="sxs-lookup"><span data-stu-id="032af-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="032af-120">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="032af-120">Create a storage account</span></span>
<span data-ttu-id="032af-121">Als u wilt gebruiken EventProcessorHost, hebt u een [Azure Storage-account][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="032af-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="032af-122">Meld u aan bij de [Azure-portal][Azure portal], en klik op **+ nieuw** aan de linkerkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="032af-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="032af-123">Klik op **Opslag** en klik vervolgens op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="032af-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="032af-124">Typ op de blade **Opslagaccount maken** een naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="032af-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="032af-125">Voltooi de rest van de velden, selecteer de gewenste regio en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="032af-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="032af-126">Klik op het zojuist gemaakte opslagaccount en klik vervolgens op **Toegangssleutels beheren**:</span><span class="sxs-lookup"><span data-stu-id="032af-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="032af-127">Kopieer de primaire toegangssleutel naar een tijdelijke locatie, voor gebruik verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="032af-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="032af-128">Maak een Java-project met behulp van EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="032af-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="032af-129">De Java-clientbibliotheek voor Event Hubs is beschikbaar voor gebruik in Maven-projecten uit de [Maven centrale opslagplaats][Maven Package], en kan worden verwezen met de volgende afhankelijkheid declaratie binnen uw Maven projectbestand:</span><span class="sxs-lookup"><span data-stu-id="032af-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="032af-130">Voor verschillende soorten build-omgevingen, kunt u de meest recente uitgebrachte JAR-bestanden uit expliciet verkrijgen de [Maven centrale opslagplaats] [ Maven Package] of van [het distributiepunt release op GitHub ](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="032af-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="032af-131">Maak voor het volgende voorbeeld eerst een nieuw Maven-project voor een console/shell-toepassing in uw favoriete Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="032af-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="032af-132">De klasse wordt aangeroepen `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="032af-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="032af-133">Gebruik de volgende code om een nieuwe klasse te maken met de naam `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="032af-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="032af-134">Maak een meer klasse aangeroepen `EventProcessorSample`, met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="032af-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="032af-135">De volgende velden vervangen door de waarden gebruikt bij het maken van het event hub- en storage-account.</span><span class="sxs-lookup"><span data-stu-id="032af-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="032af-136">In deze zelfstudie wordt één exemplaar van EventProcessorHost gebruikt.</span><span class="sxs-lookup"><span data-stu-id="032af-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="032af-137">Voor een betere doorvoer wordt aangeraden dat u meerdere exemplaren van EventProcessorHost, bij voorkeur op afzonderlijke computers uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="032af-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="032af-138">Dit biedt ook de redundantie.</span><span class="sxs-lookup"><span data-stu-id="032af-138">This provides redundancy as well.</span></span> <span data-ttu-id="032af-139">In die gevallen werken de verschillende exemplaren automatisch samen om de ontvangen gebeurtenissen gelijkmatig te verdelen.</span><span class="sxs-lookup"><span data-stu-id="032af-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="032af-140">Als u wilt dat meerdere ontvangers *alle* gebeurtenissen verwerken, gebruik dan het concept **ConsumerGroup**.</span><span class="sxs-lookup"><span data-stu-id="032af-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="032af-141">Wanneer er gebeurtenissen van verschillende computers worden ontvangen, kan het nuttig zijn om namen voor EventProcessorHost-exemplaren op te geven op basis van de computers waarop (of rollen waarin) ze zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="032af-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="032af-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="032af-142">Next steps</span></span>
<span data-ttu-id="032af-143">U kunt meer informatie over Event Hubs vinden via de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="032af-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="032af-144">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="032af-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="032af-145">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="032af-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="032af-146">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="032af-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
