---
title: aaaWork met proxy's in Azure Functions | Microsoft Docs
description: Overzicht van hoe toouse Azure Functions-proxy's
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Werken met Azure Functions-proxy's (preview)

> [!NOTE] 
> Azure Functions-proxy's is momenteel in preview. Het is gratis terwijl in preview, maar standaardfuncties facturering tooproxy uitvoeringen toegepast. Zie voor meer informatie [prijzen van Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Functions-proxy's. Met deze functie kunt u eindpunten op de functie-app die zijn geïmplementeerd door een andere resource. Terwijl u nog steeds één API-gebied voor clients kunt u deze toobreak proxy's een grote API in meerdere functie-apps (zoals in een microservice-architectuur).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Azure Functions-proxy's inschakelen

Proxy's worden niet standaard ingeschakeld. U kunt de proxy's maken bij het Hallo-functie is uitgeschakeld, maar ze niet kan worden uitgevoerd. tooenable proxy's, Hallo te volgen:

1. Open Hallo [Azure-portal], en ga tooyour functie-app.
2. Selecteer **werken app-instellingen**.
3. Switch **inschakelen Azure Functions-proxy's (preview)** te**op**.

U kunt ook teruggaan hier tooupdate Hallo proxy runtime nieuwe functies beschikbaar komen.


## <a name="create"></a>Maken van een proxy

Deze sectie leest u hoe toocreate een proxy in Hallo Functions-portal.

1. Open Hallo [Azure-portal], en ga tooyour functie-app.
2. Selecteer in het linkerdeelvenster Hallo **nieuwe proxy**.
3. Geef een naam voor de proxy.
4. Hallo-eindpunt dat wordt weergegeven op deze functie-app configureren door te geven van Hallo **Routesjabloon** en **HTTP-methoden**. Deze parameters zich gedragen volgens toohello regels voor [HTTP-triggers].
5. Set Hallo **back-end-URL** tooanother eindpunt. Dit eindpunt kan een functie in een andere functie-app, of andere API kan zijn. Hallo waarde hoeft niet toobe statisch en deze kan verwijzen naar [toepassingsinstellingen] en [parameters uit de oorspronkelijke clientaanvraag Hallo].
6. Klik op **Create**.

De proxy bestaat nu als een nieuw eindpunt op functie-app. Vanuit het clientperspectief van een is het equivalent tooan HttpTrigger in Azure Functions. U kunt uw nieuwe proxy uitproberen door Hallo Proxy URL kopiëren en testen van het met uw favoriete HTTP-client.

## <a name="modify-requests-responses"></a>Aanvragen en antwoorden wijzigen

U kunt aanvragen tooand reacties van de back-end Hallo wijzigen met Azure Functions-proxy's. Deze transformaties kunnen variabelen gebruiken zoals gedefinieerd in [variabelen gebruiken].

### <a name="modify-backend-request"></a>Hallo back-end aanvraag wijzigen

Hallo back-end-aanvraag is standaard geïnitialiseerd als een kopie van de oorspronkelijke aanvraag Hallo. Bovendien toosetting Hallo back-end-URL, kunt u wijzigingen toohello HTTP-methode, headers en querytekenreeksparameters. Hallo gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen] en [parameters uit de oorspronkelijke clientaanvraag Hallo].

Er is momenteel geen portal ervaring voor het wijzigen van de back-end-aanvragen. toolearn hoe tooapply deze mogelijkheid van proxies.json, Zie [definiëren van een object requestOverrides].

### <a name="modify-response"></a>Hallo-antwoord worden gewijzigd

Standaard is antwoord Hallo-client als een kopie van het antwoord van de back-end Hallo geïnitialiseerd. U kunt wijzigingen toohello van code voor antwoordstatus, reden, kopteksten en hoofdtekst. Hallo gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen], [parameters uit de oorspronkelijke clientaanvraag Hallo], en [parameters uit het antwoord van de back-end Hallo].

Er is momenteel geen portal ervaring voor het wijzigen van antwoorden. toolearn hoe tooapply deze mogelijkheid van proxies.json, Zie [definiëren van een object responseOverrides].

## <a name="using-variables"></a>Variabelen gebruiken

Hallo-configuratie voor een proxy hoeft niet toobe statisch. U kunt deze voorwaarde toouse variabelen van de oorspronkelijke aanvraag hello, back-end-antwoord Hallo of toepassingsinstellingen.

### <a name="request-parameters"></a>Aanvraagparameters verwijzing

U kunt parameters van de aanvraag als eigenschap toohello back-end-URL-ingangen of als onderdeel van het wijzigen van aanvragen en antwoorden. Sommige parameters kunnen afhankelijk zijn van Hallo Routesjabloon die opgegeven in de base proxyconfiguratie Hallo en anderen kunnen afkomstig zijn uit de eigenschappen voor inkomende hello-aanvraag.

