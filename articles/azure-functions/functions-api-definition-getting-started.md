---
title: aaaGetting gestart met OpenAPI Metadata in Azure Functions | Microsoft Docs
description: Aan de slag met ondersteuning voor OpenAPI in Azure Functions
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="b4269-103">Maken van OpenAPI (Swagger) 2.0-metagegevens voor een functie-App (Preview)</span><span class="sxs-lookup"><span data-stu-id="b4269-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="b4269-104">Dit document begeleidt u bij Hallo stapsgewijze proces voor het maken van de definitie van een OpenAPI voor een eenvoudige API gehost op Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b4269-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="b4269-105">Wat is OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="b4269-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="b4269-106">[Metagegevens van swagger](http://swagger.io/) is een bestand dat Hallo-functionaliteit definieert en biedt de mogelijkheid een functie die als host fungeert voor een REST-API-toobe gebruikt door een groot aantal andere software modi van uw API wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4269-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="b4269-107">Aanbiedingen van Microsoft, zoals PowerApps en [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), evenals 3e partij ontwikkelaarstools zoals [Postman](https://www.getpostman.com/docs/importing_swagger) en [veel meer pakketten](http://swagger.io/tools/) alle toestaan uw API-toobe gebruikt met een Swagger-definitie.</span><span class="sxs-lookup"><span data-stu-id="b4269-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="b4269-108"><a name="prepare-function"></a>Het maken van een functie met een eenvoudige API</span><span class="sxs-lookup"><span data-stu-id="b4269-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="b4269-109">de definitie van een OpenAPI toocreate, moeten we eerst toocreate een functie met een eenvoudige API.</span><span class="sxs-lookup"><span data-stu-id="b4269-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="b4269-110">Als u een API die wordt gehost op een functie-App al hebt, kunt u de volgende sectie rechte toohello overslaan</span><span class="sxs-lookup"><span data-stu-id="b4269-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="b4269-111">Maak een nieuwe functie-App.</span><span class="sxs-lookup"><span data-stu-id="b4269-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="b4269-112">[Azure-portal](https://portal.azure.com)  >  `+ New` > Zoek naar 'Functie-App'</span><span class="sxs-lookup"><span data-stu-id="b4269-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="b4269-113">Maak een nieuwe functie van HTTP-trigger binnen uw nieuwe functie-App</span><span class="sxs-lookup"><span data-stu-id="b4269-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="b4269-114">De functie is al ingevuld met code voor het definiëren van een zeer eenvoudige REST-API.</span><span class="sxs-lookup"><span data-stu-id="b4269-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="b4269-115">Elke tekenreeks toohello functie doorgegeven als een queryparameter of Hallo hoofdtekst geretourneerd als "Hallo {invoer}"</span><span class="sxs-lookup"><span data-stu-id="b4269-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="b4269-116">Ga toohello `Integrate` tabblad van uw nieuwe functie van de HTTP-Trigger</span><span class="sxs-lookup"><span data-stu-id="b4269-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="b4269-117">Wisselknop `Allowed HTTP methods` te`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="b4269-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="b4269-118">In `Selected HTTP methods` Schakel het selectievakje van elke bewerking met uitzondering van POST.</span><span class="sxs-lookup"><span data-stu-id="b4269-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="b4269-119">![Geselecteerde HTTP-methoden](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="b4269-120">Deze stap wordt later in uw API-definitie eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="b4269-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="b4269-121"><a name="enable"></a>Inschakelen van ondersteuning voor API-definitie</span><span class="sxs-lookup"><span data-stu-id="b4269-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="b4269-122">Navigeer te`your function name` > `Platform Features` > `API Definition`
![tabblad definitie.](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="b4269-123">Stel `API Definition Source` te`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="b4269-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="b4269-124">In deze stap kunt u een reeks OpenAPI opties voor functie-App, met inbegrip van een eindpunt toohost een OpenAPI-bestand van de functie-App-domein, een inline-kopie van Hallo [OpenAPI Editor](http://editor.swagger.io), en een generator Quick Start-definitie.</span><span class="sxs-lookup"><span data-stu-id="b4269-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="b4269-125">![Ingeschakelde definitie](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="b4269-126"><a name="create-definition"></a>Uw API-definitie maken uit een sjabloon</span><span class="sxs-lookup"><span data-stu-id="b4269-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="b4269-127">Klik op `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="b4269-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="b4269-128">Deze stap uw App in de functie voor het aantal HTTP-Trigger functies gescand en Hallo info in functions.json toogenerate een document OpenAPI gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b4269-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="b4269-129">Een object van de bewerking te toevoegen`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="b4269-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="b4269-130">Hallo Quick Start OpenAPI document is een overzicht van een volledige OpenAPI-document. Vereist meer metagegevens toobe volledige OpenAPI definitie bewerking objecten en antwoord-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b4269-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="b4269-131">onderstaande Hallo voorbeeld bewerking-object heeft een gevulde sectie produceert/verbruikt, een parameter-object en een antwoordobject.</span><span class="sxs-lookup"><span data-stu-id="b4269-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="b4269-132">x-ms-overzicht bevat een weergavenaam in Logic Apps, stroom en PowerApps.</span><span class="sxs-lookup"><span data-stu-id="b4269-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="b4269-133">Bekijk [aanpassen van uw Swagger-definitie voor PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="b4269-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="b4269-134">Klik op `save` toosave uw wijzigingen ![Sjabloondefinitie toe te voegen](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="b4269-135"><a name="use-definition"></a>Met behulp van uw API-definitie</span><span class="sxs-lookup"><span data-stu-id="b4269-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="b4269-136">Kopieer uw `API definition URL` en plak deze in een nieuwe browser tabblad tooview uw onbewerkte OpenAPI-document.</span><span class="sxs-lookup"><span data-stu-id="b4269-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="b4269-137">U kunt het nummer van uw OpenAPI document tooany van hulpprogramma's voor het testen en integratie met gebruikmaking van die URL importeren.</span><span class="sxs-lookup"><span data-stu-id="b4269-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="b4269-138">Veel Azure-resources zijn kunt tooautomatically importeren uw OpenAPI-document met behulp van API-definitie-URL die is opgeslagen in de instellingen van de functie toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b4269-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="b4269-139">Als onderdeel van het Hallo `Function` API-definitie bron, wordt die url bijwerken voor u.</span><span class="sxs-lookup"><span data-stu-id="b4269-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="b4269-140"><a name="test-definition"></a>Met behulp van Hallo Swagger-gebruikersinterface tootest uw API-definitie</span><span class="sxs-lookup"><span data-stu-id="b4269-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="b4269-141">Er worden hulpprogramma's die zijn ingebouwd in toohello UI weergave van Hallo ingebed API-definitie editor wordt getest.</span><span class="sxs-lookup"><span data-stu-id="b4269-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="b4269-142">Toevoegen van uw API-sleutel en gebruik vervolgens Hallo `Try this operation` knop onder elke methode.</span><span class="sxs-lookup"><span data-stu-id="b4269-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="b4269-143">Hallo tool gebruikt de API-definitie tooformat Hallo aanvragen en antwoorden geslaagde wordt aangegeven dat de definitie van de juist is.</span><span class="sxs-lookup"><span data-stu-id="b4269-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="b4269-144">stappen:</span><span class="sxs-lookup"><span data-stu-id="b4269-144">Steps:</span></span>

1. <span data-ttu-id="b4269-145">Kopieer de functie API-sleutel</span><span class="sxs-lookup"><span data-stu-id="b4269-145">Copy your function API key</span></span>
    1. <span data-ttu-id="b4269-146">Hallo API-sleutel vindt u in uw HTTP-activeringsfunctie onder `function name` > `Keys` > `Function Keys` 
   ![functietoets](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="b4269-147">Navigeer toohello `API Definition` pagina.</span><span class="sxs-lookup"><span data-stu-id="b4269-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="b4269-148">Klik op `Authenticate` en voeg uw beveiligingsobject Function-API-sleutel toohello Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b4269-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="b4269-149">![OpenAPI sleutel](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="b4269-150">Selecteer`/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="b4269-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="b4269-151">Klik op `Try it out` en voer een naam tootest</span><span class="sxs-lookup"><span data-stu-id="b4269-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="b4269-152">Er is een resultaat geslaagd onder `Pretty` 
 ![test API-definitie](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="b4269-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4269-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4269-153">Next steps</span></span>
* [<span data-ttu-id="b4269-154">OpenAPI definitie in het overzicht van functies</span><span class="sxs-lookup"><span data-stu-id="b4269-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="b4269-155">Hallo volledige documentatie voor meer informatie over OpenAPI ondersteuning te lezen.</span><span class="sxs-lookup"><span data-stu-id="b4269-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="b4269-156">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="b4269-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="b4269-157">Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="b4269-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="b4269-158">GitHub-opslagplaats voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b4269-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="b4269-159">Bekijk Hallo functies GitHub toogive ons feedback op Hallo API-definitie ondersteuning preview.</span><span class="sxs-lookup"><span data-stu-id="b4269-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="b4269-160">Maak een probleem met de GitHub voor alles wat die u toosee bijgewerkt dat wilt.</span><span class="sxs-lookup"><span data-stu-id="b4269-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
