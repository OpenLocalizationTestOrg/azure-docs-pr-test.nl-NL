---
title: aaaScenario - Trigger logische apps met Azure Functions en Azure Service Bus | Microsoft Docs
description: Een functie tootrigger een logische app maken met behulp van Azure Functions en Azure Service Bus
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="87b5c-103">Scenario: Een logische app met Azure Functions en Azure Service Bus activeren</span><span class="sxs-lookup"><span data-stu-id="87b5c-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="87b5c-104">Als u toodeploy een langlopende listener of taak nodig hebt, kunt u Azure Functions toocreate een trigger voor een logische app.</span><span class="sxs-lookup"><span data-stu-id="87b5c-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="87b5c-105">U kunt bijvoorbeeld een functie die een wachtrij luistert maken en een logische app als een push-signaal wordt direct gestart.</span><span class="sxs-lookup"><span data-stu-id="87b5c-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="87b5c-106">Hallo logische app bouwen</span><span class="sxs-lookup"><span data-stu-id="87b5c-106">Build hello logic app</span></span>
<span data-ttu-id="87b5c-107">In dit voorbeeld hebt u een functie die wordt uitgevoerd voor elke logische app, die toobe geactiveerd behoeften.</span><span class="sxs-lookup"><span data-stu-id="87b5c-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="87b5c-108">Maak eerst een logische app, die een HTTP-verzoek-trigger heeft.</span><span class="sxs-lookup"><span data-stu-id="87b5c-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="87b5c-109">Hallo-functie aanroepen dat eindpunt wanneer er een wachtrijbericht is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="87b5c-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="87b5c-110">Een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="87b5c-110">Create a logic app.</span></span>
2. <span data-ttu-id="87b5c-111">Selecteer Hallo **handmatig - wanneer er een HTTP-aanvraag wordt ontvangen** trigger.</span><span class="sxs-lookup"><span data-stu-id="87b5c-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="87b5c-112">Desgewenst kunt u een JSON-schema toouse met wachtrij het Hallo-bericht met behulp van een hulpprogramma zoals [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="87b5c-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="87b5c-113">Hallo-schema in Hallo trigger te plakken.</span><span class="sxs-lookup"><span data-stu-id="87b5c-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="87b5c-114">Schema's helpen bij het Hallo-designer Hallo vorm van gegevens en stroom eigenschappen Hallo gemakkelijker via Hallo workflow begrijpen.</span><span class="sxs-lookup"><span data-stu-id="87b5c-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="87b5c-115">Voeg eventuele extra stappen die u wilt toooccur nadat een wachtrijbericht is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="87b5c-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="87b5c-116">Bijvoorbeeld, sturen een e-mail via Office 365.</span><span class="sxs-lookup"><span data-stu-id="87b5c-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="87b5c-117">Hallo logic app toogenerate Hallo callback URL voor Hallo trigger toothis logische app opslaan.</span><span class="sxs-lookup"><span data-stu-id="87b5c-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="87b5c-118">Hallo-URL wordt weergegeven op Hallo trigger-kaart.</span><span class="sxs-lookup"><span data-stu-id="87b5c-118">hello URL appears on hello trigger card.</span></span>

![Hallo-callback URL wordt weergegeven op Hallo trigger-kaart][1]

## <a name="build-hello-function"></a><span data-ttu-id="87b5c-120">Hallo-functie maken</span><span class="sxs-lookup"><span data-stu-id="87b5c-120">Build hello function</span></span>
<span data-ttu-id="87b5c-121">Vervolgens moet u een functie die fungeert als Hallo trigger en luistert toohello wachtrij maken.</span><span class="sxs-lookup"><span data-stu-id="87b5c-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="87b5c-122">In Hallo [Azure Functions-portal](https://functions.azure.com/signin), selecteer **nieuwe functie**, en selecteer vervolgens Hallo **ServiceBusQueueTrigger - C#** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="87b5c-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions-portal][2]
2. <span data-ttu-id="87b5c-124">Hallo verbinding toohello Service Bus-wachtrij, die gebruikmaakt hello Azure Service Bus-SDK configureren `OnMessageReceive()` listener.</span><span class="sxs-lookup"><span data-stu-id="87b5c-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="87b5c-125">Schrijf een eenvoudige functie toocall Hallo logic app-eindpunt (eerder hebt gemaakt) met behulp van wachtrij het Hallo-bericht als een trigger.</span><span class="sxs-lookup"><span data-stu-id="87b5c-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="87b5c-126">Hier volgt een voorbeeld van een volledige van een functie.</span><span class="sxs-lookup"><span data-stu-id="87b5c-126">Here's a full example of a function.</span></span> <span data-ttu-id="87b5c-127">Hallo-voorbeeld wordt een `application/json` inhoud berichttype, maar u kunt dit type zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="87b5c-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="87b5c-128">tootest, toevoegen van een wachtrijbericht via een hulpprogramma zoals [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="87b5c-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="87b5c-129">Zie Hallo logische app gestart onmiddellijk nadat de functie Hallo Hallo-bericht ontvangt.</span><span class="sxs-lookup"><span data-stu-id="87b5c-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
