---
title: Werkstroomacties en triggers - Azure Logic Apps | Microsoft Docs
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="b9278-102">Werkstroomacties en triggers voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b9278-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="b9278-103">Logische apps bestaan uit het triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="b9278-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="b9278-104">Er zijn zes soorten triggers.</span><span class="sxs-lookup"><span data-stu-id="b9278-104">There are six types of triggers.</span></span> <span data-ttu-id="b9278-105">Elk type heeft een andere interface en ander gedrag.</span><span class="sxs-lookup"><span data-stu-id="b9278-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="b9278-106">U kunt ook meer informatie over andere gegevens door te kijken in de details van de [werkstroom Definition Language](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="b9278-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="b9278-107">Lees verder voor meer informatie over triggers en acties en hoe u ze kunt gebruiken voor het bouwen van logic apps om uw bedrijfsprocessen en werkstromen te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="b9278-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="b9278-108">Triggers</span><span class="sxs-lookup"><span data-stu-id="b9278-108">Triggers</span></span>  

<span data-ttu-id="b9278-109">Een trigger geeft de oproepen die een uitvoering van uw logische app werkstroom kunnen initiëren.</span><span class="sxs-lookup"><span data-stu-id="b9278-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="b9278-110">Hier volgen de twee verschillende manieren een uitvoering van uw werkstroom te starten:</span><span class="sxs-lookup"><span data-stu-id="b9278-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="b9278-111">Een polling-trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-111">A polling trigger</span></span>  

-   <span data-ttu-id="b9278-112">Een push-signaal - door het aanroepen van de [REST-API van Workflow](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="b9278-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="b9278-113">Alle triggers bevatten deze op het hoogste niveau elementen:</span><span class="sxs-lookup"><span data-stu-id="b9278-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="b9278-114">Triggertypen en hun invoer</span><span class="sxs-lookup"><span data-stu-id="b9278-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="b9278-115">U kunt deze typen triggers:</span><span class="sxs-lookup"><span data-stu-id="b9278-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="b9278-116">**Aanvraag** \- de logische app maakt een eindpunt voor u aan te roepen</span><span class="sxs-lookup"><span data-stu-id="b9278-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="b9278-117">**Terugkeerpatroon** \- deze gebeurtenis wordt gestart op basis van een gedefinieerde planning</span><span class="sxs-lookup"><span data-stu-id="b9278-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="b9278-118">**HTTP** \- een HTTP-web-eindpunt worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="b9278-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="b9278-119">Het HTTP-eindpunt moet voldoen aan een specifieke activerende contract \- met behulp van een 202\-asynchrone patroon, of door te retourneren van een matrix</span><span class="sxs-lookup"><span data-stu-id="b9278-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="b9278-120">**ApiConnection** \- Polls zoals HTTP is geactiveerd, maar deze wordt gebruikgemaakt van de [door Microsoft beheerde API's](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="b9278-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="b9278-121">**HTTPWebhook** \- opent een eindpunt, vergelijkbaar met de handmatige trigger echter ook roept uit met een opgegeven URL registreren en ongedaan maken</span><span class="sxs-lookup"><span data-stu-id="b9278-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="b9278-122">**ApiConnectionWebhook** \- werkt zoals de trigger HTTPWebhook door gebruik te maken van de API door Microsoft beheerd</span><span class="sxs-lookup"><span data-stu-id="b9278-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="b9278-123">Elk triggertype heeft een andere set **invoer** het gedrag te definiëren.</span><span class="sxs-lookup"><span data-stu-id="b9278-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="b9278-124">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-124">Request trigger</span></span>  

<span data-ttu-id="b9278-125">Deze trigger fungeert als een eindpunt dat u via een HTTP-aanvraag om aan te roepen uw logische app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9278-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="b9278-126">Een aanvraag-trigger ziet er in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="b9278-127">Er is ook een optionele eigenschap aangeroepen **schema**:</span><span class="sxs-lookup"><span data-stu-id="b9278-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="b9278-128">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-128">Element name</span></span>|<span data-ttu-id="b9278-129">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-129">Required</span></span>|<span data-ttu-id="b9278-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="b9278-131">Schema</span><span class="sxs-lookup"><span data-stu-id="b9278-131">schema</span></span>|<span data-ttu-id="b9278-132">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-132">No</span></span>|<span data-ttu-id="b9278-133">Een JSON-schema te valideren en de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b9278-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="b9278-134">Handig voor het helpen werkstroomstappen van de volgende weten welke eigenschappen om te verwijzen.</span><span class="sxs-lookup"><span data-stu-id="b9278-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="b9278-135">Om aan te roepen dit eindpunt, moet u aan te roepen de *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="b9278-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="b9278-136">Zie [REST-API van werkstroom](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="b9278-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="b9278-137">Terugkeerpatroon trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-137">Recurrence trigger</span></span>  

<span data-ttu-id="b9278-138">Een terugkeerpatroon trigger is die wordt uitgevoerd op basis volgens een ingesteld schema.</span><span class="sxs-lookup"><span data-stu-id="b9278-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="b9278-139">Dergelijke trigger lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="b9278-140">Zoals u ziet, is een eenvoudige manier voor het uitvoeren van een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="b9278-141">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-141">Element name</span></span>|<span data-ttu-id="b9278-142">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-142">Required</span></span>|<span data-ttu-id="b9278-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="b9278-144">Frequentie</span><span class="sxs-lookup"><span data-stu-id="b9278-144">frequency</span></span>|<span data-ttu-id="b9278-145">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-145">Yes</span></span>|<span data-ttu-id="b9278-146">Hoe vaak de trigger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-146">How often the trigger executes.</span></span> <span data-ttu-id="b9278-147">Gebruik slechts één van deze mogelijke waarden: seconde, minuut, uur, dag, week, maand of jaar</span><span class="sxs-lookup"><span data-stu-id="b9278-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="b9278-148">Interval</span><span class="sxs-lookup"><span data-stu-id="b9278-148">interval</span></span>|<span data-ttu-id="b9278-149">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-149">Yes</span></span>|<span data-ttu-id="b9278-150">Interval van de opgegeven frequentie voor het terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="b9278-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="b9278-151">startTime</span><span class="sxs-lookup"><span data-stu-id="b9278-151">startTime</span></span>|<span data-ttu-id="b9278-152">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-152">No</span></span>|<span data-ttu-id="b9278-153">Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="b9278-154">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="b9278-154">timeZone</span></span>|<span data-ttu-id="b9278-155">Er is geen</span><span class="sxs-lookup"><span data-stu-id="b9278-155">no</span></span>|<span data-ttu-id="b9278-156">Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="b9278-157">U kunt ook een trigger worden gestart in de toekomst wordt uitgevoerd op een bepaald moment plannen.</span><span class="sxs-lookup"><span data-stu-id="b9278-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="b9278-158">Als u wilt een wekelijks rapport elke maandag starten kunt u bijvoorbeeld de logische app aan elke maandag begint met het maken van de volgende trigger plannen:</span><span class="sxs-lookup"><span data-stu-id="b9278-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="b9278-159">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-159">HTTP trigger</span></span>  

<span data-ttu-id="b9278-160">HTTP-triggers peilen op een opgegeven eindpunt en controleert u het antwoord om te bepalen of de werkstroom moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="b9278-161">De invoer-object wordt gebruikt in de set parameters die zijn vereist om een HTTP-aanroep samen te stellen:</span><span class="sxs-lookup"><span data-stu-id="b9278-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="b9278-162">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-162">Element name</span></span>|<span data-ttu-id="b9278-163">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-163">Required</span></span>|<span data-ttu-id="b9278-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-164">Description</span></span>|<span data-ttu-id="b9278-165">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="b9278-166">Methode</span><span class="sxs-lookup"><span data-stu-id="b9278-166">method</span></span>|<span data-ttu-id="b9278-167">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-167">yes</span></span>|<span data-ttu-id="b9278-168">Kan een van de volgende HTTP-methoden zijn: GET, POST, PUT, DELETE, PATCH of HEAD</span><span class="sxs-lookup"><span data-stu-id="b9278-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="b9278-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-169">String</span></span>|  
|<span data-ttu-id="b9278-170">URI</span><span class="sxs-lookup"><span data-stu-id="b9278-170">uri</span></span>|<span data-ttu-id="b9278-171">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-171">yes</span></span>|<span data-ttu-id="b9278-172">Het http of https-eindpunt dat wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="b9278-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="b9278-173">Maximum van 2 kB.</span><span class="sxs-lookup"><span data-stu-id="b9278-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="b9278-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-174">String</span></span>|  
|<span data-ttu-id="b9278-175">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-175">queries</span></span>|<span data-ttu-id="b9278-176">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-176">No</span></span>|<span data-ttu-id="b9278-177">Een object dat de queryparameters toevoegen aan de URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="b9278-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="b9278-178">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="b9278-179">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-179">Object</span></span>|  
|<span data-ttu-id="b9278-180">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-180">headers</span></span>|<span data-ttu-id="b9278-181">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-181">No</span></span>|<span data-ttu-id="b9278-182">Object voor elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-183">Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="b9278-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="b9278-184">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-184">Object</span></span>|  
|<span data-ttu-id="b9278-185">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-185">body</span></span>|<span data-ttu-id="b9278-186">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-186">No</span></span>|<span data-ttu-id="b9278-187">Een object dat de nettolading dat wordt verzonden naar het eindpunt vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="b9278-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="b9278-188">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-188">Object</span></span>|  
|<span data-ttu-id="b9278-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="b9278-189">retryPolicy</span></span>|<span data-ttu-id="b9278-190">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-190">No</span></span>|<span data-ttu-id="b9278-191">Een object dat u kunt het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b9278-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="b9278-192">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-192">Object</span></span>|  
|<span data-ttu-id="b9278-193">Verificatie</span><span class="sxs-lookup"><span data-stu-id="b9278-193">authentication</span></span>|<span data-ttu-id="b9278-194">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-194">No</span></span>|<span data-ttu-id="b9278-195">Hiermee geeft u de methode die de aanvraag moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="b9278-196">Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="b9278-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="b9278-197">Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority` deze waarde is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="b9278-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="b9278-198">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-198">Object</span></span>|  
  
<span data-ttu-id="b9278-199">De HTTP-trigger is vereist voor de HTTP-API om te voldoen aan een specifiek patroon voor gebruik met uw logische app.</span><span class="sxs-lookup"><span data-stu-id="b9278-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="b9278-200">Hiervoor de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="b9278-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="b9278-201">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b9278-201">Response</span></span>|<span data-ttu-id="b9278-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="b9278-203">Statuscode</span><span class="sxs-lookup"><span data-stu-id="b9278-203">Status code</span></span>|<span data-ttu-id="b9278-204">Statuscode 200 \(OK\) run veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="b9278-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="b9278-205">Andere statuscode niet leiden tot een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="b9278-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="b9278-206">Probeer\-na header</span><span class="sxs-lookup"><span data-stu-id="b9278-206">Retry\-after header</span></span>|<span data-ttu-id="b9278-207">Het aantal seconden tot de logische app het eindpunt opnieuw worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="b9278-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="b9278-208">Locatieheader</span><span class="sxs-lookup"><span data-stu-id="b9278-208">Location header</span></span>|<span data-ttu-id="b9278-209">De URL aan te roepen voor de volgende pollinginterval.</span><span class="sxs-lookup"><span data-stu-id="b9278-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="b9278-210">Als niet wordt opgegeven, wordt de oorspronkelijke URL gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="b9278-211">Hier volgen enkele voorbeelden van andere problemen voor verschillende soorten aanvragen:</span><span class="sxs-lookup"><span data-stu-id="b9278-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="b9278-212">Reactiecode</span><span class="sxs-lookup"><span data-stu-id="b9278-212">Response code</span></span>|<span data-ttu-id="b9278-213">Probeer\-na</span><span class="sxs-lookup"><span data-stu-id="b9278-213">Retry\-After</span></span>|<span data-ttu-id="b9278-214">Gedrag</span><span class="sxs-lookup"><span data-stu-id="b9278-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="b9278-215">200</span><span class="sxs-lookup"><span data-stu-id="b9278-215">200</span></span>|<span data-ttu-id="b9278-216">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="b9278-216">\(none\)</span></span>|<span data-ttu-id="b9278-217">Niet een geldig worden geactiveerd, opnieuw proberen\-na is vereist, of anders de engine nooit worden opgevraagd voor de volgende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b9278-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="b9278-218">202</span><span class="sxs-lookup"><span data-stu-id="b9278-218">202</span></span>|<span data-ttu-id="b9278-219">60</span><span class="sxs-lookup"><span data-stu-id="b9278-219">60</span></span>|<span data-ttu-id="b9278-220">De werkstroom niet activeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-220">Do not trigger the workflow.</span></span> <span data-ttu-id="b9278-221">De volgende poging gebeurt in een minuut.</span><span class="sxs-lookup"><span data-stu-id="b9278-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="b9278-222">200</span><span class="sxs-lookup"><span data-stu-id="b9278-222">200</span></span>|<span data-ttu-id="b9278-223">10</span><span class="sxs-lookup"><span data-stu-id="b9278-223">10</span></span>|<span data-ttu-id="b9278-224">De werkstroom uitvoert, en opnieuw controleren voor meer informatie over 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="b9278-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="b9278-225">400</span><span class="sxs-lookup"><span data-stu-id="b9278-225">400</span></span>|<span data-ttu-id="b9278-226">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="b9278-226">\(none\)</span></span>|<span data-ttu-id="b9278-227">Onjuiste aanvraag, de werkstroom niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="b9278-228">Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="b9278-229">Nadat u het aantal nieuwe pogingen is bereikt, is de trigger niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="b9278-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="b9278-230">500</span><span class="sxs-lookup"><span data-stu-id="b9278-230">500</span></span>|<span data-ttu-id="b9278-231">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="b9278-231">\(none\)</span></span>|<span data-ttu-id="b9278-232">Fout-server, worden de werkstroom niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="b9278-233">Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="b9278-234">Nadat u het aantal nieuwe pogingen is bereikt, is de trigger niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="b9278-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="b9278-235">De uitvoer van een HTTP-trigger eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="b9278-236">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-236">Element name</span></span>|<span data-ttu-id="b9278-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-237">Description</span></span>|<span data-ttu-id="b9278-238">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="b9278-239">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-239">headers</span></span>|<span data-ttu-id="b9278-240">De headers van de http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="b9278-240">The headers of the http response.</span></span>|<span data-ttu-id="b9278-241">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-241">Object</span></span>|  
|<span data-ttu-id="b9278-242">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-242">body</span></span>|<span data-ttu-id="b9278-243">De hoofdtekst van het http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="b9278-243">The body of the http response.</span></span>|<span data-ttu-id="b9278-244">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="b9278-245">API-verbinding activeren</span><span class="sxs-lookup"><span data-stu-id="b9278-245">API Connection trigger</span></span>  

<span data-ttu-id="b9278-246">De API verbinding trigger is vergelijkbaar met de HTTP-trigger in de basisfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="b9278-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="b9278-247">De parameters voor het identificeren van de actie zijn echter verschillend.</span><span class="sxs-lookup"><span data-stu-id="b9278-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="b9278-248">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="b9278-249">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-249">Element name</span></span>|<span data-ttu-id="b9278-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-250">Required</span></span>|<span data-ttu-id="b9278-251">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-251">Type</span></span>|<span data-ttu-id="b9278-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="b9278-253">host</span><span class="sxs-lookup"><span data-stu-id="b9278-253">host</span></span>|<span data-ttu-id="b9278-254">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-254">Yes</span></span>||<span data-ttu-id="b9278-255">De ApiApp gehost gateway en -id.</span><span class="sxs-lookup"><span data-stu-id="b9278-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="b9278-256">Methode</span><span class="sxs-lookup"><span data-stu-id="b9278-256">method</span></span>|<span data-ttu-id="b9278-257">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-257">Yes</span></span>|<span data-ttu-id="b9278-258">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-258">String</span></span>|<span data-ttu-id="b9278-259">Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="b9278-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="b9278-260">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-260">queries</span></span>|<span data-ttu-id="b9278-261">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-261">No</span></span>|<span data-ttu-id="b9278-262">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-262">Object</span></span>|<span data-ttu-id="b9278-263">Vertegenwoordigt de queryparameters worden toegevoegd aan de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="b9278-264">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="b9278-265">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-265">headers</span></span>|<span data-ttu-id="b9278-266">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-266">No</span></span>|<span data-ttu-id="b9278-267">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-267">Object</span></span>|<span data-ttu-id="b9278-268">Hiermee geeft u elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-269">Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="b9278-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="b9278-270">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-270">body</span></span>|<span data-ttu-id="b9278-271">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-271">No</span></span>|<span data-ttu-id="b9278-272">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-272">Object</span></span>|<span data-ttu-id="b9278-273">Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="b9278-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="b9278-274">retryPolicy</span></span>|<span data-ttu-id="b9278-275">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-275">No</span></span>|<span data-ttu-id="b9278-276">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-276">Object</span></span>|<span data-ttu-id="b9278-277">Hiermee kunt u aanpassen van het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten.</span><span class="sxs-lookup"><span data-stu-id="b9278-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="b9278-278">Verificatie</span><span class="sxs-lookup"><span data-stu-id="b9278-278">authentication</span></span>|<span data-ttu-id="b9278-279">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-279">No</span></span>|<span data-ttu-id="b9278-280">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-280">Object</span></span>|<span data-ttu-id="b9278-281">Hiermee geeft u de methode die de aanvraag moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="b9278-282">Zie voor meer informatie over dit object [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="b9278-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="b9278-283">De eigenschappen voor de host zijn:</span><span class="sxs-lookup"><span data-stu-id="b9278-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="b9278-284">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-284">Element name</span></span>|<span data-ttu-id="b9278-285">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-285">Required</span></span>|<span data-ttu-id="b9278-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="b9278-287">API-runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="b9278-287">api runtimeUrl</span></span>|<span data-ttu-id="b9278-288">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-288">Yes</span></span>|<span data-ttu-id="b9278-289">Het eindpunt van de beheerde API.</span><span class="sxs-lookup"><span data-stu-id="b9278-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="b9278-290">Verbindingsnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-290">connection name</span></span>||<span data-ttu-id="b9278-291">Moet een verwijzing naar een parameter met de naam `$connection` en de naam van de beheerde API-verbinding die gebruikmaakt van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="b9278-292">De uitvoer van een trigger API-verbinding zijn:</span><span class="sxs-lookup"><span data-stu-id="b9278-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="b9278-293">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-293">Element name</span></span>|<span data-ttu-id="b9278-294">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-294">Type</span></span>|<span data-ttu-id="b9278-295">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="b9278-296">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-296">headers</span></span>|<span data-ttu-id="b9278-297">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-297">Object</span></span>|<span data-ttu-id="b9278-298">De headers van de http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="b9278-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="b9278-299">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-299">body</span></span>|<span data-ttu-id="b9278-300">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-300">Object</span></span>|<span data-ttu-id="b9278-301">De hoofdtekst van het http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="b9278-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="b9278-302">HTTPWebhook trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="b9278-303">De trigger HTTPWebhook opent een eindpunt, vergelijkbaar met de handmatige worden geactiveerd, maar de trigger HTTPWebhook roept ook uit op een opgegeven URL registreren en ongedaan maken.</span><span class="sxs-lookup"><span data-stu-id="b9278-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="b9278-304">Hier volgt een voorbeeld van wat een trigger HTTPWebhook als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="b9278-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="b9278-305">Veel van deze gedeelten zijn optioneel en het gedrag van de Webhook is afhankelijk van welke gedeelten wordt geleverd of wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="b9278-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="b9278-306">De eigenschappen van een Webhook zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="b9278-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="b9278-307">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-307">Element name</span></span>|<span data-ttu-id="b9278-308">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-308">Required</span></span>|<span data-ttu-id="b9278-309">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="b9278-310">abonneren</span><span class="sxs-lookup"><span data-stu-id="b9278-310">subscribe</span></span>|<span data-ttu-id="b9278-311">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-311">No</span></span>|<span data-ttu-id="b9278-312">De uitgaande aanvraag die wordt aangeroepen wanneer de trigger wordt gemaakt en de initiële registratie voert.</span><span class="sxs-lookup"><span data-stu-id="b9278-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="b9278-313">afmelden</span><span class="sxs-lookup"><span data-stu-id="b9278-313">unsubscribe</span></span>|<span data-ttu-id="b9278-314">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-314">No</span></span>|<span data-ttu-id="b9278-315">De uitgaande aanvraag wanneer de trigger wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b9278-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="b9278-316">**Abonneren** is de uitgaande aanroep die beginnen met luisteren op gebeurtenissen heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9278-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="b9278-317">Deze aanroep begint met dezelfde set parameters die de normale HTTP-acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="b9278-318">Deze uitgaande wordt aanroep een wanneer de werkstroom wordt gewijzigd op elke manier, bijvoorbeeld wanneer de referenties worden hersteld of de trigger invoerparameters wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b9278-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="b9278-319">Ter ondersteuning van deze aanroep is een nieuwe functie: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="b9278-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="b9278-320">Deze functie retourneert een unieke URL voor deze specifieke trigger in deze workflow.</span><span class="sxs-lookup"><span data-stu-id="b9278-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="b9278-321">Hiermee geeft u de unieke id voor de eindpunten die gebruikmaken van de REST van de Service.</span><span class="sxs-lookup"><span data-stu-id="b9278-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="b9278-322">**Afmelden** wordt aangeroepen wanneer een bewerking renders deze trigger ongeldig, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="b9278-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="b9278-323">Het verwijderen of uitschakelen van de trigger</span><span class="sxs-lookup"><span data-stu-id="b9278-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="b9278-324">Het verwijderen of uitschakelen van de werkstroom</span><span class="sxs-lookup"><span data-stu-id="b9278-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="b9278-325">Het verwijderen of uitschakelen van het abonnement</span><span class="sxs-lookup"><span data-stu-id="b9278-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="b9278-326">De logische app roept automatisch de actie afmelden.</span><span class="sxs-lookup"><span data-stu-id="b9278-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="b9278-327">De parameters voor deze functie zijn hetzelfde als de HTTP-trigger.</span><span class="sxs-lookup"><span data-stu-id="b9278-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="b9278-328">De uitvoer van de trigger HTTPWebhook zijn de inhoud van de binnenkomende aanvraag:</span><span class="sxs-lookup"><span data-stu-id="b9278-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="b9278-329">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-329">Element name</span></span>|<span data-ttu-id="b9278-330">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-330">Type</span></span>|<span data-ttu-id="b9278-331">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="b9278-332">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-332">headers</span></span>|<span data-ttu-id="b9278-333">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-333">Object</span></span>|<span data-ttu-id="b9278-334">De headers van de http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b9278-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="b9278-335">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-335">body</span></span>|<span data-ttu-id="b9278-336">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-336">Object</span></span>|<span data-ttu-id="b9278-337">De hoofdtekst van de http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b9278-337">The body of the http request.</span></span>|  

<span data-ttu-id="b9278-338">Limieten van een webhook-actie kunnen worden opgegeven op dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="b9278-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="b9278-339">Voorwaarden</span><span class="sxs-lookup"><span data-stu-id="b9278-339">Conditions</span></span>  

<span data-ttu-id="b9278-340">U kunt een of meer voorwaarden om te bepalen of de werkstroom moet worden uitgevoerd of niet gebruiken voor een trigger.</span><span class="sxs-lookup"><span data-stu-id="b9278-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="b9278-341">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="b9278-342">In dit geval wordt het rapport alleen triggers terwijl de werkstroom `sendReports` parameter is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="b9278-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="b9278-343">Ten slotte voorwaarden kunnen verwijzen naar de statuscode van de trigger.</span><span class="sxs-lookup"><span data-stu-id="b9278-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="b9278-344">U kan bijvoorbeeld ere van een werkstroom alleen als uw website een statuscode 500, als volgt retourneert:</span><span class="sxs-lookup"><span data-stu-id="b9278-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="b9278-345">Wanneer een expressie verwijst naar de statuscode van de trigger \(op elke manier\), het standaardgedrag \(trigger alleen op 200 \(OK\) \) wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="b9278-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="b9278-346">Bijvoorbeeld, als u activeren op zowel de statuscode 200 als de statuscode 201 wilt, hebt u omvatten: `@or(equals(triggers().code, 200),equals(triggers().code,201))` als de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="b9278-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="b9278-347">Meerdere wordt uitgevoerd voor een aanvraag starten</span><span class="sxs-lookup"><span data-stu-id="b9278-347">Start multiple runs for a request</span></span>

<span data-ttu-id="b9278-348">Activeer meerdere wordt uitgevoerd voor een enkele aanvraag `splitOn` is nuttig, bijvoorbeeld wanneer u wilt pollen een eindpunt dat meerdere nieuwe items tussen polling-intervallen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="b9278-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="b9278-349">Met `splitOn`, geeft u de eigenschap binnen de nettolading van antwoord met de matrix van items die u gebruiken wilt voor het starten van een uitvoering van de trigger.</span><span class="sxs-lookup"><span data-stu-id="b9278-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="b9278-350">Stel dat u hebt een API waarmee het volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b9278-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="b9278-351">Uw logische app moet alleen de inhoud van de rijen, zodat u de trigger zoals in dit voorbeeld kunt maken:</span><span class="sxs-lookup"><span data-stu-id="b9278-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="b9278-352">Klik in de werkstroomdefinitie `@triggerBody().name` retourneert `mycoolrow` voor het eerst wordt uitgevoerd, en `another row` voor de tweede uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="b9278-353">De trigger uitvoer eruit zien in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="b9278-354">Als u in dat geval `SplitOn`, u de eigenschappen die in dit geval buiten de matrix zijn geen krijgt de `Status` veld.</span><span class="sxs-lookup"><span data-stu-id="b9278-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="b9278-355">In dit voorbeeld gebruiken we de `?` operator om te voorkomen dat een fout als de `Rows` eigenschap is niet aanwezig.</span><span class="sxs-lookup"><span data-stu-id="b9278-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="b9278-356">SIS uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b9278-356">Single run instance</span></span>

<span data-ttu-id="b9278-357">Triggers die een terugkeerpatroon-eigenschap moet worden alleen gestart als alle actieve sessies hebt voltooid, kunt u configureren.</span><span class="sxs-lookup"><span data-stu-id="b9278-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="b9278-358">Als een geplande terugkeer optreedt terwijl er een uitgevoerd in voortgang is, wordt de trigger wordt overgeslagen en wacht tot het volgende geplande terugkeerpatroon opnieuw te controleren.</span><span class="sxs-lookup"><span data-stu-id="b9278-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="b9278-359">U kunt deze instelling door de bewerking-opties configureren:</span><span class="sxs-lookup"><span data-stu-id="b9278-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="b9278-360">Typen en invoer</span><span class="sxs-lookup"><span data-stu-id="b9278-360">Types and inputs</span></span>  

<span data-ttu-id="b9278-361">Er zijn veel verschillende soorten acties, elk met unieke gedrag.</span><span class="sxs-lookup"><span data-stu-id="b9278-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="b9278-362">Verzameling acties mogelijk veel andere acties in zichzelf bevatten.</span><span class="sxs-lookup"><span data-stu-id="b9278-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="b9278-363">Standaardacties</span><span class="sxs-lookup"><span data-stu-id="b9278-363">Standard actions</span></span>  

-   <span data-ttu-id="b9278-364">**HTTP** deze actie wordt een HTTP-web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="b9278-365">**ApiConnection** \- deze bewerking gedraagt zich als de HTTP-actie, maar gebruikt de door Microsoft beheerd-API's.</span><span class="sxs-lookup"><span data-stu-id="b9278-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="b9278-366">**ApiConnectionWebhook** \- zoals HTTPWebhook hierbij wordt gebruikgemaakt van de Microsoft-beheerde API's.</span><span class="sxs-lookup"><span data-stu-id="b9278-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="b9278-367">**Antwoord** \- deze actie wordt een antwoord voor een inkomend gesprek gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="b9278-368">**Wacht** \- deze eenvoudige actie wacht een vast bedrag tijd of totdat een bepaalde tijd.</span><span class="sxs-lookup"><span data-stu-id="b9278-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="b9278-369">**Werkstroom** \- deze actie vertegenwoordigt een geneste werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="b9278-370">**De functie** \- deze actie vertegenwoordigt een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="b9278-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="b9278-371">Verzameling acties</span><span class="sxs-lookup"><span data-stu-id="b9278-371">Collection actions</span></span>

-   <span data-ttu-id="b9278-372">**Bereik** \- deze actie is een logische groepering van andere acties.</span><span class="sxs-lookup"><span data-stu-id="b9278-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="b9278-373">**Voorwaarde** \- met deze actie evalueert een expressie en de bijbehorende resultaat vertakking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="b9278-374">**ForEach** \- samenvoegartikel hierdoor een matrix doorlopen en interne acties uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="b9278-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="b9278-375">**Pas** \- deze samenvoegartikel actie binnenste acties worden uitgevoerd totdat een voorwaarde in waar resulteert.</span><span class="sxs-lookup"><span data-stu-id="b9278-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="b9278-376">Elk type actie heeft een andere set **invoer** die een actie gedrag definiëren.</span><span class="sxs-lookup"><span data-stu-id="b9278-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="b9278-377">HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="b9278-377">HTTP action</span></span>  

<span data-ttu-id="b9278-378">Acties voor HTTP-aanroepen van een opgegeven eindpunt en controleren van het antwoord om te bepalen of de werkstroom moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="b9278-379">De **invoer** object neemt de set parameters die zijn vereist om de HTTP-aanroep samen te stellen:</span><span class="sxs-lookup"><span data-stu-id="b9278-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="b9278-380">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-380">Element name</span></span>|<span data-ttu-id="b9278-381">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-381">Required</span></span>|<span data-ttu-id="b9278-382">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-382">Type</span></span>|<span data-ttu-id="b9278-383">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="b9278-384">Methode</span><span class="sxs-lookup"><span data-stu-id="b9278-384">method</span></span>|<span data-ttu-id="b9278-385">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-385">Yes</span></span>|<span data-ttu-id="b9278-386">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-386">String</span></span>|<span data-ttu-id="b9278-387">Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="b9278-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="b9278-388">URI</span><span class="sxs-lookup"><span data-stu-id="b9278-388">uri</span></span>|<span data-ttu-id="b9278-389">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-389">Yes</span></span>|<span data-ttu-id="b9278-390">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-390">String</span></span>|<span data-ttu-id="b9278-391">Het http of https-eindpunt dat wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="b9278-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="b9278-392">Maximale lengte is 2 kB.</span><span class="sxs-lookup"><span data-stu-id="b9278-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="b9278-393">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-393">queries</span></span>|<span data-ttu-id="b9278-394">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-394">No</span></span>|<span data-ttu-id="b9278-395">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-395">Object</span></span>|<span data-ttu-id="b9278-396">Vertegenwoordigt de queryparameters toevoegen aan de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="b9278-397">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="b9278-398">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-398">headers</span></span>|<span data-ttu-id="b9278-399">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-399">No</span></span>|<span data-ttu-id="b9278-400">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-400">Object</span></span>|<span data-ttu-id="b9278-401">Hiermee geeft u elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-402">Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="b9278-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="b9278-403">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-403">body</span></span>|<span data-ttu-id="b9278-404">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-404">No</span></span>|<span data-ttu-id="b9278-405">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-405">Object</span></span>|<span data-ttu-id="b9278-406">Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="b9278-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="b9278-407">retryPolicy</span></span>|<span data-ttu-id="b9278-408">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-408">No</span></span>|<span data-ttu-id="b9278-409">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-409">Object</span></span>|<span data-ttu-id="b9278-410">Hiermee kunt u het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b9278-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="b9278-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="b9278-411">operationsOptions</span></span>|<span data-ttu-id="b9278-412">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-412">No</span></span>|<span data-ttu-id="b9278-413">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-413">String</span></span>|<span data-ttu-id="b9278-414">Definieert de set met speciaal gedrag negeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="b9278-415">Verificatie</span><span class="sxs-lookup"><span data-stu-id="b9278-415">authentication</span></span>|<span data-ttu-id="b9278-416">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-416">No</span></span>|<span data-ttu-id="b9278-417">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-417">Object</span></span>|<span data-ttu-id="b9278-418">Hiermee geeft u de methode die de aanvraag moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="b9278-419">Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="b9278-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="b9278-420">Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority`.</span><span class="sxs-lookup"><span data-stu-id="b9278-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="b9278-421">Dit is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="b9278-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="b9278-422">HTTP-acties \(en API-verbinding\) acties ondersteuning beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="b9278-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="b9278-423">Een beleid voor opnieuw proberen is van toepassing op onregelmatige problemen, gekenmerkt als HTTP-statuscodes 408 429 en 5xx, naast eventuele uitzonderingen connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b9278-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="b9278-424">Dit beleid wordt beschreven met behulp van de *retryPolicy* object dat is gedefinieerd als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="b9278-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="b9278-425">Het interval voor opnieuw proberen is opgegeven in de ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="b9278-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="b9278-426">Dit interval heeft een waarde standaard en een minimum van 20 seconden, terwijl de maximale waarde een uur is.</span><span class="sxs-lookup"><span data-stu-id="b9278-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="b9278-427">Het standaard- en maximum aantal is gelijk aan vier uur.</span><span class="sxs-lookup"><span data-stu-id="b9278-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="b9278-428">Als de beleidsdefinitie voor nieuwe pogingen niet is opgegeven, een `fixed` strategie met een standaardwaarde opnieuw telling en het interval wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9278-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="b9278-429">Als wilt uitschakelen in het beleid voor opnieuw proberen, stelt u het type in op `None`.</span><span class="sxs-lookup"><span data-stu-id="b9278-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="b9278-430">Bijvoorbeeld de volgende actie pogingen ophalen van het laatste nieuws twee keer als er onregelmatige problemen, voor een totaal van drie uitvoeringen, met een vertraging 30 seconden tussen elke poging:</span><span class="sxs-lookup"><span data-stu-id="b9278-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="b9278-431">Asynchrone patronen</span><span class="sxs-lookup"><span data-stu-id="b9278-431">Asynchronous patterns</span></span>

<span data-ttu-id="b9278-432">Standaard ondersteunt alle HTTP-gebaseerde acties het patroon standaard asynchrone bewerking.</span><span class="sxs-lookup"><span data-stu-id="b9278-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="b9278-433">Als de externe server geeft aan dat de aanvraag is geaccepteerd voor verwerking met een 202 \(geaccepteerde\) antwoord wordt de Logic Apps-engine houdt de URL die is opgegeven in de antwoordheader locatie tot het bereiken van een definitieve status polling\(niet\-202 antwoord\).</span><span class="sxs-lookup"><span data-stu-id="b9278-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="b9278-434">Instellen als wilt uitschakelen in het asynchrone gedrag die eerder is beschreven, een `DisableAsyncPattern` optie in de invoer in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="b9278-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="b9278-435">In dit geval wordt is de uitvoer van de actie gebaseerd op de eerste 202 reactie van de server.</span><span class="sxs-lookup"><span data-stu-id="b9278-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="b9278-436">Asynchrone limieten</span><span class="sxs-lookup"><span data-stu-id="b9278-436">Asynchronous Limits</span></span>

<span data-ttu-id="b9278-437">Een asynchrone patroon worden beperkt de duur van een bepaald tijdsinterval.</span><span class="sxs-lookup"><span data-stu-id="b9278-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="b9278-438">Als het tijdsinterval is verstreken zonder dat een definitieve status bereikt, wordt de status van de actie gemarkeerd `Cancelled` met de code `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="b9278-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="b9278-439">De time-out voor de limiet is opgegeven in de ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="b9278-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="b9278-440">Limieten kunnen worden opgegeven met de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="b9278-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="b9278-441">API-verbinding</span><span class="sxs-lookup"><span data-stu-id="b9278-441">API Connection</span></span>  

<span data-ttu-id="b9278-442">API-verbinding is een actie die verwijst naar een connector door Microsoft beheerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="b9278-443">Deze actie vereist een verwijzing naar een geldige verbinding en informatie over de API en de parameters die zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="b9278-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="b9278-444">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="b9278-444">Element name</span></span>|<span data-ttu-id="b9278-445">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-445">Required</span></span>|<span data-ttu-id="b9278-446">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-446">Type</span></span>|<span data-ttu-id="b9278-447">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="b9278-448">host</span><span class="sxs-lookup"><span data-stu-id="b9278-448">host</span></span>|<span data-ttu-id="b9278-449">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-449">Yes</span></span>|<span data-ttu-id="b9278-450">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-450">Object</span></span>|<span data-ttu-id="b9278-451">Hiermee geeft u de connector informatie zoals de runtimeUrl en de verwijzing naar het verbindingsobject</span><span class="sxs-lookup"><span data-stu-id="b9278-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="b9278-452">Methode</span><span class="sxs-lookup"><span data-stu-id="b9278-452">method</span></span>|<span data-ttu-id="b9278-453">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-453">Yes</span></span>|<span data-ttu-id="b9278-454">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-454">String</span></span>|<span data-ttu-id="b9278-455">Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="b9278-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="b9278-456">Pad</span><span class="sxs-lookup"><span data-stu-id="b9278-456">path</span></span>|<span data-ttu-id="b9278-457">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-457">Yes</span></span>|<span data-ttu-id="b9278-458">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-458">String</span></span>|<span data-ttu-id="b9278-459">Het pad van de API-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b9278-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="b9278-460">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-460">queries</span></span>|<span data-ttu-id="b9278-461">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-461">No</span></span>|<span data-ttu-id="b9278-462">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-462">Object</span></span>|<span data-ttu-id="b9278-463">Vertegenwoordigt de queryparameters toevoegen aan de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="b9278-464">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="b9278-465">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-465">headers</span></span>|<span data-ttu-id="b9278-466">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-466">No</span></span>|<span data-ttu-id="b9278-467">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-467">Object</span></span>|<span data-ttu-id="b9278-468">Hiermee geeft u elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-469">Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="b9278-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="b9278-470">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-470">body</span></span>|<span data-ttu-id="b9278-471">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-471">No</span></span>|<span data-ttu-id="b9278-472">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-472">Object</span></span>|<span data-ttu-id="b9278-473">Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="b9278-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="b9278-474">retryPolicy</span></span>|<span data-ttu-id="b9278-475">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-475">No</span></span>|<span data-ttu-id="b9278-476">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-476">Object</span></span>|<span data-ttu-id="b9278-477">Hiermee kunt u het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b9278-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="b9278-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="b9278-478">operationsOptions</span></span>|<span data-ttu-id="b9278-479">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-479">No</span></span>|<span data-ttu-id="b9278-480">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-480">String</span></span>|<span data-ttu-id="b9278-481">Definieert de set met speciaal gedrag negeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="b9278-482">API-verbinding webhook actie</span><span class="sxs-lookup"><span data-stu-id="b9278-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="b9278-483">Limieten van een webhook-actie kunnen worden opgegeven op dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="b9278-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="b9278-484">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="b9278-484">Response action</span></span>  

<span data-ttu-id="b9278-485">Dit actietype de nettolading van het volledige antwoord van een HTTP-aanvraag bevat en een statusCode, hoofdtekst en headers omvat:</span><span class="sxs-lookup"><span data-stu-id="b9278-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="b9278-486">De actie antwoord heeft speciale beperkingen die niet van toepassing op andere acties.</span><span class="sxs-lookup"><span data-stu-id="b9278-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="b9278-487">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="b9278-487">Specifically:</span></span>  
  
-   <span data-ttu-id="b9278-488">Reacties kunnen niet in een definitie van een parallelle omdat een deterministische antwoord aan de binnenkomende aanvraag vereist is.</span><span class="sxs-lookup"><span data-stu-id="b9278-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="b9278-489">Als een antwoord-actie is bereikt, nadat de binnenkomende aanvraag heeft een antwoord ontvangen, de actie wordt beschouwd als mislukt \(conflict\), en als gevolg hiervan, het uitvoeren is `Failed`.</span><span class="sxs-lookup"><span data-stu-id="b9278-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="b9278-490">Een werkstroom met reacties kan geen `splitOn` in de trigger omdat één aanroep ervoor zorgt veel wordt uitgevoerd dat.</span><span class="sxs-lookup"><span data-stu-id="b9278-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="b9278-491">Dit moet als gevolg hiervan worden gevalideerd wanneer de stroom PUT en oorzaak is een ongeldige aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="b9278-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="b9278-492">Actie wachten</span><span class="sxs-lookup"><span data-stu-id="b9278-492">Wait action</span></span>  

<span data-ttu-id="b9278-493">De `wait` actie onderbreekt de uitvoering van de werkstroom voor het opgegeven interval.</span><span class="sxs-lookup"><span data-stu-id="b9278-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="b9278-494">Bijvoorbeeld, om de 15 minuten wachten, kunt u in dit fragment:</span><span class="sxs-lookup"><span data-stu-id="b9278-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="b9278-495">Als u wilt wachten tot een bepaald moment, kunt u ook in dit voorbeeld gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b9278-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="b9278-496">De duur van de wachttijd ofwel kan worden opgegeven met de **interval** object of de **totdat** , maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="b9278-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="b9278-497">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-497">Name</span></span>|<span data-ttu-id="b9278-498">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-498">Required</span></span>|<span data-ttu-id="b9278-499">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-499">Type</span></span>|<span data-ttu-id="b9278-500">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-501">Interval</span><span class="sxs-lookup"><span data-stu-id="b9278-501">interval</span></span>|<span data-ttu-id="b9278-502">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-502">No</span></span>|<span data-ttu-id="b9278-503">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-503">Object</span></span>|<span data-ttu-id="b9278-504">De duur van de wachttijd op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="b9278-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="b9278-505">intervaleenheid</span><span class="sxs-lookup"><span data-stu-id="b9278-505">interval unit</span></span>|<span data-ttu-id="b9278-506">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-506">Yes</span></span>|<span data-ttu-id="b9278-507">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-507">String</span></span>|<span data-ttu-id="b9278-508">Een van deze intervallen: seconde, minuut, uur, dag, week, maand, jaar.</span><span class="sxs-lookup"><span data-stu-id="b9278-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="b9278-509">interval aantal</span><span class="sxs-lookup"><span data-stu-id="b9278-509">interval count</span></span>|<span data-ttu-id="b9278-510">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-510">Yes</span></span>|<span data-ttu-id="b9278-511">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-511">String</span></span>|<span data-ttu-id="b9278-512">De duur op basis van de opgegeven interne eenheid.</span><span class="sxs-lookup"><span data-stu-id="b9278-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="b9278-513">pas</span><span class="sxs-lookup"><span data-stu-id="b9278-513">until</span></span>|<span data-ttu-id="b9278-514">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-514">No</span></span>|<span data-ttu-id="b9278-515">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-515">Object</span></span>|<span data-ttu-id="b9278-516">De duur van de wachttijd op basis van een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="b9278-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="b9278-517">Pas de timestamp</span><span class="sxs-lookup"><span data-stu-id="b9278-517">until timestamp</span></span>|<span data-ttu-id="b9278-518">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-518">Yes</span></span>|<span data-ttu-id="b9278-519">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-519">String</span></span>|<span data-ttu-id="b9278-520">Tekenreeks &#124; Het punt in tijd in UTC wanneer de wachttijd is verlopen.</span><span class="sxs-lookup"><span data-stu-id="b9278-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="b9278-521">Queryactie</span><span class="sxs-lookup"><span data-stu-id="b9278-521">Query action</span></span>

<span data-ttu-id="b9278-522">De `query` actie kunt u filteren op basis van een voorwaarde matrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="b9278-523">Bijvoorbeeld, om te selecteren getallen die groter zijn dan 2, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b9278-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="b9278-524">De uitvoer van de `query` actie is een matrix met elementen van de invoermatrix die voldoen aan de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="b9278-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="b9278-525">Als geen waarden voldoen aan de `where` voorwaarde, het resultaat is een lege matrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="b9278-526">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-526">Name</span></span>|<span data-ttu-id="b9278-527">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-527">Required</span></span>|<span data-ttu-id="b9278-528">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-528">Type</span></span>|<span data-ttu-id="b9278-529">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="b9278-530">Van</span><span class="sxs-lookup"><span data-stu-id="b9278-530">from</span></span>|<span data-ttu-id="b9278-531">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-531">Yes</span></span>|<span data-ttu-id="b9278-532">matrix</span><span class="sxs-lookup"><span data-stu-id="b9278-532">Array</span></span>|<span data-ttu-id="b9278-533">De bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-533">The source array.</span></span>|
|<span data-ttu-id="b9278-534">waar</span><span class="sxs-lookup"><span data-stu-id="b9278-534">where</span></span>|<span data-ttu-id="b9278-535">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-535">Yes</span></span>|<span data-ttu-id="b9278-536">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-536">String</span></span>|<span data-ttu-id="b9278-537">De voorwaarde van toepassing op elk element van de bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="b9278-538">Selecteer actie</span><span class="sxs-lookup"><span data-stu-id="b9278-538">Select action</span></span>

<span data-ttu-id="b9278-539">De `select` actie kunt u elk element van een matrix project in een nieuwe waarde.</span><span class="sxs-lookup"><span data-stu-id="b9278-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="b9278-540">Bijvoorbeeld, als u wilt converteren van een matrix van getallen in een matrix met objecten, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b9278-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="b9278-541">De uitvoer van de `select` actie is een matrix met de dezelfde kardinaliteit als de invoermatrix met elk element getransformeerd zoals gedefinieerd door de `select` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b9278-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="b9278-542">Als de invoer een lege matrix is, wordt de uitvoer is ook een lege matrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="b9278-543">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-543">Name</span></span>|<span data-ttu-id="b9278-544">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-544">Required</span></span>|<span data-ttu-id="b9278-545">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-545">Type</span></span>|<span data-ttu-id="b9278-546">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="b9278-547">Van</span><span class="sxs-lookup"><span data-stu-id="b9278-547">from</span></span>|<span data-ttu-id="b9278-548">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-548">Yes</span></span>|<span data-ttu-id="b9278-549">matrix</span><span class="sxs-lookup"><span data-stu-id="b9278-549">Array</span></span>|<span data-ttu-id="b9278-550">De bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-550">The source array.</span></span>|
|<span data-ttu-id="b9278-551">Selecteer</span><span class="sxs-lookup"><span data-stu-id="b9278-551">select</span></span>|<span data-ttu-id="b9278-552">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-552">Yes</span></span>|<span data-ttu-id="b9278-553">Alle</span><span class="sxs-lookup"><span data-stu-id="b9278-553">Any</span></span>|<span data-ttu-id="b9278-554">De projectie toepassen op elk element van de bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="b9278-555">Actie beëindigen</span><span class="sxs-lookup"><span data-stu-id="b9278-555">Terminate action</span></span>

<span data-ttu-id="b9278-556">De actie beëindigen stopt u de uitvoering van de werkstroom uitvoeren, wordt afgebroken onderweg acties en eventuele resterende acties wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b9278-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="b9278-557">Bijvoorbeeld, een reeks met de status afgebroken **mislukt**, kunt u het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="b9278-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="b9278-558">Reeds voltooide acties worden niet beïnvloed door de actie beëindigen.</span><span class="sxs-lookup"><span data-stu-id="b9278-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="b9278-559">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-559">Name</span></span>|<span data-ttu-id="b9278-560">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-560">Required</span></span>|<span data-ttu-id="b9278-561">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-561">Type</span></span>|<span data-ttu-id="b9278-562">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="b9278-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="b9278-563">runStatus</span></span>|<span data-ttu-id="b9278-564">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-564">Yes</span></span>|<span data-ttu-id="b9278-565">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-565">String</span></span>|<span data-ttu-id="b9278-566">Het doel status uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-566">The target run status.</span></span> <span data-ttu-id="b9278-567">Beide **mislukt** of **geannuleerd**.</span><span class="sxs-lookup"><span data-stu-id="b9278-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="b9278-568">runError</span><span class="sxs-lookup"><span data-stu-id="b9278-568">runError</span></span>|<span data-ttu-id="b9278-569">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-569">No</span></span>|<span data-ttu-id="b9278-570">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-570">Object</span></span>|<span data-ttu-id="b9278-571">De details van de fout.</span><span class="sxs-lookup"><span data-stu-id="b9278-571">The error details.</span></span> <span data-ttu-id="b9278-572">Alleen ondersteund wanneer **runStatus** is ingesteld op **mislukt**.</span><span class="sxs-lookup"><span data-stu-id="b9278-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="b9278-573">runError code</span><span class="sxs-lookup"><span data-stu-id="b9278-573">runError code</span></span>|<span data-ttu-id="b9278-574">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-574">No</span></span>|<span data-ttu-id="b9278-575">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-575">String</span></span>|<span data-ttu-id="b9278-576">De uitvoering van de foutcode.</span><span class="sxs-lookup"><span data-stu-id="b9278-576">The run error code.</span></span>|
|<span data-ttu-id="b9278-577">runError bericht</span><span class="sxs-lookup"><span data-stu-id="b9278-577">runError message</span></span>|<span data-ttu-id="b9278-578">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-578">No</span></span>|<span data-ttu-id="b9278-579">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-579">String</span></span>|<span data-ttu-id="b9278-580">Het foutbericht voor uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9278-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="b9278-581">Actie opstellen</span><span class="sxs-lookup"><span data-stu-id="b9278-581">Compose action</span></span>

<span data-ttu-id="b9278-582">De actie opstellen kunt u een willekeurig object samenstellen.</span><span class="sxs-lookup"><span data-stu-id="b9278-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="b9278-583">De uitvoer van de actie compose is het resultaat van evaluatie van de invoer.</span><span class="sxs-lookup"><span data-stu-id="b9278-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="b9278-584">Bijvoorbeeld, kunt u de actie opstellen om samen te voegen uitvoerwaarden van meerdere acties:</span><span class="sxs-lookup"><span data-stu-id="b9278-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="b9278-585">De **opstellen** actie kan worden gebruikt om eventuele uitvoer, met inbegrip van objecten, matrices en een ander type systeemeigen worden ondersteund door logische apps zoals XML en binaire samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="b9278-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="b9278-586">Tabel actie</span><span class="sxs-lookup"><span data-stu-id="b9278-586">Table action</span></span>

<span data-ttu-id="b9278-587">De `table` kunt u converteren van een matrix van items in een **CSV** of **HTML** tabel.</span><span class="sxs-lookup"><span data-stu-id="b9278-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="b9278-588">Stel @triggerBody() is</span><span class="sxs-lookup"><span data-stu-id="b9278-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="b9278-589">En kunt u de actie die worden gedefinieerd als</span><span class="sxs-lookup"><span data-stu-id="b9278-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="b9278-590">De bovenstaande geeft als resultaat</span><span class="sxs-lookup"><span data-stu-id="b9278-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="b9278-591">id</span><span class="sxs-lookup"><span data-stu-id="b9278-591">id</span></span></th><th><span data-ttu-id="b9278-592">naam</span><span class="sxs-lookup"><span data-stu-id="b9278-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="b9278-593">0</span><span class="sxs-lookup"><span data-stu-id="b9278-593">0</span></span></td><td><span data-ttu-id="b9278-594">appels</span><span class="sxs-lookup"><span data-stu-id="b9278-594">apples</span></span></td></tr><tr><td><span data-ttu-id="b9278-595">1</span><span class="sxs-lookup"><span data-stu-id="b9278-595">1</span></span></td><td><span data-ttu-id="b9278-596">appels</span><span class="sxs-lookup"><span data-stu-id="b9278-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="b9278-597">"</span><span class="sxs-lookup"><span data-stu-id="b9278-597">"</span></span>

<span data-ttu-id="b9278-598">Als u wilt aanpassen in de tabel, kunt u de kolommen expliciet opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9278-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="b9278-599">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b9278-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="b9278-600">De bovenstaande geeft als resultaat</span><span class="sxs-lookup"><span data-stu-id="b9278-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="b9278-601">id maken</span><span class="sxs-lookup"><span data-stu-id="b9278-601">produce id</span></span></th><th><span data-ttu-id="b9278-602">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="b9278-603">0</span><span class="sxs-lookup"><span data-stu-id="b9278-603">0</span></span></td><td><span data-ttu-id="b9278-604">nieuwe appels</span><span class="sxs-lookup"><span data-stu-id="b9278-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="b9278-605">1</span><span class="sxs-lookup"><span data-stu-id="b9278-605">1</span></span></td><td><span data-ttu-id="b9278-606">nieuwe appels</span><span class="sxs-lookup"><span data-stu-id="b9278-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="b9278-607">"</span><span class="sxs-lookup"><span data-stu-id="b9278-607">"</span></span>

<span data-ttu-id="b9278-608">Als de `from` waarde van de eigenschap is een lege matrix, de uitvoer is een lege tabel.</span><span class="sxs-lookup"><span data-stu-id="b9278-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="b9278-609">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-609">Name</span></span>|<span data-ttu-id="b9278-610">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-610">Required</span></span>|<span data-ttu-id="b9278-611">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-611">Type</span></span>|<span data-ttu-id="b9278-612">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="b9278-613">Van</span><span class="sxs-lookup"><span data-stu-id="b9278-613">from</span></span>|<span data-ttu-id="b9278-614">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-614">Yes</span></span>|<span data-ttu-id="b9278-615">matrix</span><span class="sxs-lookup"><span data-stu-id="b9278-615">Array</span></span>|<span data-ttu-id="b9278-616">De bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="b9278-616">The source array.</span></span>|
|<span data-ttu-id="b9278-617">Indeling</span><span class="sxs-lookup"><span data-stu-id="b9278-617">format</span></span>|<span data-ttu-id="b9278-618">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-618">Yes</span></span>|<span data-ttu-id="b9278-619">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-619">String</span></span>|<span data-ttu-id="b9278-620">De indeling beide **CSV** of **HTML**.</span><span class="sxs-lookup"><span data-stu-id="b9278-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="b9278-621">Kolommen</span><span class="sxs-lookup"><span data-stu-id="b9278-621">columns</span></span>|<span data-ttu-id="b9278-622">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-622">No</span></span>|<span data-ttu-id="b9278-623">matrix</span><span class="sxs-lookup"><span data-stu-id="b9278-623">Array</span></span>|<span data-ttu-id="b9278-624">De kolommen.</span><span class="sxs-lookup"><span data-stu-id="b9278-624">The columns.</span></span> <span data-ttu-id="b9278-625">Kan de standaardvorm van de tabel overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b9278-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="b9278-626">kolomkop</span><span class="sxs-lookup"><span data-stu-id="b9278-626">column header</span></span>|<span data-ttu-id="b9278-627">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-627">No</span></span>|<span data-ttu-id="b9278-628">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-628">String</span></span>|<span data-ttu-id="b9278-629">De koptekst van de kolom.</span><span class="sxs-lookup"><span data-stu-id="b9278-629">The header of the column.</span></span>|
|<span data-ttu-id="b9278-630">waarde in de kolom</span><span class="sxs-lookup"><span data-stu-id="b9278-630">column value</span></span>|<span data-ttu-id="b9278-631">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-631">Yes</span></span>|<span data-ttu-id="b9278-632">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-632">String</span></span>|<span data-ttu-id="b9278-633">De waarde van de kolom.</span><span class="sxs-lookup"><span data-stu-id="b9278-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="b9278-634">Werkstroomactie</span><span class="sxs-lookup"><span data-stu-id="b9278-634">Workflow action</span></span>   

|<span data-ttu-id="b9278-635">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-635">Name</span></span>|<span data-ttu-id="b9278-636">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-636">Required</span></span>|<span data-ttu-id="b9278-637">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-637">Type</span></span>|<span data-ttu-id="b9278-638">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-639">host-id</span><span class="sxs-lookup"><span data-stu-id="b9278-639">host id</span></span>|<span data-ttu-id="b9278-640">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-640">Yes</span></span>|<span data-ttu-id="b9278-641">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-641">String</span></span>|<span data-ttu-id="b9278-642">De resource-ID van de werkstroom die u wilt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9278-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="b9278-643">host triggernaam</span><span class="sxs-lookup"><span data-stu-id="b9278-643">host triggerName</span></span>|<span data-ttu-id="b9278-644">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-644">Yes</span></span>|<span data-ttu-id="b9278-645">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-645">String</span></span>|<span data-ttu-id="b9278-646">De naam van de trigger die u wilt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9278-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="b9278-647">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-647">queries</span></span>|<span data-ttu-id="b9278-648">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-648">No</span></span>|<span data-ttu-id="b9278-649">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-649">Object</span></span>|<span data-ttu-id="b9278-650">Vertegenwoordigt de queryparameters toevoegen aan de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="b9278-651">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="b9278-652">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-652">headers</span></span>|<span data-ttu-id="b9278-653">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-653">No</span></span>|<span data-ttu-id="b9278-654">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-654">Object</span></span>|<span data-ttu-id="b9278-655">Hiermee geeft u elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-656">Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="b9278-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="b9278-657">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-657">body</span></span>|<span data-ttu-id="b9278-658">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-658">No</span></span>|<span data-ttu-id="b9278-659">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-659">Object</span></span>|<span data-ttu-id="b9278-660">Hiermee geeft u de nettolading van de verzonden naar het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="b9278-661">Een toegangscontrole wordt gemaakt op de werkstroom \(meer specifiek, de trigger\), wat betekent dat u moet toegang hebben tot de workflow.</span><span class="sxs-lookup"><span data-stu-id="b9278-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="b9278-662">De uitvoer van de `workflow` actie zijn gebaseerd op wat u hebt gedefinieerd in de `response` bewerking in de onderliggende werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="b9278-663">Als u nog geen gedefinieerd een `response` actie wordt de uitvoer is leeg.</span><span class="sxs-lookup"><span data-stu-id="b9278-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="b9278-664">Functie actie</span><span class="sxs-lookup"><span data-stu-id="b9278-664">Function action</span></span>   

|<span data-ttu-id="b9278-665">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-665">Name</span></span>|<span data-ttu-id="b9278-666">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-666">Required</span></span>|<span data-ttu-id="b9278-667">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-667">Type</span></span>|<span data-ttu-id="b9278-668">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-669">functie-id</span><span class="sxs-lookup"><span data-stu-id="b9278-669">function id</span></span>|<span data-ttu-id="b9278-670">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-670">Yes</span></span>|<span data-ttu-id="b9278-671">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-671">String</span></span>|<span data-ttu-id="b9278-672">De resource-ID van de functie die u wilt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9278-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="b9278-673">Methode</span><span class="sxs-lookup"><span data-stu-id="b9278-673">method</span></span>|<span data-ttu-id="b9278-674">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-674">No</span></span>|<span data-ttu-id="b9278-675">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-675">String</span></span>|<span data-ttu-id="b9278-676">De HTTP-methode die wordt gebruikt voor het aanroepen van de functie.</span><span class="sxs-lookup"><span data-stu-id="b9278-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="b9278-677">Dit is standaard `POST` als niet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b9278-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="b9278-678">Query 's</span><span class="sxs-lookup"><span data-stu-id="b9278-678">queries</span></span>|<span data-ttu-id="b9278-679">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-679">No</span></span>|<span data-ttu-id="b9278-680">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-680">Object</span></span>|<span data-ttu-id="b9278-681">Vertegenwoordigt de queryparameters toevoegen aan de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="b9278-682">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.</span><span class="sxs-lookup"><span data-stu-id="b9278-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="b9278-683">Headers</span><span class="sxs-lookup"><span data-stu-id="b9278-683">headers</span></span>|<span data-ttu-id="b9278-684">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-684">No</span></span>|<span data-ttu-id="b9278-685">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-685">Object</span></span>|<span data-ttu-id="b9278-686">Hiermee geeft u elk van de headers die aan de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b9278-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="b9278-687">Bijvoorbeeld, om de taal en type ingesteld op een aanvraag: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="b9278-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="b9278-688">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b9278-688">body</span></span>|<span data-ttu-id="b9278-689">Nee</span><span class="sxs-lookup"><span data-stu-id="b9278-689">No</span></span>|<span data-ttu-id="b9278-690">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-690">Object</span></span>|<span data-ttu-id="b9278-691">Hiermee geeft u de nettolading van de verzonden naar het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9278-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="b9278-692">Wanneer u de logische app opslaat, voeren we enkele controles op de functie waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="b9278-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="b9278-693">U moet toegang hebben tot de functie.</span><span class="sxs-lookup"><span data-stu-id="b9278-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="b9278-694">Alleen de standaard HTTP-trigger of algemene JSON webhook trigger is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="b9278-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="b9278-695">Er mogen geen enkele route gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="b9278-696">Alleen 'functioneren' en 'anonymous' autorisatieniveau is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="b9278-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="b9278-697">De URL van de trigger is opgehaald, in de cache opgeslagen en gebruikt tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="b9278-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="b9278-698">Dus als een bewerking wordt ongeldig gemaakt van de URL in de cache, mislukt de actie tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="b9278-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="b9278-699">Om dit te voorkomen, slaat u de logische app opnieuw, waardoor de logische app op te halen en de trigger-URL opnieuw in de cache.</span><span class="sxs-lookup"><span data-stu-id="b9278-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="b9278-700">Verzameling acties (bereiken en lussen)</span><span class="sxs-lookup"><span data-stu-id="b9278-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="b9278-701">Sommige actietypen kunnen acties in zichzelf bevatten.</span><span class="sxs-lookup"><span data-stu-id="b9278-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="b9278-702">Verwijzing acties binnen een verzameling kunnen worden verwezen rechtstreeks buiten de verzameling.</span><span class="sxs-lookup"><span data-stu-id="b9278-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="b9278-703">Als u hebt gedefinieerd `http` in een bereik `@body('http')` nog geldig overal in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="b9278-704">Acties binnen een verzameling kunnen `runAfter` alleen andere acties in dezelfde verzameling.</span><span class="sxs-lookup"><span data-stu-id="b9278-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="b9278-705">Bereikactie</span><span class="sxs-lookup"><span data-stu-id="b9278-705">Scope action</span></span>

<span data-ttu-id="b9278-706">De `scope` actie kunt u logische groep acties in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="b9278-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="b9278-707">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-707">Name</span></span>|<span data-ttu-id="b9278-708">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-708">Required</span></span>|<span data-ttu-id="b9278-709">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-709">Type</span></span>|<span data-ttu-id="b9278-710">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-711">acties</span><span class="sxs-lookup"><span data-stu-id="b9278-711">actions</span></span>|<span data-ttu-id="b9278-712">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-712">Yes</span></span>|<span data-ttu-id="b9278-713">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-713">Object</span></span>|<span data-ttu-id="b9278-714">Interne acties worden uitgevoerd binnen het bereik</span><span class="sxs-lookup"><span data-stu-id="b9278-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="b9278-715">ForEach-actie</span><span class="sxs-lookup"><span data-stu-id="b9278-715">ForEach action</span></span>

<span data-ttu-id="b9278-716">Deze actie samenvoegartikel een matrix doorlopen en interne acties uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="b9278-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="b9278-717">Standaard voert de lus foreach parallel (20 uitvoeringen parallel tegelijk).</span><span class="sxs-lookup"><span data-stu-id="b9278-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="b9278-718">U kunt instellen dat uitvoering regels die gebruikmaken van de `operationOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="b9278-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="b9278-719">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-719">Name</span></span>|<span data-ttu-id="b9278-720">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-720">Required</span></span>|<span data-ttu-id="b9278-721">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-721">Type</span></span>|<span data-ttu-id="b9278-722">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-723">acties</span><span class="sxs-lookup"><span data-stu-id="b9278-723">actions</span></span>|<span data-ttu-id="b9278-724">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-724">Yes</span></span>|<span data-ttu-id="b9278-725">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-725">Object</span></span>|<span data-ttu-id="b9278-726">Interne acties worden uitgevoerd binnen de lus</span><span class="sxs-lookup"><span data-stu-id="b9278-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="b9278-727">foreach</span><span class="sxs-lookup"><span data-stu-id="b9278-727">foreach</span></span>|<span data-ttu-id="b9278-728">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-728">Yes</span></span>|<span data-ttu-id="b9278-729">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-729">string</span></span>|<span data-ttu-id="b9278-730">De matrix te herhalen</span><span class="sxs-lookup"><span data-stu-id="b9278-730">The array to iterate over</span></span>|
|<span data-ttu-id="b9278-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="b9278-731">operationOptions</span></span>|<span data-ttu-id="b9278-732">Er is geen</span><span class="sxs-lookup"><span data-stu-id="b9278-732">no</span></span>|<span data-ttu-id="b9278-733">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-733">string</span></span>|<span data-ttu-id="b9278-734">Bewerking opties voor het gedrag.</span><span class="sxs-lookup"><span data-stu-id="b9278-734">Any operation options for behavior.</span></span> <span data-ttu-id="b9278-735">Ondersteunt momenteel alleen `sequential` iteraties sequentieel uitvoeren (standaardgedrag is parallelle)</span><span class="sxs-lookup"><span data-stu-id="b9278-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="b9278-736">Totdat de actie</span><span class="sxs-lookup"><span data-stu-id="b9278-736">Until action</span></span>

<span data-ttu-id="b9278-737">Deze samenvoegartikel actie uitgevoerd binnenste acties totdat een voorwaarde in waar resulteert.</span><span class="sxs-lookup"><span data-stu-id="b9278-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="b9278-738">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-738">Name</span></span>|<span data-ttu-id="b9278-739">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-739">Required</span></span>|<span data-ttu-id="b9278-740">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-740">Type</span></span>|<span data-ttu-id="b9278-741">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-742">acties</span><span class="sxs-lookup"><span data-stu-id="b9278-742">actions</span></span>|<span data-ttu-id="b9278-743">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-743">Yes</span></span>|<span data-ttu-id="b9278-744">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-744">Object</span></span>|<span data-ttu-id="b9278-745">Interne acties worden uitgevoerd binnen de lus</span><span class="sxs-lookup"><span data-stu-id="b9278-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="b9278-746">expressie</span><span class="sxs-lookup"><span data-stu-id="b9278-746">expression</span></span>|<span data-ttu-id="b9278-747">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-747">Yes</span></span>|<span data-ttu-id="b9278-748">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-748">string</span></span>|<span data-ttu-id="b9278-749">De expressie na elke iteratie evalueren</span><span class="sxs-lookup"><span data-stu-id="b9278-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="b9278-750">Limiet</span><span class="sxs-lookup"><span data-stu-id="b9278-750">limit</span></span>|<span data-ttu-id="b9278-751">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-751">yes</span></span>|<span data-ttu-id="b9278-752">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-752">Object</span></span>|<span data-ttu-id="b9278-753">De limieten voor de lus - ten minste één limiet moeten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="b9278-754">Aantal</span><span class="sxs-lookup"><span data-stu-id="b9278-754">count</span></span>|<span data-ttu-id="b9278-755">Er is geen</span><span class="sxs-lookup"><span data-stu-id="b9278-755">no</span></span>|<span data-ttu-id="b9278-756">int</span><span class="sxs-lookup"><span data-stu-id="b9278-756">int</span></span>|<span data-ttu-id="b9278-757">De limiet voor het aantal iteraties die kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="b9278-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="b9278-758">Time-out</span><span class="sxs-lookup"><span data-stu-id="b9278-758">timeout</span></span>|<span data-ttu-id="b9278-759">Er is geen</span><span class="sxs-lookup"><span data-stu-id="b9278-759">no</span></span>|<span data-ttu-id="b9278-760">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-760">string</span></span>|<span data-ttu-id="b9278-761">De time-out voor hoe lang deze moet worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="b9278-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="b9278-762">ISO 8601-notatie</span><span class="sxs-lookup"><span data-stu-id="b9278-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="b9278-763">Voorwaarden - als actie</span><span class="sxs-lookup"><span data-stu-id="b9278-763">Conditions - If Action</span></span>

<span data-ttu-id="b9278-764">De `If` actie kunt u een voorwaarde evalueren en uitvoeren van een vertakking op basis van of de expressie resulteert in `true`.</span><span class="sxs-lookup"><span data-stu-id="b9278-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="b9278-765">Naam</span><span class="sxs-lookup"><span data-stu-id="b9278-765">Name</span></span>|<span data-ttu-id="b9278-766">Vereist</span><span class="sxs-lookup"><span data-stu-id="b9278-766">Required</span></span>|<span data-ttu-id="b9278-767">Type</span><span class="sxs-lookup"><span data-stu-id="b9278-767">Type</span></span>|<span data-ttu-id="b9278-768">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b9278-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="b9278-769">acties</span><span class="sxs-lookup"><span data-stu-id="b9278-769">actions</span></span>|<span data-ttu-id="b9278-770">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-770">Yes</span></span>|<span data-ttu-id="b9278-771">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-771">Object</span></span>|<span data-ttu-id="b9278-772">Interne acties uit te voeren wanneer expressie resulteert in`true`</span><span class="sxs-lookup"><span data-stu-id="b9278-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="b9278-773">expressie</span><span class="sxs-lookup"><span data-stu-id="b9278-773">expression</span></span>|<span data-ttu-id="b9278-774">Ja</span><span class="sxs-lookup"><span data-stu-id="b9278-774">Yes</span></span>|<span data-ttu-id="b9278-775">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b9278-775">string</span></span>|<span data-ttu-id="b9278-776">De expressie om te evalueren</span><span class="sxs-lookup"><span data-stu-id="b9278-776">The expression to evaluate</span></span>|
|<span data-ttu-id="b9278-777">anders</span><span class="sxs-lookup"><span data-stu-id="b9278-777">else</span></span>|<span data-ttu-id="b9278-778">Er is geen</span><span class="sxs-lookup"><span data-stu-id="b9278-778">no</span></span>|<span data-ttu-id="b9278-779">Object</span><span class="sxs-lookup"><span data-stu-id="b9278-779">Object</span></span>|<span data-ttu-id="b9278-780">Interne acties uit te voeren wanneer expressie resulteert in`false`</span><span class="sxs-lookup"><span data-stu-id="b9278-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="b9278-781">De volgende tabel ziet u voorbeelden van hoe voorwaarden expressies in een actie kunnen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b9278-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="b9278-782">JSON-waarde</span><span class="sxs-lookup"><span data-stu-id="b9278-782">JSON value</span></span>|<span data-ttu-id="b9278-783">Resultaat</span><span class="sxs-lookup"><span data-stu-id="b9278-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="b9278-784">De waarde die als waar evalueren verbindingspogingen, wordt dit probleem op te geven.</span><span class="sxs-lookup"><span data-stu-id="b9278-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="b9278-785">Alleen Booleaanse expressies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b9278-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="b9278-786">Functies gebruiken om andere typen converteren naar Booleaanse waarde, `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="b9278-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="b9278-787">Vergelijking van functies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b9278-787">Comparison functions are supported.</span></span> <span data-ttu-id="b9278-788">In het voorbeeld hier de actie alleen wordt uitgevoerd wanneer de uitvoer van act1 groter dan de drempelwaarde is.</span><span class="sxs-lookup"><span data-stu-id="b9278-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="b9278-789">Bedrijfslogica-functies worden ook ondersteund voor het maken van geneste Booleaanse expressies.</span><span class="sxs-lookup"><span data-stu-id="b9278-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="b9278-790">In dit geval wordt de actie uitgevoerd wanneer de uitvoer van act1 boven de drempelwaarde of onder de 100.</span><span class="sxs-lookup"><span data-stu-id="b9278-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="b9278-791">Matrixfuncties kunt u controleren of een matrix alle items heeft.</span><span class="sxs-lookup"><span data-stu-id="b9278-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="b9278-792">In dit geval wordt de actie uitgevoerd wanneer de fouten matrix leeg is.</span><span class="sxs-lookup"><span data-stu-id="b9278-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="b9278-793">Fout: geen geldige voorwaarde omdat @ is vereist voor voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="b9278-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="b9278-794">Als een voorwaarde is geëvalueerd, de voorwaarde is gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="b9278-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="b9278-795">Acties in ofwel de `actions` of `else` objecten worden geëvalueerd tot `Succeeded` wanneer die wordt uitgevoerd en is voltooid, `Failed` wanneer die wordt uitgevoerd en is mislukt, of `Skipped` wanneer dat filiaal niet is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9278-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9278-796">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9278-796">Next steps</span></span>

[<span data-ttu-id="b9278-797">REST-API van workflow</span><span class="sxs-lookup"><span data-stu-id="b9278-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
