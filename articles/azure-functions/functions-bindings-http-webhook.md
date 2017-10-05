---
title: Azure Functions HTTP- en webhook bindingen | Microsoft Docs
description: Het gebruik van HTTP- en webhook triggers en bindingen in de Azure Functions begrijpen.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, gebeurtenis verwerking, webhooks, dynamische Reken-, zonder server-architectuur, HTTP-API, REST
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="5c20f-104">Azure Functions HTTP- en webhook bindingen</span><span class="sxs-lookup"><span data-stu-id="5c20f-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5c20f-105">In dit artikel wordt uitgelegd hoe configureren en werken met HTTP-triggers en bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5c20f-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="5c20f-106">Met deze, kunt u Azure Functions te bouwen zonder Server API's en reageren op webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="5c20f-107">Azure Functions bevat de volgende bindingen:</span><span class="sxs-lookup"><span data-stu-id="5c20f-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="5c20f-108">Een [HTTP-trigger](#httptrigger) kunt u een functie met een HTTP-aanvraag worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="5c20f-109">Dit kan worden aangepast om te reageren op [webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="5c20f-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="5c20f-110">Een [HTTP uitvoer binding](#output) kunt u om te reageren op de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="5c20f-111">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="5c20f-111">HTTP trigger</span></span>
<span data-ttu-id="5c20f-112">De HTTP-trigger wordt de functie worden uitgevoerd in reactie op een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="5c20f-113">U kunt aanpassen om te reageren op een bepaalde URL of set HTTP-methoden.</span><span class="sxs-lookup"><span data-stu-id="5c20f-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="5c20f-114">Een HTTP-trigger kan ook worden geconfigureerd om te reageren op webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="5c20f-115">Als u de functies portal gebruikt, u kunt ook aan de slag meteen met een vooraf gemaakte sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5c20f-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="5c20f-116">Selecteer **nieuwe functie** en kiest u 'API & Webhooks' in de **Scenario** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5c20f-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="5c20f-117">Selecteer een van de sjablonen en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="5c20f-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="5c20f-118">Standaard reageert een HTTP-trigger op de aanvraag met een HTTP 200 OK-statuscode en een lege hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="5c20f-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="5c20f-119">Configureren voor het wijzigen van het antwoord een [HTTP uitvoer binding](#output)</span><span class="sxs-lookup"><span data-stu-id="5c20f-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="5c20f-120">Configureren van een HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="5c20f-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="5c20f-121">Een HTTP-trigger is gedefinieerd door een vergelijkbaar met het volgende in JSON-object, waaronder de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="5c20f-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="5c20f-122">De binding ondersteunt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5c20f-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="5c20f-123">**naam** : is vereist: de naam van de variabele in functiecode gebruikt voor de aanvraag of de hoofdtekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="5c20f-124">Zie [werken met een HTTP-trigger vanuit code](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="5c20f-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="5c20f-125">**type** : vereist - moet worden ingesteld op 'httpTrigger'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="5c20f-126">**richting** : vereist - moet worden ingesteld op 'in'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="5c20f-127">_authLevel_ : Hiermee bepaalt u wat sleutels, indien van toepassing, aanwezig zijn op de aanvraag moeten om de functie aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="5c20f-128">Zie [werken met sleutels](#keys) hieronder.</span><span class="sxs-lookup"><span data-stu-id="5c20f-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="5c20f-129">De waarde kan een van de volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="5c20f-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="5c20f-130">_anonieme_: Er is geen API-sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="5c20f-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="5c20f-131">_de functie_: een functiespecifieke API-sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="5c20f-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="5c20f-132">Dit is de standaardwaarde als niets wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c20f-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="5c20f-133">_beheerder_ : de hoofdsleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="5c20f-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="5c20f-134">**methoden** : dit is een matrix met de HTTP-methoden waarop de functie wordt reageren.</span><span class="sxs-lookup"><span data-stu-id="5c20f-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="5c20f-135">Als niet wordt opgegeven, wordt de functie reageren op alle HTTP-methoden.</span><span class="sxs-lookup"><span data-stu-id="5c20f-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="5c20f-136">Zie [aanpassen van het HTTP-eindpunt](#url).</span><span class="sxs-lookup"><span data-stu-id="5c20f-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="5c20f-137">**route** : Hiermee definieert u de Routesjabloon, waarmee aanvragen URL's beheren de functie reageert.</span><span class="sxs-lookup"><span data-stu-id="5c20f-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="5c20f-138">De standaardwaarde als niets wordt opgegeven is `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="5c20f-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="5c20f-139">Zie [aanpassen van het HTTP-eindpunt](#url).</span><span class="sxs-lookup"><span data-stu-id="5c20f-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="5c20f-140">**webHookType** : Hiermee configureert u de HTTP-trigger om te fungeren als een webhook reciever voor de opgegeven provider.</span><span class="sxs-lookup"><span data-stu-id="5c20f-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="5c20f-141">De _methoden_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="5c20f-142">Zie [reageert op webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="5c20f-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="5c20f-143">De waarde kan een van de volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="5c20f-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="5c20f-144">_genericJson_ : een eindpunt van de webhook algemeen zonder logica voor een specifieke provider.</span><span class="sxs-lookup"><span data-stu-id="5c20f-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="5c20f-145">_github_ : de functie reageert op GitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="5c20f-146">De _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="5c20f-147">_vertraging_ : de functie reageert op toegestane webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="5c20f-148">De _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="5c20f-149">Werken met een HTTP-trigger van code</span><span class="sxs-lookup"><span data-stu-id="5c20f-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="5c20f-150">Voor C# en F #, kunt u het type van de invoer voor deze trigger declareren `HttpRequestMessage` of een aangepast type.</span><span class="sxs-lookup"><span data-stu-id="5c20f-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="5c20f-151">Als u ervoor kiest `HttpRequestMessage`, en vervolgens u volledige toegang tot het request-object krijgt.</span><span class="sxs-lookup"><span data-stu-id="5c20f-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="5c20f-152">Voor een aangepast type (zoals een POCO) probeert functies de aanvraagtekst parseren als JSON om de objecteigenschappen te vullen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="5c20f-153">De runtime van Functions biedt voor Node.js-functies, de aanvraagtekst in plaats van het request-object.</span><span class="sxs-lookup"><span data-stu-id="5c20f-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="5c20f-154">Zie [voorbeelden van HTTP-trigger](#httptriggersample) bijvoorbeeld gebruik.</span><span class="sxs-lookup"><span data-stu-id="5c20f-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="5c20f-155">Binding voor de HTTP-antwoord van de uitvoer</span><span class="sxs-lookup"><span data-stu-id="5c20f-155">HTTP response output binding</span></span>
<span data-ttu-id="5c20f-156">Gebruik de uitvoer van de HTTP-binding om te reageren op de afzender van HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="5c20f-157">Deze binding vereist een HTTP-trigger en Hiermee kunt u het antwoord is gekoppeld aan de aanvraag van de trigger aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="5c20f-158">Als een HTTP-uitvoer binding is niet opgegeven, wordt een HTTP-trigger HTTP 200 OK wordt geretourneerd met een lege hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="5c20f-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="5c20f-159">Binding uitvoer voor het configureren van een HTTP</span><span class="sxs-lookup"><span data-stu-id="5c20f-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="5c20f-160">De HTTP uitvoer binding wordt gedefinieerd door een vergelijkbaar met het volgende in JSON-object, waaronder de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="5c20f-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="5c20f-161">De binding bevat de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5c20f-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="5c20f-162">**naam** : is vereist: de naam van de variabele in functiecode gebruikt voor het antwoord.</span><span class="sxs-lookup"><span data-stu-id="5c20f-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="5c20f-163">Zie [werken met een HTTP-uitvoer binding vanuit code](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="5c20f-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="5c20f-164">**type** : vereist - moet worden ingesteld op 'http'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="5c20f-165">**richting** : vereist - moet worden ingesteld op 'out'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="5c20f-166">Werken met een HTTP-uitvoer binding van code</span><span class="sxs-lookup"><span data-stu-id="5c20f-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="5c20f-167">U kunt de output-parameter (bijvoorbeeld ' res') om te reageren op de aanroeper HTTP- of webhook gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5c20f-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="5c20f-168">U kunt ook kunt u de standaard `Request.CreateResponse()` (C#) of `context.res` (Node.JS) patroon uw antwoord retourneren.</span><span class="sxs-lookup"><span data-stu-id="5c20f-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="5c20f-169">Zie voor voorbeelden voor het gebruik van de laatste methode [voorbeelden van HTTP-trigger](#httptriggersample) en [Webhook trigger voorbeelden](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="5c20f-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="5c20f-170">Reageren op webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-170">Responding to webhooks</span></span>
<span data-ttu-id="5c20f-171">Een HTTP-trigger met de _webHookType_ eigenschap worden geconfigureerd om te reageren op [webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="5c20f-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="5c20f-172">De instelling 'genericJson' maakt gebruik van de basisconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="5c20f-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="5c20f-173">Hiermee beperkt u aanvragen tot alleen degenen met behulp van HTTP POST en met de `application/json` inhoudstype.</span><span class="sxs-lookup"><span data-stu-id="5c20f-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="5c20f-174">De trigger kan ook worden aangepast aan een specifieke webhook-provider (bijv, [GitHub](https://developer.github.com/webhooks/) en [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="5c20f-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="5c20f-175">Als een provider is opgegeven, kan de runtime van Functions behandelen validatielogica van de provider voor u.</span><span class="sxs-lookup"><span data-stu-id="5c20f-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="5c20f-176">GitHub als een webhook-provider configureren</span><span class="sxs-lookup"><span data-stu-id="5c20f-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="5c20f-177">Om te reageren op GitHub webhooks, eerst uw functie te maken met een HTTP-Trigger en stel de _webHookType_ eigenschap in op 'github'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="5c20f-178">Kopieer de [URL](#url) en [API-sleutel](#keys) in uw GitHub-opslagplaats **webhook toevoegen** pagina.</span><span class="sxs-lookup"><span data-stu-id="5c20f-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="5c20f-179">Zie de GitHub [Webhooks maken](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5c20f-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="5c20f-180">Vertraging configureren als een webhook-provider</span><span class="sxs-lookup"><span data-stu-id="5c20f-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="5c20f-181">De toegestane webhook genereert een token voor u in plaats van waarin u kunt opgeven, dus u een sleutel functiespecifieke met het token van de toegestane vertraging configureren moet.</span><span class="sxs-lookup"><span data-stu-id="5c20f-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="5c20f-182">Zie [werken met sleutels](#keys).</span><span class="sxs-lookup"><span data-stu-id="5c20f-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="5c20f-183">Het HTTP-eindpunt aanpassen</span><span class="sxs-lookup"><span data-stu-id="5c20f-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="5c20f-184">Wanneer u een functie voor een HTTP-trigger of WebHook, is de functie standaard adresseerbare met een route van het formulier:</span><span class="sxs-lookup"><span data-stu-id="5c20f-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="5c20f-185">U kunt deze route met de optionele `route` eigenschap voor de HTTP-trigger binding de invoer.</span><span class="sxs-lookup"><span data-stu-id="5c20f-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="5c20f-186">Als u bijvoorbeeld de volgende *function.json* -bestand definieert een `route` eigenschap voor een HTTP-trigger:</span><span class="sxs-lookup"><span data-stu-id="5c20f-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="5c20f-187">Met behulp van deze configuratie de functie is nu adresseerbare met de volgende route in plaats van de oorspronkelijke route.</span><span class="sxs-lookup"><span data-stu-id="5c20f-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="5c20f-188">Hierdoor kan de functiecode ter ondersteuning van twee parameters in het adres, 'categorie' en 'id'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="5c20f-189">U kunt een [Web API Route beperking](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) met de parameters.</span><span class="sxs-lookup"><span data-stu-id="5c20f-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="5c20f-190">De volgende C#-functiecode maakt gebruik van beide parameters.</span><span class="sxs-lookup"><span data-stu-id="5c20f-190">The following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="5c20f-191">Hier volgt een Node.js-code voor de functie dezelfde Routeparameters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5c20f-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="5c20f-192">Standaard worden alle routes van de functie voorafgegaan door *api*.</span><span class="sxs-lookup"><span data-stu-id="5c20f-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="5c20f-193">U kunt ook aanpassen of verwijderen van het voorvoegsel met behulp van de `http.routePrefix` eigenschap in uw *host.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="5c20f-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="5c20f-194">Het volgende voorbeeld verwijdert u de *api* routeprefix met behulp van een lege tekenreeks voor het voorvoegsel op in de *host.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="5c20f-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="5c20f-195">Voor gedetailleerde informatie over het bijwerken van de *host.json* -bestand voor de functie, Zie [het bijwerken van de functie app-bestanden](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="5c20f-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="5c20f-196">Voor informatie over andere eigenschappen kunt u configureren uw *host.json* bestand, Zie [host.json verwijzing](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="5c20f-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="5c20f-197">Werken met sleutels</span><span class="sxs-lookup"><span data-stu-id="5c20f-197">Working with keys</span></span>
<span data-ttu-id="5c20f-198">HttpTriggers kunt gebruikmaken van sleutels voor extra beveiliging.</span><span class="sxs-lookup"><span data-stu-id="5c20f-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="5c20f-199">Een standaard HttpTrigger kunt deze als een API-sleutel gebruiken voor het vereisen van de sleutel moet aanwezig zijn op de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="5c20f-200">Webhooks kunt sleutels gebruiken voor het toestaan van aanvragen in verschillende manieren, afhankelijk van wat de provider ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="5c20f-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="5c20f-201">Sleutels worden opgeslagen als onderdeel van de functie-app in Azure en zijn versleuteld in rust.</span><span class="sxs-lookup"><span data-stu-id="5c20f-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="5c20f-202">Als u wilt uw sleutels weergeven, nieuwe te maken of sleutels rouleert met nieuwe waarden, navigeer naar een van uw functies in de portal en selecteer 'Beheren'.</span><span class="sxs-lookup"><span data-stu-id="5c20f-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="5c20f-203">Er zijn twee soorten sleutels:</span><span class="sxs-lookup"><span data-stu-id="5c20f-203">There are two types of keys:</span></span>
- <span data-ttu-id="5c20f-204">**Hostsleutels**: deze sleutels worden gedeeld door alle functies in de functie-app.</span><span class="sxs-lookup"><span data-stu-id="5c20f-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="5c20f-205">Wanneer als een API-sleutel gebruikt, kunnen toegang tot een functie binnen de functie-app.</span><span class="sxs-lookup"><span data-stu-id="5c20f-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="5c20f-206">**Functietoetsen**: deze sleutels alleen van toepassing op de specifieke functies waarin ze zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5c20f-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="5c20f-207">Wanneer als een API-sleutel gebruikt, kan deze alleen toegang tot deze functie.</span><span class="sxs-lookup"><span data-stu-id="5c20f-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="5c20f-208">Elke sleutel met de naam voor de verwijzing en er is een standaard-sleutel (met de naam 'standaard') op het niveau van de functie en de host.</span><span class="sxs-lookup"><span data-stu-id="5c20f-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="5c20f-209">De **hoofdsleutel** een standaard host-sleutel is met de naam '_master' die is gedefinieerd voor elke functie-app en kan niet worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="5c20f-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="5c20f-210">Het biedt beheerderstoegang tot de runtime-API's.</span><span class="sxs-lookup"><span data-stu-id="5c20f-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="5c20f-211">Met behulp van `"authLevel": "admin"` in de binding JSON deze sleutel moeten worden weergegeven in de aanvraag is vereist; een andere toets resulteert in een mislukte verificatiepogingen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="5c20f-212">Vanwege de verhoogde machtigingen verleend door de hoofdsleutel, moet u geen deze sleutel delen met derden of distribueren in systeemeigen clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="5c20f-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="5c20f-213">Wees voorzichtig bij het kiezen van de beheerder autorisatieniveau.</span><span class="sxs-lookup"><span data-stu-id="5c20f-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="5c20f-214">API-sleutel autorisatie</span><span class="sxs-lookup"><span data-stu-id="5c20f-214">API key authorization</span></span>
<span data-ttu-id="5c20f-215">Een HttpTrigger moet standaard een API-sleutel in de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="5c20f-216">Dus de HTTP-aanvraag normaal ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="5c20f-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="5c20f-217">De sleutel kan worden opgenomen in een queryreeks-variabele met de naam `code`, zoals hierboven, of kan worden opgenomen in een `x-functions-key` HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="5c20f-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="5c20f-218">De waarde van de sleutel mag een gedefinieerd voor de functie functietoets of op een host-toets.</span><span class="sxs-lookup"><span data-stu-id="5c20f-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="5c20f-219">U kunt aanvragen zonder sleutels toestaan of opgeven dat de hoofdsleutel moet worden gebruikt door het wijzigen van de `authLevel` eigenschap in de JSON van de binding (Zie [HTTP-trigger](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="5c20f-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="5c20f-220">Sleutels en webhooks.</span><span class="sxs-lookup"><span data-stu-id="5c20f-220">Keys and webhooks</span></span>
<span data-ttu-id="5c20f-221">Webhook autorisatie wordt verwerkt door de webhook reciever component, onderdeel van de HttpTrigger en het mechanisme voor varieert op basis van de webhook-type.</span><span class="sxs-lookup"><span data-stu-id="5c20f-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="5c20f-222">Elke mechanisme komt, maar afhankelijk zijn van een sleutel.</span><span class="sxs-lookup"><span data-stu-id="5c20f-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="5c20f-223">Standaard wordt de sleutel van de functie met de naam 'standaard' worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5c20f-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="5c20f-224">Als u een andere sleutel wordt gebruikt wilt, moet u de webhook-provider voor het verzenden van de naam van de sleutel met de aanvraag in een van de volgende manieren configureren:</span><span class="sxs-lookup"><span data-stu-id="5c20f-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="5c20f-225">**Querytekenreeks**: de provider geeft de naam van de sleutel in de `clientid` querytekenreeksparameter (bijv, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="5c20f-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="5c20f-226">**Aanvraagheader**: de provider geeft de naam van de sleutel in de `x-functions-clientid` header.</span><span class="sxs-lookup"><span data-stu-id="5c20f-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="5c20f-227">Functietoetsen hebben voorrang op de hostsleutels.</span><span class="sxs-lookup"><span data-stu-id="5c20f-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="5c20f-228">Als twee sleutels zijn gedefinieerd met dezelfde naam, kunt u de functie-sleutel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5c20f-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="5c20f-229">Voorbeelden van HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="5c20f-229">HTTP trigger samples</span></span>
<span data-ttu-id="5c20f-230">Stel dat u hebt de volgende HTTP-trigger in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="5c20f-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="5c20f-231">Zie de taalspecifieke-voorbeeldtoepassing die u zoekt een `name` parameter in de query-tekenreeks of de hoofdtekst van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5c20f-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="5c20f-232">C#</span><span class="sxs-lookup"><span data-stu-id="5c20f-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="5c20f-233">F#</span><span class="sxs-lookup"><span data-stu-id="5c20f-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="5c20f-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="5c20f-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="5c20f-235">Voorbeeld van de HTTP-trigger in C#</span><span class="sxs-lookup"><span data-stu-id="5c20f-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="5c20f-236">U kunt ook binden aan een POCO in plaats van `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="5c20f-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="5c20f-237">Dit wordt gehydrateerd uit de hoofdtekst van de aanvraag kan worden geparseerd als JSON.</span><span class="sxs-lookup"><span data-stu-id="5c20f-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="5c20f-238">Op deze manier een type kan worden doorgegeven aan de uitvoer van de HTTP-antwoord binding en dit wordt geretourneerd als de berichttekst antwoord met een statuscode 200.</span><span class="sxs-lookup"><span data-stu-id="5c20f-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="5c20f-239">Voorbeeld van de HTTP-trigger in F #</span><span class="sxs-lookup"><span data-stu-id="5c20f-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="5c20f-240">U moet een `project.json` bestand met NuGet om te verwijzen naar de `FSharp.Interop.Dynamic` en `Dynamitey` assembly's, als volgt:</span><span class="sxs-lookup"><span data-stu-id="5c20f-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="5c20f-241">Dit NuGet wordt gebruikt voor het ophalen van de afhankelijkheden en worden ze in uw script verwijst.</span><span class="sxs-lookup"><span data-stu-id="5c20f-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="5c20f-242">Voorbeeld van de HTTP-trigger in Node.JS</span><span class="sxs-lookup"><span data-stu-id="5c20f-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="5c20f-243">Webhook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="5c20f-243">Webhook samples</span></span>
<span data-ttu-id="5c20f-244">Stel dat u hebt de volgende webhook trigger in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="5c20f-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="5c20f-245">Zie de taalspecifieke-voorbeeldtoepassing die u GitHub probleem opmerkingen registreert.</span><span class="sxs-lookup"><span data-stu-id="5c20f-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="5c20f-246">C#</span><span class="sxs-lookup"><span data-stu-id="5c20f-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="5c20f-247">F#</span><span class="sxs-lookup"><span data-stu-id="5c20f-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="5c20f-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="5c20f-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="5c20f-249">Voorbeeld van de Webhook in C#</span><span class="sxs-lookup"><span data-stu-id="5c20f-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="5c20f-250">Voorbeeld van de Webhook in F #</span><span class="sxs-lookup"><span data-stu-id="5c20f-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="5c20f-251">Voorbeeld van de Webhook in Node.JS</span><span class="sxs-lookup"><span data-stu-id="5c20f-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="5c20f-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c20f-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

