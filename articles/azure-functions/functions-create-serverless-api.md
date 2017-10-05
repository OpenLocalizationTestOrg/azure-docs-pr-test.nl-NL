---
title: Maken van een zonder Server API met behulp van Azure Functions | Microsoft Docs
description: Het maken van een zonder Server API met behulp van Azure Functions
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Een zonder Server API met behulp van Azure Functions maken

In deze zelfstudie leert u hoe Azure-functies kunt u zeer schaalbare API's maken. Azure Functions wordt geleverd met een verzameling van ingebouwde HTTP-triggers en bindingen die gemakkelijk te maken van een eindpunt in verschillende talen, waaronder Node.JS, C# en meer. In deze zelfstudie maakt gaat u een HTTP-trigger voor het afhandelen van bepaalde acties in uw API-ontwerp aanpassen. U wordt ook voorbereiden voor uw API groeiende door integratie met Azure Functions-proxy's en het instellen van mock-API's. Dit alles wordt gerealiseerd boven op de compute-functies zonder server omgeving, zodat u geen zorgen te hoeven maken over het schalen van resources - u kunt alleen zich richten op uw API-logica.

## <a name="prerequisites"></a>Vereisten 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

De resulterende functie wordt gebruikt voor de rest van deze zelfstudie.

### <a name="sign-in-to-azure"></a>Aanmelden bij Azure

