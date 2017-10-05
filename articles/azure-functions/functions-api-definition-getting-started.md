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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Maken van OpenAPI (Swagger) 2.0-metagegevens voor een functie-App (Preview)

Dit document begeleidt u bij de stap voor stap-proces voor het maken van de definitie van een OpenAPI voor een eenvoudige API gehost op Azure Functions.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Wat is OpenAPI (Swagger)?
[Metagegevens van swagger](http://swagger.io/) is een bestand dat u definieert de functionaliteit en bewerkingsmodi van uw API en biedt de mogelijkheid een functie die als host fungeert voor een REST-API om te worden verbruikt door een groot aantal andere software. Aanbiedingen van Microsoft, zoals PowerApps en [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), evenals 3e partij ontwikkelaarstools zoals [Postman](https://www.getpostman.com/docs/importing_swagger) en [veel meer pakketten](http://swagger.io/tools/) alle toestaan uw API kunnen worden gebruikt met een Swagger-definitie.

## <a name="prepare-function"></a>Het maken van een functie met een eenvoudige API
  Voor het maken van de definitie van een OpenAPI eerst we een functie maken met een eenvoudige API. Als u een API die wordt gehost op een functie-App al hebt, kunt u meteen naar de volgende sectie overslaan
1. Maak een nieuwe functie-App.
    1. [Azure-portal](https://portal.azure.com)  >  `+ New` > Zoek naar 'Functie-App'
1. Maak een nieuwe functie van HTTP-trigger binnen uw nieuwe functie-App
    1. De functie is al ingevuld met code voor het definiëren van een zeer eenvoudige REST-API.
    1. Elke tekenreeks die is doorgegeven aan de functie als een queryparameter of de hoofdtekst is geretourneerd als "Hallo {invoer}"
1. Ga naar de `Integrate` tabblad van uw nieuwe functie van de HTTP-Trigger
    1. Wisselknop `Allowed HTTP methods` naar`Selected methods`
    1. In `Selected HTTP methods` Schakel het selectievakje van elke bewerking met uitzondering van POST.
    ![Geselecteerde HTTP-methoden](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Deze stap wordt later in uw API-definitie eenvoudiger.

## <a name="enable"></a>Inschakelen van ondersteuning voor API-definitie
1. Navigeer naar `your function name`  >  `Platform Features`  >  `API Definition` 
 ![tabblad definitie.](./media/functions-api-definition-getting-started/definitiontab.png)
1. Stel `API Definition Source` naar`Function (preview)`
    1. In deze stap kunt u een reeks OpenAPI opties voor functie-App, met inbegrip van een eindpunt voor het hosten van een bestand OpenAPI uit van de functie App-domein, een inline-kopie van de [OpenAPI Editor](http://editor.swagger.io), en een generator Quick Start-definitie.
![Ingeschakelde definitie](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Uw API-definitie maken uit een sjabloon
1. Klik op `Generate API Definition template`
    1. Deze stap scant uw App in de functie voor het aantal HTTP-Trigger functies en maakt gebruik van de gegevens in functions.json om een document OpenAPI te genereren.
1. Een object van de bewerking wilt toevoegen`paths: /api/yourfunctionroute post:`
    1. De Quick Start OpenAPI document is een overzicht van een volledige OpenAPI-document. Vereist meer metagegevens moet een volledige OpenAPI-definitie, zoals bewerking objecten en antwoord-sjablonen.
    1. Het onderstaande voorbeeld bewerking object heeft een gevulde sectie produceert/verbruikt, een parameter-object en een antwoordobject.
    
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
    >  x-ms-overzicht bevat een weergavenaam in Logic Apps, stroom en PowerApps.
    >
    > Bekijk [aanpassen van uw Swagger-definitie voor PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) voor meer informatie.

1. Klik op `save` uw wijzigingen op te slaan ![Sjabloondefinitie toe te voegen](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Met behulp van uw API-definitie
1. Kopieer uw `API definition URL` en plak deze in een nieuw browsertabblad om uw onbewerkte OpenAPI document weer te geven.
1. U kunt uw document OpenAPI importeren naar een willekeurig aantal hulpprogramma's voor het testen en integratie met behulp van deze URL.
    1. Veel Azure-resources kunnen uw OpenAPI-document met behulp van de API-definitie-URL die is opgeslagen in de instellingen van de functie-toepassing automatisch geïmporteerd. Als onderdeel van de `Function` API-definitie bron, wordt die url bijwerken voor u.


## <a name="test-definition"></a>Met behulp van de Swagger-gebruikersinterface voor het testen van uw API-definitie
Er worden hulpprogramma's die zijn ingebouwd in de weergave van de gebruikersinterface van de editor voor de definitie van ingebed API testen. Toevoegen van uw API-sleutel en gebruik vervolgens de `Try this operation` knop onder elke methode. Het hulpprogramma voor uw API-definitie gebruikt om de aanvragen en geslaagde antwoorden wordt aangegeven dat de definitie van de juist is.

### <a name="steps"></a>stappen:

1. Kopieer de functie API-sleutel
    1. De API-sleutel vindt u in uw HTTP-activeringsfunctie onder `function name` > `Keys` > `Function Keys` 
   ![functietoets](./media/functions-api-definition-getting-started/functionkey.png)
1. Navigeer naar de `API Definition` pagina.
    1. Klik op `Authenticate` en uw Function-API-sleutel toevoegen aan het object aan de bovenkant.
  ![OpenAPI sleutel](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Selecteer`/api/yourfunctionroute` > `POST`
1. Klik op `Try it out` en voer een naam voor het testen
1. Er is een resultaat geslaagd onder `Pretty` 
 ![test API-definitie](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Volgende stappen
* [OpenAPI definitie in het overzicht van functies](functions-api-definition.md)
  * Lees de volledige documentatie voor meer informatie over de OpenAPI worden ondersteund.
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)  
  * Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.
* [GitHub-opslagplaats voor Azure Functions](https://github.com/Azure/Azure-Functions/)
  * Ga naar de GitHub-functies aan ons feedback geven over de API-definitie ondersteuning preview. Maak een probleem met de GitHub voor alles wat die u graag zou zien bijgewerkt.
