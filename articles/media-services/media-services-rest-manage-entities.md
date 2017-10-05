---
title: Het beheren van Media Services-entiteiten met REST | Microsoft Docs
description: Informatie over het beheren van Media Services-entiteiten met REST-API.
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
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="b3dcd-103">Media Services-entiteiten met REST beheren</span><span class="sxs-lookup"><span data-stu-id="b3dcd-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3dcd-104">REST</span><span class="sxs-lookup"><span data-stu-id="b3dcd-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="b3dcd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b3dcd-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="b3dcd-106">Microsoft Azure Media Services is een REST gebaseerde service gebouwd op OData v3.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="b3dcd-107">U kunt toevoegen, query, bijwerken en delete entiteiten op ongeveer dezelfde manier kunt u op een willekeurige andere OData-service.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="b3dcd-108">Uitzonderingen moeten worden aangeroepen om, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="b3dcd-109">Zie voor meer informatie over OData [Open Data Protocol documentatie](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="b3dcd-110">Dit onderwerp leest u hoe u voor het beheren van Azure Media Services-entiteiten met REST.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="b3dcd-111">Vanaf 1 april 2017 wordt elke taakrecord in uw account die ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende onderliggende taakrecords, zelfs als het totale aantal records lager is dan het maximale quotum.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="b3dcd-112">Bijvoorbeeld: op 1 April 2017 elke record taak in uw account die ouder zijn dan 31 December 2016, worden automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="b3dcd-113">Als u nodig hebt bij de archivering van gegevens van de taak/taak, kunt u de code in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="b3dcd-114">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="b3dcd-114">Considerations</span></span>  

<span data-ttu-id="b3dcd-115">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b3dcd-116">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="b3dcd-117">Verbinding met Media Services maken</span><span class="sxs-lookup"><span data-stu-id="b3dcd-117">Connect to Media Services</span></span>

<span data-ttu-id="b3dcd-118">Zie voor meer informatie over de verbinding maken met de AMS API [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b3dcd-119">Na het correct verbinding maakt met https://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b3dcd-120">U moet de volgende aanroepen naar de nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="b3dcd-121">Toevoegen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="b3dcd-121">Adding entities</span></span>
<span data-ttu-id="b3dcd-122">Elke entiteit in Media Services wordt toegevoegd aan een entiteit ingesteld, zoals activa, via een HTTP POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="b3dcd-123">Het volgende voorbeeld laat zien hoe een AccessPolicy maken.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-123">The following example shows how to create an AccessPolicy.</span></span>

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

## <a name="querying-entities"></a><span data-ttu-id="b3dcd-124">Opvragen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="b3dcd-124">Querying entities</span></span>
<span data-ttu-id="b3dcd-125">Uitvoeren van query's en entiteiten aanbieding is eenvoudig en alleen omvat een ophalen van HTTP-aanvraag en optionele OData-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="b3dcd-126">Het volgende voorbeeld wordt een lijst met alle MediaProcessor entiteiten opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b3dcd-127">U kunt ook een specifieke entiteit of alle entiteitsets die is gekoppeld aan een specifieke entiteit, zoals in de volgende voorbeelden ophalen:</span><span class="sxs-lookup"><span data-stu-id="b3dcd-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

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

<span data-ttu-id="b3dcd-128">Het volgende voorbeeld retourneert alleen de eigenschap State van alle taken.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b3dcd-129">Het volgende voorbeeld worden alle JobTemplates met de naam 'SampleTemplate'.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="b3dcd-130">De $expand-bewerking wordt niet ondersteund in Media Services, evenals de niet-ondersteunde LINQ methoden van LINQ overwegingen (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="b3dcd-131">Door grote verzamelingen van entiteiten opsommen</span><span class="sxs-lookup"><span data-stu-id="b3dcd-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="b3dcd-132">Tijdens het opvragen van entiteiten, is er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten tot 1000 resultaten beperkt.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="b3dcd-133">Gebruik **overslaan** en **boven** opsommen via de grote verzameling entiteiten.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="b3dcd-134">Het volgende voorbeeld ziet u hoe u **overslaan** en **boven** overslaan van de eerste 2000 taken en ophalen van de volgende 1000 taken.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="b3dcd-135">Entiteiten bijwerken</span><span class="sxs-lookup"><span data-stu-id="b3dcd-135">Updating entities</span></span>
<span data-ttu-id="b3dcd-136">Afhankelijk van het entiteitstype en de status van deze, kunt u eigenschappen op die entiteit via een PATCH bijwerken plaatsen of samenvoegen HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="b3dcd-137">Zie voor meer informatie over deze bewerkingen [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="b3dcd-138">Het volgende voorbeeld laat zien hoe de eigenschap Name in een entiteit Asset bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

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

## <a name="deleting-entities"></a><span data-ttu-id="b3dcd-139">Entiteiten verwijderen</span><span class="sxs-lookup"><span data-stu-id="b3dcd-139">Deleting entities</span></span>
<span data-ttu-id="b3dcd-140">Entiteiten kunnen worden verwijderd in een Media Services met behulp van een verwijderd HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="b3dcd-141">Afhankelijk van de entiteit zijn de volgorde waarin u entiteiten verwijderen belangrijk.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="b3dcd-142">Bijvoorbeeld: entiteiten zoals activa vereisen dat u intrekken (of verwijderen) alle Locators die verwijzen naar dat bepaalde actief voordat u verwijdert de Asset.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="b3dcd-143">Het volgende voorbeeld laat zien hoe een Locator die is gebruikt voor het uploaden van een bestand naar de blobopslag verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="b3dcd-144">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="b3dcd-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b3dcd-145">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="b3dcd-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

