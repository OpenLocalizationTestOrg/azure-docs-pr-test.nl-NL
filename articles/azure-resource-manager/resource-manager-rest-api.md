---
title: aaaResource Manager REST-API's | Microsoft Docs
description: Een overzicht van Hallo REST-API's van Resource Manager-verificatie en gebruiksvoorbeelden
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>REST API's voor Resource Manager
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure-CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

Achter elke aanroep tooAzure Resource Manager achter elke geïmplementeerde sjabloon achter elke geconfigureerde storage-account zijn er een of meer aanroepen toohello Azure Resource Manager van RESTful-API. Dit onderwerp is besteed toothose API's en hoe u ze kunt aanroepen zonder helemaal SDK gebruiken. Deze aanpak is handig als u volledig beheer van aanvragen tooAzure wilt, of als Hallo SDK voor uw voorkeurstaal is niet beschikbaar of biedt geen ondersteuning voor Hallo-bewerkingen die u nodig hebt.

In dit artikel via elke API die wordt weergegeven in Azure, maar in plaats daarvan maakt gebruik van bepaalde bewerkingen als voorbeelden van hoe u verbinding toothem maakt niet. Nadat u Hallo basisbeginselen, kunt u lezen Hallo [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind gedetailleerde informatie over hoe toouse Hallo rest van Hallo API's.

## <a name="authentication"></a>Authentication
Verificatie voor Resource Manager is verwerkt door Azure Active Directory (AD). tooconnect tooany API, moet u eerst tooauthenticate met Azure AD-tooreceive geen verificatietoken dat u bij tooevery-aanvraag doorgeven kunt. Als we zijn met een beschrijving van een aanroep van pure direct toohello REST-API's, gaan we ervan uit dat u niet dat tooauthenticate wilt door u wordt gevraagd om een gebruikersnaam en wachtwoord. We ook wordt ervan uitgegaan dat u geen gebruikmaakt van twee mechanismen voor factor-verificatie. We ook maken wat wordt een Azure AD-toepassing en een service-principal die gebruikte toolog in genoemd. Maar houd er rekening mee dat Azure AD ondersteunen verschillende procedures voor verificatie en ze alle gebruikte tooretrieve die verificatietoken die we nodig hebben voor de volgende API-aanvragen kan worden.
Ga als volgt [maken van Azure AD-toepassing en Service-Principal](resource-group-create-service-principal-portal.md) voor stapsgewijze instructies.

### <a name="generating-an-access-token"></a>Genereren van een toegangstoken
Verificatie met Azure AD wordt gedaan door het aanroepen van tooAzure AD, zich bevindt op login.microsoftonline.com. tooauthenticate, moet u toohave Hallo volgende informatie:

* Azure AD-Tenant-ID (naam van die Azure AD gebruikt u toolog in hello, Hallo vaak hetzelfde als uw bedrijf, maar niet nodig)
* Toepassings-ID (die zijn uitgevoerd tijdens stap van het maken van toepassing hello Azure AD)
* Wachtwoord (die u hebt geselecteerd tijdens het maken van Azure AD-toepassing hello)

Zorg ervoor dat tooreplace 'Azure AD-Tenant-ID', 'Toepassings-ID' en 'Password' met de juiste waarden Hallo in Hallo HTTP-aanvraag te volgen.

**Algemene HTTP-aanvraag:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... wordt (als de verificatie slaagt) leiden tot een reactie vergelijkbaar toohello antwoord te volgen:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(Hallo access_token in Hallo voorafgaand aan de reactie is verkort tooincrease leesbaarheid)

**Genereren met behulp van Bash toegangstoken:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Genereren met behulp van PowerShell toegangstoken:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

Hallo-antwoord bevat een toegangstoken, informatie over hoe lang dat token geldig is en informatie over welke resource kunt u dat token voor.
Hallo toegangstoken die u hebt ontvangen in de vorige aanroep van HTTP-Hallo moet worden doorgegeven voor alle aanvraag toohello Resource Manager-API. Als u doorgeeft als een headerwaarde met de naam 'Autorisatie' Hallo-waarde 'Bearer YOUR_ACCESS_TOKEN'. U ziet Hallo ruimte tussen 'Bearer' en uw toegangstoken.

Zoals u van Hallo boven HTTP-resultaat zien kunt, is Hallo token geldig voor een bepaalde periode gedurende welke u moet in de cache en dat hetzelfde token opnieuw gebruiken. Zelfs als het is mogelijk tooauthenticate met Azure AD voor elke API-aanroep, zou het zeer inefficiënt zijn.

## <a name="calling-resource-manager-rest-apis"></a>Aanroepen van Resource Manager REST-API 's
In dit onderwerp wordt alleen gebruikt voor een paar API's tooexplain Hallo basisgebruik van Hallo REST-bewerkingen. Zie voor meer informatie over alle Hallo bewerkingen [Azure Resource Manager REST API's](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Lijst van alle abonnementen
Een van de Hallo eenvoudigste bewerkingen die u kunt doen is toolist Hallo beschikbare abonnementen waartoe u toegang hebt. Hallo na aanvraag, ziet u hoe Hallo toegangstoken is doorgegeven als een header:

(YOUR_ACCESS_TOKEN vervangen door uw werkelijke Access Token).

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... daardoor hebt u een lijst met abonnementen dat deze service-principal tooaccess is toegestaan

(Abonnement-id's zijn ingekort voor leesbaarheid)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Lijst van alle resourcegroepen in een specifiek abonnement
Alle resources die beschikbaar zijn met de Hallo Resource Manager-API's zijn genest binnen een resourcegroep. U kunt een Resource Manager query voor bestaande resourcegroepen in uw abonnement met Hallo HTTP GET-aanvraag te volgen. U ziet hoe Hallo abonnements-ID is doorgegeven als onderdeel van Hallo-URL van deze tijd.

(YOUR_ACCESS_TOKEN en SUBSCRIPTION_ID vervangen door uw werkelijke access token en de abonnement-ID)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Hallo u antwoord is afhankelijk van of u gedefinieerd bronnengroepen hebt en zo ja, hoeveel.

(Abonnement-id's zijn ingekort voor leesbaarheid)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken
Tot nu toe hebben we alleen is opvragen Hallo Resource Manager-API's voor meer informatie. Is het tijd we sommige resources maken en u begint met het Hallo eenvoudigste hiervan alle, een resourcegroep. Hallo volgende HTTP-aanvraag maakt een resourcegroep in een regio of de locatie van uw keuze en voegt een label tooit.

(YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME vervangen door uw werkelijke Access Token, abonnements-ID en naam van resourcegroep die u wilt dat toocreate Hallo)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

Als dit lukt, kunt u een antwoord dat vergelijkbare toohello na antwoord krijgen:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

U hebt een resourcegroep gemaakt in Azure. Gefeliciteerd.

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Tooa-resourcegroep voor de resources met een Resource Manager-sjabloon implementeren
Met Resource Manager kunt u uw resources met behulp van sjablonen implementeren. Een sjabloon worden gedefinieerd voor verschillende resources en de bijbehorende afhankelijkheden. Voor deze sectie we ervan uitgaan dat u bekend bent met Resource Manager-sjablonen en we enkel laten zien hoe toomake Hallo API aanroepen toostart implementatie. Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).

Implementatie van een sjabloon verschillen niet veel toohow u andere API aanroepen. Een belangrijk aspect is dat de implementatie van een sjabloon kan erg lang duren. Hallo API-aanroep slechts retourneert en is tooyou als ontwikkelaar tooquery van status van Hallo implementatie toofind uit als het Hallo-implementatie is voltooid. Zie voor meer informatie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).

In dit voorbeeld gebruiken we een openbaar blootgestelde sjabloon beschikbaar is op [GitHub](https://github.com/Azure/azure-quickstart-templates). Hallo-sjabloon we gebruiken implementeert een Linux-VM toohello VS-West regio. Hoewel dit voorbeeld wordt een beschikbare sjabloon in een openbare opslagplaats, zoals GitHub gebruikt, kunt u in plaats daarvan de volledige sjabloon Hallo als onderdeel van de aanvraag Hallo doorgeven. Let op: we parameterwaarden in Hallo-aanvraag die worden gebruikt binnen Hallo opgeven geïmplementeerd sjabloon.

(SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD en DNS_NAME_FOR_PUBLIC_IP toovalues geschikt is voor uw aanvraag vervangen)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

Hallo lang JSON-antwoord voor deze aanvraag is weggelaten tooimprove leesbaarheid van deze documentatie. Hallo-antwoord bevat informatie over de sjablonen Hallo-implementatie die u hebt gemaakt.

## <a name="next-steps"></a>Volgende stappen

- toolearn over het verwerken van asynchrone REST-bewerkingen, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).
