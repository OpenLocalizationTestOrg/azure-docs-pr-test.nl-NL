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
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Ontvangen van gebeurtenissen van Azure Event Hubs met Java


## <a name="introduction"></a>Inleiding
Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Als ze eenmaal in Event Hubs zijn verzameld, kunt u de gegevens omzetten en opslaan met een realtime analytics-provider of opslagcluster.

Zie voor meer informatie, Hallo [overzicht van Event Hubs][Event Hubs overview].

Deze zelfstudie laat zien hoe tooreceive gebeurtenissen in een event hub met een consoletoepassing die is geschreven in Java.

## <a name="prerequisites"></a>Vereisten

In volgorde toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* Een Java-ontwikkelomgeving. Voor deze zelfstudie gaan we ervan uit [Eclipse](https://www.eclipse.org/).
* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken. Zie <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Berichten ontvangen met EventProcessorHost in Java

**EventProcessorHost** is een Javaklasse die ontvangen van gebeurtenissen van Event Hubs vereenvoudigt door permanente controlepunten beheren en parallelle ontvangst van deze Event Hubs. EventProcessorHost gebruikt, splitsen u gebeurtenissen over meerdere ontvangers, zelfs wanneer deze wordt gehost in verschillende knooppunten. Dit voorbeeld ziet u hoe toouse EventProcessorHost voor één ontvanger.

### <a name="create-a-storage-account"></a>Een opslagaccount maken
toouse EventProcessorHost, hebt u een [Azure Storage-account][Azure Storage account]:

1. Meld u aan toohello [Azure-portal][Azure portal], en klik op **+ nieuw** aan de linkerkant Hallo van welkomstscherm.
2. Klik op **Opslag** en klik vervolgens op **Opslagaccount**. In Hallo **storage-account maken** blade een naam voor het Hallo-opslagaccount. Voltooi de rest Hallo Hallo velden, selecteer de gewenste regio en klik op **maken**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Klik op nieuw gemaakte Hallo storage-account en klik vervolgens op **toegangssleutels beheren**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Kopieer Hallo primaire sleutel tooa tijdelijke locatie, toouse verderop in deze zelfstudie.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Een Java-project met behulp van Hallo EventProcessor Host maken
Hallo Java-clientbibliotheek voor Event Hubs is beschikbaar voor gebruik in Maven-projecten uit Hallo [Maven centrale opslagplaats][Maven Package], en kan worden verwezen met Hallo na afhankelijkheid declaratie binnen uw Maven project-bestand:    

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

Voor verschillende soorten build-omgevingen, kunt u de meest recente uitgebracht Hallo JAR-bestanden expliciet ophalen uit Hallo [Maven centrale opslagplaats] [ Maven Package] of van [release-distributiepunt op Hallo GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Voor Hallo voorbeeld te volgen, moet u eerst een nieuw Maven-project voor een console/shell-toepassing maken in uw favoriete Java-ontwikkelomgeving. Hallo-klasse wordt aangeroepen `ErrorNotificationHandler`.     
   
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
2. Gebruik Hallo volgende code toocreate aangeroepen voor een nieuwe klasse `EventProcessor`.
   
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
3. Maak een meer klasse aangeroepen `EventProcessorSample`met Hallo volgende code.
   
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
4. Vervang Hallo velden te volgen met Hallo waarden gebruikt wanneer u Hallo event hub en storage-account hebt gemaakt.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> In deze zelfstudie wordt één exemplaar van EventProcessorHost gebruikt. tooincrease doorvoer, wordt aangeraden dat u meerdere exemplaren van EventProcessorHost, bij voorkeur op afzonderlijke computers uitvoeren.  Dit biedt ook de redundantie. In deze gevallen ontvangen Hallo die verschillende exemplaren automatisch wordt samen met elkaar in volgorde tooload saldo Hallo gebeurtenissen. Als u wilt dat meerdere ontvangers tooeach proces *alle* Hallo gebeurtenissen, moet u Hallo **ConsumerGroup** concept. Wanneer gebeurtenissen ontvangen van andere computers, het mogelijk handig toospecify namen voor EventProcessorHost-exemplaren op basis van Hallo machines (of rollen) die worden geïmplementeerd.
> 
> 

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
