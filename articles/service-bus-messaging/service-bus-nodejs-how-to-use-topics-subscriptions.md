---
title: Het gebruik van Azure Service Bus-onderwerpen en abonnementen met behulp van Node.js | Microsoft Docs
description: Informatie over het gebruik van Service Bus-onderwerpen en abonnementen van een Node.js-app in Azure.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="01143-103">Gebruik Service Bus-onderwerpen en abonnementen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="01143-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="01143-104">Deze handleiding wordt beschreven hoe u Service Bus-onderwerpen en abonnementen van Node.js-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="01143-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="01143-105">De scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten** naar een onderwerp **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="01143-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="01143-106">Zie de sectie [Volgende stappen](#next-steps) voor meer informatie over onderwerpen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="01143-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="01143-107">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="01143-107">Create a Node.js application</span></span>
<span data-ttu-id="01143-108">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="01143-108">Create a blank Node.js application.</span></span> <span data-ttu-id="01143-109">Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing naar een Azure-website], [Node.js-Cloudservice] [ Node.js Cloud Service] met behulp van Windows PowerShell of website met WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="01143-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="01143-110">Uw toepassing configureren voor het gebruik van Service Bus</span><span class="sxs-lookup"><span data-stu-id="01143-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="01143-111">Voor het gebruik van Service Bus de Node.js-Azure-pakket te downloaden.</span><span class="sxs-lookup"><span data-stu-id="01143-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="01143-112">Dit pakket bevat een set van bibliotheken die met de Service Bus REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="01143-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="01143-113">Knooppunt Package Manager (NPM) gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="01143-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="01143-114">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u naar de map waar u uw voorbeeldtoepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01143-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="01143-115">Type **npm installeren azure** in het opdrachtvenster die moet resulteren in de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="01143-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="01143-116">U kunt handmatig uitvoeren de **ls** opdracht om te controleren of een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01143-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="01143-117">In deze map te zoeken naar de **azure** , dit pakket de bibliotheken die u nodig hebt bevat voor toegang tot de Service Bus-onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="01143-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="01143-118">Importeer de module</span><span class="sxs-lookup"><span data-stu-id="01143-118">Import the module</span></span>
<span data-ttu-id="01143-119">Het volgende in Kladblok of een andere teksteditor toevoegen aan de bovenkant van de **server.js** -bestand van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="01143-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="01143-120">Een Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="01143-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="01143-121">De Azure-module leest de omgevingsvariabelen `AZURE_SERVICEBUS_NAMESPACE` en `AZURE_SERVICEBUS_ACCESS_KEY` voor de benodigde informatie om te verbinden met Service Bus.</span><span class="sxs-lookup"><span data-stu-id="01143-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="01143-122">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens opgeven bij het aanroepen van `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="01143-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="01143-123">Zie voor een voorbeeld van de omgevingsvariabelen instellen voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="01143-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="01143-124">Zie voor een voorbeeld van het instellen van de omgevingsvariabelen voor een Azure-Website [Node.js-webtoepassing met Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="01143-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="01143-125">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="01143-125">Create a topic</span></span>
<span data-ttu-id="01143-126">De **ServiceBusService** object kunt u werken met onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="01143-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="01143-127">De volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="01143-128">Voeg deze toe aan de bovenkant van de **server.js** bestand na de instructie voor het importeren van de azure-module:</span><span class="sxs-lookup"><span data-stu-id="01143-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="01143-129">Door het aanroepen van `createTopicIfNotExists` op de **ServiceBusService** object, wordt het opgegeven onderwerp geretourneerd (indien aanwezig) of een nieuw onderwerp met de opgegeven naam wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01143-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="01143-130">De volgende code gebruikt `createTopicIfNotExists` maken of verbinding maken met het onderwerp met de naam `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="01143-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="01143-131">De `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u kunt de standaardinstellingen voor onderwerp zoals bericht of grootte van het maximum aantal onderwerp negeren.</span><span class="sxs-lookup"><span data-stu-id="01143-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="01143-132">Het volgende voorbeeld wordt de grootte van het maximum aantal onderwerp ingesteld op 5GB met een levensduur van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="01143-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="01143-133">Filters</span><span class="sxs-lookup"><span data-stu-id="01143-133">Filters</span></span>
<span data-ttu-id="01143-134">Optionele filteren bewerkingen kunnen worden toegepast op de bewerkingen die worden uitgevoerd met behulp van **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="01143-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="01143-135">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met de handtekening implementeren:</span><span class="sxs-lookup"><span data-stu-id="01143-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="01143-136">Na het uitvoeren van voorverwerking van de aanvraag-opties, de methode roept `next`, een retouraanroep met de volgende handtekening doorgeven:</span><span class="sxs-lookup"><span data-stu-id="01143-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="01143-137">In deze retouraanroep en na de verwerking de `returnObject` (de reactie van de aanvraag naar de server), de callback moet vervolgens worden aangeroepen als het al bestaat als u wilt doorgaan met het verwerken van andere filters of aanroepen `finalCallback` anders wordt de aanroep van de service beëindigen.</span><span class="sxs-lookup"><span data-stu-id="01143-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="01143-138">Twee filters die Pogingslogica implementeren zijn opgenomen in de Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="01143-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="01143-139">De volgende code maakt een **ServiceBusService** -object dat gebruikmaakt van de **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="01143-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="01143-140">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="01143-140">Create subscriptions</span></span>
<span data-ttu-id="01143-141">Ook onderwerpabonnementen worden gemaakt met de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="01143-142">Abonnementen kunnen worden genoemd en een optioneel filter waarmee de verzameling berichten in de virtuele wachtrij van het abonnement wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="01143-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="01143-143">Abonnementen worden permanent en blijft bestaan totdat beide ze of het onderwerp zijn gekoppeld, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="01143-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="01143-144">Als uw toepassing bevat de logica voor het maken van een abonnement, moet deze eerst controleren als het abonnement bestaat al met behulp van de `getSubscription` methode.</span><span class="sxs-lookup"><span data-stu-id="01143-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="01143-145">Een abonnement maken met het standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="01143-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="01143-146">Het **MatchAll**-filter is het standaardfilter dat wordt gebruikt als er bij het maken van een nieuw abonnement geen filter is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="01143-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="01143-147">Wanneer de **MatchAll** filter wordt gebruikt, worden alle berichten die zijn gepubliceerd naar het onderwerp in de virtuele wachtrij van het abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="01143-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="01143-148">Het volgende voorbeeld wordt een abonnement genaamd 'AllMessages' en gebruikt de standaardinstallatielocatie **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="01143-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="01143-149">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="01143-149">Create subscriptions with filters</span></span>
<span data-ttu-id="01143-150">U kunt ook filters maken waarmee u bereik dat berichten worden verzonden naar een onderwerp binnen een bepaald onderwerpabonnement weergegeven.</span><span class="sxs-lookup"><span data-stu-id="01143-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="01143-151">Het meest flexibele type filter dat wordt ondersteund door abonnementen is de **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="01143-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="01143-152">SQL-filters worden uitgevoerd voor de eigenschappen van de berichten die worden gepubliceerd naar het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="01143-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="01143-153">Raadpleeg voor meer informatie over de expressies die kunnen worden gebruikt met een SQL-filter, de [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.</span><span class="sxs-lookup"><span data-stu-id="01143-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="01143-154">Filters kunnen worden toegevoegd aan een abonnement met behulp van de `createRule` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="01143-155">Deze methode kunt u nieuwe filters toevoegen aan een bestaand abonnement.</span><span class="sxs-lookup"><span data-stu-id="01143-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="01143-156">Omdat het standaardfilter automatisch op alle nieuwe abonnementen toegepast wordt, moet u eerst het standaardfilter verwijderen of de **MatchAll** overschrijft alle andere filters die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="01143-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="01143-157">U kunt de standaardregel verwijderen met behulp van de `deleteRule` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="01143-158">Het volgende voorbeeld wordt een abonnement genaamd `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:</span><span class="sxs-lookup"><span data-stu-id="01143-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="01143-159">Op deze manier in het volgende voorbeeld wordt een abonnement genaamd `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk aan 3:</span><span class="sxs-lookup"><span data-stu-id="01143-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="01143-160">Wanneer is nu een bericht verzonden naar `MyTopic`, deze wordt altijd worden bezorgd bij ontvangers die zijn geabonneerd op de `AllMessages` onderwerpabonnement en selectief bezorgd bij ontvangers die zijn geabonneerd op de `HighMessages` en `LowMessages` onderwerp abonnementen ( afhankelijk van de inhoud van het bericht).</span><span class="sxs-lookup"><span data-stu-id="01143-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="01143-161">Het verzenden van berichten naar een onderwerp</span><span class="sxs-lookup"><span data-stu-id="01143-161">How to send messages to a topic</span></span>
<span data-ttu-id="01143-162">Als u wilt een bericht verzendt naar een Service Bus-onderwerp, de toepassing moet gebruiken de `sendTopicMessage` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="01143-163">Berichten die worden verzonden naar Service Bus-onderwerpen zijn **BrokeredMessage** objecten.</span><span class="sxs-lookup"><span data-stu-id="01143-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="01143-164">**BrokeredMessage** objecten hebben een aantal standaardeigenschappen (zoals `Label` en `TimeToLive`), een woordenlijst die wordt gebruikt om aangepaste toepassingsspecifieke eigenschappen te bewaren en een hoofdtekst met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="01143-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="01143-165">Een toepassing kunt instellen in de hoofdtekst van het bericht voor het doorgeven van een tekenreekswaarde naar het `sendTopicMessage` en alle vereiste standaardeigenschappen standaardwaarden worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="01143-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="01143-166">Het volgende voorbeeld toont hoe vijf testberichten naar verzendt `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="01143-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="01143-167">Houd er rekening mee dat de `messagenumber` eigenschapswaarde van elk bericht varieert op de herhaling van de lus (dit wordt bepaald welke abonnementen ontvangen):</span><span class="sxs-lookup"><span data-stu-id="01143-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="01143-168">Service Bus-onderwerpen ondersteunen een maximale grootte van 256 kB in de [Standard-laag](service-bus-premium-messaging.md) en 1 MB in de [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="01143-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="01143-169">De koptekst, die de standaard- en aangepaste toepassingseigenschappen bevat, kan maximaal 64 kB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="01143-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="01143-170">Er is geen limiet voor het aantal berichten in een onderwerp, maar er is een limiet voor de totale grootte van de berichten in een onderwerp.</span><span class="sxs-lookup"><span data-stu-id="01143-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="01143-171">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="01143-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="01143-172">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="01143-172">Receive messages from a subscription</span></span>
<span data-ttu-id="01143-173">Berichten worden ontvangen van een abonnement met de `receiveSubscriptionMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="01143-174">Standaard worden berichten uit het abonnement verwijderd als ze worden gelezen; u kunt echter (peek) lezen en vergrendelen van het bericht zonder het te verwijderen uit het abonnement door de optionele parameter `isPeekLock` naar **true**.</span><span class="sxs-lookup"><span data-stu-id="01143-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="01143-175">Het standaardgedrag van lezen van en het bericht is verwijderd als onderdeel van de bewerking receive is het eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht bij een storing.</span><span class="sxs-lookup"><span data-stu-id="01143-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="01143-176">Neem bijvoorbeeld een scenario waarin de consument de ontvangstaanvraag uitgeeft en het systeem vervolgens vastloopt voordat de aanvraag wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="01143-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="01143-177">Omdat Service Bus het bericht als verbruikt heeft gemarkeerd, klikt u vervolgens wanneer de toepassing opnieuw wordt opgestart en het verbruik van berichten opnieuw begint, ontbreekt het bericht dat voor het vastlopen is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="01143-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="01143-178">Als de `isPeekLock` parameter is ingesteld op **true**, wordt het ontvangen, wordt een bewerking met twee fasen, waardoor er mogelijk worden ondersteuning voor toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="01143-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="01143-179">Als Service Bus een aanvraag ontvangt, wordt het volgende te verbruiken bericht gevonden, wordt het bericht vergrendeld om te voorkomen dat andere consumenten het ontvangen en wordt het bericht vervolgens naar de toepassing geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="01143-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="01143-180">Nadat de toepassing klaar is met verwerking van het bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase van het ontvangstproces voltooid door het aanroepen van **deleteMessage** methode en het geven van het bericht moet worden verwijderd als een parameter.</span><span class="sxs-lookup"><span data-stu-id="01143-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="01143-181">De **deleteMessage** methode wordt het bericht als verbruikt markeren en deze te verwijderen uit het abonnement.</span><span class="sxs-lookup"><span data-stu-id="01143-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="01143-182">Het volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="01143-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="01143-183">In het voorbeeld eerst ontvangt en wordt een bericht wordt verwijderd uit het abonnement 'LowMessages' en vervolgens een bericht ontvangt van de 'HighMessages' abonnement met behulp `isPeekLock` is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="01143-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="01143-184">Vervolgens wordt verwijderd het bericht met `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="01143-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="01143-185">Het vastlopen van de toepassing en onleesbare berichten afhandelen</span><span class="sxs-lookup"><span data-stu-id="01143-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="01143-186">Service Bus biedt functionaliteit om netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="01143-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="01143-187">Als een ontvangende toepassing kan niet worden verwerkt het bericht om een bepaalde reden, dan kan worden aangeroepen de `unlockMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="01143-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="01143-188">Dit zorgt ervoor dat Service Bus het bericht in het abonnement ontgrendelt en beschikbaar zijn om opnieuw te ontvangen, ofwel door dezelfde consumerende toepassing of door een andere consumerende toepassing.</span><span class="sxs-lookup"><span data-stu-id="01143-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="01143-189">Er is ook een time-out gekoppeld aan een bericht in het abonnement is vergrendeld en als de toepassing niet kan verwerken van het bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als de toepassing vastloopt), en vervolgens de Service Bus het bericht automatisch ontgrendelt en wordt het beschikbaar worden om opnieuw te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="01143-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="01143-190">In het geval dat de toepassing is vastgelopen na het verwerken van het bericht, maar voordat de `deleteMessage` methode wordt aangeroepen en vervolgens het bericht opnieuw bezorgd bij de toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="01143-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="01143-191">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in sommige situaties hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="01143-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="01143-192">Als in het scenario dubbele verwerking niet wordt getolereerd, dan moeten toepassingsontwikkelaars extra logica toevoegen aan de toepassing om dubbele berichtbezorging af te handelen.</span><span class="sxs-lookup"><span data-stu-id="01143-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="01143-193">Dit wordt vaak bereikt met behulp van de **MessageId** eigenschap van het bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="01143-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="01143-194">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="01143-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="01143-195">Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via de [Azure-portal] [ Azure portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="01143-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="01143-196">Het volgende voorbeeld laat zien hoe u het onderwerp met de naam `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="01143-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="01143-197">Als u een onderwerp verwijdert, verwijdert ook alle abonnementen die zijn geregistreerd bij het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="01143-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="01143-198">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="01143-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="01143-199">Het volgende voorbeeld laat zien hoe u een abonnement met de naam `HighMessages` van de `MyTopic` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="01143-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="01143-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01143-200">Next Steps</span></span>
<span data-ttu-id="01143-201">Nu u de basisprincipes van Service Bus-onderwerpen hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="01143-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="01143-202">Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="01143-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="01143-203">API-naslaginformatie voor [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="01143-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="01143-204">Ga naar de [Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="01143-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[maken en implementeren van een Node.js-toepassing naar een Azure-website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
