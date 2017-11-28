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
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="f53a1-103">Verzenden van gebeurtenissen tooAzure Event Hubs met behulp van Java</span><span class="sxs-lookup"><span data-stu-id="f53a1-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="f53a1-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="f53a1-104">Introduction</span></span>
<span data-ttu-id="f53a1-105">Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f53a1-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="f53a1-106">Zodra verzameld in een event hub, kunt u transformeren en opslaan van gegevens met behulp van een realtime analytics-provider of opslagcluster.</span><span class="sxs-lookup"><span data-stu-id="f53a1-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="f53a1-107">Zie voor meer informatie, Hallo [overzicht van Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="f53a1-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="f53a1-108">Deze zelfstudie laat zien hoe toosend gebeurtenissen tooan event hub met behulp van een Java-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="f53a1-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="f53a1-109">tooreceive gebeurtenissen Hallo Java Event Processor Host tapewisselaar gebruikt, Zie [in dit artikel](event-hubs-java-get-started-receive-eph.md), of klik op de juiste Hallo ontvangende taal in Hallo links inhoudsopgave.</span><span class="sxs-lookup"><span data-stu-id="f53a1-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="f53a1-110">In de volgorde toocomplete in deze zelfstudie moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f53a1-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="f53a1-111">Een Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="f53a1-111">A Java development environment.</span></span> <span data-ttu-id="f53a1-112">Voor deze zelfstudie gaan we ervan uit [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="f53a1-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="f53a1-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f53a1-113">An active Azure account.</span></span> <br/><span data-ttu-id="f53a1-114">Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="f53a1-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="f53a1-115">Zie <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f53a1-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="f53a1-116">Berichten verzenden tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="f53a1-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="f53a1-117">Hallo Java-clientbibliotheek voor Event Hubs is beschikbaar voor gebruik in Maven-projecten uit Hallo [Maven centrale opslagplaats](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="f53a1-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="f53a1-118">U kunt verwijzen naar deze bibliotheek met Hallo afhankelijkheid declaratie binnen het projectbestand Maven te volgen:</span><span class="sxs-lookup"><span data-stu-id="f53a1-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="f53a1-119">Voor verschillende soorten build-omgevingen, kunt u de meest recente uitgebracht Hallo JAR-bestanden expliciet ophalen uit Hallo [Maven centrale opslagplaats](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="f53a1-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="f53a1-120">Voor een publisher eenvoudige gebeurtenis importeren Hallo *com.microsoft.azure.eventhubs* -pakket voor Hallo Event Hubs clientklassen en Hallo *com.microsoft.azure.servicebus* voor hulpprogramma zoals klassen van het pakket Als algemene uitzonderingen die worden gedeeld met hello Azure Service Bus messaging-client.</span><span class="sxs-lookup"><span data-stu-id="f53a1-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="f53a1-121">Voor Hallo voorbeeld te volgen, moet u eerst een nieuw Maven-project voor een console/shell-toepassing maken in uw favoriete Java-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="f53a1-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="f53a1-122">Naam Hallo klasse `Send`.</span><span class="sxs-lookup"><span data-stu-id="f53a1-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="f53a1-123">Hallo-naamruimte en event hub namen vervangen door Hallo waarden gebruikt bij het maken van Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="f53a1-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="f53a1-124">Vervolgens maakt u een enkelvoudige gebeurtenis door het omzetten van een tekenreeks in de UTF-8-byte-codering.</span><span class="sxs-lookup"><span data-stu-id="f53a1-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="f53a1-125">Vervolgens maakt u een nieuw exemplaar van de Event Hubs-client uit de verbindingsreeks Hallo en het Hallo-bericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="f53a1-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="f53a1-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f53a1-126">Next steps</span></span>
<span data-ttu-id="f53a1-127">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f53a1-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="f53a1-128">Hallo EventProcessorHost met gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="f53a1-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="f53a1-129">[Event Hubs-overzicht][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="f53a1-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="f53a1-130">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="f53a1-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="f53a1-131">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f53a1-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md