#### <a name="route-template-parameters"></a>Route-Sjabloonparameters
Parameters die worden gebruikt in de Routesjabloon Hallo zijn beschikbaar toobe waarnaar wordt verwezen door de naam. Hallo parameternamen zijn tussen accolades ({}).

Bijvoorbeeld, als een proxy heeft een Routesjabloon zoals `/pets/{petId}`, Hallo back-end-URL kan bevatten Hallo-waarde van `{petId}`als in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Als Routesjabloon hello wordt beëindigd in een jokerteken, zoals `/api/{*restOfPath}`, Hallo waarde `{restOfPath}` is een tekenreeksrepresentatie van Hallo resterende padsegmenten van inkomende hello-aanvraag.

#### <a name="additional-request-parameters"></a>Aanvullende aanvraagparameters
Bovendien toohello Sjabloonparameters routeren, Hallo volgende waarden kan worden gebruikt in configuratiewaarden:

* **{request.method}** : HTTP-methode die wordt gebruikt op de oorspronkelijke aanvraag Hallo Hallo.
* **{request.headers. \<HeaderName is opgeslagen\>}**: een header die kan worden gelezen vanaf de oorspronkelijke aanvraag Hallo. Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooread Hallo-header. Als het Hallo-header wordt niet geleverd op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.
* **{request.querystring. \<ParameterName\>}**: een queryreeksparameter opgeven die kan worden gelezen vanaf de oorspronkelijke aanvraag Hallo. Vervang  *\<ParameterName\>*  met Hallo naam van de gewenste tooread Hallo-parameter. Als het Hallo-parameter niet is opgenomen op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.

### <a name="response-parameters"></a>Verwijzing naar back-end antwoord parameters

Antwoord parameters kunnen worden gebruikt als onderdeel van het Hallo-antwoord toohello client wijzigen. Hallo volgende waarden kan worden gebruikt in configuratiewaarden:

* **{backend.response.statusCode}** : HTTP-statuscode geretourneerd op antwoord van de back-end Hallo Hallo.
* **{backend.response.statusReason}** : Hallo HTTP reden dat op antwoord van de back-end Hallo wordt geretourneerd.
* **{backend.response.headers. \<HeaderName is opgeslagen\>}**: een header die kan worden gelezen vanaf de back-end-antwoord Hallo. Vervang  *\<HeaderName is opgeslagen\>*  met de naam van Hallo header Hallo gewenste tooread. Als het Hallo-header wordt niet geleverd op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.

### <a name="use-appsettings"></a>Toepassingsinstellingen-verwijzing

U kunt ook verwijzen naar [toepassingsinstellingen gedefinieerd voor de functie-app Hallo](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) door Hallo Instellingsnaam tussen procenttekens (%).

Bijvoorbeeld, een back-end-URL van *https://%ORDER_PROCESSING_HOST%/api/orders* "% ORDER_PROCESSING_HOST %" vervangen door de waarde Hallo van Hallo ORDER_PROCESSING_HOST instelling zou hebben.

> [!TIP] 
> Toepassingsinstellingen voor back-end-hosts gebruiken wanneer u meerdere implementaties of testomgeving. Op die manier kunt u ervoor zorgen dat u altijd praten toohello terugkeren beëindigen voor die omgeving.

## <a name="advanced-configuration"></a>Geavanceerde configuratie

Hallo-proxy's die u configureert, worden opgeslagen in een proxies.json-bestand bevindt zich in de hoofdmap Hallo van een functie app-map. U handmatig dit bestand bewerken en implementeren als onderdeel van uw app als u een Hallo [implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) die functies worden ondersteund. Hallo-functie moet [ingeschakeld](#enable) voor Hallo bestand toobe verwerkt. 

> [!TIP] 
> Als u hebt niet een van de methoden voor het implementeren van hello, kunt u ook werken met Hallo proxies.json bestand in Hallo-portal. Ga tooyour functie-app, selecteer **platformfuncties**, en selecteer vervolgens **App Service-Editor**. U kunt op deze manier Hallo hele bestandsstructuur van uw app functie bekijken en brengt wijzigingen aan.

