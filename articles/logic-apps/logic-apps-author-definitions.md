---
title: aaaDefine werkstromen met JSON - Azure Logic Apps | Microsoft Docs
description: Hoe toowrite werkstroomdefinities in JSON voor logic apps
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Werkstroomdefinities voor logische apps met JSON maken

U kunt de werkstroomdefinities voor de maken [Azure Logic Apps](logic-apps-what-are-logic-apps.md) met eenvoudig, declaratief JSON-taal. Als u nog niet gedaan hebt, moet u rekening houden [hoe toocreate uw eerste logische app met Logic App-ontwerper](logic-apps-create-a-logic-app.md). Zie ook Hallo [volledige naslaginformatie voor Hallo werkstroom Definition Language](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Herhaal de stappen via een lijst

tooiterate via een matrix heeft too10, 000 items en een actie uitvoert voor elk item, gebruikt u Hallo [foreach type](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Afhandelen van fouten als er iets mis gaat

Normaal gesproken gewenste tooinclude een *herstel stap* : bepaalde logica die wordt uitgevoerd *als* een of meer van uw aanroepen mislukken. In dit voorbeeld ontvangt gegevens van verschillende locaties, maar als het Hallo-aanroep is mislukt, willen we tooPOST een bericht ergens zodat we later omlaag die is mislukt bijhouden kunt:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify die `postToErrorMessageQueue` alleen wordt uitgevoerd na `readData` heeft `Failed`, gebruik Hallo `runAfter` eigenschap, bijvoorbeeld een lijst van mogelijke waarden toospecify zodat `runAfter` kan worden `["Succeeded", "Failed"]`.

Ten slotte omdat in dit voorbeeld wordt nu Hallo fout verwerkt, wordt niet langer markeren Hallo run as- `Failed`. Omdat we Hallo stap voor het verwerken van deze fout in dit voorbeeld hebt toegevoegd, Hallo uitvoeren heeft `Succeeded` maar één stap `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Twee of meer stappen parallel uitvoeren

toorun meerdere acties parallel Hallo `runAfter` eigenschap moet gelijkwaardige tijdens runtime. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

In dit voorbeeld beide `branch1` en `branch2` zijn ingesteld toorun na `readData`. Als gevolg hiervan beide vertakkingen parallel worden uitgevoerd. Hallo tijdstempel voor beide vertakkingen is identiek.

![Parallel](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Twee parallelle vertakkingen koppelen

U kunt deelnemen aan twee acties die zijn ingesteld toorun parallel door toe te voegen items toohello `runAfter` eigenschap zoals in het vorige voorbeeld Hallo.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Parallel](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Lijst met items tooa andere configuratie toewijzen

Volgende, stel willen we tooget andere inhoud op basis van Hallo-waarde van een eigenschap. We kunnen een overzicht van waarden toodestinations maken als een parameter:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

In dit geval krijgen we eerst een lijst met artikelen. Op basis van het Hallo-categorie die is gedefinieerd als een parameter, Hallo tweede stap maakt gebruik van een kaart toolook up Hallo-URL voor het Hallo-inhoud ophalen.

Enkele voorbeelden van momenten toonote hier: 

*   Hallo [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) functie gecontroleerd of Hallo categorie overeenkomt met een van de Hallo bekend gedefinieerde categorieën.

*   Nadat we Hallo categorie hebt ontvangen, kunnen we pull-hallo item uit Hallo-toewijzing met vierkante haken:`parameters[...]`

## <a name="process-strings"></a>Proces tekenreeksen

Hier kunt u verschillende functies toomanipulate tekenreeksen. Stel bijvoorbeeld dat we hebben een tekenreeks dat we toopass tooa systeem willen, maar we zijn ervan overtuigd over het afhandelen van de juiste voor codering niet. Een mogelijkheid is toobase64 coderen van deze tekenreeks. Echter tooavoid aanhalingstekens in een URL, gaan we tooreplace enkele tekens. 

We willen ook een subtekenreeks van de naam van de order Hallo omdat de eerste vijf tekens Hallo niet worden gebruikt.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Werkdagen van binnen toooutside:

1. Hallo ophalen [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) voor de naam van Hallo besteller, dus we terughalen Hallo totaal aantal tekens.

2. Aftrekken 5 aangezien we een kortere tekenreeks.

3. Pas Hallo [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). We beginnen bij index `5` en ga Hallo rest van Hallo-tekenreeks.

4. Deze tooa subtekenreeks converteren [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) tekenreeks.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)alle Hallo `+` tekens `-` tekens.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)alle Hallo `/` tekens `_` tekens.

## <a name="work-with-date-times"></a>Werken met datums en tijden

Datums en tijden kan handig zijn met name wanneer u probeert toopull gegevens uit een gegevensbron die natuurlijk biedt geen ondersteuning voor *triggers*. U kunt ook datums en tijden voor het vinden van hoe lang verschillende stappen nemen.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

In dit voorbeeld we Hallo extraheren `startTime` uit de vorige stap Hallo. Vervolgens we Hallo huidige tijd niet ophalen en afgetrokken van één seconde:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

U kunt andere tijdseenheden, zoals `minutes` of `hours`. Ten slotte kunnen we deze twee waarden vergelijken. Als de eerste waarde Hallo lager dan de tweede waarde hello, wordt meer dan één seconde is verstreken sinds Hallo volgorde voor het eerst is geplaatst.

tooformat datums, kunnen we tekenreeks formatters gebruiken. Bijvoorbeeld, tooget hello RFC1123, gebruiken we [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). Zie toolearn over datumopmaak [werkstroom Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Implementatieparameters voor verschillende omgevingen

Implementatie levenscycli hebben doorgaans een ontwikkelomgeving, een testomgeving en een productie-omgeving. Bijvoorbeeld, kunt u dezelfde definitie in alle deze omgevingen Hallo maar verschillende databases gebruikt. Evenzo kunt u toouse dezelfde definitie Hallo over verschillende regio's voor hoge beschikbaarheid, maar elke logic app-exemplaar tootalk toothat regio van database wilt.
Dit scenario verschilt van de parameters op te nemen *runtime* waar in plaats daarvan moet u Hallo `trigger()` werken zoals in het vorige voorbeeld Hallo.

U kunt beginnen met een basisdefinitie zoals in dit voorbeeld:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

In de werkelijke Hallo `PUT` aanvragen voor Hallo logic apps, kunt u de parameter Hallo bieden `uri`. Omdat een standaardwaarde niet meer bestaat, is deze parameter in Hallo logic app nettolading vereist:

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

In elke omgeving, kunt u een andere waarde opgeven voor Hallo `connection` parameter. 

Zie voor alle opties die u hebt voor het maken en beheren van logic apps hello, Hallo [REST API-documentatie](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
