---
title: Communicatie met een willekeurig eindpunt via HTTP - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="f763e-103">Aan de slag met de HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="f763e-103">Get started with the HTTP action</span></span>

<span data-ttu-id="f763e-104">U kunt met de HTTP-actie werkstromen voor uw organisatie uitbreiden en communiceren met een willekeurig eindpunt via HTTP.</span><span class="sxs-lookup"><span data-stu-id="f763e-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="f763e-105">U kunt:</span><span class="sxs-lookup"><span data-stu-id="f763e-105">You can:</span></span>

* <span data-ttu-id="f763e-106">Logic app-werkstromen waarmee (trigger) wordt geactiveerd wanneer een website die u beheert uitvalt maken.</span><span class="sxs-lookup"><span data-stu-id="f763e-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="f763e-107">Naar een willekeurig eindpunt communiceren via HTTP voor het uitbreiden van uw werkstromen bij andere services.</span><span class="sxs-lookup"><span data-stu-id="f763e-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="f763e-108">Om te beginnen met de HTTP-actie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f763e-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="f763e-109">De HTTP-trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="f763e-109">Use the HTTP trigger</span></span>
<span data-ttu-id="f763e-110">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="f763e-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="f763e-111">[Meer informatie over triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f763e-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="f763e-112">Hier volgt een voorbeeld van de volgorde van het instellen van de HTTP-trigger in de ontwerpfunctie voor Logic App.</span><span class="sxs-lookup"><span data-stu-id="f763e-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="f763e-113">De HTTP-trigger toevoegen in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="f763e-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="f763e-114">Vul de parameters voor het HTTP-eindpunt dat u wilt pollen.</span><span class="sxs-lookup"><span data-stu-id="f763e-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="f763e-115">Wijzig het terugkeerpatroon op hoe vaak het moet peilen.</span><span class="sxs-lookup"><span data-stu-id="f763e-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="f763e-116">De logische app wordt nu gestart met inhoud die is geretourneerd tijdens elke controle.</span><span class="sxs-lookup"><span data-stu-id="f763e-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP-trigger](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="f763e-118">De werking van de HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="f763e-118">How the HTTP trigger works</span></span>

<span data-ttu-id="f763e-119">De HTTP-trigger stuurt een aanroep van HTTP-eindpunt op een terugkerend interval.</span><span class="sxs-lookup"><span data-stu-id="f763e-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="f763e-120">Standaard een HTTP-antwoordcode die lager is dan 300 zorgt ervoor dat een logische app om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f763e-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="f763e-121">U kunt om op te geven of de logische app moet worden geactiveerd, de logische app in de codeweergave bewerken en toevoegen van een voorwaarde die wordt geëvalueerd als na de HTTP-aanroep.</span><span class="sxs-lookup"><span data-stu-id="f763e-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="f763e-122">Hier volgt een voorbeeld van een HTTP-trigger wordt geactiveerd wanneer de geretourneerde statuscode is groter dan of gelijk zijn aan `400`.</span><span class="sxs-lookup"><span data-stu-id="f763e-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

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

<span data-ttu-id="f763e-123">Volledige details over de HTTP-trigger-parameters zijn beschikbaar op [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="f763e-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="f763e-124">Gebruik de HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="f763e-124">Use the HTTP action</span></span>

<span data-ttu-id="f763e-125">Een actie is een bewerking die wordt uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="f763e-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="f763e-126">[Meer informatie over acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f763e-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="f763e-127">Kies **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f763e-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="f763e-128">Typ in het zoekvak actie **http** voor een lijst met de HTTP-acties.</span><span class="sxs-lookup"><span data-stu-id="f763e-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Selecteer de HTTP-actie](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="f763e-130">Voeg eventueel vereiste parameters voor de HTTP-aanroep.</span><span class="sxs-lookup"><span data-stu-id="f763e-130">Add any required parameters for the HTTP call.</span></span>
   
    ![De HTTP-actie niet voltooien](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="f763e-132">Klik op de werkbalk designer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f763e-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="f763e-133">Uw logische app worden opgeslagen en gepubliceerd (geactiveerd) op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="f763e-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="f763e-134">HTTP-trigger</span><span class="sxs-lookup"><span data-stu-id="f763e-134">HTTP trigger</span></span>
<span data-ttu-id="f763e-135">Hier volgen de details voor de trigger die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="f763e-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="f763e-136">De HTTP-connector heeft een trigger.</span><span class="sxs-lookup"><span data-stu-id="f763e-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="f763e-137">Trigger</span><span class="sxs-lookup"><span data-stu-id="f763e-137">Trigger</span></span> | <span data-ttu-id="f763e-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f763e-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="f763e-139">HTTP</span></span> |<span data-ttu-id="f763e-140">Maakt een HTTP-aanroep en retourneert de antwoordinhoud.</span><span class="sxs-lookup"><span data-stu-id="f763e-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="f763e-141">HTTP-actie</span><span class="sxs-lookup"><span data-stu-id="f763e-141">HTTP action</span></span>
<span data-ttu-id="f763e-142">Hier volgen de details voor de actie die ondersteuning biedt voor deze connector.</span><span class="sxs-lookup"><span data-stu-id="f763e-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="f763e-143">De HTTP-connector heeft een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="f763e-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="f763e-144">Actie</span><span class="sxs-lookup"><span data-stu-id="f763e-144">Action</span></span> | <span data-ttu-id="f763e-145">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f763e-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="f763e-146">HTTP</span></span> |<span data-ttu-id="f763e-147">Maakt een HTTP-aanroep en retourneert de antwoordinhoud.</span><span class="sxs-lookup"><span data-stu-id="f763e-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="f763e-148">HTTP-details</span><span class="sxs-lookup"><span data-stu-id="f763e-148">HTTP details</span></span>
<span data-ttu-id="f763e-149">De volgende tabellen beschrijven de vereiste en optionele invoervelden voor de actie en de bijbehorende uitvoerdetails die zijn gekoppeld met de actie.</span><span class="sxs-lookup"><span data-stu-id="f763e-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="f763e-150">HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f763e-150">HTTP request</span></span>
<span data-ttu-id="f763e-151">Hier volgen de invoervelden voor de actie, waardoor een uitgaande HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f763e-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="f763e-152">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="f763e-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="f763e-153">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="f763e-153">Display name</span></span> | <span data-ttu-id="f763e-154">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f763e-154">Property name</span></span> | <span data-ttu-id="f763e-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f763e-156">Methode *</span><span class="sxs-lookup"><span data-stu-id="f763e-156">Method*</span></span> |<span data-ttu-id="f763e-157">Methode</span><span class="sxs-lookup"><span data-stu-id="f763e-157">method</span></span> |<span data-ttu-id="f763e-158">De HTTP-term moet worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="f763e-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="f763e-159">URI *</span><span class="sxs-lookup"><span data-stu-id="f763e-159">URI*</span></span> |<span data-ttu-id="f763e-160">URI</span><span class="sxs-lookup"><span data-stu-id="f763e-160">uri</span></span> |<span data-ttu-id="f763e-161">De URI voor de HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f763e-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="f763e-162">Headers</span><span class="sxs-lookup"><span data-stu-id="f763e-162">Headers</span></span> |<span data-ttu-id="f763e-163">Headers</span><span class="sxs-lookup"><span data-stu-id="f763e-163">headers</span></span> |<span data-ttu-id="f763e-164">De HTTP-headers te nemen van een JSON-object</span><span class="sxs-lookup"><span data-stu-id="f763e-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="f763e-165">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="f763e-165">Body</span></span> |<span data-ttu-id="f763e-166">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="f763e-166">body</span></span> |<span data-ttu-id="f763e-167">De hoofdtekst van de HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f763e-167">The HTTP request body</span></span> |
| <span data-ttu-id="f763e-168">Authentication</span><span class="sxs-lookup"><span data-stu-id="f763e-168">Authentication</span></span> |<span data-ttu-id="f763e-169">Verificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-169">authentication</span></span> |<span data-ttu-id="f763e-170">Gegevens in de [verificatie](#authentication) sectie</span><span class="sxs-lookup"><span data-stu-id="f763e-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="f763e-171">Uitvoerdetails</span><span class="sxs-lookup"><span data-stu-id="f763e-171">Output details</span></span>
<span data-ttu-id="f763e-172">Hier volgen de uitvoerdetails voor het HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="f763e-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="f763e-173">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f763e-173">Property name</span></span> | <span data-ttu-id="f763e-174">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="f763e-174">Data type</span></span> | <span data-ttu-id="f763e-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f763e-176">Headers</span><span class="sxs-lookup"><span data-stu-id="f763e-176">Headers</span></span> |<span data-ttu-id="f763e-177">object</span><span class="sxs-lookup"><span data-stu-id="f763e-177">object</span></span> |<span data-ttu-id="f763e-178">Antwoordheaders</span><span class="sxs-lookup"><span data-stu-id="f763e-178">Response headers</span></span> |
| <span data-ttu-id="f763e-179">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="f763e-179">Body</span></span> |<span data-ttu-id="f763e-180">object</span><span class="sxs-lookup"><span data-stu-id="f763e-180">object</span></span> |<span data-ttu-id="f763e-181">Response-object</span><span class="sxs-lookup"><span data-stu-id="f763e-181">Response object</span></span> |
| <span data-ttu-id="f763e-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="f763e-182">Status Code</span></span> |<span data-ttu-id="f763e-183">int</span><span class="sxs-lookup"><span data-stu-id="f763e-183">int</span></span> |<span data-ttu-id="f763e-184">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="f763e-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="f763e-185">Authentication</span><span class="sxs-lookup"><span data-stu-id="f763e-185">Authentication</span></span>
<span data-ttu-id="f763e-186">De functie Logic Apps kunt u verschillende soorten verificatie op basis van HTTP-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f763e-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="f763e-187">U kunt deze verificatie met de **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, en  **[HTTP-Webhook](connectors-native-webhook.md)**  connectors.</span><span class="sxs-lookup"><span data-stu-id="f763e-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="f763e-188">De volgende soorten authenticatie worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="f763e-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="f763e-189">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="f763e-190">Verificatie van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="f763e-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="f763e-191">Azure Active Directory (Azure AD) OAuth-verificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="f763e-192">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-192">Basic authentication</span></span>

<span data-ttu-id="f763e-193">De volgende verificatieobject is nodig voor basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="f763e-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="f763e-194">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="f763e-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="f763e-195">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f763e-195">Property name</span></span> | <span data-ttu-id="f763e-196">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="f763e-196">Data type</span></span> | <span data-ttu-id="f763e-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f763e-198">Type *</span><span class="sxs-lookup"><span data-stu-id="f763e-198">Type*</span></span> |<span data-ttu-id="f763e-199">type</span><span class="sxs-lookup"><span data-stu-id="f763e-199">type</span></span> |<span data-ttu-id="f763e-200">Type verificatie (moet `Basic` voor basisverificatie)</span><span class="sxs-lookup"><span data-stu-id="f763e-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="f763e-201">Gebruikersnaam *</span><span class="sxs-lookup"><span data-stu-id="f763e-201">Username*</span></span> |<span data-ttu-id="f763e-202">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="f763e-202">username</span></span> |<span data-ttu-id="f763e-203">Gebruikersnaam voor verificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-203">User name to authenticate</span></span> |
| <span data-ttu-id="f763e-204">Wachtwoord *</span><span class="sxs-lookup"><span data-stu-id="f763e-204">Password*</span></span> |<span data-ttu-id="f763e-205">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="f763e-205">password</span></span> |<span data-ttu-id="f763e-206">Wachtwoord voor verificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="f763e-207">Als u wilt geen wachtwoord gebruiken dat niet uit de definitie van gebruik ophalen een `securestring` parameter en de `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="f763e-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="f763e-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f763e-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="f763e-209">Clientverificatie via certificaat</span><span class="sxs-lookup"><span data-stu-id="f763e-209">Client certificate authentication</span></span>

<span data-ttu-id="f763e-210">De volgende verificatieobject is nodig voor verificatie van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="f763e-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="f763e-211">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="f763e-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="f763e-212">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f763e-212">Property name</span></span> | <span data-ttu-id="f763e-213">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="f763e-213">Data type</span></span> | <span data-ttu-id="f763e-214">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f763e-215">Type *</span><span class="sxs-lookup"><span data-stu-id="f763e-215">Type*</span></span> |<span data-ttu-id="f763e-216">type</span><span class="sxs-lookup"><span data-stu-id="f763e-216">type</span></span> |<span data-ttu-id="f763e-217">Het type verificatie (moet `ClientCertificate` voor SSL-certificaten voor client)</span><span class="sxs-lookup"><span data-stu-id="f763e-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="f763e-218">PFX *</span><span class="sxs-lookup"><span data-stu-id="f763e-218">PFX*</span></span> |<span data-ttu-id="f763e-219">PFX</span><span class="sxs-lookup"><span data-stu-id="f763e-219">pfx</span></span> |<span data-ttu-id="f763e-220">De Base64-gecodeerde inhoud van het bestand (Personal Information Exchange (PFX)</span><span class="sxs-lookup"><span data-stu-id="f763e-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="f763e-221">Wachtwoord *</span><span class="sxs-lookup"><span data-stu-id="f763e-221">Password*</span></span> |<span data-ttu-id="f763e-222">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="f763e-222">password</span></span> |<span data-ttu-id="f763e-223">Het wachtwoord voor toegang tot het PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="f763e-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="f763e-224">Als u wilt een parameter die niet leesbaar in de definitie na het opslaan van de logische app gebruikt, kunt u een `securestring` parameter en de `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="f763e-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="f763e-225">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f763e-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="f763e-226">Azure AD-OAuth-verificatie</span><span class="sxs-lookup"><span data-stu-id="f763e-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="f763e-227">De volgende verificatieobject is nodig voor Azure AD OAuth-verificatie.</span><span class="sxs-lookup"><span data-stu-id="f763e-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="f763e-228">A * houdt in dat een vereist veld.</span><span class="sxs-lookup"><span data-stu-id="f763e-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="f763e-229">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="f763e-229">Property name</span></span> | <span data-ttu-id="f763e-230">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="f763e-230">Data type</span></span> | <span data-ttu-id="f763e-231">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f763e-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f763e-232">Type *</span><span class="sxs-lookup"><span data-stu-id="f763e-232">Type*</span></span> |<span data-ttu-id="f763e-233">type</span><span class="sxs-lookup"><span data-stu-id="f763e-233">type</span></span> |<span data-ttu-id="f763e-234">Het type verificatie (moet `ActiveDirectoryOAuth` voor Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="f763e-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="f763e-235">Tenant *</span><span class="sxs-lookup"><span data-stu-id="f763e-235">Tenant*</span></span> |<span data-ttu-id="f763e-236">Tenant</span><span class="sxs-lookup"><span data-stu-id="f763e-236">tenant</span></span> |<span data-ttu-id="f763e-237">De tenant-id voor de Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="f763e-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="f763e-238">Doelgroep *</span><span class="sxs-lookup"><span data-stu-id="f763e-238">Audience*</span></span> |<span data-ttu-id="f763e-239">doelgroep</span><span class="sxs-lookup"><span data-stu-id="f763e-239">audience</span></span> |<span data-ttu-id="f763e-240">De bron die u aanvraagt autorisatie moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f763e-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="f763e-241">Bijvoorbeeld: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="f763e-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="f763e-242">Client -ID *</span><span class="sxs-lookup"><span data-stu-id="f763e-242">Client ID*</span></span> |<span data-ttu-id="f763e-243">clientId</span><span class="sxs-lookup"><span data-stu-id="f763e-243">clientId</span></span> |<span data-ttu-id="f763e-244">De client-id voor de Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="f763e-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="f763e-245">Geheim *</span><span class="sxs-lookup"><span data-stu-id="f763e-245">Secret*</span></span> |<span data-ttu-id="f763e-246">Geheim</span><span class="sxs-lookup"><span data-stu-id="f763e-246">secret</span></span> |<span data-ttu-id="f763e-247">Het geheim van de client die het token is aangevraagd</span><span class="sxs-lookup"><span data-stu-id="f763e-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="f763e-248">U kunt een `securestring` parameter en de `@parameters()` [Werkstroomfunctie definitie](http://aka.ms/logicappdocs) gebruiken een parameter die niet leesbaar in de definitie nadat ze zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f763e-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="f763e-249">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f763e-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="f763e-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f763e-250">Next steps</span></span>
<span data-ttu-id="f763e-251">Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f763e-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f763e-252">U kunt de beschikbare connectors in Logic Apps verkennen door te kijken onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f763e-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

