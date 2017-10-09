---
title: aaaWorkflow acties en de triggers - Azure Logic Apps | Microsoft Docs
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Werkstroomacties en triggers voor Azure Logic Apps

Logische apps bestaan uit het triggers en acties. Er zijn zes soorten triggers. Elk type heeft een andere interface en ander gedrag. U kunt ook andere details leren door te kijken Hallo details van Hallo [werkstroom Definition Language](logic-apps-workflow-definition-language.md).  
  
Lees verder toolearn meer informatie over triggers en acties en hoe u kunt ze gebruiken toobuild logic apps tooimprove uw bedrijfsprocessen en werkstromen.  
  
### <a name="triggers"></a>Triggers  

Een trigger geeft Hallo-aanroepen die een uitvoering van uw logische app werkstroom kunnen initiëren. Hier volgen Hallo twee verschillende manieren tooinitiate een uitvoering van uw werkstroom:  
  
-   Een polling-trigger  

-   Een push-signaal - door de aanroepende Hallo [REST-API van Workflow](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Alle triggers bevatten deze op het hoogste niveau elementen:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Triggertypen en hun invoer  

U kunt deze typen triggers:
  
-   **Aanvraag** \- Hallo logische app maakt een eindpunt voor u toocall  
  
-   **Terugkeerpatroon** \- deze gebeurtenis wordt gestart op basis van een gedefinieerde planning  
  
-   **HTTP** \- een HTTP-web-eindpunt worden opgevraagd. Hallo HTTP-eindpunt moet voldoen tooa specifieke activerende contract \- met behulp van een 202\-asynchrone patroon, of door te retourneren van een matrix  
  
-   **ApiConnection** \- Polls zoals Hallo HTTP is geactiveerd, maar deze wordt gebruikgemaakt van Hallo [door Microsoft beheerde API's](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- opent een eindpunt, vergelijkbare toohello handmatige worden geactiveerd, maar deze ook illustreert tooa opgegeven URL tooregister en ongedaan maken  
  
-   **ApiConnectionWebhook** \- fungeert als HTTPWebhook trigger Hallo door gebruik te maken van Hallo door Microsoft beheerde API's       
    Elk triggertype heeft een andere set **invoer** het gedrag te definiëren.  
  
## <a name="request-trigger"></a>Aanvraag trigger  

Deze trigger fungeert als een eindpunt dat u via een HTTP-aanvraag tooinvoke uw logische app aanroepen. Een aanvraag-trigger ziet er in dit voorbeeld:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Er is ook een optionele eigenschap aangeroepen **schema**:  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|Schema|Nee|Een JSON-schema waarmee inkomende hello-aanvraag wordt gevalideerd. Is handig voor het volgende werkstroomstappen weten welke tooreference eigenschappen.|

tooinvoke dit eindpunt, moet u toocall hello *listCallbackUrl* API. Zie [REST-API van werkstroom](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Terugkeerpatroon trigger  

Een terugkeerpatroon trigger is die wordt uitgevoerd op basis volgens een ingesteld schema. Dergelijke trigger lijkt op het volgende voorbeeld:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Zoals u ziet, is een eenvoudige manier toorun een werkstroom.  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|frequency|Ja|Hoe vaak hello trigger wordt uitgevoerd. Gebruik slechts één van deze mogelijke waarden: seconde, minuut, uur, dag, week, maand of jaar|  
|interval|Ja|Het interval van Hallo opgegeven frequentie voor Hallo terugkeerpatroon|  
|startTime|Nee|Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.|  
|Tijdzone|Er is geen|Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.|  
  
U kunt ook een trigger toostart uitvoeren op een bepaald moment in toekomstige Hallo plannen. Bijvoorbeeld, als u wilt dat een wekelijkse rapporteren elke maandag toostart kunt u plannen Hallo logic app toostart elke maandag door het maken van Hallo trigger te volgen:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>HTTP-trigger  

HTTP-triggers peilen op een opgegeven eindpunt en Hallo antwoord toodetermine controleren of er Hallo werkstroom moet worden uitgevoerd. Hallo invoer object heeft Hallo set parameters vereist tooconstruct een HTTP-aanroep:  
  
|Elementnaam|Vereist|Beschrijving|Type|  
|----------------|------------|---------------|--------|  
|Methode|Ja|Een van de volgende HTTP-methoden Hallo: GET, POST, PUT, DELETE, PATCH of HEAD|Tekenreeks|  
|URI|Ja|Hallo http of https-eindpunt dat wordt aangeroepen. Maximum van 2 kB.|Tekenreeks|  
|Query 's|Nee|Een object die Hallo query parameters tooadd toohello URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|Object|  
|Headers|Nee|Object voor elk van de Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Object|  
|Hoofdtekst|Nee|Een object dat vertegenwoordigt Hallo nettolading dat toohello eindpunt wordt verzonden.|Object|  
|retryPolicy|Nee|Een object dat u kunt aanpassen Hallo gedrag voor het opnieuw op 4xx of 5xx-fouten.|Object|  
|Verificatie|Nee|Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd. Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority` deze waarde is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`|Object|  
  
de HTTP-trigger Hallo vereist Hallo HTTP API tooconform met een specifiek patroon toowork goed met uw logische app. Hiervoor Hallo velden te volgen:  
  
|Antwoord|Beschrijving|  
|------------|---------------|  
|Statuscode|Statuscode 200 \(OK\) toocause-run. Andere statuscode niet leiden tot een uitvoering.|  
|Probeer\-na header|Het aantal seconden tot Hallo logische app Hallo eindpunt opnieuw worden opgevraagd.|  
|Locatieheader|Hallo URL toocall op Hallo volgende polling-interval. Als niet wordt opgegeven, wordt de oorspronkelijke URL Hallo gebruikt.|  
  
Hier volgen enkele voorbeelden van andere problemen voor verschillende soorten aanvragen:  
  
|Reactiecode|Probeer\-na|Gedrag|  
|-----------------|----------------|------------|  
|200|\(geen\)|Niet een geldig worden geactiveerd, opnieuw proberen\-na is vereist of anders Hallo-engine nooit polls voor volgende Hallo-aanvraag.|  
|202|60|Hallo-werkstroom niet activeren. Hallo opnieuw probeert gebeurt in een minuut.|  
|200|10|Hallo-werkstroom uitvoert, en opnieuw controleren voor meer informatie over 10 seconden.|  
|400|\(geen\)|Onjuiste aanvraag, Hallo-werkstroom niet uitgevoerd. Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid Hallo gebruikt. Nadat het Hallo aantal nieuwe pogingen is bereikt, is Hallo trigger niet meer geldig.|  
|500|\(geen\)|Fout-server, worden niet uitgevoerd Hallo-werkstroom.  Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid Hallo gebruikt. Nadat het Hallo aantal nieuwe pogingen is bereikt, is Hallo trigger niet meer geldig.|  
  
Hallo uitvoerwaarden van een HTTP-trigger eruitzien als in dit voorbeeld:  
  
|Elementnaam|Beschrijving|Type|  
|----------------|---------------|--------|  
|Headers|Hallo-headers van Hallo http-antwoord.|Object|  
|Hoofdtekst|Hallo-hoofdtekst van Hallo http-antwoord.|Object|  
  
## <a name="api-connection-trigger"></a>API-verbinding activeren  

Hallo API verbinding trigger is vergelijkbaar toohello HTTP-trigger in de basisfunctionaliteit. Hallo-parameters voor het identificeren van Hallo actie zijn echter verschillend. Hier volgt een voorbeeld:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Elementnaam|Vereist|Type|Beschrijving|  
|----------------|------------|--------|---------------|  
|host|Ja||Hallo ApiApp gehost gateway en -id.|  
|Methode|Ja|Tekenreeks|Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|Query 's|Nee|Object|Vertegenwoordigt Hallo query parameters toobe toohello URL toegevoegd. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|  
|Headers|Nee|Object|Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.|  
|retryPolicy|Nee|Object|Hiermee kunt u toocustomize Hallo gedrag voor het opnieuw op 4xx of 5xx-fouten.|  
|Verificatie|Nee|Object|Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd. Zie voor meer informatie over dit object [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
Hallo-eigenschappen voor de host zijn:  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|API-runtimeUrl|Ja|Hallo-eindpunt van Hallo beheerde API.|  
|Verbindingsnaam||Moet worden verwijzing tooa parameter aangeroepen `$connection` en de naam Hallo Hallo managed API verbinding dat Hallo werkstroom gebruikt.|
  
Hallo uitvoerwaarden van een API-trigger verbinding zijn:
  
|Elementnaam|Type|Beschrijving|  
|----------------|--------|---------------|  
|Headers|Object|Hallo-headers van Hallo http-antwoord.|  
|Hoofdtekst|Object|Hallo-hoofdtekst van Hallo http-antwoord.|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook trigger  

Hallo HTTPWebhook trigger opent een eindpunt, vergelijkbare toohello handmatige trigger, maar Hallo HTTPWebhook trigger ook illustreert tooa opgegeven URL tooregister en ongedaan maken. Hier volgt een voorbeeld van wat een trigger HTTPWebhook als volgt uitzien:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Veel van deze gedeelten zijn optioneel en Hallo gedrag van Hallo Webhook is afhankelijk van welke gedeelten wordt geleverd of wordt weggelaten.  
Hallo-eigenschappen van een Webhook zijn als volgt:  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|abonneren|Nee|Hallo uitgaande aanvraag die wordt aangeroepen wanneer het Hallo-trigger wordt gemaakt en voert de initiële registratie Hallo.|  
|afmelden|Nee|Hallo uitgaande aanvraag wanneer Hallo trigger wordt verwijderd.|  
  
-   **Abonneren** Hallo uitgaand aanroep die toostart luisterende tooevents heeft gemaakt. Deze aanroep begint met het Hallo dezelfde set parameters die normale HTTP acties Hallo doen. Deze uitgaande aanroep uitgevoerd elke keer Hallo wijzigingen voor de workflow op elke manier, bijvoorbeeld wanneer Hallo referenties worden hersteld of Hallo trigger parameters wijzigen de invoer.
  
    toosupport dit aanroepen, er is een nieuwe functie: `@listCallbackUrl()`. Deze functie retourneert een unieke URL voor deze specifieke trigger in deze workflow. Deze vertegenwoordigt unieke id voor Hallo-eindpunten die gebruikmaken van Hallo Service REST Hallo.  
  
-   **Afmelden** wordt aangeroepen wanneer een bewerking renders deze trigger ongeldig, met inbegrip van:  
  
    -   Het verwijderen of Hallo trigger uitschakelen  
  
    -   Het verwijderen of uitschakelen van Hallo-werkstroom  
  
    -   Het verwijderen of uitschakelen van Hallo-abonnement  
  
    Hallo logic app roept automatisch Hallo actie opzeggen. Hallo-parameters zijn van de functie toothis Hallo dezelfde als Hallo HTTP-trigger.  
  
    Hallo zijn uitvoerwaarden van Hallo HTTPWebhook trigger Hallo-inhoud voor inkomende hello-aanvraag:  
  
|Elementnaam|Type|Beschrijving|  
|-----------------|--------|---------------|  
|Headers|Object|Hallo-headers van Hallo HTTP-aanvraag.|  
|Hoofdtekst|Object|Hallo-hoofdtekst van Hallo HTTP-aanvraag.|  

Limieten van een webhook-actie kunnen worden opgegeven in Hallo dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).
  

## <a name="conditions"></a>Voorwaarden  

Voor een trigger, kunt u een of meer voorwaarden toodetermine of Hallo werkstroom moet worden uitgevoerd of niet. Bijvoorbeeld:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

In dit geval Hallo rapport alleen triggers tijdens het Hallo-werkstroom `sendReports` parameter tootrue is ingesteld. Ten slotte voorwaarden kunnen verwijzen naar Hallo statuscode Hallo-trigger. U kan bijvoorbeeld ere van een werkstroom alleen als uw website een statuscode 500, als volgt retourneert:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Wanneer een expressie verwijst naar het Hallo-statuscode van Hallo trigger \(op elke manier\), Hallo standaardgedrag \(trigger alleen op 200 \(OK\) \) wordt vervangen. Bijvoorbeeld, als u tootrigger op zowel de statuscode 200 als de statuscode 201 wilt, hebt u tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` als de voorwaarde.  
  
## <a name="start-multiple-runs-for-a-request"></a>Meerdere wordt uitgevoerd voor een aanvraag starten

tookick uit meerdere wordt uitgevoerd voor een enkele aanvraag `splitOn` is handig, bijvoorbeeld, als u wilt toopoll een eindpunt dat meerdere nieuwe items tussen polling-intervallen kan hebben.
  
Met `splitOn`, geeft u de eigenschap Hallo binnen Hallo antwoord nettolading met Hallo-matrix van items die u wilt dat toouse toostart een uitvoering van het Hallo-trigger. Stel dat u hebt een API waarmee Hallo volgende antwoord geretourneerd:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Uw logische app moet alleen inhoud van de rijen hello, zodat u de trigger zoals in dit voorbeeld kunt maken:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Klik in de workflowdefinitie Hallo `@triggerBody().name` retourneert `mycoolrow` voor Hallo eerst uitvoert, en `another row` voor de tweede run Hallo. Hallo trigger uitvoer eruit zien in dit voorbeeld:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Als u in dat geval `SplitOn`, je geen toegang hebt Hallo-eigenschappen die buiten het Hallo-matrix in dit geval Hallo `Status` veld.  
  
> [!NOTE]  
> In dit voorbeeld gebruiken we Hallo `?` operator toobe kunnen tooavoid een fout als hello `Rows` eigenschap is niet aanwezig. 
  
## <a name="single-run-instance"></a>SIS uitvoeren

Triggers die een terugkeerpatroon eigenschap tooonly brand hebben als alle actieve sessies hebt voltooid, kunt u configureren. Als een geplande terugkeer optreedt terwijl er een uitgevoerd in voortgang is, wordt Hallo trigger wordt overgeslagen en wordt gewacht tot Hallo volgende geplande terugkeerpatroon interval toocheck opnieuw.

U kunt deze instelling door Hallo bewerking opties configureren:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Typen en invoer  

Er zijn veel verschillende soorten acties, elk met unieke gedrag. Verzameling acties mogelijk veel andere acties in zichzelf bevatten.

### <a name="standard-actions"></a>Standaardacties  

-   **HTTP** deze actie wordt een HTTP-web-eindpunt.  
  
-   **ApiConnection** \- deze bewerking gedraagt zich alsof Hallo HTTP-actie, maar gebruikt Hallo door Microsoft beheerde API's.  
  
-   **ApiConnectionWebhook** \- zoals HTTPWebhook, maar gebruikt Hallo door Microsoft beheerde API's.  
  
-   **Antwoord** \- deze actie wordt een antwoord voor een inkomend gesprek gedefinieerd.  
  
-   **Wacht** \- deze eenvoudige actie wacht een vast bedrag tijd of totdat een bepaalde tijd.  
  
-   **Werkstroom** \- deze actie vertegenwoordigt een geneste werkstroom.  

-   **De functie** \- deze actie vertegenwoordigt een Azure-functie.

### <a name="collection-actions"></a>Verzameling acties

-   **Bereik** \- deze actie is een logische groepering van andere acties.

-   **Voorwaarde** \- met deze actie evalueert een expressie en het bijbehorende resultaat vertakking hello wordt uitgevoerd.

-   **ForEach** \- samenvoegartikel hierdoor een matrix doorlopen en interne acties uitvoert voor elk item.

-   **Pas** \- binnenste acties van deze samenvoegartikel actie wordt uitgevoerd totdat een voorwaarde tootrue resulteert.
  
Elk type actie heeft een andere set **invoer** die een actie gedrag definiëren.  
  
## <a name="http-action"></a>HTTP-actie  

HTTP-acties aanroepen van een opgegeven eindpunt en Hallo antwoord toodetermine controleren of er Hallo werkstroom moet worden uitgevoerd. Hallo **invoer** object Hallo set parameters vereist tooconstruct Hallo HTTP-aanroep heeft:  
  
|Elementnaam|Vereist|Type|Beschrijving|  
|----------------|------------|--------|---------------|  
|Methode|Ja|Tekenreeks|Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|URI|Ja|Tekenreeks|Hallo http of https-eindpunt dat wordt aangeroepen. Maximale lengte is 2 kB.|  
|Query 's|Nee|Object|Hallo query parameters tooadd toohello URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|  
|Headers|Nee|Object|Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.|  
|retryPolicy|Nee|Object|Hiermee kunt u aanpassen Hallo opnieuw gedrag voor 4xx of 5xx-fouten.|  
|operationsOptions|Nee|Tekenreeks|Hallo set speciaal gedrag toooverride gedefinieerd.|  
|Verificatie|Nee|Object|Hallo-methode voor vertegenwoordigt die aanvraag Hallo moet worden geverifieerd. Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority`. Dit is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`|  
  
HTTP-acties \(en API-verbinding\) acties ondersteuning beleid voor opnieuw proberen. Een beleid voor opnieuw proberen is van toepassing toointermittent fouten, gekenmerkt als HTTP-status 408 429 en 5xx in toevoeging tooany verbindingsuitzonderingen-codes. Dit beleid wordt beschreven met Hallo *retryPolicy* object dat is gedefinieerd als volgt te werk:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Hallo-interval voor opnieuw proberen is opgegeven in Hallo ISO 8601-notatie. Dit interval heeft een standaard en de minimumwaarde van 20 seconden terwijl Hallo maximale waarde een uur is. Hallo standaard en maximum aantal pogingen een waarde is gelijk aan vier uur. Als de definitie voor nieuwe pogingen voor Hallo niet is opgegeven, een `fixed` strategie met een standaardwaarde opnieuw telling en het interval wordt gebruikt. beleid voor opnieuw proberen van toodisable hello, stel het type te`None`.  
  
Bijvoorbeeld hello volgende actie probeert opnieuw ophalen Hallo laatste nieuws twee keer als er onregelmatige problemen, voor een totaal van drie uitvoeringen, met een vertraging 30 seconden tussen elke poging:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Asynchrone patronen

Standaard ondersteunt alle HTTP-gebaseerde acties Hallo standaard asynchrone bewerking patroon. Dus als de externe server Hallo die Hallo-aanvraag aangeeft is geaccepteerd voor verwerking met een 202 \(geaccepteerde\) antwoord Hallo Logic Apps-engine houdt polling Hallo URL die is opgegeven in de locatie-header van het antwoord Hallo tot het bereiken van een terminal status \(niet\-202 antwoord\).  
  
toodisable hello asynchrone gedrag ingesteld eerder beschreven, een `DisableAsyncPattern` optie in Hallo actie invoer. In dit geval is Hallo-uitvoer van Hallo actie gebaseerd op Hallo initiële 202 reactie van Hallo-server.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Asynchrone limieten

Een asynchrone patroon worden de tijdsinterval duur tooa specifieke beperkt.  Als Hallo tijdsinterval is verstreken zonder dat een definitieve status bereikt, Hallo status van Hallo actie gemarkeerd `Cancelled` met de code `ActionTimedOut`.  Hallo limiet time-out is opgegeven in de ISO 8601-notatie.  Limieten kunnen worden opgegeven met de Hallo de volgende syntaxis:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API-verbinding  

API-verbinding is een actie die verwijst naar een connector door Microsoft beheerd.
Deze actie vereist een geldige verwijzing tooa-verbinding en informatie over het Hallo API en de vereiste parameters.

|Elementnaam|Vereist|Type|Beschrijving|  
|----------------|------------|--------|---------------|  
|host|Ja|Object|Hiermee geeft u Hallo connector informatie zoals Hallo runtimeUrl en verwijzing toohello connection-object|
|Methode|Ja|Tekenreeks|Een van de volgende HTTP-methoden Hallo: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|Pad|Ja|Tekenreeks|Hallo-pad van Hallo API-bewerking.|  
|Query 's|Nee|Object|Hallo query parameters tooadd toohello URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|  
|Headers|Nee|Object|Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u Hallo nettolading dat toohello eindpunt wordt verzonden.|  
|retryPolicy|Nee|Object|Hiermee kunt u aanpassen Hallo opnieuw gedrag voor 4xx of 5xx-fouten.|  
|operationsOptions|Nee|Tekenreeks|Hallo set speciaal gedrag toooverride gedefinieerd.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>API-verbinding webhook actie

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Limieten van een webhook-actie kunnen worden opgegeven in Hallo dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).
  
## <a name="response-action"></a>Antwoord actie  

Dit actietype Hallo volledige antwoord nettolading van een HTTP-aanvraag bevat en een statusCode, hoofdtekst en headers omvat:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
Hallo antwoord actie heeft speciale beperkingen die niet van toepassing tooother acties. Specifiek:  
  
-   Reacties kunnen niet in een definitie van een parallelle omdat een deterministische antwoord toohello binnenkomende aanvraag vereist is.  
  
-   Als een antwoord-actie is bereikt nadat inkomende hello-aanvraag heeft een antwoord ontvangen, Hallo actie wordt beschouwd als mislukt \(conflict\), en als gevolg hiervan Hallo uitvoeren `Failed`.  
  
-   Een werkstroom met reacties kan geen `splitOn` in de trigger omdat één aanroep ervoor zorgt veel wordt uitgevoerd dat. Dit moet als gevolg hiervan worden gevalideerd wanneer het Hallo-stroom is PUT en oorzaak is een ongeldige aanvraag.  
  
## <a name="wait-action"></a>Actie wachten  

Hallo `wait` actie onderbreekt de uitvoering van de werkstroom voor Hallo opgegeven interval. Bijvoorbeeld, toowait 15 minuten kunt u in dit fragment:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
U kunt ook toowait tot een bepaald moment, kunt u dit voorbeeld:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> Hallo wacht duur ofwel kan worden opgegeven met de Hallo **interval** object of Hallo **totdat** , maar niet beide.  
  
|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|interval|Nee|Object|Hallo wacht duur op basis van tijd.|  
|intervaleenheid|Ja|Tekenreeks|Een van deze intervallen: seconde, minuut, uur, dag, week, maand, jaar.|  
|interval aantal|Ja|Tekenreeks|De duur op basis van Hallo opgegeven interne eenheid.|  
|pas|Nee|Object|Hallo wacht duur op basis van een punt in tijd.|  
|Pas de timestamp|Ja|Tekenreeks|Tekenreeks &#124; Hallo punt in tijd in UTC wanneer Hallo wachttijd is verlopen.|  

## <a name="query-action"></a>Queryactie

Hallo `query` actie kunt u filteren op basis van een voorwaarde matrix. Bijvoorbeeld: tooselect getallen die groter zijn dan 2, u kunt gebruiken:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

de uitvoer van Hallo Hallo `query` actie is een matrix met elementen van de invoermatrix Hallo die voldoen aan de voorwaarde Hallo.

> [!NOTE]
> Als geen waarden voldoen aan Hallo `where` voorwaarde, hello resultaat is een lege matrix.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|Matrix|Hallo bronmatrix.|
|waar|Ja|Tekenreeks|Hallo voorwaarde tooapply tooeach element van de bronmatrix Hallo.|

## <a name="select-action"></a>Selecteer actie

Hallo `select` actie kunt u elk element van een matrix project in een nieuwe waarde.
Bijvoorbeeld, tooconvert een matrix van getallen in een matrix met objecten, kunt u het volgende gebruiken:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

uitvoer van Hallo Hallo `select` actie is een matrix met Hallo dezelfde kardinaliteit zoals Hallo invoermatrix, waarbij elk element omgezet als gedefinieerd door Hallo `select` eigenschap. Als het Hallo-invoer is een lege matrix, is Hallo uitvoer ook een lege matrix.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|Matrix|Hallo bronmatrix.|
|Selecteer|Ja|Alle|Hallo projectie tooapply tooeach element van de bronmatrix Hallo.|

## <a name="terminate-action"></a>Actie beëindigen

Hallo actie beëindigen stopt u de uitvoering van Hallo werkstroom uitvoert, wordt afgebroken onderweg acties en eventuele resterende acties wordt overgeslagen. Bijvoorbeeld, een reeks met de status tooterminate **mislukt**, kunt u Hallo volgende codefragment:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Reeds voltooide acties worden niet beïnvloed door Hallo actie beëindigen.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|runStatus|Ja|Tekenreeks|Hallo-doel status uitvoeren. Beide **mislukt** of **geannuleerd**.|
|runError|Nee|Object|Hallo foutgegevens. Alleen ondersteund wanneer **runStatus** te is ingesteld,**mislukt**.|
|runError code|Nee|Tekenreeks|Hallo foutcode uitvoeren.|
|runError bericht|Nee|Tekenreeks|Hallo foutbericht uitvoeren.|

## <a name="compose-action"></a>Actie opstellen

Hallo opstellen actie kunt u een willekeurig object samenstellen. Hallo-uitvoer van Hallo opstellen actie Hallo resultaat van evaluatie van de invoer is. Bijvoorbeeld, kunt u Hallo opstellen actie toomerge uitvoerwaarden van meerdere acties:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Hallo **opstellen** actie gebruikte tooconstruct uitvoer, met inbegrip van objecten, matrices en een ander type systeemeigen worden ondersteund door logische apps zoals XML en binaire kan zijn.

## <a name="table-action"></a>Tabel actie

Hallo `table` kunt u tooconvert een matrix van items in een **CSV** of **HTML** tabel.

Stel @triggerBody() is

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

En laat Hallo actie worden gedefinieerd als

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Hallo bovenstaande geeft als resultaat

<table><thead><tr><th>id</th><th>naam</th></tr></thead><tbody><tr><td>0</td><td>appels</td></tr><tr><td>1</td><td>appels</td></tr></tbody></table>"

In de volgorde toocustomize Hallo tabel kunt u expliciet Hallo kolommen opgeven. Bijvoorbeeld:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Hallo bovenstaande geeft als resultaat

<table><thead><tr><th>id maken</th><th>description</th></tr></thead><tbody><tr><td>0</td><td>nieuwe appels</td></tr><tr><td>1</td><td>nieuwe appels</td></tr></tbody></table>"

Als hello `from` eigenschapswaarde is een lege matrix, Hallo uitvoer is een lege tabel.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|Matrix|Hallo bronmatrix.|
|Indeling|Ja|Tekenreeks|Hallo-indeling, ofwel **CSV** of **HTML**.|
|Kolommen|Nee|Matrix|Hallo-kolommen. Hiermee kunt toooverride Hallo standaardvorm van Hallo tabel.|
|kolomkop|Nee|Tekenreeks|Hallo-header van Hallo-kolom.|
|waarde in de kolom|Ja|Tekenreeks|Hallo-waarde van Hallo-kolom.|

## <a name="workflow-action"></a>Werkstroomactie   

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|host-id|Ja|Tekenreeks|Hallo-bron-ID van dat u wilt dat toocall Hallo-werkstroom.|  
|host triggernaam|Ja|Tekenreeks|Hallo-naam van dat u wilt dat tooinvoke Hallo-trigger.|  
|Query 's|Nee|Object|Hallo query parameters tooadd toohello URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|  
|Headers|Nee|Object|Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u Hallo nettolading toohello eindpunt verzonden.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Een toegangscontrole wordt gemaakt op Hallo werkstroom \(meer specifiek, Hallo trigger\), wat betekent dat u moet toegang tot toohello werkstroom.  
  
Hallo levert van Hallo `workflow` actie zijn gebaseerd op wat u hebt gedefinieerd in Hallo `response` actie in Hallo onderliggende werkstroom. Als u nog geen gedefinieerd een `response` actie en klik vervolgens Hallo uitvoer leeg zijn.  

## <a name="function-action"></a>Functie actie   

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|functie-id|Ja|Tekenreeks|Hallo resource-ID van de gewenste tooinvoke Hallo-functie.|  
|Methode|Nee|Tekenreeks|Hallo HTTP-methode tooinvoke Hallo functie gebruikt. Dit is standaard `POST` als niet is opgegeven.|  
|Query 's|Nee|Object|Hallo query parameters tooadd toohello URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` toohello URL.|  
|Headers|Nee|Object|Hiermee geeft u elk Hallo headers die toohello-aanvraag is verzonden. Bijvoorbeeld: tooset Hallo taal en het type voor een aanvraag: `"headers" : { "Accept-Language": "en-us" }`.|  
|Hoofdtekst|Nee|Object|Hiermee geeft u Hallo nettolading toohello eindpunt verzonden.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Wanneer u Hallo logische app opslaat, voer we enkele controles van de functie Hallo waarnaar wordt verwezen:
-   U moet de functie voor toegang tot toohello toohave.
-   Alleen de standaard HTTP-trigger of algemene JSON webhook trigger is toegestaan.
-   Er mogen geen enkele route gedefinieerd.
-   Alleen 'functioneren' en 'anonymous' autorisatieniveau is toegestaan.

Hallo trigger-URL is opgehaald, in de cache opgeslagen en gebruikt tijdens runtime. Dus als een bewerking wordt ongeldig in de cache opgeslagen Hallo-URL gemaakt, mislukt de Hallo actie tijdens runtime. toowork dit, Hallo logische app opnieuw, waarmee u logic app tooretrieve veroorzaken en Hallo trigger URL opnieuw in de cache opslaan.

## <a name="collection-actions-scopes-and-loops"></a>Verzameling acties (bereiken en lussen)

Sommige actietypen kunnen acties in zichzelf bevatten. Verwijzing acties binnen een verzameling kunnen worden verwezen rechtstreeks buiten Hallo-verzameling. Als u hebt gedefinieerd `http` in een bereik `@body('http')` nog geldig overal in een werkstroom. Acties binnen een verzameling kunnen `runAfter` alleen andere acties in Hallo dezelfde verzameling.

## <a name="scope-action"></a>Bereikactie

Hallo `scope` actie kunt u logische groep acties in een werkstroom.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties tooexecute binnen Hallo bereik|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>ForEach-actie

Deze actie samenvoegartikel een matrix doorlopen en interne acties uitvoert voor elk item. Hallo foreach lus wordt standaard uitgevoerd parallel (20 uitvoeringen parallel tegelijk). U kunt uitvoering regels met behulp van Hallo instellen `operationOptions` parameter.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties tooexecute binnen de lus Hallo|
|foreach|Ja|Tekenreeks|Hallo matrix tooiterate via|
|operationOptions|Er is geen|Tekenreeks|Bewerking opties voor het gedrag. Momenteel ondersteunt alleen `sequential` tooexecute iteraties sequentieel (standaardgedrag is parallelle)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Totdat de actie

Deze samenvoegartikel actie uitgevoerd binnenste acties totdat een voorwaarde tootrue resulteert.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties tooexecute binnen de lus Hallo|
|expressie|Ja|Tekenreeks|Hallo expressie tooevaluate na elke iteratie|
|Limiet|Ja|Object|Hallo-limieten voor het Hallo-lus - ten minste één limiet moeten worden gedefinieerd.|
|Aantal|Er is geen|int|Hallo limiet toohello aantal iteraties die kunnen worden uitgevoerd|
|timeout|Er is geen|Tekenreeks|Hallo-out voor hoe lang deze moet worden herhaald.  ISO 8601-notatie|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Voorwaarden - als actie

Hallo `If` actie kunt u een voorwaarde evalueren en uitvoeren van een vertakking op basis van of Hallo expressie wordt geëvalueerd te`true`.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties tooexecute wanneer expressie te evalueert.`true`|
|expressie|Ja|Tekenreeks|Hallo expressie tooevaluate|
|anders|Er is geen|Object|Interne acties tooexecute wanneer expressie te evalueert.`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Hallo ziet volgende tabel u voorbeelden van hoe voorwaarden expressies in een actie kunnen gebruiken:  
  
|JSON-waarde|Resultaat|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|De waarde die tootrue evalueren verbindingspogingen wordt deze voorwaarde toopass. Alleen Booleaanse expressies worden ondersteund. tooconvert andere typen tooBoolean, gebruik functies `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Vergelijking van functies worden ondersteund. Hallo bijvoorbeeld hier Hallo handeling alleen uitgevoerd wanneer het Hallo-uitvoer van act1 is groter dan de drempelwaarde Hallo.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Bedrijfslogica-functies zijn ook ondersteunde toocreate genest Booleaanse expressies. In dit geval Hallo actie worden uitgevoerd wanneer het Hallo-uitvoer van act1 is hoger dan drempelwaarde Hallo of onder de 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|U kunt matrix functies toocheck gebruiken als een matrix alle items heeft. In dit geval Hallo actie worden uitgevoerd wanneer Hallo fouten matrix leeg is.| 
|`"expression": "parameters('hasSpecialAction')"`|Fout: geen geldige voorwaarde omdat @ is vereist voor voorwaarden.|  
  
Als een voorwaarde is geëvalueerd, Hallo-voorwaarde is gemarkeerd als `Succeeded`. Acties in beide Hallo `actions` of `else` objecten te evalueren`Succeeded` wanneer die wordt uitgevoerd en is voltooid, `Failed` wanneer die wordt uitgevoerd en is mislukt, of `Skipped` wanneer dat filiaal niet is uitgevoerd.

## <a name="next-steps"></a>Volgende stappen

[REST-API van workflow](https://docs.microsoft.com/rest/api/logic/workflows)
