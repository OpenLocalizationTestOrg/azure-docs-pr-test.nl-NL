---
title: aaaHow toouse Azure Service Bus-onderwerpen met Java | Microsoft Docs
description: Service Bus-onderwerpen en abonnementen in Azure gebruiken.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="8a911-103">Hoe toouse Service Bus-onderwerpen en abonnementen met Java</span><span class="sxs-lookup"><span data-stu-id="8a911-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="8a911-104">Deze handleiding wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="8a911-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="8a911-105">Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure SDK voor Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="8a911-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="8a911-106">Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="8a911-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="8a911-107">Wat zijn Service Bus-onderwerpen en -abonnementen?</span><span class="sxs-lookup"><span data-stu-id="8a911-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="8a911-108">Service Bus-onderwerpen en -abonnementen bieden ondersteuning voor een berichtencommunicatiemodel op basis van *publiceren/abonneren*.</span><span class="sxs-lookup"><span data-stu-id="8a911-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="8a911-109">Wanneer u gebruikmaakt van onderwerpen en abonnementen, communiceren onderdelen van een gedistribueerde toepassing niet direct met elkaar. In plaats daarvan wisselen ze berichten uit via een onderwerp dat als intermediair fungeert.</span><span class="sxs-lookup"><span data-stu-id="8a911-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="8a911-111">Anders dan bij Service Bus-wachtrijen, waarin elk bericht door een enkele gebruiker wordt verwerkt, bieden onderwerpen en abonnementen een 'één-naar-veel'-communicatiewijze, waarbij een patroon voor publiceren/abonneren wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8a911-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="8a911-112">Het is mogelijk meerdere abonnementen tooa onderwerp registreren.</span><span class="sxs-lookup"><span data-stu-id="8a911-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="8a911-113">Wanneer een bericht wordt verzonden tooa onderwerp, wordt deze beschikbaar tooeach abonnement toohandle/proces vervolgens afzonderlijk gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a911-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="8a911-114">Een abonnement tooa onderwerp lijkt op een virtuele wachtrij die kopieën van Hallo-berichten dat is verzonden toohello onderwerp ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8a911-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="8a911-115">U kunt eventueel registreren filterregels voor een onderwerp op basis van per abonnement, waarmee u kunt toofilter of te beperken welke berichten tooa onderwerp door welke onderwerpabonnementen worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8a911-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="8a911-116">Service Bus-onderwerpen en abonnementen kunnen u tooscale tooprocess een zeer groot aantal berichten via een zeer groot aantal gebruikers en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8a911-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="8a911-117">Een servicenaamruimte maken</span><span class="sxs-lookup"><span data-stu-id="8a911-117">Create a service namespace</span></span>
<span data-ttu-id="8a911-118">toobegin met Service Bus-onderwerpen en abonnementen in Azure, moet u eerst een naamruimte een scoping container biedt voor het adresseren van Service Bus-resources in uw toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="8a911-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="8a911-119">een naamruimte toocreate:</span><span class="sxs-lookup"><span data-stu-id="8a911-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="8a911-120">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="8a911-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="8a911-121">Zorg ervoor dat u hebt geïnstalleerd Hallo [Azure SDK voor Java] [ Azure SDK for Java] voordat u dit voorbeeld maakt.</span><span class="sxs-lookup"><span data-stu-id="8a911-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="8a911-122">Als u Eclipse gebruikt, kunt u Hallo installeren [Azure Toolkit voor Eclipse] [ Azure Toolkit for Eclipse] die hello Azure SDK voor Java bevat.</span><span class="sxs-lookup"><span data-stu-id="8a911-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="8a911-123">Vervolgens kunt u toevoegen Hallo **Microsoft Azure-beheerbibliotheken voor Java** tooyour project:</span><span class="sxs-lookup"><span data-stu-id="8a911-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="8a911-124">Voeg de volgende Hallo `import` instructies toohello boven in Hallo Java-bestand:</span><span class="sxs-lookup"><span data-stu-id="8a911-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="8a911-125">Hello Azure-beheerbibliotheken voor Java tooyour pad maken en deze opnemen in uw project implementatie assembly toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8a911-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="8a911-126">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="8a911-126">Create a topic</span></span>
<span data-ttu-id="8a911-127">Beheerbewerkingen voor Service Bus-onderwerpen kunnen worden uitgevoerd via de **ServiceBusContract** klasse.</span><span class="sxs-lookup"><span data-stu-id="8a911-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="8a911-128">Een **ServiceBusContract** object is gemaakt met een juiste configuratie die door de SAS-token met machtigingen toomanage ingekapseld en Hallo **ServiceBusContract** klasse is de enige punt Hallo communicatie met Azure.</span><span class="sxs-lookup"><span data-stu-id="8a911-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="8a911-129">Hallo **ServiceBusService** klasse biedt methoden toocreate, opsommen en verwijderen van onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8a911-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="8a911-130">Hallo volgende voorbeeld ziet u hoe een **ServiceBusService** -object dat wordt gebruikt toocreate een onderwerp met de naam `TestTopic`, met een naamruimte aangeroepen `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="8a911-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="8a911-131">Er zijn methoden op **TopicInfo** waarmee de eigenschappen van Hallo onderwerp moet worden ingesteld (bijvoorbeeld: tooset Hallo standaard time-to-live (TTL) waarde toobe toegepast toomessages toohello onderwerp verzonden).</span><span class="sxs-lookup"><span data-stu-id="8a911-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="8a911-132">Hallo volgende voorbeeld laat zien hoe toocreate een onderwerp met de naam `TestTopic` met een maximale grootte van 5 GB:</span><span class="sxs-lookup"><span data-stu-id="8a911-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="8a911-133">Dat kunt u gebruikmaken van Hallo **listTopics** methode op **ServiceBusContract** toocheck objecten als een onderwerp met een opgegeven naam al in een Servicenaamruimte bestaat.</span><span class="sxs-lookup"><span data-stu-id="8a911-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="8a911-134">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="8a911-134">Create subscriptions</span></span>
<span data-ttu-id="8a911-135">Abonnementen tootopics tevens zijn gemaakt met de Hallo **ServiceBusService** klasse.</span><span class="sxs-lookup"><span data-stu-id="8a911-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="8a911-136">Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling virtuele wachtrij van het abonnement toohello doorgegeven berichten wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="8a911-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="8a911-137">Een abonnement maken met de Hallo standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="8a911-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="8a911-138">Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a911-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="8a911-139">Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in de virtuele wachtrij van het abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="8a911-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="8a911-140">Hallo volgende voorbeeld wordt een abonnement genaamd 'AllMessages' en gebruikt standaard Hallo **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="8a911-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="8a911-141">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="8a911-141">Create subscriptions with filters</span></span>
<span data-ttu-id="8a911-142">U kunt filters waarmee u kunt ook welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement tooscope maken.</span><span class="sxs-lookup"><span data-stu-id="8a911-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="8a911-143">Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is de [SqlFilter][SqlFilter], waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="8a911-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="8a911-144">SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn.</span><span class="sxs-lookup"><span data-stu-id="8a911-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="8a911-145">Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.</span><span class="sxs-lookup"><span data-stu-id="8a911-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="8a911-146">Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een [SqlFilter] [ SqlFilter] -object dat alleen berichten selecteert die een aangepaste **MessageNumber** de eigenschap is groter dan 3:</span><span class="sxs-lookup"><span data-stu-id="8a911-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="8a911-147">Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een [SqlFilter] [ SqlFilter] -object dat alleen berichten selecteert die een **MessageNumber** eigenschap kleiner dan of gelijk too3:</span><span class="sxs-lookup"><span data-stu-id="8a911-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="8a911-148">Wanneer een bericht nu te verzonden`TestTopic`, het altijd bezorgd tooreceivers geabonneerd toohello `AllMessages` abonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` (abonnementen afhankelijk van de inhoud van het bericht).</span><span class="sxs-lookup"><span data-stu-id="8a911-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="8a911-149">Verzenden van berichten tooa onderwerp</span><span class="sxs-lookup"><span data-stu-id="8a911-149">Send messages tooa topic</span></span>
<span data-ttu-id="8a911-150">een bericht tooa Service Bus-onderwerp toosend, beheersbaarheid voor uw toepassing een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="8a911-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="8a911-151">Hallo volgende code laat zien hoe een bericht voor Hallo toosend `TestTopic` onderwerp eerder hebt gemaakt in Hallo `HowToSample` naamruimte:</span><span class="sxs-lookup"><span data-stu-id="8a911-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="8a911-152">Berichten tooService Bus-onderwerpen, zijn exemplaren van de [BrokeredMessage] [ BrokeredMessage] klasse.</span><span class="sxs-lookup"><span data-stu-id="8a911-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="8a911-153">[BrokeredMessage][BrokeredMessage]* objecten hebben een aantal standaardmethoden (zoals **setLabel** en **TimeToLive**), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="8a911-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="8a911-154">Een toepassing kunt Hallo hoofdtekst van het bericht instellen door elk serialiseerbaar object doorgeven aan de constructor Hallo van de [BrokeredMessage][BrokeredMessage], en de juiste Hallo **DataContractSerializer**  gebruikte tooserialize Hallo object zijn.</span><span class="sxs-lookup"><span data-stu-id="8a911-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="8a911-155">U kunt ook een **java.io.InputStream** kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8a911-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="8a911-156">Hallo volgende voorbeeld toont hoe vijf toosend test toothe berichten `TestTopic` **MessageSender** we verkregen in de bovenstaande Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="8a911-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="8a911-157">Opmerking hoe Hallo **MessageNumber** eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (dit wordt bepaald welke abonnementen ontvangen):</span><span class="sxs-lookup"><span data-stu-id="8a911-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="8a911-158">Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="8a911-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="8a911-159">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="8a911-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="8a911-160">Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet op de totale grootte van berichten in een onderwerp Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8a911-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="8a911-161">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="8a911-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="8a911-162">Hoe tooreceive berichten van een abonnement</span><span class="sxs-lookup"><span data-stu-id="8a911-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="8a911-163">tooreceive berichten van een abonnement gebruiken een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="8a911-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="8a911-164">Ontvangen berichten kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="8a911-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="8a911-165">Bij gebruik van Hallo **ReceiveAndDelete** -modus ontvangt een enkele bewerking - dat wil zeggen, wanneer Service Bus een leesaanvraag voor een bericht ontvangt, wordt gemarkeerd als verbruikt het Hallo-bericht en retourneert het toothe toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a911-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="8a911-166">**ReceiveAndDelete** modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="8a911-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="8a911-167">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8a911-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="8a911-168">Omdat Service Bus het bericht als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint heeft gemarkeerd, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="8a911-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="8a911-169">In **PeekLock** -modus ontvangt, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="8a911-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="8a911-170">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a911-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="8a911-171">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van **verwijderen** op Hallo ontvangen bericht.</span><span class="sxs-lookup"><span data-stu-id="8a911-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="8a911-172">Wanneer Service Bus de aanroep Hallo **verwijderen** aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8a911-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="8a911-173">Hallo in het volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp **PeekLock** modus (geen Hallo standaardmodus).</span><span class="sxs-lookup"><span data-stu-id="8a911-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="8a911-174">Hallo in het volgende voorbeeld wordt een lus uitgevoerd en verwerkt berichten in Hallo 'HighMessages' abonnement en vervolgens afgesloten wanneer er geen berichten meer zijn (u kunt ook deze kan worden ingesteld toowait op nieuwe berichten).</span><span class="sxs-lookup"><span data-stu-id="8a911-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="8a911-175">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="8a911-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="8a911-176">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="8a911-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="8a911-177">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **unlockMessage** methode voor het ontvangen Hallo-bericht (in plaats van Hallo **deleteMessage** methode).</span><span class="sxs-lookup"><span data-stu-id="8a911-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="8a911-178">Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht Hallo onderwerp en beschikbaar toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="8a911-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="8a911-179">Daarnaast is er een time-out gekoppeld aan een bericht in het onderwerp is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt de time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="8a911-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="8a911-180">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **deleteMessage** verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8a911-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="8a911-181">Dit wordt vaak genoemd **tenminste eenmaal verwerken**, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="8a911-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="8a911-182">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8a911-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="8a911-183">Dit wordt vaak bereikt met behulp van Hallo **getMessageId** methode van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="8a911-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="8a911-184">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="8a911-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="8a911-185">Hallo primaire manier toodelete onderwerpen en abonnementen is toouse een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="8a911-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="8a911-186">Als u een onderwerp verwijdert, verwijdert ook alle abonnementen die zijn geregistreerd bij Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8a911-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="8a911-187">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8a911-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="8a911-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a911-188">Next Steps</span></span>
<span data-ttu-id="8a911-189">Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [Service Bus-wachtrijen, onderwerpen en abonnementen] [ Service Bus queues, topics, and subscriptions] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8a911-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
