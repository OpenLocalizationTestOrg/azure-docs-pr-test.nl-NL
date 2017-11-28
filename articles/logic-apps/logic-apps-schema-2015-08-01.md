---
title: Schema-updates augustus-1-2015 preview - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="56181-103">Schema-updates voor Azure Logic Apps - preview 1 augustus 2015</span><span class="sxs-lookup"><span data-stu-id="56181-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="56181-104">Deze nieuwe schema en de API-versie voor Azure Logic Apps bevat belangrijke verbeteringen die logische apps betrouwbaarder en eenvoudiger te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="56181-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="56181-105">De **APIApp** actietype wordt bijgewerkt naar een nieuwe [ **APIConnection** ](#api-connections) action-type.</span><span class="sxs-lookup"><span data-stu-id="56181-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="56181-106">**Herhaal** is gewijzigd in [ **Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="56181-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="56181-107">De [ **HTTP-Listener** API-App](#http-listener) is niet langer vereist.</span><span class="sxs-lookup"><span data-stu-id="56181-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="56181-108">Het aanroepen van onderliggende werkstromen gebruikt een [nieuwe schema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="56181-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="56181-109">Verplaatsen naar de API-verbindingen</span><span class="sxs-lookup"><span data-stu-id="56181-109">Move to API connections</span></span>

<span data-ttu-id="56181-110">De grootste wijziging is dat u niet langer API-Apps implementeren in uw Azure-abonnement moet, zodat u API's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56181-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="56181-111">Hier volgen de manieren waarop u API's kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="56181-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="56181-112">Beheerde API 's</span><span class="sxs-lookup"><span data-stu-id="56181-112">Managed APIs</span></span>
* <span data-ttu-id="56181-113">Uw aangepaste Web-API 's</span><span class="sxs-lookup"><span data-stu-id="56181-113">Your custom Web APIs</span></span>

<span data-ttu-id="56181-114">Elke manier wordt anders verwerkt omdat het beheer en het hosten van modellen verschillend zijn.</span><span class="sxs-lookup"><span data-stu-id="56181-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="56181-115">Een voordeel van dit model is dat u bent niet meer beperkt tot resources die zijn geïmplementeerd in uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="56181-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="56181-116">Beheerde API 's</span><span class="sxs-lookup"><span data-stu-id="56181-116">Managed APIs</span></span>

<span data-ttu-id="56181-117">Microsoft beheert sommige API's namens u, zoals Office 365, Salesforce, Twitter en FTP.</span><span class="sxs-lookup"><span data-stu-id="56181-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="56181-118">U kunt sommige beheerde API's als-is, zoals Bing vertalen, terwijl anderen configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="56181-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="56181-119">Deze configuratie wordt aangeroepen een *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="56181-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="56181-120">Wanneer u Office 365 gebruikt, moet u bijvoorbeeld een verbinding met uw Office 365-in-token maken.</span><span class="sxs-lookup"><span data-stu-id="56181-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="56181-121">Dit token is veilig opgeslagen en wordt vernieuwd zodat uw logische app kunt altijd de Office 365-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="56181-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="56181-122">Als u wilt verbinding maken met uw SQL- of FTP-server, moet u ook een verbinding met de verbindingsreeks maken.</span><span class="sxs-lookup"><span data-stu-id="56181-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="56181-123">In deze definitie deze acties worden genoemd `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="56181-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="56181-124">Hier volgt een voorbeeld van een verbinding die Office 365 voor het verzenden van een e-mailbericht aanroept:</span><span class="sxs-lookup"><span data-stu-id="56181-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="56181-125">De `host` object is gedeelte van de ingangen die uniek is voor de API-verbindingen en bestaat uit twee delen: `api` en `connection`.</span><span class="sxs-lookup"><span data-stu-id="56181-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="56181-126">De `api` heeft de runtime URL van het waar dat beheerd API wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="56181-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="56181-127">U kunt zien alle beschikbare beheerde API's door het aanroepen van `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="56181-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="56181-128">Wanneer u een API gebruikt, de API kan of kunnen geen *verbindingsparameters* gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="56181-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="56181-129">De API niet het geval, geen *verbinding* is vereist.</span><span class="sxs-lookup"><span data-stu-id="56181-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="56181-130">Als de API is, moet u een verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="56181-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="56181-131">De gemaakte verbinding heeft de naam die u kiest.</span><span class="sxs-lookup"><span data-stu-id="56181-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="56181-132">U vervolgens verwijzen naar de naam in de `connection` object binnen de `host` object.</span><span class="sxs-lookup"><span data-stu-id="56181-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="56181-133">Een verbinding wilt maken in een resourcegroep, aanroepen:</span><span class="sxs-lookup"><span data-stu-id="56181-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="56181-134">Met de volgende hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="56181-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="56181-135">Beheerde API's in een Azure Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="56181-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="56181-136">U kunt een volledige toepassing in een Azure Resource Manager-sjabloon maken, zolang interactief aanmelden is niet vereist.</span><span class="sxs-lookup"><span data-stu-id="56181-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="56181-137">Als aanmelden vereist is, kunt u een alles met Azure Resource Manager-sjabloon instellen, maar u hebt nog wel gaat u naar de portal voor het autoriseren van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="56181-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="56181-138">U kunt zien in dit voorbeeld is dat de verbindingen zijn alleen bronnen die bevinden zich in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="56181-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="56181-139">Ze verwijzen naar de beheerde API's die u in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="56181-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="56181-140">Uw aangepaste Web-API 's</span><span class="sxs-lookup"><span data-stu-id="56181-140">Your custom Web APIs</span></span>

<span data-ttu-id="56181-141">Als u uw eigen API's, die niet door Microsoft beheerde gebruiken de ingebouwde **HTTP** actie die moet worden ze aanroept.</span><span class="sxs-lookup"><span data-stu-id="56181-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="56181-142">Voor een ideaal ervaring, moet u een Swagger-eindpunt weergeven voor uw API.</span><span class="sxs-lookup"><span data-stu-id="56181-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="56181-143">Dit eindpunt maakt de Logic App-ontwerper voor het weergeven van de invoer en uitvoer voor uw API.</span><span class="sxs-lookup"><span data-stu-id="56181-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="56181-144">Zonder Swagger, kan de designer alleen weergeven in- en uitgangen als ondoorzichtige JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="56181-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="56181-145">Hier volgt een voorbeeld van de nieuwe `metadata.apiDefinitionUrl` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="56181-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="56181-146">Als u uw Web-API op Azure App Service host, wordt uw Web-API automatisch weergegeven in de lijst met acties die beschikbaar zijn in de ontwerpfunctie.</span><span class="sxs-lookup"><span data-stu-id="56181-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="56181-147">Als dat niet het geval is, hebt u rechtstreeks in de URL plakken.</span><span class="sxs-lookup"><span data-stu-id="56181-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="56181-148">Het Swagger-eindpunt moet worden niet-geverifieerde om te worden gebruikt in de ontwerpfunctie voor Logic App Hoewel u de API zichzelf met welke methoden die ondersteuning biedt voor Swagger kunt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="56181-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="56181-149">Aanroepen van geïmplementeerde API-apps met 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="56181-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="56181-150">Als u een API-App hebt geïmplementeerd, kunt u de app met bellen de **HTTP** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="56181-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="56181-151">Als u Dropbox weergeven van bestanden, bijvoorbeeld uw **2014-12-01-preview** versie schemadefinitie wellicht ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="56181-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="56181-152">U kunt de equivalente HTTP-actie zoals in dit voorbeeld maken terwijl de parameters-sectie van de definitie van Logic Apps ongewijzigd blijft:</span><span class="sxs-lookup"><span data-stu-id="56181-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="56181-153">Stap voor stap één voor één van deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="56181-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="56181-154">Eigenschap Action</span><span class="sxs-lookup"><span data-stu-id="56181-154">Action property</span></span> | <span data-ttu-id="56181-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="56181-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="56181-156">`Http`In plaats van`APIapp`</span><span class="sxs-lookup"><span data-stu-id="56181-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="56181-157">Als u wilt gebruiken met deze actie in de ontwerpfunctie voor Logic App, zijn de metagegevenseindpunt is samengesteld uit:`{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="56181-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="56181-158">Gemaakt op basis van:`{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="56181-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="56181-159">Altijd`POST`</span><span class="sxs-lookup"><span data-stu-id="56181-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="56181-160">Identiek aan de API-App-parameters</span><span class="sxs-lookup"><span data-stu-id="56181-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="56181-161">Identiek aan de API-App-verificatie</span><span class="sxs-lookup"><span data-stu-id="56181-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="56181-162">Deze aanpak moet werken voor alle acties van de API-App.</span><span class="sxs-lookup"><span data-stu-id="56181-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="56181-163">Vergeet echter niet dat deze vorige API-Apps niet langer worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="56181-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="56181-164">Daarom moet u overstappen op een van de twee andere vorige opties, een beheerde API of die als host fungeert voor uw aangepaste Web-API.</span><span class="sxs-lookup"><span data-stu-id="56181-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="56181-165">De naam 'Herhaal' gewijzigd in 'foreach'</span><span class="sxs-lookup"><span data-stu-id="56181-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="56181-166">We ontvangen voor de vorige schemaversie veel feedback van klanten die **herhalen** verwarrend is en niet goed vast te leggen die **herhalen** werd echt een voor elke lus.</span><span class="sxs-lookup"><span data-stu-id="56181-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="56181-167">We hebben als gevolg hiervan hernoemd `repeat` naar `foreach`.</span><span class="sxs-lookup"><span data-stu-id="56181-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="56181-168">Bijvoorbeeld zou eerder u schrijven:</span><span class="sxs-lookup"><span data-stu-id="56181-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="56181-169">U zou nu schrijven:</span><span class="sxs-lookup"><span data-stu-id="56181-169">Now you would write:</span></span>

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

<span data-ttu-id="56181-170">De functie `@repeatItem()` eerder werd gebruikt om te verwijzen naar het huidige item wordt iteratie.</span><span class="sxs-lookup"><span data-stu-id="56181-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="56181-171">Deze functie is nu eenvoudiger te `@item()`.</span><span class="sxs-lookup"><span data-stu-id="56181-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="56181-172">Verwijzing naar uitvoer van 'foreach'</span><span class="sxs-lookup"><span data-stu-id="56181-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="56181-173">Voor de uitvoer van vereenvoudiging `foreach` acties niet zijn ingepakt in een object aangeroepen `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="56181-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="56181-174">Terwijl de uitvoer van de vorige `repeat` voorbeeld zijn:</span><span class="sxs-lookup"><span data-stu-id="56181-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="56181-175">Nu zijn deze uitgangen:</span><span class="sxs-lookup"><span data-stu-id="56181-175">Now these outputs are:</span></span>

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

<span data-ttu-id="56181-176">Voorheen om aan de hoofdtekst van de actie die verwijzen naar deze uitvoer:</span><span class="sxs-lookup"><span data-stu-id="56181-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="56181-177">Nu kunt u doen in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="56181-177">Now you can do instead:</span></span>

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

<span data-ttu-id="56181-178">Met deze wijzigingen, de functies `@repeatItem()`, `@repeatBody()`, en `@repeatOutputs()` worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="56181-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="56181-179">Native HTTP-listener</span><span class="sxs-lookup"><span data-stu-id="56181-179">Native HTTP listener</span></span>

<span data-ttu-id="56181-180">De HTTP-Listener-mogelijkheden zijn nu ingebouwd in.</span><span class="sxs-lookup"><span data-stu-id="56181-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="56181-181">Daarom moet u niet meer voor het implementeren van een HTTP-Listener API-App.</span><span class="sxs-lookup"><span data-stu-id="56181-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="56181-182">Zie [de volledige details voor het maken van uw logische app eindpunt aanroepbare hier](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="56181-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="56181-183">Met deze wijzigingen verwijderd we de `@accessKeys()` functie, die wordt vervangen door de `@listCallbackURL()` functie voor het ophalen van het eindpunt indien nodig.</span><span class="sxs-lookup"><span data-stu-id="56181-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="56181-184">Bovendien moet u ten minste één trigger nu definiëren in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="56181-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="56181-185">Als u wilt `/run` de werkstroom, hebt u een van deze triggers: `manual`, `apiConnectionWebhook`, of `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="56181-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="56181-186">Aanroepen van onderliggende werkstromen</span><span class="sxs-lookup"><span data-stu-id="56181-186">Call child workflows</span></span>

<span data-ttu-id="56181-187">Het aanroepen van onderliggende werkstromen vereist voorheen gaan naar de werkstroom, het toegangstoken ophalen en het token in de definitie van logic Apps waar u aan te roepen die onderliggende werkstroom wilt plakken.</span><span class="sxs-lookup"><span data-stu-id="56181-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="56181-188">Met het nieuwe schema genereert de Logic Apps-engine automatisch een SAS tijdens runtime voor de onderliggende werkstroom zodat u hoeft geen geheimen in de definitie te plakken.</span><span class="sxs-lookup"><span data-stu-id="56181-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="56181-189">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="56181-189">Here is an example:</span></span>

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

<span data-ttu-id="56181-190">Een tweede verbetering is dat we zijn de onderliggende werkstromen volledige toegang geven tot de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="56181-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="56181-191">Dit betekent dat u kunt de parameters in doorgeven dat de *query's* sectie en in de *headers* object en die u kunt de volledige hoofdtekst volledig definiëren.</span><span class="sxs-lookup"><span data-stu-id="56181-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="56181-192">Er zijn ten slotte vereist wijzigingen in de onderliggende werkstroom.</span><span class="sxs-lookup"><span data-stu-id="56181-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="56181-193">Terwijl u onderliggende werkstroom eerder rechtstreeks aanroepen kan, moet nu u een trigger-eindpunt in de werkstroom voor de bovenliggende aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="56181-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="56181-194">In het algemeen, voegt u een trigger die heeft `manual` typen en vervolgens deze trigger te gebruiken in de definitie van de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="56181-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="56181-195">Opmerking de `host` eigenschap specifiek heeft een `triggerName` omdat u altijd waarvan de trigger moet opgeven dat u aanroept.</span><span class="sxs-lookup"><span data-stu-id="56181-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="56181-196">Andere wijzigingen</span><span class="sxs-lookup"><span data-stu-id="56181-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="56181-197">Nieuwe 'query'-eigenschap</span><span class="sxs-lookup"><span data-stu-id="56181-197">New 'queries' property</span></span>

<span data-ttu-id="56181-198">Alle actietypen ondersteunen nu een nieuwe invoer aangeroepen `queries`.</span><span class="sxs-lookup"><span data-stu-id="56181-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="56181-199">Deze gegevens kan worden gestructureerd object, in plaats van u hoeft voor het samenstellen van de tekenreeks met de hand.</span><span class="sxs-lookup"><span data-stu-id="56181-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="56181-200">Nieuwe naam parse() functie 'json()'</span><span class="sxs-lookup"><span data-stu-id="56181-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="56181-201">We toevoegen meer inhoudstypen snel, zodat we hernoemd de `parse()` functie `json()`.</span><span class="sxs-lookup"><span data-stu-id="56181-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="56181-202">Binnenkort beschikbaar: Enterprise Integration-API's</span><span class="sxs-lookup"><span data-stu-id="56181-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="56181-203">Er zijn momenteel geen beheerde versies nog van de Enterprise Integration-API's, zoals AS2.</span><span class="sxs-lookup"><span data-stu-id="56181-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="56181-204">Ondertussen kunt u uw bestaande BizTalk-APIs geïmplementeerde via de HTTP-actie.</span><span class="sxs-lookup"><span data-stu-id="56181-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="56181-205">Voor meer informatie Zie ' de reeds geïmplementeerde API-apps gebruiken ' in de [integratie roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="56181-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
