---
title: aaaCreate een zonder Server API met behulp van Azure Functions | Microsoft Docs
description: Hoe toocreate een zonder Server API met behulp van Azure Functions
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
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Een zonder Server API met behulp van Azure Functions maken

In deze zelfstudie leert u hoe Azure-functies kunt u toobuild uiterst schaalbare API's. Azure Functions wordt geleverd met een verzameling van ingebouwde HTTP-triggers en bindingen zodat het eenvoudig tooauthor een eindpunt in verschillende talen, waaronder Node.JS, C# en meer. In deze zelfstudie gaat u een HTTP-trigger toohandle specifieke acties in uw ontwerp API aanpassen. U wordt ook voorbereiden voor uw API groeiende door integratie met Azure Functions-proxy's en het instellen van mock-API's. Dit alles wordt gerealiseerd boven op Hallo functies zonder server compute omgeving, dus u hebt geen tooworry over het schalen van resources: u kunt alleen zich richten op uw API-logica.

## <a name="prerequisites"></a>Vereisten 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

Hallo resulterende functie wordt gebruikt voor Hallo rest van deze zelfstudie.

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure

Open hello Azure-portal. toodo dit te melden[https://portal.azure.com](https://portal.azure.com) met uw Azure-account.

## <a name="customize-your-http-function"></a>Aanpassen van uw HTTP-functie

Uw HTTP-geactiveerde-functie is standaard geconfigureerd tooaccept alle HTTP-methode. Er is ook een standaard-URL van Hallo formulier `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Als u de Quick Start hello, vervolgens gevolgd `<funcname>` waarschijnlijk ziet er ongeveer zo 'HttpTriggerJS1'. In deze sectie, wijzigt u Hallo functie toorespond alleen tooGET aanvragen op basis van `/api/hello` in plaats daarvan te routeren. 

Navigeer tooyour-functie in hello Azure-portal. Selecteer **integreren** in Hallo linkernavigatiebalk.

![Aanpassen van een HTTP-functie](./media/functions-create-serverless-api/customizing-http.png)

De HTTP-trigger-instellingen zoals opgegeven in de tabel hello gebruiken.

| Veld | Voorbeeldwaarde | Beschrijving |
|---|---|---|
| Toegestane HTTP-methoden | Geselecteerde methoden | Bepaalt welke HTTP-methoden mogelijk gebruikte tooinvoke deze functie |
| Geselecteerde HTTP-methoden | TOEVOEGEN | Kan deze functie hebt gebruikt tooinvoke alleen geselecteerde HTTP-methoden toobe |
| Routesjabloon | uit | Hiermee wordt bepaald welke route gebruikte tooinvoke deze functie |

U hebt geen Hallo opgenomen opmerking `/api` baseren pad-voorvoegsel op in de Routesjabloon hello, als dit wordt verwerkt door een algemene instelling.

Klik op **Opslaan**.

U kunt meer informatie over het aanpassen van HTTP-functies in [bindingen van Azure Functions HTTP- en webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Uw API testen

Vervolgens testen uw toosee functie werken met de nieuwe API-gebied Hallo.

Navigeer terug toohello ontwikkeling pagina door te klikken op Hallo van de functienaam in de linkernavigatiebalk Hallo.

Klik op **ophalen van de functie URL** en kopieer Hallo-URL. U ziet dat deze gebruikmaakt van Hallo `/api/hello` nu routeren.

Kopieer Hallo-URL in een nieuw browsertabblad of uw voorkeur REST-client. Browsers wordt GET standaard gebruikt.

Hallo-functie uitvoeren en controleren of deze werkt. U moet mogelijk tooprovide Hallo 'name' parameter als een query-tekenreeks toosatisfy Hallo Quick Start-code.

U kunt ook proberen het Hallo-eindpunt met een andere HTTP-methode tooconfirm Hallo-functie is niet uitgevoerd wordt aangeroepen. Hiervoor moet u een REST-client, zoals cURL, Postman of Fiddler toouse.

## <a name="proxies-overview"></a>Overzicht van proxy 's

In de volgende sectie hello, wordt u uw API via een proxy surface. Azure Functions-proxy's is een preview-functie waarmee u tooforward aanvragen tooother resources. U net zoals een HTTP-eindpunt definiëren met HTTP-trigger, maar in plaats van het schrijven van code tooexecute wanneer dat eindpunt wordt aangeroepen, bieden u een externe URL tooa-implementatie. Hiermee kunt u meerdere API gegevensbronnen in een enkel API-gebied gemakkelijk voor clients tooconsume toocompose. Dit is vooral handig als u uw API als microservices toobuild wenst.

Een proxy kan verwijzen tooany HTTP-resource, zoals:
- Azure Functions 
- API-apps in [-Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Docker-containers in [op Linux-App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Andere gehoste API

toolearn meer informatie over proxy's, Zie [werken met Azure Functions-proxy's (preview)].

## <a name="create-your-first-proxy"></a>Uw eerste proxy maken

In deze sectie maakt u een nieuwe proxy die fungeert als een frontend tooyour algemene API. 

### <a name="setting-up-hello-frontend-environment"></a>Hallo frontend-omgeving instellen

Herhaal de stappen van de Hallo te[maken van een functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate een nieuwe functie-app in die u de proxy maakt. Deze nieuwe app fungeert als Hallo frontend voor onze API en Hallo functie-app die u eerder hebt bewerkt fungeert als een back-end.

Navigeer tooyour nieuwe frontend functie-app in Hallo-portal.

Selecteer **instellingen**. Klik in-of uitschakelen **inschakelen Azure Functions-proxy's (preview)** te 'op'.

Selecteer **Platform instellingen** en kies **toepassingsinstellingen**.

Schuif naar beneden te**appinstellingen** en maak een nieuwe instelling met sleutel 'HELLO_HOST'. De waarde toohello host van uw back-end-functie-app, zoals ingesteld `<YourApp>.azurewebsites.net`. Dit is onderdeel van het Hallo-URL die u eerder hebt gekopieerd bij het testen van uw HTTP-functie. U moet deze instelling in configuratie hello later naar verwijzen.

> [!NOTE] 
> App-instellingen worden aanbevolen voor Hallo host configuratie tooprevent een afhankelijkheid vastgelegde omgeving voor Hallo proxy. Met behulp van appinstellingen betekent dat u de proxyconfiguratie Hallo tussen omgevingen verplaatsen kunt en Hallo omgeving-specifieke app-instellingen worden toegepast.

Klik op **Opslaan**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Maken van een proxy op Hallo frontend

Navigeer terug tooyour frontend functie-app in Hallo-portal.

Klik in de linkernavigatiebalk hello, op Hallo plusteken '+' volgende te 'Proxy's (preview)'.

![Maken van een proxy](./media/functions-create-serverless-api/creating-proxy.png)

Proxy-instellingen zoals opgegeven in de tabel hello gebruiken.

| Veld | Voorbeeldwaarde | Beschrijving |
|---|---|---|
| Naam | HelloProxy | Een beschrijvende naam wordt alleen gebruikt voor beheer |
| Routesjabloon | / api/Hallo | Hiermee wordt bepaald welke route gebruikte tooinvoke deze proxy |
| Back-end-URL | https://%HELLO_HOST%/API/Hello | Hiermee wordt aangegeven Hallo eindpunt toowhich Hallo aanvraag moeten via proxy |

Houd er rekening mee dat proxy's geen Hallo biedt `/api` basispad voorvoegsel en deze moet worden opgenomen in de Routesjabloon Hallo.

Hallo `%HELLO_HOST%` syntaxis wordt verwezen naar Hallo app-instelling die u eerder hebt gemaakt. Hallo opgelost dat URL wordt de oorspronkelijke functie tooyour verwijzen.

Klik op **Create**.

U kunt uw nieuwe proxy uitproberen door Hallo Proxy URL kopiëren en testen van het in de browser Hallo of met uw favoriete HTTP-client.

## <a name="create-a-mock-api"></a>Een mock-API maken

Vervolgens gebruikt u een proxy toocreate een mock-API voor uw oplossing. Hierdoor kunnen client-ontwikkeling tooprogress zonder Hallo backend volledig geïmplementeerd. Verderop in ontwikkeling, kan u een nieuwe functie-app die ondersteuning biedt voor deze logica maken en uw proxy-tooit omleiden.

toocreate dit model API, maken we een nieuwe proxy met behulp van Hallo [App Service-Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget gestart, gaat u tooyour functie-app in Hallo-portal. Selecteer **platformfuncties** en zoek **App Service-Editor**. Als u dit opent u Hallo App Service-Editor in een nieuw tabblad.

Selecteer `proxies.json` in Hallo linkernavigatiebalk. Dit is Hallo-bestand waarin Hallo-configuratie voor al uw proxy's worden opgeslagen. Als u een Hallo [fungeert implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), dit is een Hallo u in broncodebeheer bewaart. Zie toolearn meer informatie over dit bestand [proxy's geavanceerde configuratie](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Als u tot nu toe hebt opgevolgd langs, worden uw proxies.json moet eruitzien als Hallo volgende:

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

Vervolgens voegt u uw mock-API. Uw bestand proxies.json vervangen door de volgende Hallo:

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

Hiermee wordt een nieuwe proxy 'GetUserByName' zonder Hallo backendUri eigenschap toegevoegd. In plaats van een andere resource aanroept, wijzigt het Hallo standaardreactie van proxy's met een onderdrukking antwoord. Aanvraag en -antwoord onderdrukkingen kunnen ook worden gebruikt in combinatie met een back-end-URL. Dit is vooral handig bij het gebruik van proxy tooa oude systeem, zult u toomodify headers, queryparameters, enz. toolearn meer informatie over aanvraag- en onderdrukkingen, Zie [wijzigen aanvragen en antwoorden in de proxy's](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Uw mock API testen door aanroepen Hallo `/api/users/{username}` -eindpunt met een browser of uw favoriete REST-client. Ervoor tooreplace worden _{username}_ met de waarde van een tekenreeks die een gebruikersnaam vertegenwoordigt.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd hoe toobuild en aanpassen van een API van Azure Functions. U hebt ook geleerd hoe toobring meerdere API's, waaronder mocks, samen als een geïntegreerde API-gebied. U kunt deze toobuild technieken uit API's van elk complexiteit, alle bij het uitvoeren op Hallo zonder server model verstrekt door Azure Functions compute.

Hallo te volgende verwijzingen helpen bij het ontwikkelen van uw API verder:

- [Azure Functions HTTP- en webhook bindingen](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [werken met Azure Functions-proxy's (preview)]
- [Een Azure-functies-API (preview) documenteren](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[werken met Azure Functions-proxy's (preview)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
