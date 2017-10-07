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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="417b5-103">Log Analytics logboek search REST-API</span><span class="sxs-lookup"><span data-stu-id="417b5-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="417b5-104">Deze handleiding biedt een eenvoudige zelfstudie, inclusief voorbeelden van hoe u Hallo Log Analytics Search REST-API kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="417b5-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="417b5-105">Log Analytics maakt deel uit van Hallo Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="417b5-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="417b5-106">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens u toouse Hallo verouderde querytaal met Hallo logboek search API blijven moet, zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="417b5-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="417b5-107">Een nieuwe API worden uitgebracht voor bijgewerkte werkruimten en Hallo-documentatie op dat moment wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="417b5-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="417b5-108">Log Analytics is eerder operationeel inzicht, dat is waarom het Hallo-naam die wordt gebruikt in het Hallo-resourceprovider is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="417b5-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="417b5-109">Overzicht van Hallo logboek Search REST-API</span><span class="sxs-lookup"><span data-stu-id="417b5-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="417b5-110">Hallo Log Analytics Search REST-API RESTful is en toegankelijk zijn via hello Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="417b5-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="417b5-111">Dit artikel vindt u voorbeelden van de toegang tot API Hallo via [ARMClient](https://github.com/projectkudu/ARMClient), een open-source-opdrachtregelprogramma dat wordt aangeroepen vereenvoudigt hello Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="417b5-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="417b5-112">Hallo-gebruik van ARMClient is een van de vele opties tooaccess Hallo Log Analytics zoeken-API.</span><span class="sxs-lookup"><span data-stu-id="417b5-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="417b5-113">Een andere optie is toouse hello Azure PowerShell-module voor OperationalInsights, waaronder de cmdlets voor toegang tot zoeken.</span><span class="sxs-lookup"><span data-stu-id="417b5-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="417b5-114">Met deze hulpprogramma's, kunt u gebruikmaken van hello Azure Resource Manager-API toomake aanroepen tooOMS werkruimten en zoekvariabelen binnen deze.</span><span class="sxs-lookup"><span data-stu-id="417b5-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="417b5-115">Hallo API levert zoekresultaten in JSON-indeling, zodat u toouse Hallo zoekresultaten in veel verschillende manieren programmatisch.</span><span class="sxs-lookup"><span data-stu-id="417b5-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="417b5-116">Hello Azure Resource Manager kan worden gebruikt een [-bibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) en Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="417b5-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="417b5-117">toolearn Bekijk meer Hallo gekoppelde webpagina's.</span><span class="sxs-lookup"><span data-stu-id="417b5-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="417b5-118">Als u een aggregatie-opdracht zoals gebruiken `|measure count()` of `distinct`, elke aanroep toosearch kan resulteren in een Resourcegroepnaam 500.000 records.</span><span class="sxs-lookup"><span data-stu-id="417b5-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="417b5-119">Zoekopdrachten dat een aggregatie-opdracht niet opneemt retourneren maximaal 5.000 records.</span><span class="sxs-lookup"><span data-stu-id="417b5-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="417b5-120">Basic Log Analytics Search REST-API-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="417b5-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="417b5-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="417b5-121">toouse ARMClient</span></span>
1. <span data-ttu-id="417b5-122">Installeer [Chocolatey](https://chocolatey.org/), dit is een Open Source Package Manager voor Windows.</span><span class="sxs-lookup"><span data-stu-id="417b5-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="417b5-123">Open een opdrachtpromptvenster als administrator en voer vervolgens de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="417b5-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="417b5-124">Installeer ARMClient Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="417b5-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="417b5-125">tooperform een zoekopdracht met ARMClient</span><span class="sxs-lookup"><span data-stu-id="417b5-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="417b5-126">Meld u aan met uw Microsoft-account of de account van uw werk of school:</span><span class="sxs-lookup"><span data-stu-id="417b5-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="417b5-127">Een geslaagde aanmelding geeft een lijst van alle abonnementen gekoppeld toohello opgegeven account:</span><span class="sxs-lookup"><span data-stu-id="417b5-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="417b5-128">Hallo Operations Management Suite werkruimten ophalen:</span><span class="sxs-lookup"><span data-stu-id="417b5-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="417b5-129">Een geslaagde Get-aanvraag zou uitvoer dat alle werkruimten toohello abonnement gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="417b5-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="417b5-130">Uw zoekopdracht-variabele maken:</span><span class="sxs-lookup"><span data-stu-id="417b5-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="417b5-131">Zoeken met behulp van de variabele van uw nieuwe zoekopdracht:</span><span class="sxs-lookup"><span data-stu-id="417b5-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="417b5-132">Meld u voorbeelden van Analytics Search REST-API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="417b5-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="417b5-133">Hallo volgen voorbeelden laten zien hoe u Hallo Search API kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="417b5-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="417b5-134">Zoeken - actie leestijd</span><span class="sxs-lookup"><span data-stu-id="417b5-134">Search - Action/Read</span></span>
<span data-ttu-id="417b5-135">**Voorbeeld-Url:**</span><span class="sxs-lookup"><span data-stu-id="417b5-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="417b5-136">**Aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="417b5-136">**Request:**</span></span>

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
<span data-ttu-id="417b5-137">Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="417b5-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="417b5-138">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="417b5-138">**Property**</span></span> | <span data-ttu-id="417b5-139">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="417b5-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="417b5-140">Boven</span><span class="sxs-lookup"><span data-stu-id="417b5-140">top</span></span> |<span data-ttu-id="417b5-141">Hallo maximum aantal resultaten tooreturn.</span><span class="sxs-lookup"><span data-stu-id="417b5-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="417b5-142">Markeer</span><span class="sxs-lookup"><span data-stu-id="417b5-142">highlight</span></span> |<span data-ttu-id="417b5-143">Bevat vóór en na-parameters, meestal gebruikt voor de overeenkomende velden markeren</span><span class="sxs-lookup"><span data-stu-id="417b5-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="417b5-144">vooraf</span><span class="sxs-lookup"><span data-stu-id="417b5-144">pre</span></span> |<span data-ttu-id="417b5-145">Prefixes Hallo tekenreeksvelden tooyour komt overeen met gegeven.</span><span class="sxs-lookup"><span data-stu-id="417b5-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="417b5-146">Verzenden</span><span class="sxs-lookup"><span data-stu-id="417b5-146">post</span></span> |<span data-ttu-id="417b5-147">Voegt Hallo tekenreeksvelden tooyour komt overeen met gegeven.</span><span class="sxs-lookup"><span data-stu-id="417b5-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="417b5-148">query</span><span class="sxs-lookup"><span data-stu-id="417b5-148">query</span></span> |<span data-ttu-id="417b5-149">Hallo zoekquery toocollect gebruikt en retourneren van resultaten.</span><span class="sxs-lookup"><span data-stu-id="417b5-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="417b5-150">start</span><span class="sxs-lookup"><span data-stu-id="417b5-150">start</span></span> |<span data-ttu-id="417b5-151">Hallo begin van tijdvenster Hallo resultaten toobe gevonden gewenste.</span><span class="sxs-lookup"><span data-stu-id="417b5-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="417b5-152">Einde</span><span class="sxs-lookup"><span data-stu-id="417b5-152">end</span></span> |<span data-ttu-id="417b5-153">Hallo einde van tijdvenster Hallo resultaten toobe gevonden gewenste.</span><span class="sxs-lookup"><span data-stu-id="417b5-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="417b5-154">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="417b5-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="417b5-155">Zoek / {-ID} - actie leestijd</span><span class="sxs-lookup"><span data-stu-id="417b5-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="417b5-156">**Aanvraag Hallo inhoud van een opgeslagen zoekopdracht:**</span><span class="sxs-lookup"><span data-stu-id="417b5-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="417b5-157">Zoekresultaten met status 'In behandeling' hello, kunnen polling Hallo bijgewerkt resultaten worden uitgevoerd via deze API.</span><span class="sxs-lookup"><span data-stu-id="417b5-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="417b5-158">Na 6 min Hallo resultaat van de Hallo zoekactie wordt verwijderd uit de cache Hallo en HTTP-geworden wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="417b5-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="417b5-159">Als de aanvankelijke zoekaanvraag Hallo onmiddellijk een 'Geslaagd' status retourneert, Hallo resultaten toohello cache waardoor deze API tooreturn HTTP geworden als opgevraagd niet toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="417b5-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="417b5-160">Hallo-inhoud van een HTTP 200-resultaat zijn in Hallo dezelfde notatie als de aanvankelijke zoekaanvraag Hallo alleen met de bijgewerkte waarden.</span><span class="sxs-lookup"><span data-stu-id="417b5-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="417b5-161">Opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="417b5-161">Saved searches</span></span>
<span data-ttu-id="417b5-162">**Lijst met opgeslagen zoekopdrachten aanvragen:**</span><span class="sxs-lookup"><span data-stu-id="417b5-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="417b5-163">Ondersteunde methoden: GET, PUT verwijderen</span><span class="sxs-lookup"><span data-stu-id="417b5-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="417b5-164">Ondersteunde methoden: ophalen</span><span class="sxs-lookup"><span data-stu-id="417b5-164">Supported collection methods: GET</span></span>

<span data-ttu-id="417b5-165">Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="417b5-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="417b5-166">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="417b5-166">Property</span></span> | <span data-ttu-id="417b5-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="417b5-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="417b5-168">Id</span><span class="sxs-lookup"><span data-stu-id="417b5-168">Id</span></span> |<span data-ttu-id="417b5-169">Hallo unieke id.</span><span class="sxs-lookup"><span data-stu-id="417b5-169">hello unique identifier.</span></span> |
| <span data-ttu-id="417b5-170">ETag</span><span class="sxs-lookup"><span data-stu-id="417b5-170">Etag</span></span> |<span data-ttu-id="417b5-171">**Vereist voor Patch**.</span><span class="sxs-lookup"><span data-stu-id="417b5-171">**Required for Patch**.</span></span> <span data-ttu-id="417b5-172">Bijgewerkt met de server bij elke schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="417b5-172">Updated by server on each write.</span></span> <span data-ttu-id="417b5-173">De waarde moet gelijk toohello huidige opgeslagen waarde of ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="417b5-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="417b5-174">409 geretourneerd voor waarden van de oude/ongeldig.</span><span class="sxs-lookup"><span data-stu-id="417b5-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="417b5-175">Properties.query</span><span class="sxs-lookup"><span data-stu-id="417b5-175">properties.query</span></span> |<span data-ttu-id="417b5-176">**Vereist**.</span><span class="sxs-lookup"><span data-stu-id="417b5-176">**Required**.</span></span> <span data-ttu-id="417b5-177">Hallo-zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="417b5-177">hello search query.</span></span> |
| <span data-ttu-id="417b5-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="417b5-178">properties.displayName</span></span> |<span data-ttu-id="417b5-179">**Vereist**.</span><span class="sxs-lookup"><span data-stu-id="417b5-179">**Required**.</span></span> <span data-ttu-id="417b5-180">Hallo gebruiker gedefinieerde weergavenaam van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="417b5-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="417b5-181">Properties.Category</span><span class="sxs-lookup"><span data-stu-id="417b5-181">properties.category</span></span> |<span data-ttu-id="417b5-182">**Vereist**.</span><span class="sxs-lookup"><span data-stu-id="417b5-182">**Required**.</span></span> <span data-ttu-id="417b5-183">Hallo gebruiker gedefinieerde categorie van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="417b5-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="417b5-184">Hallo Log Analytics-API van zoekservice retourneert momenteel gebruiker gemaakte opgeslagen zoekopdrachten wanneer gepeild voor opgeslagen zoekopdrachten in een werkruimte.</span><span class="sxs-lookup"><span data-stu-id="417b5-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="417b5-185">Hallo API retourneert geen opgeslagen zoekopdrachten geleverd door oplossingen.</span><span class="sxs-lookup"><span data-stu-id="417b5-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="417b5-186">Opgeslagen zoekopdrachten maken</span><span class="sxs-lookup"><span data-stu-id="417b5-186">Create saved searches</span></span>
<span data-ttu-id="417b5-187">**Aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="417b5-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="417b5-188">Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="417b5-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="417b5-189">Verwijder opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="417b5-189">Delete saved searches</span></span>
<span data-ttu-id="417b5-190">**Aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="417b5-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="417b5-191">Opgeslagen zoekopdrachten bijwerken</span><span class="sxs-lookup"><span data-stu-id="417b5-191">Update saved searches</span></span>
 <span data-ttu-id="417b5-192">**Aanvraag:**</span><span class="sxs-lookup"><span data-stu-id="417b5-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="417b5-193">Metagegevens - JSON alleen</span><span class="sxs-lookup"><span data-stu-id="417b5-193">Metadata - JSON only</span></span>
<span data-ttu-id="417b5-194">Hier volgt een manier toosee Hallo velden voor alle logboekbestanden typen voor Hallo verzamelde gegevens in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="417b5-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="417b5-195">Bijvoorbeeld, als u wilt dat u weet of Hallo gebeurtenistype een veld met de naam Computer, klikt u vervolgens deze query is eenrichtingssessie toocheck.</span><span class="sxs-lookup"><span data-stu-id="417b5-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="417b5-196">**Aanvraag voor velden:**</span><span class="sxs-lookup"><span data-stu-id="417b5-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="417b5-197">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="417b5-197">**Response:**</span></span>

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

<span data-ttu-id="417b5-198">Hallo volgende tabel beschrijft Hallo-eigenschappen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="417b5-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="417b5-199">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="417b5-199">**Property**</span></span> | <span data-ttu-id="417b5-200">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="417b5-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="417b5-201">naam</span><span class="sxs-lookup"><span data-stu-id="417b5-201">name</span></span> |<span data-ttu-id="417b5-202">Veldnaam.</span><span class="sxs-lookup"><span data-stu-id="417b5-202">Field name.</span></span> |
| <span data-ttu-id="417b5-203">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="417b5-203">displayName</span></span> |<span data-ttu-id="417b5-204">Hallo weergavenaam van het Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="417b5-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="417b5-205">type</span><span class="sxs-lookup"><span data-stu-id="417b5-205">type</span></span> |<span data-ttu-id="417b5-206">Hallo Type Hallo veldwaarde.</span><span class="sxs-lookup"><span data-stu-id="417b5-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="417b5-207">geschikt voor facetten</span><span class="sxs-lookup"><span data-stu-id="417b5-207">facetable</span></span> |<span data-ttu-id="417b5-208">De combinatie van huidige 'indexed', ' opgeslagen ' en 'facet' Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="417b5-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="417b5-209">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="417b5-209">display</span></span> |<span data-ttu-id="417b5-210">Huidige 'weergeven'-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="417b5-210">Current ‘display’ property.</span></span> <span data-ttu-id="417b5-211">True als het veld wordt weergegeven in de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="417b5-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="417b5-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="417b5-212">ownerType</span></span> |<span data-ttu-id="417b5-213">Verminderde tooonly typen die behoren tooonboarded IP's.</span><span class="sxs-lookup"><span data-stu-id="417b5-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="417b5-214">Optionele parameters</span><span class="sxs-lookup"><span data-stu-id="417b5-214">Optional parameters</span></span>
<span data-ttu-id="417b5-215">Hallo volgende informatie beschrijft de optionele parameters beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="417b5-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="417b5-216">Markeren</span><span class="sxs-lookup"><span data-stu-id="417b5-216">Highlighting</span></span>
<span data-ttu-id="417b5-217">Hallo "Highlight" parameter is een optionele parameter, mag u toorequest Hallo zoeken subsysteem omvatten een reeks markeringen in zijn reactie.</span><span class="sxs-lookup"><span data-stu-id="417b5-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="417b5-218">Deze markeringen geven Hallo starten en eindigen gemarkeerde tekst die overeenkomt met de Hallo voorwaarden vindt u in uw query.</span><span class="sxs-lookup"><span data-stu-id="417b5-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="417b5-219">U kunt opgeven Hallo moet worden gestart en eindigen markeringen die worden gebruikt door een zoekterm toowrap Hallo gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="417b5-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="417b5-220">**Voorbeeld van de zoekopdracht**</span><span class="sxs-lookup"><span data-stu-id="417b5-220">**Example search query**</span></span>

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

<span data-ttu-id="417b5-221">**Resultaat van de steekproef:**</span><span class="sxs-lookup"><span data-stu-id="417b5-221">**Sample result:**</span></span>

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

<span data-ttu-id="417b5-222">U ziet dat Hallo voorgaande resultaat bevat een foutbericht weergegeven dat is voorafgegaan en toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="417b5-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="417b5-223">Computergroepen</span><span class="sxs-lookup"><span data-stu-id="417b5-223">Computer groups</span></span>
<span data-ttu-id="417b5-224">Computergroepen zijn speciale opgeslagen zoekopdrachten die resulteren in een set computers.</span><span class="sxs-lookup"><span data-stu-id="417b5-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="417b5-225">U kunt een computergroep in andere query's toolimit Hallo resultaten toohello computers in de groep hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="417b5-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="417b5-226">Een computergroep is geïmplementeerd als een zoekopdracht met een code van de groep met een waarde van de Computer.</span><span class="sxs-lookup"><span data-stu-id="417b5-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="417b5-227">Hier volgt een voorbeeldantwoord voor een computergroep.</span><span class="sxs-lookup"><span data-stu-id="417b5-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="417b5-228">Bij het ophalen van computergroepen</span><span class="sxs-lookup"><span data-stu-id="417b5-228">Retrieving computer groups</span></span>
<span data-ttu-id="417b5-229">tooretrieve een computergroep Hallo gebruik Get-methode met Hallo groep-id.</span><span class="sxs-lookup"><span data-stu-id="417b5-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="417b5-230">Maken of bijwerken van een computergroep</span><span class="sxs-lookup"><span data-stu-id="417b5-230">Creating or updating a computer group</span></span>
<span data-ttu-id="417b5-231">een computergroep toocreate Hallo Put-methode gebruiken met een opgeslagen zoekopdracht unieke ID.</span><span class="sxs-lookup"><span data-stu-id="417b5-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="417b5-232">Als u een bestaande computer-ID gebruikt, is dat een gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="417b5-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="417b5-233">Wanneer u een computergroep in Hallo Log Analytics-portal maakt, wordt de Hallo-ID van het Hallo-groep en de naam gemaakt.</span><span class="sxs-lookup"><span data-stu-id="417b5-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="417b5-234">Hallo-query die wordt gebruikt voor de definitie van de groep Hallo moet een verzameling van computers voor Hallo groep toofunction goed retourneren.</span><span class="sxs-lookup"><span data-stu-id="417b5-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="417b5-235">Het raadzaam dat u uw query met beëindigen `| Distinct Computer` tooensure Hallo juiste gegevens geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="417b5-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="417b5-236">Hallo-definitie Hallo opgeslagen zoekopdracht moet een label met de naam groep met een waarde van de Computer voor Hallo zoeken toobe geclassificeerd als een computergroep bevatten.</span><span class="sxs-lookup"><span data-stu-id="417b5-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="417b5-237">Computergroepen verwijderen</span><span class="sxs-lookup"><span data-stu-id="417b5-237">Deleting computer groups</span></span>
<span data-ttu-id="417b5-238">toodelete een computergroep, gebruik Hallo Delete-methode met Hallo groep-id.</span><span class="sxs-lookup"><span data-stu-id="417b5-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="417b5-239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="417b5-239">Next steps</span></span>
* <span data-ttu-id="417b5-240">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toobuild query's op basis van aangepaste velden voor de criteria.</span><span class="sxs-lookup"><span data-stu-id="417b5-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
