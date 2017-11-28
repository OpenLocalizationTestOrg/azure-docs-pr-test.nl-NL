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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="ba8fa-103">Hoe toouse Hallo Java bericht Service (JMS) API met Service Bus en AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="ba8fa-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="ba8fa-104">Hallo is geavanceerde Message Queuing-Protocol (AMQP) 1.0 een efficiënte, betrouwbare, wire-niveau messaging protocol waarmee u toobuild robuuste, platformoverschrijdende berichttoepassingen kunt.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="ba8fa-105">Ondersteuning voor AMQP 1.0 in Service Bus houdt in dat u kunt Hallo queuing en publiceren/abonneren brokered messaging-onderdelen uit een reeks met behulp van een efficiënte binaire protocol platforms.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="ba8fa-106">Bovendien kunt u toepassingen bestaan uit de onderdelen die zijn gebouwd met behulp van een combinatie van talen en frameworks besturingssystemen maken.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="ba8fa-107">Dit artikel wordt uitgelegd hoe toouse Service Bus messaging-functies (wachtrijen en publiceren/abonneren onderwerpen) vanuit Java-toepassingen met populaire Java bericht Service (JMS) API standaard Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="ba8fa-108">Er is een [companion artikel](service-bus-amqp-dotnet.md) waarin wordt uitgelegd hoe toodo Hallo dezelfde met Hallo Service Bus-.NET API.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="ba8fa-109">U kunt deze twee hulplijnen samen toolearn over platformonafhankelijke berichten met AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="ba8fa-110">Aan de slag met Service Bus</span><span class="sxs-lookup"><span data-stu-id="ba8fa-110">Get started with Service Bus</span></span>
<span data-ttu-id="ba8fa-111">Deze handleiding wordt ervan uitgegaan dat er al een Service Bus-naamruimte met een wachtrij met de naam **Wachtrij1**.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="ba8fa-112">Als u dit niet doet, dan u kunt [Hallo-naamruimte en wachtrij maken](service-bus-create-namespace-portal.md) met Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba8fa-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba8fa-113">Voor meer informatie over hoe toocreate Service Bus-naamruimten en -wachtrijen, Zie [aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ba8fa-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba8fa-114">Gepartitioneerde wachtrijen en onderwerpen bieden ook ondersteuning voor AMQP.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="ba8fa-115">Zie voor meer informatie [gepartitioneerde berichtentiteiten](service-bus-partitioning.md) en [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba8fa-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="ba8fa-116">Hallo AMQP 1.0 JMS clientbibliotheek downloaden</span><span class="sxs-lookup"><span data-stu-id="ba8fa-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="ba8fa-117">Voor informatie over waar toodownload meest recente versie van de clientbibliotheek Hallo Apache Qpid JMS AMQP 1.0 hello, gaat u naar [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ba8fa-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="ba8fa-118">Moet u de volgende vier JAR-bestanden uit Hallo Apache Qpid JMS AMQP 1.0 distributie archief toohello Java-KLASSENPAD bij het maken en uitvoeren van JMS toepassingen met Service Bus Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="ba8fa-119">geronimo jms\_1.1\_spec 1.0.jar</span><span class="sxs-lookup"><span data-stu-id="ba8fa-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="ba8fa-120">qpid-amqp-1-0-client-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="ba8fa-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="ba8fa-121">qpid-amqp-1-0-client-jms-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="ba8fa-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="ba8fa-122">qpid-amqp-1-0-Common-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="ba8fa-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="ba8fa-123">Codering van Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="ba8fa-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="ba8fa-124">Naam van Java en de Directory-Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="ba8fa-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="ba8fa-125">JMS hello naamgeving van Java en Directory-Interface (JNDI) toocreate een scheiding tussen de namen van logische en fysieke gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="ba8fa-126">Twee typen JMS objecten worden opgelost met JNDI: ConnectionFactory- en doelserver.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="ba8fa-127">JNDI maakt gebruik van een provider waarnaar u andere directory services toohandle name resolution rechten kunt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="ba8fa-128">Hallo Apache Qpid JMS AMQP 1.0 bibliotheek wordt geleverd met een eenvoudige eigenschappen op basis van bestanden JNDI Provider die is geconfigureerd met een eigenschappenbestand van de volgende Hallo opmaken:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="ba8fa-129">Hallo ConnectionFactory configureren</span><span class="sxs-lookup"><span data-stu-id="ba8fa-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="ba8fa-130">Hallo toodefine post gebruikt een **ConnectionFactory** in Hallo Qpid eigenschappen bestand JNDI provider is Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="ba8fa-131">Waar **[jndi_name]** en **[ConnectionURL]** Hallo na betekenis hebben:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="ba8fa-132">**[jndi_name]** : logische naam Hallo Hallo ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="ba8fa-133">Dit is Hallo-naam die worden opgelost in Hallo Java-toepassing hello JNDI IntialContext.lookup() methode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="ba8fa-134">**[ConnectionURL]** : Een URL die Hallo JMS bibliotheek Hallo informatie biedt vereist toohello AMQP broker.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="ba8fa-135">Hallo-indeling van Hallo **ConnectionURL** is als volgt:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="ba8fa-136">Waar **[namespace]**, **[SASPolicyName]** en **[SASPolicyKey]** Hallo na betekenis hebben:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="ba8fa-137">**[namespace]** : Hallo Service Bus-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="ba8fa-138">**[SASPolicyName]** : Hallo wachtrij Shared Access Signature beleidsnaam.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="ba8fa-139">**[SASPolicyKey]** : Hallo wachtrij Shared Access Signature beleidssleutel.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8fa-140">U moet handmatig URL coderen Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="ba8fa-141">Er is een nuttig URL-codering hulpprogramma beschikbaar op [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="ba8fa-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="ba8fa-142">Doelen configureren</span><span class="sxs-lookup"><span data-stu-id="ba8fa-142">Configure destinations</span></span>
<span data-ttu-id="ba8fa-143">Hallo-vermelding gebruikt toodefine die een bestemming in Hallo Qpid eigenschappen bestand JNDI provider Hallo na indeling is:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="ba8fa-144">of</span><span class="sxs-lookup"><span data-stu-id="ba8fa-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="ba8fa-145">Waar **[jndi\_name]** en **[fysieke\_name]** Hallo na betekenis hebben:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="ba8fa-146">**[jndi_name]** : Hallo logische naam van het Hallo-doel.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="ba8fa-147">Dit is Hallo-naam die worden opgelost in Hallo Java-toepassing hello JNDI IntialContext.lookup() methode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="ba8fa-148">**[physical_name]** : Hallo-naam van Service Bus-entiteit toowhich Hallo toepassing hello worden verzonden of ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8fa-149">Bij de ontvangst van een Service Bus-onderwerpabonnement, moet Hallo fysieke naam opgegeven in JNDI Hallo-naam van Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="ba8fa-150">naam van het abonnement Hello wordt verstrekt wanneer Hallo duurzame abonnement is gemaakt in Hallo JMS toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="ba8fa-151">Hallo [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) biedt meer details over het werken met Service Bus-onderwerpen van JMS.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="ba8fa-152">Hallo JMS toepassing schrijven</span><span class="sxs-lookup"><span data-stu-id="ba8fa-152">Write hello JMS application</span></span>
<span data-ttu-id="ba8fa-153">Er zijn geen speciale-API's of opties die vereist zijn wanneer u JMS met Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="ba8fa-154">Er zijn echter enkele beperkingen die later aan bod.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="ba8fa-155">Zoals Hallo eerst te beginnen vereist voor elke toepassing JMS configuratie van Hallo JNDI omgeving, kunnen tooresolve toobe een **ConnectionFactory** en doelen.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="ba8fa-156">Hallo JNDI InitialContext configureren</span><span class="sxs-lookup"><span data-stu-id="ba8fa-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="ba8fa-157">Hallo JNDI omgeving wordt geconfigureerd met een hashtabel van configuratie-informatie wordt doorgegeven aan de constructor Hallo van Hallo javax.naming.InitialContext klasse.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="ba8fa-158">Hallo twee vereiste elementen in de hashtabel Hallo zijn klassenaam Hallo Hallo initiële Context Factory en Hallo URL van de Provider.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="ba8fa-159">Hallo volgende code toont hoe tooconfigure Hallo JNDI omgeving toouse hello Qpid eigenschappen op basis van bestanden JNDI Provider met een eigenschappenbestand met de naam **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="ba8fa-160">Een eenvoudige JMS-toepassing met behulp van een Service Bus-wachtrij</span><span class="sxs-lookup"><span data-stu-id="ba8fa-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="ba8fa-161">Hallo volgende voorbeeld wordt JMS TextMessages tooa Service Bus-wachtrij met Hallo JNDI logische naam van de wachtrij verzendt en ontvangt terug Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="ba8fa-162">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ba8fa-162">Run hello application</span></span>
<span data-ttu-id="ba8fa-163">Hallo-toepassing, wordt de uitvoer van Hallo formulier:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="ba8fa-164">Cross-platform uitwisseling van berichten tussen JMS en .NET</span><span class="sxs-lookup"><span data-stu-id="ba8fa-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="ba8fa-165">Deze handleiding hebt u geleerd hoe toosend en ontvangen berichten tooand van Service Bus JMS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="ba8fa-166">Een van de belangrijkste voordelen Hallo van AMQP 1.0 is echter dat deze toepassingen toobe gebouwd op basis van onderdelen die zijn geschreven in verschillende talen met berichten die worden uitgewisseld betrouwbaar en volledig betrouwbaar mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="ba8fa-167">Met behulp van Hallo JMS voorbeeldtoepassing die hierboven worden beschreven en een vergelijkbare .NET-toepassing die afkomstig zijn uit een artikel companion [met behulp van Service Bus in .NET met AMQP 1.0](service-bus-amqp-dotnet.md), kunt u berichten tussen .NET en Java uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="ba8fa-168">Lees dit artikel voor meer informatie over Hallo van platformonafhankelijke berichten met behulp van Service Bus en AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="ba8fa-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="ba8fa-169">JMS too.NET</span></span>
<span data-ttu-id="ba8fa-170">toodemonstrate JMS too.NET messaging:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="ba8fa-171">Start Hallo .NET-voorbeeldtoepassing zonder opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="ba8fa-172">Hallo Java-voorbeeldtoepassing beginnen met 'sendonly' Hallo-opdrachtregelargument.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="ba8fa-173">In deze modus wordt hello toepassing ontvangt geen berichten uit de wachtrij hello, alleen verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="ba8fa-174">Druk op **Enter** een paar keer in Hallo Java-toepassing console waardoor berichten toobe verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="ba8fa-175">Deze berichten worden ontvangen door Hallo .NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="ba8fa-176">Uitvoer van de toepassing JMS</span><span class="sxs-lookup"><span data-stu-id="ba8fa-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="ba8fa-177">De uitvoer van .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="ba8fa-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="ba8fa-178">.NET-tooJMS</span><span class="sxs-lookup"><span data-stu-id="ba8fa-178">.NET tooJMS</span></span>
<span data-ttu-id="ba8fa-179">toodemonstrate .NET tooJMS messaging:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="ba8fa-180">Hallo .NET-voorbeeldtoepassing beginnen met 'sendonly' Hallo-opdrachtregelargument.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="ba8fa-181">In deze modus wordt hello toepassing ontvangt geen berichten uit de wachtrij hello, alleen verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="ba8fa-182">Start Hallo Java-voorbeeldtoepassing zonder opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="ba8fa-183">Druk op **Enter** een paar keer in Hallo-.NET console waardoor berichten toobe verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="ba8fa-184">Deze berichten worden ontvangen door Hallo Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="ba8fa-185">De uitvoer van .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="ba8fa-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="ba8fa-186">Uitvoer van de toepassing JMS</span><span class="sxs-lookup"><span data-stu-id="ba8fa-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="ba8fa-187">Niet-ondersteunde functies en -beperkingen</span><span class="sxs-lookup"><span data-stu-id="ba8fa-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="ba8fa-188">Hallo volgen beperkingen bestaan wanneer deze met behulp van JMS via AMQP 1.0 met Service Bus weten:</span><span class="sxs-lookup"><span data-stu-id="ba8fa-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="ba8fa-189">Slechts één **MessageProducer** of **MessageConsumer** is toegestaan **sessie**.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="ba8fa-190">Als u toocreate moet meerdere **MessageProducers** of **MessageConsumers** in een toepassing, maakt u een speciaal **sessie** voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="ba8fa-191">Vluchtige onderwerpabonnementen worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="ba8fa-192">**MessageSelectors** worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="ba8fa-193">Tijdelijke bestemmingen; bijvoorbeeld: **TemporaryQueue**, **TemporaryTopic** worden momenteel niet ondersteund, samen met de Hallo **QueueRequestor** en **TopicRequestor**API's die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="ba8fa-194">Transactionele sessies en gedistribueerde transacties worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="ba8fa-195">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ba8fa-195">Summary</span></span>
<span data-ttu-id="ba8fa-196">Deze procedure-tooguide hebt u geleerd hoe toouse Service Bus brokered messaging-functies (wachtrijen en publiceren/abonneren onderwerpen) van het gebruik van Java Hallo populaire JMS API en AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="ba8fa-197">U kunt ook een Service Bus AMQP 1.0 gebruiken van andere talen, waaronder .NET, C, Python en PHP.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="ba8fa-198">Onderdelen die zijn gebouwd met behulp van deze andere talen kunnen berichten worden uitgewisseld betrouwbaar en volledige fidelity met Hallo AMQP 1.0-ondersteuning in Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ba8fa-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba8fa-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba8fa-199">Next steps</span></span>
* [<span data-ttu-id="ba8fa-200">AMQP 1.0-ondersteuning in Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="ba8fa-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="ba8fa-201">Hoe toouse AMQP 1.0 met Service Bus-.NET API Hallo</span><span class="sxs-lookup"><span data-stu-id="ba8fa-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="ba8fa-202">Service Bus AMQP 1.0-handleiding voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="ba8fa-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="ba8fa-203">Aan de slag met Service Bus-wachtrijen</span><span class="sxs-lookup"><span data-stu-id="ba8fa-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="ba8fa-204">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="ba8fa-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

