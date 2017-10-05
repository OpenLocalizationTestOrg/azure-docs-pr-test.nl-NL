---
title: Werkstroomacties en triggers - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Werkstroomacties en triggers voor Azure Logic Apps

Logische apps bestaan uit het triggers en acties. Er zijn zes soorten triggers. Elk type heeft een andere interface en ander gedrag. U kunt ook meer informatie over andere gegevens door te kijken in de details van de [werkstroom Definition Language](logic-apps-workflow-definition-language.md).  
  
Lees verder voor meer informatie over triggers en acties en hoe u ze kunt gebruiken voor het bouwen van logic apps om uw bedrijfsprocessen en werkstromen te verbeteren.  
  
### <a name="triggers"></a>Triggers  

Een trigger geeft de oproepen die een uitvoering van uw logische app werkstroom kunnen initiëren. Hier volgen de twee verschillende manieren een uitvoering van uw werkstroom te starten:  
  
-   Een polling-trigger  

-   Een push-signaal - door het aanroepen van de [REST-API van Workflow](https://docs.microsoft.com/rest/api/logic/workflows)  
  
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
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Triggertypen en hun invoer  

U kunt deze typen triggers:
  
-   **Aanvraag** \- de logische app maakt een eindpunt voor u aan te roepen  
  
-   **Terugkeerpatroon** \- deze gebeurtenis wordt gestart op basis van een gedefinieerde planning  
  
-   **HTTP** \- een HTTP-web-eindpunt worden opgevraagd. Het HTTP-eindpunt moet voldoen aan een specifieke activerende contract \- met behulp van een 202\-asynchrone patroon, of door te retourneren van een matrix  
  
-   **ApiConnection** \- Polls zoals HTTP is geactiveerd, maar deze wordt gebruikgemaakt van de [door Microsoft beheerde API's](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- opent een eindpunt, vergelijkbaar met de handmatige trigger echter ook roept uit met een opgegeven URL registreren en ongedaan maken  
  
-   **ApiConnectionWebhook** \- werkt zoals de trigger HTTPWebhook door gebruik te maken van de API door Microsoft beheerd       
    Elk triggertype heeft een andere set **invoer** het gedrag te definiëren.  
  
## <a name="request-trigger"></a>Aanvraag trigger  

Deze trigger fungeert als een eindpunt dat u via een HTTP-aanvraag om aan te roepen uw logische app aanroepen. Een aanvraag-trigger ziet er in dit voorbeeld:  
  
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
|Schema|Nee|Een JSON-schema te valideren en de binnenkomende aanvraag. Handig voor het helpen werkstroomstappen van de volgende weten welke eigenschappen om te verwijzen.|

Om aan te roepen dit eindpunt, moet u aan te roepen de *listCallbackUrl* API. Zie [REST-API van werkstroom](https://docs.microsoft.com/rest/api/logic/workflows).  
  
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

Zoals u ziet, is een eenvoudige manier voor het uitvoeren van een werkstroom.  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|Frequentie|Ja|Hoe vaak de trigger wordt uitgevoerd. Gebruik slechts één van deze mogelijke waarden: seconde, minuut, uur, dag, week, maand of jaar|  
|Interval|Ja|Interval van de opgegeven frequentie voor het terugkeerpatroon|  
|startTime|Nee|Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.|  
|Tijdzone|Er is geen|Als een startTime zonder een UTC-offset is opgegeven, wordt deze tijdzone gebruikt.|  
  
U kunt ook een trigger worden gestart in de toekomst wordt uitgevoerd op een bepaald moment plannen. Als u wilt een wekelijks rapport elke maandag starten kunt u bijvoorbeeld de logische app aan elke maandag begint met het maken van de volgende trigger plannen:  

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

HTTP-triggers peilen op een opgegeven eindpunt en controleert u het antwoord om te bepalen of de werkstroom moet worden uitgevoerd. De invoer-object wordt gebruikt in de set parameters die zijn vereist om een HTTP-aanroep samen te stellen:  
  
|Elementnaam|Vereist|Beschrijving|Type|  
|----------------|------------|---------------|--------|  
|Methode|Ja|Kan een van de volgende HTTP-methoden zijn: GET, POST, PUT, DELETE, PATCH of HEAD|Tekenreeks|  
|URI|Ja|Het http of https-eindpunt dat wordt genoemd. Maximum van 2 kB.|Tekenreeks|  
|Query 's|Nee|Een object dat de queryparameters toevoegen aan de URL vertegenwoordigt. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|Object|  
|Headers|Nee|Object voor elk van de headers die aan de aanvraag is verzonden. Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Object|  
|Hoofdtekst|Nee|Een object dat de nettolading dat wordt verzonden naar het eindpunt vertegenwoordigt.|Object|  
|retryPolicy|Nee|Een object dat u kunt het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.|Object|  
|Verificatie|Nee|Hiermee geeft u de methode die de aanvraag moet worden geverifieerd. Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority` deze waarde is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`|Object|  
  
De HTTP-trigger is vereist voor de HTTP-API om te voldoen aan een specifiek patroon voor gebruik met uw logische app. Hiervoor de volgende velden:  
  
|Antwoord|Beschrijving|  
|------------|---------------|  
|Statuscode|Statuscode 200 \(OK\) run veroorzaken. Andere statuscode niet leiden tot een uitvoering.|  
|Probeer\-na header|Het aantal seconden tot de logische app het eindpunt opnieuw worden opgevraagd.|  
|Locatieheader|De URL aan te roepen voor de volgende pollinginterval. Als niet wordt opgegeven, wordt de oorspronkelijke URL gebruikt.|  
  
Hier volgen enkele voorbeelden van andere problemen voor verschillende soorten aanvragen:  
  
|Reactiecode|Probeer\-na|Gedrag|  
|-----------------|----------------|------------|  
|200|\(geen\)|Niet een geldig worden geactiveerd, opnieuw proberen\-na is vereist, of anders de engine nooit worden opgevraagd voor de volgende aanvraag.|  
|202|60|De werkstroom niet activeren. De volgende poging gebeurt in een minuut.|  
|200|10|De werkstroom uitvoert, en opnieuw controleren voor meer informatie over 10 seconden.|  
|400|\(geen\)|Onjuiste aanvraag, de werkstroom niet uitgevoerd. Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid gebruikt. Nadat u het aantal nieuwe pogingen is bereikt, is de trigger niet meer geldig.|  
|500|\(geen\)|Fout-server, worden de werkstroom niet uitgevoerd.  Als er geen **beleid voor opnieuw proberen** gedefinieerd, wordt het standaardbeleid gebruikt. Nadat u het aantal nieuwe pogingen is bereikt, is de trigger niet meer geldig.|  
  
De uitvoer van een HTTP-trigger eruitzien als in dit voorbeeld:  
  
|Elementnaam|Beschrijving|Type|  
|----------------|---------------|--------|  
|Headers|De headers van de http-antwoord.|Object|  
|Hoofdtekst|De hoofdtekst van het http-antwoord.|Object|  
  
## <a name="api-connection-trigger"></a>API-verbinding activeren  

De API verbinding trigger is vergelijkbaar met de HTTP-trigger in de basisfunctionaliteit. De parameters voor het identificeren van de actie zijn echter verschillend. Hier volgt een voorbeeld:  
  
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
|host|Ja||De ApiApp gehost gateway en -id.|  
|Methode|Ja|Tekenreeks|Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|Query 's|Nee|Object|Vertegenwoordigt de queryparameters worden toegevoegd aan de URL. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|  
|Headers|Nee|Object|Hiermee geeft u elk van de headers die aan de aanvraag is verzonden. Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.|  
|retryPolicy|Nee|Object|Hiermee kunt u aanpassen van het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten.|  
|Verificatie|Nee|Object|Hiermee geeft u de methode die de aanvraag moet worden geverifieerd. Zie voor meer informatie over dit object [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
De eigenschappen voor de host zijn:  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|API-runtimeUrl|Ja|Het eindpunt van de beheerde API.|  
|Verbindingsnaam||Moet een verwijzing naar een parameter met de naam `$connection` en de naam van de beheerde API-verbinding die gebruikmaakt van de werkstroom.|
  
De uitvoer van een trigger API-verbinding zijn:
  
|Elementnaam|Type|Beschrijving|  
|----------------|--------|---------------|  
|Headers|Object|De headers van de http-antwoord.|  
|Hoofdtekst|Object|De hoofdtekst van het http-antwoord.|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook trigger  

De trigger HTTPWebhook opent een eindpunt, vergelijkbaar met de handmatige worden geactiveerd, maar de trigger HTTPWebhook roept ook uit op een opgegeven URL registreren en ongedaan maken. Hier volgt een voorbeeld van wat een trigger HTTPWebhook als volgt uitzien:  

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

Veel van deze gedeelten zijn optioneel en het gedrag van de Webhook is afhankelijk van welke gedeelten wordt geleverd of wordt weggelaten.  
De eigenschappen van een Webhook zijn als volgt:  
  
|Elementnaam|Vereist|Beschrijving|  
|----------------|------------|---------------|  
|abonneren|Nee|De uitgaande aanvraag die wordt aangeroepen wanneer de trigger wordt gemaakt en de initiële registratie voert.|  
|afmelden|Nee|De uitgaande aanvraag wanneer de trigger wordt verwijderd.|  
  
-   **Abonneren** is de uitgaande aanroep die beginnen met luisteren op gebeurtenissen heeft gemaakt. Deze aanroep begint met dezelfde set parameters die de normale HTTP-acties uitvoeren. Deze uitgaande wordt aanroep een wanneer de werkstroom wordt gewijzigd op elke manier, bijvoorbeeld wanneer de referenties worden hersteld of de trigger invoerparameters wijzigen.
  
    Ter ondersteuning van deze aanroep is een nieuwe functie: `@listCallbackUrl()`. Deze functie retourneert een unieke URL voor deze specifieke trigger in deze workflow. Hiermee geeft u de unieke id voor de eindpunten die gebruikmaken van de REST van de Service.  
  
-   **Afmelden** wordt aangeroepen wanneer een bewerking renders deze trigger ongeldig, met inbegrip van:  
  
    -   Het verwijderen of uitschakelen van de trigger  
  
    -   Het verwijderen of uitschakelen van de werkstroom  
  
    -   Het verwijderen of uitschakelen van het abonnement  
  
    De logische app roept automatisch de actie afmelden. De parameters voor deze functie zijn hetzelfde als de HTTP-trigger.  
  
    De uitvoer van de trigger HTTPWebhook zijn de inhoud van de binnenkomende aanvraag:  
  
|Elementnaam|Type|Beschrijving|  
|-----------------|--------|---------------|  
|Headers|Object|De headers van de http-aanvraag.|  
|Hoofdtekst|Object|De hoofdtekst van de http-aanvraag.|  

Limieten van een webhook-actie kunnen worden opgegeven op dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).
  

## <a name="conditions"></a>Voorwaarden  

U kunt een of meer voorwaarden om te bepalen of de werkstroom moet worden uitgevoerd of niet gebruiken voor een trigger. Bijvoorbeeld:  

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

In dit geval wordt het rapport alleen triggers terwijl de werkstroom `sendReports` parameter is ingesteld op true. Ten slotte voorwaarden kunnen verwijzen naar de statuscode van de trigger. U kan bijvoorbeeld ere van een werkstroom alleen als uw website een statuscode 500, als volgt retourneert:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Wanneer een expressie verwijst naar de statuscode van de trigger \(op elke manier\), het standaardgedrag \(trigger alleen op 200 \(OK\) \) wordt vervangen. Bijvoorbeeld, als u activeren op zowel de statuscode 200 als de statuscode 201 wilt, hebt u omvatten: `@or(equals(triggers().code, 200),equals(triggers().code,201))` als de voorwaarde.  
  
## <a name="start-multiple-runs-for-a-request"></a>Meerdere wordt uitgevoerd voor een aanvraag starten

Activeer meerdere wordt uitgevoerd voor een enkele aanvraag `splitOn` is nuttig, bijvoorbeeld wanneer u wilt pollen een eindpunt dat meerdere nieuwe items tussen polling-intervallen kan hebben.
  
Met `splitOn`, geeft u de eigenschap binnen de nettolading van antwoord met de matrix van items die u gebruiken wilt voor het starten van een uitvoering van de trigger. Stel dat u hebt een API waarmee het volgende antwoord geretourneerd:  
  
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
  
Uw logische app moet alleen de inhoud van de rijen, zodat u de trigger zoals in dit voorbeeld kunt maken:  
  
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
  
Klik in de werkstroomdefinitie `@triggerBody().name` retourneert `mycoolrow` voor het eerst wordt uitgevoerd, en `another row` voor de tweede uitvoeren. De trigger uitvoer eruit zien in dit voorbeeld:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Als u in dat geval `SplitOn`, u de eigenschappen die in dit geval buiten de matrix zijn geen krijgt de `Status` veld.  
  
> [!NOTE]  
> In dit voorbeeld gebruiken we de `?` operator om te voorkomen dat een fout als de `Rows` eigenschap is niet aanwezig. 
  
## <a name="single-run-instance"></a>SIS uitvoeren

Triggers die een terugkeerpatroon-eigenschap moet worden alleen gestart als alle actieve sessies hebt voltooid, kunt u configureren. Als een geplande terugkeer optreedt terwijl er een uitgevoerd in voortgang is, wordt de trigger wordt overgeslagen en wacht tot het volgende geplande terugkeerpatroon opnieuw te controleren.

U kunt deze instelling door de bewerking-opties configureren:

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
  
-   **ApiConnection** \- deze bewerking gedraagt zich als de HTTP-actie, maar gebruikt de door Microsoft beheerd-API's.  
  
-   **ApiConnectionWebhook** \- zoals HTTPWebhook hierbij wordt gebruikgemaakt van de Microsoft-beheerde API's.  
  
-   **Antwoord** \- deze actie wordt een antwoord voor een inkomend gesprek gedefinieerd.  
  
-   **Wacht** \- deze eenvoudige actie wacht een vast bedrag tijd of totdat een bepaalde tijd.  
  
-   **Werkstroom** \- deze actie vertegenwoordigt een geneste werkstroom.  

-   **De functie** \- deze actie vertegenwoordigt een Azure-functie.

### <a name="collection-actions"></a>Verzameling acties

-   **Bereik** \- deze actie is een logische groepering van andere acties.

-   **Voorwaarde** \- met deze actie evalueert een expressie en de bijbehorende resultaat vertakking wordt uitgevoerd.

-   **ForEach** \- samenvoegartikel hierdoor een matrix doorlopen en interne acties uitvoert voor elk item.

-   **Pas** \- deze samenvoegartikel actie binnenste acties worden uitgevoerd totdat een voorwaarde in waar resulteert.
  
Elk type actie heeft een andere set **invoer** die een actie gedrag definiëren.  
  
## <a name="http-action"></a>HTTP-actie  

Acties voor HTTP-aanroepen van een opgegeven eindpunt en controleren van het antwoord om te bepalen of de werkstroom moet worden uitgevoerd. De **invoer** object neemt de set parameters die zijn vereist om de HTTP-aanroep samen te stellen:  
  
|Elementnaam|Vereist|Type|Beschrijving|  
|----------------|------------|--------|---------------|  
|Methode|Ja|Tekenreeks|Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|URI|Ja|Tekenreeks|Het http of https-eindpunt dat wordt genoemd. Maximale lengte is 2 kB.|  
|Query 's|Nee|Object|Vertegenwoordigt de queryparameters toevoegen aan de URL. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|  
|Headers|Nee|Object|Hiermee geeft u elk van de headers die aan de aanvraag is verzonden. Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.|  
|retryPolicy|Nee|Object|Hiermee kunt u het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.|  
|operationsOptions|Nee|Tekenreeks|Definieert de set met speciaal gedrag negeren.|  
|Verificatie|Nee|Object|Hiermee geeft u de methode die de aanvraag moet worden geverifieerd. Zie voor meer informatie over dit object, [Scheduler uitgaande verificatie](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Afgezien van scheduler, er is een meer ondersteunde eigenschap: `authority`. Dit is standaard `https://login.windows.net` wanneer niet wordt opgegeven, maar u kunt een andere doelgroep zoals gebruiken`https://login.windows\-ppe.net`|  
  
HTTP-acties \(en API-verbinding\) acties ondersteuning beleid voor opnieuw proberen. Een beleid voor opnieuw proberen is van toepassing op onregelmatige problemen, gekenmerkt als HTTP-statuscodes 408 429 en 5xx, naast eventuele uitzonderingen connectiviteit. Dit beleid wordt beschreven met behulp van de *retryPolicy* object dat is gedefinieerd als volgt te werk:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Het interval voor opnieuw proberen is opgegeven in de ISO 8601-notatie. Dit interval heeft een waarde standaard en een minimum van 20 seconden, terwijl de maximale waarde een uur is. Het standaard- en maximum aantal is gelijk aan vier uur. Als de beleidsdefinitie voor nieuwe pogingen niet is opgegeven, een `fixed` strategie met een standaardwaarde opnieuw telling en het interval wordt gebruikt. Als wilt uitschakelen in het beleid voor opnieuw proberen, stelt u het type in op `None`.  
  
Bijvoorbeeld de volgende actie pogingen ophalen van het laatste nieuws twee keer als er onregelmatige problemen, voor een totaal van drie uitvoeringen, met een vertraging 30 seconden tussen elke poging:  
  
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

Standaard ondersteunt alle HTTP-gebaseerde acties het patroon standaard asynchrone bewerking. Als de externe server geeft aan dat de aanvraag is geaccepteerd voor verwerking met een 202 \(geaccepteerde\) antwoord wordt de Logic Apps-engine houdt de URL die is opgegeven in de antwoordheader locatie tot het bereiken van een definitieve status polling\(niet\-202 antwoord\).  
  
Instellen als wilt uitschakelen in het asynchrone gedrag die eerder is beschreven, een `DisableAsyncPattern` optie in de invoer in te grijpen. In dit geval wordt is de uitvoer van de actie gebaseerd op de eerste 202 reactie van de server.  
  
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

Een asynchrone patroon worden beperkt de duur van een bepaald tijdsinterval.  Als het tijdsinterval is verstreken zonder dat een definitieve status bereikt, wordt de status van de actie gemarkeerd `Cancelled` met de code `ActionTimedOut`.  De time-out voor de limiet is opgegeven in de ISO 8601-notatie.  Limieten kunnen worden opgegeven met de volgende syntaxis:

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
Deze actie vereist een verwijzing naar een geldige verbinding en informatie over de API en de parameters die zijn vereist.

|Elementnaam|Vereist|Type|Beschrijving|  
|----------------|------------|--------|---------------|  
|host|Ja|Object|Hiermee geeft u de connector informatie zoals de runtimeUrl en de verwijzing naar het verbindingsobject|
|Methode|Ja|Tekenreeks|Kan een van de volgende HTTP-methoden zijn: **ophalen**, **POST**, **plaatsen**, **verwijderen**, **PATCH**, of  **HEAD**|  
|Pad|Ja|Tekenreeks|Het pad van de API-bewerking.|  
|Query 's|Nee|Object|Vertegenwoordigt de queryparameters toevoegen aan de URL. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|  
|Headers|Nee|Object|Hiermee geeft u elk van de headers die aan de aanvraag is verzonden. Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u de nettolading dat wordt verzonden naar het eindpunt.|  
|retryPolicy|Nee|Object|Hiermee kunt u het gedrag voor opnieuw proberen voor 4xx of 5xx-fouten aanpassen.|  
|operationsOptions|Nee|Tekenreeks|Definieert de set met speciaal gedrag negeren.|  

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

Limieten van een webhook-actie kunnen worden opgegeven op dezelfde manier als [HTTP asynchrone limieten](#asynchronous-limits).
  
## <a name="response-action"></a>Antwoord actie  

Dit actietype de nettolading van het volledige antwoord van een HTTP-aanvraag bevat en een statusCode, hoofdtekst en headers omvat:  
  
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
  
De actie antwoord heeft speciale beperkingen die niet van toepassing op andere acties. Specifiek:  
  
-   Reacties kunnen niet in een definitie van een parallelle omdat een deterministische antwoord aan de binnenkomende aanvraag vereist is.  
  
-   Als een antwoord-actie is bereikt, nadat de binnenkomende aanvraag heeft een antwoord ontvangen, de actie wordt beschouwd als mislukt \(conflict\), en als gevolg hiervan, het uitvoeren is `Failed`.  
  
-   Een werkstroom met reacties kan geen `splitOn` in de trigger omdat één aanroep ervoor zorgt veel wordt uitgevoerd dat. Dit moet als gevolg hiervan worden gevalideerd wanneer de stroom PUT en oorzaak is een ongeldige aanvraag is.  
  
## <a name="wait-action"></a>Actie wachten  

De `wait` actie onderbreekt de uitvoering van de werkstroom voor het opgegeven interval. Bijvoorbeeld, om de 15 minuten wachten, kunt u in dit fragment:  
  
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
  
Als u wilt wachten tot een bepaald moment, kunt u ook in dit voorbeeld gebruiken:  
  
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
> De duur van de wachttijd ofwel kan worden opgegeven met de **interval** object of de **totdat** , maar niet beide.  
  
|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|Interval|Nee|Object|De duur van de wachttijd op basis van tijd.|  
|intervaleenheid|Ja|Tekenreeks|Een van deze intervallen: seconde, minuut, uur, dag, week, maand, jaar.|  
|interval aantal|Ja|Tekenreeks|De duur op basis van de opgegeven interne eenheid.|  
|pas|Nee|Object|De duur van de wachttijd op basis van een punt in tijd.|  
|Pas de timestamp|Ja|Tekenreeks|Tekenreeks &#124; Het punt in tijd in UTC wanneer de wachttijd is verlopen.|  

## <a name="query-action"></a>Queryactie

De `query` actie kunt u filteren op basis van een voorwaarde matrix. Bijvoorbeeld, om te selecteren getallen die groter zijn dan 2, kunt u gebruiken:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

De uitvoer van de `query` actie is een matrix met elementen van de invoermatrix die voldoen aan de voorwaarde.

> [!NOTE]
> Als geen waarden voldoen aan de `where` voorwaarde, het resultaat is een lege matrix.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|matrix|De bronmatrix.|
|waar|Ja|Tekenreeks|De voorwaarde van toepassing op elk element van de bronmatrix.|

## <a name="select-action"></a>Selecteer actie

De `select` actie kunt u elk element van een matrix project in een nieuwe waarde.
Bijvoorbeeld, als u wilt converteren van een matrix van getallen in een matrix met objecten, kunt u gebruiken:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

De uitvoer van de `select` actie is een matrix met de dezelfde kardinaliteit als de invoermatrix met elk element getransformeerd zoals gedefinieerd door de `select` eigenschap. Als de invoer een lege matrix is, wordt de uitvoer is ook een lege matrix.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|matrix|De bronmatrix.|
|Selecteer|Ja|Alle|De projectie toepassen op elk element van de bronmatrix.|

## <a name="terminate-action"></a>Actie beëindigen

De actie beëindigen stopt u de uitvoering van de werkstroom uitvoeren, wordt afgebroken onderweg acties en eventuele resterende acties wordt overgeslagen. Bijvoorbeeld, een reeks met de status afgebroken **mislukt**, kunt u het volgende fragment:

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
> Reeds voltooide acties worden niet beïnvloed door de actie beëindigen.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|runStatus|Ja|Tekenreeks|Het doel status uitvoeren. Beide **mislukt** of **geannuleerd**.|
|runError|Nee|Object|De details van de fout. Alleen ondersteund wanneer **runStatus** is ingesteld op **mislukt**.|
|runError code|Nee|Tekenreeks|De uitvoering van de foutcode.|
|runError bericht|Nee|Tekenreeks|Het foutbericht voor uitvoeren.|

## <a name="compose-action"></a>Actie opstellen

De actie opstellen kunt u een willekeurig object samenstellen. De uitvoer van de actie compose is het resultaat van evaluatie van de invoer. Bijvoorbeeld, kunt u de actie opstellen om samen te voegen uitvoerwaarden van meerdere acties:

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
> De **opstellen** actie kan worden gebruikt om eventuele uitvoer, met inbegrip van objecten, matrices en een ander type systeemeigen worden ondersteund door logische apps zoals XML en binaire samen te stellen.

## <a name="table-action"></a>Tabel actie

De `table` kunt u converteren van een matrix van items in een **CSV** of **HTML** tabel.

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

En kunt u de actie die worden gedefinieerd als

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

De bovenstaande geeft als resultaat

<table><thead><tr><th>id</th><th>naam</th></tr></thead><tbody><tr><td>0</td><td>appels</td></tr><tr><td>1</td><td>appels</td></tr></tbody></table>"

Als u wilt aanpassen in de tabel, kunt u de kolommen expliciet opgeven. Bijvoorbeeld:

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

De bovenstaande geeft als resultaat

<table><thead><tr><th>id maken</th><th>Beschrijving</th></tr></thead><tbody><tr><td>0</td><td>nieuwe appels</td></tr><tr><td>1</td><td>nieuwe appels</td></tr></tbody></table>"

Als de `from` waarde van de eigenschap is een lege matrix, de uitvoer is een lege tabel.

|Naam|Vereist|Type|Beschrijving|
|--------|------------|--------|---------------|
|Van|Ja|matrix|De bronmatrix.|
|Indeling|Ja|Tekenreeks|De indeling beide **CSV** of **HTML**.|
|Kolommen|Nee|matrix|De kolommen. Kan de standaardvorm van de tabel overschrijven.|
|kolomkop|Nee|Tekenreeks|De koptekst van de kolom.|
|waarde in de kolom|Ja|Tekenreeks|De waarde van de kolom.|

## <a name="workflow-action"></a>Werkstroomactie   

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|host-id|Ja|Tekenreeks|De resource-ID van de werkstroom die u wilt aanroepen.|  
|host triggernaam|Ja|Tekenreeks|De naam van de trigger die u wilt aanroepen.|  
|Query 's|Nee|Object|Vertegenwoordigt de queryparameters toevoegen aan de URL. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|  
|Headers|Nee|Object|Hiermee geeft u elk van de headers die aan de aanvraag is verzonden. Als u bijvoorbeeld de taal instellen en typt u op een aanvraag:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Hoofdtekst|Nee|Object|Hiermee geeft u de nettolading van de verzonden naar het eindpunt.|  
  
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
  
Een toegangscontrole wordt gemaakt op de werkstroom \(meer specifiek, de trigger\), wat betekent dat u moet toegang hebben tot de workflow.  
  
De uitvoer van de `workflow` actie zijn gebaseerd op wat u hebt gedefinieerd in de `response` bewerking in de onderliggende werkstroom. Als u nog geen gedefinieerd een `response` actie wordt de uitvoer is leeg.  

## <a name="function-action"></a>Functie actie   

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|functie-id|Ja|Tekenreeks|De resource-ID van de functie die u wilt aanroepen.|  
|Methode|Nee|Tekenreeks|De HTTP-methode die wordt gebruikt voor het aanroepen van de functie. Dit is standaard `POST` als niet is opgegeven.|  
|Query 's|Nee|Object|Vertegenwoordigt de queryparameters toevoegen aan de URL. Bijvoorbeeld: `"queries" : { "api-version": "2015-02-01" }` voegt `?api-version=2015-02-01` naar de URL.|  
|Headers|Nee|Object|Hiermee geeft u elk van de headers die aan de aanvraag is verzonden. Bijvoorbeeld, om de taal en type ingesteld op een aanvraag: `"headers" : { "Accept-Language": "en-us" }`.|  
|Hoofdtekst|Nee|Object|Hiermee geeft u de nettolading van de verzonden naar het eindpunt.|  

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

Wanneer u de logische app opslaat, voeren we enkele controles op de functie waarnaar wordt verwezen:
-   U moet toegang hebben tot de functie.
-   Alleen de standaard HTTP-trigger of algemene JSON webhook trigger is toegestaan.
-   Er mogen geen enkele route gedefinieerd.
-   Alleen 'functioneren' en 'anonymous' autorisatieniveau is toegestaan.

De URL van de trigger is opgehaald, in de cache opgeslagen en gebruikt tijdens runtime. Dus als een bewerking wordt ongeldig gemaakt van de URL in de cache, mislukt de actie tijdens runtime. Om dit te voorkomen, slaat u de logische app opnieuw, waardoor de logische app op te halen en de trigger-URL opnieuw in de cache.

## <a name="collection-actions-scopes-and-loops"></a>Verzameling acties (bereiken en lussen)

Sommige actietypen kunnen acties in zichzelf bevatten. Verwijzing acties binnen een verzameling kunnen worden verwezen rechtstreeks buiten de verzameling. Als u hebt gedefinieerd `http` in een bereik `@body('http')` nog geldig overal in een werkstroom. Acties binnen een verzameling kunnen `runAfter` alleen andere acties in dezelfde verzameling.

## <a name="scope-action"></a>Bereikactie

De `scope` actie kunt u logische groep acties in een werkstroom.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties worden uitgevoerd binnen het bereik|

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

Deze actie samenvoegartikel een matrix doorlopen en interne acties uitvoert voor elk item. Standaard voert de lus foreach parallel (20 uitvoeringen parallel tegelijk). U kunt instellen dat uitvoering regels die gebruikmaken van de `operationOptions` parameter.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties worden uitgevoerd binnen de lus|
|foreach|Ja|Tekenreeks|De matrix te herhalen|
|operationOptions|Er is geen|Tekenreeks|Bewerking opties voor het gedrag. Ondersteunt momenteel alleen `sequential` iteraties sequentieel uitvoeren (standaardgedrag is parallelle)|

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

Deze samenvoegartikel actie uitgevoerd binnenste acties totdat een voorwaarde in waar resulteert.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties worden uitgevoerd binnen de lus|
|expressie|Ja|Tekenreeks|De expressie na elke iteratie evalueren|
|Limiet|Ja|Object|De limieten voor de lus - ten minste één limiet moeten worden gedefinieerd.|
|Aantal|Er is geen|int|De limiet voor het aantal iteraties die kunnen worden uitgevoerd|
|Time-out|Er is geen|Tekenreeks|De time-out voor hoe lang deze moet worden herhaald.  ISO 8601-notatie|


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

De `If` actie kunt u een voorwaarde evalueren en uitvoeren van een vertakking op basis van of de expressie resulteert in `true`.

|Naam|Vereist|Type|Beschrijving|  
|--------|------------|--------|---------------|  
|acties|Ja|Object|Interne acties uit te voeren wanneer expressie resulteert in`true`|
|expressie|Ja|Tekenreeks|De expressie om te evalueren|
|anders|Er is geen|Object|Interne acties uit te voeren wanneer expressie resulteert in`false`|
  
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
  
De volgende tabel ziet u voorbeelden van hoe voorwaarden expressies in een actie kunnen gebruiken:  
  
|JSON-waarde|Resultaat|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|De waarde die als waar evalueren verbindingspogingen, wordt dit probleem op te geven. Alleen Booleaanse expressies worden ondersteund. Functies gebruiken om andere typen converteren naar Booleaanse waarde, `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Vergelijking van functies worden ondersteund. In het voorbeeld hier de actie alleen wordt uitgevoerd wanneer de uitvoer van act1 groter dan de drempelwaarde is.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Bedrijfslogica-functies worden ook ondersteund voor het maken van geneste Booleaanse expressies. In dit geval wordt de actie uitgevoerd wanneer de uitvoer van act1 boven de drempelwaarde of onder de 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Matrixfuncties kunt u controleren of een matrix alle items heeft. In dit geval wordt de actie uitgevoerd wanneer de fouten matrix leeg is.| 
|`"expression": "parameters('hasSpecialAction')"`|Fout: geen geldige voorwaarde omdat @ is vereist voor voorwaarden.|  
  
Als een voorwaarde is geëvalueerd, de voorwaarde is gemarkeerd als `Succeeded`. Acties in ofwel de `actions` of `else` objecten worden geëvalueerd tot `Succeeded` wanneer die wordt uitgevoerd en is voltooid, `Failed` wanneer die wordt uitgevoerd en is mislukt, of `Skipped` wanneer dat filiaal niet is uitgevoerd.

## <a name="next-steps"></a>Volgende stappen

[REST-API van workflow](https://docs.microsoft.com/rest/api/logic/workflows)
