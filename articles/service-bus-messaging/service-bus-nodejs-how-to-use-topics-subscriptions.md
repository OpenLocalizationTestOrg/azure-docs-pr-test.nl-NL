---
title: aaaHow toouse Azure Service Bus-onderwerpen en abonnementen met behulp van Node.js | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus-onderwerpen en abonnementen in Azure van een Node.js-app.
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="b239e-103">Hoe tooUse Service Bus-onderwerpen en abonnementen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="b239e-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="b239e-104">Deze handleiding wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen van Node.js-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b239e-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="b239e-105">Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten** tooa onderwerp **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="b239e-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="b239e-106">Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="b239e-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="b239e-107">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="b239e-107">Create a Node.js application</span></span>
<span data-ttu-id="b239e-108">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b239e-108">Create a blank Node.js application.</span></span> <span data-ttu-id="b239e-109">Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing tooan Azure-website], [Node.js-Cloudservice] [ Node.js Cloud Service] met behulp van Windows PowerShell of website met WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="b239e-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="b239e-110">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="b239e-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="b239e-111">Service Bus toouse downloaden Hallo Node.js Azure-pakket.</span><span class="sxs-lookup"><span data-stu-id="b239e-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="b239e-112">Dit pakket bevat een set van bibliotheken die met Hallo Service Bus REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="b239e-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="b239e-113">Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="b239e-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="b239e-114">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u toohello map waar u uw voorbeeldtoepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b239e-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="b239e-115">Type **npm installeren azure** in Hallo opdrachtvenster moet die leiden tot Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="b239e-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="b239e-116">U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b239e-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="b239e-117">In deze map te zoeken naar de **azure** , dit pakket bevat, moet u Service Bus-onderwerpen tooaccess Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="b239e-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="b239e-118">Hallo-module importeren</span><span class="sxs-lookup"><span data-stu-id="b239e-118">Import hello module</span></span>
<span data-ttu-id="b239e-119">Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** bestand van de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="b239e-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="b239e-120">Een Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="b239e-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="b239e-121">Hello Azure module leest Hallo omgevingsvariabelen `AZURE_SERVICEBUS_NAMESPACE` en `AZURE_SERVICEBUS_ACCESS_KEY` vereist tooconnect tooService Bus voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b239e-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="b239e-122">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="b239e-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="b239e-123">Zie voor een voorbeeld van het Hallo-omgevingsvariabelen instellen voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="b239e-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="b239e-124">Zie voor een voorbeeld van het instellen van de omgevingsvariabelen Hallo voor een Azure-Website [Node.js-webtoepassing met Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="b239e-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="b239e-125">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="b239e-125">Create a topic</span></span>
<span data-ttu-id="b239e-126">Hallo **ServiceBusService** object kunt u toowork met onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b239e-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="b239e-127">De volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="b239e-128">Voeg deze toe aan de bovenkant van Hallo **server.js** bestand na Hallo instructie tooimport hello azure module:</span><span class="sxs-lookup"><span data-stu-id="b239e-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="b239e-129">Door het aanroepen van `createTopicIfNotExists` op Hallo **ServiceBusService** object, Hallo opgegeven onderwerp worden geretourneerd (indien aanwezig) of een nieuw onderwerp met de opgegeven naam hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b239e-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="b239e-130">Hallo volgende code gebruikt `createTopicIfNotExists` toocreate of verbinding maken met de naam toohello-onderwerp `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="b239e-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="b239e-131">Hallo `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht of grootte van het maximum aantal onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b239e-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="b239e-132">Hallo volgende voorbeeld wordt Hallo onderwerp maximale grootte too5GB met een tijd toolive van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="b239e-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="b239e-133">Filters</span><span class="sxs-lookup"><span data-stu-id="b239e-133">Filters</span></span>
<span data-ttu-id="b239e-134">Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="b239e-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="b239e-135">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:</span><span class="sxs-lookup"><span data-stu-id="b239e-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="b239e-136">Na het uitvoeren van voorverwerking op Hallo certificaataanvraagopties Hallo methodeaanroepen `next`, een retouraanroep wordt doorgegeven met Hallo handtekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="b239e-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="b239e-137">In deze retouraanroep en na verwerking Hallo `returnObject` (hello reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als het verwerken van andere filters toocontinue al bestaat of aan te roepen `finalCallback` anders tooend Hallo het aanroepen van de service.</span><span class="sxs-lookup"><span data-stu-id="b239e-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="b239e-138">Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="b239e-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="b239e-139">Hallo volgende maakt een **ServiceBusService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="b239e-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="b239e-140">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="b239e-140">Create subscriptions</span></span>
<span data-ttu-id="b239e-141">Onderwerpabonnementen worden ook gemaakt met de Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="b239e-142">Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="b239e-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="b239e-143">Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp ze zijn gekoppeld, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b239e-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="b239e-144">Als uw toepassing bevat de logica toocreate een abonnement, moet deze eerst controleren als Hallo abonnement bestaat al met behulp van de `getSubscription` methode.</span><span class="sxs-lookup"><span data-stu-id="b239e-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="b239e-145">Een abonnement maken met de Hallo standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="b239e-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="b239e-146">Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b239e-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="b239e-147">Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in de virtuele wachtrij van het abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b239e-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="b239e-148">Hallo volgende voorbeeld maakt u een abonnement genaamd 'AllMessages' en gebruikt standaard Hallo **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="b239e-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="b239e-149">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="b239e-149">Create subscriptions with filters</span></span>
<span data-ttu-id="b239e-150">U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement tooscope maken.</span><span class="sxs-lookup"><span data-stu-id="b239e-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="b239e-151">Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is de **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="b239e-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="b239e-152">SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn.</span><span class="sxs-lookup"><span data-stu-id="b239e-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="b239e-153">Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.</span><span class="sxs-lookup"><span data-stu-id="b239e-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="b239e-154">Filters kunnen tooa abonnement worden toegevoegd met behulp van Hallo `createRule` methode Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="b239e-155">Deze methode kunt u nieuwe filters tooan bestaande abonnement toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b239e-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b239e-156">Omdat het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo verwijderen of de **MatchAll** overschrijft alle andere filters die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="b239e-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="b239e-157">U kunt de standaardregel Hallo verwijderen via Hallo `deleteRule` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="b239e-158">Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:</span><span class="sxs-lookup"><span data-stu-id="b239e-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="b239e-159">Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk too3:</span><span class="sxs-lookup"><span data-stu-id="b239e-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="b239e-160">Wanneer een bericht nu te verzonden`MyTopic`, worden altijd geleverd naar ontvangers die zijn geabonneerd toohello `AllMessages` onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` onderwerpabonnementen (al naar gelang de inhoud van de Hallo-bericht).</span><span class="sxs-lookup"><span data-stu-id="b239e-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="b239e-161">Hoe toosend tooa onderwerp berichten</span><span class="sxs-lookup"><span data-stu-id="b239e-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="b239e-162">een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken de `sendTopicMessage` methode Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="b239e-163">Berichten verzonden tooService Bus-onderwerpen zijn **BrokeredMessage** objecten.</span><span class="sxs-lookup"><span data-stu-id="b239e-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="b239e-164">**BrokeredMessage** objecten hebben een aantal standaardeigenschappen (zoals `Label` en `TimeToLive`), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="b239e-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="b239e-165">Een toepassing hello hoofdtekst van het Hallo-bericht worden ingesteld door een string-waarde wordt doorgegeven aan Hallo `sendTopicMessage` en alle vereiste standaardeigenschappen standaardwaarden worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="b239e-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="b239e-166">Hallo volgende voorbeeld laat zien hoe toosend vijf testberichten naar `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="b239e-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="b239e-167">Houd er rekening mee dat Hallo `messagenumber` eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (dit wordt bepaald welke abonnementen ontvangen):</span><span class="sxs-lookup"><span data-stu-id="b239e-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="b239e-168">Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="b239e-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="b239e-169">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="b239e-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="b239e-170">Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b239e-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="b239e-171">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="b239e-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="b239e-172">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="b239e-172">Receive messages from a subscription</span></span>
<span data-ttu-id="b239e-173">Berichten worden ontvangen van een abonnement met de `receiveSubscriptionMessage` methode op Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="b239e-174">Standaard worden berichten verwijderd uit het Hallo-abonnement als ze worden gelezen; echter (peek) lezen en vergrendelen Hallo-bericht zonder het te verwijderen uit het Hallo-abonnement door de optionele parameter Hallo instelling `isPeekLock` te**true**.</span><span class="sxs-lookup"><span data-stu-id="b239e-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="b239e-175">standaardgedrag Hallo van lezen en verwijderen van het Hallo-bericht als onderdeel van de bewerking receive het eenvoudigste model Hallo is en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="b239e-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="b239e-176">toounderstand dit, Neem bijvoorbeeld een scenario waarin de consument problemen Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b239e-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="b239e-177">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b239e-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="b239e-178">Als hello `isPeekLock` parameter is ingesteld, te**true**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="b239e-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b239e-179">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="b239e-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="b239e-180">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is Hallo tweede fase van het ontvangstproces voltooid door het aanroepen van **deleteMessage** methode en het geven van het bericht toobe Als een parameter is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b239e-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="b239e-181">Hallo **deleteMessage** methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b239e-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="b239e-182">Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="b239e-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="b239e-183">Hallo voorbeeld eerst ontvangt en wordt een bericht uit de Hallo 'LowMessages' abonnement verwijderd en vervolgens een bericht ontvangt van het gebruik van Hallo 'HighMessages' abonnement `isPeekLock` tootrue ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b239e-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="b239e-184">Vervolgens wordt verwijderd Hallo-bericht met `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="b239e-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="b239e-185">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="b239e-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="b239e-186">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="b239e-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="b239e-187">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b239e-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="b239e-188">Dit wordt Service Bus toounlock veroorzaken binnen Hallo-abonnement en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b239e-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="b239e-189">Daarnaast is er een time-out gekoppeld aan een bericht in het abonnement is vergrendeld en als de toepassing hello tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus Hiermee ontgrendelt u het Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b239e-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="b239e-190">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b239e-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="b239e-191">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="b239e-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="b239e-192">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b239e-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="b239e-193">Dit wordt vaak bereikt met behulp van de **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="b239e-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="b239e-194">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="b239e-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="b239e-195">Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="b239e-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="b239e-196">Hallo volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="b239e-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="b239e-197">Als u een onderwerp verwijdert, verwijdert ook alle abonnementen die zijn geregistreerd bij Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b239e-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="b239e-198">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b239e-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="b239e-199">Het volgende voorbeeld ziet u hoe toodelete een abonnement met de naam `HighMessages` van Hallo `MyTopic` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="b239e-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="b239e-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b239e-200">Next Steps</span></span>
<span data-ttu-id="b239e-201">Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="b239e-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="b239e-202">Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="b239e-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="b239e-203">API-naslaginformatie voor [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="b239e-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="b239e-204">Ga naar Hallo [Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="b239e-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[maken en implementeren van een Node.js-toepassing tooan Azure-website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
