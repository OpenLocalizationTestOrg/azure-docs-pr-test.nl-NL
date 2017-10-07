---
title: aaaLog Analytics logboek search REST-API | Microsoft Docs
description: Deze handleiding biedt een eenvoudige zelfstudie beschrijven hoe u kunt Hallo logboekanalyse zoeken REST-API in Hallo Operations Management Suite (OMS) en deze voorbeelden die laten hoe u zien toouse Hallo opdrachten.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>Log Analytics logboek search REST-API
Deze handleiding biedt een eenvoudige zelfstudie, inclusief voorbeelden van hoe u Hallo Log Analytics Search REST-API kan gebruiken. Log Analytics maakt deel uit van Hallo Operations Management Suite (OMS).

> [!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens u toouse Hallo verouderde querytaal met Hallo logboek search API blijven moet, zoals beschreven in dit artikel.  Een nieuwe API worden uitgebracht voor bijgewerkte werkruimten en Hallo-documentatie op dat moment wordt bijgewerkt. 

> [!NOTE]
> Log Analytics is eerder operationeel inzicht, dat is waarom het Hallo-naam die wordt gebruikt in het Hallo-resourceprovider is aangeroepen.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Overzicht van Hallo logboek Search REST-API
Hallo Log Analytics Search REST-API RESTful is en toegankelijk zijn via hello Azure Resource Manager-API. Dit artikel vindt u voorbeelden van de toegang tot API Hallo via [ARMClient](https://github.com/projectkudu/ARMClient), een open-source-opdrachtregelprogramma dat wordt aangeroepen vereenvoudigt hello Azure Resource Manager-API. Hallo-gebruik van ARMClient is een van de vele opties tooaccess Hallo Log Analytics zoeken-API. Een andere optie is toouse hello Azure PowerShell-module voor OperationalInsights, waaronder de cmdlets voor toegang tot zoeken. Met deze hulpprogramma's, kunt u gebruikmaken van hello Azure Resource Manager-API toomake aanroepen tooOMS werkruimten en zoekvariabelen binnen deze. Hallo API levert zoekresultaten in JSON-indeling, zodat u toouse Hallo zoekresultaten in veel verschillende manieren programmatisch.

Hello Azure Resource Manager kan worden gebruikt een [-bibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) en Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn Bekijk meer Hallo gekoppelde webpagina's.

> [!NOTE]
> Als u een aggregatie-opdracht zoals gebruiken `|measure count()` of `distinct`, elke aanroep toosearch kan resulteren in een Resourcegroepnaam 500.000 records. Zoekopdrachten dat een aggregatie-opdracht niet opneemt retourneren maximaal 5.000 records.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Basic Log Analytics Search REST-API-zelfstudie
### <a name="toouse-armclient"></a>toouse ARMClient
1. Installeer [Chocolatey](https://chocolatey.org/), dit is een Open Source Package Manager voor Windows. Open een opdrachtpromptvenster als administrator en voer vervolgens de volgende opdracht Hallo:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Installeer ARMClient Hallo na de opdracht uitgevoerd:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform een zoekopdracht met ARMClient
1. Meld u aan met uw Microsoft-account of de account van uw werk of school:

    ```
    armclient login
    ```

    Een geslaagde aanmelding geeft een lijst van alle abonnementen gekoppeld toohello opgegeven account:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Hallo Operations Management Suite werkruimten ophalen:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Een geslaagde Get-aanvraag zou uitvoer dat alle werkruimten toohello abonnement gekoppeld:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Uw zoekopdracht-variabele maken:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Zoeken met behulp van de variabele van uw nieuwe zoekopdracht:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Meld u voorbeelden van Analytics Search REST-API-verwijzing
Hallo volgen voorbeelden laten zien hoe u Hallo Search API kunt gebruiken.

### <a name="search---actionread"></a>Zoeken - actie leestijd
**Voorbeeld-Url:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Aanvraag:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.

| **Eigenschap** | **Beschrijving** |
| --- | --- |
| Boven |Hallo maximum aantal resultaten tooreturn. |
| Markeer |Bevat vóór en na-parameters, meestal gebruikt voor de overeenkomende velden markeren |
| vooraf |Prefixes Hallo tekenreeksvelden tooyour komt overeen met gegeven. |
| Verzenden |Voegt Hallo tekenreeksvelden tooyour komt overeen met gegeven. |
| query |Hallo zoekquery toocollect gebruikt en retourneren van resultaten. |
| start |Hallo begin van tijdvenster Hallo resultaten toobe gevonden gewenste. |
| Einde |Hallo einde van tijdvenster Hallo resultaten toobe gevonden gewenste. |

**Antwoord:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Zoek / {-ID} - actie leestijd
**Aanvraag Hallo inhoud van een opgeslagen zoekopdracht:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Zoekresultaten met status 'In behandeling' hello, kunnen polling Hallo bijgewerkt resultaten worden uitgevoerd via deze API. Na 6 min Hallo resultaat van de Hallo zoekactie wordt verwijderd uit de cache Hallo en HTTP-geworden wordt geretourneerd. Als de aanvankelijke zoekaanvraag Hallo onmiddellijk een 'Geslaagd' status retourneert, Hallo resultaten toohello cache waardoor deze API tooreturn HTTP geworden als opgevraagd niet toegevoegd. Hallo-inhoud van een HTTP 200-resultaat zijn in Hallo dezelfde notatie als de aanvankelijke zoekaanvraag Hallo alleen met de bijgewerkte waarden.
>
>

### <a name="saved-searches"></a>Opgeslagen zoekopdrachten
**Lijst met opgeslagen zoekopdrachten aanvragen:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Ondersteunde methoden: GET, PUT verwijderen

Ondersteunde methoden: ophalen

Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.

| Eigenschap | Beschrijving |
| --- | --- |
| Id |Hallo unieke id. |
| ETag |**Vereist voor Patch**. Bijgewerkt met de server bij elke schrijfbewerking. De waarde moet gelijk toohello huidige opgeslagen waarde of ' *' tooupdate. 409 geretourneerd voor waarden van de oude/ongeldig. |
| Properties.query |**Vereist**. Hallo-zoekopdracht. |
| properties.displayName |**Vereist**. Hallo gebruiker gedefinieerde weergavenaam van Hallo-query. |
| Properties.Category |**Vereist**. Hallo gebruiker gedefinieerde categorie van Hallo-query. |

> [!NOTE]
> Hallo Log Analytics-API van zoekservice retourneert momenteel gebruiker gemaakte opgeslagen zoekopdrachten wanneer gepeild voor opgeslagen zoekopdrachten in een werkruimte. Hallo API retourneert geen opgeslagen zoekopdrachten geleverd door oplossingen.
>
>

### <a name="create-saved-searches"></a>Opgeslagen zoekopdrachten maken
**Aanvraag:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.

### <a name="delete-saved-searches"></a>Verwijder opgeslagen zoekopdrachten
**Aanvraag:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Opgeslagen zoekopdrachten bijwerken
 **Aanvraag:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metagegevens - JSON alleen
Hier volgt een manier toosee Hallo velden voor alle logboekbestanden typen voor Hallo verzamelde gegevens in uw werkruimte. Bijvoorbeeld, als u wilt dat u weet of Hallo gebeurtenistype een veld met de naam Computer, klikt u vervolgens deze query is eenrichtingssessie toocheck.

**Aanvraag voor velden:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Antwoord:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.

| **Eigenschap** | **Beschrijving** |
| --- | --- |
| naam |Veldnaam. |
| Weergavenaam |Hallo weergavenaam van het Hallo-veld. |
| type |Hallo Type Hallo veldwaarde. |
| geschikt voor facetten |De combinatie van huidige 'indexed', ' opgeslagen ' en 'facet' Eigenschappen. |
| Weergavenaam |Huidige 'weergeven'-eigenschap. True als het veld wordt weergegeven in de zoekopdracht. |
| ownerType |Verminderde tooonly typen die behoren tooonboarded IP's. |

## <a name="optional-parameters"></a>Optionele parameters
Hallo volgende informatie beschrijft de optionele parameters beschikbaar.

### <a name="highlighting"></a>Markeren
Hallo "Highlight" parameter is een optionele parameter, mag u toorequest Hallo zoeken subsysteem omvatten een reeks markeringen in zijn reactie.

Deze markeringen geven Hallo starten en eindigen gemarkeerde tekst die overeenkomt met de Hallo voorwaarden vindt u in uw query.
U kunt opgeven Hallo moet worden gestart en eindigen markeringen die worden gebruikt door een zoekterm toowrap Hallo gemarkeerd.

**Voorbeeld van de zoekopdracht**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Resultaat van de steekproef:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

U ziet dat Hallo voorgaande resultaat bevat een foutbericht weergegeven dat is voorafgegaan en toegevoegd.

## <a name="computer-groups"></a>Computergroepen
Computergroepen zijn speciale opgeslagen zoekopdrachten die resulteren in een set computers.  U kunt een computergroep in andere query's toolimit Hallo resultaten toohello computers in de groep hello gebruiken.  Een computergroep is geïmplementeerd als een zoekopdracht met een code van de groep met een waarde van de Computer.

Hier volgt een voorbeeldantwoord voor een computergroep.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Bij het ophalen van computergroepen
tooretrieve een computergroep Hallo gebruik Get-methode met Hallo groep-id.

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Maken of bijwerken van een computergroep
een computergroep toocreate Hallo Put-methode gebruiken met een opgeslagen zoekopdracht unieke ID. Als u een bestaande computer-ID gebruikt, is dat een gewijzigd. Wanneer u een computergroep in Hallo Log Analytics-portal maakt, wordt de Hallo-ID van het Hallo-groep en de naam gemaakt.

Hallo-query die wordt gebruikt voor de definitie van de groep Hallo moet een verzameling van computers voor Hallo groep toofunction goed retourneren.  Het raadzaam dat u uw query met beëindigen `| Distinct Computer` tooensure Hallo juiste gegevens geretourneerd.

Hallo-definitie Hallo opgeslagen zoekopdracht moet een label met de naam groep met een waarde van de Computer voor Hallo zoeken toobe geclassificeerd als een computergroep bevatten.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Computergroepen verwijderen
toodelete een computergroep, gebruik Hallo Delete-methode met Hallo groep-id.

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toobuild query's op basis van aangepaste velden voor de criteria.
