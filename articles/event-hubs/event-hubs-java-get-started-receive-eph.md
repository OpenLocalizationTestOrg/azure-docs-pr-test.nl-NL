---
title: aaaReceive gebeurtenissen van Azure Event Hubs met behulp van Java | Microsoft Docs
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
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="9484b-103">Ontvangen van gebeurtenissen van Azure Event Hubs met Java</span><span class="sxs-lookup"><span data-stu-id="9484b-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="9484b-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="9484b-104">Introduction</span></span>
<span data-ttu-id="9484b-105">Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9484b-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="9484b-106">Als ze eenmaal in Event Hubs zijn verzameld, kunt u de gegevens omzetten en opslaan met een realtime analytics-provider of opslagcluster.</span><span class="sxs-lookup"><span data-stu-id="9484b-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="9484b-107">Zie voor meer informatie, Hallo [overzicht van Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="9484b-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="9484b-108">Deze zelfstudie laat zien hoe tooreceive gebeurtenissen in een event hub met een consoletoepassing die is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="9484b-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9484b-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9484b-109">Prerequisites</span></span>

<span data-ttu-id="9484b-110">In volgorde toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="9484b-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="9484b-111">Een Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="9484b-111">A Java development environment.</span></span> <span data-ttu-id="9484b-112">Voor deze zelfstudie gaan we ervan uit [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="9484b-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="9484b-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9484b-113">An active Azure account.</span></span> <br/><span data-ttu-id="9484b-114">Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="9484b-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="9484b-115">Zie <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9484b-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="9484b-116">Berichten ontvangen met EventProcessorHost in Java</span><span class="sxs-lookup"><span data-stu-id="9484b-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="9484b-117">**EventProcessorHost** is een Javaklasse die ontvangen van gebeurtenissen van Event Hubs vereenvoudigt door permanente controlepunten beheren en parallelle ontvangst van deze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9484b-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="9484b-118">EventProcessorHost gebruikt, splitsen u gebeurtenissen over meerdere ontvangers, zelfs wanneer deze wordt gehost in verschillende knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9484b-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="9484b-119">Dit voorbeeld ziet u hoe toouse EventProcessorHost voor één ontvanger.</span><span class="sxs-lookup"><span data-stu-id="9484b-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="9484b-120">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="9484b-120">Create a storage account</span></span>
<span data-ttu-id="9484b-121">toouse EventProcessorHost, hebt u een [Azure Storage-account][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="9484b-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="9484b-122">Meld u aan toohello [Azure-portal][Azure portal], en klik op **+ nieuw** aan de linkerkant Hallo van welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="9484b-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="9484b-123">Klik op **Opslag** en klik vervolgens op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="9484b-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="9484b-124">In Hallo **storage-account maken** blade een naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9484b-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="9484b-125">Voltooi de rest Hallo Hallo velden, selecteer de gewenste regio en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="9484b-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="9484b-126">Klik op nieuw gemaakte Hallo storage-account en klik vervolgens op **toegangssleutels beheren**:</span><span class="sxs-lookup"><span data-stu-id="9484b-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="9484b-127">Kopieer Hallo primaire sleutel tooa tijdelijke locatie, toouse verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="9484b-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="9484b-128">Een Java-project met behulp van Hallo EventProcessor Host maken</span><span class="sxs-lookup"><span data-stu-id="9484b-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="9484b-129">Hallo Java-clientbibliotheek voor Event Hubs is beschikbaar voor gebruik in Maven-projecten uit Hallo [Maven centrale opslagplaats][Maven Package], en kan worden verwezen met Hallo na afhankelijkheid declaratie binnen uw Maven project-bestand:</span><span class="sxs-lookup"><span data-stu-id="9484b-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="9484b-130">Voor verschillende soorten build-omgevingen, kunt u de meest recente uitgebracht Hallo JAR-bestanden expliciet ophalen uit Hallo [Maven centrale opslagplaats] [ Maven Package] of van [release-distributiepunt op Hallo GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="9484b-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="9484b-131">Voor Hallo voorbeeld te volgen, moet u eerst een nieuw Maven-project voor een console/shell-toepassing maken in uw favoriete Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="9484b-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="9484b-132">Hallo-klasse wordt aangeroepen `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="9484b-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="9484b-133">Gebruik Hallo volgende code toocreate aangeroepen voor een nieuwe klasse `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="9484b-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="9484b-134">Maak een meer klasse aangeroepen `EventProcessorSample`met Hallo volgende code.</span><span class="sxs-lookup"><span data-stu-id="9484b-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
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
   
            System.out.println("Press enter toostop");
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
4. <span data-ttu-id="9484b-135">Vervang Hallo velden te volgen met Hallo waarden gebruikt wanneer u Hallo event hub en storage-account hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9484b-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="9484b-136">In deze zelfstudie wordt één exemplaar van EventProcessorHost gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9484b-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="9484b-137">tooincrease doorvoer, wordt aangeraden dat u meerdere exemplaren van EventProcessorHost, bij voorkeur op afzonderlijke computers uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9484b-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="9484b-138">Dit biedt ook de redundantie.</span><span class="sxs-lookup"><span data-stu-id="9484b-138">This provides redundancy as well.</span></span> <span data-ttu-id="9484b-139">In deze gevallen ontvangen Hallo die verschillende exemplaren automatisch wordt samen met elkaar in volgorde tooload saldo Hallo gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="9484b-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="9484b-140">Als u wilt dat meerdere ontvangers tooeach proces *alle* Hallo gebeurtenissen, moet u Hallo **ConsumerGroup** concept.</span><span class="sxs-lookup"><span data-stu-id="9484b-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="9484b-141">Wanneer gebeurtenissen ontvangen van andere computers, het mogelijk handig toospecify namen voor EventProcessorHost-exemplaren op basis van Hallo machines (of rollen) die worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9484b-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9484b-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9484b-142">Next steps</span></span>
<span data-ttu-id="9484b-143">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9484b-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9484b-144">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="9484b-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9484b-145">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="9484b-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="9484b-146">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9484b-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
