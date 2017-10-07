---
title: aaaHow toouse AMQP 1.0 Hello Java Service Bus-API | Microsoft Docs
description: Hoe Hallo toouse Java bericht Service (JMS) met Azure Service Bus en geavanceerde Message Queuing Protodol (AMQP) 1.0.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Hoe toouse Hallo Java bericht Service (JMS) API met Service Bus en AMQP 1.0
Hallo is geavanceerde Message Queuing-Protocol (AMQP) 1.0 een efficiënte, betrouwbare, wire-niveau messaging protocol waarmee u toobuild robuuste, platformoverschrijdende berichttoepassingen kunt.

Ondersteuning voor AMQP 1.0 in Service Bus houdt in dat u kunt Hallo queuing en publiceren/abonneren brokered messaging-onderdelen uit een reeks met behulp van een efficiënte binaire protocol platforms. Bovendien kunt u toepassingen bestaan uit de onderdelen die zijn gebouwd met behulp van een combinatie van talen en frameworks besturingssystemen maken.

Dit artikel wordt uitgelegd hoe toouse Service Bus messaging-functies (wachtrijen en publiceren/abonneren onderwerpen) vanuit Java-toepassingen met populaire Java bericht Service (JMS) API standaard Hallo. Er is een [companion artikel](service-bus-amqp-dotnet.md) waarin wordt uitgelegd hoe toodo Hallo dezelfde met Hallo Service Bus-.NET API. U kunt deze twee hulplijnen samen toolearn over platformonafhankelijke berichten met AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Aan de slag met Service Bus
Deze handleiding wordt ervan uitgegaan dat er al een Service Bus-naamruimte met een wachtrij met de naam **Wachtrij1**. Als u dit niet doet, dan u kunt [Hallo-naamruimte en wachtrij maken](service-bus-create-namespace-portal.md) met Hallo [Azure-portal](https://portal.azure.com). Voor meer informatie over hoe toocreate Service Bus-naamruimten en -wachtrijen, Zie [aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Gepartitioneerde wachtrijen en onderwerpen bieden ook ondersteuning voor AMQP. Zie voor meer informatie [gepartitioneerde berichtentiteiten](service-bus-partitioning.md) en [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Hallo AMQP 1.0 JMS clientbibliotheek downloaden
Voor informatie over waar toodownload meest recente versie van de clientbibliotheek Hallo Apache Qpid JMS AMQP 1.0 hello, gaat u naar [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Moet u de volgende vier JAR-bestanden uit Hallo Apache Qpid JMS AMQP 1.0 distributie archief toohello Java-KLASSENPAD bij het maken en uitvoeren van JMS toepassingen met Service Bus Hallo toevoegen:

* geronimo jms\_1.1\_spec 1.0.jar
* qpid-amqp-1-0-client-[Version].jar
* qpid-amqp-1-0-client-jms-[Version].jar
* qpid-amqp-1-0-Common-[Version].jar

## <a name="coding-java-applications"></a>Codering van Java-toepassingen
### <a name="java-naming-and-directory-interface-jndi"></a>Naam van Java en de Directory-Interface (JNDI)
JMS hello naamgeving van Java en Directory-Interface (JNDI) toocreate een scheiding tussen de namen van logische en fysieke gebruikt. Twee typen JMS objecten worden opgelost met JNDI: ConnectionFactory- en doelserver. JNDI maakt gebruik van een provider waarnaar u andere directory services toohandle name resolution rechten kunt aansluiten. Hallo Apache Qpid JMS AMQP 1.0 bibliotheek wordt geleverd met een eenvoudige eigenschappen op basis van bestanden JNDI Provider die is geconfigureerd met een eigenschappenbestand van de volgende Hallo opmaken:

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>Hallo ConnectionFactory configureren
Hallo toodefine post gebruikt een **ConnectionFactory** in Hallo Qpid eigenschappen bestand JNDI provider is Hallo volgende indeling:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Waar **[jndi_name]** en **[ConnectionURL]** Hallo na betekenis hebben:

* **[jndi_name]** : logische naam Hallo Hallo ConnectionFactory. Dit is Hallo-naam die worden opgelost in Hallo Java-toepassing hello JNDI IntialContext.lookup() methode gebruikt.
* **[ConnectionURL]** : Een URL die Hallo JMS bibliotheek Hallo informatie biedt vereist toohello AMQP broker.

Hallo-indeling van Hallo **ConnectionURL** is als volgt:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Waar **[namespace]**, **[SASPolicyName]** en **[SASPolicyKey]** Hallo na betekenis hebben:

* **[namespace]** : Hallo Service Bus-naamruimte.
* **[SASPolicyName]** : Hallo wachtrij Shared Access Signature beleidsnaam.
* **[SASPolicyKey]** : Hallo wachtrij Shared Access Signature beleidssleutel.

> [!NOTE]
> U moet handmatig URL coderen Hallo wachtwoord. Er is een nuttig URL-codering hulpprogramma beschikbaar op [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Doelen configureren
Hallo-vermelding gebruikt toodefine die een bestemming in Hallo Qpid eigenschappen bestand JNDI provider Hallo na indeling is:

```
queue.[jndi_name] = [physical_name]
```

of

```
topic.[jndi_name] = [physical_name]
```

Waar **[jndi\_name]** en **[fysieke\_name]** Hallo na betekenis hebben:

* **[jndi_name]** : Hallo logische naam van het Hallo-doel. Dit is Hallo-naam die worden opgelost in Hallo Java-toepassing hello JNDI IntialContext.lookup() methode gebruikt.
* **[physical_name]** : Hallo-naam van Service Bus-entiteit toowhich Hallo toepassing hello worden verzonden of ontvangen van berichten.

> [!NOTE]
> Bij de ontvangst van een Service Bus-onderwerpabonnement, moet Hallo fysieke naam opgegeven in JNDI Hallo-naam van Hallo onderwerp. naam van het abonnement Hello wordt verstrekt wanneer Hallo duurzame abonnement is gemaakt in Hallo JMS toepassingscode. Hallo [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) biedt meer details over het werken met Service Bus-onderwerpen van JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Hallo JMS toepassing schrijven
Er zijn geen speciale-API's of opties die vereist zijn wanneer u JMS met Service Bus. Er zijn echter enkele beperkingen die later aan bod. Zoals Hallo eerst te beginnen vereist voor elke toepassing JMS configuratie van Hallo JNDI omgeving, kunnen tooresolve toobe een **ConnectionFactory** en doelen.

#### <a name="configure-hello-jndi-initialcontext"></a>Hallo JNDI InitialContext configureren
Hallo JNDI omgeving wordt geconfigureerd met een hashtabel van configuratie-informatie wordt doorgegeven aan de constructor Hallo van Hallo javax.naming.InitialContext klasse. Hallo twee vereiste elementen in de hashtabel Hallo zijn klassenaam Hallo Hallo initiële Context Factory en Hallo URL van de Provider. Hallo volgende code toont hoe tooconfigure Hallo JNDI omgeving toouse hello Qpid eigenschappen op basis van bestanden JNDI Provider met een eigenschappenbestand met de naam **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Een eenvoudige JMS-toepassing met behulp van een Service Bus-wachtrij
Hallo volgende voorbeeld wordt JMS TextMessages tooa Service Bus-wachtrij met Hallo JNDI logische naam van de wachtrij verzendt en ontvangt terug Hallo-berichten.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
Hallo-toepassing, wordt de uitvoer van Hallo formulier:

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>Cross-platform uitwisseling van berichten tussen JMS en .NET
Deze handleiding hebt u geleerd hoe toosend en ontvangen berichten tooand van Service Bus JMS gebruiken. Een van de belangrijkste voordelen Hallo van AMQP 1.0 is echter dat deze toepassingen toobe gebouwd op basis van onderdelen die zijn geschreven in verschillende talen met berichten die worden uitgewisseld betrouwbaar en volledig betrouwbaar mogelijk maakt.

Met behulp van Hallo JMS voorbeeldtoepassing die hierboven worden beschreven en een vergelijkbare .NET-toepassing die afkomstig zijn uit een artikel companion [met behulp van Service Bus in .NET met AMQP 1.0](service-bus-amqp-dotnet.md), kunt u berichten tussen .NET en Java uitwisselen. Lees dit artikel voor meer informatie over Hallo van platformonafhankelijke berichten met behulp van Service Bus en AMQP 1.0.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET messaging:

* Start Hallo .NET-voorbeeldtoepassing zonder opdrachtregelargumenten.
* Hallo Java-voorbeeldtoepassing beginnen met 'sendonly' Hallo-opdrachtregelargument. In deze modus wordt hello toepassing ontvangt geen berichten uit de wachtrij hello, alleen verzonden.
* Druk op **Enter** een paar keer in Hallo Java-toepassing console waardoor berichten toobe verzonden.
* Deze berichten worden ontvangen door Hallo .NET-toepassing.

#### <a name="output-from-jms-application"></a>Uitvoer van de toepassing JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>De uitvoer van .NET-toepassing
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET-tooJMS
toodemonstrate .NET tooJMS messaging:

* Hallo .NET-voorbeeldtoepassing beginnen met 'sendonly' Hallo-opdrachtregelargument. In deze modus wordt hello toepassing ontvangt geen berichten uit de wachtrij hello, alleen verzonden.
* Start Hallo Java-voorbeeldtoepassing zonder opdrachtregelargumenten.
* Druk op **Enter** een paar keer in Hallo-.NET console waardoor berichten toobe verzonden.
* Deze berichten worden ontvangen door Hallo Java-toepassing.

#### <a name="output-from-net-application"></a>De uitvoer van .NET-toepassing
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Uitvoer van de toepassing JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Niet-ondersteunde functies en -beperkingen
Hallo volgen beperkingen bestaan wanneer deze met behulp van JMS via AMQP 1.0 met Service Bus weten:

* Slechts één **MessageProducer** of **MessageConsumer** is toegestaan **sessie**. Als u toocreate moet meerdere **MessageProducers** of **MessageConsumers** in een toepassing, maakt u een speciaal **sessie** voor elk van deze.
* Vluchtige onderwerpabonnementen worden momenteel niet ondersteund.
* **MessageSelectors** worden momenteel niet ondersteund.
* Tijdelijke bestemmingen; bijvoorbeeld: **TemporaryQueue**, **TemporaryTopic** worden momenteel niet ondersteund, samen met de Hallo **QueueRequestor** en **TopicRequestor**API's die ze gebruiken.
* Transactionele sessies en gedistribueerde transacties worden niet ondersteund.

## <a name="summary"></a>Samenvatting
Deze procedure-tooguide hebt u geleerd hoe toouse Service Bus brokered messaging-functies (wachtrijen en publiceren/abonneren onderwerpen) van het gebruik van Java Hallo populaire JMS API en AMQP 1.0.

U kunt ook een Service Bus AMQP 1.0 gebruiken van andere talen, waaronder .NET, C, Python en PHP. Onderdelen die zijn gebouwd met behulp van deze andere talen kunnen berichten worden uitgewisseld betrouwbaar en volledige fidelity met Hallo AMQP 1.0-ondersteuning in Service Bus.

## <a name="next-steps"></a>Volgende stappen
* [AMQP 1.0-ondersteuning in Azure Service Bus](service-bus-amqp-overview.md)
* [Hoe toouse AMQP 1.0 met Service Bus-.NET API Hallo](service-bus-dotnet-advanced-message-queuing.md)
* [Service Bus AMQP 1.0-handleiding voor ontwikkelaars](service-bus-amqp-dotnet.md)
* [Aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* [Java Developer Center](https://azure.microsoft.com/develop/java/)

