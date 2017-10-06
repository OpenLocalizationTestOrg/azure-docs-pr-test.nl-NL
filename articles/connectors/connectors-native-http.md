---
title: aaaCommunicate met een willekeurig eindpunt via HTTP - Azure Logic Apps | Microsoft Docs
description: Logische apps die kunnen communiceren met een willekeurig eindpunt te maken via HTTP
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="19da7-103">Aan de slag met Hallo HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="19da7-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="19da7-104">Met HTTP-actie hello, kunt u werkstromen voor uw organisatie uitbreiden en tooany eindpunt communicatie via HTTP.</span><span class="sxs-lookup"><span data-stu-id="19da7-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="19da7-105">U kunt:</span><span class="sxs-lookup"><span data-stu-id="19da7-105">You can:</span></span>

* <span data-ttu-id="19da7-106">Logic app-werkstromen waarmee (trigger) wordt geactiveerd wanneer een website die u beheert uitvalt maken.</span><span class="sxs-lookup"><span data-stu-id="19da7-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="19da7-107">Communiceren tooany eindpunt via HTTP tooextend uw werkstromen bij andere services.</span><span class="sxs-lookup"><span data-stu-id="19da7-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="19da7-108">tooget gestart met Hallo HTTP-actie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="19da7-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="19da7-109">Hallo HTTP-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="19da7-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="19da7-110">Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="19da7-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="19da7-111">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19da7-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="19da7-112">Hier volgt een van de voorbeeldreeks hoe tooset up Hallo HTTP activeren in Hallo Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="19da7-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="19da7-113">Hallo HTTP-trigger toevoegen in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="19da7-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="19da7-114">Hallo-parameters voor Hallo HTTP-eindpunt dat u wilt dat toopoll invullen.</span><span class="sxs-lookup"><span data-stu-id="19da7-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="19da7-115">Hallo terugkeerpatroon op hoe vaak het pollen moet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="19da7-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="19da7-116">Hallo logische app wordt nu gestart met inhoud die is geretourneerd tijdens elke controle.</span><span class="sxs-lookup"><span data-stu-id="19da7-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP-trigger](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="19da7-118">De werking van de HTTP-trigger Hallo</span><span class="sxs-lookup"><span data-stu-id="19da7-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="19da7-119">Hallo HTTP-trigger stuurt een aanroep van tooHTTP-eindpunt op een terugkerend interval.</span><span class="sxs-lookup"><span data-stu-id="19da7-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="19da7-120">Standaard een HTTP-antwoordcode die lager is dan 300 zorgt ervoor dat de toorun van een logische app.</span><span class="sxs-lookup"><span data-stu-id="19da7-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="19da7-121">toospecify of Hallo logische app moet worden geactiveerd, u kunt Hallo logische app in de codeweergave bewerken en toevoegen van een voorwaarde die wordt geëvalueerd als na Hallo HTTP-aanroep.</span><span class="sxs-lookup"><span data-stu-id="19da7-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="19da7-122">Hier volgt een voorbeeld van een HTTP-trigger wordt geactiveerd wanneer het Hallo geretourneerde statuscode is groter dan of gelijk zijn aan te`400`.</span><span class="sxs-lookup"><span data-stu-id="19da7-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="19da7-123">Volledige details over Hallo HTTP-trigger-parameters zijn beschikbaar op [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="19da7-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="19da7-124">Gebruik Hallo HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="19da7-124">Use hello HTTP action</span></span>

<span data-ttu-id="19da7-125">Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="19da7-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="19da7-126">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19da7-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="19da7-127">Kies **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="19da7-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="19da7-128">Typ in het zoekvak Hallo actie, **http** toolist Hallo HTTP acties.</span><span class="sxs-lookup"><span data-stu-id="19da7-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Selecteer Hallo HTTP-actie](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="19da7-130">Voeg eventueel vereiste parameters voor Hallo HTTP-aanroep.</span><span class="sxs-lookup"><span data-stu-id="19da7-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Volledige Hallo HTTP-actie](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="19da7-132">Op de werkbalk Hallo designer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="19da7-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="19da7-133">Uw logische app worden opgeslagen en gepubliceerd (geactiveerd) op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="19da7-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="19da7-134">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="19da7-134">HTTP trigger</span></span>
<span data-ttu-id="19da7-135">Hier vindt u details Hallo Hallo-trigger die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="19da7-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="19da7-136">Hallo HTTP-connector heeft een trigger.</span><span class="sxs-lookup"><span data-stu-id="19da7-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="19da7-137">Trigger</span><span class="sxs-lookup"><span data-stu-id="19da7-137">Trigger</span></span> | <span data-ttu-id="19da7-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19da7-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="19da7-139">HTTP</span></span> |<span data-ttu-id="19da7-140">Maakt een HTTP-aanroep en antwoordinhoud Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="19da7-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="19da7-141">HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="19da7-141">HTTP action</span></span>
<span data-ttu-id="19da7-142">Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="19da7-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="19da7-143">Hallo HTTP-connector heeft een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="19da7-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="19da7-144">Actie</span><span class="sxs-lookup"><span data-stu-id="19da7-144">Action</span></span> | <span data-ttu-id="19da7-145">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19da7-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="19da7-146">HTTP</span></span> |<span data-ttu-id="19da7-147">Maakt een HTTP-aanroep en antwoordinhoud Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="19da7-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="19da7-148">HTTP-details</span><span class="sxs-lookup"><span data-stu-id="19da7-148">HTTP details</span></span>
<span data-ttu-id="19da7-149">Hallo volgende tabellen worden beschreven Hallo vereiste en optionele invoervelden voor Hallo actie en het bijbehorende uitvoerdetails hello, die gekoppeld zijn aan het Hallo-actie.</span><span class="sxs-lookup"><span data-stu-id="19da7-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="19da7-150">HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="19da7-150">HTTP request</span></span>
<span data-ttu-id="19da7-151">Hallo volgen invoervelden voor Hallo actie, waardoor een uitgaande HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="19da7-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="19da7-152">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="19da7-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="19da7-153">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="19da7-153">Display name</span></span> | <span data-ttu-id="19da7-154">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="19da7-154">Property name</span></span> | <span data-ttu-id="19da7-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19da7-156">Methode *</span><span class="sxs-lookup"><span data-stu-id="19da7-156">Method*</span></span> |<span data-ttu-id="19da7-157">Methode</span><span class="sxs-lookup"><span data-stu-id="19da7-157">method</span></span> |<span data-ttu-id="19da7-158">Hallo HTTP-term toouse</span><span class="sxs-lookup"><span data-stu-id="19da7-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="19da7-159">URI *</span><span class="sxs-lookup"><span data-stu-id="19da7-159">URI*</span></span> |<span data-ttu-id="19da7-160">URI</span><span class="sxs-lookup"><span data-stu-id="19da7-160">uri</span></span> |<span data-ttu-id="19da7-161">Hallo URI voor Hallo HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="19da7-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="19da7-162">Headers</span><span class="sxs-lookup"><span data-stu-id="19da7-162">Headers</span></span> |<span data-ttu-id="19da7-163">Headers</span><span class="sxs-lookup"><span data-stu-id="19da7-163">headers</span></span> |<span data-ttu-id="19da7-164">Een JSON-object van het HTTP-headers tooinclude</span><span class="sxs-lookup"><span data-stu-id="19da7-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="19da7-165">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="19da7-165">Body</span></span> |<span data-ttu-id="19da7-166">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="19da7-166">body</span></span> |<span data-ttu-id="19da7-167">Hallo hoofdtekst van de HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="19da7-167">hello HTTP request body</span></span> |
| <span data-ttu-id="19da7-168">Authentication</span><span class="sxs-lookup"><span data-stu-id="19da7-168">Authentication</span></span> |<span data-ttu-id="19da7-169">Verificatie</span><span class="sxs-lookup"><span data-stu-id="19da7-169">authentication</span></span> |<span data-ttu-id="19da7-170">De details in Hallo [verificatie](#authentication) sectie</span><span class="sxs-lookup"><span data-stu-id="19da7-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="19da7-171">Uitvoerdetails</span><span class="sxs-lookup"><span data-stu-id="19da7-171">Output details</span></span>
<span data-ttu-id="19da7-172">Hallo hieronder vindt u uitvoerdetails voor Hallo HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="19da7-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="19da7-173">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="19da7-173">Property name</span></span> | <span data-ttu-id="19da7-174">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="19da7-174">Data type</span></span> | <span data-ttu-id="19da7-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19da7-176">Headers</span><span class="sxs-lookup"><span data-stu-id="19da7-176">Headers</span></span> |<span data-ttu-id="19da7-177">object</span><span class="sxs-lookup"><span data-stu-id="19da7-177">object</span></span> |<span data-ttu-id="19da7-178">Antwoordheaders</span><span class="sxs-lookup"><span data-stu-id="19da7-178">Response headers</span></span> |
| <span data-ttu-id="19da7-179">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="19da7-179">Body</span></span> |<span data-ttu-id="19da7-180">object</span><span class="sxs-lookup"><span data-stu-id="19da7-180">object</span></span> |<span data-ttu-id="19da7-181">Response-object</span><span class="sxs-lookup"><span data-stu-id="19da7-181">Response object</span></span> |
| <span data-ttu-id="19da7-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="19da7-182">Status Code</span></span> |<span data-ttu-id="19da7-183">int</span><span class="sxs-lookup"><span data-stu-id="19da7-183">int</span></span> |<span data-ttu-id="19da7-184">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="19da7-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="19da7-185">Authentication</span><span class="sxs-lookup"><span data-stu-id="19da7-185">Authentication</span></span>
<span data-ttu-id="19da7-186">Hallo Logic Apps-functie kunt u verschillende soorten verificatie op basis van HTTP-eindpunten toouse.</span><span class="sxs-lookup"><span data-stu-id="19da7-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="19da7-187">U kunt deze verificatie Hallo **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, en  **[HTTP-Webhook](connectors-native-webhook.md)**  connectors.</span><span class="sxs-lookup"><span data-stu-id="19da7-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="19da7-188">Hallo volgende typen verificatie worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="19da7-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="19da7-189">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="19da7-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="19da7-190">Verificatie van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="19da7-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="19da7-191">Azure Active Directory (Azure AD) OAuth-verificatie</span><span class="sxs-lookup"><span data-stu-id="19da7-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="19da7-192">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="19da7-192">Basic authentication</span></span>

<span data-ttu-id="19da7-193">Hallo na verificatieobject is nodig voor basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="19da7-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="19da7-194">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="19da7-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="19da7-195">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="19da7-195">Property name</span></span> | <span data-ttu-id="19da7-196">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="19da7-196">Data type</span></span> | <span data-ttu-id="19da7-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19da7-198">Type *</span><span class="sxs-lookup"><span data-stu-id="19da7-198">Type*</span></span> |<span data-ttu-id="19da7-199">type</span><span class="sxs-lookup"><span data-stu-id="19da7-199">type</span></span> |<span data-ttu-id="19da7-200">Type verificatie (moet `Basic` voor basisverificatie)</span><span class="sxs-lookup"><span data-stu-id="19da7-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="19da7-201">Gebruikersnaam *</span><span class="sxs-lookup"><span data-stu-id="19da7-201">Username*</span></span> |<span data-ttu-id="19da7-202">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="19da7-202">username</span></span> |<span data-ttu-id="19da7-203">Gebruiker naam tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="19da7-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="19da7-204">Wachtwoord *</span><span class="sxs-lookup"><span data-stu-id="19da7-204">Password*</span></span> |<span data-ttu-id="19da7-205">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="19da7-205">password</span></span> |<span data-ttu-id="19da7-206">Wachtwoord tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="19da7-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="19da7-207">Als u een wachtwoord dat niet uit de definitie van Hallo ophalen toouse wilt, gebruikt een `securestring` parameter en Hallo `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="19da7-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="19da7-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19da7-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="19da7-209">Clientverificatie via certificaat</span><span class="sxs-lookup"><span data-stu-id="19da7-209">Client certificate authentication</span></span>

<span data-ttu-id="19da7-210">Hallo is volgende verificatieobject nodig voor verificatie van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="19da7-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="19da7-211">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="19da7-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="19da7-212">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="19da7-212">Property name</span></span> | <span data-ttu-id="19da7-213">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="19da7-213">Data type</span></span> | <span data-ttu-id="19da7-214">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19da7-215">Type *</span><span class="sxs-lookup"><span data-stu-id="19da7-215">Type*</span></span> |<span data-ttu-id="19da7-216">type</span><span class="sxs-lookup"><span data-stu-id="19da7-216">type</span></span> |<span data-ttu-id="19da7-217">Hallo type verificatie (moet `ClientCertificate` voor SSL-certificaten voor client)</span><span class="sxs-lookup"><span data-stu-id="19da7-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="19da7-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="19da7-218">PFX*</span></span> |<span data-ttu-id="19da7-219">PFX</span><span class="sxs-lookup"><span data-stu-id="19da7-219">pfx</span></span> |<span data-ttu-id="19da7-220">Hallo Base64-gecodeerde inhoud van Hallo Personal Information Exchange (PFX)-bestand</span><span class="sxs-lookup"><span data-stu-id="19da7-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="19da7-221">Wachtwoord *</span><span class="sxs-lookup"><span data-stu-id="19da7-221">Password*</span></span> |<span data-ttu-id="19da7-222">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="19da7-222">password</span></span> |<span data-ttu-id="19da7-223">Hallo wachtwoord tooaccess Hallo PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="19da7-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="19da7-224">een parameter die niet in de definitie van de Hallo na het opslaan van Hallo logische app leesbaar toouse, kunt u een `securestring` parameter en Hallo `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="19da7-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="19da7-225">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19da7-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="19da7-226">Azure AD-OAuth-verificatie</span><span class="sxs-lookup"><span data-stu-id="19da7-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="19da7-227">Hallo na verificatieobject is nodig voor Azure AD OAuth-verificatie.</span><span class="sxs-lookup"><span data-stu-id="19da7-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="19da7-228">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="19da7-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="19da7-229">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="19da7-229">Property name</span></span> | <span data-ttu-id="19da7-230">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="19da7-230">Data type</span></span> | <span data-ttu-id="19da7-231">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19da7-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19da7-232">Type *</span><span class="sxs-lookup"><span data-stu-id="19da7-232">Type*</span></span> |<span data-ttu-id="19da7-233">type</span><span class="sxs-lookup"><span data-stu-id="19da7-233">type</span></span> |<span data-ttu-id="19da7-234">Hallo type verificatie (moet `ActiveDirectoryOAuth` voor Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="19da7-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="19da7-235">Tenant *</span><span class="sxs-lookup"><span data-stu-id="19da7-235">Tenant*</span></span> |<span data-ttu-id="19da7-236">Tenant</span><span class="sxs-lookup"><span data-stu-id="19da7-236">tenant</span></span> |<span data-ttu-id="19da7-237">Hallo tenant-id voor hello Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="19da7-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="19da7-238">Doelgroep *</span><span class="sxs-lookup"><span data-stu-id="19da7-238">Audience*</span></span> |<span data-ttu-id="19da7-239">doelgroep</span><span class="sxs-lookup"><span data-stu-id="19da7-239">audience</span></span> |<span data-ttu-id="19da7-240">Hallo bron die u aanvraagt autorisatie toouse.</span><span class="sxs-lookup"><span data-stu-id="19da7-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="19da7-241">Bijvoorbeeld: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="19da7-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="19da7-242">Client -ID *</span><span class="sxs-lookup"><span data-stu-id="19da7-242">Client ID*</span></span> |<span data-ttu-id="19da7-243">clientId</span><span class="sxs-lookup"><span data-stu-id="19da7-243">clientId</span></span> |<span data-ttu-id="19da7-244">Hallo van client-id voor de toepassing hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19da7-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="19da7-245">Geheim *</span><span class="sxs-lookup"><span data-stu-id="19da7-245">Secret*</span></span> |<span data-ttu-id="19da7-246">Geheim</span><span class="sxs-lookup"><span data-stu-id="19da7-246">secret</span></span> |<span data-ttu-id="19da7-247">Hallo geheim van Hallo-client die Hallo-token aanvraagt</span><span class="sxs-lookup"><span data-stu-id="19da7-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="19da7-248">U kunt een `securestring` parameter en Hallo `@parameters()` [definitie Werkstroomfunctie](http://aka.ms/logicappdocs) toouse een parameter die niet leesbaar is in definitie van de Hallo nadat ze zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="19da7-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="19da7-249">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19da7-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="19da7-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19da7-250">Next steps</span></span>
<span data-ttu-id="19da7-251">Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="19da7-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="19da7-252">U kunt verkennen Hallo van andere beschikbare connectors in Logic Apps door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="19da7-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

