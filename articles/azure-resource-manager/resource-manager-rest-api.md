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
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="ef102-103">REST API's voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef102-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef102-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef102-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="ef102-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="ef102-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="ef102-106">Portal</span><span class="sxs-lookup"><span data-stu-id="ef102-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="ef102-107">REST API</span><span class="sxs-lookup"><span data-stu-id="ef102-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="ef102-108">Achter elke aanroep tooAzure Resource Manager achter elke geïmplementeerde sjabloon achter elke geconfigureerde storage-account zijn er een of meer aanroepen toohello Azure Resource Manager van RESTful-API.</span><span class="sxs-lookup"><span data-stu-id="ef102-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="ef102-109">Dit onderwerp is besteed toothose API's en hoe u ze kunt aanroepen zonder helemaal SDK gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef102-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="ef102-110">Deze aanpak is handig als u volledig beheer van aanvragen tooAzure wilt, of als Hallo SDK voor uw voorkeurstaal is niet beschikbaar of biedt geen ondersteuning voor Hallo-bewerkingen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="ef102-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="ef102-111">In dit artikel via elke API die wordt weergegeven in Azure, maar in plaats daarvan maakt gebruik van bepaalde bewerkingen als voorbeelden van hoe u verbinding toothem maakt niet.</span><span class="sxs-lookup"><span data-stu-id="ef102-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="ef102-112">Nadat u Hallo basisbeginselen, kunt u lezen Hallo [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind gedetailleerde informatie over hoe toouse Hallo rest van Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="ef102-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="ef102-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="ef102-113">Authentication</span></span>
<span data-ttu-id="ef102-114">Verificatie voor Resource Manager is verwerkt door Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="ef102-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="ef102-115">tooconnect tooany API, moet u eerst tooauthenticate met Azure AD-tooreceive geen verificatietoken dat u bij tooevery-aanvraag doorgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="ef102-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="ef102-116">Als we zijn met een beschrijving van een aanroep van pure direct toohello REST-API's, gaan we ervan uit dat u niet dat tooauthenticate wilt door u wordt gevraagd om een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ef102-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="ef102-117">We ook wordt ervan uitgegaan dat u geen gebruikmaakt van twee mechanismen voor factor-verificatie.</span><span class="sxs-lookup"><span data-stu-id="ef102-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="ef102-118">We ook maken wat wordt een Azure AD-toepassing en een service-principal die gebruikte toolog in genoemd.</span><span class="sxs-lookup"><span data-stu-id="ef102-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="ef102-119">Maar houd er rekening mee dat Azure AD ondersteunen verschillende procedures voor verificatie en ze alle gebruikte tooretrieve die verificatietoken die we nodig hebben voor de volgende API-aanvragen kan worden.</span><span class="sxs-lookup"><span data-stu-id="ef102-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="ef102-120">Ga als volgt [maken van Azure AD-toepassing en Service-Principal](resource-group-create-service-principal-portal.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="ef102-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="ef102-121">Genereren van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="ef102-121">Generating an Access Token</span></span>
<span data-ttu-id="ef102-122">Verificatie met Azure AD wordt gedaan door het aanroepen van tooAzure AD, zich bevindt op login.microsoftonline.com. tooauthenticate, moet u toohave Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="ef102-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="ef102-123">Azure AD-Tenant-ID (naam van die Azure AD gebruikt u toolog in hello, Hallo vaak hetzelfde als uw bedrijf, maar niet nodig)</span><span class="sxs-lookup"><span data-stu-id="ef102-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="ef102-124">Toepassings-ID (die zijn uitgevoerd tijdens stap van het maken van toepassing hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ef102-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="ef102-125">Wachtwoord (die u hebt geselecteerd tijdens het maken van Azure AD-toepassing hello)</span><span class="sxs-lookup"><span data-stu-id="ef102-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="ef102-126">Zorg ervoor dat tooreplace 'Azure AD-Tenant-ID', 'Toepassings-ID' en 'Password' met de juiste waarden Hallo in Hallo HTTP-aanvraag te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef102-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="ef102-127">**Algemene HTTP-aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="ef102-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="ef102-128">... wordt (als de verificatie slaagt) leiden tot een reactie vergelijkbaar toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef102-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="ef102-129">(Hallo access_token in Hallo voorafgaand aan de reactie is verkort tooincrease leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="ef102-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="ef102-130">**Genereren met behulp van Bash toegangstoken:**</span><span class="sxs-lookup"><span data-stu-id="ef102-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="ef102-131">**Genereren met behulp van PowerShell toegangstoken:**</span><span class="sxs-lookup"><span data-stu-id="ef102-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="ef102-132">Hallo-antwoord bevat een toegangstoken, informatie over hoe lang dat token geldig is en informatie over welke resource kunt u dat token voor.</span><span class="sxs-lookup"><span data-stu-id="ef102-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="ef102-133">Hallo toegangstoken die u hebt ontvangen in de vorige aanroep van HTTP-Hallo moet worden doorgegeven voor alle aanvraag toohello Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="ef102-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="ef102-134">Als u doorgeeft als een headerwaarde met de naam 'Autorisatie' Hallo-waarde 'Bearer YOUR_ACCESS_TOKEN'.</span><span class="sxs-lookup"><span data-stu-id="ef102-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="ef102-135">U ziet Hallo ruimte tussen 'Bearer' en uw toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="ef102-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="ef102-136">Zoals u van Hallo boven HTTP-resultaat zien kunt, is Hallo token geldig voor een bepaalde periode gedurende welke u moet in de cache en dat hetzelfde token opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef102-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="ef102-137">Zelfs als het is mogelijk tooauthenticate met Azure AD voor elke API-aanroep, zou het zeer inefficiënt zijn.</span><span class="sxs-lookup"><span data-stu-id="ef102-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="ef102-138">Aanroepen van Resource Manager REST-API 's</span><span class="sxs-lookup"><span data-stu-id="ef102-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="ef102-139">In dit onderwerp wordt alleen gebruikt voor een paar API's tooexplain Hallo basisgebruik van Hallo REST-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ef102-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="ef102-140">Zie voor meer informatie over alle Hallo bewerkingen [Azure Resource Manager REST API's](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="ef102-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="ef102-141">Lijst van alle abonnementen</span><span class="sxs-lookup"><span data-stu-id="ef102-141">List all subscriptions</span></span>
<span data-ttu-id="ef102-142">Een van de Hallo eenvoudigste bewerkingen die u kunt doen is toolist Hallo beschikbare abonnementen waartoe u toegang hebt.</span><span class="sxs-lookup"><span data-stu-id="ef102-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="ef102-143">Hallo na aanvraag, ziet u hoe Hallo toegangstoken is doorgegeven als een header:</span><span class="sxs-lookup"><span data-stu-id="ef102-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="ef102-144">(YOUR_ACCESS_TOKEN vervangen door uw werkelijke Access Token).</span><span class="sxs-lookup"><span data-stu-id="ef102-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="ef102-145">... daardoor hebt u een lijst met abonnementen dat deze service-principal tooaccess is toegestaan</span><span class="sxs-lookup"><span data-stu-id="ef102-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="ef102-146">(Abonnement-id's zijn ingekort voor leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="ef102-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="ef102-147">Lijst van alle resourcegroepen in een specifiek abonnement</span><span class="sxs-lookup"><span data-stu-id="ef102-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="ef102-148">Alle resources die beschikbaar zijn met de Hallo Resource Manager-API's zijn genest binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef102-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="ef102-149">U kunt een Resource Manager query voor bestaande resourcegroepen in uw abonnement met Hallo HTTP GET-aanvraag te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef102-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="ef102-150">U ziet hoe Hallo abonnements-ID is doorgegeven als onderdeel van Hallo-URL van deze tijd.</span><span class="sxs-lookup"><span data-stu-id="ef102-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="ef102-151">(YOUR_ACCESS_TOKEN en SUBSCRIPTION_ID vervangen door uw werkelijke access token en de abonnement-ID)</span><span class="sxs-lookup"><span data-stu-id="ef102-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="ef102-152">Hallo u antwoord is afhankelijk van of u gedefinieerd bronnengroepen hebt en zo ja, hoeveel.</span><span class="sxs-lookup"><span data-stu-id="ef102-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="ef102-153">(Abonnement-id's zijn ingekort voor leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="ef102-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="ef102-154">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ef102-154">Create a resource group</span></span>
<span data-ttu-id="ef102-155">Tot nu toe hebben we alleen is opvragen Hallo Resource Manager-API's voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef102-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="ef102-156">Is het tijd we sommige resources maken en u begint met het Hallo eenvoudigste hiervan alle, een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef102-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="ef102-157">Hallo volgende HTTP-aanvraag maakt een resourcegroep in een regio of de locatie van uw keuze en voegt een label tooit.</span><span class="sxs-lookup"><span data-stu-id="ef102-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="ef102-158">(YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME vervangen door uw werkelijke Access Token, abonnements-ID en naam van resourcegroep die u wilt dat toocreate Hallo)</span><span class="sxs-lookup"><span data-stu-id="ef102-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="ef102-159">Als dit lukt, kunt u een antwoord dat vergelijkbare toohello na antwoord krijgen:</span><span class="sxs-lookup"><span data-stu-id="ef102-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="ef102-160">U hebt een resourcegroep gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef102-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="ef102-161">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="ef102-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="ef102-162">Tooa-resourcegroep voor de resources met een Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="ef102-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="ef102-163">Met Resource Manager kunt u uw resources met behulp van sjablonen implementeren.</span><span class="sxs-lookup"><span data-stu-id="ef102-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="ef102-164">Een sjabloon worden gedefinieerd voor verschillende resources en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="ef102-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="ef102-165">Voor deze sectie we ervan uitgaan dat u bekend bent met Resource Manager-sjablonen en we enkel laten zien hoe toomake Hallo API aanroepen toostart implementatie.</span><span class="sxs-lookup"><span data-stu-id="ef102-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="ef102-166">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ef102-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ef102-167">Implementatie van een sjabloon verschillen niet veel toohow u andere API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ef102-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="ef102-168">Een belangrijk aspect is dat de implementatie van een sjabloon kan erg lang duren.</span><span class="sxs-lookup"><span data-stu-id="ef102-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="ef102-169">Hallo API-aanroep slechts retourneert en is tooyou als ontwikkelaar tooquery van status van Hallo implementatie toofind uit als het Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ef102-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="ef102-170">Zie voor meer informatie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ef102-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="ef102-171">In dit voorbeeld gebruiken we een openbaar blootgestelde sjabloon beschikbaar is op [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ef102-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="ef102-172">Hallo-sjabloon we gebruiken implementeert een Linux-VM toohello VS-West regio.</span><span class="sxs-lookup"><span data-stu-id="ef102-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="ef102-173">Hoewel dit voorbeeld wordt een beschikbare sjabloon in een openbare opslagplaats, zoals GitHub gebruikt, kunt u in plaats daarvan de volledige sjabloon Hallo als onderdeel van de aanvraag Hallo doorgeven.</span><span class="sxs-lookup"><span data-stu-id="ef102-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="ef102-174">Let op: we parameterwaarden in Hallo-aanvraag die worden gebruikt binnen Hallo opgeven geïmplementeerd sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ef102-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="ef102-175">(SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD en DNS_NAME_FOR_PUBLIC_IP toovalues geschikt is voor uw aanvraag vervangen)</span><span class="sxs-lookup"><span data-stu-id="ef102-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="ef102-176">Hallo lang JSON-antwoord voor deze aanvraag is weggelaten tooimprove leesbaarheid van deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="ef102-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="ef102-177">Hallo-antwoord bevat informatie over de sjablonen Hallo-implementatie die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef102-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef102-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef102-178">Next steps</span></span>

- <span data-ttu-id="ef102-179">toolearn over het verwerken van asynchrone REST-bewerkingen, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ef102-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
