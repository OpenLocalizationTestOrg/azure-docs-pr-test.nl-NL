---
title: REST-API's van Resource Manager | Microsoft Docs
description: Een overzicht van de REST-API's van Resource Manager-verificatie- en gebruiksgegevens-voorbeelden
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
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="a2481-103">REST API's voor Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2481-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2481-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2481-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a2481-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="a2481-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a2481-106">Portal</span><span class="sxs-lookup"><span data-stu-id="a2481-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="a2481-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a2481-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="a2481-108">Achter elke aanroep in Azure Resource Manager achter elke geïmplementeerde sjabloon achter elke geconfigureerde storage-account zijn er een of meer aanroepen naar de Azure Resource Manager-RESTful-API.</span><span class="sxs-lookup"><span data-stu-id="a2481-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="a2481-109">In dit onderwerp wordt besteed aan de API's en hoe u ze kunt aanroepen zonder een SDK helemaal.</span><span class="sxs-lookup"><span data-stu-id="a2481-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="a2481-110">Deze methode is handig als u volledig beheer van aanvragen naar Azure wilt, of als de SDK voor uw voorkeurstaal niet beschikbaar is of biedt geen ondersteuning voor de bewerkingen die u nodig.</span><span class="sxs-lookup"><span data-stu-id="a2481-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="a2481-111">In dit artikel verder niet via elke API die wordt weergegeven in Azure, maar in plaats daarvan maakt gebruik van bepaalde bewerkingen als voorbeelden van hoe u verbinding mee te maken.</span><span class="sxs-lookup"><span data-stu-id="a2481-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="a2481-112">Nadat u de basisbeginselen, kunt u lezen de [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) voor gedetailleerde informatie over het gebruik van de rest van de API's.</span><span class="sxs-lookup"><span data-stu-id="a2481-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="a2481-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="a2481-113">Authentication</span></span>
<span data-ttu-id="a2481-114">Verificatie voor Resource Manager is verwerkt door Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="a2481-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="a2481-115">Als u wilt verbinding maken met API's, moet u eerst om te verifiëren met Azure AD ontvangt geen verificatietoken die u aan elke aanvraag doorgeven kunt.</span><span class="sxs-lookup"><span data-stu-id="a2481-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="a2481-116">Als we beschrijving van een aanroep van pure rechtstreeks aan de REST API's, gaan we ervan uit dat u niet verifiëren wilt met een gebruikersnaam en wachtwoord wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a2481-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="a2481-117">We ook wordt ervan uitgegaan dat u geen gebruikmaakt van twee mechanismen voor factor-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a2481-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="a2481-118">We maken daarom, wat een Azure AD-toepassing en een service principal die worden gebruikt voor het aanmelden wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a2481-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="a2481-119">Maar houd er rekening mee dat Azure AD ondersteunen verschillende procedures voor verificatie en deze kan worden gebruikt om op te halen die verificatietoken die we nodig hebben voor de volgende API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a2481-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="a2481-120">Ga als volgt [maken van Azure AD-toepassing en Service-Principal](resource-group-create-service-principal-portal.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="a2481-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="a2481-121">Genereren van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="a2481-121">Generating an Access Token</span></span>
<span data-ttu-id="a2481-122">Verificatie met Azure AD wordt uitgevoerd door Azure AD, die zich bevindt op login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="a2481-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="a2481-123">Om te verifiëren, moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="a2481-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="a2481-124">Azure AD-Tenant met ID (de naam van die Azure AD dat u bent aan te melden, vaak hetzelfde zijn als uw bedrijf worden gebruikt, maar niet nodig)</span><span class="sxs-lookup"><span data-stu-id="a2481-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="a2481-125">Toepassings-ID (die zijn uitgevoerd tijdens de stap het maken van Azure AD toepassing)</span><span class="sxs-lookup"><span data-stu-id="a2481-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="a2481-126">Wachtwoord (die u hebt geselecteerd tijdens het maken van de Azure AD-toepassing)</span><span class="sxs-lookup"><span data-stu-id="a2481-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="a2481-127">Zorg dat u 'Azure AD-Tenant-ID', 'Toepassings-ID' en 'Password' vervangen door de juiste waarden in de volgende HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a2481-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="a2481-128">**Algemene HTTP-aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="a2481-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="a2481-129">... wordt (als de verificatie slaagt) leiden tot een reactie vergelijkbaar met het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="a2481-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

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
<span data-ttu-id="a2481-130">(De access_token in het vorige antwoord zijn ingekort voor een verhoging van de leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="a2481-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="a2481-131">**Genereren met behulp van Bash toegangstoken:**</span><span class="sxs-lookup"><span data-stu-id="a2481-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="a2481-132">**Genereren met behulp van PowerShell toegangstoken:**</span><span class="sxs-lookup"><span data-stu-id="a2481-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="a2481-133">Het antwoord bevat een toegangstoken, informatie over hoe lang dat token geldig is en informatie over welke resource kunt u dat token voor.</span><span class="sxs-lookup"><span data-stu-id="a2481-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="a2481-134">Het toegangstoken dat u hebt ontvangen in de vorige aanroep van de HTTP-moet voor alle aanvragen worden doorgegeven aan de Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="a2481-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="a2481-135">Als u doorgeeft als een headerwaarde met de naam "Autorisatie" met de waarde 'Bearer YOUR_ACCESS_TOKEN'.</span><span class="sxs-lookup"><span data-stu-id="a2481-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="a2481-136">U ziet de ruimte tussen 'Bearer' en uw toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="a2481-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="a2481-137">Als u in het bovenstaande HTTP-resultaat zien kunt, is het token is ongeldig voor een bepaalde periode gedurende welke u moet in de cache en dat hetzelfde token opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a2481-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="a2481-138">Zelfs als het is mogelijk om te verifiëren met Azure AD voor elke API-aanroep, zou het zeer inefficiënt zijn.</span><span class="sxs-lookup"><span data-stu-id="a2481-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="a2481-139">Aanroepen van Resource Manager REST-API 's</span><span class="sxs-lookup"><span data-stu-id="a2481-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="a2481-140">In dit onderwerp wordt alleen enkele API's gebruikt om uit te leggen het basisgebruik van de REST-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a2481-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="a2481-141">Zie voor meer informatie over de bewerkingen [Azure Resource Manager REST API's](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a2481-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="a2481-142">Lijst van alle abonnementen</span><span class="sxs-lookup"><span data-stu-id="a2481-142">List all subscriptions</span></span>
<span data-ttu-id="a2481-143">Een van de meest eenvoudige bewerkingen die u kunt doen is voor een lijst met de beschikbare abonnementen waartoe u toegang hebt.</span><span class="sxs-lookup"><span data-stu-id="a2481-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="a2481-144">In de volgende aanvraag ziet u hoe het toegangstoken is doorgegeven als een header:</span><span class="sxs-lookup"><span data-stu-id="a2481-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="a2481-145">(YOUR_ACCESS_TOKEN vervangen door uw werkelijke Access Token).</span><span class="sxs-lookup"><span data-stu-id="a2481-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a2481-146">... en daardoor het ophalen van een lijst met abonnementen dat is toegestaan voor toegang tot deze service-principal</span><span class="sxs-lookup"><span data-stu-id="a2481-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="a2481-147">(Abonnement-id's zijn ingekort voor leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="a2481-147">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="a2481-148">Lijst van alle resourcegroepen in een specifiek abonnement</span><span class="sxs-lookup"><span data-stu-id="a2481-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="a2481-149">Alle resources die beschikbaar zijn met de Resource Manager-API's zijn genest binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a2481-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="a2481-150">U kunt een Resource Manager query voor bestaande resourcegroepen in uw abonnement met de volgende HTTP GET-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a2481-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="a2481-151">U ziet hoe de abonnements-ID is doorgegeven als onderdeel van de URL van deze tijd.</span><span class="sxs-lookup"><span data-stu-id="a2481-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="a2481-152">(YOUR_ACCESS_TOKEN en SUBSCRIPTION_ID vervangen door uw werkelijke access token en de abonnement-ID)</span><span class="sxs-lookup"><span data-stu-id="a2481-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a2481-153">Het antwoord dat u afhankelijk van of u gedefinieerd bronnengroepen hebt en zo ja, hoeveel.</span><span class="sxs-lookup"><span data-stu-id="a2481-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="a2481-154">(Abonnement-id's zijn ingekort voor leesbaarheid)</span><span class="sxs-lookup"><span data-stu-id="a2481-154">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="a2481-155">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a2481-155">Create a resource group</span></span>
<span data-ttu-id="a2481-156">Tot nu toe hebben we alleen is opvragen van de Resource Manager-API's voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a2481-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="a2481-157">Is het tijd we sommige resources maken en u begint met de eenvoudigste ze allemaal zijn, een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a2481-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="a2481-158">De volgende HTTP-aanvraag maakt een resourcegroep in een regio of de locatie van uw keuze en voegt een label aan.</span><span class="sxs-lookup"><span data-stu-id="a2481-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="a2481-159">(YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME vervangen door uw werkelijke Access Token, abonnements-ID en naam van de resourcegroep die u wilt maken)</span><span class="sxs-lookup"><span data-stu-id="a2481-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

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

<span data-ttu-id="a2481-160">Als dit lukt, kunt u een reactie die vergelijkbaar is met het volgende antwoord krijgen:</span><span class="sxs-lookup"><span data-stu-id="a2481-160">If successful, you get a response that is similar to the following response:</span></span>

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

<span data-ttu-id="a2481-161">U hebt een resourcegroep gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2481-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="a2481-162">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a2481-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="a2481-163">Resources aan een resourcegroep met een Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="a2481-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="a2481-164">Met Resource Manager kunt u uw resources met behulp van sjablonen implementeren.</span><span class="sxs-lookup"><span data-stu-id="a2481-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="a2481-165">Een sjabloon worden gedefinieerd voor verschillende resources en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="a2481-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="a2481-166">Voor deze sectie we ervan uitgaan dat u bekend bent met Resource Manager-sjablonen en we alleen beschreven hoe u de API-aanroep implementatie te starten.</span><span class="sxs-lookup"><span data-stu-id="a2481-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="a2481-167">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a2481-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a2481-168">Implementatie van een sjabloon verschillen niet veel hoe u andere API niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a2481-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="a2481-169">Een belangrijk aspect is dat de implementatie van een sjabloon kan erg lang duren.</span><span class="sxs-lookup"><span data-stu-id="a2481-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="a2481-170">De API-aanroep slechts retourneert en het is aan u als ontwikkelaar query voor de status van de implementatie nagaan wanneer de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a2481-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="a2481-171">Zie voor meer informatie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a2481-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="a2481-172">In dit voorbeeld gebruiken we een openbaar blootgestelde sjabloon beschikbaar is op [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a2481-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="a2481-173">De sjabloon we gebruiken implementeert een Linux-VM voor de regio VS-West.</span><span class="sxs-lookup"><span data-stu-id="a2481-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="a2481-174">Hoewel dit voorbeeld gebruikt een beschikbare sjabloon in een openbare zoals GitHub-opslagplaats, kunt u in plaats daarvan de volledige sjabloon doorgeven als onderdeel van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a2481-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="a2481-175">Houd er rekening mee dat we parameterwaarden in de aanvraag die worden gebruikt in de geïmplementeerde sjabloon opgeven.</span><span class="sxs-lookup"><span data-stu-id="a2481-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="a2481-176">(SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD en DNS_NAME_FOR_PUBLIC_IP vervangen op waarden die geschikt is voor uw aanvraag)</span><span class="sxs-lookup"><span data-stu-id="a2481-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

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

<span data-ttu-id="a2481-177">Het lang JSON-antwoord voor deze aanvraag is weggelaten om de leesbaarheid van deze documentatie te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="a2481-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="a2481-178">Het antwoord bevat informatie over de sjablonen implementatie die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a2481-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2481-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2481-179">Next steps</span></span>

- <span data-ttu-id="a2481-180">Zie voor meer informatie over het verwerken van asynchrone REST-bewerkingen, [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a2481-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
