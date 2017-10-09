---
title: aaaWorkflow acties en de triggers - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="daa50-102">Werkstroomacties en triggers voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="daa50-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="daa50-103">Logische apps bestaan uit het triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="daa50-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="daa50-104">Er zijn zes soorten triggers.</span><span class="sxs-lookup"><span data-stu-id="daa50-104">There are six types of triggers.</span></span> <span data-ttu-id="daa50-105">Elk type heeft een andere interface en ander gedrag.</span><span class="sxs-lookup"><span data-stu-id="daa50-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="daa50-106">U kunt ook andere details leren door te kijken Hallo details van Hallo [werkstroom Definition Language](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="daa50-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="daa50-107">Lees verder toolearn meer informatie over triggers en acties en hoe u kunt ze gebruiken toobuild logic apps tooimprove uw bedrijfsprocessen en werkstromen.</span><span class="sxs-lookup"><span data-stu-id="daa50-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="daa50-108">Triggers</span><span class="sxs-lookup"><span data-stu-id="daa50-108">Triggers</span></span>  

<span data-ttu-id="daa50-109">Een trigger geeft Hallo-aanroepen die een uitvoering van uw logische app werkstroom kunnen initiëren.</span><span class="sxs-lookup"><span data-stu-id="daa50-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="daa50-110">Hier volgen Hallo twee verschillende manieren tooinitiate een uitvoering van uw werkstroom:</span><span class="sxs-lookup"><span data-stu-id="daa50-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="daa50-111">Een polling-trigger</span><span class="sxs-lookup"><span data-stu-id="daa50-111">A polling trigger</span></span>  

