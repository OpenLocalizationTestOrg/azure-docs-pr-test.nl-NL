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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="bd0bb-103">Schema-updates voor Azure Logic Apps - preview 1 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="bd0bb-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="bd0bb-104">Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die het maken van logische apps meer betrouwbare en gemakkelijker toouse:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="bd0bb-105">Hallo **APIApp** actietype is bijgewerkte tooa nieuwe [ **APIConnection** ](#api-connections) action-type.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="bd0bb-106">**Herhaal** wordt gewijzigd te[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="bd0bb-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="bd0bb-107">Hallo [ **HTTP-Listener** API-App](#http-listener) is niet langer vereist.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="bd0bb-108">Het aanroepen van onderliggende werkstromen gebruikt een [nieuwe schema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="bd0bb-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="bd0bb-109">TooAPI verbindingen verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bd0bb-109">Move tooAPI connections</span></span>

<span data-ttu-id="bd0bb-110">Hallo grootste wijziging is dat u niet langer toodeploy API-Apps in uw Azure-abonnement zodat u API's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="bd0bb-111">Hier volgen Hallo manieren waarop u API's kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="bd0bb-112">Beheerde API 's</span><span class="sxs-lookup"><span data-stu-id="bd0bb-112">Managed APIs</span></span>
* <span data-ttu-id="bd0bb-113">Uw aangepaste Web-API 's</span><span class="sxs-lookup"><span data-stu-id="bd0bb-113">Your custom Web APIs</span></span>

<span data-ttu-id="bd0bb-114">Elke manier wordt anders verwerkt omdat het beheer en het hosten van modellen verschillend zijn.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="bd0bb-115">Een voordeel van dit model is dat u bent niet meer beperkt tooresources die zijn geïmplementeerd in uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="bd0bb-116">Beheerde API 's</span><span class="sxs-lookup"><span data-stu-id="bd0bb-116">Managed APIs</span></span>

<span data-ttu-id="bd0bb-117">Microsoft beheert sommige API's namens u, zoals Office 365, Salesforce, Twitter en FTP.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="bd0bb-118">U kunt sommige beheerde API's als-is, zoals Bing vertalen, terwijl anderen configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="bd0bb-119">Deze configuratie wordt aangeroepen een *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="bd0bb-120">Wanneer u Office 365 gebruikt, moet u bijvoorbeeld een verbinding met uw Office 365-in-token maken.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="bd0bb-121">Dit token is veilig opgeslagen en wordt vernieuwd zodat uw logische app kan altijd Hallo Office 365-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="bd0bb-122">Als u tooconnect tooyour SQL- of FTP-server wilt, moet u ook een verbinding met de verbindingsreeks Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="bd0bb-123">In deze definitie deze acties worden genoemd `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="bd0bb-124">Hier volgt een voorbeeld van een verbinding die een e-mailbericht voor Office 365 toosend aanroept:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

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

<span data-ttu-id="bd0bb-125">Hallo `host` object is gedeelte van de ingangen die unieke tooAPI verbindingen is en bestaat uit twee delen: `api` en `connection`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="bd0bb-126">Hallo `api` heeft Hallo runtime URL van het waar dat beheerd API wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="bd0bb-127">U kunt zien alle Hallo beschikbaar beheerde API's door het aanroepen van `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="bd0bb-128">Wanneer u een API gebruikt, Hallo API kan of kunnen geen *verbindingsparameters* gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="bd0bb-129">Hallo API niet het geval, geen *verbinding* is vereist.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="bd0bb-130">Als Hallo API geval is, moet u een verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="bd0bb-131">Hallo gemaakt verbinding heeft Hallo-naam die u kiest.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="bd0bb-132">U vervolgens verwijzen naar de naam Hallo in Hallo `connection` object binnen Hallo `host` object.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="bd0bb-133">een verbinding in een resourcegroep of aanroep toocreate:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="bd0bb-134">Hello instantie te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-134">With hello following body:</span></span>

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="bd0bb-135">Beheerde API's in een Azure Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="bd0bb-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="bd0bb-136">U kunt een volledige toepassing in een Azure Resource Manager-sjabloon maken, zolang interactief aanmelden is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="bd0bb-137">Als aanmelden vereist is, kunt u een alles met hello Azure Resource Manager-sjabloon instellen, maar u hebt nog toovisit Hallo portal tooauthorize Hallo verbindingen.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

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

<span data-ttu-id="bd0bb-138">U kunt zien in dit voorbeeld dat Hallo verbindingen zijn alleen bronnen die bevinden zich in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="bd0bb-139">Ze verwijzen naar Hallo beheerde API's beschikbaar tooyou in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="bd0bb-140">Uw aangepaste Web-API 's</span><span class="sxs-lookup"><span data-stu-id="bd0bb-140">Your custom Web APIs</span></span>

<span data-ttu-id="bd0bb-141">Als u uw eigen API's, die niet door Microsoft beheerd zijn, gebruiken ingebouwde Hallo **HTTP** actie toocall ze.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="bd0bb-142">Voor een ideaal ervaring, moet u een Swagger-eindpunt weergeven voor uw API.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="bd0bb-143">Dit eindpunt Hiermee Hallo Logic App-ontwerper toorender Hallo invoer en uitvoer voor uw API.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="bd0bb-144">Zonder Swagger, kan Hallo designer alleen weergeven Hallo in- en uitgangen als ondoorzichtige JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="bd0bb-145">Hier volgt een voorbeeld waarin Hallo nieuwe `metadata.apiDefinitionUrl` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="bd0bb-146">Als u uw Web-API op Azure App Service host, wordt uw Web-API automatisch weergegeven in de lijst van acties die beschikbaar zijn in de ontwerpfunctie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="bd0bb-147">Als dat niet het geval is, hebt u toopaste in Hallo URL rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="bd0bb-148">Hallo Swagger-eindpunt moet niet-geverifieerde toobe kan worden gebruikt in Hallo Logic App-ontwerper, hoewel u Hallo API zichzelf met welke methoden die ondersteuning biedt voor Swagger kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="bd0bb-149">Aanroepen van geïmplementeerde API-apps met 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="bd0bb-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="bd0bb-150">Als u een API-App hebt geïmplementeerd, kunt u app Hallo Hello bellen **HTTP** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="bd0bb-151">Als u Dropbox toolist bestanden, bijvoorbeeld uw **2014-12-01-preview** versie schemadefinitie wellicht ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="bd0bb-152">Tijdens het gedeelte van de parameters Hallo Hallo definitie van Logic Apps ongewijzigd blijft, kunt u Hallo equivalente HTTP-actie zoals in dit voorbeeld maken:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="bd0bb-153">Stap voor stap één voor één van deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="bd0bb-154">Eigenschap Action</span><span class="sxs-lookup"><span data-stu-id="bd0bb-154">Action property</span></span> | <span data-ttu-id="bd0bb-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bd0bb-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="bd0bb-156">`Http`In plaats van`APIapp`</span><span class="sxs-lookup"><span data-stu-id="bd0bb-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="bd0bb-157">toouse deze actie Hallo Logic App-ontwerper, zijn onder andere Hallo metagegevenseindpunt, is samengesteld uit:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="bd0bb-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="bd0bb-158">Gemaakt op basis van:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="bd0bb-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="bd0bb-159">Altijd`POST`</span><span class="sxs-lookup"><span data-stu-id="bd0bb-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="bd0bb-160">Parameters voor identieke toohello API-App</span><span class="sxs-lookup"><span data-stu-id="bd0bb-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="bd0bb-161">Identieke toohello API-App-verificatie</span><span class="sxs-lookup"><span data-stu-id="bd0bb-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="bd0bb-162">Deze aanpak moet werken voor alle acties van de API-App.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="bd0bb-163">Vergeet echter niet dat deze vorige API-Apps niet langer worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="bd0bb-164">Daarom moet u overstappen tooone Hallo twee andere vorige opties, een beheerde API of die als host fungeert voor uw aangepaste Web-API.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="bd0bb-165">Herhaal too'foreach hernoemd '</span><span class="sxs-lookup"><span data-stu-id="bd0bb-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="bd0bb-166">We ontvangen voor het vorige schemaversie hello, veel feedback van klanten die **herhalen** verwarrend is en niet goed vast te leggen die **herhalen** werd echt een voor elke lus.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="bd0bb-167">We hebben als gevolg hiervan hernoemd `repeat` te`foreach`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="bd0bb-168">Bijvoorbeeld zou eerder u schrijven:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="bd0bb-169">U zou nu schrijven:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-169">Now you would write:</span></span>

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

<span data-ttu-id="bd0bb-170">Hallo functie `@repeatItem()` is eerder gebruikte tooreference Hallo het huidige item wordt iteratie.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="bd0bb-171">Deze functie is nu te vereenvoudigd`@item()`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="bd0bb-172">Verwijzing naar uitvoer van 'foreach'</span><span class="sxs-lookup"><span data-stu-id="bd0bb-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="bd0bb-173">Voor vereenvoudiging Hallo levert van `foreach` acties niet zijn ingepakt in een object aangeroepen `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="bd0bb-174">Tijdens het Hallo levert van vorige Hallo `repeat` voorbeeld zijn:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-174">While hello outputs from hello previous `repeat` example were:</span></span>

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

<span data-ttu-id="bd0bb-175">Nu zijn deze uitgangen:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-175">Now these outputs are:</span></span>

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

<span data-ttu-id="bd0bb-176">Voorheen tooget toohello hoofdtekst van Hallo actie bij verwijzingen naar deze uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

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

<span data-ttu-id="bd0bb-177">Nu kunt u doen in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-177">Now you can do instead:</span></span>

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

<span data-ttu-id="bd0bb-178">Met deze wijzigingen Hallo functies `@repeatItem()`, `@repeatBody()`, en `@repeatOutputs()` worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="bd0bb-179">Native HTTP-listener</span><span class="sxs-lookup"><span data-stu-id="bd0bb-179">Native HTTP listener</span></span>

<span data-ttu-id="bd0bb-180">Hallo mogelijkheden nu zijn ingebouwd in HTTP-Listener.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="bd0bb-181">Daarom moet u niet langer toodeploy een HTTP-Listener API-App.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="bd0bb-182">Zie [volledige details voor het Hallo toomake uw logische app eindpunt aanroepbare hier](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="bd0bb-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="bd0bb-183">Met deze wijzigingen hebben wij Hallo verwijderd `@accessKeys()` functie, die wordt vervangen door Hallo `@listCallbackURL()` functie voor het ophalen van Hallo eindpunt indien nodig.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="bd0bb-184">Bovendien moet u ten minste één trigger nu definiëren in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="bd0bb-185">Als u wilt dat te`/run` Hallo werkstroom, hebt u een van deze triggers: `manual`, `apiConnectionWebhook`, of `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="bd0bb-186">Aanroepen van onderliggende werkstromen</span><span class="sxs-lookup"><span data-stu-id="bd0bb-186">Call child workflows</span></span>

<span data-ttu-id="bd0bb-187">Voorheen vereist voor het aanroepen van onderliggende werkstromen toohello werkstroom, aan de Hallo-toegangstoken en plakken Hallo token in definitie Hallo logic Apps waar u toocall die onderliggende werkstroom gaan.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="bd0bb-188">Hallo Logic Apps engine genereert automatisch een SAS tijdens runtime voor Hallo onderliggende werkstroom met het nieuwe schema hello, zodat u niet hebt te geen geheimen in plakken Hallo definitie.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="bd0bb-189">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bd0bb-189">Here is an example:</span></span>

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

<span data-ttu-id="bd0bb-190">Een tweede verbetering is dat we Hallo onderliggende geeft werkstromen volledige toegang toohello binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="bd0bb-191">Dit betekent dat u kunt parameters doorgeven in Hallo *query's* sectie en in Hallo *headers* object en die u volledig kunt definiëren Hallo volledige hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="bd0bb-192">Er zijn ten slotte vereiste wijzigingen toohello onderliggende werkstroom.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="bd0bb-193">Terwijl u onderliggende werkstroom eerder rechtstreeks aanroepen kan, moet nu u een trigger-eindpunt in de werkstroom Hallo voor Hallo bovenliggende toocall.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="bd0bb-194">In het algemeen, voegt u een trigger die heeft `manual` typt en gebruik vervolgens deze trigger in Hallo bovenliggende definitie.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="bd0bb-195">Opmerking Hallo `host` eigenschap specifiek heeft een `triggerName` omdat u altijd waarvan de trigger moet opgeven dat u aanroept.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="bd0bb-196">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="bd0bb-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="bd0bb-197">Nieuwe 'query'-eigenschap</span><span class="sxs-lookup"><span data-stu-id="bd0bb-197">New 'queries' property</span></span>

<span data-ttu-id="bd0bb-198">Alle actietypen ondersteunen nu een nieuwe invoer aangeroepen `queries`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="bd0bb-199">Deze gegevens kan worden gestructureerd object, in plaats van u hoeft tooassemble Hallo tekenreeks handmatig.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="bd0bb-200">'Parse()' functie too'json() hernoemd '</span><span class="sxs-lookup"><span data-stu-id="bd0bb-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="bd0bb-201">We toevoegen meer inhoudstypen snel, zodat we Hallo hernoemd `parse()` te functioneren`json()`.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="bd0bb-202">Binnenkort beschikbaar: Enterprise Integration-API's</span><span class="sxs-lookup"><span data-stu-id="bd0bb-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="bd0bb-203">Er zijn momenteel geen beheerde versies nog van Hallo Enterprise Integration-API's, zoals AS2.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="bd0bb-204">Ondertussen kunt u uw bestaande BizTalk-APIs geïmplementeerde via Hallo HTTP-actie.</span><span class="sxs-lookup"><span data-stu-id="bd0bb-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="bd0bb-205">Voor meer informatie Zie ' de reeds geïmplementeerde API-apps gebruiken ' in hello [integratie roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="bd0bb-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
