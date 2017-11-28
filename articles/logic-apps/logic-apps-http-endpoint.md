---
title: aaaCall, trigger of nesten van werkstromen met HTTP-eindpunten - Azure Logic Apps | Microsoft Docs
description: HTTP-eindpunten toocall, trigger of geneste werkstromen instellen voor Azure Logic Apps
services: logic-apps
keywords: werkstromen, HTTP-eindpunten
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="182c4-104">Bel, trigger of nesten van werkstromen met HTTP-eindpunten in logic apps</span><span class="sxs-lookup"><span data-stu-id="182c4-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="182c4-105">U kunt systeemeigen synchrone HTTP-eindpunten weergeven als triggers voor logic apps, zodat u kunt activeren of aanroepen van uw logische apps via een andere URL.</span><span class="sxs-lookup"><span data-stu-id="182c4-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="182c4-106">U kunt ook de werkstromen in uw logische apps nesten met behulp van een patroon van callable-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="182c4-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="182c4-107">toocreate HTTP-eindpunten, kunt u de triggers toevoegen zodat uw logische apps inkomende aanvragen kunnen ontvangen:</span><span class="sxs-lookup"><span data-stu-id="182c4-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="182c4-108">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="182c4-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="182c4-109">API-verbinding Webhook</span><span class="sxs-lookup"><span data-stu-id="182c4-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="182c4-110">HTTP-webhook</span><span class="sxs-lookup"><span data-stu-id="182c4-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="182c4-111">Hoewel onze voorbeelden Hallo gebruiken **aanvragen** worden geactiveerd, kunt u een van Hallo vermeld HTTP-triggers en alle identiek beginselen toohello andere triggertypen.</span><span class="sxs-lookup"><span data-stu-id="182c4-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="182c4-112">Een HTTP-eindpunt voor uw logische app instellen</span><span class="sxs-lookup"><span data-stu-id="182c4-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="182c4-113">toocreate een HTTP-eindpunt toevoegen een trigger die inkomende aanvragen kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="182c4-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="182c4-114">Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="182c4-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="182c4-115">Ga tooyour logische app en open Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="182c4-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="182c4-116">Toevoegen van een trigger waarmee uw logische app inkomende aanvragen worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="182c4-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="182c4-117">Bijvoorbeeld, voeg Hallo **aanvragen** trigger tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="182c4-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="182c4-118">Onder **aanvraag hoofdtekst JSON-Schema**, kunt u eventueel een JSON-schema voor Hallo nettolading (gegevens), waarop u verwacht Hallo trigger tooreceive dat invoeren.</span><span class="sxs-lookup"><span data-stu-id="182c4-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="182c4-119">Dit schema Hallo designer gebruikt om tokens die uw logische app tooconsume, parse en de gegevens op te geven van Hallo trigger via uw werkstroom gebruiken kunt te genereren.</span><span class="sxs-lookup"><span data-stu-id="182c4-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="182c4-120">Informatie over [tokens die zijn gegenereerd op basis van de JSON-schema's](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="182c4-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="182c4-121">Geef voor dit voorbeeld Hallo-schema in Hallo ontwerpen weergegeven:</span><span class="sxs-lookup"><span data-stu-id="182c4-121">For this example, enter hello schema shown in hello designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Hallo aanvraagactie toevoegen][1]

    > [!TIP]
    > 
    > <span data-ttu-id="182c4-123">U kunt een schema voor een voorbeeld JSON-nettolading genereren vanuit een hulpprogramma zoals [jsonschema.net](http://jsonschema.net/), of in Hallo **aanvragen** trigger door te kiezen **gebruik voorbeeld nettolading toogenerate schema**.</span><span class="sxs-lookup"><span data-stu-id="182c4-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="182c4-124">Voer uw payload voorbeeld en kies **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="182c4-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="182c4-125">Bijvoorbeeld, de nettolading van dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="182c4-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="182c4-126">Dit schema genereert:</span><span class="sxs-lookup"><span data-stu-id="182c4-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="182c4-127">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="182c4-127">Save your logic app.</span></span> <span data-ttu-id="182c4-128">Onder **HTTP POST toothis URL**, u ziet nu een gegenereerde retouraanroep-URL, zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="182c4-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL van de gegenereerde retouraanroep voor het eindpunt](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="182c4-130">Deze URL bevat een Shared Access Signature (SAS)-sleutel in Hallo queryparameters die worden gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="182c4-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="182c4-131">U kunt ook Hallo HTTP-eindpunt-URL ophalen uit uw logische app overzicht in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="182c4-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="182c4-132">Onder **Trigger geschiedenis**, selecteer uw trigger:</span><span class="sxs-lookup"><span data-stu-id="182c4-132">Under **Trigger History**, select your trigger:</span></span>

    ![HTTP-eindpunt-URL ophalen uit Azure-portal][2]

    <span data-ttu-id="182c4-134">Of u kunt Hallo-URL ophalen door deze oproep te plaatsen:</span><span class="sxs-lookup"><span data-stu-id="182c4-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="182c4-135">Hallo HTTP-methode voor de trigger wijzigen</span><span class="sxs-lookup"><span data-stu-id="182c4-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="182c4-136">Standaard Hallo **aanvraag** trigger een HTTP POST-aanvraag verwacht, maar u kunt een andere HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="182c4-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="182c4-137">U kunt slechts één methodetype opgeven.</span><span class="sxs-lookup"><span data-stu-id="182c4-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="182c4-138">Op uw **aanvragen** activeren, kiest u **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="182c4-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="182c4-139">Open Hallo **methode** lijst.</span><span class="sxs-lookup"><span data-stu-id="182c4-139">Open hello **Method** list.</span></span> <span data-ttu-id="182c4-140">Selecteer voor dit voorbeeld **ophalen** zodat u kunt uw HTTP-eindpunt-URL later testen.</span><span class="sxs-lookup"><span data-stu-id="182c4-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="182c4-141">U kunt selecteren van een andere HTTP-methode of een aangepaste methode voor uw eigen logische app opgeven.</span><span class="sxs-lookup"><span data-stu-id="182c4-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![HTTP-methode wijzigen](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="182c4-143">Accepteren parameters via uw HTTP-eindpunt-URL</span><span class="sxs-lookup"><span data-stu-id="182c4-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="182c4-144">Als u wilt dat de HTTP-eindpunt-URL tooaccept parameters aanpassen relatieve pad van de trigger.</span><span class="sxs-lookup"><span data-stu-id="182c4-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="182c4-145">Op uw **aanvragen** activeren, kiest u **geavanceerde opties weergeven**.</span><span class="sxs-lookup"><span data-stu-id="182c4-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="182c4-146">Onder **methode**, dat u wilt dat uw aanvraag toouse Hallo HTTP-methode opgeven.</span><span class="sxs-lookup"><span data-stu-id="182c4-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="182c4-147">Selecteer voor dit voorbeeld Hallo **ophalen** methode, als u nog niet gedaan, hebt zodat u kunt uw HTTP-eindpunt-URL testen.</span><span class="sxs-lookup"><span data-stu-id="182c4-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="182c4-148">Wanneer u een relatief pad voor de trigger opgeeft, kunt u een HTTP-methode moet ook expliciet opgeven voor de trigger.</span><span class="sxs-lookup"><span data-stu-id="182c4-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="182c4-149">Onder **relatief pad**, geef Hallo relatief pad voor Hallo-parameter die de URL, bijvoorbeeld accepteren moet `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="182c4-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Hallo HTTP-methode en het relatieve pad voor de parameter opgeven](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="182c4-151">toouse Hallo parameter, het toevoegen van een **antwoord** actie tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="182c4-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="182c4-152">(Kies onder de trigger **nieuwe stap** > **een actie toevoegen** > **antwoord**)</span><span class="sxs-lookup"><span data-stu-id="182c4-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="182c4-153">In uw antwoord **hoofdtekst**, Hallo token voor Hallo-parameter die u hebt opgegeven in de trigger relatief pad opnemen.</span><span class="sxs-lookup"><span data-stu-id="182c4-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="182c4-154">Bijvoorbeeld: tooreturn `Hello {customerID}`, uw antwoord bijwerken **hoofdtekst** met `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="182c4-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="182c4-155">Hallo-lijst met dynamische inhoud moet worden weergegeven en weergeven van Hallo `customerID` token voor u tooselect.</span><span class="sxs-lookup"><span data-stu-id="182c4-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Parameter tooresponse hoofdtekst toevoegen](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="182c4-157">Uw **hoofdtekst** moet eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="182c4-157">Your **Body** should look like this example:</span></span>

    ![Antwoordtekst met de parameter](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="182c4-159">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="182c4-159">Save your logic app.</span></span> 

    <span data-ttu-id="182c4-160">De HTTP-eindpunt-URL bevat nu Hallo relatief pad, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="182c4-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="182c4-161">HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="182c4-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="182c4-162">tootest uw HTTP-eindpunt, kopiëren en plakken bijgewerkte URL naar een ander browservenster hello, maar vervang `{customerID}` met `123456`, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="182c4-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="182c4-163">Deze tekst moet worden weergegeven in uw browser:</span><span class="sxs-lookup"><span data-stu-id="182c4-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="182c4-164">Tokens die zijn gegenereerd op basis van de JSON-schema's voor uw logische app</span><span class="sxs-lookup"><span data-stu-id="182c4-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="182c4-165">Wanneer het bieden van een JSON-schema in uw **aanvragen** activeren, hello Logic App-ontwerper-tokens gegenereerd voor de eigenschappen in dat het schema.</span><span class="sxs-lookup"><span data-stu-id="182c4-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="182c4-166">U kunt deze tokens vervolgens gebruiken voor het doorgeven van gegevens via uw logische app-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="182c4-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="182c4-167">Voor dit voorbeeld als u Hallo toevoegt `title` en `name` eigenschappen tooyour JSON-schema, hun tokens zijn nu beschikbaar toouse in latere werkstroomstappen.</span><span class="sxs-lookup"><span data-stu-id="182c4-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="182c4-168">Hier volgt Hallo voltooid JSON-schema:</span><span class="sxs-lookup"><span data-stu-id="182c4-168">Here is hello complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="182c4-169">Geneste werkstromen voor logic apps maken</span><span class="sxs-lookup"><span data-stu-id="182c4-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="182c4-170">U kunt werkstromen in uw logische app nesten door toe te voegen andere logic apps die aanvragen kunnen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="182c4-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="182c4-171">tooinclude deze logische apps toevoegen Hallo **Azure Logic Apps - kiest u een werkstroom Logic Apps** actie tooyour trigger.</span><span class="sxs-lookup"><span data-stu-id="182c4-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="182c4-172">U kunt selecteren van in aanmerking komende logic apps.</span><span class="sxs-lookup"><span data-stu-id="182c4-172">You can then select from eligible logic apps.</span></span>

![Een andere logische app toevoegen](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="182c4-174">Aanroepen of activeren van logische apps via HTTP-eindpunten</span><span class="sxs-lookup"><span data-stu-id="182c4-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="182c4-175">Nadat u uw HTTP-eindpunt hebt gemaakt, kunt u uw logische app via activeren een `POST` methode toohello volledige URL.</span><span class="sxs-lookup"><span data-stu-id="182c4-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="182c4-176">Logische apps hebben een ingebouwde ondersteuning voor directe toegang eindpunten.</span><span class="sxs-lookup"><span data-stu-id="182c4-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="182c4-177">Referentie-inhoud van een binnenkomende aanvraag</span><span class="sxs-lookup"><span data-stu-id="182c4-177">Reference content from an incoming request</span></span>

<span data-ttu-id="182c4-178">Als Hallo inhoud van het type is `application/json`, kunt u verwijzen naar eigenschappen van de binnenkomende aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="182c4-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="182c4-179">Anders wordt inhoud behandeld als één eenheid binaire dat u tooother API's kunt doorgeven.</span><span class="sxs-lookup"><span data-stu-id="182c4-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="182c4-180">Deze inhoud binnen de werkstroom Hallo tooreference, moet u die inhoud converteren.</span><span class="sxs-lookup"><span data-stu-id="182c4-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="182c4-181">Bijvoorbeeld, als u doorgeeft `application/xml` inhoud, kunt u `@xpath()` voor een extractie XPath of `@json()` voor het converteren van XML-tooJSON.</span><span class="sxs-lookup"><span data-stu-id="182c4-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="182c4-182">Meer informatie over [werken met inhoudstypen](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="182c4-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="182c4-183">tooget Hallo de uitvoer van een binnenkomende aanvraag opgegeven, kunt u Hallo `@triggerOutputs()` functie.</span><span class="sxs-lookup"><span data-stu-id="182c4-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="182c4-184">Hallo uitvoer lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="182c4-184">hello output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="182c4-185">Hallo tooaccess `body` eigenschap specifiek, kunt u Hallo `@triggerBody()` snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="182c4-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="182c4-186">Toorequests reageren</span><span class="sxs-lookup"><span data-stu-id="182c4-186">Respond toorequests</span></span>

<span data-ttu-id="182c4-187">U kunt toorespond toocertain aanvragen met een logische app door de aanroeper inhoud toohello terug te starten.</span><span class="sxs-lookup"><span data-stu-id="182c4-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="182c4-188">tooconstruct hello statuscode, koptekst en hoofdtekst voor uw antwoord, kunt u Hallo **antwoord** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="182c4-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="182c4-189">Deze actie kan overal voorkomen in uw logische app, niet alleen aan Hallo einde van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="182c4-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="182c4-190">Als uw logische app geen een **antwoord**, Hallo HTTP-eindpunt reageert *onmiddellijk* met een **202 geaccepteerde** status.</span><span class="sxs-lookup"><span data-stu-id="182c4-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="182c4-191">Ook voor de oorspronkelijke aanvraag tooget Hallo antwoord Hallo, alle stappen die nodig zijn voor antwoord Hallo moeten zijn voltooid binnen de Hallo [aanvraag time-outlimiet](./logic-apps-limits-and-config.md) tenzij u Hallo werkstroom als een geneste logische app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="182c4-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="182c4-192">Als er geen reactie binnen deze limiet gebeurt, inkomende hello-aanvraag een time-out optreedt en Hallo HTTP-antwoord ontvangt **408 time-out van de Client**.</span><span class="sxs-lookup"><span data-stu-id="182c4-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="182c4-193">Voor geneste logic apps blijft Hallo bovenliggende logische app toowait voor een antwoord pas voltooid, ongeacht hoeveel tijd vereist is.</span><span class="sxs-lookup"><span data-stu-id="182c4-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="182c4-194">Antwoord Hallo maken</span><span class="sxs-lookup"><span data-stu-id="182c4-194">Construct hello response</span></span>

<span data-ttu-id="182c4-195">U kunt meer dan één header en elk type inhoud in de antwoordtekst Hallo opnemen.</span><span class="sxs-lookup"><span data-stu-id="182c4-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="182c4-196">In ons voorbeeld antwoord Hallo header geeft aan dat antwoord Hallo type inhoud heeft `application/json`.</span><span class="sxs-lookup"><span data-stu-id="182c4-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="182c4-197">en Hallo hoofdtekst bevat `title` en `name`, op basis van de JSON-schema Hallo eerder bijgewerkt in verband met Hallo **aanvragen** trigger.</span><span class="sxs-lookup"><span data-stu-id="182c4-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![HTTP-antwoord actie][3]

<span data-ttu-id="182c4-199">Antwoorden hebben deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="182c4-199">Responses have these properties:</span></span>

| <span data-ttu-id="182c4-200">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="182c4-200">Property</span></span> | <span data-ttu-id="182c4-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="182c4-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="182c4-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="182c4-202">statusCode</span></span> |<span data-ttu-id="182c4-203">Hiermee geeft u Hallo HTTP-statuscode voor reageert toohello binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="182c4-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="182c4-204">Deze code kan geldige statuscode die met 2xx, 4xx of 5xx begint zijn.</span><span class="sxs-lookup"><span data-stu-id="182c4-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="182c4-205">Statuscodes 3xx zijn echter niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="182c4-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="182c4-206">Headers</span><span class="sxs-lookup"><span data-stu-id="182c4-206">headers</span></span> |<span data-ttu-id="182c4-207">Definieert een willekeurig aantal headers tooinclude Hallo reactie.</span><span class="sxs-lookup"><span data-stu-id="182c4-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="182c4-208">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="182c4-208">body</span></span> |<span data-ttu-id="182c4-209">Hiermee geeft u een instantie-object dat kan bestaan uit een tekenreeks, een JSON-object of zelfs binaire inhoud waarnaar wordt verwezen vanuit de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="182c4-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="182c4-210">Hier ziet u welke Hallo JSON-schema nu voor Hallo lijkt **antwoord** actie:</span><span class="sxs-lookup"><span data-stu-id="182c4-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="182c4-211">tooview hello voltooid JSON-definitie voor uw logische app, op Hallo Logic App-ontwerper, kies **codeweergave**.</span><span class="sxs-lookup"><span data-stu-id="182c4-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="182c4-212">Vragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="182c4-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="182c4-213">V: hoe zit URL beveiliging?</span><span class="sxs-lookup"><span data-stu-id="182c4-213">Q: What about URL security?</span></span>

<span data-ttu-id="182c4-214">A: azure genereert veilig logic app retouraanroep-URL's met behulp van een Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="182c4-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="182c4-215">Deze handtekening als een queryparameter passeert en moet worden gevalideerd voordat uw logische app kan worden gestart.</span><span class="sxs-lookup"><span data-stu-id="182c4-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="182c4-216">Azure genereert Hallo handtekening met een unieke combinatie van een geheime sleutel per logische app, Hallo triggernaam en Hallo-bewerking die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="182c4-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="182c4-217">Dus tenzij iemand toegang toohello geheime logic app-sleutel heeft, deze een geldige handtekening niet genereren kunnen.</span><span class="sxs-lookup"><span data-stu-id="182c4-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="182c4-218">Voor productie en beveiligde systemen kunt beter geen aanroepen van uw logische app rechtstreeks vanuit de browser Hallo omdat:</span><span class="sxs-lookup"><span data-stu-id="182c4-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="182c4-219">Hallo gedeelde toegangssleutel wordt weergegeven in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="182c4-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="182c4-220">U beheren geen beveiligde inhoud beleidsregels vanwege tooshared domeinen voor klanten is logische App.</span><span class="sxs-lookup"><span data-stu-id="182c4-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="182c4-221">V: kan ik meer HTTP-eindpunten configureren?</span><span class="sxs-lookup"><span data-stu-id="182c4-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="182c4-222">A: Ja, HTTP-eindpunten ondersteuning voor meer geavanceerde configuratie via [ **API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="182c4-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="182c4-223">Deze service biedt ook Hallo mogelijkheden voor u tooconsistently alle uw API's, met inbegrip van logische apps beheren, instellen van aangepaste domeinnamen, gebruik meer verificatiemethoden en meer, zoals:</span><span class="sxs-lookup"><span data-stu-id="182c4-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="182c4-224">Hallo aanvraagmethode wijzigen</span><span class="sxs-lookup"><span data-stu-id="182c4-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="182c4-225">Hallo URL-segmenten van Hallo aanvraag wijzigen</span><span class="sxs-lookup"><span data-stu-id="182c4-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="182c4-226">Instellen van uw API Management-domeinen in Hallo [Azure-portal](https://portal.azure.com/ "Azure-portal")</span><span class="sxs-lookup"><span data-stu-id="182c4-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="182c4-227">Beleid toocheck voor basisverificatie instellen</span><span class="sxs-lookup"><span data-stu-id="182c4-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="182c4-228">V: wat als Hallo schema gemigreerd van Hallo 1 December 2014 preview gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="182c4-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="182c4-229">A: Hier volgt een samenvatting over deze wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="182c4-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="182c4-230">Voorbeeld 1 december 2014</span><span class="sxs-lookup"><span data-stu-id="182c4-230">December 1, 2014 preview</span></span> | <span data-ttu-id="182c4-231">1 juni 2016</span><span class="sxs-lookup"><span data-stu-id="182c4-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="182c4-232">Klik op **HTTP-Listener** API-App</span><span class="sxs-lookup"><span data-stu-id="182c4-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="182c4-233">Klik op **handmatige trigger** (Er is geen API App vereist)</span><span class="sxs-lookup"><span data-stu-id="182c4-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="182c4-234">HTTP-Listener-instelling '*automatisch antwoord verzendt*'</span><span class="sxs-lookup"><span data-stu-id="182c4-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="182c4-235">Beide omvatten een **antwoord** actie of niet in de workflowdefinitie Hallo</span><span class="sxs-lookup"><span data-stu-id="182c4-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="182c4-236">Basisverificatie of OAuth-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="182c4-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="182c4-237">via API-beheer</span><span class="sxs-lookup"><span data-stu-id="182c4-237">via API Management</span></span> |
| <span data-ttu-id="182c4-238">Configureren van HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="182c4-238">Configure HTTP method</span></span> |<span data-ttu-id="182c4-239">Onder **geavanceerde opties weergeven**, kiest u een HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="182c4-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="182c4-240">Relatief pad configureren</span><span class="sxs-lookup"><span data-stu-id="182c4-240">Configure relative path</span></span> |<span data-ttu-id="182c4-241">Onder **geavanceerde opties weergeven**, voegt u een relatief pad</span><span class="sxs-lookup"><span data-stu-id="182c4-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="182c4-242">Verwijzing Hallo binnenkomende hoofdtekst via`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="182c4-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="182c4-243">Verwijzing via`@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="182c4-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="182c4-244">**HTTP-antwoord verzonden** actie op Hallo HTTP-Listener</span><span class="sxs-lookup"><span data-stu-id="182c4-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="182c4-245">Klik op **reageren tooHTTP aanvraag** (Er is geen API App vereist)</span><span class="sxs-lookup"><span data-stu-id="182c4-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="182c4-246">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="182c4-246">Get help</span></span>

<span data-ttu-id="182c4-247">tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="182c4-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="182c4-248">toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="182c4-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="182c4-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="182c4-249">Next steps</span></span>

* [<span data-ttu-id="182c4-250">Definities voor logische apps maken</span><span class="sxs-lookup"><span data-stu-id="182c4-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="182c4-251">Fouten en uitzonderingen verwerken</span><span class="sxs-lookup"><span data-stu-id="182c4-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
