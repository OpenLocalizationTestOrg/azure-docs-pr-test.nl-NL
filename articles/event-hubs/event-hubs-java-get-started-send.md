---
title: aaaSend gebeurtenissen tooAzure Event Hubs met behulp van Java | Microsoft Docs
description: Aan de slag verzenden tooEvent Hubs met Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>Verzenden van gebeurtenissen tooAzure Event Hubs met behulp van Java

## <a name="introduction"></a>Inleiding
Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Zodra verzameld in een event hub, kunt u transformeren en opslaan van gegevens met behulp van een realtime analytics-provider of opslagcluster.

Zie voor meer informatie, Hallo [overzicht van Event Hubs][Event Hubs overview].

Deze zelfstudie laat zien hoe toosend gebeurtenissen tooan event hub met behulp van een Java-consoletoepassing. tooreceive gebeurtenissen Hallo Java Event Processor Host tapewisselaar gebruikt, Zie [in dit artikel](event-hubs-java-get-started-receive-eph.md), of klik op de juiste Hallo ontvangende taal in Hallo links inhoudsopgave.

In de volgorde toocomplete in deze zelfstudie moet u hello te volgen:

* Een Java-ontwikkelomgeving. Voor deze zelfstudie gaan we ervan uit [Eclipse](https://www.eclipse.org/).
* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken. Zie <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.

## <a name="send-messages-tooevent-hubs"></a>Berichten verzenden tooEvent Hubs
Hallo Java-clientbibliotheek voor Event Hubs is beschikbaar voor gebruik in Maven-projecten uit Hallo [Maven centrale opslagplaats](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). U kunt verwijzen naar deze bibliotheek met Hallo afhankelijkheid declaratie binnen het projectbestand Maven te volgen:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Voor verschillende soorten build-omgevingen, kunt u de meest recente uitgebracht Hallo JAR-bestanden expliciet ophalen uit Hallo [Maven centrale opslagplaats](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Voor een publisher eenvoudige gebeurtenis importeren Hallo *com.microsoft.azure.eventhubs* -pakket voor Hallo Event Hubs clientklassen en Hallo *com.microsoft.azure.servicebus* voor hulpprogramma zoals klassen van het pakket Als algemene uitzonderingen die worden gedeeld met hello Azure Service Bus messaging-client. 

Voor Hallo voorbeeld te volgen, moet u eerst een nieuw Maven-project voor een console/shell-toepassing maken in uw favoriete Java-ontwikkelomgeving. Naam Hallo klasse `Send`.     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

Hallo-naamruimte en event hub namen vervangen door Hallo waarden gebruikt bij het maken van Hallo event hub.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Vervolgens maakt u een enkelvoudige gebeurtenis door het omzetten van een tekenreeks in de UTF-8-byte-codering. Vervolgens maakt u een nieuw exemplaar van de Event Hubs-client uit de verbindingsreeks Hallo en het Hallo-bericht verzenden.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Hallo EventProcessorHost met gebeurtenissen ontvangen](event-hubs-java-get-started-receive-eph.md)
* [Event Hubs-overzicht][Event Hubs overview]
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md