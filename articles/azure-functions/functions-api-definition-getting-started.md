---
title: Aan de slag met OpenAPI metagegevens in Azure Functions | Microsoft Docs
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
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="33272-103">Maken van OpenAPI (Swagger) 2.0-metagegevens voor een functie-App (Preview)</span><span class="sxs-lookup"><span data-stu-id="33272-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="33272-104">Dit document begeleidt u bij de stap voor stap-proces voor het maken van de definitie van een OpenAPI voor een eenvoudige API gehost op Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="33272-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="33272-105">Wat is OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="33272-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="33272-106">[Metagegevens van swagger](http://swagger.io/) is een bestand dat u definieert de functionaliteit en bewerkingsmodi van uw API en biedt de mogelijkheid een functie die als host fungeert voor een REST-API om te worden verbruikt door een groot aantal andere software.</span><span class="sxs-lookup"><span data-stu-id="33272-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="33272-107">Aanbiedingen van Microsoft, zoals PowerApps en [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), evenals 3e partij ontwikkelaarstools zoals [Postman](https://www.getpostman.com/docs/importing_swagger) en [veel meer pakketten](http://swagger.io/tools/) alle toestaan uw API kunnen worden gebruikt met een Swagger-definitie.</span><span class="sxs-lookup"><span data-stu-id="33272-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="33272-108"><a name="prepare-function"></a>Het maken van een functie met een eenvoudige API</span><span class="sxs-lookup"><span data-stu-id="33272-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="33272-109">Voor het maken van de definitie van een OpenAPI eerst we een functie maken met een eenvoudige API.</span><span class="sxs-lookup"><span data-stu-id="33272-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="33272-110">Als u een API die wordt gehost op een functie-App al hebt, kunt u meteen naar de volgende sectie overslaan</span><span class="sxs-lookup"><span data-stu-id="33272-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="33272-111">Maak een nieuwe functie-App.</span><span class="sxs-lookup"><span data-stu-id="33272-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="33272-112">[Azure-portal](https://portal.azure.com)  >  `+ New` > Zoek naar 'Functie-App'</span><span class="sxs-lookup"><span data-stu-id="33272-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="33272-113">Maak een nieuwe functie van HTTP-trigger binnen uw nieuwe functie-App</span><span class="sxs-lookup"><span data-stu-id="33272-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="33272-114">De functie is al ingevuld met code voor het definiëren van een zeer eenvoudige REST-API.</span><span class="sxs-lookup"><span data-stu-id="33272-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="33272-115">Elke tekenreeks die is doorgegeven aan de functie als een queryparameter of de hoofdtekst is geretourneerd als "Hallo {invoer}"</span><span class="sxs-lookup"><span data-stu-id="33272-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="33272-116">Ga naar de `Integrate` tabblad van uw nieuwe functie van de HTTP-Trigger</span><span class="sxs-lookup"><span data-stu-id="33272-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="33272-117">Wisselknop `Allowed HTTP methods` naar`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="33272-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="33272-118">In `Selected HTTP methods` Schakel het selectievakje van elke bewerking met uitzondering van POST.</span><span class="sxs-lookup"><span data-stu-id="33272-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="33272-119">![Geselecteerde HTTP-methoden](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="33272-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="33272-120">Deze stap wordt later in uw API-definitie eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="33272-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="33272-121"><a name="enable"></a>Inschakelen van ondersteuning voor API-definitie</span><span class="sxs-lookup"><span data-stu-id="33272-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="33272-122">Navigeer naar `your function name`  >  `Platform Features`  >  `API Definition` 
 ![tabblad definitie.](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="33272-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="33272-123">Stel `API Definition Source` naar`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="33272-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="33272-124">In deze stap kunt u een reeks OpenAPI opties voor functie-App, met inbegrip van een eindpunt voor het hosten van een bestand OpenAPI uit van de functie App-domein, een inline-kopie van de [OpenAPI Editor](http://editor.swagger.io), en een generator Quick Start-definitie.</span><span class="sxs-lookup"><span data-stu-id="33272-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="33272-125">![Ingeschakelde definitie](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="33272-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="33272-126"><a name="create-definition"></a>Uw API-definitie maken uit een sjabloon</span><span class="sxs-lookup"><span data-stu-id="33272-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="33272-127">Klik op `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="33272-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="33272-128">Deze stap scant uw App in de functie voor het aantal HTTP-Trigger functies en maakt gebruik van de gegevens in functions.json om een document OpenAPI te genereren.</span><span class="sxs-lookup"><span data-stu-id="33272-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="33272-129">Een object van de bewerking wilt toevoegen`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="33272-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="33272-130">De Quick Start OpenAPI document is een overzicht van een volledige OpenAPI-document. Vereist meer metagegevens moet een volledige OpenAPI-definitie, zoals bewerking objecten en antwoord-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="33272-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="33272-131">Het onderstaande voorbeeld bewerking object heeft een gevulde sectie produceert/verbruikt, een parameter-object en een antwoordobject.</span><span class="sxs-lookup"><span data-stu-id="33272-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="33272-132">x-ms-overzicht bevat een weergavenaam in Logic Apps, stroom en PowerApps.</span><span class="sxs-lookup"><span data-stu-id="33272-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="33272-133">Bekijk [aanpassen van uw Swagger-definitie voor PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="33272-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="33272-134">Klik op `save` uw wijzigingen op te slaan ![Sjabloondefinitie toe te voegen](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="33272-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="33272-135"><a name="use-definition"></a>Met behulp van uw API-definitie</span><span class="sxs-lookup"><span data-stu-id="33272-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="33272-136">Kopieer uw `API definition URL` en plak deze in een nieuw browsertabblad om uw onbewerkte OpenAPI document weer te geven.</span><span class="sxs-lookup"><span data-stu-id="33272-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="33272-137">U kunt uw document OpenAPI importeren naar een willekeurig aantal hulpprogramma's voor het testen en integratie met behulp van deze URL.</span><span class="sxs-lookup"><span data-stu-id="33272-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="33272-138">Veel Azure-resources kunnen uw OpenAPI-document met behulp van de API-definitie-URL die is opgeslagen in de instellingen van de functie-toepassing automatisch geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="33272-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="33272-139">Als onderdeel van de `Function` API-definitie bron, wordt die url bijwerken voor u.</span><span class="sxs-lookup"><span data-stu-id="33272-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="33272-140"><a name="test-definition"></a>Met behulp van de Swagger-gebruikersinterface voor het testen van uw API-definitie</span><span class="sxs-lookup"><span data-stu-id="33272-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="33272-141">Er worden hulpprogramma's die zijn ingebouwd in de weergave van de gebruikersinterface van de editor voor de definitie van ingebed API testen.</span><span class="sxs-lookup"><span data-stu-id="33272-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="33272-142">Toevoegen van uw API-sleutel en gebruik vervolgens de `Try this operation` knop onder elke methode.</span><span class="sxs-lookup"><span data-stu-id="33272-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="33272-143">Het hulpprogramma voor uw API-definitie gebruikt om de aanvragen en geslaagde antwoorden wordt aangegeven dat de definitie van de juist is.</span><span class="sxs-lookup"><span data-stu-id="33272-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="33272-144">stappen:</span><span class="sxs-lookup"><span data-stu-id="33272-144">Steps:</span></span>

1. <span data-ttu-id="33272-145">Kopieer de functie API-sleutel</span><span class="sxs-lookup"><span data-stu-id="33272-145">Copy your function API key</span></span>
    1. <span data-ttu-id="33272-146">De API-sleutel vindt u in uw HTTP-activeringsfunctie onder `function name` > `Keys` > `Function Keys` 
   ![functietoets](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="33272-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="33272-147">Navigeer naar de `API Definition` pagina.</span><span class="sxs-lookup"><span data-stu-id="33272-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="33272-148">Klik op `Authenticate` en uw Function-API-sleutel toevoegen aan het object aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="33272-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="33272-149">![OpenAPI sleutel](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="33272-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="33272-150">Selecteer`/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="33272-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="33272-151">Klik op `Try it out` en voer een naam voor het testen</span><span class="sxs-lookup"><span data-stu-id="33272-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="33272-152">Er is een resultaat geslaagd onder `Pretty` 
 ![test API-definitie](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="33272-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="33272-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33272-153">Next steps</span></span>
* [<span data-ttu-id="33272-154">OpenAPI definitie in het overzicht van functies</span><span class="sxs-lookup"><span data-stu-id="33272-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="33272-155">Lees de volledige documentatie voor meer informatie over de OpenAPI worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="33272-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="33272-156">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="33272-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="33272-157">Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="33272-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="33272-158">GitHub-opslagplaats voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="33272-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="33272-159">Ga naar de GitHub-functies aan ons feedback geven over de API-definitie ondersteuning preview.</span><span class="sxs-lookup"><span data-stu-id="33272-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="33272-160">Maak een probleem met de GitHub voor alles wat die u graag zou zien bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="33272-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
