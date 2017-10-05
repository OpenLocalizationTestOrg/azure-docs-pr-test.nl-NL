---
title: AMQP 1.0 gebruiken met Java Service Bus-API | Microsoft Docs
description: Klik hier voor meer informatie over het gebruik van de Java bericht Service (JMS) met Azure Service Bus en geavanceerde Message Queuing Protodol (AMQP) 1.0.
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="892f2-103">Het gebruik van Java bericht Service (JMS) API met Service Bus en AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="892f2-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="892f2-104">De geavanceerde Message Queuing-Protocol (AMQP) 1.0 is een efficiënte, betrouwbare, wire-niveau messaging protocol die u gebruiken kunt om robuuste, platformoverschrijdende messaging toepassingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="892f2-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="892f2-105">Ondersteuning voor AMQP 1.0 in Service Bus betekent dat u kunt het in de wachtrij gebruiken en publiceren/abonneren brokered messaging-onderdelen uit een reeks met behulp van een efficiënte binaire protocol platforms.</span><span class="sxs-lookup"><span data-stu-id="892f2-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="892f2-106">Bovendien kunt u toepassingen bestaan uit de onderdelen die zijn gebouwd met behulp van een combinatie van talen en frameworks besturingssystemen maken.</span><span class="sxs-lookup"><span data-stu-id="892f2-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="892f2-107">Dit artikel wordt uitgelegd hoe u Service Bus-berichtenservice functies (wachtrijen en onderwerpen publiceren/abonneren) gebruiken vanuit Java-toepassingen met behulp van de populaire Java bericht Service (JMS) API standaard.</span><span class="sxs-lookup"><span data-stu-id="892f2-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="892f2-108">Er is een [companion artikel](service-bus-amqp-dotnet.md) waarin wordt uitgelegd hoe hetzelfde met de Service Bus .NET API.</span><span class="sxs-lookup"><span data-stu-id="892f2-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="892f2-109">U kunt deze twee handleidingen samen gebruiken voor meer informatie over cross-platform messaging met AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="892f2-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="892f2-110">Aan de slag met Service Bus</span><span class="sxs-lookup"><span data-stu-id="892f2-110">Get started with Service Bus</span></span>
<span data-ttu-id="892f2-111">Deze handleiding wordt ervan uitgegaan dat er al een Service Bus-naamruimte met een wachtrij met de naam **Wachtrij1**.</span><span class="sxs-lookup"><span data-stu-id="892f2-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="892f2-112">Als u dit niet doet, dan u kunt [maken van de naamruimte en de wachtrij](service-bus-create-namespace-portal.md) met behulp van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="892f2-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="892f2-113">Zie voor meer informatie over het maken van Service Bus-naamruimten en -wachtrijen [aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="892f2-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="892f2-114">Gepartitioneerde wachtrijen en onderwerpen bieden ook ondersteuning voor AMQP.</span><span class="sxs-lookup"><span data-stu-id="892f2-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="892f2-115">Zie voor meer informatie [gepartitioneerde berichtentiteiten](service-bus-partitioning.md) en [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="892f2-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="892f2-116">Downloaden van de clientbibliotheek AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="892f2-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="892f2-117">Voor informatie over de nieuwste versie van de clientbibliotheek Apache Qpid JMS AMQP 1.0 te downloaden, gaat u naar [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="892f2-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="892f2-118">U moet de volgende vier JAR-bestanden uit het archief van de Apache Qpid JMS AMQP 1.0-distributiepunt toevoegen aan het Java-KLASSENPAD bij het maken en uitvoeren van JMS toepassingen met Service Bus:</span><span class="sxs-lookup"><span data-stu-id="892f2-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="892f2-119">geronimo jms\_1.1\_spec 1.0.jar</span><span class="sxs-lookup"><span data-stu-id="892f2-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="892f2-120">qpid-amqp-1-0-client-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="892f2-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="892f2-121">qpid-amqp-1-0-client-jms-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="892f2-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="892f2-122">qpid-amqp-1-0-Common-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="892f2-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="892f2-123">Codering van Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="892f2-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="892f2-124">Naam van Java en de Directory-Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="892f2-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="892f2-125">JMS gebruikt de naamgeving van Java en de Directory-Interface (JNDI) voor het maken van een scheiding tussen de namen van logische en fysieke.</span><span class="sxs-lookup"><span data-stu-id="892f2-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="892f2-126">Twee typen JMS objecten worden opgelost met JNDI: ConnectionFactory- en doelserver.</span><span class="sxs-lookup"><span data-stu-id="892f2-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="892f2-127">JNDI maakt gebruik van een provider waarnaar u andere directoryservices voor het afhandelen van name resolution rechten kunt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="892f2-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="892f2-128">De Apache Qpid JMS AMQP 1.0-bibliotheek wordt geleverd met een eenvoudige eigenschappen op basis van bestanden JNDI Provider die is geconfigureerd met behulp van een eigenschappenbestand van de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="892f2-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="892f2-129">De ConnectionFactory configureren</span><span class="sxs-lookup"><span data-stu-id="892f2-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="892f2-130">De vermelding die wordt gebruikt voor het definiëren van een **ConnectionFactory** JNDI provider in het bestand van de eigenschappen Qpid is de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="892f2-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="892f2-131">Waar **[jndi_name]** en **[ConnectionURL]** hebben de volgende betekenis:</span><span class="sxs-lookup"><span data-stu-id="892f2-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="892f2-132">**[jndi_name]** : De logische naam van de ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="892f2-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="892f2-133">Dit is de naam die in de Java-toepassing met de methode JNDI IntialContext.lookup() worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="892f2-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="892f2-134">**[ConnectionURL]** : Een URL die de JMS-bibliotheek met de vereiste informatie aan de AMQP broker biedt.</span><span class="sxs-lookup"><span data-stu-id="892f2-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="892f2-135">De indeling van de **ConnectionURL** is als volgt:</span><span class="sxs-lookup"><span data-stu-id="892f2-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="892f2-136">Waar **[namespace]**, **[SASPolicyName]** en **[SASPolicyKey]** hebben de volgende betekenis:</span><span class="sxs-lookup"><span data-stu-id="892f2-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="892f2-137">**[namespace]** : De Service Bus-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="892f2-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="892f2-138">**[SASPolicyName]** : Naam van de wachtrij Shared Access Signature-beleid.</span><span class="sxs-lookup"><span data-stu-id="892f2-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="892f2-139">**[SASPolicyKey]** : Sleutel voor de wachtrij Shared Access Signature-beleid.</span><span class="sxs-lookup"><span data-stu-id="892f2-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="892f2-140">Moet u URL coderen het wachtwoord handmatig.</span><span class="sxs-lookup"><span data-stu-id="892f2-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="892f2-141">Er is een nuttig URL-codering hulpprogramma beschikbaar op [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="892f2-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="892f2-142">Doelen configureren</span><span class="sxs-lookup"><span data-stu-id="892f2-142">Configure destinations</span></span>
<span data-ttu-id="892f2-143">De vermelding die wordt gebruikt voor het definiëren van een bestemming in de provider Qpid eigenschappen bestand JNDI is van de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="892f2-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="892f2-144">of</span><span class="sxs-lookup"><span data-stu-id="892f2-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="892f2-145">Waar **[jndi\_name]** en **[fysieke\_name]** hebben de volgende betekenis:</span><span class="sxs-lookup"><span data-stu-id="892f2-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="892f2-146">**[jndi_name]** : De logische naam van de bestemming.</span><span class="sxs-lookup"><span data-stu-id="892f2-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="892f2-147">Dit is de naam die in de Java-toepassing met de methode JNDI IntialContext.lookup() worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="892f2-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="892f2-148">**[physical_name]** : De naam van de Service Bus-entiteit waarop de toepassing worden verzonden of ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="892f2-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="892f2-149">Bij de ontvangst van een Service Bus-onderwerpabonnement, is de fysieke naam die is opgegeven in JNDI moet de naam van het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="892f2-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="892f2-150">Naam van het abonnement wordt verstrekt wanneer het duurzame abonnement is gemaakt in de toepassingscode JMS.</span><span class="sxs-lookup"><span data-stu-id="892f2-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="892f2-151">De [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) biedt meer details over het werken met Service Bus-onderwerpen van JMS.</span><span class="sxs-lookup"><span data-stu-id="892f2-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="892f2-152">De toepassing JMS schrijven</span><span class="sxs-lookup"><span data-stu-id="892f2-152">Write the JMS application</span></span>
<span data-ttu-id="892f2-153">Er zijn geen speciale-API's of opties die vereist zijn wanneer u JMS met Service Bus.</span><span class="sxs-lookup"><span data-stu-id="892f2-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="892f2-154">Er zijn echter enkele beperkingen die later aan bod.</span><span class="sxs-lookup"><span data-stu-id="892f2-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="892f2-155">Net als bij elke toepassing JMS eerst te beginnen de vereiste configuratie van de omgeving JNDI kunnen omzetten een **ConnectionFactory** en doelen.</span><span class="sxs-lookup"><span data-stu-id="892f2-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="892f2-156">De InitialContext JNDI configureren</span><span class="sxs-lookup"><span data-stu-id="892f2-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="892f2-157">De omgeving JNDI wordt geconfigureerd met een hashtabel van configuratie-informatie wordt doorgegeven aan de constructor van de klasse javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="892f2-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="892f2-158">De twee vereiste elementen in de hashtabel zijn de naam van de klasse van de eerste Context fabriek en de URL van de Provider.</span><span class="sxs-lookup"><span data-stu-id="892f2-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="892f2-159">De volgende code toont hoe u configureert de JNDI-omgeving voor het gebruik van de Provider JNDI met een eigenschappenbestand met de naam op basis van eigenschappen bestanden Qpid **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="892f2-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="892f2-160">Een eenvoudige JMS-toepassing met behulp van een Service Bus-wachtrij</span><span class="sxs-lookup"><span data-stu-id="892f2-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="892f2-161">Het volgende voorbeeldprogramma JMS TextMessages naar een Service Bus-wachtrij met de logische naam JNDI van wachtrij verzendt en ontvangt de berichten terug.</span><span class="sxs-lookup"><span data-stu-id="892f2-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="892f2-162">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="892f2-162">Run the application</span></span>
<span data-ttu-id="892f2-163">De toepassing wordt uitgevoerd, wordt de uitvoer van het formulier:</span><span class="sxs-lookup"><span data-stu-id="892f2-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="892f2-164">Cross-platform uitwisseling van berichten tussen JMS en .NET</span><span class="sxs-lookup"><span data-stu-id="892f2-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="892f2-165">Deze handleiding hebt u geleerd hoe verzenden en ontvangen van berichten naar en van Service Bus JMS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="892f2-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="892f2-166">Een van de belangrijkste voordelen van AMQP 1.0 is echter dat deze kan worden gebouwd van onderdelen die zijn geschreven in verschillende talen met berichten die worden uitgewisseld betrouwbaar en volledige fidelity-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="892f2-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="892f2-167">Met behulp van de voorbeeldtoepassing JMS die hierboven worden beschreven en een vergelijkbare .NET-toepassing die afkomstig zijn uit een artikel companion [met behulp van Service Bus in .NET met AMQP 1.0](service-bus-amqp-dotnet.md), kunt u berichten tussen .NET en Java uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="892f2-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="892f2-168">Lees dit artikel voor meer informatie over de details van platformonafhankelijke berichten met behulp van Service Bus en AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="892f2-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="892f2-169">JMS naar .NET</span><span class="sxs-lookup"><span data-stu-id="892f2-169">JMS to .NET</span></span>
<span data-ttu-id="892f2-170">Ter illustratie van JMS .NET Messaging:</span><span class="sxs-lookup"><span data-stu-id="892f2-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="892f2-171">Start de voorbeeldtoepassing .NET zonder opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="892f2-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="892f2-172">De Java-voorbeeldtoepassing beginnen met het opdrachtregelargument 'sendonly'.</span><span class="sxs-lookup"><span data-stu-id="892f2-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="892f2-173">In deze modus kan de toepassing geen berichten ontvangen uit de wachtrij wordt alleen verzonden.</span><span class="sxs-lookup"><span data-stu-id="892f2-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="892f2-174">Druk op **Enter** een paar keer in de console van Java-toepassing, waardoor berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="892f2-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="892f2-175">Deze berichten worden ontvangen door de .NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="892f2-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="892f2-176">Uitvoer van de toepassing JMS</span><span class="sxs-lookup"><span data-stu-id="892f2-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="892f2-177">De uitvoer van .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="892f2-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="892f2-178">.NET naar JMS</span><span class="sxs-lookup"><span data-stu-id="892f2-178">.NET to JMS</span></span>
<span data-ttu-id="892f2-179">Ter illustratie van .NET JMS Messaging:</span><span class="sxs-lookup"><span data-stu-id="892f2-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="892f2-180">De voorbeeldtoepassing .NET beginnen met het opdrachtregelargument 'sendonly'.</span><span class="sxs-lookup"><span data-stu-id="892f2-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="892f2-181">In deze modus kan de toepassing geen berichten ontvangen uit de wachtrij wordt alleen verzonden.</span><span class="sxs-lookup"><span data-stu-id="892f2-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="892f2-182">Start de Java-voorbeeldtoepassing zonder opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="892f2-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="892f2-183">Druk op **Enter** een paar keer in de console van de toepassing .NET waardoor berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="892f2-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="892f2-184">Deze berichten worden ontvangen door de Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="892f2-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="892f2-185">De uitvoer van .NET-toepassing</span><span class="sxs-lookup"><span data-stu-id="892f2-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="892f2-186">Uitvoer van de toepassing JMS</span><span class="sxs-lookup"><span data-stu-id="892f2-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="892f2-187">Niet-ondersteunde functies en -beperkingen</span><span class="sxs-lookup"><span data-stu-id="892f2-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="892f2-188">De volgende beperkingen bestaan wanneer deze met behulp van JMS via AMQP 1.0 met Service Bus weten:</span><span class="sxs-lookup"><span data-stu-id="892f2-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="892f2-189">Slechts één **MessageProducer** of **MessageConsumer** is toegestaan **sessie**.</span><span class="sxs-lookup"><span data-stu-id="892f2-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="892f2-190">Als u wilt maken van meerdere **MessageProducers** of **MessageConsumers** in een toepassing, maakt u een speciaal **sessie** voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="892f2-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="892f2-191">Vluchtige onderwerpabonnementen worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="892f2-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="892f2-192">**MessageSelectors** worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="892f2-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="892f2-193">Tijdelijke bestemmingen; bijvoorbeeld: **TemporaryQueue**, **TemporaryTopic** worden momenteel niet ondersteund, samen met de **QueueRequestor** en **TopicRequestor** API's die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="892f2-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="892f2-194">Transactionele sessies en gedistribueerde transacties worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="892f2-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="892f2-195">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="892f2-195">Summary</span></span>
<span data-ttu-id="892f2-196">Deze handleiding instructies hebt u geleerd hoe u Service Bus brokered messaging functies (wachtrijen en onderwerpen publiceren/abonneren) met Java met behulp van de populaire JMS API en de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="892f2-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="892f2-197">U kunt ook een Service Bus AMQP 1.0 gebruiken van andere talen, waaronder .NET, C, Python en PHP.</span><span class="sxs-lookup"><span data-stu-id="892f2-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="892f2-198">Onderdelen die zijn gebouwd met behulp van deze andere talen kunnen betrouwbaar berichten uitwisselen en ondersteuning op volledige fidelity met behulp van de AMQP 1.0 in Service Bus.</span><span class="sxs-lookup"><span data-stu-id="892f2-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="892f2-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="892f2-199">Next steps</span></span>
* [<span data-ttu-id="892f2-200">AMQP 1.0-ondersteuning in Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="892f2-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="892f2-201">AMQP 1.0 gebruiken met de Service Bus .NET API</span><span class="sxs-lookup"><span data-stu-id="892f2-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="892f2-202">Service Bus AMQP 1.0-handleiding voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="892f2-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="892f2-203">Aan de slag met Service Bus-wachtrijen</span><span class="sxs-lookup"><span data-stu-id="892f2-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="892f2-204">Java Developer Center</span><span class="sxs-lookup"><span data-stu-id="892f2-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

