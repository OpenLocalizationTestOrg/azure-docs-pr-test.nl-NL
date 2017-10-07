---
title: aaaManaging Media Services entiteiten met REST | Microsoft Docs
description: Meer informatie over hoe toomanage Media Services-entiteiten met REST-API.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="fe35d-103">Media Services-entiteiten met REST beheren</span><span class="sxs-lookup"><span data-stu-id="fe35d-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe35d-104">REST</span><span class="sxs-lookup"><span data-stu-id="fe35d-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="fe35d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fe35d-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="fe35d-106">Microsoft Azure Media Services is een REST gebaseerde service gebouwd op OData v3.</span><span class="sxs-lookup"><span data-stu-id="fe35d-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="fe35d-107">U kunt toevoegen, query, update en delete-entiteiten in veel Hallo dezelfde manier zoals u op een willekeurige andere OData-service kunt.</span><span class="sxs-lookup"><span data-stu-id="fe35d-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="fe35d-108">Uitzonderingen moeten worden aangeroepen om, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe35d-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="fe35d-109">Zie voor meer informatie over OData [Open Data Protocol documentatie](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="fe35d-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="fe35d-110">Dit onderwerp leest u hoe toomanage Azure Media Services entiteiten met REST.</span><span class="sxs-lookup"><span data-stu-id="fe35d-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="fe35d-111">Vanaf 1 April 2017 worden elke record taak in uw account ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende records van de taak zelfs als Hallo kunt u het totale aantal records lager dan de maximumquotum Hallo is.</span><span class="sxs-lookup"><span data-stu-id="fe35d-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="fe35d-112">Bijvoorbeeld: op 1 April 2017 elke record taak in uw account die ouder zijn dan 31 December 2016, worden automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fe35d-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="fe35d-113">Als u tooarchive Hallo projecttaak/informatie nodig hebt, kunt u Hallo-code in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="fe35d-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="fe35d-114">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="fe35d-114">Considerations</span></span>  

<span data-ttu-id="fe35d-115">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="fe35d-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fe35d-116">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="fe35d-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="fe35d-117">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="fe35d-117">Connect tooMedia Services</span></span>

<span data-ttu-id="fe35d-118">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="fe35d-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="fe35d-119">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fe35d-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fe35d-120">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="fe35d-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="fe35d-121">Toevoegen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="fe35d-121">Adding entities</span></span>
<span data-ttu-id="fe35d-122">Elke entiteit in Media Services wordt tooan entiteitset, zoals activa, via een HTTP POST-aanvraag toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fe35d-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="fe35d-123">Hallo volgende voorbeeld ziet u hoe een AccessPolicy toocreate.</span><span class="sxs-lookup"><span data-stu-id="fe35d-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="fe35d-124">Opvragen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="fe35d-124">Querying entities</span></span>
<span data-ttu-id="fe35d-125">Uitvoeren van query's en entiteiten aanbieding is eenvoudig en alleen omvat een ophalen van HTTP-aanvraag en optionele OData-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="fe35d-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="fe35d-126">Hallo haalt volgende voorbeeld een lijst van alle MediaProcessor entiteiten.</span><span class="sxs-lookup"><span data-stu-id="fe35d-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="fe35d-127">U kunt ook een specifieke entiteit of alle entiteitsets die is gekoppeld aan een specifieke entiteit, zoals in Hallo volgen voorbeelden ophalen:</span><span class="sxs-lookup"><span data-stu-id="fe35d-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="fe35d-128">Hallo wordt volgende voorbeeld alleen Hallo de eigenschap State van alle taken.</span><span class="sxs-lookup"><span data-stu-id="fe35d-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="fe35d-129">Hallo retourneert volgende voorbeeld alle JobTemplates met de naam van de Hallo 'SampleTemplate'.</span><span class="sxs-lookup"><span data-stu-id="fe35d-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="fe35d-130">Hallo $expand-bewerking wordt niet ondersteund in Media Services goed Hallo wordt niet ondersteund in LINQ overwegingen (WCF Data Services) beschreven LINQ-methoden.</span><span class="sxs-lookup"><span data-stu-id="fe35d-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="fe35d-131">Door grote verzamelingen van entiteiten opsommen</span><span class="sxs-lookup"><span data-stu-id="fe35d-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="fe35d-132">Tijdens het opvragen van entiteiten, moet u er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten resultaten too1000 beperkt is.</span><span class="sxs-lookup"><span data-stu-id="fe35d-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="fe35d-133">Gebruik **overslaan** en **boven** tooenumerate via Hallo grote verzameling entiteiten.</span><span class="sxs-lookup"><span data-stu-id="fe35d-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="fe35d-134">Hallo volgende voorbeeld wordt getoond hoe toouse **overslaan** en **boven** tooskip Hallo eerst 2000 taken en get Hallo naast 1000 taken.</span><span class="sxs-lookup"><span data-stu-id="fe35d-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="fe35d-135">Entiteiten bijwerken</span><span class="sxs-lookup"><span data-stu-id="fe35d-135">Updating entities</span></span>
<span data-ttu-id="fe35d-136">Afhankelijk van het entiteitstype Hallo en Hallo status van deze, kunt u eigenschappen op die entiteit via een PATCH bijwerken plaatsen of samenvoegen HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="fe35d-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="fe35d-137">Zie voor meer informatie over deze bewerkingen [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe35d-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="fe35d-138">Hallo volgende codevoorbeeld toont hoe tooupdate Hallo naameigenschap voor een Asset-entiteit.</span><span class="sxs-lookup"><span data-stu-id="fe35d-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="fe35d-139">Entiteiten verwijderen</span><span class="sxs-lookup"><span data-stu-id="fe35d-139">Deleting entities</span></span>
<span data-ttu-id="fe35d-140">Entiteiten kunnen worden verwijderd in een Media Services met behulp van een verwijderd HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="fe35d-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="fe35d-141">Afhankelijk van het Hallo-entiteit zijn Hallo volgorde waarin u entiteiten verwijderen belangrijk.</span><span class="sxs-lookup"><span data-stu-id="fe35d-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="fe35d-142">Bijvoorbeeld: entiteiten zoals activa vereisen dat u intrekken (of verwijderen) alle Locators die verwijzen naar dat bepaalde actief voordat u deze verwijdert Hallo Asset.</span><span class="sxs-lookup"><span data-stu-id="fe35d-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="fe35d-143">Hallo volgende voorbeeld wordt getoond hoe toodelete een Locator die gebruikte tooupload een bestand naar de blobopslag was.</span><span class="sxs-lookup"><span data-stu-id="fe35d-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="fe35d-144">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="fe35d-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fe35d-145">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="fe35d-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