Open de Azure-portal. Om dit te doen, moet u zich aanmelden bij [https://portal.azure.com](https://portal.azure.com) met uw Azure-account.

## <a name="customize-your-http-function"></a>Aanpassen van uw HTTP-functie

Uw HTTP-geactiveerde-functie is standaard geconfigureerd voor het accepteren van een HTTP-methode. Er is ook een standaard-URL van het formulier `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Als u de Quick Start, vervolgens gevolgd `<funcname>` waarschijnlijk ziet er ongeveer zo 'HttpTriggerJS1'. In deze sectie, wijzigt u de functie zodat deze alleen reageert op GET-aanvragen op basis van `/api/hello` in plaats daarvan te routeren. 

Navigeer naar de functie in de Azure portal. Selecteer **integreren** in de linkernavigatiebalk.

![Aanpassen van een HTTP-functie](./media/functions-create-serverless-api/customizing-http.png)

Gebruik de instellingen van de HTTP-trigger zoals opgegeven in de tabel.

| Veld | Voorbeeldwaarde | Beschrijving |
|---|---|---|
| Toegestane HTTP-methoden | Geselecteerde methoden | Hiermee wordt bepaald welke HTTP-methoden kunnen worden gebruikt voor deze functie aanroepen |
| Geselecteerde HTTP-methoden | TOEVOEGEN | Hiermee kunt u alleen geselecteerde HTTP-methoden moeten worden gebruikt voor deze functie aanroepen |
| Routesjabloon | uit | Bepaalt welke route wordt gebruikt voor deze functie aanroepen |

Opmerking die u niet de `/api` pad-voorvoegsel op in de Routesjabloon baseren als dit wordt verwerkt door een algemene instelling.

Klik op **Opslaan**.

U kunt meer informatie over het aanpassen van HTTP-functies in [bindingen van Azure Functions HTTP- en webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Uw API testen

De functie voor het werken met de nieuwe API-gebied vervolgens testen.

Ga terug naar de pagina ontwikkeling door te klikken op de functienaam in de linkernavigatiebalk.

Klik op **ophalen van de functie URL** en kopieer de URL. U ziet dat deze gebruikmaakt van de `/api/hello` nu routeren.

Kopieer de URL naar een nieuw browsertabblad of uw voorkeur REST-client. Browsers wordt GET standaard gebruikt.

De functie uitvoeren en controleren of deze werkt. Mogelijk moet u de parameter 'name' opgeven als een queryreeks om te voldoen aan de Quick Start-code.

U kunt ook proberen het aanroepen van het eindpunt met een andere HTTP-methode om te bevestigen dat de functie niet wordt uitgevoerd. Hiervoor moet u een REST-client, zoals cURL, Postman of Fiddler gebruiken.

## <a name="proxies-overview"></a>Overzicht van proxy 's

U kunt uw API via een proxy wordt surface in de volgende sectie. Azure Functions-proxy's is een preview-functie waarmee u aanvragen doorsturen naar andere bronnen. U definieert een HTTP-eindpunt net zoals met HTTP-trigger, maar in plaats van het schrijven van code voor het uitvoeren als dat eindpunt wordt aangeroepen, u een URL naar een externe implementatie opgeven. Hiermee kunt u meerdere API bronnen in één API-gebied op die clients gebruiken voor eenvoudige opstellen. Dit is vooral handig als u wilt maken van uw API als microservices.

Een proxy kan verwijzen naar een HTTP-resource, zoals:
- Azure Functions 
- API-apps in [-Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Docker-containers in [op Linux-App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Andere gehoste API

Zie voor meer informatie over proxy's, [werken met Azure Functions-proxy's (preview)].

## <a name="create-your-first-proxy"></a>Uw eerste proxy maken

In deze sectie maakt u een nieuwe proxy die als een frontend naar uw algehele API fungeert. 

### <a name="setting-up-the-frontend-environment"></a>De frontend-omgeving instellen

Herhaal de stappen voor het [maken van een functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) voor het maken van een nieuwe functie-app waarin u uw proxy maakt. Deze nieuwe app fungeert als de frontend voor onze API en de functie-app die u eerder hebt bewerkt fungeert als een back-end.

Navigeer naar uw nieuwe frontend functie-app in de portal.

Selecteer **instellingen**. Klik in-of uitschakelen **inschakelen Azure Functions-proxy's (preview)** naar 'Op'.

Selecteer **Platform instellingen** en kies **toepassingsinstellingen**.

Schuif omlaag naar **appinstellingen** en maak een nieuwe instelling met sleutel 'HELLO_HOST'. Stel de waarde voor de host van uw back-end-functie-app, zoals `<YourApp>.azurewebsites.net`. Dit is onderdeel van de URL die u eerder hebt gekopieerd bij het testen van uw HTTP-functie. U moet deze instelling in de configuratie later naar verwijzen.

> [!NOTE] 
> App-instellingen worden aanbevolen voor de configuratie van de host om te voorkomen dat een afhankelijkheid vastgelegde omgeving voor de proxy. Met behulp van appinstellingen, betekent dat u de proxyconfiguratie tussen omgevingen verplaatsen kunt en de omgeving-specifieke app-instellingen worden toegepast.

Klik op **Opslaan**.

### <a name="creating-a-proxy-on-the-frontend"></a>Maken van een proxy op de frontend

Ga terug naar uw frontend-functie-app in de portal.

Klik op het plusteken in de linkernavigatiebalk '+' naast 'Proxy's (preview)'.

![Maken van een proxy](./media/functions-create-serverless-api/creating-proxy.png)

Proxy-instellingen gebruiken die zijn opgegeven in de tabel.

| Veld | Voorbeeldwaarde | Beschrijving |
|---|---|---|
| Naam | HelloProxy | Een beschrijvende naam wordt alleen gebruikt voor beheer |
| Routesjabloon | / api/Hallo | Bepaalt welke route wordt gebruikt om aan te roepen via deze proxy |
| Back-end-URL | https://%HELLO_HOST%/API/Hello | Hiermee geeft u het eindpunt waarop de aanvraag via proxy moet |

Let op proxy's zorgt niet voor de `/api` basispad voorvoegsel en deze moet worden opgenomen in de Routesjabloon.

De `%HELLO_HOST%` syntaxis wordt verwezen naar de app-instelling die u eerder hebt gemaakt. De opgelost URL verwijst naar de oorspronkelijke functie.

Klik op **Create**.

U kunt uw nieuwe proxy uitproberen door te kopiëren van de Proxy-URL en testen van het in de browser of met uw favoriete HTTP-client.

## <a name="create-a-mock-api"></a>Een mock-API maken

Vervolgens gebruikt u een proxy voor het maken van een mock-API voor uw oplossing. Hierdoor kunnen client-ontwikkeling voor de voortgang, zonder dat de back-end volledig geïmplementeerd. Verderop in ontwikkeling, kan u een nieuwe functie-app die ondersteuning biedt voor deze logica maken en uw proxy omleiden naar deze.

Voor het maken van deze mock-API maken we een nieuwe proxy deze tijd met de [App Service-Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). Navigeer naar de functie-app in de portal om te beginnen. Selecteer **platformfuncties** en zoek **App Service-Editor**. Als u dit opent u de App Service-Editor in een nieuw tabblad.

Selecteer `proxies.json` in de linkernavigatiebalk. Dit is het bestand waarin de configuratie voor al uw proxy's worden opgeslagen. Als u een van de [fungeert implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), dit is het bestand dat u in bronbeheer wordt onderhouden. Zie voor meer informatie over dit bestand, [proxy's geavanceerde configuratie](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Als u tot nu toe hebt opgevolgd langs, worden uw proxies.json moet eruitzien als in het volgende:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Vervolgens voegt u uw mock-API. Vervang uw proxies.json-bestand met de volgende opties:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Hiermee wordt een nieuwe proxy 'GetUserByName', zonder de eigenschap backendUri toegevoegd. In plaats van een andere resource aanroept, wordt het standaardantwoord van proxy's met een onderdrukking antwoord gewijzigd. Aanvraag en -antwoord onderdrukkingen kunnen ook worden gebruikt in combinatie met een back-end-URL. Dit is vooral handig als proxy voor een oudere systeem, waarin u mogelijk wilt wijzigen, kopteksten, query's parameters, enzovoort. Zie voor meer informatie over aanvraag- en onderdrukkingen, [wijzigen aanvragen en antwoorden in de proxy's](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Uw mock API testen door het aanroepen van de `/api/users/{username}` -eindpunt met een browser of uw favoriete REST-client. Zorg ervoor dat u _{username}_ met de waarde van een tekenreeks die een gebruikersnaam vertegenwoordigt.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe ontwikkelen en aanpassen van een API van Azure Functions. U hebt ook geleerd hoe om meerdere API's, inclusief mocks, samenwerken als een geïntegreerde API-gebied. U kunt deze technieken gebruiken voor het bouwen van API's van elk complexiteit alle tijdens de uitvoering van het model zonder server compute verstrekt door Azure Functions.

De volgende verwijzingen te helpen bij het ontwikkelen van uw API verder:

- [Azure Functions HTTP- en webhook bindingen](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [werken met Azure Functions-proxy's (preview)]
- [Een Azure-functies-API (preview) documenteren](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[werken met Azure Functions-proxy's (preview)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
