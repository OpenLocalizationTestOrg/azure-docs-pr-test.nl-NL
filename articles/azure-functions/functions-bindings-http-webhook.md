---
title: de HTTP-functies en webhook bindingen aaaAzure | Microsoft Docs
description: Begrijpen hoe toouse HTTP en webhook triggers en bindingen in de Azure Functions.
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
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="31a48-104">Azure Functions HTTP- en webhook bindingen</span><span class="sxs-lookup"><span data-stu-id="31a48-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="31a48-105">Dit artikel wordt uitgelegd hoe tooconfigure en werken met HTTP triggers en bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="31a48-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="31a48-106">Met deze, kunt u Azure Functions toobuild zonder Server-API's en antwoorden toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="31a48-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="31a48-107">Azure Functions bevat Hallo bindingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31a48-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="31a48-108">Een [HTTP-trigger](#httptrigger) kunt u een functie met een HTTP-aanvraag worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="31a48-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="31a48-109">Dit kan aangepaste toorespond te zijn[webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="31a48-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="31a48-110">Een [HTTP uitvoer binding](#output) kunt u toorespond toohello aanvraag.</span><span class="sxs-lookup"><span data-stu-id="31a48-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="31a48-111">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="31a48-111">HTTP trigger</span></span>
<span data-ttu-id="31a48-112">Hallo HTTP-trigger wordt de functie uitgevoerd in reactie tooan HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="31a48-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="31a48-113">U kunt deze aanpassen toorespond tooa bepaalde URL of een set HTTP-methoden.</span><span class="sxs-lookup"><span data-stu-id="31a48-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="31a48-114">Een HTTP-trigger kan ook worden geconfigureerd toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="31a48-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="31a48-115">Als u Hallo functies portal gebruikt, u kunt ook aan de slag meteen met een vooraf gemaakte sjabloon.</span><span class="sxs-lookup"><span data-stu-id="31a48-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="31a48-116">Selecteer **nieuwe functie** en kiest u 'API & Webhooks' in hello **Scenario** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="31a48-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="31a48-117">Selecteer een van de sjablonen Hallo en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="31a48-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="31a48-118">Standaard wordt een HTTP-trigger toohello aanvraag met een HTTP 200 OK-statuscode en een lege hoofdtekst reageren.</span><span class="sxs-lookup"><span data-stu-id="31a48-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="31a48-119">toomodify Hallo antwoord, configureert een [HTTP uitvoer binding](#output)</span><span class="sxs-lookup"><span data-stu-id="31a48-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="31a48-120">Configureren van een HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="31a48-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="31a48-121">Een HTTP-trigger is gedefinieerd door een JSON-object vergelijkbare toohello in hello te volgen, waaronder `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="31a48-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="31a48-122">Hallo binding ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="31a48-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="31a48-123">**naam** : vereist - Hallo variabelenaam in functiecode gebruikt voor het Hallo-aanvraag of de hoofdtekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="31a48-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="31a48-124">Zie [werken met een HTTP-trigger vanuit code](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="31a48-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="31a48-125">**type** : vereist - moet worden ingesteld te 'httpTrigger'.</span><span class="sxs-lookup"><span data-stu-id="31a48-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="31a48-126">**richting** : vereist - moet zijn ingesteld te 'in'.</span><span class="sxs-lookup"><span data-stu-id="31a48-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="31a48-127">_authLevel_ : Hiermee bepaalt u welke sleutels, indien van toepassing, moeten toobe aanwezig is op Hallo-aanvraag in de volgorde tooinvoke Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="31a48-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="31a48-128">Zie [werken met sleutels](#keys) hieronder.</span><span class="sxs-lookup"><span data-stu-id="31a48-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="31a48-129">Hallo-waarde kan zijn dat een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="31a48-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="31a48-130">_anonieme_: Er is geen API-sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="31a48-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="31a48-131">_de functie_: een functiespecifieke API-sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="31a48-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="31a48-132">Dit is de standaardwaarde Hallo als niets wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="31a48-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="31a48-133">_beheerder_ : Hallo hoofdsleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="31a48-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="31a48-134">**methoden** : dit is een matrix van Hallo HTTP-methoden toowhich Hallo functie reageert.</span><span class="sxs-lookup"><span data-stu-id="31a48-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="31a48-135">Als niet wordt opgegeven, reageert Hallo functie tooall HTTP-methoden.</span><span class="sxs-lookup"><span data-stu-id="31a48-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="31a48-136">Zie [aanpassen Hallo HTTP-eindpunt](#url).</span><span class="sxs-lookup"><span data-stu-id="31a48-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="31a48-137">**route** : Hiermee definieert u Hallo-Routesjabloon toowhich beheren uw functie reageert URL's aanvragen.</span><span class="sxs-lookup"><span data-stu-id="31a48-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="31a48-138">Hallo standaardwaarde als niets wordt opgegeven is `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="31a48-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="31a48-139">Zie [aanpassen Hallo HTTP-eindpunt](#url).</span><span class="sxs-lookup"><span data-stu-id="31a48-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="31a48-140">**webHookType** : Hiermee configureert u Hallo HTTP-trigger tooact als een webhook reciever voor de opgegeven provider Hallo.</span><span class="sxs-lookup"><span data-stu-id="31a48-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="31a48-141">Hallo _methoden_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="31a48-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="31a48-142">Zie [reageren toowebhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="31a48-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="31a48-143">Hallo-waarde kan zijn dat een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="31a48-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="31a48-144">_genericJson_ : een eindpunt van de webhook algemeen zonder logica voor een specifieke provider.</span><span class="sxs-lookup"><span data-stu-id="31a48-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="31a48-145">_github_ : Hallo functie tooGitHub webhooks reageert.</span><span class="sxs-lookup"><span data-stu-id="31a48-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="31a48-146">Hallo _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="31a48-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="31a48-147">_vertraging_ : Hallo functie tooSlack webhooks reageert.</span><span class="sxs-lookup"><span data-stu-id="31a48-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="31a48-148">Hallo _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="31a48-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="31a48-149">Werken met een HTTP-trigger van code</span><span class="sxs-lookup"><span data-stu-id="31a48-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="31a48-150">Voor C# en F #, kunt u ofwel Hallo-type van uw invoer toobe trigger declareren `HttpRequestMessage` of een aangepast type.</span><span class="sxs-lookup"><span data-stu-id="31a48-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="31a48-151">Als u ervoor kiest `HttpRequestMessage`, en vervolgens wordt u volledige toegang toohello request-object.</span><span class="sxs-lookup"><span data-stu-id="31a48-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="31a48-152">Voor een aangepast type (zoals een POCO) probeert functies tooparse Hallo aanvraagtekst als JSON toopopulate Hallo objecteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="31a48-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="31a48-153">Voor Node.js-functies biedt runtime van Functions Hallo Hallo aanvraagtekst in plaats van Hallo request-object.</span><span class="sxs-lookup"><span data-stu-id="31a48-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="31a48-154">Zie [voorbeelden van HTTP-trigger](#httptriggersample) bijvoorbeeld gebruik.</span><span class="sxs-lookup"><span data-stu-id="31a48-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="31a48-155">Binding voor de HTTP-antwoord van de uitvoer</span><span class="sxs-lookup"><span data-stu-id="31a48-155">HTTP response output binding</span></span>
<span data-ttu-id="31a48-156">Hallo HTTP-uitvoer binding toorespond toohello HTTP-aanvraag afzender gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31a48-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="31a48-157">Deze binding vereist een HTTP-trigger en kunt u toocustomize Hallo antwoord is gekoppeld aan de aanvraag van trigger Hallo.</span><span class="sxs-lookup"><span data-stu-id="31a48-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="31a48-158">Als een HTTP-uitvoer binding is niet opgegeven, wordt een HTTP-trigger HTTP 200 OK wordt geretourneerd met een lege hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="31a48-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="31a48-159">Binding uitvoer voor het configureren van een HTTP</span><span class="sxs-lookup"><span data-stu-id="31a48-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="31a48-160">Hallo HTTP uitvoer binding wordt gedefinieerd door een JSON-object vergelijkbare toohello in hello te volgen, waaronder `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="31a48-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="31a48-161">Hallo binding bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="31a48-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="31a48-162">**naam** : vereist - variabelenaam in functiecode gebruikt voor het antwoord Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="31a48-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="31a48-163">Zie [werken met een HTTP-uitvoer binding vanuit code](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="31a48-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="31a48-164">**type** : vereist - moet worden ingesteld te 'http'.</span><span class="sxs-lookup"><span data-stu-id="31a48-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="31a48-165">**richting** : vereist - moet zijn ingesteld te 'uit'.</span><span class="sxs-lookup"><span data-stu-id="31a48-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="31a48-166">Werken met een HTTP-uitvoer binding van code</span><span class="sxs-lookup"><span data-stu-id="31a48-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="31a48-167">U kunt Hallo uitvoer parameter (bijvoorbeeld ' res') toorespond toohello HTTP- of webhook aanroeper gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31a48-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="31a48-168">U kunt ook kunt u de standaard `Request.CreateResponse()` (C#) of `context.res` (Node.JS) patroon tooreturn uw antwoord.</span><span class="sxs-lookup"><span data-stu-id="31a48-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="31a48-169">Zie voor voorbeelden van hoe toouse de laatste methode hello, [voorbeelden van HTTP-trigger](#httptriggersample) en [Webhook trigger voorbeelden](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="31a48-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="31a48-170">Toowebhooks reageert</span><span class="sxs-lookup"><span data-stu-id="31a48-170">Responding toowebhooks</span></span>
<span data-ttu-id="31a48-171">Een HTTP-trigger Hello _webHookType_ eigenschap worden geconfigureerde toorespond te[webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="31a48-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="31a48-172">Hallo-basisconfiguratie gebruikt Hallo 'genericJson' instelling.</span><span class="sxs-lookup"><span data-stu-id="31a48-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="31a48-173">Hiermee beperkt u aanvragen tooonly die via HTTP POST en Hello `application/json` inhoudstype.</span><span class="sxs-lookup"><span data-stu-id="31a48-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="31a48-174">Hallo trigger kan ook worden aangepast tooa specifieke webhook provider (bijv, [GitHub](https://developer.github.com/webhooks/) en [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="31a48-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="31a48-175">Als een provider is opgegeven, kan runtime van Functions Hallo behandelen validatielogica Hallo-provider voor u.</span><span class="sxs-lookup"><span data-stu-id="31a48-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="31a48-176">GitHub als een webhook-provider configureren</span><span class="sxs-lookup"><span data-stu-id="31a48-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="31a48-177">toorespond tooGitHub webhooks, eerst uw functie te maken met een HTTP-Trigger en stel Hallo _webHookType_ eigenschap te 'github'.</span><span class="sxs-lookup"><span data-stu-id="31a48-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="31a48-178">Kopieer de [URL](#url) en [API-sleutel](#keys) in uw GitHub-opslagplaats **webhook toevoegen** pagina.</span><span class="sxs-lookup"><span data-stu-id="31a48-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="31a48-179">Zie de GitHub [Webhooks maken](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="31a48-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="31a48-180">Vertraging configureren als een webhook-provider</span><span class="sxs-lookup"><span data-stu-id="31a48-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="31a48-181">Hallo toegestane webhook genereert een token voor u in plaats van waarin u kunt opgeven, dus u een sleutel functiespecifieke met Hallo-token van de toegestane vertraging configureren moet.</span><span class="sxs-lookup"><span data-stu-id="31a48-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="31a48-182">Zie [werken met sleutels](#keys).</span><span class="sxs-lookup"><span data-stu-id="31a48-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="31a48-183">Hallo HTTP-eindpunt aanpassen</span><span class="sxs-lookup"><span data-stu-id="31a48-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="31a48-184">Wanneer u een functie voor een HTTP-trigger of WebHook, is Hallo-functie standaard adresseerbare met een route Hallo vorm:</span><span class="sxs-lookup"><span data-stu-id="31a48-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="31a48-185">U kunt deze route met optionele Hallo `route` -eigenschap op Hallo HTTP-trigger binding de invoer.</span><span class="sxs-lookup"><span data-stu-id="31a48-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="31a48-186">Als u bijvoorbeeld Hallo na *function.json* -bestand definieert een `route` eigenschap voor een HTTP-trigger:</span><span class="sxs-lookup"><span data-stu-id="31a48-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="31a48-187">Met deze configuratie, is Hallo-functie nu adresseerbare Hello route in plaats van de oorspronkelijke route hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="31a48-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="31a48-188">Hierdoor kan de functiecode Hallo toosupport twee parameters in het Hallo-adres, 'categorie' en 'id'.</span><span class="sxs-lookup"><span data-stu-id="31a48-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="31a48-189">U kunt een [Web API Route beperking](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) met de parameters.</span><span class="sxs-lookup"><span data-stu-id="31a48-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="31a48-190">Hallo volgende C#-functiecode maakt gebruik van beide parameters.</span><span class="sxs-lookup"><span data-stu-id="31a48-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="31a48-191">Hier volgt Node.js functie code toouse Hallo dezelfde Routeparameters.</span><span class="sxs-lookup"><span data-stu-id="31a48-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="31a48-192">Standaard worden alle routes van de functie voorafgegaan door *api*.</span><span class="sxs-lookup"><span data-stu-id="31a48-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="31a48-193">U kunt ook aanpassen of verwijderen van Hallo-adresvoorvoegsel dat gebruikmaakt van Hallo `http.routePrefix` eigenschap in uw *host.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="31a48-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="31a48-194">Hallo volgende voorbeeld wordt verwijderd Hallo *api* routeprefix met behulp van een lege tekenreeks voor Hallo-voorvoegsel in Hallo *host.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="31a48-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="31a48-195">Voor gedetailleerde informatie over het tooupdate hello *host.json* -bestand voor de functie, Zie [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="31a48-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="31a48-196">Voor informatie over andere eigenschappen kunt u configureren uw *host.json* bestand, Zie [host.json verwijzing](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="31a48-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="31a48-197">Werken met sleutels</span><span class="sxs-lookup"><span data-stu-id="31a48-197">Working with keys</span></span>
<span data-ttu-id="31a48-198">HttpTriggers kunt gebruikmaken van sleutels voor extra beveiliging.</span><span class="sxs-lookup"><span data-stu-id="31a48-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="31a48-199">Een standaard HttpTrigger kunt deze als een API-sleutel gebruiken sleutel toobe Hallo aanwezig is op verzoek Hallo vereisen.</span><span class="sxs-lookup"><span data-stu-id="31a48-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="31a48-200">Webhooks kunt sleutels tooauthorize aanvragen in verschillende manieren, afhankelijk van welke Hallo-provider ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="31a48-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="31a48-201">Sleutels worden opgeslagen als onderdeel van de functie-app in Azure en zijn versleuteld in rust.</span><span class="sxs-lookup"><span data-stu-id="31a48-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="31a48-202">tooview uw sleutels, maakt u nieuwe of draai sleutels toonew waarden, gaat u tooone van uw functies binnen Hallo-portal en selecteert u 'Beheren'.</span><span class="sxs-lookup"><span data-stu-id="31a48-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="31a48-203">Er zijn twee soorten sleutels:</span><span class="sxs-lookup"><span data-stu-id="31a48-203">There are two types of keys:</span></span>
- <span data-ttu-id="31a48-204">**Hostsleutels**: deze sleutels worden gedeeld door alle functies binnen Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="31a48-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="31a48-205">Wanneer als een API-sleutel gebruikt, kunnen deze functie voor toegang tot tooany binnen Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="31a48-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="31a48-206">**Functietoetsen**: deze sleutels toepassen alleen toohello specifieke functies waarin ze zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="31a48-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="31a48-207">Wanneer als een API-sleutel gebruikt, kan deze alleen toegang toothat functie.</span><span class="sxs-lookup"><span data-stu-id="31a48-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="31a48-208">Elke sleutel met de naam voor de verwijzing en er is een standaard-sleutel (met de naam 'standaard') op Hallo-functie en host-niveau.</span><span class="sxs-lookup"><span data-stu-id="31a48-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="31a48-209">Hallo **hoofdsleutel** een standaard host-sleutel is met de naam '_master' die is gedefinieerd voor elke functie-app en kan niet worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="31a48-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="31a48-210">Het biedt beheerderstoegang toohello runtime-API's.</span><span class="sxs-lookup"><span data-stu-id="31a48-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="31a48-211">Met behulp van `"authLevel": "admin"` in Hallo JSON binding vereist deze sleutel toobe die wordt weergegeven op Hallo aanvraag; een andere toets resulteert in een mislukte verificatiepogingen.</span><span class="sxs-lookup"><span data-stu-id="31a48-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="31a48-212">Vervaldatum toohello verhoogde machtigingen verleend door hoofdsleutel hello, u dient deze sleutel delen met derden of distribueren in systeemeigen clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="31a48-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="31a48-213">Wees voorzichtig bij het kiezen van Hallo beheerder autorisatieniveau.</span><span class="sxs-lookup"><span data-stu-id="31a48-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="31a48-214">API-sleutel autorisatie</span><span class="sxs-lookup"><span data-stu-id="31a48-214">API key authorization</span></span>
<span data-ttu-id="31a48-215">Een HttpTrigger moet standaard een API-sleutel in Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="31a48-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="31a48-216">Dus de HTTP-aanvraag normaal ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="31a48-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="31a48-217">Hallo-sleutel kan worden opgenomen in een queryreeks-variabele met de naam `code`, zoals hierboven, of kan worden opgenomen in een `x-functions-key` HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="31a48-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="31a48-218">Hallo-waarde van Hallo sleutel mag een gedefinieerd voor de functie Hallo functietoets of op een host-toets.</span><span class="sxs-lookup"><span data-stu-id="31a48-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="31a48-219">U kunt kiezen tooallow aanvragen zonder sleutels of opgeven die hoofdsleutel Hallo moet worden gebruikt door het wijzigen van Hallo `authLevel` eigenschap in JSON-binding hello (Zie [HTTP-trigger](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="31a48-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="31a48-220">Sleutels en webhooks.</span><span class="sxs-lookup"><span data-stu-id="31a48-220">Keys and webhooks</span></span>
<span data-ttu-id="31a48-221">Webhook-autorisatie is verwerkt door Hallo webhook reciever onderdeel, deel van Hallo HttpTrigger en Hallo mechanisme varieert op basis van Hallo webhook type.</span><span class="sxs-lookup"><span data-stu-id="31a48-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="31a48-222">Elke mechanisme komt, maar afhankelijk zijn van een sleutel.</span><span class="sxs-lookup"><span data-stu-id="31a48-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="31a48-223">Standaard wordt Hallo functie sleutel met de naam 'standaard' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="31a48-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="31a48-224">Als u op een andere sleutel toouse wenst, moet u tooconfigure hello webhook provider toosend Hallo sleutelnaam met Hallo-aanvraag in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="31a48-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="31a48-225">**Querytekenreeks**: Hallo provider doorgeeft Hallo sleutelnaam in Hallo `clientid` querytekenreeksparameter (bijv, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="31a48-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="31a48-226">**Aanvraagheader**: Hallo provider doorgeeft Hallo sleutelnaam in Hallo `x-functions-clientid` header.</span><span class="sxs-lookup"><span data-stu-id="31a48-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="31a48-227">Functietoetsen hebben voorrang op de hostsleutels.</span><span class="sxs-lookup"><span data-stu-id="31a48-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="31a48-228">Als twee sleutels zijn gedefinieerd met dezelfde naam, Hallo Hallo functietoets wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="31a48-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="31a48-229">Voorbeelden van HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="31a48-229">HTTP trigger samples</span></span>
<span data-ttu-id="31a48-230">Stel dat er na HTTP-trigger in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="31a48-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="31a48-231">Zie Hallo taalspecifieke voorbeeldtoepassing die u zoekt een `name` parameter in de queryreeks Hallo of Hallo hoofdtekst van Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="31a48-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="31a48-232">C#</span><span class="sxs-lookup"><span data-stu-id="31a48-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="31a48-233">F#</span><span class="sxs-lookup"><span data-stu-id="31a48-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="31a48-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="31a48-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="31a48-235">Voorbeeld van de HTTP-trigger in C#</span><span class="sxs-lookup"><span data-stu-id="31a48-235">HTTP trigger sample in C#</span></span> #
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

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="31a48-236">U kunt ook tooa POCO binden in plaats van `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="31a48-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="31a48-237">Dit wordt gehydrateerd van Hallo instantie van de aanvraag hello, geparseerd als JSON.</span><span class="sxs-lookup"><span data-stu-id="31a48-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="31a48-238">Op deze manier kan een type worden doorgegeven antwoorduitvoer toohello HTTP-binding en dit wordt geretourneerd als de antwoordtekst Hallo met een statuscode 200.</span><span class="sxs-lookup"><span data-stu-id="31a48-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="31a48-239">Voorbeeld van de HTTP-trigger in F #</span><span class="sxs-lookup"><span data-stu-id="31a48-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="31a48-240">U moet een `project.json` bestand met NuGet tooreference hello `FSharp.Interop.Dynamic` en `Dynamitey` assembly's, als volgt:</span><span class="sxs-lookup"><span data-stu-id="31a48-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="31a48-241">Dit NuGet toofetch afhankelijkheden gebruikt en wordt deze in uw script verwijst.</span><span class="sxs-lookup"><span data-stu-id="31a48-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="31a48-242">Voorbeeld van de HTTP-trigger in Node.JS</span><span class="sxs-lookup"><span data-stu-id="31a48-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="31a48-243">Webhook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="31a48-243">Webhook samples</span></span>
<span data-ttu-id="31a48-244">Stel dat er na webhook trigger in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="31a48-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="31a48-245">Zie Hallo taalspecifieke voorbeeldtoepassing die u GitHub probleem opmerkingen registreert.</span><span class="sxs-lookup"><span data-stu-id="31a48-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="31a48-246">C#</span><span class="sxs-lookup"><span data-stu-id="31a48-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="31a48-247">F#</span><span class="sxs-lookup"><span data-stu-id="31a48-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="31a48-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="31a48-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="31a48-249">Voorbeeld van de Webhook in C#</span><span class="sxs-lookup"><span data-stu-id="31a48-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="31a48-250">Voorbeeld van de Webhook in F #</span><span class="sxs-lookup"><span data-stu-id="31a48-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="31a48-251">Voorbeeld van de Webhook in Node.JS</span><span class="sxs-lookup"><span data-stu-id="31a48-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="31a48-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31a48-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