Proxies.JSON wordt gedefinieerd door een object proxy's, die bestaan uit benoemde proxy's en de bijbehorende definities. Eventueel, als uw editor ondersteunt, kunt u verwijzen naar een [JSON-schema](http://json.schemastore.org/proxies) voor de codevoltooiing. Een voorbeeld van een bestand lijkt Hallo volgende:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Elke proxy heeft een beschrijvende naam, zoals *proxy1* in het voorgaande voorbeeld Hallo. Hallo bijbehorende proxy definitie van object wordt gedefinieerd door Hallo volgende eigenschappen:

* **matchCondition**: vereist--een object definiëren Hallo-aanvragen die Hallo uitvoering van deze proxy activeren. Deze twee eigenschappen die worden gedeeld met bevat [HTTP-triggers]:
    * _methoden_: een matrix van Hallo HTTP-methoden die Hallo proxy reageert op. Als deze niet is opgegeven, reageert Hallo proxy tooall HTTP-methoden op Hallo route.
    * _route_: vereist--definieert Hallo-Routesjabloon beheren die aanvragen URL's van uw proxy reageert op. In tegenstelling tot in de HTTP-triggers is er geen standaardwaarde.
* **backendUri**: Hallo-URL van Hallo back-end-resource toowhich Hallo aanvraag moet via proxy. Deze waarde kan verwijzen naar toepassingsinstellingen en parameters van de oorspronkelijke clientaanvraag Hallo. Als deze eigenschap niet opgenomen is, wordt Azure Functions reageert met een HTTP 200 OK.
* **requestOverrides**: een object dat transformaties toohello back-end-aanvraag bepaalt. Zie [definiëren van een object requestOverrides].
* **responseOverrides**: een object dat transformaties toohello client antwoord bepaalt. Zie [definiëren van een object responseOverrides].

> [!NOTE] 
> Hallo route eigenschap Azure Functions-proxy's worden niet door Hallo routePrefix eigenschap van hostconfiguratie Hallo-functies. Als u een voorvoegsel zoals /api tooinclude wilt, moet worden opgenomen in Hallo route-eigenschap.

### <a name="requestOverrides"></a>Een object requestOverrides definiëren

Hallo requestOverrides object definieert toohello aanvraag voor wijzigingen als Hallo back-end bron wordt aangeroepen. Hallo-object wordt gedefinieerd door Hallo volgende eigenschappen:

* **backend.Request.Method**: Hallo HTTP-methode die is gebruikt toocall Hallo back-end.
* **backend.Request.QueryString. \<ParameterName\>**: een queryreeksparameter opgeven die kan worden ingesteld voor Hallo toohello back-end-aanroep. Vervang  *\<ParameterName\>*  met Hallo naam van de gewenste tooset Hallo-parameter. Als Hallo lege tekenreeks is opgegeven, wordt Hallo-parameter is niet opgenomen op Hallo back-end-aanvraag.
* **backend.Request.headers. \<HeaderName is opgeslagen\>**: een header die kan worden ingesteld voor Hallo toohello back-end-aanroep. Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooset Hallo-header. Als u een lege tekenreeks Hallo opgeeft, wordt Hallo-header is niet opgenomen op Hallo back-end-aanvraag.

Waarden kunnen verwijzen naar toepassingsinstellingen en parameters van de oorspronkelijke clientaanvraag Hallo.

Een voorbeeldconfiguratie lijkt Hallo volgende:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Een object responseOverrides definiëren

Hallo requestOverrides object definieert wijzigingen die zijn aangebracht toohello antwoord back toohello client is verstreken. Hallo-object wordt gedefinieerd door Hallo volgende eigenschappen:

* **response.statusCode**: Hallo HTTP status code toobe toohello client geretourneerd.
* **response.statusReason**: Hallo HTTP reden woordgroep toobe toohello client geretourneerd.
* **Response.BODY**: Hallo tekenreeksweergave van Hallo hoofdtekst toobe toohello client geretourneerd.
* **Response.headers. \<HeaderName is opgeslagen\>**: een koptekst voor Hallo antwoord toohello client kan worden ingesteld. Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooset Hallo-header. Als u een lege tekenreeks Hallo opgeeft, is niet Hallo-header op antwoord Hallo opgenomen.

Waarden kunnen verwijzen naar toepassingsinstellingen, parameters uit de oorspronkelijke clientaanvraag Hallo en parameters uit Hallo back-end-antwoord.

Een voorbeeldconfiguratie lijkt Hallo volgende:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> In dit voorbeeld Hallo-instantie wordt ingesteld rechtstreeks, dus er is geen `backendUri` eigenschap nodig is. Hallo-voorbeeld ziet u hoe u Azure Functions-proxy's kunt gebruiken voor mocking API's.

[Azure-portal]: https://portal.azure.com
[HTTP-triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definiëren van een object requestOverrides]: #requestOverrides
[definiëren van een object responseOverrides]: #responseOverrides
[toepassingsinstellingen]: #use-appsettings
[variabelen gebruiken]: #using-variables
[parameters uit de oorspronkelijke clientaanvraag Hallo]: #request-parameters
[parameters uit het antwoord van de back-end Hallo]: #response-parameters
