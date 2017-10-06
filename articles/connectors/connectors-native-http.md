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
# <a name="get-started-with-hello-http-action"></a>Aan de slag met Hallo HTTP-actie

Met HTTP-actie hello, kunt u werkstromen voor uw organisatie uitbreiden en tooany eindpunt communicatie via HTTP.

U kunt:

* Logic app-werkstromen waarmee (trigger) wordt geactiveerd wanneer een website die u beheert uitvalt maken.
* Communiceren tooany eindpunt via HTTP tooextend uw werkstromen bij andere services.

tooget gestart met Hallo HTTP-actie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Hallo HTTP-trigger te gebruiken
Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app. [Meer informatie over triggers](connectors-overview.md).

Hier volgt een van de voorbeeldreeks hoe tooset up Hallo HTTP activeren in Hallo Logic App-ontwerper.

1. Hallo HTTP-trigger toevoegen in uw logische app.
2. Hallo-parameters voor Hallo HTTP-eindpunt dat u wilt dat toopoll invullen.
3. Hallo terugkeerpatroon op hoe vaak het pollen moet wijzigen.

   Hallo logische app wordt nu gestart met inhoud die is geretourneerd tijdens elke controle.

   ![HTTP-trigger](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>De werking van de HTTP-trigger Hallo

Hallo HTTP-trigger stuurt een aanroep van tooHTTP-eindpunt op een terugkerend interval. Standaard een HTTP-antwoordcode die lager is dan 300 zorgt ervoor dat de toorun van een logische app. toospecify of Hallo logische app moet worden geactiveerd, u kunt Hallo logische app in de codeweergave bewerken en toevoegen van een voorwaarde die wordt geëvalueerd als na Hallo HTTP-aanroep. Hier volgt een voorbeeld van een HTTP-trigger wordt geactiveerd wanneer het Hallo geretourneerde statuscode is groter dan of gelijk zijn aan te`400`.

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

Volledige details over Hallo HTTP-trigger-parameters zijn beschikbaar op [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Gebruik Hallo HTTP-actie

Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app. 
[Meer informatie over acties](connectors-overview.md).

1. Kies **nieuwe stap** > **een actie toevoegen**.
3. Typ in het zoekvak Hallo actie, **http** toolist Hallo HTTP acties.
   
    ![Selecteer Hallo HTTP-actie](./media/connectors-native-http/using-action-1.png)

4. Voeg eventueel vereiste parameters voor Hallo HTTP-aanroep.
   
    ![Volledige Hallo HTTP-actie](./media/connectors-native-http/using-action-2.png)

5. Op de werkbalk Hallo designer **opslaan**. Uw logische app worden opgeslagen en gepubliceerd (geactiveerd) op Hallo hetzelfde moment.

## <a name="http-trigger"></a>HTTP-trigger
Hier vindt u details Hallo Hallo-trigger die ondersteuning biedt voor deze connector. Hallo HTTP-connector heeft een trigger.

| Trigger | Beschrijving |
| --- | --- |
| HTTP |Maakt een HTTP-aanroep en antwoordinhoud Hallo retourneert. |

## <a name="http-action"></a>HTTP-actie
Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector. Hallo HTTP-connector heeft een mogelijke actie.

| Actie | Beschrijving |
| --- | --- |
| HTTP |Maakt een HTTP-aanroep en antwoordinhoud Hallo retourneert. |

## <a name="http-details"></a>HTTP-details
Hallo volgende tabellen worden beschreven Hallo vereiste en optionele invoervelden voor Hallo actie en het bijbehorende uitvoerdetails hello, die gekoppeld zijn aan het Hallo-actie.

#### <a name="http-request"></a>HTTP-aanvraag
Hallo volgen invoervelden voor Hallo actie, waardoor een uitgaande HTTP-aanvraag.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Methode * |Methode |Hallo HTTP-term toouse |
| URI * |URI |Hallo URI voor Hallo HTTP-aanvraag |
| Headers |Headers |Een JSON-object van het HTTP-headers tooinclude |
| Hoofdtekst |Hoofdtekst |Hallo hoofdtekst van de HTTP-aanvraag |
| Authentication |Verificatie |De details in Hallo [verificatie](#authentication) sectie |

<br>

#### <a name="output-details"></a>Uitvoerdetails
Hallo hieronder vindt u uitvoerdetails voor Hallo HTTP-antwoord.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Headers |object |Antwoordheaders |
| Hoofdtekst |object |Response-object |
| Statuscode |int |HTTP-statuscode |

## <a name="authentication"></a>Authentication
Hallo Logic Apps-functie kunt u verschillende soorten verificatie op basis van HTTP-eindpunten toouse. U kunt deze verificatie Hallo **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, en  **[HTTP-Webhook](connectors-native-webhook.md)**  connectors. Hallo volgende typen verificatie worden geconfigureerd:

* [Basisverificatie](#basic-authentication)
* [Verificatie van clientcertificaten](#client-certificate-authentication)
* [Azure Active Directory (Azure AD) OAuth-verificatie](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Basisverificatie

Hallo na verificatieobject is nodig voor basisverificatie.
A * houdt in dat een vereist veld.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Type * |type |Type verificatie (moet `Basic` voor basisverificatie) |
| Gebruikersnaam * |gebruikersnaam |Gebruiker naam tooauthenticate |
| Wachtwoord * |wachtwoord |Wachtwoord tooauthenticate |

> [!TIP]
> Als u een wachtwoord dat niet uit de definitie van Hallo ophalen toouse wilt, gebruikt een `securestring` parameter en Hallo `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).

Bijvoorbeeld:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Clientverificatie via certificaat

Hallo is volgende verificatieobject nodig voor verificatie van clientcertificaten. A * houdt in dat een vereist veld.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Type * |type |Hallo type verificatie (moet `ClientCertificate` voor SSL-certificaten voor client) |
| PFX * |PFX |Hallo Base64-gecodeerde inhoud van Hallo Personal Information Exchange (PFX)-bestand |
| Wachtwoord * |wachtwoord |Hallo wachtwoord tooaccess Hallo PFX-bestand |

> [!TIP]
> een parameter die niet in de definitie van de Hallo na het opslaan van Hallo logische app leesbaar toouse, kunt u een `securestring` parameter en Hallo `@parameters()`  
>  [definitie Werkstroomfunctie](http://aka.ms/logicappdocs).

Bijvoorbeeld:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Azure AD-OAuth-verificatie
Hallo na verificatieobject is nodig voor Azure AD OAuth-verificatie. A * houdt in dat een vereist veld.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Type * |type |Hallo type verificatie (moet `ActiveDirectoryOAuth` voor Azure AD OAuth) |
| Tenant * |Tenant |Hallo tenant-id voor hello Azure AD-tenant |
| Doelgroep * |doelgroep |Hallo bron die u aanvraagt autorisatie toouse. Bijvoorbeeld: `https://management.core.windows.net/` |
| Client -ID * |clientId |Hallo van client-id voor de toepassing hello Azure AD |
| Geheim * |Geheim |Hallo geheim van Hallo-client die Hallo-token aanvraagt |

> [!TIP]
> U kunt een `securestring` parameter en Hallo `@parameters()` [definitie Werkstroomfunctie](http://aka.ms/logicappdocs) toouse een parameter die niet leesbaar is in definitie van de Hallo nadat ze zijn opgeslagen.
> 
> 

Bijvoorbeeld:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt verkennen Hallo van andere beschikbare connectors in Logic Apps door te kijken onze [API's lijst](apis-list.md).

