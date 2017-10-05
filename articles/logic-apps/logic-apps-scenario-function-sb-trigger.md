---
title: Scenario - Trigger logische apps met Azure Functions en Azure Service Bus | Microsoft Docs
description: Maken van een functie in om een logische app activeren met behulp van Azure Functions en Azure Service Bus
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="669a8-103">Scenario: Een logische app met Azure Functions en Azure Service Bus activeren</span><span class="sxs-lookup"><span data-stu-id="669a8-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="669a8-104">U kunt Azure Functions gebruiken voor het maken van een trigger voor een logische app wanneer u moet een langlopende listener of taak implementeren.</span><span class="sxs-lookup"><span data-stu-id="669a8-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="669a8-105">U kunt bijvoorbeeld een functie die een wachtrij luistert maken en een logische app als een push-signaal wordt direct gestart.</span><span class="sxs-lookup"><span data-stu-id="669a8-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="669a8-106">De logische app bouwen</span><span class="sxs-lookup"><span data-stu-id="669a8-106">Build the logic app</span></span>
<span data-ttu-id="669a8-107">In dit voorbeeld hebt u een functie die wordt uitgevoerd voor elke logische app die moet worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="669a8-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="669a8-108">Maak eerst een logische app, die een HTTP-verzoek-trigger heeft.</span><span class="sxs-lookup"><span data-stu-id="669a8-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="669a8-109">De functie aanroept dat eindpunt wanneer er een wachtrijbericht is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="669a8-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="669a8-110">Een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="669a8-110">Create a logic app.</span></span>
2. <span data-ttu-id="669a8-111">Selecteer de **handmatig - wanneer er een HTTP-aanvraag wordt ontvangen** trigger.</span><span class="sxs-lookup"><span data-stu-id="669a8-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="669a8-112">Desgewenst kunt u een JSON-schema te gebruiken met het bericht uit de wachtrij met behulp van een hulpprogramma zoals [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="669a8-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="669a8-113">Het schema in de trigger te plakken.</span><span class="sxs-lookup"><span data-stu-id="669a8-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="669a8-114">Schema's kunnen de ontwerpfunctie voor inzicht in de vorm van de gegevens en stroom eigenschappen gemakkelijker via de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="669a8-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="669a8-115">Eventuele extra stappen die u laten uitvoeren wilt na de ontvangst van een wachtrijbericht toevoegen.</span><span class="sxs-lookup"><span data-stu-id="669a8-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="669a8-116">Bijvoorbeeld, sturen een e-mail via Office 365.</span><span class="sxs-lookup"><span data-stu-id="669a8-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="669a8-117">Sla de logische app voor het genereren van de callback-URL voor de trigger aan deze logische app.</span><span class="sxs-lookup"><span data-stu-id="669a8-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="669a8-118">De URL wordt weergegeven op de trigger-kaart.</span><span class="sxs-lookup"><span data-stu-id="669a8-118">The URL appears on the trigger card.</span></span>

![De callback URL wordt weergegeven op de trigger-kaart][1]

## <a name="build-the-function"></a><span data-ttu-id="669a8-120">De functie bouwen</span><span class="sxs-lookup"><span data-stu-id="669a8-120">Build the function</span></span>
<span data-ttu-id="669a8-121">Vervolgens moet u een functie die fungeert als de trigger en luistert naar de wachtrij maken.</span><span class="sxs-lookup"><span data-stu-id="669a8-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="669a8-122">In de [Azure Functions-portal](https://functions.azure.com/signin), selecteer **nieuwe functie**, en selecteer vervolgens de **ServiceBusQueueTrigger - C#** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="669a8-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions-portal][2]
2. <span data-ttu-id="669a8-124">Configureer de verbinding met de Service Bus-wachtrij die gebruikmaakt van de SDK van Azure Service Bus `OnMessageReceive()` listener.</span><span class="sxs-lookup"><span data-stu-id="669a8-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="669a8-125">Een eenvoudige functie voor het aanroepen van de logische app-eindpunt (eerder hebt gemaakt) met behulp van bericht in de wachtrij als een trigger schrijven.</span><span class="sxs-lookup"><span data-stu-id="669a8-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="669a8-126">Hier volgt een voorbeeld van een volledige van een functie.</span><span class="sxs-lookup"><span data-stu-id="669a8-126">Here's a full example of a function.</span></span> <span data-ttu-id="669a8-127">In het voorbeeld wordt een `application/json` inhoud berichttype, maar u kunt dit type zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="669a8-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="669a8-128">Als u wilt testen, Voeg een wachtrijbericht via een hulpprogramma zoals [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="669a8-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="669a8-129">Zie de logische app gestart onmiddellijk nadat de functie heeft het bericht ontvangen.</span><span class="sxs-lookup"><span data-stu-id="669a8-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
