---
title: aaaSend gebeurtenissen tooAzure Event Hubs met C | Microsoft Docs
description: Verzenden van gebeurtenissen tooAzure Event Hubs met C
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="b62ed-103">Verzenden van gebeurtenissen tooAzure Event Hubs met C</span><span class="sxs-lookup"><span data-stu-id="b62ed-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="b62ed-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="b62ed-104">Introduction</span></span>
<span data-ttu-id="b62ed-105">Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b62ed-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="b62ed-106">Zodra verzameld in een event hub, kunt u transformeren en opslaan van gegevens met behulp van een realtime analytics-provider of opslagcluster.</span><span class="sxs-lookup"><span data-stu-id="b62ed-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="b62ed-107">Zie voor meer informatie Hallo [Event Hubs-overview] [Event Hubs-overview].</span><span class="sxs-lookup"><span data-stu-id="b62ed-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="b62ed-108">In deze zelfstudie leert u hoe toosend gebeurtenissen tooan event hub met een consoletoepassing in C. tooreceive gebeurtenissen, klikt u op Hallo juiste ontvangende taal in Hallo links inhoudsopgave.</span><span class="sxs-lookup"><span data-stu-id="b62ed-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="b62ed-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="b62ed-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="b62ed-110">Een C-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="b62ed-110">A C development environment.</span></span> <span data-ttu-id="b62ed-111">Voor deze zelfstudie wordt ervan uitgegaan Hallo gcc stack op een Azure Linux-VM met Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="b62ed-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="b62ed-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="b62ed-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="b62ed-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b62ed-113">An active Azure account.</span></span> <span data-ttu-id="b62ed-114">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="b62ed-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b62ed-115">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b62ed-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="b62ed-116">Berichten verzenden tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="b62ed-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="b62ed-117">In deze sectie schrijven we een C app toosend gebeurtenissen tooyour event hub.</span><span class="sxs-lookup"><span data-stu-id="b62ed-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="b62ed-118">Hallo code gebruikt Hallo Proton AMQP-bibliotheek van Hallo [Apache Qpid project](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="b62ed-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="b62ed-119">Dit is vergelijkbaar toousing Service Bus-wachtrijen en onderwerpen met AMQP van C zoals [hier](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="b62ed-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="b62ed-120">Zie voor meer informatie [Qpid Proton documentatie](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="b62ed-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="b62ed-121">Van Hallo [Qpid AMQP Messenger pagina](https://qpid.apache.org/proton/messenger.html), volg Hallo instructies tooinstall Qpid Proton, afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="b62ed-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="b62ed-122">toocompile Proton bibliotheek hello, installeert u hello-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="b62ed-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="b62ed-123">Hallo downloaden [Qpid Proton bibliotheek](http://qpid.apache.org/proton/index.html), en pak het bestand, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b62ed-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="b62ed-124">Maak een build-directory, compileren en installeren:</span><span class="sxs-lookup"><span data-stu-id="b62ed-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="b62ed-125">Maak een nieuw bestand met de naam in uw directory work **sender.c** Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="b62ed-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="b62ed-126">Houd er rekening mee toosubstitute Hallo waarde voor uw naam event hub en naamruimtenaam.</span><span class="sxs-lookup"><span data-stu-id="b62ed-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="b62ed-127">U moet ook een URL-codering versie van de sleutel Hallo voor Hallo vervangen **SendRule** eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b62ed-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="b62ed-128">U kunt URL coderen deze [hier](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="b62ed-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="b62ed-129">Compileer Hallo-bestand, ervan uitgaande dat **gcc**:</span><span class="sxs-lookup"><span data-stu-id="b62ed-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="b62ed-130">In deze code gebruiken we een uitgaande venster van 1 tooforce Hallo-berichten uit zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="b62ed-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="b62ed-131">Uw toepassing moet in het algemeen toobatch berichten tooincrease doorvoer te proberen.</span><span class="sxs-lookup"><span data-stu-id="b62ed-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="b62ed-132">Zie Hallo [Qpid AMQP Messenger pagina](https://qpid.apache.org/proton/messenger.html) voor meer informatie over hoe toouse Qpid Proton bibliotheek in deze en andere omgevingen en platforms waarvoor bindingen zijn opgegeven Hallo (momenteel Perl, PHP, Python en Ruby).</span><span class="sxs-lookup"><span data-stu-id="b62ed-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b62ed-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b62ed-133">Next steps</span></span>
<span data-ttu-id="b62ed-134">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b62ed-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="b62ed-135">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="b62ed-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="b62ed-136">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="b62ed-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="b62ed-137">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b62ed-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
