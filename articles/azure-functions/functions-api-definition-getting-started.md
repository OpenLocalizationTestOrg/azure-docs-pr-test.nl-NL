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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Maken van OpenAPI (Swagger) 2.0-metagegevens voor een functie-App (Preview)

Dit document begeleidt u bij Hallo stapsgewijze proces voor het maken van de definitie van een OpenAPI voor een eenvoudige API gehost op Azure Functions.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Wat is OpenAPI (Swagger)?
[Metagegevens van swagger](http://swagger.io/) is een bestand dat Hallo-functionaliteit definieert en biedt de mogelijkheid een functie die als host fungeert voor een REST-API-toobe gebruikt door een groot aantal andere software modi van uw API wordt uitgevoerd. Aanbiedingen van Microsoft, zoals PowerApps en [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), evenals 3e partij ontwikkelaarstools zoals [Postman](https://www.getpostman.com/docs/importing_swagger) en [veel meer pakketten](http://swagger.io/tools/) alle toestaan uw API-toobe gebruikt met een Swagger-definitie.

## <a name="prepare-function"></a>Het maken van een functie met een eenvoudige API
  de definitie van een OpenAPI toocreate, moeten we eerst toocreate een functie met een eenvoudige API. Als u een API die wordt gehost op een functie-App al hebt, kunt u de volgende sectie rechte toohello overslaan
1. Maak een nieuwe functie-App.
    1. [Azure-portal](https://portal.azure.com)  >  `+ New` > Zoek naar 'Functie-App'
1. Maak een nieuwe functie van HTTP-trigger binnen uw nieuwe functie-App
    1. De functie is al ingevuld met code voor het definiëren van een zeer eenvoudige REST-API.
    1. Elke tekenreeks toohello functie doorgegeven als een queryparameter of Hallo hoofdtekst geretourneerd als "Hallo {invoer}"
1. Ga toohello `Integrate` tabblad van uw nieuwe functie van de HTTP-Trigger
    1. Wisselknop `Allowed HTTP methods` te`Selected methods`
    1. In `Selected HTTP methods` Schakel het selectievakje van elke bewerking met uitzondering van POST.
    ![Geselecteerde HTTP-methoden](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Deze stap wordt later in uw API-definitie eenvoudiger.

## <a name="enable"></a>Inschakelen van ondersteuning voor API-definitie
1. Navigeer te`your function name` > `Platform Features` > `API Definition`
![tabblad definitie.](./media/functions-api-definition-getting-started/definitiontab.png)
1. Stel `API Definition Source` te`Function (preview)`
    1. In deze stap kunt u een reeks OpenAPI opties voor functie-App, met inbegrip van een eindpunt toohost een OpenAPI-bestand van de functie-App-domein, een inline-kopie van Hallo [OpenAPI Editor](http://editor.swagger.io), en een generator Quick Start-definitie.
![Ingeschakelde definitie](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Uw API-definitie maken uit een sjabloon
1. Klik op `Generate API Definition template`
    1. Deze stap uw App in de functie voor het aantal HTTP-Trigger functies gescand en Hallo info in functions.json toogenerate een document OpenAPI gebruikt.
1. Een object van de bewerking te toevoegen`paths: /api/yourfunctionroute post:`
    1. Hallo Quick Start OpenAPI document is een overzicht van een volledige OpenAPI-document. Vereist meer metagegevens toobe volledige OpenAPI definitie bewerking objecten en antwoord-sjablonen.
    1. onderstaande Hallo voorbeeld bewerking-object heeft een gevulde sectie produceert/verbruikt, een parameter-object en een antwoordobject.
    
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
    > Bekijk [aanpassen van uw Swagger-definitie voor PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn meer.

1. Klik op `save` toosave uw wijzigingen ![Sjabloondefinitie toe te voegen](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Met behulp van uw API-definitie
1. Kopieer uw `API definition URL` en plak deze in een nieuwe browser tabblad tooview uw onbewerkte OpenAPI-document.
1. U kunt het nummer van uw OpenAPI document tooany van hulpprogramma's voor het testen en integratie met gebruikmaking van die URL importeren.
    1. Veel Azure-resources zijn kunt tooautomatically importeren uw OpenAPI-document met behulp van API-definitie-URL die is opgeslagen in de instellingen van de functie toepassing hello. Als onderdeel van het Hallo `Function` API-definitie bron, wordt die url bijwerken voor u.


## <a name="test-definition"></a>Met behulp van Hallo Swagger-gebruikersinterface tootest uw API-definitie
Er worden hulpprogramma's die zijn ingebouwd in toohello UI weergave van Hallo ingebed API-definitie editor wordt getest. Toevoegen van uw API-sleutel en gebruik vervolgens Hallo `Try this operation` knop onder elke methode. Hallo tool gebruikt de API-definitie tooformat Hallo aanvragen en antwoorden geslaagde wordt aangegeven dat de definitie van de juist is.

### <a name="steps"></a>stappen:

1. Kopieer de functie API-sleutel
    1. Hallo API-sleutel vindt u in uw HTTP-activeringsfunctie onder `function name` > `Keys` > `Function Keys` 
   ![functietoets](./media/functions-api-definition-getting-started/functionkey.png)
1. Navigeer toohello `API Definition` pagina.
    1. Klik op `Authenticate` en voeg uw beveiligingsobject Function-API-sleutel toohello Hallo bovenaan.
  ![OpenAPI sleutel](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Selecteer`/api/yourfunctionroute` > `POST`
1. Klik op `Try it out` en voer een naam tootest
1. Er is een resultaat geslaagd onder `Pretty` 
 ![test API-definitie](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Volgende stappen
* [OpenAPI definitie in het overzicht van functies](functions-api-definition.md)
  * Hallo volledige documentatie voor meer informatie over OpenAPI ondersteuning te lezen.
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)  
  * Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.
* [GitHub-opslagplaats voor Azure Functions](https://github.com/Azure/Azure-Functions/)
  * Bekijk Hallo functies GitHub toogive ons feedback op Hallo API-definitie ondersteuning preview. Maak een probleem met de GitHub voor alles wat die u toosee bijgewerkt dat wilt.