-   <span data-ttu-id="daa50-112">Een push-signaal - door de aanroepende Hallo [REST-API van Workflow](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="daa50-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="daa50-113">Alle triggers bevatten deze op het hoogste niveau elementen:</span><span class="sxs-lookup"><span data-stu-id="daa50-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="daa50-114">Triggertypen en hun invoer</span><span class="sxs-lookup"><span data-stu-id="daa50-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="daa50-115">U kunt deze typen triggers:</span><span class="sxs-lookup"><span data-stu-id="daa50-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="daa50-116">**Aanvraag** \- Hallo logische app maakt een eindpunt voor u toocall</span><span class="sxs-lookup"><span data-stu-id="daa50-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="daa50-117">**Terugkeerpatroon** \- deze gebeurtenis wordt gestart op basis van een gedefinieerde planning</span><span class="sxs-lookup"><span data-stu-id="daa50-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="daa50-118">**HTTP** \- een HTTP-web-eindpunt worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="daa50-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="daa50-119">Hallo HTTP-eindpunt moet voldoen tooa specifieke activerende contract \- met behulp van een 202\-asynchrone patroon, of door te retourneren van een matrix</span><span class="sxs-lookup"><span data-stu-id="daa50-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="daa50-120">**ApiConnection** \- Polls zoals Hallo HTTP is geactiveerd, maar deze wordt gebruikgemaakt van Hallo [door Microsoft beheerde API's](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="daa50-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="daa50-121">**HTTPWebhook** \- opent een eindpunt, vergelijkbare toohello handmatige worden geactiveerd, maar deze ook illustreert tooa opgegeven URL tooregister en ongedaan maken</span><span class="sxs-lookup"><span data-stu-id="daa50-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="daa50-122">**ApiConnectionWebhook** \- fungeert als HTTPWebhook trigger Hallo door gebruik te maken van Hallo door Microsoft beheerde API's</span><span class="sxs-lookup"><span data-stu-id="daa50-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="daa50-123">Elk triggertype heeft een andere set **invoer** het gedrag te definiëren.</span><span class="sxs-lookup"><span data-stu-id="daa50-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="daa50-124">Aanvraag trigger</span><span class="sxs-lookup"><span data-stu-id="daa50-124">Request trigger</span></span>  

<span data-ttu-id="daa50-125">Deze trigger fungeert als een eindpunt dat u via een HTTP-aanvraag tooinvoke uw logische app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="daa50-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="daa50-126">Een aanvraag-trigger ziet er in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="daa50-127">Er is ook een optionele eigenschap aangeroepen **schema**:</span><span class="sxs-lookup"><span data-stu-id="daa50-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="daa50-128">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-128">Element name</span></span>|<span data-ttu-id="daa50-129">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-129">Required</span></span>|<span data-ttu-id="daa50-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="daa50-131">Schema</span><span class="sxs-lookup"><span data-stu-id="daa50-131">schema</span></span>|<span data-ttu-id="daa50-132">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-132">No</span></span>|<span data-ttu-id="daa50-133">Een JSON-schema waarmee inkomende hello-aanvraag wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="daa50-134">Is handig voor het volgende werkstroomstappen weten welke tooreference eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="daa50-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="daa50-135">tooinvoke dit eindpunt, moet u toocall hello *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="daa50-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="daa50-136">Zie [REST-API van werkstroom](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="daa50-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="daa50-137">Terugkeerpatroon trigger</span><span class="sxs-lookup"><span data-stu-id="daa50-137">Recurrence trigger</span></span>  

<span data-ttu-id="daa50-138">Een terugkeerpatroon trigger is die wordt uitgevoerd op basis volgens een ingesteld schema.</span><span class="sxs-lookup"><span data-stu-id="daa50-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="daa50-139">Dergelijke trigger lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="daa50-140">Zoals u ziet, is een eenvoudige manier toorun een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="daa50-141">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-141">Element name</span></span>|<span data-ttu-id="daa50-142">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-142">Required</span></span>|<span data-ttu-id="daa50-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="daa50-144">frequency</span><span class="sxs-lookup"><span data-stu-id="daa50-144">frequency</span></span>|<span data-ttu-id="daa50-145">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-145">Yes</span></span>|<span data-ttu-id="daa50-146">Hoe vaak hello trigger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-146">How often hello trigger executes.</span></span> <span data-ttu-id="daa50-147">Gebruik slechts één van deze mogelijke waarden: seconde, minuut, uur, dag, week, maand of jaar</span><span class="sxs-lookup"><span data-stu-id="daa50-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="daa50-148">interval</span><span class="sxs-lookup"><span data-stu-id="daa50-148">interval</span></span>|<span data-ttu-id="daa50-149">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-149">Yes</span></span>|<span data-ttu-id="daa50-150">Het interval van Hallo opgegeven frequentie voor Hallo terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="daa50-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="daa50-151">startTime</span><span class="sxs-lookup"><span data-stu-id="daa50-151">startTime</span></span>|<span data-ttu-id="daa50-152">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-152">No</span></span>|<span data-ttu-id="daa50-153">Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="daa50-154">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="daa50-154">timeZone</span></span>|<span data-ttu-id="daa50-155">Er is geen</span><span class="sxs-lookup"><span data-stu-id="daa50-155">no</span></span>|<span data-ttu-id="daa50-156">Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="daa50-157">U kunt ook een trigger toostart uitvoeren op een bepaald moment in toekomstige Hallo plannen.</span><span class="sxs-lookup"><span data-stu-id="daa50-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="daa50-158">Bijvoorbeeld, als u wilt dat een wekelijkse rapporteren elke maandag toostart kunt u plannen Hallo logic app toostart elke maandag door het maken van Hallo trigger te volgen:</span><span class="sxs-lookup"><span data-stu-id="daa50-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="daa50-159">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="daa50-159">HTTP trigger</span></span>  

<span data-ttu-id="daa50-160">HTTP-triggers peilen op een opgegeven eindpunt en Hallo antwoord toodetermine controleren of er Hallo werkstroom moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="daa50-161">Hallo invoer object heeft Hallo set parameters vereist tooconstruct een HTTP-aanroep:</span><span class="sxs-lookup"><span data-stu-id="daa50-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="daa50-162">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-162">Element name</span></span>|<span data-ttu-id="daa50-163">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-163">Required</span></span>|<span data-ttu-id="daa50-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-164">Description</span></span>|<span data-ttu-id="daa50-165">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="daa50-166">Methode</span><span class="sxs-lookup"><span data-stu-id="daa50-166">method</span></span>|<span data-ttu-id="daa50-167">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-167">yes</span></span>|<span data-ttu-id="daa50-168">Een van de volgende HTTP-methoden Hallo: GET, POST, PUT, DELETE, PATCH of HEAD</span><span class="sxs-lookup"><span data-stu-id="daa50-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="daa50-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-169">String</span></span>|  
|<span data-ttu-id="daa50-170">URI</span><span class="sxs-lookup"><span data-stu-id="daa50-170">uri</span></span>|<span data-ttu-id="daa50-171">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-171">yes</span></span>|<span data-ttu-id="daa50-172">Hallo http of https-eindpunt dat wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="daa50-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="daa50-173">Maximum van 2 kB.</span><span class="sxs-lookup"><span data-stu-id="daa50-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="daa50-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-174">String</span></span>|  
|<span data-ttu-id="daa50-175">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-175">queries</span></span>|<span data-ttu-id="daa50-176">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-176">No</span></span>|<span data-ttu-id="daa50-177">Een object die Hallo query parameters tooadd toohello URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="daa50-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="daa50-178">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="daa50-179">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-179">Object</span></span>|  
|<span data-ttu-id="daa50-180">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-180">headers</span></span>|<span data-ttu-id="daa50-181">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-181">No</span></span>|<span data-ttu-id="daa50-182">Object voor elk van de Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-183">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="daa50-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="daa50-184">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-184">Object</span></span>|  
|<span data-ttu-id="daa50-185">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-185">body</span></span>|<span data-ttu-id="daa50-186">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-186">No</span></span>|<span data-ttu-id="daa50-187">Een object dat vertegenwoordigt Hallo nettolading dat toohello eindpunt wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="daa50-188">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-188">Object</span></span>|  
|<span data-ttu-id="daa50-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="daa50-189">retryPolicy</span></span>|<span data-ttu-id="daa50-190">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-190">No</span></span>|<span data-ttu-id="daa50-191">Een object dat u kunt aanpassen Hallo gedrag voor het opnieuw op 4xx of 5xx-fouten.</span><span class="sxs-lookup"><span data-stu-id="daa50-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="daa50-192">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-192">Object</span></span>|  
|<span data-ttu-id="daa50-193">Verificatie</span><span class="sxs-lookup"><span data-stu-id="daa50-193">authentication</span></span>|<span data-ttu-id="daa50-194">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-194">No</span></span>|<span data-ttu-id="daa50-195">Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="daa50-196">Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="daa50-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="daa50-197">Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority` deze waarde is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="daa50-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="daa50-198">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-198">Object</span></span>|  
  
<span data-ttu-id="daa50-199">de HTTP-trigger Hallo vereist Hallo HTTP API tooconform met een specifiek patroon toowork goed met uw logische app.</span><span class="sxs-lookup"><span data-stu-id="daa50-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="daa50-200">Hiervoor Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="daa50-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="daa50-201">Antwoord</span><span class="sxs-lookup"><span data-stu-id="daa50-201">Response</span></span>|<span data-ttu-id="daa50-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="daa50-203">Statuscode</span><span class="sxs-lookup"><span data-stu-id="daa50-203">Status code</span></span>|<span data-ttu-id="daa50-204">Statuscode 200 \(OK\) toocause-run.</span><span class="sxs-lookup"><span data-stu-id="daa50-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="daa50-205">Andere statuscode niet leiden tot een uitvoering.</span><span class="sxs-lookup"><span data-stu-id="daa50-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="daa50-206">Probeer\-na header</span><span class="sxs-lookup"><span data-stu-id="daa50-206">Retry\-after header</span></span>|<span data-ttu-id="daa50-207">Het aantal seconden tot Hallo logische app Hallo eindpunt opnieuw worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="daa50-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="daa50-208">Locatieheader</span><span class="sxs-lookup"><span data-stu-id="daa50-208">Location header</span></span>|<span data-ttu-id="daa50-209">Hallo URL toocall op Hallo volgende polling-interval.</span><span class="sxs-lookup"><span data-stu-id="daa50-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="daa50-210">Als niet wordt opgegeven, wordt de oorspronkelijke URL Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="daa50-211">Hier volgen enkele voorbeelden van andere problemen voor verschillende soorten aanvragen:</span><span class="sxs-lookup"><span data-stu-id="daa50-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="daa50-212">Reactiecode</span><span class="sxs-lookup"><span data-stu-id="daa50-212">Response code</span></span>|<span data-ttu-id="daa50-213">Probeer\-na</span><span class="sxs-lookup"><span data-stu-id="daa50-213">Retry\-After</span></span>|<span data-ttu-id="daa50-214">Gedrag</span><span class="sxs-lookup"><span data-stu-id="daa50-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="daa50-215">200</span><span class="sxs-lookup"><span data-stu-id="daa50-215">200</span></span>|<span data-ttu-id="daa50-216">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="daa50-216">\(none\)</span></span>|<span data-ttu-id="daa50-217">Niet een geldig worden geactiveerd, opnieuw proberen\-na is vereist of anders Hallo-engine nooit polls voor volgende Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="daa50-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="daa50-218">202</span><span class="sxs-lookup"><span data-stu-id="daa50-218">202</span></span>|<span data-ttu-id="daa50-219">60</span><span class="sxs-lookup"><span data-stu-id="daa50-219">60</span></span>|<span data-ttu-id="daa50-220">Hallo-werkstroom niet activeren.</span><span class="sxs-lookup"><span data-stu-id="daa50-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="daa50-221">Hallo opnieuw probeert gebeurt in een minuut.</span><span class="sxs-lookup"><span data-stu-id="daa50-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="daa50-222">200</span><span class="sxs-lookup"><span data-stu-id="daa50-222">200</span></span>|<span data-ttu-id="daa50-223">10</span><span class="sxs-lookup"><span data-stu-id="daa50-223">10</span></span>|<span data-ttu-id="daa50-224">Hallo-werkstroom uitvoert, en opnieuw controleren voor meer informatie over 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="daa50-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="daa50-225">400</span><span class="sxs-lookup"><span data-stu-id="daa50-225">400</span></span>|<span data-ttu-id="daa50-226">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="daa50-226">\(none\)</span></span>|<span data-ttu-id="daa50-227">Onjuiste aanvraag, Hallo-werkstroom niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="daa50-228">Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="daa50-229">Nadat het Hallo aantal nieuwe pogingen is bereikt, is Hallo trigger niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="daa50-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="daa50-230">500</span><span class="sxs-lookup"><span data-stu-id="daa50-230">500</span></span>|<span data-ttu-id="daa50-231">\(geen\)</span><span class="sxs-lookup"><span data-stu-id="daa50-231">\(none\)</span></span>|<span data-ttu-id="daa50-232">Fout-server, worden niet uitgevoerd Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="daa50-233">Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="daa50-234">Nadat het Hallo aantal nieuwe pogingen is bereikt, is Hallo trigger niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="daa50-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="daa50-235">Hallo uitvoerwaarden van een HTTP-trigger eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="daa50-236">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-236">Element name</span></span>|<span data-ttu-id="daa50-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-237">Description</span></span>|<span data-ttu-id="daa50-238">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="daa50-239">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-239">headers</span></span>|<span data-ttu-id="daa50-240">Hallo-headers van Hallo http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="daa50-240">hello headers of hello http response.</span></span>|<span data-ttu-id="daa50-241">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-241">Object</span></span>|  
|<span data-ttu-id="daa50-242">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-242">body</span></span>|<span data-ttu-id="daa50-243">Hallo-hoofdtekst van Hallo http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="daa50-243">hello body of hello http response.</span></span>|<span data-ttu-id="daa50-244">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="daa50-245">API-verbinding activeren</span><span class="sxs-lookup"><span data-stu-id="daa50-245">API Connection trigger</span></span>  

<span data-ttu-id="daa50-246">Hallo API verbinding trigger is vergelijkbaar toohello HTTP-trigger in de basisfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="daa50-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="daa50-247">Hallo-parameters voor het identificeren van Hallo actie zijn echter verschillend.</span><span class="sxs-lookup"><span data-stu-id="daa50-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="daa50-248">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="daa50-249">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-249">Element name</span></span>|<span data-ttu-id="daa50-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-250">Required</span></span>|<span data-ttu-id="daa50-251">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-251">Type</span></span>|<span data-ttu-id="daa50-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="daa50-253">host</span><span class="sxs-lookup"><span data-stu-id="daa50-253">host</span></span>|<span data-ttu-id="daa50-254">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-254">Yes</span></span>||<span data-ttu-id="daa50-255">Hallo ApiApp gehost gateway en -id.</span><span class="sxs-lookup"><span data-stu-id="daa50-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="daa50-256">Methode</span><span class="sxs-lookup"><span data-stu-id="daa50-256">method</span></span>|<span data-ttu-id="daa50-257">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-257">Yes</span></span>|<span data-ttu-id="daa50-258">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-258">String</span></span>|<span data-ttu-id="daa50-259">Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="daa50-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="daa50-260">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-260">queries</span></span>|<span data-ttu-id="daa50-261">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-261">No</span></span>|<span data-ttu-id="daa50-262">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-262">Object</span></span>|<span data-ttu-id="daa50-263">Vertegenwoordigt Hallo query parameters toobe toohello URL toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="daa50-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="daa50-264">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="daa50-265">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-265">headers</span></span>|<span data-ttu-id="daa50-266">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-266">No</span></span>|<span data-ttu-id="daa50-267">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-267">Object</span></span>|<span data-ttu-id="daa50-268">Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-269">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="daa50-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="daa50-270">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-270">body</span></span>|<span data-ttu-id="daa50-271">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-271">No</span></span>|<span data-ttu-id="daa50-272">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-272">Object</span></span>|<span data-ttu-id="daa50-273">Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="daa50-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="daa50-274">retryPolicy</span></span>|<span data-ttu-id="daa50-275">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-275">No</span></span>|<span data-ttu-id="daa50-276">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-276">Object</span></span>|<span data-ttu-id="daa50-277">Hiermee kunt u toocustomize Hallo gedrag voor het opnieuw op 4xx of 5xx-fouten.</span><span class="sxs-lookup"><span data-stu-id="daa50-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="daa50-278">Verificatie</span><span class="sxs-lookup"><span data-stu-id="daa50-278">authentication</span></span>|<span data-ttu-id="daa50-279">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-279">No</span></span>|<span data-ttu-id="daa50-280">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-280">Object</span></span>|<span data-ttu-id="daa50-281">Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="daa50-282">Zie voor meer informatie over dit object [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="daa50-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="daa50-283">Hallo-eigenschappen voor de host zijn:</span><span class="sxs-lookup"><span data-stu-id="daa50-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="daa50-284">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-284">Element name</span></span>|<span data-ttu-id="daa50-285">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-285">Required</span></span>|<span data-ttu-id="daa50-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="daa50-287">API-runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="daa50-287">api runtimeUrl</span></span>|<span data-ttu-id="daa50-288">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-288">Yes</span></span>|<span data-ttu-id="daa50-289">Hallo-eindpunt van Hallo beheerde API.</span><span class="sxs-lookup"><span data-stu-id="daa50-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="daa50-290">Verbindingsnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-290">connection name</span></span>||<span data-ttu-id="daa50-291">Moet worden verwijzing tooa parameter aangeroepen `$connection` en de naam Hallo Hallo managed API verbinding dat Hallo werkstroom gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="daa50-292">Hallo uitvoerwaarden van een API-trigger verbinding zijn:</span><span class="sxs-lookup"><span data-stu-id="daa50-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="daa50-293">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-293">Element name</span></span>|<span data-ttu-id="daa50-294">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-294">Type</span></span>|<span data-ttu-id="daa50-295">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="daa50-296">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-296">headers</span></span>|<span data-ttu-id="daa50-297">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-297">Object</span></span>|<span data-ttu-id="daa50-298">Hallo-headers van Hallo http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="daa50-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="daa50-299">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-299">body</span></span>|<span data-ttu-id="daa50-300">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-300">Object</span></span>|<span data-ttu-id="daa50-301">Hallo-hoofdtekst van Hallo http-antwoord.</span><span class="sxs-lookup"><span data-stu-id="daa50-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="daa50-302">HTTPWebhook trigger</span><span class="sxs-lookup"><span data-stu-id="daa50-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="daa50-303">Hallo HTTPWebhook trigger opent een eindpunt, vergelijkbare toohello handmatige trigger, maar Hallo HTTPWebhook trigger ook illustreert tooa opgegeven URL tooregister en ongedaan maken.</span><span class="sxs-lookup"><span data-stu-id="daa50-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="daa50-304">Hier volgt een voorbeeld van wat een trigger HTTPWebhook als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="daa50-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="daa50-305">Veel van deze gedeelten zijn optioneel en Hallo gedrag van Hallo Webhook is afhankelijk van welke gedeelten wordt geleverd of wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="daa50-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="daa50-306">Hallo-eigenschappen van een Webhook zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="daa50-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="daa50-307">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-307">Element name</span></span>|<span data-ttu-id="daa50-308">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-308">Required</span></span>|<span data-ttu-id="daa50-309">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="daa50-310">abonneren</span><span class="sxs-lookup"><span data-stu-id="daa50-310">subscribe</span></span>|<span data-ttu-id="daa50-311">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-311">No</span></span>|<span data-ttu-id="daa50-312">Hallo uitgaande aanvraag die wordt aangeroepen wanneer het Hallo-trigger wordt gemaakt en voert de initiële registratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="daa50-313">afmelden</span><span class="sxs-lookup"><span data-stu-id="daa50-313">unsubscribe</span></span>|<span data-ttu-id="daa50-314">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-314">No</span></span>|<span data-ttu-id="daa50-315">Hallo uitgaande aanvraag wanneer Hallo trigger wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="daa50-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="daa50-316">**Abonneren** Hallo uitgaand aanroep die toostart luisterende tooevents heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="daa50-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="daa50-317">Deze aanroep begint met het Hallo dezelfde set parameters die normale HTTP acties Hallo doen.</span><span class="sxs-lookup"><span data-stu-id="daa50-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="daa50-318">Deze uitgaande aanroep uitgevoerd elke keer Hallo wijzigingen voor de workflow op elke manier, bijvoorbeeld wanneer Hallo referenties worden hersteld of Hallo trigger parameters wijzigen de invoer.</span><span class="sxs-lookup"><span data-stu-id="daa50-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="daa50-319">toosupport dit aanroepen, er is een nieuwe functie: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="daa50-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="daa50-320">Deze functie retourneert een unieke URL voor deze specifieke trigger in deze workflow.</span><span class="sxs-lookup"><span data-stu-id="daa50-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="daa50-321">Deze vertegenwoordigt unieke id voor Hallo-eindpunten die gebruikmaken van Hallo Service REST Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="daa50-322">**Afmelden** wordt aangeroepen wanneer een bewerking renders deze trigger ongeldig, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="daa50-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="daa50-323">Het verwijderen of Hallo trigger uitschakelen</span><span class="sxs-lookup"><span data-stu-id="daa50-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="daa50-324">Het verwijderen of uitschakelen van Hallo-werkstroom</span><span class="sxs-lookup"><span data-stu-id="daa50-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="daa50-325">Het verwijderen of uitschakelen van Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="daa50-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="daa50-326">Hallo logic app roept automatisch Hallo actie opzeggen.</span><span class="sxs-lookup"><span data-stu-id="daa50-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="daa50-327">Hallo-parameters zijn van de functie toothis Hallo dezelfde als Hallo HTTP-trigger.</span><span class="sxs-lookup"><span data-stu-id="daa50-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="daa50-328">Hallo zijn uitvoerwaarden van Hallo HTTPWebhook trigger Hallo-inhoud voor inkomende hello-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="daa50-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="daa50-329">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-329">Element name</span></span>|<span data-ttu-id="daa50-330">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-330">Type</span></span>|<span data-ttu-id="daa50-331">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="daa50-332">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-332">headers</span></span>|<span data-ttu-id="daa50-333">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-333">Object</span></span>|<span data-ttu-id="daa50-334">Hallo-headers van Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="daa50-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="daa50-335">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-335">body</span></span>|<span data-ttu-id="daa50-336">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-336">Object</span></span>|<span data-ttu-id="daa50-337">Hallo-hoofdtekst van Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="daa50-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="daa50-338">Limieten van een webhook-actie kunnen worden opgegeven in Hallo dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="daa50-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="daa50-339">Voorwaarden</span><span class="sxs-lookup"><span data-stu-id="daa50-339">Conditions</span></span>  

<span data-ttu-id="daa50-340">Voor een trigger, kunt u een of meer voorwaarden toodetermine of Hallo werkstroom moet worden uitgevoerd of niet.</span><span class="sxs-lookup"><span data-stu-id="daa50-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="daa50-341">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-341">For example:</span></span>  

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

<span data-ttu-id="daa50-342">In dit geval Hallo rapport alleen triggers tijdens het Hallo-werkstroom `sendReports` parameter tootrue is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="daa50-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="daa50-343">Ten slotte voorwaarden kunnen verwijzen naar Hallo statuscode Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="daa50-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="daa50-344">U kan bijvoorbeeld ere van een werkstroom alleen als uw website een statuscode 500, als volgt retourneert:</span><span class="sxs-lookup"><span data-stu-id="daa50-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="daa50-345">Wanneer een expressie verwijst naar het Hallo-statuscode van Hallo trigger \(op elke manier\), Hallo standaardgedrag \(trigger alleen op 200 \(OK\) \) wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="daa50-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="daa50-346">Bijvoorbeeld, als u tootrigger op zowel de statuscode 200 als de statuscode 201 wilt, hebt u tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` als de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="daa50-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="daa50-347">Meerdere wordt uitgevoerd voor een aanvraag starten</span><span class="sxs-lookup"><span data-stu-id="daa50-347">Start multiple runs for a request</span></span>

<span data-ttu-id="daa50-348">tookick uit meerdere wordt uitgevoerd voor een enkele aanvraag `splitOn` is handig, bijvoorbeeld, als u wilt toopoll een eindpunt dat meerdere nieuwe items tussen polling-intervallen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="daa50-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="daa50-349">Met `splitOn`, geeft u de eigenschap Hallo binnen Hallo antwoord nettolading met Hallo-matrix van items die u wilt dat toouse toostart een uitvoering van het Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="daa50-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="daa50-350">Stel dat u hebt een API waarmee Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="daa50-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="daa50-351">Uw logische app moet alleen inhoud van de rijen hello, zodat u de trigger zoals in dit voorbeeld kunt maken:</span><span class="sxs-lookup"><span data-stu-id="daa50-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="daa50-352">Klik in de workflowdefinitie Hallo `@triggerBody().name` retourneert `mycoolrow` voor Hallo eerst uitvoert, en `another row` voor de tweede run Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="daa50-353">Hallo trigger uitvoer eruit zien in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="daa50-354">Als u in dat geval `SplitOn`, je geen toegang hebt Hallo-eigenschappen die buiten het Hallo-matrix in dit geval Hallo `Status` veld.</span><span class="sxs-lookup"><span data-stu-id="daa50-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="daa50-355">In dit voorbeeld gebruiken we Hallo `?` operator toobe kunnen tooavoid een fout als hello `Rows` eigenschap is niet aanwezig.</span><span class="sxs-lookup"><span data-stu-id="daa50-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="daa50-356">SIS uitvoeren</span><span class="sxs-lookup"><span data-stu-id="daa50-356">Single run instance</span></span>

<span data-ttu-id="daa50-357">Triggers die een terugkeerpatroon eigenschap tooonly brand hebben als alle actieve sessies hebt voltooid, kunt u configureren.</span><span class="sxs-lookup"><span data-stu-id="daa50-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="daa50-358">Als een geplande terugkeer optreedt terwijl er een uitgevoerd in voortgang is, wordt Hallo trigger wordt overgeslagen en wordt gewacht tot Hallo volgende geplande terugkeerpatroon interval toocheck opnieuw.</span><span class="sxs-lookup"><span data-stu-id="daa50-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="daa50-359">U kunt deze instelling door Hallo bewerking opties configureren:</span><span class="sxs-lookup"><span data-stu-id="daa50-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="daa50-360">Typen en invoer</span><span class="sxs-lookup"><span data-stu-id="daa50-360">Types and inputs</span></span>  

<span data-ttu-id="daa50-361">Er zijn veel verschillende soorten acties, elk met unieke gedrag.</span><span class="sxs-lookup"><span data-stu-id="daa50-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="daa50-362">Verzameling acties mogelijk veel andere acties in zichzelf bevatten.</span><span class="sxs-lookup"><span data-stu-id="daa50-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="daa50-363">Standaardacties</span><span class="sxs-lookup"><span data-stu-id="daa50-363">Standard actions</span></span>  

-   <span data-ttu-id="daa50-364">**HTTP** deze actie wordt een HTTP-web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="daa50-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="daa50-365">**ApiConnection** \- deze bewerking gedraagt zich alsof Hallo HTTP-actie, maar gebruikt Hallo door Microsoft beheerde API's.</span><span class="sxs-lookup"><span data-stu-id="daa50-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="daa50-366">**ApiConnectionWebhook** \- zoals HTTPWebhook, maar gebruikt Hallo door Microsoft beheerde API's.</span><span class="sxs-lookup"><span data-stu-id="daa50-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="daa50-367">**Antwoord** \- deze actie wordt een antwoord voor een inkomend gesprek gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="daa50-368">**Wacht** \- deze eenvoudige actie wacht een vast bedrag tijd of totdat een bepaalde tijd.</span><span class="sxs-lookup"><span data-stu-id="daa50-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="daa50-369">**Werkstroom** \- deze actie vertegenwoordigt een geneste werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="daa50-370">**De functie** \- deze actie vertegenwoordigt een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="daa50-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="daa50-371">Verzameling acties</span><span class="sxs-lookup"><span data-stu-id="daa50-371">Collection actions</span></span>

-   <span data-ttu-id="daa50-372">**Bereik** \- deze actie is een logische groepering van andere acties.</span><span class="sxs-lookup"><span data-stu-id="daa50-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="daa50-373">**Voorwaarde** \- met deze actie evalueert een expressie en het bijbehorende resultaat vertakking hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="daa50-374">**ForEach** \- samenvoegartikel hierdoor een matrix doorlopen en interne acties uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="daa50-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="daa50-375">**Pas** \- binnenste acties van deze samenvoegartikel actie wordt uitgevoerd totdat een voorwaarde tootrue resulteert.</span><span class="sxs-lookup"><span data-stu-id="daa50-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="daa50-376">Elk type actie heeft een andere set **invoer** die een actie gedrag definiëren.</span><span class="sxs-lookup"><span data-stu-id="daa50-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="daa50-377">HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="daa50-377">HTTP action</span></span>  

<span data-ttu-id="daa50-378">HTTP-acties aanroepen van een opgegeven eindpunt en Hallo antwoord toodetermine controleren of er Hallo werkstroom moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="daa50-379">Hallo **invoer** object Hallo set parameters vereist tooconstruct Hallo HTTP-aanroep heeft:</span><span class="sxs-lookup"><span data-stu-id="daa50-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="daa50-380">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-380">Element name</span></span>|<span data-ttu-id="daa50-381">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-381">Required</span></span>|<span data-ttu-id="daa50-382">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-382">Type</span></span>|<span data-ttu-id="daa50-383">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="daa50-384">Methode</span><span class="sxs-lookup"><span data-stu-id="daa50-384">method</span></span>|<span data-ttu-id="daa50-385">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-385">Yes</span></span>|<span data-ttu-id="daa50-386">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-386">String</span></span>|<span data-ttu-id="daa50-387">Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="daa50-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="daa50-388">URI</span><span class="sxs-lookup"><span data-stu-id="daa50-388">uri</span></span>|<span data-ttu-id="daa50-389">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-389">Yes</span></span>|<span data-ttu-id="daa50-390">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-390">String</span></span>|<span data-ttu-id="daa50-391">Hallo http of https-eindpunt dat wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="daa50-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="daa50-392">Maximale lengte is 2 kB.</span><span class="sxs-lookup"><span data-stu-id="daa50-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="daa50-393">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-393">queries</span></span>|<span data-ttu-id="daa50-394">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-394">No</span></span>|<span data-ttu-id="daa50-395">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-395">Object</span></span>|<span data-ttu-id="daa50-396">Hallo query parameters tooadd toohello URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="daa50-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="daa50-397">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="daa50-398">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-398">headers</span></span>|<span data-ttu-id="daa50-399">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-399">No</span></span>|<span data-ttu-id="daa50-400">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-400">Object</span></span>|<span data-ttu-id="daa50-401">Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-402">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="daa50-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="daa50-403">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-403">body</span></span>|<span data-ttu-id="daa50-404">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-404">No</span></span>|<span data-ttu-id="daa50-405">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-405">Object</span></span>|<span data-ttu-id="daa50-406">Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="daa50-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="daa50-407">retryPolicy</span></span>|<span data-ttu-id="daa50-408">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-408">No</span></span>|<span data-ttu-id="daa50-409">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-409">Object</span></span>|<span data-ttu-id="daa50-410">Hiermee kunt u aanpassen Hallo opnieuw gedrag voor 4xx of 5xx-fouten.</span><span class="sxs-lookup"><span data-stu-id="daa50-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="daa50-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="daa50-411">operationsOptions</span></span>|<span data-ttu-id="daa50-412">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-412">No</span></span>|<span data-ttu-id="daa50-413">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-413">String</span></span>|<span data-ttu-id="daa50-414">Hallo set speciaal gedrag toooverride gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="daa50-415">Verificatie</span><span class="sxs-lookup"><span data-stu-id="daa50-415">authentication</span></span>|<span data-ttu-id="daa50-416">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-416">No</span></span>|<span data-ttu-id="daa50-417">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-417">Object</span></span>|<span data-ttu-id="daa50-418">Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="daa50-419">Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="daa50-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="daa50-420">Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority`.</span><span class="sxs-lookup"><span data-stu-id="daa50-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="daa50-421">Dit is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="daa50-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="daa50-422">HTTP-acties \(en API-verbinding\) acties ondersteuning beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="daa50-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="daa50-423">Een beleid voor opnieuw proberen is van toepassing toointermittent fouten, gekenmerkt als HTTP-status 408 429 en 5xx in toevoeging tooany verbindingsuitzonderingen-codes.</span><span class="sxs-lookup"><span data-stu-id="daa50-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="daa50-424">Dit beleid wordt beschreven met Hallo *retryPolicy* object dat is gedefinieerd als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="daa50-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="daa50-425">Hallo-interval voor opnieuw proberen is opgegeven in Hallo ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="daa50-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="daa50-426">Dit interval heeft een standaard en de minimumwaarde van 20 seconden terwijl Hallo maximale waarde een uur is.</span><span class="sxs-lookup"><span data-stu-id="daa50-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="daa50-427">Hallo standaard en maximum aantal pogingen een waarde is gelijk aan vier uur.</span><span class="sxs-lookup"><span data-stu-id="daa50-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="daa50-428">Als de definitie voor nieuwe pogingen voor Hallo niet is opgegeven, een `fixed` strategie met een standaardwaarde opnieuw telling en het interval wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="daa50-429">beleid voor opnieuw proberen van toodisable hello, stel het type te`None`.</span><span class="sxs-lookup"><span data-stu-id="daa50-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="daa50-430">Bijvoorbeeld hello volgende actie probeert opnieuw ophalen Hallo laatste nieuws twee keer als er onregelmatige problemen, voor een totaal van drie uitvoeringen, met een vertraging 30 seconden tussen elke poging:</span><span class="sxs-lookup"><span data-stu-id="daa50-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="daa50-431">Asynchrone patronen</span><span class="sxs-lookup"><span data-stu-id="daa50-431">Asynchronous patterns</span></span>

<span data-ttu-id="daa50-432">Standaard ondersteunt alle HTTP-gebaseerde acties Hallo standaard asynchrone bewerking patroon.</span><span class="sxs-lookup"><span data-stu-id="daa50-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="daa50-433">Dus als de externe server Hallo die Hallo-aanvraag aangeeft is geaccepteerd voor verwerking met een 202 \(geaccepteerde\) antwoord Hallo Logic Apps-engine houdt polling Hallo URL die is opgegeven in de locatie-header van het antwoord Hallo tot het bereiken van een terminal status \(niet\-202 antwoord\).</span><span class="sxs-lookup"><span data-stu-id="daa50-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="daa50-434">toodisable hello asynchrone gedrag ingesteld eerder beschreven, een `DisableAsyncPattern` optie in Hallo actie invoer.</span><span class="sxs-lookup"><span data-stu-id="daa50-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="daa50-435">In dit geval is Hallo-uitvoer van Hallo actie gebaseerd op Hallo initiële 202 reactie van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="daa50-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="daa50-436">Asynchrone limieten</span><span class="sxs-lookup"><span data-stu-id="daa50-436">Asynchronous Limits</span></span>

<span data-ttu-id="daa50-437">Een asynchrone patroon worden de tijdsinterval duur tooa specifieke beperkt.</span><span class="sxs-lookup"><span data-stu-id="daa50-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="daa50-438">Als Hallo tijdsinterval is verstreken zonder dat een definitieve status bereikt, Hallo status van Hallo actie gemarkeerd `Cancelled` met de code `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="daa50-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="daa50-439">Hallo limiet time-out is opgegeven in de ISO 8601-notatie.</span><span class="sxs-lookup"><span data-stu-id="daa50-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="daa50-440">Limieten kunnen worden opgegeven met de Hallo de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="daa50-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="daa50-441">API-verbinding</span><span class="sxs-lookup"><span data-stu-id="daa50-441">API Connection</span></span>  

<span data-ttu-id="daa50-442">API-verbinding is een actie die verwijst naar een connector door Microsoft beheerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="daa50-443">Deze actie vereist een geldige verwijzing tooa-verbinding en informatie over het Hallo API en de vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="daa50-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="daa50-444">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="daa50-444">Element name</span></span>|<span data-ttu-id="daa50-445">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-445">Required</span></span>|<span data-ttu-id="daa50-446">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-446">Type</span></span>|<span data-ttu-id="daa50-447">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="daa50-448">host</span><span class="sxs-lookup"><span data-stu-id="daa50-448">host</span></span>|<span data-ttu-id="daa50-449">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-449">Yes</span></span>|<span data-ttu-id="daa50-450">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-450">Object</span></span>|<span data-ttu-id="daa50-451">Hiermee geeft u Hallo connector informatie zoals Hallo runtimeUrl en verwijzing toohello connection-object</span><span class="sxs-lookup"><span data-stu-id="daa50-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="daa50-452">Methode</span><span class="sxs-lookup"><span data-stu-id="daa50-452">method</span></span>|<span data-ttu-id="daa50-453">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-453">Yes</span></span>|<span data-ttu-id="daa50-454">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-454">String</span></span>|<span data-ttu-id="daa50-455">Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="daa50-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="daa50-456">Pad</span><span class="sxs-lookup"><span data-stu-id="daa50-456">path</span></span>|<span data-ttu-id="daa50-457">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-457">Yes</span></span>|<span data-ttu-id="daa50-458">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-458">String</span></span>|<span data-ttu-id="daa50-459">Hallo-pad van Hallo API-bewerking.</span><span class="sxs-lookup"><span data-stu-id="daa50-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="daa50-460">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-460">queries</span></span>|<span data-ttu-id="daa50-461">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-461">No</span></span>|<span data-ttu-id="daa50-462">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-462">Object</span></span>|<span data-ttu-id="daa50-463">Hallo query parameters tooadd toohello URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="daa50-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="daa50-464">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="daa50-465">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-465">headers</span></span>|<span data-ttu-id="daa50-466">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-466">No</span></span>|<span data-ttu-id="daa50-467">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-467">Object</span></span>|<span data-ttu-id="daa50-468">Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-469">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="daa50-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="daa50-470">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-470">body</span></span>|<span data-ttu-id="daa50-471">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-471">No</span></span>|<span data-ttu-id="daa50-472">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-472">Object</span></span>|<span data-ttu-id="daa50-473">Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="daa50-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="daa50-474">retryPolicy</span></span>|<span data-ttu-id="daa50-475">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-475">No</span></span>|<span data-ttu-id="daa50-476">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-476">Object</span></span>|<span data-ttu-id="daa50-477">Hiermee kunt u aanpassen Hallo opnieuw gedrag voor 4xx of 5xx-fouten.</span><span class="sxs-lookup"><span data-stu-id="daa50-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="daa50-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="daa50-478">operationsOptions</span></span>|<span data-ttu-id="daa50-479">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-479">No</span></span>|<span data-ttu-id="daa50-480">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-480">String</span></span>|<span data-ttu-id="daa50-481">Hallo set speciaal gedrag toooverride gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="daa50-482">API-verbinding webhook actie</span><span class="sxs-lookup"><span data-stu-id="daa50-482">API Connection webhook action</span></span>

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

<span data-ttu-id="daa50-483">Limieten van een webhook-actie kunnen worden opgegeven in Hallo dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="daa50-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="daa50-484">Antwoord actie</span><span class="sxs-lookup"><span data-stu-id="daa50-484">Response action</span></span>  

<span data-ttu-id="daa50-485">Dit actietype Hallo volledige antwoord nettolading van een HTTP-aanvraag bevat en een statusCode, hoofdtekst en headers omvat:</span><span class="sxs-lookup"><span data-stu-id="daa50-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="daa50-486">Hallo antwoord actie heeft speciale beperkingen die niet van toepassing tooother acties.</span><span class="sxs-lookup"><span data-stu-id="daa50-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="daa50-487">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="daa50-487">Specifically:</span></span>  
  
-   <span data-ttu-id="daa50-488">Reacties kunnen niet in een definitie van een parallelle omdat een deterministische antwoord toohello binnenkomende aanvraag vereist is.</span><span class="sxs-lookup"><span data-stu-id="daa50-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="daa50-489">Als een antwoord-actie is bereikt nadat inkomende hello-aanvraag heeft een antwoord ontvangen, Hallo actie wordt beschouwd als mislukt \(conflict\), en als gevolg hiervan Hallo uitvoeren `Failed`.</span><span class="sxs-lookup"><span data-stu-id="daa50-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="daa50-490">Een werkstroom met reacties kan geen `splitOn` in de trigger omdat één aanroep ervoor zorgt veel wordt uitgevoerd dat.</span><span class="sxs-lookup"><span data-stu-id="daa50-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="daa50-491">Dit moet als gevolg hiervan worden gevalideerd wanneer het Hallo-stroom is PUT en oorzaak is een ongeldige aanvraag.</span><span class="sxs-lookup"><span data-stu-id="daa50-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="daa50-492">Actie wachten</span><span class="sxs-lookup"><span data-stu-id="daa50-492">Wait action</span></span>  

<span data-ttu-id="daa50-493">Hallo `wait` actie onderbreekt de uitvoering van de werkstroom voor Hallo opgegeven interval.</span><span class="sxs-lookup"><span data-stu-id="daa50-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="daa50-494">Bijvoorbeeld, toowait 15 minuten kunt u in dit fragment:</span><span class="sxs-lookup"><span data-stu-id="daa50-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="daa50-495">U kunt ook toowait tot een bepaald moment, kunt u dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="daa50-496">Hallo wacht duur ofwel kan worden opgegeven met de Hallo **interval** object of Hallo **totdat** , maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="daa50-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="daa50-497">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-497">Name</span></span>|<span data-ttu-id="daa50-498">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-498">Required</span></span>|<span data-ttu-id="daa50-499">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-499">Type</span></span>|<span data-ttu-id="daa50-500">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-501">interval</span><span class="sxs-lookup"><span data-stu-id="daa50-501">interval</span></span>|<span data-ttu-id="daa50-502">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-502">No</span></span>|<span data-ttu-id="daa50-503">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-503">Object</span></span>|<span data-ttu-id="daa50-504">Hallo wacht duur op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="daa50-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="daa50-505">intervaleenheid</span><span class="sxs-lookup"><span data-stu-id="daa50-505">interval unit</span></span>|<span data-ttu-id="daa50-506">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-506">Yes</span></span>|<span data-ttu-id="daa50-507">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-507">String</span></span>|<span data-ttu-id="daa50-508">Een van deze intervallen: seconde, minuut, uur, dag, week, maand, jaar.</span><span class="sxs-lookup"><span data-stu-id="daa50-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="daa50-509">interval aantal</span><span class="sxs-lookup"><span data-stu-id="daa50-509">interval count</span></span>|<span data-ttu-id="daa50-510">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-510">Yes</span></span>|<span data-ttu-id="daa50-511">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-511">String</span></span>|<span data-ttu-id="daa50-512">De duur op basis van Hallo opgegeven interne eenheid.</span><span class="sxs-lookup"><span data-stu-id="daa50-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="daa50-513">pas</span><span class="sxs-lookup"><span data-stu-id="daa50-513">until</span></span>|<span data-ttu-id="daa50-514">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-514">No</span></span>|<span data-ttu-id="daa50-515">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-515">Object</span></span>|<span data-ttu-id="daa50-516">Hallo wacht duur op basis van een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="daa50-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="daa50-517">Pas de timestamp</span><span class="sxs-lookup"><span data-stu-id="daa50-517">until timestamp</span></span>|<span data-ttu-id="daa50-518">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-518">Yes</span></span>|<span data-ttu-id="daa50-519">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-519">String</span></span>|<span data-ttu-id="daa50-520">Tekenreeks &#124; Hallo punt in tijd in UTC wanneer Hallo wachttijd is verlopen.</span><span class="sxs-lookup"><span data-stu-id="daa50-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="daa50-521">Queryactie</span><span class="sxs-lookup"><span data-stu-id="daa50-521">Query action</span></span>

<span data-ttu-id="daa50-522">Hallo `query` actie kunt u filteren op basis van een voorwaarde matrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="daa50-523">Bijvoorbeeld: tooselect getallen die groter zijn dan 2, u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="daa50-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="daa50-524">de uitvoer van Hallo Hallo `query` actie is een matrix met elementen van de invoermatrix Hallo die voldoen aan de voorwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="daa50-525">Als geen waarden voldoen aan Hallo `where` voorwaarde, hello resultaat is een lege matrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="daa50-526">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-526">Name</span></span>|<span data-ttu-id="daa50-527">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-527">Required</span></span>|<span data-ttu-id="daa50-528">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-528">Type</span></span>|<span data-ttu-id="daa50-529">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="daa50-530">Van</span><span class="sxs-lookup"><span data-stu-id="daa50-530">from</span></span>|<span data-ttu-id="daa50-531">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-531">Yes</span></span>|<span data-ttu-id="daa50-532">Matrix</span><span class="sxs-lookup"><span data-stu-id="daa50-532">Array</span></span>|<span data-ttu-id="daa50-533">Hallo bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-533">hello source array.</span></span>|
|<span data-ttu-id="daa50-534">waar</span><span class="sxs-lookup"><span data-stu-id="daa50-534">where</span></span>|<span data-ttu-id="daa50-535">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-535">Yes</span></span>|<span data-ttu-id="daa50-536">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-536">String</span></span>|<span data-ttu-id="daa50-537">Hallo voorwaarde tooapply tooeach element van de bronmatrix Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="daa50-538">Selecteer actie</span><span class="sxs-lookup"><span data-stu-id="daa50-538">Select action</span></span>

<span data-ttu-id="daa50-539">Hallo `select` actie kunt u elk element van een matrix project in een nieuwe waarde.</span><span class="sxs-lookup"><span data-stu-id="daa50-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="daa50-540">Bijvoorbeeld, tooconvert een matrix van getallen in een matrix met objecten, kunt u het volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="daa50-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="daa50-541">uitvoer van Hallo Hallo `select` actie is een matrix met Hallo dezelfde kardinaliteit zoals Hallo invoermatrix, waarbij elk element omgezet als gedefinieerd door Hallo `select` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="daa50-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="daa50-542">Als het Hallo-invoer is een lege matrix, is Hallo uitvoer ook een lege matrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="daa50-543">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-543">Name</span></span>|<span data-ttu-id="daa50-544">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-544">Required</span></span>|<span data-ttu-id="daa50-545">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-545">Type</span></span>|<span data-ttu-id="daa50-546">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="daa50-547">Van</span><span class="sxs-lookup"><span data-stu-id="daa50-547">from</span></span>|<span data-ttu-id="daa50-548">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-548">Yes</span></span>|<span data-ttu-id="daa50-549">Matrix</span><span class="sxs-lookup"><span data-stu-id="daa50-549">Array</span></span>|<span data-ttu-id="daa50-550">Hallo bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-550">hello source array.</span></span>|
|<span data-ttu-id="daa50-551">Selecteer</span><span class="sxs-lookup"><span data-stu-id="daa50-551">select</span></span>|<span data-ttu-id="daa50-552">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-552">Yes</span></span>|<span data-ttu-id="daa50-553">Alle</span><span class="sxs-lookup"><span data-stu-id="daa50-553">Any</span></span>|<span data-ttu-id="daa50-554">Hallo projectie tooapply tooeach element van de bronmatrix Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="daa50-555">Actie beëindigen</span><span class="sxs-lookup"><span data-stu-id="daa50-555">Terminate action</span></span>

<span data-ttu-id="daa50-556">Hallo actie beëindigen stopt u de uitvoering van Hallo werkstroom uitvoert, wordt afgebroken onderweg acties en eventuele resterende acties wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="daa50-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="daa50-557">Bijvoorbeeld, een reeks met de status tooterminate **mislukt**, kunt u Hallo volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="daa50-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="daa50-558">Reeds voltooide acties worden niet beïnvloed door Hallo actie beëindigen.</span><span class="sxs-lookup"><span data-stu-id="daa50-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="daa50-559">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-559">Name</span></span>|<span data-ttu-id="daa50-560">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-560">Required</span></span>|<span data-ttu-id="daa50-561">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-561">Type</span></span>|<span data-ttu-id="daa50-562">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="daa50-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="daa50-563">runStatus</span></span>|<span data-ttu-id="daa50-564">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-564">Yes</span></span>|<span data-ttu-id="daa50-565">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-565">String</span></span>|<span data-ttu-id="daa50-566">Hallo-doel status uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="daa50-566">hello target run status.</span></span> <span data-ttu-id="daa50-567">Beide **mislukt** of **geannuleerd**.</span><span class="sxs-lookup"><span data-stu-id="daa50-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="daa50-568">runError</span><span class="sxs-lookup"><span data-stu-id="daa50-568">runError</span></span>|<span data-ttu-id="daa50-569">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-569">No</span></span>|<span data-ttu-id="daa50-570">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-570">Object</span></span>|<span data-ttu-id="daa50-571">Hallo foutgegevens.</span><span class="sxs-lookup"><span data-stu-id="daa50-571">hello error details.</span></span> <span data-ttu-id="daa50-572">Alleen ondersteund wanneer **runStatus** te is ingesteld,**mislukt**.</span><span class="sxs-lookup"><span data-stu-id="daa50-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="daa50-573">runError code</span><span class="sxs-lookup"><span data-stu-id="daa50-573">runError code</span></span>|<span data-ttu-id="daa50-574">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-574">No</span></span>|<span data-ttu-id="daa50-575">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-575">String</span></span>|<span data-ttu-id="daa50-576">Hallo foutcode uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="daa50-576">hello run error code.</span></span>|
|<span data-ttu-id="daa50-577">runError bericht</span><span class="sxs-lookup"><span data-stu-id="daa50-577">runError message</span></span>|<span data-ttu-id="daa50-578">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-578">No</span></span>|<span data-ttu-id="daa50-579">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-579">String</span></span>|<span data-ttu-id="daa50-580">Hallo foutbericht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="daa50-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="daa50-581">Actie opstellen</span><span class="sxs-lookup"><span data-stu-id="daa50-581">Compose action</span></span>

<span data-ttu-id="daa50-582">Hallo opstellen actie kunt u een willekeurig object samenstellen.</span><span class="sxs-lookup"><span data-stu-id="daa50-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="daa50-583">Hallo-uitvoer van Hallo opstellen actie Hallo resultaat van evaluatie van de invoer is.</span><span class="sxs-lookup"><span data-stu-id="daa50-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="daa50-584">Bijvoorbeeld, kunt u Hallo opstellen actie toomerge uitvoerwaarden van meerdere acties:</span><span class="sxs-lookup"><span data-stu-id="daa50-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="daa50-585">Hallo **opstellen** actie gebruikte tooconstruct uitvoer, met inbegrip van objecten, matrices en een ander type systeemeigen worden ondersteund door logische apps zoals XML en binaire kan zijn.</span><span class="sxs-lookup"><span data-stu-id="daa50-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="daa50-586">Tabel actie</span><span class="sxs-lookup"><span data-stu-id="daa50-586">Table action</span></span>

<span data-ttu-id="daa50-587">Hallo `table` kunt u tooconvert een matrix van items in een **CSV** of **HTML** tabel.</span><span class="sxs-lookup"><span data-stu-id="daa50-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="daa50-588">Stel @triggerBody() is</span><span class="sxs-lookup"><span data-stu-id="daa50-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="daa50-589">En laat Hallo actie worden gedefinieerd als</span><span class="sxs-lookup"><span data-stu-id="daa50-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="daa50-590">Hallo bovenstaande geeft als resultaat</span><span class="sxs-lookup"><span data-stu-id="daa50-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="daa50-591">id</span><span class="sxs-lookup"><span data-stu-id="daa50-591">id</span></span></th><th><span data-ttu-id="daa50-592">naam</span><span class="sxs-lookup"><span data-stu-id="daa50-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="daa50-593">0</span><span class="sxs-lookup"><span data-stu-id="daa50-593">0</span></span></td><td><span data-ttu-id="daa50-594">appels</span><span class="sxs-lookup"><span data-stu-id="daa50-594">apples</span></span></td></tr><tr><td><span data-ttu-id="daa50-595">1</span><span class="sxs-lookup"><span data-stu-id="daa50-595">1</span></span></td><td><span data-ttu-id="daa50-596">appels</span><span class="sxs-lookup"><span data-stu-id="daa50-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="daa50-597">"</span><span class="sxs-lookup"><span data-stu-id="daa50-597">"</span></span>

<span data-ttu-id="daa50-598">In de volgorde toocustomize Hallo tabel kunt u expliciet Hallo kolommen opgeven.</span><span class="sxs-lookup"><span data-stu-id="daa50-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="daa50-599">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="daa50-599">For example:</span></span>

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

<span data-ttu-id="daa50-600">Hallo bovenstaande geeft als resultaat</span><span class="sxs-lookup"><span data-stu-id="daa50-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="daa50-601">id maken</span><span class="sxs-lookup"><span data-stu-id="daa50-601">produce id</span></span></th><th><span data-ttu-id="daa50-602">description</span><span class="sxs-lookup"><span data-stu-id="daa50-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="daa50-603">0</span><span class="sxs-lookup"><span data-stu-id="daa50-603">0</span></span></td><td><span data-ttu-id="daa50-604">nieuwe appels</span><span class="sxs-lookup"><span data-stu-id="daa50-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="daa50-605">1</span><span class="sxs-lookup"><span data-stu-id="daa50-605">1</span></span></td><td><span data-ttu-id="daa50-606">nieuwe appels</span><span class="sxs-lookup"><span data-stu-id="daa50-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="daa50-607">"</span><span class="sxs-lookup"><span data-stu-id="daa50-607">"</span></span>

<span data-ttu-id="daa50-608">Als hello `from` eigenschapswaarde is een lege matrix, Hallo uitvoer is een lege tabel.</span><span class="sxs-lookup"><span data-stu-id="daa50-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="daa50-609">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-609">Name</span></span>|<span data-ttu-id="daa50-610">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-610">Required</span></span>|<span data-ttu-id="daa50-611">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-611">Type</span></span>|<span data-ttu-id="daa50-612">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="daa50-613">Van</span><span class="sxs-lookup"><span data-stu-id="daa50-613">from</span></span>|<span data-ttu-id="daa50-614">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-614">Yes</span></span>|<span data-ttu-id="daa50-615">Matrix</span><span class="sxs-lookup"><span data-stu-id="daa50-615">Array</span></span>|<span data-ttu-id="daa50-616">Hallo bronmatrix.</span><span class="sxs-lookup"><span data-stu-id="daa50-616">hello source array.</span></span>|
|<span data-ttu-id="daa50-617">Indeling</span><span class="sxs-lookup"><span data-stu-id="daa50-617">format</span></span>|<span data-ttu-id="daa50-618">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-618">Yes</span></span>|<span data-ttu-id="daa50-619">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-619">String</span></span>|<span data-ttu-id="daa50-620">Hallo-indeling, ofwel **CSV** of **HTML**.</span><span class="sxs-lookup"><span data-stu-id="daa50-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="daa50-621">Kolommen</span><span class="sxs-lookup"><span data-stu-id="daa50-621">columns</span></span>|<span data-ttu-id="daa50-622">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-622">No</span></span>|<span data-ttu-id="daa50-623">Matrix</span><span class="sxs-lookup"><span data-stu-id="daa50-623">Array</span></span>|<span data-ttu-id="daa50-624">Hallo-kolommen.</span><span class="sxs-lookup"><span data-stu-id="daa50-624">hello columns.</span></span> <span data-ttu-id="daa50-625">Hiermee kunt toooverride Hallo standaardvorm van Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="daa50-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="daa50-626">kolomkop</span><span class="sxs-lookup"><span data-stu-id="daa50-626">column header</span></span>|<span data-ttu-id="daa50-627">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-627">No</span></span>|<span data-ttu-id="daa50-628">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-628">String</span></span>|<span data-ttu-id="daa50-629">Hallo-header van Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="daa50-629">hello header of hello column.</span></span>|
|<span data-ttu-id="daa50-630">waarde in de kolom</span><span class="sxs-lookup"><span data-stu-id="daa50-630">column value</span></span>|<span data-ttu-id="daa50-631">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-631">Yes</span></span>|<span data-ttu-id="daa50-632">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-632">String</span></span>|<span data-ttu-id="daa50-633">Hallo-waarde van Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="daa50-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="daa50-634">Werkstroomactie</span><span class="sxs-lookup"><span data-stu-id="daa50-634">Workflow action</span></span>   

|<span data-ttu-id="daa50-635">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-635">Name</span></span>|<span data-ttu-id="daa50-636">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-636">Required</span></span>|<span data-ttu-id="daa50-637">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-637">Type</span></span>|<span data-ttu-id="daa50-638">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-639">host-id</span><span class="sxs-lookup"><span data-stu-id="daa50-639">host id</span></span>|<span data-ttu-id="daa50-640">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-640">Yes</span></span>|<span data-ttu-id="daa50-641">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-641">String</span></span>|<span data-ttu-id="daa50-642">Hallo-bron-ID van dat u wilt dat toocall Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="daa50-643">host triggernaam</span><span class="sxs-lookup"><span data-stu-id="daa50-643">host triggerName</span></span>|<span data-ttu-id="daa50-644">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-644">Yes</span></span>|<span data-ttu-id="daa50-645">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-645">String</span></span>|<span data-ttu-id="daa50-646">Hallo-naam van dat u wilt dat tooinvoke Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="daa50-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="daa50-647">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-647">queries</span></span>|<span data-ttu-id="daa50-648">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-648">No</span></span>|<span data-ttu-id="daa50-649">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-649">Object</span></span>|<span data-ttu-id="daa50-650">Hallo query parameters tooadd toohello URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="daa50-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="daa50-651">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="daa50-652">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-652">headers</span></span>|<span data-ttu-id="daa50-653">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-653">No</span></span>|<span data-ttu-id="daa50-654">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-654">Object</span></span>|<span data-ttu-id="daa50-655">Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-656">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="daa50-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="daa50-657">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-657">body</span></span>|<span data-ttu-id="daa50-658">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-658">No</span></span>|<span data-ttu-id="daa50-659">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-659">Object</span></span>|<span data-ttu-id="daa50-660">Hiermee geeft u Hallo nettolading toohello eindpunt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="daa50-661">Een toegangscontrole wordt gemaakt op Hallo werkstroom \(meer specifiek, Hallo trigger\), wat betekent dat u moet toegang tot toohello werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="daa50-662">Hallo levert van Hallo `workflow` actie zijn gebaseerd op wat u hebt gedefinieerd in Hallo `response` actie in Hallo onderliggende werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="daa50-663">Als u nog geen gedefinieerd een `response` actie en klik vervolgens Hallo uitvoer leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="daa50-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="daa50-664">Functie actie</span><span class="sxs-lookup"><span data-stu-id="daa50-664">Function action</span></span>   

|<span data-ttu-id="daa50-665">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-665">Name</span></span>|<span data-ttu-id="daa50-666">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-666">Required</span></span>|<span data-ttu-id="daa50-667">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-667">Type</span></span>|<span data-ttu-id="daa50-668">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-669">functie-id</span><span class="sxs-lookup"><span data-stu-id="daa50-669">function id</span></span>|<span data-ttu-id="daa50-670">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-670">Yes</span></span>|<span data-ttu-id="daa50-671">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-671">String</span></span>|<span data-ttu-id="daa50-672">Hallo resource-ID van de gewenste tooinvoke Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="daa50-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="daa50-673">Methode</span><span class="sxs-lookup"><span data-stu-id="daa50-673">method</span></span>|<span data-ttu-id="daa50-674">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-674">No</span></span>|<span data-ttu-id="daa50-675">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-675">String</span></span>|<span data-ttu-id="daa50-676">Hallo HTTP-methode tooinvoke Hallo functie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="daa50-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="daa50-677">Dit is standaard `POST` als niet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="daa50-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="daa50-678">Query 's</span><span class="sxs-lookup"><span data-stu-id="daa50-678">queries</span></span>|<span data-ttu-id="daa50-679">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-679">No</span></span>|<span data-ttu-id="daa50-680">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-680">Object</span></span>|<span data-ttu-id="daa50-681">Hallo query parameters tooadd toohello URL vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="daa50-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="daa50-682">Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="daa50-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="daa50-683">Headers</span><span class="sxs-lookup"><span data-stu-id="daa50-683">headers</span></span>|<span data-ttu-id="daa50-684">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-684">No</span></span>|<span data-ttu-id="daa50-685">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-685">Object</span></span>|<span data-ttu-id="daa50-686">Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="daa50-687">Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="daa50-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="daa50-688">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="daa50-688">body</span></span>|<span data-ttu-id="daa50-689">Nee</span><span class="sxs-lookup"><span data-stu-id="daa50-689">No</span></span>|<span data-ttu-id="daa50-690">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-690">Object</span></span>|<span data-ttu-id="daa50-691">Hiermee geeft u Hallo nettolading toohello eindpunt verzonden.</span><span class="sxs-lookup"><span data-stu-id="daa50-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="daa50-692">Wanneer u Hallo logische app opslaat, voer we enkele controles van de functie Hallo waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="daa50-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="daa50-693">U moet de functie voor toegang tot toohello toohave.</span><span class="sxs-lookup"><span data-stu-id="daa50-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="daa50-694">Alleen de standaard HTTP-trigger of algemene JSON webhook trigger is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="daa50-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="daa50-695">Er mogen geen enkele route gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="daa50-696">Alleen 'functioneren' en 'anonymous' autorisatieniveau is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="daa50-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="daa50-697">Hallo trigger-URL is opgehaald, in de cache opgeslagen en gebruikt tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="daa50-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="daa50-698">Dus als een bewerking wordt ongeldig in de cache opgeslagen Hallo-URL gemaakt, mislukt de Hallo actie tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="daa50-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="daa50-699">toowork dit, Hallo logische app opnieuw, waarmee u logic app tooretrieve veroorzaken en Hallo trigger URL opnieuw in de cache opslaan.</span><span class="sxs-lookup"><span data-stu-id="daa50-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="daa50-700">Verzameling acties (bereiken en lussen)</span><span class="sxs-lookup"><span data-stu-id="daa50-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="daa50-701">Sommige actietypen kunnen acties in zichzelf bevatten.</span><span class="sxs-lookup"><span data-stu-id="daa50-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="daa50-702">Verwijzing acties binnen een verzameling kunnen worden verwezen rechtstreeks buiten Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="daa50-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="daa50-703">Als u hebt gedefinieerd `http` in een bereik `@body('http')` nog geldig overal in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="daa50-704">Acties binnen een verzameling kunnen `runAfter` alleen andere acties in Hallo dezelfde verzameling.</span><span class="sxs-lookup"><span data-stu-id="daa50-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="daa50-705">Bereikactie</span><span class="sxs-lookup"><span data-stu-id="daa50-705">Scope action</span></span>

<span data-ttu-id="daa50-706">Hallo `scope` actie kunt u logische groep acties in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="daa50-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="daa50-707">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-707">Name</span></span>|<span data-ttu-id="daa50-708">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-708">Required</span></span>|<span data-ttu-id="daa50-709">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-709">Type</span></span>|<span data-ttu-id="daa50-710">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-711">acties</span><span class="sxs-lookup"><span data-stu-id="daa50-711">actions</span></span>|<span data-ttu-id="daa50-712">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-712">Yes</span></span>|<span data-ttu-id="daa50-713">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-713">Object</span></span>|<span data-ttu-id="daa50-714">Interne acties tooexecute binnen Hallo bereik</span><span class="sxs-lookup"><span data-stu-id="daa50-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="daa50-715">ForEach-actie</span><span class="sxs-lookup"><span data-stu-id="daa50-715">ForEach action</span></span>

<span data-ttu-id="daa50-716">Deze actie samenvoegartikel een matrix doorlopen en interne acties uitvoert voor elk item.</span><span class="sxs-lookup"><span data-stu-id="daa50-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="daa50-717">Hallo foreach lus wordt standaard uitgevoerd parallel (20 uitvoeringen parallel tegelijk).</span><span class="sxs-lookup"><span data-stu-id="daa50-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="daa50-718">U kunt uitvoering regels met behulp van Hallo instellen `operationOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="daa50-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="daa50-719">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-719">Name</span></span>|<span data-ttu-id="daa50-720">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-720">Required</span></span>|<span data-ttu-id="daa50-721">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-721">Type</span></span>|<span data-ttu-id="daa50-722">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-723">acties</span><span class="sxs-lookup"><span data-stu-id="daa50-723">actions</span></span>|<span data-ttu-id="daa50-724">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-724">Yes</span></span>|<span data-ttu-id="daa50-725">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-725">Object</span></span>|<span data-ttu-id="daa50-726">Interne acties tooexecute binnen de lus Hallo</span><span class="sxs-lookup"><span data-stu-id="daa50-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="daa50-727">foreach</span><span class="sxs-lookup"><span data-stu-id="daa50-727">foreach</span></span>|<span data-ttu-id="daa50-728">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-728">Yes</span></span>|<span data-ttu-id="daa50-729">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-729">string</span></span>|<span data-ttu-id="daa50-730">Hallo matrix tooiterate via</span><span class="sxs-lookup"><span data-stu-id="daa50-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="daa50-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="daa50-731">operationOptions</span></span>|<span data-ttu-id="daa50-732">Er is geen</span><span class="sxs-lookup"><span data-stu-id="daa50-732">no</span></span>|<span data-ttu-id="daa50-733">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-733">string</span></span>|<span data-ttu-id="daa50-734">Bewerking opties voor het gedrag.</span><span class="sxs-lookup"><span data-stu-id="daa50-734">Any operation options for behavior.</span></span> <span data-ttu-id="daa50-735">Momenteel ondersteunt alleen `sequential` tooexecute iteraties sequentieel (standaardgedrag is parallelle)</span><span class="sxs-lookup"><span data-stu-id="daa50-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="daa50-736">Totdat de actie</span><span class="sxs-lookup"><span data-stu-id="daa50-736">Until action</span></span>

<span data-ttu-id="daa50-737">Deze samenvoegartikel actie uitgevoerd binnenste acties totdat een voorwaarde tootrue resulteert.</span><span class="sxs-lookup"><span data-stu-id="daa50-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="daa50-738">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-738">Name</span></span>|<span data-ttu-id="daa50-739">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-739">Required</span></span>|<span data-ttu-id="daa50-740">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-740">Type</span></span>|<span data-ttu-id="daa50-741">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-742">acties</span><span class="sxs-lookup"><span data-stu-id="daa50-742">actions</span></span>|<span data-ttu-id="daa50-743">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-743">Yes</span></span>|<span data-ttu-id="daa50-744">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-744">Object</span></span>|<span data-ttu-id="daa50-745">Interne acties tooexecute binnen de lus Hallo</span><span class="sxs-lookup"><span data-stu-id="daa50-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="daa50-746">expressie</span><span class="sxs-lookup"><span data-stu-id="daa50-746">expression</span></span>|<span data-ttu-id="daa50-747">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-747">Yes</span></span>|<span data-ttu-id="daa50-748">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-748">string</span></span>|<span data-ttu-id="daa50-749">Hallo expressie tooevaluate na elke iteratie</span><span class="sxs-lookup"><span data-stu-id="daa50-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="daa50-750">Limiet</span><span class="sxs-lookup"><span data-stu-id="daa50-750">limit</span></span>|<span data-ttu-id="daa50-751">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-751">yes</span></span>|<span data-ttu-id="daa50-752">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-752">Object</span></span>|<span data-ttu-id="daa50-753">Hallo-limieten voor het Hallo-lus - ten minste één limiet moeten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="daa50-754">Aantal</span><span class="sxs-lookup"><span data-stu-id="daa50-754">count</span></span>|<span data-ttu-id="daa50-755">Er is geen</span><span class="sxs-lookup"><span data-stu-id="daa50-755">no</span></span>|<span data-ttu-id="daa50-756">int</span><span class="sxs-lookup"><span data-stu-id="daa50-756">int</span></span>|<span data-ttu-id="daa50-757">Hallo limiet toohello aantal iteraties die kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="daa50-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="daa50-758">timeout</span><span class="sxs-lookup"><span data-stu-id="daa50-758">timeout</span></span>|<span data-ttu-id="daa50-759">Er is geen</span><span class="sxs-lookup"><span data-stu-id="daa50-759">no</span></span>|<span data-ttu-id="daa50-760">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-760">string</span></span>|<span data-ttu-id="daa50-761">Hallo-out voor hoe lang deze moet worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="daa50-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="daa50-762">ISO 8601-notatie</span><span class="sxs-lookup"><span data-stu-id="daa50-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="daa50-763">Voorwaarden - als actie</span><span class="sxs-lookup"><span data-stu-id="daa50-763">Conditions - If Action</span></span>

<span data-ttu-id="daa50-764">Hallo `If` actie kunt u een voorwaarde evalueren en uitvoeren van een vertakking op basis van of Hallo expressie wordt geëvalueerd te`true`.</span><span class="sxs-lookup"><span data-stu-id="daa50-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="daa50-765">Naam</span><span class="sxs-lookup"><span data-stu-id="daa50-765">Name</span></span>|<span data-ttu-id="daa50-766">Vereist</span><span class="sxs-lookup"><span data-stu-id="daa50-766">Required</span></span>|<span data-ttu-id="daa50-767">Type</span><span class="sxs-lookup"><span data-stu-id="daa50-767">Type</span></span>|<span data-ttu-id="daa50-768">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="daa50-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="daa50-769">acties</span><span class="sxs-lookup"><span data-stu-id="daa50-769">actions</span></span>|<span data-ttu-id="daa50-770">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-770">Yes</span></span>|<span data-ttu-id="daa50-771">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-771">Object</span></span>|<span data-ttu-id="daa50-772">Interne acties tooexecute wanneer expressie te evalueert.`true`</span><span class="sxs-lookup"><span data-stu-id="daa50-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="daa50-773">expressie</span><span class="sxs-lookup"><span data-stu-id="daa50-773">expression</span></span>|<span data-ttu-id="daa50-774">Ja</span><span class="sxs-lookup"><span data-stu-id="daa50-774">Yes</span></span>|<span data-ttu-id="daa50-775">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="daa50-775">string</span></span>|<span data-ttu-id="daa50-776">Hallo expressie tooevaluate</span><span class="sxs-lookup"><span data-stu-id="daa50-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="daa50-777">anders</span><span class="sxs-lookup"><span data-stu-id="daa50-777">else</span></span>|<span data-ttu-id="daa50-778">Er is geen</span><span class="sxs-lookup"><span data-stu-id="daa50-778">no</span></span>|<span data-ttu-id="daa50-779">Object</span><span class="sxs-lookup"><span data-stu-id="daa50-779">Object</span></span>|<span data-ttu-id="daa50-780">Interne acties tooexecute wanneer expressie te evalueert.`false`</span><span class="sxs-lookup"><span data-stu-id="daa50-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="daa50-781">Hallo ziet volgende tabel u voorbeelden van hoe voorwaarden expressies in een actie kunnen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="daa50-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="daa50-782">JSON-waarde</span><span class="sxs-lookup"><span data-stu-id="daa50-782">JSON value</span></span>|<span data-ttu-id="daa50-783">Resultaat</span><span class="sxs-lookup"><span data-stu-id="daa50-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="daa50-784">De waarde die tootrue evalueren verbindingspogingen wordt deze voorwaarde toopass.</span><span class="sxs-lookup"><span data-stu-id="daa50-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="daa50-785">Alleen Booleaanse expressies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="daa50-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="daa50-786">tooconvert andere typen tooBoolean, gebruik functies `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="daa50-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="daa50-787">Vergelijking van functies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="daa50-787">Comparison functions are supported.</span></span> <span data-ttu-id="daa50-788">Hallo bijvoorbeeld hier Hallo handeling alleen uitgevoerd wanneer het Hallo-uitvoer van act1 is groter dan de drempelwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="daa50-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="daa50-789">Bedrijfslogica-functies zijn ook ondersteunde toocreate genest Booleaanse expressies.</span><span class="sxs-lookup"><span data-stu-id="daa50-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="daa50-790">In dit geval Hallo actie worden uitgevoerd wanneer het Hallo-uitvoer van act1 is hoger dan drempelwaarde Hallo of onder de 100.</span><span class="sxs-lookup"><span data-stu-id="daa50-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="daa50-791">U kunt matrix functies toocheck gebruiken als een matrix alle items heeft.</span><span class="sxs-lookup"><span data-stu-id="daa50-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="daa50-792">In dit geval Hallo actie worden uitgevoerd wanneer Hallo fouten matrix leeg is.</span><span class="sxs-lookup"><span data-stu-id="daa50-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="daa50-793">Fout: geen geldige voorwaarde omdat @ is vereist voor voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="daa50-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="daa50-794">Als een voorwaarde is geëvalueerd, Hallo-voorwaarde is gemarkeerd als `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="daa50-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="daa50-795">Acties in beide Hallo `actions` of `else` objecten te evalueren`Succeeded` wanneer die wordt uitgevoerd en is voltooid, `Failed` wanneer die wordt uitgevoerd en is mislukt, of `Skipped` wanneer dat filiaal niet is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="daa50-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa50-796">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="daa50-796">Next steps</span></span>

[<span data-ttu-id="daa50-797">REST-API van workflow</span><span class="sxs-lookup"><span data-stu-id="daa50-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
