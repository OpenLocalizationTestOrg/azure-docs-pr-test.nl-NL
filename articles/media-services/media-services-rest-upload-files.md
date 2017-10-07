---
title: aaaUpload bestanden naar een Media Services-account met behulp van REST | Microsoft Docs
description: Meer informatie over hoe tooget media van inhoud in Media Services door het maken en uploaden van activa.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="f11f7-103">Bestanden uploaden naar een Media Services-account met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="f11f7-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f11f7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f11f7-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="f11f7-105">REST</span><span class="sxs-lookup"><span data-stu-id="f11f7-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="f11f7-106">Portal</span><span class="sxs-lookup"><span data-stu-id="f11f7-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="f11f7-107">In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="f11f7-108">Hallo [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload naar Hallo asset, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="f11f7-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="f11f7-109">Hallo overwegingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="f11f7-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="f11f7-110">Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f11f7-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="f11f7-111">waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '.</span><span class="sxs-lookup"><span data-stu-id="f11f7-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="f11f7-112">Bovendien kunnen alleen er een '.' hello bestandsnaamextensie.</span><span class="sxs-lookup"><span data-stu-id="f11f7-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="f11f7-113">Hallo-lengte van Hallo-naam mag niet groter zijn dan 260 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="f11f7-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="f11f7-114">Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f11f7-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="f11f7-115">Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="f11f7-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="f11f7-116">Hallo basiswerkstroom voor het uploaden van de activa is onderverdeeld in Hallo uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f11f7-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="f11f7-117">Maak een Asset</span><span class="sxs-lookup"><span data-stu-id="f11f7-117">Create an Asset</span></span>
* <span data-ttu-id="f11f7-118">Versleutelen van een actief (optioneel)</span><span class="sxs-lookup"><span data-stu-id="f11f7-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="f11f7-119">Een bestandsopslag tooblob uploaden</span><span class="sxs-lookup"><span data-stu-id="f11f7-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="f11f7-120">AMS kunt u ook tooupload activa in bulk.</span><span class="sxs-lookup"><span data-stu-id="f11f7-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="f11f7-121">Zie [deze](media-services-rest-upload-files.md#upload_in_bulk) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f11f7-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="f11f7-122">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f11f7-123">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f11f7-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="f11f7-124">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="f11f7-124">Connect tooMedia Services</span></span>

<span data-ttu-id="f11f7-125">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f11f7-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f11f7-126">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="f11f7-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f11f7-127">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="f11f7-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="f11f7-128">Uploaden van activa</span><span class="sxs-lookup"><span data-stu-id="f11f7-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="f11f7-129">Maak een asset</span><span class="sxs-lookup"><span data-stu-id="f11f7-129">Create an asset</span></span>

