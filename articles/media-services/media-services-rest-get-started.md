---
title: aaaGet gestart met het leveren van inhoud on demand met REST | Microsoft Docs
description: In deze zelfstudie wordt u begeleid Hallo stappen voor het implementeren van een on demand leveren van inhoud toepassing met Azure Media Services met REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="8867a-103">Aan de slag met het leveren van inhoud on demand met REST</span><span class="sxs-lookup"><span data-stu-id="8867a-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="8867a-104">Deze snelstartgids wordt u begeleid Hallo stappen van de implementatie van een eenvoudige (VoD) leveren van inhoud toepassing met Azure Media Services (AMS) REST-API's.</span><span class="sxs-lookup"><span data-stu-id="8867a-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="8867a-105">Hallo-zelfstudie introduceert Hallo basiswerkstroom Media Services en de meest algemene programmeerobjecten Hallo en taken die zijn vereist voor het ontwikkelen van Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="8867a-106">Bij voltooiing Hallo Hallo zelfstudie, wordt u kunnen toostream of progressief downloaden van media met een voorbeeldbestand die geüpload, gecodeerd en gedownload.</span><span class="sxs-lookup"><span data-stu-id="8867a-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="8867a-107">Hello volgende afbeelding ziet u enkele van de meest gebruikte Hallo objecten wanneer VoD toepassingen ontwikkelt voor Hallo Media Services OData-model.</span><span class="sxs-lookup"><span data-stu-id="8867a-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="8867a-108">Klik op Hallo installatiekopie tooview het maximale grootte.</span><span class="sxs-lookup"><span data-stu-id="8867a-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="8867a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8867a-109">Prerequisites</span></span>
<span data-ttu-id="8867a-110">Hallo zijn volgende vereiste onderdelen vereist toostart ontwikkelen met Media Services met REST-API's.</span><span class="sxs-lookup"><span data-stu-id="8867a-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="8867a-111">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8867a-111">An Azure account.</span></span> <span data-ttu-id="8867a-112">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8867a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8867a-113">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="8867a-113">A Media Services account.</span></span> <span data-ttu-id="8867a-114">een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="8867a-115">Begrijpt hoe toodevelop met Media Services REST-API.</span><span class="sxs-lookup"><span data-stu-id="8867a-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="8867a-116">Zie voor meer informatie [REST API voor Media Services-overzicht](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="8867a-117">Een toepassing van uw keuze waarmee HTTP-aanvragen en antwoorden kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="8867a-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="8867a-118">Deze zelfstudie wordt gebruikgemaakt van [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="8867a-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="8867a-119">Hallo volgende taken worden weergegeven in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="8867a-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="8867a-120">Start de streaming-eindpunt (met behulp van hello Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="8867a-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="8867a-121">Verbinding toohello Media Services-account maken met de REST-API.</span><span class="sxs-lookup"><span data-stu-id="8867a-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="8867a-122">Een nieuwe asset maken en een videobestand uploaden met de REST-API.</span><span class="sxs-lookup"><span data-stu-id="8867a-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="8867a-123">Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden met de REST-API.</span><span class="sxs-lookup"><span data-stu-id="8867a-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="8867a-124">Hallo asset publiceren en get streamen en progressief downloaden van URL's met de REST-API.</span><span class="sxs-lookup"><span data-stu-id="8867a-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="8867a-125">Uw inhoud afspelen.</span><span class="sxs-lookup"><span data-stu-id="8867a-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="8867a-126">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="8867a-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8867a-127">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="8867a-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8867a-128">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8867a-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8867a-129">Zie voor meer informatie over de REST van de AMS-entiteiten in dit onderwerp gebruikt, [Azure Media Services REST API-verwijzing](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="8867a-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="8867a-130">Zie ook [Azure Media Services-concepten](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="8867a-131">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8867a-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8867a-132">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="8867a-133">Start de streaming-eindpunten met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8867a-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="8867a-134">Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo leveren van video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="8867a-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="8867a-135">Media Services biedt dynamische pakketten zodat u toodeliver uw adaptive bitrate MP4-inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, zonder dat u vooraf verpakte toostore hoeft versies van elk van deze streaming-indelingen.</span><span class="sxs-lookup"><span data-stu-id="8867a-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="8867a-136">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="8867a-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="8867a-137">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="8867a-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="8867a-138">toostart Hallo streaming-eindpunt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8867a-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="8867a-139">Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8867a-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8867a-140">Klik in het venster Instellingen Hallo, Streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8867a-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="8867a-141">Klik op Hallo standaardstreaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8867a-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="8867a-142">Hallo DEFAULT STREAMING ENDPOINT DETAILS venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8867a-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="8867a-143">Klik op Hallo Start pictogram.</span><span class="sxs-lookup"><span data-stu-id="8867a-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="8867a-144">Klik op Hallo opslaan knop toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="8867a-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="8867a-145"><a id="connect"></a>Toohello Media Services-account verbinding met de REST-API</span><span class="sxs-lookup"><span data-stu-id="8867a-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="8867a-146">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8867a-147">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8867a-148">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="8867a-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="8867a-149">Bijvoorbeeld, als nadat u hebt geprobeerd tooconnect, u hebt verkregen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8867a-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="8867a-150">U moet de volgende API-aanroepen toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ boeken.</span><span class="sxs-lookup"><span data-stu-id="8867a-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="8867a-151"><a id="upload"></a>Een nieuwe asset maken en een videobestand uploaden met de REST-API</span><span class="sxs-lookup"><span data-stu-id="8867a-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="8867a-152">In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="8867a-153">Hallo **Asset** entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload naar Hallo asset, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="8867a-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="8867a-154">Een van de Hallo waarden dat u tooprovide hebt bij het maken van een asset is opties voor het maken van asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="8867a-155">Hallo **opties** eigenschap is een inventarisatiewaarde die Hallo versleuteling worden opties die een Asset kan worden gemaakt beschreven met.</span><span class="sxs-lookup"><span data-stu-id="8867a-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="8867a-156">Een geldige waarde is een van de Hallo waarden uit de lijst Hallo hieronder niet een combinatie van waarden in deze lijst:</span><span class="sxs-lookup"><span data-stu-id="8867a-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="8867a-157">**Geen** = **0** -er wordt geen versleuteling wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8867a-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="8867a-158">Wanneer u deze optie wordt de inhoud is niet beveiligd de overdracht of in rust in de opslag.</span><span class="sxs-lookup"><span data-stu-id="8867a-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="8867a-159">Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8867a-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="8867a-160">**StorageEncrypted** = **1** - versleutelde inhoud lokaal met AES-256-bitsversleuteling versleuteld en geüpload en tooAzure opslag wordt bewaard in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="8867a-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="8867a-161">Automatisch worden beveiligd met Storage Encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="8867a-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="8867a-162">Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is wanneer u dat deze toosecure invoer van hoge kwaliteit mediabestanden met een sterke codering in rust op schijf.</span><span class="sxs-lookup"><span data-stu-id="8867a-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="8867a-163">**CommonEncryptionProtected** = **2** -Gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="8867a-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="8867a-164">**EnvelopeEncryptionProtected** = **4** – Gebruik deze optie als u HLS versleuteld met AES uploaden wilt.</span><span class="sxs-lookup"><span data-stu-id="8867a-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="8867a-165">Hallo-bestanden zijn moeten gecodeerd en versleuteld door Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="8867a-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="8867a-166">Maak een asset</span><span class="sxs-lookup"><span data-stu-id="8867a-166">Create an asset</span></span>
<span data-ttu-id="8867a-167">Een actief is een container voor meerdere typen of sets van objecten in Media Services, waaronder video, audio, afbeeldingen, verzamelingen miniaturen, tekst-nummers en ondertitelingsbestanden bestanden.</span><span class="sxs-lookup"><span data-stu-id="8867a-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="8867a-168">In de REST-API maken van een Asset, moet u verzenden POST Hallo tooMedia Services aanvragen en eigenschapsinformatie over uw asset in de aanvraagtekst hello te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8867a-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="8867a-169">Hallo volgende voorbeeld wordt getoond hoe toocreate een asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="8867a-170">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="8867a-171">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-171">**HTTP Response**</span></span>

<span data-ttu-id="8867a-172">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-172">If successful, hello following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="8867a-173">Een AssetFile maken</span><span class="sxs-lookup"><span data-stu-id="8867a-173">Create an AssetFile</span></span>
<span data-ttu-id="8867a-174">Hallo [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entiteit vertegenwoordigt een video of audio-bestand dat is opgeslagen in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="8867a-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="8867a-175">Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of meer AssetFiles bevatten.</span><span class="sxs-lookup"><span data-stu-id="8867a-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="8867a-176">Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.</span><span class="sxs-lookup"><span data-stu-id="8867a-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="8867a-177">Nadat u uw digitale media-bestand naar een blobcontainer uploadt, gebruikt u Hallo **samenvoegen** HTTP-aanvraag tooupdate hello AssetFile met informatie over uw mediabestand (zoals verderop in Hallo onderwerp).</span><span class="sxs-lookup"><span data-stu-id="8867a-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="8867a-178">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="8867a-179">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="8867a-180">Hallo AccessPolicy maken met de machtiging schrijven</span><span class="sxs-lookup"><span data-stu-id="8867a-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="8867a-181">Voordat u bestanden uploadt naar blobopslag, Hallo toegang beleid rechten instellen voor het schrijven van tooan asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="8867a-182">toodo die na een HTTP-aanvraag toohello AccessPolicies entiteit ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8867a-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="8867a-183">Een waarde DurationInMinutes tijdens het maken van definiëren of foutbericht een 500 Interne Server terug in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="8867a-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="8867a-184">Zie voor meer informatie over AccessPolicies [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="8867a-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="8867a-185">Hallo volgende voorbeeld ziet u hoe een AccessPolicy toocreate:</span><span class="sxs-lookup"><span data-stu-id="8867a-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="8867a-186">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="8867a-187">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-187">**HTTP Response**</span></span>

<span data-ttu-id="8867a-188">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-188">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a><span data-ttu-id="8867a-189">Hallo uploaden URL ophalen</span><span class="sxs-lookup"><span data-stu-id="8867a-189">Get hello Upload URL</span></span>

<span data-ttu-id="8867a-190">tooreceive Hallo werkelijke upload-URL, een SAS-Locator te maken.</span><span class="sxs-lookup"><span data-stu-id="8867a-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="8867a-191">Locators definiëren Hallo begintijd en type van het verbindingseindpunt voor clients die tooaccess bestanden in een Asset wilt.</span><span class="sxs-lookup"><span data-stu-id="8867a-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="8867a-192">U kunt meerdere Locator-entiteiten maken voor een bepaalde AccessPolicy en Asset paar toohandle andere client aanvragen en behoeften.</span><span class="sxs-lookup"><span data-stu-id="8867a-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="8867a-193">Elk van deze Locators maakt gebruik van de waarde StartTime Hallo plus Hallo DurationInMinutes waarde van Hallo AccessPolicy toodetermine Hallo tijdsduur die een URL kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8867a-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="8867a-194">Zie voor meer informatie [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="8867a-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="8867a-195">Een SAS-URL heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="8867a-196">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="8867a-196">Some considerations apply:</span></span>

* <span data-ttu-id="8867a-197">Er kan niet meer dan vijf unieke Locators die tegelijk zijn gekoppeld aan een bepaalde Asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="8867a-198">Zie voor meer informatie Locator.</span><span class="sxs-lookup"><span data-stu-id="8867a-198">For more information, see Locator.</span></span>
* <span data-ttu-id="8867a-199">Als u tooupload uw bestanden onmiddellijk moet, moet u uw StartTime waarde toofive minuten voordat de huidige tijd Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="8867a-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="8867a-200">Dit is omdat er mogelijk klok scheeftrekken tussen uw client-computer en de Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="8867a-201">De waarde StartTime moet ook zijn in de volgende datum-/ tijdindeling Hallo: jjjj-MM-ssZ (bijvoorbeeld ' 2014-05-23T17:53:50Z ').</span><span class="sxs-lookup"><span data-stu-id="8867a-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="8867a-202">Er is mogelijk een tweede 30 tot 40 vertraging nadat toowhen is beschikbaar voor gebruik door een Locator is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8867a-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="8867a-203">Dit probleem geldt tooboth SAS-URL en oorsprong Locators.</span><span class="sxs-lookup"><span data-stu-id="8867a-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="8867a-204">Zie voor meer informatie over SAS locators [dit](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="8867a-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="8867a-205">Hallo volgende voorbeeld ziet u hoe toocreate een SAS-URL-Locator, zoals gedefinieerd door de eigenschap Type in de aanvraagtekst hello ('1' voor een SAS-locator) en '2' voor een On-Demand oorsprong locator Hallo.</span><span class="sxs-lookup"><span data-stu-id="8867a-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="8867a-206">Hallo **pad** eigenschap geretourneerd bevat dat u tooupload uw bestand gebruiken moet Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="8867a-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="8867a-207">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="8867a-208">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-208">**HTTP Response**</span></span>

<span data-ttu-id="8867a-209">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-209">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="8867a-210">Uploaden van een bestand naar een blob storage-container</span><span class="sxs-lookup"><span data-stu-id="8867a-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="8867a-211">Zodra u Hallo AccessPolicy en Locator set hebt, is het werkelijke bestand Hallo geüploade tooan Azure blob storage-container die met behulp van hello Azure Storage REST-API's.</span><span class="sxs-lookup"><span data-stu-id="8867a-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="8867a-212">U moet Hallo bestanden uploaden als blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="8867a-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="8867a-213">Pagina-blobs worden niet ondersteund door Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="8867a-214">Moet u de bestandsnaam Hallo toevoegen voor het bestand Hallo gewenste tooupload toohello Locator **pad** ontvangen in de vorige sectie Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="8867a-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="8867a-215">Bijvoorbeeld: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="8867a-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="8867a-216">.</span><span class="sxs-lookup"><span data-stu-id="8867a-216">.</span></span> <span data-ttu-id="8867a-217">.</span><span class="sxs-lookup"><span data-stu-id="8867a-217">.</span></span> <span data-ttu-id="8867a-218">.</span><span class="sxs-lookup"><span data-stu-id="8867a-218">.</span></span>
>
>

<span data-ttu-id="8867a-219">Zie voor meer informatie over het werken met Azure storage-blobs [REST-API van Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="8867a-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="8867a-220">Hallo AssetFile bijwerken</span><span class="sxs-lookup"><span data-stu-id="8867a-220">Update hello AssetFile</span></span>
<span data-ttu-id="8867a-221">Nu dat u het bestand hebt geüpload, moet u Hallo FileAsset grootte (en andere) gegevens bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8867a-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="8867a-222">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8867a-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="8867a-223">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-223">**HTTP Response**</span></span>

<span data-ttu-id="8867a-224">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="8867a-225">Hallo Locator en AccessPolicy verwijderen</span><span class="sxs-lookup"><span data-stu-id="8867a-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="8867a-226">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="8867a-227">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-227">**HTTP Response**</span></span>

<span data-ttu-id="8867a-228">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="8867a-229">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="8867a-230">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-230">**HTTP Response**</span></span>

<span data-ttu-id="8867a-231">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="8867a-232"><a id="encode"></a>Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden</span><span class="sxs-lookup"><span data-stu-id="8867a-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="8867a-233">Na het opnemen van de die activa in Media Services media kunnen worden gecodeerd, transmuxed, een watermerk, enzovoort, voordat deze is geleverd tooclients.</span><span class="sxs-lookup"><span data-stu-id="8867a-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="8867a-234">Deze activiteiten worden gepland en uitgevoerd op meerdere achtergrond rol exemplaren tooensure hoge prestaties en beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="8867a-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="8867a-235">Deze activiteiten worden taken genoemd en elke taak bestaat uit atomische taken die daadwerkelijk werken op Hallo assetbestand Hallo (Zie voor meer informatie [taak](/rest/api/media/services/job), [taak](/rest/api/media/services/task) beschrijvingen).</span><span class="sxs-lookup"><span data-stu-id="8867a-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="8867a-236">Zoals eerder is vermeld, wanneer werken met Azure mediaservices een van de meest voorkomende scenario's Hallo adaptive bitrate streaming-tooyour clients levert.</span><span class="sxs-lookup"><span data-stu-id="8867a-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="8867a-237">Media Services kunt u een dynamisch pakket een set adaptive bitrate MP4-bestanden in een van de volgende indelingen Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="8867a-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="8867a-238">Hallo volgende sectie ziet u hoe toocreate een taak met één codering van de taak.</span><span class="sxs-lookup"><span data-stu-id="8867a-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="8867a-239">Hallo taak geeft tootranscode Hallo tussentijds bestand in een set adaptive bitrate MP4s met behulp van **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="8867a-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="8867a-240">Hallo sectie wordt ook uitgelegd hoe toomonitor Hallo voortgang van taak verwerken.</span><span class="sxs-lookup"><span data-stu-id="8867a-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="8867a-241">Wanneer het Hallo-taak is voltooid, zou u kunnen toocreate locators die benodigde tooget toegang tooyour activa zijn.</span><span class="sxs-lookup"><span data-stu-id="8867a-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="8867a-242">Ophalen van een Mediaprocessor</span><span class="sxs-lookup"><span data-stu-id="8867a-242">Get a media processor</span></span>
<span data-ttu-id="8867a-243">In Media Services is een Mediaprocessor een component die verantwoordelijk is voor een specifieke verwerkingstaak, zoals de codering, versleutelen of ontsleutelen media-inhoud Indelingsconversie.</span><span class="sxs-lookup"><span data-stu-id="8867a-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="8867a-244">Hallo codering van de taak wordt weergegeven in deze zelfstudie, gaan we toouse Hallo Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="8867a-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="8867a-245">Hallo volgende code aanvragen Hallo encoder-id.</span><span class="sxs-lookup"><span data-stu-id="8867a-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="8867a-246">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="8867a-247">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="8867a-248">Een taak maken</span><span class="sxs-lookup"><span data-stu-id="8867a-248">Create a job</span></span>
<span data-ttu-id="8867a-249">Elke taak kan een of meer taken, afhankelijk van Hallo type verwerken die u wilt dat tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="8867a-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="8867a-250">U kunt taken en hun bijbehorende taken via Hallo REST-API, maken op twee manieren: taken kunnen worden gedefinieerd in line via Hallo taken navigatie-eigenschap op taak entiteiten of OData-batch-verwerking.</span><span class="sxs-lookup"><span data-stu-id="8867a-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="8867a-251">Hallo Media Services SDK maakt gebruik van batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="8867a-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="8867a-252">Taken zijn echter omwille van de leesbaarheid van Hallo-codevoorbeelden in dit onderwerp Hallo inline gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="8867a-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="8867a-253">Zie voor informatie over batchverwerking, [Open Data Protocol (OData) batchverwerking](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="8867a-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="8867a-254">Hallo volgende voorbeeld ziet u hoe toocreate en na een taak met één taak ingesteld tooencode video op een specifieke oplossingsstatus en kwaliteit.</span><span class="sxs-lookup"><span data-stu-id="8867a-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="8867a-255">Hallo volgende sectie documentatie bevat Hallo lijst met alle Hallo [standaardinstellingen van de taak](http://msdn.microsoft.com/library/mt269960) ondersteund door Media Encoder Standard Hallo-processor.</span><span class="sxs-lookup"><span data-stu-id="8867a-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="8867a-256">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="8867a-257">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-257">**HTTP Response**</span></span>

<span data-ttu-id="8867a-258">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-258">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="8867a-259">Er zijn enkele belangrijke opmerkingen toonote in elke Taakaanvraag:</span><span class="sxs-lookup"><span data-stu-id="8867a-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="8867a-260">TaskBody eigenschappen moeten letterlijke XML toodefine Hallo aantal invoer of uitvoer-elementen die worden gebruikt door Hallo taak gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8867a-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="8867a-261">Hallo onderwerp bevat Hallo XML-schemadefinitie voor Hallo XML.</span><span class="sxs-lookup"><span data-stu-id="8867a-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="8867a-262">In Hallo TaskBody definition, elke interne waarde voor <inputAsset> en <outputAsset> JobInputAsset(value) of JobOutputAsset(value) moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8867a-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="8867a-263">Een taak kan meerdere uitvoer elementen hebben.</span><span class="sxs-lookup"><span data-stu-id="8867a-263">A task can have multiple output assets.</span></span> <span data-ttu-id="8867a-264">Één JobOutputAsset(x) kan slechts eenmaal worden gebruikt als uitvoer van een taak in een taak.</span><span class="sxs-lookup"><span data-stu-id="8867a-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="8867a-265">U kunt JobInputAsset of JobOutputAsset opgeven als een invoer actief van een taak.</span><span class="sxs-lookup"><span data-stu-id="8867a-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="8867a-266">Taken moeten vormen geen cyclus.</span><span class="sxs-lookup"><span data-stu-id="8867a-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="8867a-267">Hallo parameter value dat u tooJobInputAsset doorgeven of JobOutputAsset Hallo indexwaarde voor een Asset staat.</span><span class="sxs-lookup"><span data-stu-id="8867a-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="8867a-268">Hallo die werkelijke activa in Hallo InputMediaAssets en OutputMediaAssets navigatie-eigenschappen op Hallo taakdefinitie entiteit zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="8867a-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="8867a-269">Omdat het Media Services is gebouwd op OData v3, Hallo afzonderlijke activa in InputMediaAssets en OutputMediaAssets navigatie-eigenschap verzamelingen wordt verwezen door een ' __metadata: uri ' naam / waarde-paar.</span><span class="sxs-lookup"><span data-stu-id="8867a-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="8867a-270">InputMediaAssets maps tooone of meer elementen die u hebt gemaakt in een Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="8867a-271">OutputMediaAssets zijn gemaakt door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="8867a-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="8867a-272">Ze niet verwijzen naar een bestaande asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="8867a-273">OutputMediaAssets kunnen worden gebruikt als naam Hallo assetName kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8867a-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="8867a-274">Als dit kenmerk niet aanwezig is, wordt de naam van de Hallo Hallo OutputMediaAsset de waarde van de interne tekst hello Hallo is <outputAsset> -element is en het achtervoegsel Hallo taaknaam waarde of Hallo taak-Id-waarde (in geval van Hallo waar Hallo Name-eigenschap niet is gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="8867a-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="8867a-275">Bijvoorbeeld, als u een waarde voor assetName instellen voorbeeld te "Voorbeeld" en vervolgens Hallo OutputMediaAsset naam eigenschap wordt ingesteld te"".</span><span class="sxs-lookup"><span data-stu-id="8867a-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="8867a-276">Als u een waarde voor assetName niet is ingesteld, maar heeft ingesteld Hallo taaknaam zou te 'NewJob' en klik vervolgens Hallo OutputMediaAsset naam evenwel '_NewJob JobOutputAsset (waarde)'.</span><span class="sxs-lookup"><span data-stu-id="8867a-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="8867a-277">Hallo volgende voorbeeld ziet u hoe tooset Hallo assetName kenmerk:</span><span class="sxs-lookup"><span data-stu-id="8867a-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="8867a-278">tooenable taak koppeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="8867a-279">Een taak moet ten minste twee taken hebben</span><span class="sxs-lookup"><span data-stu-id="8867a-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="8867a-280">Er moet ten minste één taak waarvan invoer is de uitvoer van een andere taak in het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="8867a-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="8867a-281">Zie voor meer informatie, [maken van een taak codering met Hallo REST API voor Media Services](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="8867a-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="8867a-282">Verwerking van de voortgang van de monitor</span><span class="sxs-lookup"><span data-stu-id="8867a-282">Monitor Processing Progress</span></span>
<span data-ttu-id="8867a-283">U kunt Hallo taakstatus ophalen met behulp van de eigenschap State Hallo, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="8867a-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="8867a-284">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="8867a-285">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-285">**HTTP Response**</span></span>

<span data-ttu-id="8867a-286">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-286">If successful, hello following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="8867a-287">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="8867a-287">Cancel a job</span></span>
<span data-ttu-id="8867a-288">Media Services kunt u taken uitvoeren via Hallo CancelJob functie toocancel.</span><span class="sxs-lookup"><span data-stu-id="8867a-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="8867a-289">Deze aanroep een 400 foutcode retourneert, als u probeert een taak wanneer de status wordt geannuleerd toocancel, annuleren, fout of voltooid.</span><span class="sxs-lookup"><span data-stu-id="8867a-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="8867a-290">Hallo volgende voorbeeld wordt getoond hoe toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="8867a-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="8867a-291">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="8867a-292">Als dit lukt, wordt een 204 antwoordcode geretourneerd met geen berichttekst.</span><span class="sxs-lookup"><span data-stu-id="8867a-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="8867a-293">Moet u URL coderen Hallo taak-id (normaal gesproken nb:jid:UUID: somevalue) wanneer deze in als een parameter tooCancelJob wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="8867a-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="8867a-294">Hallo uitvoer-activum ophalen</span><span class="sxs-lookup"><span data-stu-id="8867a-294">Get hello output asset</span></span>
<span data-ttu-id="8867a-295">Hallo volgende code toont hoe toorequest Hallo uitvoer asset id.</span><span class="sxs-lookup"><span data-stu-id="8867a-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="8867a-296">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="8867a-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="8867a-297">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="8867a-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="8867a-298"><a id="publish_get_urls"></a>Hallo asset publiceren en get streamen en progressief downloaden van URL's met de REST-API</span><span class="sxs-lookup"><span data-stu-id="8867a-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="8867a-299">toostream of download een asset, u eerst moet te 'publiceren' door een locator te maken.</span><span class="sxs-lookup"><span data-stu-id="8867a-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="8867a-300">Locators bieden toegang toofiles opgenomen in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="8867a-301">Media Services ondersteunt twee typen locators: OnDemandOrigin-locators, gebruikte toostream media (bijvoorbeeld MPEG DASH, HLS of Smooth Streaming) en Access Signature (SAS)-locators, mediabestanden toodownload gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8867a-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="8867a-302">Zie voor meer informatie over SAS locators [dit](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="8867a-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="8867a-303">Als u Hallo locators hebt gemaakt, kunt u Hallo-URL's die zijn gebruikt toostream of uw bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="8867a-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="8867a-304">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="8867a-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="8867a-305">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="8867a-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="8867a-306">Een streaming-URL voor Smooth Streaming heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="8867a-307">Een streaming-URL voor HLS heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="8867a-308">Een streaming-URL voor MPEG DASH heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="8867a-309">Een SAS-URL gebruikt toodownload bestanden heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8867a-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="8867a-310">Deze sectie wordt beschreven hoe tooperform Hallo volgende taken nodig te 'publiceren' uw assets.</span><span class="sxs-lookup"><span data-stu-id="8867a-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="8867a-311">Hallo AccessPolicy maken met leesmachtiging</span><span class="sxs-lookup"><span data-stu-id="8867a-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="8867a-312">Maken van een SAS-URL voor het downloaden van inhoud</span><span class="sxs-lookup"><span data-stu-id="8867a-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="8867a-313">Maken van een oorsprong-URL voor het streaming-inhoud</span><span class="sxs-lookup"><span data-stu-id="8867a-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="8867a-314">Hallo AccessPolicy maken met leesmachtiging</span><span class="sxs-lookup"><span data-stu-id="8867a-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="8867a-315">Voordat u downloaden of streamen van mediainhoud, moet u eerst een AccessPolicy met leesmachtigingen definiëren en het juiste Locator entiteit hello, waarmee Hallo type maken van bezorgingsmechanisme gewenste tooenable voor uw clients.</span><span class="sxs-lookup"><span data-stu-id="8867a-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="8867a-316">Zie voor meer informatie over Hallo eigenschappen beschikbaar [AccessPolicy entiteitseigenschappen](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="8867a-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="8867a-317">Hallo volgende voorbeeld ziet u hoe toospecify AccessPolicy Hallo voor leesmachtigingen voor een bepaalde Asset.</span><span class="sxs-lookup"><span data-stu-id="8867a-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="8867a-318">Als dit lukt, wordt een 201 code geretourneerd met een beschrijving van Hallo AccessPolicy entiteit die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8867a-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="8867a-319">Vervolgens gebruikt u Hallo AccessPolicy Id samen met de Hallo Asset-Id van Hallo asset die u wilt dat toodeliver (zoals een uitvoerasset) toocreate Hallo Locator entiteit Hallo-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="8867a-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="8867a-320">Deze basiswerkstroom is Hallo hetzelfde als het uploaden van een bestand bij het opnemen van een actief (zoals eerder in dit onderwerp is beschreven).</span><span class="sxs-lookup"><span data-stu-id="8867a-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="8867a-321">Stel ook uw StartTime waarde toofive minuten voordat de huidige tijd Hallo zoals het uploaden van bestanden, als u (of uw clients) tooaccess moeten uw bestanden onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="8867a-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="8867a-322">Deze actie is nodig omdat er mogelijk klok scheeftrekken tussen Hallo-client en Media Services.</span><span class="sxs-lookup"><span data-stu-id="8867a-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="8867a-323">Hallo waarde StartTime moet in de volgende datum-/ tijdindeling Hallo: jjjj-MM-ssZ (bijvoorbeeld ' 2014-05-23T17:53:50Z ').</span><span class="sxs-lookup"><span data-stu-id="8867a-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="8867a-324">Maken van een SAS-URL voor het downloaden van inhoud</span><span class="sxs-lookup"><span data-stu-id="8867a-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="8867a-325">Hallo volgende code ziet u hoe tooget een URL die u gebruikte toodownload een mediabestand kan worden gemaakt en eerder hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="8867a-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="8867a-326">Hallo AccessPolicy machtigingenset heeft lees- en Hallo Locator pad verwijst tooa SAS download-URL.</span><span class="sxs-lookup"><span data-stu-id="8867a-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="8867a-327">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-327">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="8867a-328">Hallo geretourneerd **pad** eigenschap Hallo SAS-URL bevat.</span><span class="sxs-lookup"><span data-stu-id="8867a-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="8867a-329">Als u opslag versleutelde inhoud downloaden, moet u handmatig ontsleutelen voordat deze of Hallo opslag ontsleuteling MediaProcessor in een taak verwerking toooutput verwerkt bestanden in Hallo wissen tooan OutputAsset en vervolgens downloaden uit het actief gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8867a-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="8867a-330">Zie voor het maken van een taak codering met Hallo REST API voor Media Services voor meer informatie over verwerking.</span><span class="sxs-lookup"><span data-stu-id="8867a-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="8867a-331">Bovendien kan niet Locators van SAS-URL worden bijgewerkt nadat ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8867a-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="8867a-332">Bijvoorbeeld, u niet opnieuw gebruiken dezelfde Locator met de bijgewerkte waarde StartTime Hallo.</span><span class="sxs-lookup"><span data-stu-id="8867a-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="8867a-333">Dit is vanwege Hallo manier die SAS-URL's worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8867a-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="8867a-334">Als u na een Locator is verlopen tooaccess een asset downloaden wilt, moet u een nieuw bestand met een nieuwe StartTime maken.</span><span class="sxs-lookup"><span data-stu-id="8867a-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="8867a-335">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="8867a-335">Download files</span></span>
<span data-ttu-id="8867a-336">Als u Hallo AccessPolicy en Locator set hebt, kunt u bestanden met behulp van hello Azure Storage REST-API's downloaden.</span><span class="sxs-lookup"><span data-stu-id="8867a-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="8867a-337">Moet u de bestandsnaam Hallo toevoegen voor het bestand Hallo gewenste toodownload toohello Locator **pad** ontvangen in de vorige sectie Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="8867a-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="8867a-338">Bijvoorbeeld: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="8867a-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="8867a-339">.</span><span class="sxs-lookup"><span data-stu-id="8867a-339">.</span></span> <span data-ttu-id="8867a-340">.</span><span class="sxs-lookup"><span data-stu-id="8867a-340">.</span></span> <span data-ttu-id="8867a-341">.</span><span class="sxs-lookup"><span data-stu-id="8867a-341">.</span></span>
>
>

<span data-ttu-id="8867a-342">Zie voor meer informatie over het werken met Azure storage-blobs [REST-API van Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="8867a-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="8867a-343">Als gevolg van Hallo codering van de taak die u eerder hebt uitgevoerd (codering in adaptieve MP4-set), hebt u meerdere MP4-bestanden die u kunt progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="8867a-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="8867a-344">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8867a-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="8867a-345">Maken van een streaming-URL voor het streaming-inhoud</span><span class="sxs-lookup"><span data-stu-id="8867a-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="8867a-346">Hallo van de volgende code toont hoe een streaming-URL-Locator toocreate:</span><span class="sxs-lookup"><span data-stu-id="8867a-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="8867a-347">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="8867a-347">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="8867a-348">toostream een oorsprong Smooth Streaming-URL in een streaming MediaPlayer, moet u Hallo Path-eigenschap met de naam van Hallo Smooth Streaming-manifestbestand, gevolgd door ' / manifest ' hello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8867a-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="8867a-349">toostream HLS, toevoegen (format = m3u8-aapl) na Hallo '/ manifest'.</span><span class="sxs-lookup"><span data-stu-id="8867a-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="8867a-350">toostream MPEG DASH toevoegen (format = mpd-time-csf) na Hallo '/ manifest'.</span><span class="sxs-lookup"><span data-stu-id="8867a-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="8867a-351"><a id="play"></a>Uw inhoud afspelen</span><span class="sxs-lookup"><span data-stu-id="8867a-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="8867a-352">toostream video u [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="8867a-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="8867a-353">tootest progressief downloaden, plakt u een URL in een browser (bijvoorbeeld Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="8867a-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="8867a-354">Volgende stappen: Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="8867a-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8867a-355">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="8867a-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
