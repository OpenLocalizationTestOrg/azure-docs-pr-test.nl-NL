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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Verzenden van gebeurtenissen tooAzure Event Hubs met C

## <a name="introduction"></a>Inleiding
Event Hubs is een zeer schaalbaar systeem zodat kan miljoenen gebeurtenissen per seconde voor het inschakelen van een toepassing tooprocess opnemen en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Zodra verzameld in een event hub, kunt u transformeren en opslaan van gegevens met behulp van een realtime analytics-provider of opslagcluster.

Zie voor meer informatie Hallo [Event Hubs-overview] [Event Hubs-overview].

In deze zelfstudie leert u hoe toosend gebeurtenissen tooan event hub met een consoletoepassing in C. tooreceive gebeurtenissen, klikt u op Hallo juiste ontvangende taal in Hallo links inhoudsopgave.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een C-ontwikkelomgeving. Voor deze zelfstudie wordt ervan uitgegaan Hallo gcc stack op een Azure Linux-VM met Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.

## <a name="send-messages-tooevent-hubs"></a>Berichten verzenden tooEvent Hubs
In deze sectie schrijven we een C app toosend gebeurtenissen tooyour event hub. Hallo code gebruikt Hallo Proton AMQP-bibliotheek van Hallo [Apache Qpid project](http://qpid.apache.org/). Dit is vergelijkbaar toousing Service Bus-wachtrijen en onderwerpen met AMQP van C zoals [hier](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Zie voor meer informatie [Qpid Proton documentatie](http://qpid.apache.org/proton/index.html).

1. Van Hallo [Qpid AMQP Messenger pagina](https://qpid.apache.org/proton/messenger.html), volg Hallo instructies tooinstall Qpid Proton, afhankelijk van uw omgeving.
2. toocompile Proton bibliotheek hello, installeert u hello-pakketten te volgen:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Hallo downloaden [Qpid Proton bibliotheek](http://qpid.apache.org/proton/index.html), en pak het bestand, bijvoorbeeld:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Maak een build-directory, compileren en installeren:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. Maak een nieuw bestand met de naam in uw directory work **sender.c** Hello code te volgen. Houd er rekening mee toosubstitute Hallo waarde voor uw naam event hub en naamruimtenaam. U moet ook een URL-codering versie van de sleutel Hallo voor Hallo vervangen **SendRule** eerder hebt gemaakt. U kunt URL coderen deze [hier](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Compileer Hallo-bestand, ervan uitgaande dat **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > In deze code gebruiken we een uitgaande venster van 1 tooforce Hallo-berichten uit zo snel mogelijk. Uw toepassing moet in het algemeen toobatch berichten tooincrease doorvoer te proberen. Zie Hallo [Qpid AMQP Messenger pagina](https://qpid.apache.org/proton/messenger.html) voor meer informatie over hoe toouse Qpid Proton bibliotheek in deze en andere omgevingen en platforms waarvoor bindingen zijn opgegeven Hallo (momenteel Perl, PHP, Python en Ruby).


## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md
)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