<span data-ttu-id="f11f7-130">Een actief is een container voor meerdere typen of sets van objecten in Media Services, waaronder video, audio, afbeeldingen, verzamelingen miniaturen, tekst-nummers en ondertitelingsbestanden bestanden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="f11f7-131">In de REST-API maken van een Asset, moet u verzenden POST Hallo tooMedia Services aanvragen en eigenschapsinformatie over uw asset in de aanvraagtekst hello te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="f11f7-132">Hallo-eigenschappen die u kunt opgeven wanneer het maken van een asset is **opties**.</span><span class="sxs-lookup"><span data-stu-id="f11f7-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="f11f7-133">**Opties** is een opsommingswaarde die Hallo versleuteling worden opties die een Asset kan worden gemaakt beschreven met.</span><span class="sxs-lookup"><span data-stu-id="f11f7-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="f11f7-134">Een geldige waarde is een van de waarden Hallo Hallo onderstaande lijst, niet een combinatie van waarden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="f11f7-135">**Geen** = **0**: er wordt geen versleuteling wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="f11f7-136">Dit is de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="f11f7-136">This is hello default value.</span></span> <span data-ttu-id="f11f7-137">Houd er rekening mee dat wanneer u deze optie uw inhoud wordt niet beveiligd tijdens de overdracht of in rust in de opslag.</span><span class="sxs-lookup"><span data-stu-id="f11f7-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="f11f7-138">Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f11f7-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="f11f7-139">**StorageEncrypted** = **1**: Geef op of u voor uw bestanden toobe versleuteld met AES-256-bits codering voor uploaden en opslag.</span><span class="sxs-lookup"><span data-stu-id="f11f7-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="f11f7-140">Als uw asset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="f11f7-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="f11f7-141">Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f11f7-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="f11f7-142">**CommonEncryptionProtected** = **2**: als u van bestanden die zijn beveiligd met een gemeenschappelijke coderingsmethode (zoals PlayReady uploaden) opgeven.</span><span class="sxs-lookup"><span data-stu-id="f11f7-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="f11f7-143">**EnvelopeEncryptionProtected** = **4**: opgeven als u HLS versleuteld met AES-bestanden wilt uploaden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="f11f7-144">Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="f11f7-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f11f7-145">Als uw asset kan versleuteling gebruiken wilt, moet u een **ContentKey** en een koppeling tooyour asset zoals beschreven in het volgende onderwerp Hallo:[hoe toocreate een ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="f11f7-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="f11f7-146">Nadat u Hallo-bestanden in Hallo asset uploadt, u eigenschappen voor de versleuteling van tooupdate Hallo op Hallo moet Opmerking **AssetFile** entiteit met Hallo-waarden die u hebt verkregen tijdens het Hallo **Asset** versleuteling.</span><span class="sxs-lookup"><span data-stu-id="f11f7-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="f11f7-147">Dit doen met behulp van Hallo **samenvoegen** HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f11f7-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="f11f7-148">Hallo volgende voorbeeld wordt getoond hoe toocreate een asset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="f11f7-149">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="f11f7-150">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-150">**HTTP Response**</span></span>

<span data-ttu-id="f11f7-151">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="f11f7-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="f11f7-152">Een AssetFile maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-152">Create an AssetFile</span></span>
<span data-ttu-id="f11f7-153">Hallo [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entiteit vertegenwoordigt een video of audio-bestand dat is opgeslagen in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="f11f7-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="f11f7-154">Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of meer assetbestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="f11f7-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="f11f7-155">Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.</span><span class="sxs-lookup"><span data-stu-id="f11f7-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="f11f7-156">Houd er rekening mee dat Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten.</span><span class="sxs-lookup"><span data-stu-id="f11f7-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="f11f7-157">Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.</span><span class="sxs-lookup"><span data-stu-id="f11f7-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="f11f7-158">Nadat u uw digitale media-bestand naar een blobcontainer uploadt, gaat u Hallo **samenvoegen** HTTP-aanvraag tooupdate hello AssetFile met informatie over uw mediabestand (zoals verderop in Hallo onderwerp).</span><span class="sxs-lookup"><span data-stu-id="f11f7-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="f11f7-159">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="f11f7-160">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="f11f7-161">Hallo AccessPolicy maken met de machtiging schrijven.</span><span class="sxs-lookup"><span data-stu-id="f11f7-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="f11f7-162">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f11f7-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f11f7-163">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="f11f7-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f11f7-164">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f11f7-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="f11f7-165">Voordat u bestanden uploadt naar blobopslag, Hallo toegang beleid rechten instellen voor het schrijven van tooan asset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="f11f7-166">toodo die na een HTTP-aanvraag toohello AccessPolicies entiteit ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f11f7-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="f11f7-167">Een waarde DurationInMinutes tijdens het maken van definiëren of ontvangt u een 500 Interne Server foutbericht terug in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="f11f7-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="f11f7-168">Zie voor meer informatie over AccessPolicies [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="f11f7-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="f11f7-169">Hallo volgende voorbeeld ziet u hoe een AccessPolicy toocreate:</span><span class="sxs-lookup"><span data-stu-id="f11f7-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="f11f7-170">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="f11f7-171">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="f11f7-172">Hallo uploaden URL ophalen</span><span class="sxs-lookup"><span data-stu-id="f11f7-172">Get hello Upload URL</span></span>
<span data-ttu-id="f11f7-173">tooreceive Hallo werkelijke upload-URL, een SAS-Locator te maken.</span><span class="sxs-lookup"><span data-stu-id="f11f7-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="f11f7-174">Locators definiëren Hallo begintijd en type van het verbindingseindpunt voor clients die tooaccess bestanden in een Asset wilt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="f11f7-175">U kunt meerdere Locator-entiteiten maken voor een bepaalde AccessPolicy en Asset paar toohandle andere client aanvragen en behoeften.</span><span class="sxs-lookup"><span data-stu-id="f11f7-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="f11f7-176">Elk van deze Locators gebruik de waarde StartTime Hallo plus Hallo DurationInMinutes waarde van Hallo AccessPolicy toodetermine Hallo tijdsduur een URL kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="f11f7-177">Zie voor meer informatie [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="f11f7-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="f11f7-178">Een SAS-URL heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="f11f7-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="f11f7-179">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="f11f7-179">Some considerations apply:</span></span>

* <span data-ttu-id="f11f7-180">Er kan niet meer dan vijf unieke Locators die tegelijk zijn gekoppeld aan een bepaalde Asset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="f11f7-181">Zie voor meer informatie Locator.</span><span class="sxs-lookup"><span data-stu-id="f11f7-181">For more information, see Locator.</span></span>
* <span data-ttu-id="f11f7-182">Als u tooupload uw bestanden onmiddellijk moet, moet u uw StartTime waarde toofive minuten voordat de huidige tijd Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="f11f7-183">Dit is omdat er mogelijk klok scheeftrekken tussen uw client-computer en de Media Services.</span><span class="sxs-lookup"><span data-stu-id="f11f7-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="f11f7-184">De waarde StartTime moet ook zijn in de volgende datum-/ tijdindeling Hallo: jjjj-MM-ssZ (bijvoorbeeld ' 2014-05-23T17:53:50Z ').</span><span class="sxs-lookup"><span data-stu-id="f11f7-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="f11f7-185">Er is mogelijk een tweede 30 tot 40 vertraging nadat toowhen is beschikbaar voor gebruik door een Locator is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="f11f7-186">Dit probleem geldt tooboth SAS-URL en oorsprong Locators.</span><span class="sxs-lookup"><span data-stu-id="f11f7-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="f11f7-187">Hallo volgende voorbeeld ziet u hoe toocreate een SAS-URL-Locator, zoals gedefinieerd door de eigenschap Type in de aanvraagtekst hello ('1' voor een SAS-locator) en '2' voor een On-Demand oorsprong locator Hallo.</span><span class="sxs-lookup"><span data-stu-id="f11f7-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="f11f7-188">Hallo **pad** eigenschap geretourneerd bevat dat u tooupload uw bestand gebruiken moet Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="f11f7-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="f11f7-189">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="f11f7-190">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-190">**HTTP Response**</span></span>

<span data-ttu-id="f11f7-191">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="f11f7-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="f11f7-192">Uploaden van een bestand naar een blob storage-container</span><span class="sxs-lookup"><span data-stu-id="f11f7-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="f11f7-193">Zodra u Hallo AccessPolicy en Locator set hebt, is het werkelijke bestand Hallo geüploade tooan Azure Blob Storage-container met behulp van hello Azure Storage REST-API's.</span><span class="sxs-lookup"><span data-stu-id="f11f7-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="f11f7-194">U moet Hallo bestanden uploaden als blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="f11f7-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="f11f7-195">Pagina-blobs worden niet ondersteund door Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="f11f7-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="f11f7-196">Moet u de bestandsnaam Hallo toevoegen voor het bestand Hallo gewenste tooupload toohello Locator **pad** ontvangen in de vorige sectie Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="f11f7-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="f11f7-197">Bijvoorbeeld: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="f11f7-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="f11f7-198">.</span><span class="sxs-lookup"><span data-stu-id="f11f7-198">.</span></span> <span data-ttu-id="f11f7-199">.</span><span class="sxs-lookup"><span data-stu-id="f11f7-199">.</span></span> <span data-ttu-id="f11f7-200">.</span><span class="sxs-lookup"><span data-stu-id="f11f7-200">.</span></span> 
> 
> 

<span data-ttu-id="f11f7-201">Zie voor meer informatie over het werken met Azure storage-blobs [REST-API van Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="f11f7-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="f11f7-202">Hallo AssetFile bijwerken</span><span class="sxs-lookup"><span data-stu-id="f11f7-202">Update hello AssetFile</span></span>
<span data-ttu-id="f11f7-203">Nu dat u het bestand hebt geüpload, moet u Hallo FileAsset grootte (en andere) gegevens bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f11f7-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="f11f7-204">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f11f7-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="f11f7-205">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-205">**HTTP Response**</span></span>

<span data-ttu-id="f11f7-206">Als geslaagd, Hallo volgende geretourneerd: HTTP/1.1 204 geen inhoud</span><span class="sxs-lookup"><span data-stu-id="f11f7-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="f11f7-207">Hallo Locator en AccessPolicy verwijderen</span><span class="sxs-lookup"><span data-stu-id="f11f7-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="f11f7-208">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="f11f7-209">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-209">**HTTP Response**</span></span>

<span data-ttu-id="f11f7-210">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="f11f7-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="f11f7-211">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="f11f7-212">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-212">**HTTP Response**</span></span>

<span data-ttu-id="f11f7-213">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="f11f7-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="f11f7-214"><a id="upload_in_bulk"></a>Activa in bulk uploaden</span><span class="sxs-lookup"><span data-stu-id="f11f7-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="f11f7-215">Hallo IngestManifest maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-215">Create hello IngestManifest</span></span>
<span data-ttu-id="f11f7-216">Hallo IngestManifest is een container voor een set van assets, assetbestanden en statistische gegevens die kan worden gebruikt toodetermine Hallo voortgang van het opnemen van grote hoeveelheden voor Hallo set.</span><span class="sxs-lookup"><span data-stu-id="f11f7-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="f11f7-217">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="f11f7-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="f11f7-218">Activa maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-218">Create assets</span></span>
<span data-ttu-id="f11f7-219">Voordat u Hallo IngestManifestAsset maakt, moet u toocreate Hallo Asset die wordt voltooid met het opnemen van grote hoeveelheden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="f11f7-220">Een actief is een container voor meerdere typen of sets van objecten in Media Services, waaronder video, audio, afbeeldingen, verzamelingen miniaturen, tekst-nummers en ondertitelingsbestanden bestanden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="f11f7-221">Maken van een Asset vereist in Hallo REST-API, het verzenden van een HTTP POST-aanvraag tooMicrosoft Azure Media Services en eigenschapsinformatie over uw asset plaatsen in de aanvraagtekst Hallo. In dit voorbeeld wordt Hallo Asset gemaakt met Hallo StorageEncrption(1) optie opgenomen in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="f11f7-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="f11f7-222">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="f11f7-223">Hallo IngestManifestAssets maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="f11f7-224">IngestManifestAssets vertegenwoordigen activa in een IngestManifest die worden gebruikt met het opnemen van grote hoeveelheden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="f11f7-225">Hallo koppelen in feite Hallo asset toohello manifest.</span><span class="sxs-lookup"><span data-stu-id="f11f7-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="f11f7-226">Azure Media Services bestandswijzigingsmeldingscontrole intern uploaden Hallo-bestand op basis van IngestManifestFiles verzameling die is gekoppeld toohello IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="f11f7-227">Wanneer deze bestanden zijn geüpload, is Hallo asset voltooid.</span><span class="sxs-lookup"><span data-stu-id="f11f7-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="f11f7-228">U kunt een nieuwe IngestManifestAsset maken met een HTTP POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f11f7-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="f11f7-229">In de aanvraagtekst hello, omvatten Hallo IngestManifest-Id en Hallo activa-Id die Hallo IngestManifestAsset samen moeten worden gekoppeld voor het opnemen van grote hoeveelheden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="f11f7-230">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="f11f7-231">Hallo IngestManifestFiles voor elk activum maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="f11f7-232">Een IngestManifestFile vertegenwoordigt een werkelijke video of audio blob-object dat wordt geüpload als onderdeel van het opnemen van grote hoeveelheden voor een asset.</span><span class="sxs-lookup"><span data-stu-id="f11f7-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="f11f7-233">Versleuteling gerelateerd eigenschappen zijn niet vereist tenzij Hallo asset een versleutelingsoptie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="f11f7-234">Hallo-voorbeeld gebruikt in deze sectie wordt gedemonstreerd StorageEncryption maken van een IngestManifestFile die worden gebruikt voor Hallo die Asset eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f11f7-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="f11f7-235">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="f11f7-236">Hallo bestanden tooBlob opslag uploaden</span><span class="sxs-lookup"><span data-stu-id="f11f7-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="f11f7-237">U kunt een clienttoepassing hoge snelheid kunnen uploaden Hallo asset bestanden toohello blob storage-container door Hallo BlobStorageUriForUpload eigenschap Hallo IngestManifest opgegeven Uri gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f11f7-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="f11f7-238">Een opmerkelijke hoge snelheid uploaden service [Aspera On Demand voor Azure-toepassing](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="f11f7-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="f11f7-239">Monitor bulksgewijs voortgang opnemen</span><span class="sxs-lookup"><span data-stu-id="f11f7-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="f11f7-240">U kunt voortgang Hallo van Bulksgewijze bewerkingen voor een IngestManifest door Hallo statistieken eigenschap Hallo IngestManifest opnemen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="f11f7-241">Of eigenschap een complex type is [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="f11f7-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="f11f7-242">toopoll hello statistieken-eigenschap verzenden van een HTTP GET-aanvraag doorgeven Hallo IngestManifest-id.</span><span class="sxs-lookup"><span data-stu-id="f11f7-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="f11f7-243">ContentKeys gebruikt voor versleuteling maken</span><span class="sxs-lookup"><span data-stu-id="f11f7-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="f11f7-244">Als uw asset kan versleuteling gebruiken wilt, moet u Hallo ContentKey toobe gebruikt voor versleuteling voordat u Hallo assetbestanden maken.</span><span class="sxs-lookup"><span data-stu-id="f11f7-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="f11f7-245">Storage Encryption moeten hello volgende eigenschappen worden opgenomen in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="f11f7-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="f11f7-246">De eigenschap body aanvraag</span><span class="sxs-lookup"><span data-stu-id="f11f7-246">Request body property</span></span> | <span data-ttu-id="f11f7-247">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f11f7-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f11f7-248">Id</span><span class="sxs-lookup"><span data-stu-id="f11f7-248">Id</span></span> |<span data-ttu-id="f11f7-249">Hallo ContentKey-Id die we genereren onszelf met behulp van de volgende Hallo-indeling, ' nb:kid:UUID:<NEW GUID>'.</span><span class="sxs-lookup"><span data-stu-id="f11f7-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="f11f7-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="f11f7-250">ContentKeyType</span></span> |<span data-ttu-id="f11f7-251">Dit is Hallo inhoudtype belangrijke als een geheel getal voor deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="f11f7-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="f11f7-252">Hallo waarde 1 voor versleuteling van opslag doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="f11f7-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="f11f7-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="f11f7-253">EncryptedContentKey</span></span> |<span data-ttu-id="f11f7-254">We maken een nieuwe inhoud sleutelwaarde die een (32 byte) 256-bits waarde.</span><span class="sxs-lookup"><span data-stu-id="f11f7-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="f11f7-255">Hallo sleutel is gecodeerd met Hallo opslag versleuteling x.509-certificaat dat we uit Microsoft Azure Media Services ophalen door het uitvoeren van een HTTP GET-aanvraag voor Hallo GetProtectionKeyId en GetProtectionKey methoden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="f11f7-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="f11f7-256">ProtectionKeyId</span></span> |<span data-ttu-id="f11f7-257">Dit is protection sleutel-id voor Hallo opslag versleuteling X.509-certificaat dat gebruikt tooencrypt is Hallo onze inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f11f7-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="f11f7-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="f11f7-258">ProtectionKeyType</span></span> |<span data-ttu-id="f11f7-259">Dit is Hallo versleutelingstype voor Hallo beveiliging sleutel die gebruikt tooencrypt hello inhoudssleutel is.</span><span class="sxs-lookup"><span data-stu-id="f11f7-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="f11f7-260">Deze waarde is StorageEncryption(1) in ons voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f11f7-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="f11f7-261">Controlesom</span><span class="sxs-lookup"><span data-stu-id="f11f7-261">Checksum</span></span> |<span data-ttu-id="f11f7-262">Hallo MD5 berekende controlesom voor Hallo inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f11f7-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="f11f7-263">Deze wordt berekend door Hallo inhoud Id met Hallo inhoudssleutel te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="f11f7-264">Hallo voorbeeldcode laat zien hoe toocalculate Hallo controlesom.</span><span class="sxs-lookup"><span data-stu-id="f11f7-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="f11f7-265">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="f11f7-266">Hallo ContentKey toohello Asset koppelen</span><span class="sxs-lookup"><span data-stu-id="f11f7-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="f11f7-267">Hallo ContentKey is gekoppeld tooone of meer elementen door een HTTP POST-aanvraag te verzenden.</span><span class="sxs-lookup"><span data-stu-id="f11f7-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="f11f7-268">Hallo is volgende aanvraag een voorbeeld toolink Hallo voorbeeld ContentKey toohello voorbeeld actief op-id.</span><span class="sxs-lookup"><span data-stu-id="f11f7-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="f11f7-269">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="f11f7-270">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="f11f7-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="f11f7-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f11f7-271">Next steps</span></span>

<span data-ttu-id="f11f7-272">U kunt nu de geüploade assets coderen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="f11f7-273">Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f11f7-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="f11f7-274">U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="f11f7-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="f11f7-275">Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f11f7-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f11f7-276">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f11f7-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f11f7-277">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f11f7-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

