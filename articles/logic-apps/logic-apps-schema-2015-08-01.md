---
title: aaaSchema updates augustus-1-2015 preview - Azure Logic Apps | Microsoft Docs
description: JSON-definities voor Azure Logic Apps maken met 08-01-preview-schemaversie 2015
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Schema-updates voor Azure Logic Apps - preview 1 augustus 2015

Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die het maken van logische apps meer betrouwbare en gemakkelijker toouse:

*   Hallo **APIApp** actietype is bijgewerkte tooa nieuwe [ **APIConnection** ](#api-connections) action-type.
*   **Herhaal** wordt gewijzigd te[**Foreach**](#foreach).
*   Hallo [ **HTTP-Listener** API-App](#http-listener) is niet langer vereist.
*   Het aanroepen van onderliggende werkstromen gebruikt een [nieuwe schema](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>TooAPI verbindingen verplaatsen

Hallo grootste wijziging is dat u niet langer toodeploy API-Apps in uw Azure-abonnement zodat u API's kunt gebruiken. Hier volgen Hallo manieren waarop u API's kunt gebruiken:

* Beheerde API 's
* Uw aangepaste Web-API 's

Elke manier wordt anders verwerkt omdat het beheer en het hosten van modellen verschillend zijn. Een voordeel van dit model is dat u bent niet meer beperkt tooresources die zijn geïmplementeerd in uw Azure-resourcegroep. 

### <a name="managed-apis"></a>Beheerde API 's

Microsoft beheert sommige API's namens u, zoals Office 365, Salesforce, Twitter en FTP. U kunt sommige beheerde API's als-is, zoals Bing vertalen, terwijl anderen configuratie vereist. Deze configuratie wordt aangeroepen een *verbinding*.

Wanneer u Office 365 gebruikt, moet u bijvoorbeeld een verbinding met uw Office 365-in-token maken. Dit token is veilig opgeslagen en wordt vernieuwd zodat uw logische app kan altijd Hallo Office 365-API aanroepen. Als u tooconnect tooyour SQL- of FTP-server wilt, moet u ook een verbinding met de verbindingsreeks Hallo maken. 

In deze definitie deze acties worden genoemd `APIConnection`. Hier volgt een voorbeeld van een verbinding die een e-mailbericht voor Office 365 toosend aanroept:

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

Hallo `host` object is gedeelte van de ingangen die unieke tooAPI verbindingen is en bestaat uit twee delen: `api` en `connection`.

Hallo `api` heeft Hallo runtime URL van het waar dat beheerd API wordt gehost. U kunt zien alle Hallo beschikbaar beheerde API's door het aanroepen van `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Wanneer u een API gebruikt, Hallo API kan of kunnen geen *verbindingsparameters* gedefinieerd. Hallo API niet het geval, geen *verbinding* is vereist. Als Hallo API geval is, moet u een verbinding te maken. Hallo gemaakt verbinding heeft Hallo-naam die u kiest. U vervolgens verwijzen naar de naam Hallo in Hallo `connection` object binnen Hallo `host` object. een verbinding in een resourcegroep of aanroep toocreate:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Hello instantie te volgen:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Beheerde API's in een Azure Resource Manager-sjabloon implementeren

U kunt een volledige toepassing in een Azure Resource Manager-sjabloon maken, zolang interactief aanmelden is niet vereist.
Als aanmelden vereist is, kunt u een alles met hello Azure Resource Manager-sjabloon instellen, maar u hebt nog toovisit Hallo portal tooauthorize Hallo verbindingen. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

U kunt zien in dit voorbeeld dat Hallo verbindingen zijn alleen bronnen die bevinden zich in de resourcegroep. Ze verwijzen naar Hallo beheerde API's beschikbaar tooyou in uw abonnement.

### <a name="your-custom-web-apis"></a>Uw aangepaste Web-API 's

Als u uw eigen API's, die niet door Microsoft beheerd zijn, gebruiken ingebouwde Hallo **HTTP** actie toocall ze. Voor een ideaal ervaring, moet u een Swagger-eindpunt weergeven voor uw API. Dit eindpunt Hiermee Hallo Logic App-ontwerper toorender Hallo invoer en uitvoer voor uw API. Zonder Swagger, kan Hallo designer alleen weergeven Hallo in- en uitgangen als ondoorzichtige JSON-objecten.

Hier volgt een voorbeeld waarin Hallo nieuwe `metadata.apiDefinitionUrl` eigenschap:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Als u uw Web-API op Azure App Service host, wordt uw Web-API automatisch weergegeven in de lijst van acties die beschikbaar zijn in de ontwerpfunctie Hallo Hallo. Als dat niet het geval is, hebt u toopaste in Hallo URL rechtstreeks. Hallo Swagger-eindpunt moet niet-geverifieerde toobe kan worden gebruikt in Hallo Logic App-ontwerper, hoewel u Hallo API zichzelf met welke methoden die ondersteuning biedt voor Swagger kunt beveiligen.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Aanroepen van geïmplementeerde API-apps met 2015-08-01-preview

Als u een API-App hebt geïmplementeerd, kunt u app Hallo Hello bellen **HTTP** in te grijpen.

Als u Dropbox toolist bestanden, bijvoorbeeld uw **2014-12-01-preview** versie schemadefinitie wellicht ongeveer als volgt:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Tijdens het gedeelte van de parameters Hallo Hallo definitie van Logic Apps ongewijzigd blijft, kunt u Hallo equivalente HTTP-actie zoals in dit voorbeeld maken:

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Stap voor stap één voor één van deze eigenschappen:

| Eigenschap Action | Beschrijving |
| --- | --- |
| `type` |`Http`In plaats van`APIapp` |
| `metadata.apiDefinitionUrl` |toouse deze actie Hallo Logic App-ontwerper, zijn onder andere Hallo metagegevenseindpunt, is samengesteld uit:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Gemaakt op basis van:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Altijd`POST` |
| `inputs.body` |Parameters voor identieke toohello API-App |
| `inputs.authentication` |Identieke toohello API-App-verificatie |

Deze aanpak moet werken voor alle acties van de API-App. Vergeet echter niet dat deze vorige API-Apps niet langer worden ondersteund. Daarom moet u overstappen tooone Hallo twee andere vorige opties, een beheerde API of die als host fungeert voor uw aangepaste Web-API.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Herhaal too'foreach hernoemd '

We ontvangen voor het vorige schemaversie hello, veel feedback van klanten die **herhalen** verwarrend is en niet goed vast te leggen die **herhalen** werd echt een voor elke lus. We hebben als gevolg hiervan hernoemd `repeat` te`foreach`. Bijvoorbeeld zou eerder u schrijven:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

U zou nu schrijven:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

Hallo functie `@repeatItem()` is eerder gebruikte tooreference Hallo het huidige item wordt iteratie. Deze functie is nu te vereenvoudigd`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Verwijzing naar uitvoer van 'foreach'

Voor vereenvoudiging Hallo levert van `foreach` acties niet zijn ingepakt in een object aangeroepen `repeatItems`. Tijdens het Hallo levert van vorige Hallo `repeat` voorbeeld zijn:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

Nu zijn deze uitgangen:

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

Voorheen tooget toohello hoofdtekst van Hallo actie bij verwijzingen naar deze uitvoer:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

Nu kunt u doen in plaats daarvan:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

Met deze wijzigingen Hallo functies `@repeatItem()`, `@repeatBody()`, en `@repeatOutputs()` worden verwijderd.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Native HTTP-listener

Hallo mogelijkheden nu zijn ingebouwd in HTTP-Listener. Daarom moet u niet langer toodeploy een HTTP-Listener API-App. Zie [volledige details voor het Hallo toomake uw logische app eindpunt aanroepbare hier](../logic-apps/logic-apps-http-endpoint.md). 

Met deze wijzigingen hebben wij Hallo verwijderd `@accessKeys()` functie, die wordt vervangen door Hallo `@listCallbackURL()` functie voor het ophalen van Hallo eindpunt indien nodig. Bovendien moet u ten minste één trigger nu definiëren in uw logische app. Als u wilt dat te`/run` Hallo werkstroom, hebt u een van deze triggers: `manual`, `apiConnectionWebhook`, of `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Aanroepen van onderliggende werkstromen

Voorheen vereist voor het aanroepen van onderliggende werkstromen toohello werkstroom, aan de Hallo-toegangstoken en plakken Hallo token in definitie Hallo logic Apps waar u toocall die onderliggende werkstroom gaan. Hallo Logic Apps engine genereert automatisch een SAS tijdens runtime voor Hallo onderliggende werkstroom met het nieuwe schema hello, zodat u niet hebt te geen geheimen in plakken Hallo definitie. Hier volgt een voorbeeld:

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

Een tweede verbetering is dat we Hallo onderliggende geeft werkstromen volledige toegang toohello binnenkomende aanvraag. Dit betekent dat u kunt parameters doorgeven in Hallo *query's* sectie en in Hallo *headers* object en die u volledig kunt definiëren Hallo volledige hoofdtekst.

Er zijn ten slotte vereiste wijzigingen toohello onderliggende werkstroom. Terwijl u onderliggende werkstroom eerder rechtstreeks aanroepen kan, moet nu u een trigger-eindpunt in de werkstroom Hallo voor Hallo bovenliggende toocall. In het algemeen, voegt u een trigger die heeft `manual` typt en gebruik vervolgens deze trigger in Hallo bovenliggende definitie. Opmerking Hallo `host` eigenschap specifiek heeft een `triggerName` omdat u altijd waarvan de trigger moet opgeven dat u aanroept.

## <a name="other-changes"></a>Andere wijzigingen

### <a name="new-queries-property"></a>Nieuwe 'query'-eigenschap

Alle actietypen ondersteunen nu een nieuwe invoer aangeroepen `queries`. Deze gegevens kan worden gestructureerd object, in plaats van u hoeft tooassemble Hallo tekenreeks handmatig.

### <a name="renamed-parse-function-toojson"></a>'Parse()' functie too'json() hernoemd '

We toevoegen meer inhoudstypen snel, zodat we Hallo hernoemd `parse()` te functioneren`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Binnenkort beschikbaar: Enterprise Integration-API's

Er zijn momenteel geen beheerde versies nog van Hallo Enterprise Integration-API's, zoals AS2. Ondertussen kunt u uw bestaande BizTalk-APIs geïmplementeerde via Hallo HTTP-actie. Voor meer informatie Zie ' de reeds geïmplementeerde API-apps gebruiken ' in hello [integratie roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
