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
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Bestanden uploaden naar een Media Services-account met behulp van REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset. Hallo [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload naar Hallo asset, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming. 

> [!NOTE]
> Hallo overwegingen volgende van toepassing:
> 
> * Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan. waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '. Bovendien kunnen alleen er een '.' hello bestandsnaamextensie.
> * Hallo-lengte van Hallo-naam mag niet groter zijn dan 260 tekens zijn.
> * Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund. Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.
> 

Hallo basiswerkstroom voor het uploaden van de activa is onderverdeeld in Hallo uit te voeren:

* Maak een Asset
* Versleutelen van een actief (optioneel)
* Een bestandsopslag tooblob uploaden

AMS kunt u ook tooupload activa in bulk. Zie [deze](media-services-rest-upload-files.md#upload_in_bulk) sectie voor meer informatie.

> [!NOTE]
> Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen. Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>Verbinding maken met tooMedia Services

Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.

## <a name="upload-assets"></a>Uploaden van activa

### <a name="create-an-asset"></a>Maak een asset

Een actief is een container voor meerdere typen of sets van objecten in Media Services, waaronder video, audio, afbeeldingen, verzamelingen miniaturen, tekst-nummers en ondertitelingsbestanden bestanden. In de REST-API maken van een Asset, moet u verzenden POST Hallo tooMedia Services aanvragen en eigenschapsinformatie over uw asset in de aanvraagtekst hello te plaatsen.

Hallo-eigenschappen die u kunt opgeven wanneer het maken van een asset is **opties**. **Opties** is een opsommingswaarde die Hallo versleuteling worden opties die een Asset kan worden gemaakt beschreven met. Een geldige waarde is een van de waarden Hallo Hallo onderstaande lijst, niet een combinatie van waarden. 

* **Geen** = **0**: er wordt geen versleuteling wordt gebruikt. Dit is de standaardwaarde Hallo. Houd er rekening mee dat wanneer u deze optie uw inhoud wordt niet beveiligd tijdens de overdracht of in rust in de opslag.
    Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken. 
* **StorageEncrypted** = **1**: Geef op of u voor uw bestanden toobe versleuteld met AES-256-bits codering voor uploaden en opslag.
  
    Als uw asset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren. Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2**: als u van bestanden die zijn beveiligd met een gemeenschappelijke coderingsmethode (zoals PlayReady uploaden) opgeven. 
* **EnvelopeEncryptionProtected** = **4**: opgeven als u HLS versleuteld met AES-bestanden wilt uploaden. Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.

> [!NOTE]
> Als uw asset kan versleuteling gebruiken wilt, moet u een **ContentKey** en een koppeling tooyour asset zoals beschreven in het volgende onderwerp Hallo:[hoe toocreate een ContentKey](media-services-rest-create-contentkey.md). Nadat u Hallo-bestanden in Hallo asset uploadt, u eigenschappen voor de versleuteling van tooupdate Hallo op Hallo moet Opmerking **AssetFile** entiteit met Hallo-waarden die u hebt verkregen tijdens het Hallo **Asset** versleuteling. Dit doen met behulp van Hallo **samenvoegen** HTTP-aanvraag. 
> 
> 

Hallo volgende voorbeeld wordt getoond hoe toocreate een asset.

**HTTP-aanvraag**

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

**HTTP-antwoord**

Als dit lukt, wordt de volgende Hallo geretourneerd:

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

### <a name="create-an-assetfile"></a>Een AssetFile maken
Hallo [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entiteit vertegenwoordigt een video of audio-bestand dat is opgeslagen in een blob-container. Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of meer assetbestanden bevatten. Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.

Houd er rekening mee dat Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten. Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.

Nadat u uw digitale media-bestand naar een blobcontainer uploadt, gaat u Hallo **samenvoegen** HTTP-aanvraag tooupdate hello AssetFile met informatie over uw mediabestand (zoals verderop in Hallo onderwerp). 

**HTTP-aanvraag**

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

**HTTP-antwoord**

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a>Hallo AccessPolicy maken met de machtiging schrijven.

>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

Voordat u bestanden uploadt naar blobopslag, Hallo toegang beleid rechten instellen voor het schrijven van tooan asset. toodo die na een HTTP-aanvraag toohello AccessPolicies entiteit ingesteld. Een waarde DurationInMinutes tijdens het maken van definiëren of ontvangt u een 500 Interne Server foutbericht terug in het antwoord. Zie voor meer informatie over AccessPolicies [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Hallo volgende voorbeeld ziet u hoe een AccessPolicy toocreate:

**HTTP-aanvraag**

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

**HTTP-aanvraag**

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

### <a name="get-hello-upload-url"></a>Hallo uploaden URL ophalen
tooreceive Hallo werkelijke upload-URL, een SAS-Locator te maken. Locators definiëren Hallo begintijd en type van het verbindingseindpunt voor clients die tooaccess bestanden in een Asset wilt. U kunt meerdere Locator-entiteiten maken voor een bepaalde AccessPolicy en Asset paar toohandle andere client aanvragen en behoeften. Elk van deze Locators gebruik de waarde StartTime Hallo plus Hallo DurationInMinutes waarde van Hallo AccessPolicy toodetermine Hallo tijdsduur een URL kan worden gebruikt. Zie voor meer informatie [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).

Een SAS-URL heeft Hallo volgende indeling:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Hierbij geldt het volgende:

* Er kan niet meer dan vijf unieke Locators die tegelijk zijn gekoppeld aan een bepaalde Asset. Zie voor meer informatie Locator.
* Als u tooupload uw bestanden onmiddellijk moet, moet u uw StartTime waarde toofive minuten voordat de huidige tijd Hallo instellen. Dit is omdat er mogelijk klok scheeftrekken tussen uw client-computer en de Media Services. De waarde StartTime moet ook zijn in de volgende datum-/ tijdindeling Hallo: jjjj-MM-ssZ (bijvoorbeeld ' 2014-05-23T17:53:50Z ').    
* Er is mogelijk een tweede 30 tot 40 vertraging nadat toowhen is beschikbaar voor gebruik door een Locator is gemaakt. Dit probleem geldt tooboth SAS-URL en oorsprong Locators.

Hallo volgende voorbeeld ziet u hoe toocreate een SAS-URL-Locator, zoals gedefinieerd door de eigenschap Type in de aanvraagtekst hello ('1' voor een SAS-locator) en '2' voor een On-Demand oorsprong locator Hallo. Hallo **pad** eigenschap geretourneerd bevat dat u tooupload uw bestand gebruiken moet Hallo-URL.

**HTTP-aanvraag**

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

**HTTP-antwoord**

Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:

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

### <a name="upload-a-file-into-a-blob-storage-container"></a>Uploaden van een bestand naar een blob storage-container
Zodra u Hallo AccessPolicy en Locator set hebt, is het werkelijke bestand Hallo geüploade tooan Azure Blob Storage-container met behulp van hello Azure Storage REST-API's. U moet Hallo bestanden uploaden als blok-blobs. Pagina-blobs worden niet ondersteund door Azure Media Services.  

> [!NOTE]
> Moet u de bestandsnaam Hallo toevoegen voor het bestand Hallo gewenste tooupload toohello Locator **pad** ontvangen in de vorige sectie Hallo waarde. Bijvoorbeeld: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Zie voor meer informatie over het werken met Azure storage-blobs [REST-API van Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Hallo AssetFile bijwerken
Nu dat u het bestand hebt geüpload, moet u Hallo FileAsset grootte (en andere) gegevens bijwerken. Bijvoorbeeld:

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


**HTTP-antwoord**

Als geslaagd, Hallo volgende geretourneerd: HTTP/1.1 204 geen inhoud

### <a name="delete-hello-locator-and-accesspolicy"></a>Hallo Locator en AccessPolicy verwijderen
**HTTP-aanvraag**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP-antwoord**

Als dit lukt, wordt de volgende Hallo geretourneerd:

    HTTP/1.1 204 No Content 
    ...

**HTTP-aanvraag**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP-antwoord**

Als dit lukt, wordt de volgende Hallo geretourneerd:

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Activa in bulk uploaden
### <a name="create-hello-ingestmanifest"></a>Hallo IngestManifest maken
Hallo IngestManifest is een container voor een set van assets, assetbestanden en statistische gegevens die kan worden gebruikt toodetermine Hallo voortgang van het opnemen van grote hoeveelheden voor Hallo set.

**HTTP-aanvraag**

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

### <a name="create-assets"></a>Activa maken
Voordat u Hallo IngestManifestAsset maakt, moet u toocreate Hallo Asset die wordt voltooid met het opnemen van grote hoeveelheden. Een actief is een container voor meerdere typen of sets van objecten in Media Services, waaronder video, audio, afbeeldingen, verzamelingen miniaturen, tekst-nummers en ondertitelingsbestanden bestanden. Maken van een Asset vereist in Hallo REST-API, het verzenden van een HTTP POST-aanvraag tooMicrosoft Azure Media Services en eigenschapsinformatie over uw asset plaatsen in de aanvraagtekst Hallo. In dit voorbeeld wordt Hallo Asset gemaakt met Hallo StorageEncrption(1) optie opgenomen in de aanvraagtekst Hallo.

**HTTP-antwoord**

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

### <a name="create-hello-ingestmanifestassets"></a>Hallo IngestManifestAssets maken
IngestManifestAssets vertegenwoordigen activa in een IngestManifest die worden gebruikt met het opnemen van grote hoeveelheden. Hallo koppelen in feite Hallo asset toohello manifest. Azure Media Services bestandswijzigingsmeldingscontrole intern uploaden Hallo-bestand op basis van IngestManifestFiles verzameling die is gekoppeld toohello IngestManifestAsset. Wanneer deze bestanden zijn geüpload, is Hallo asset voltooid. U kunt een nieuwe IngestManifestAsset maken met een HTTP POST-aanvraag. In de aanvraagtekst hello, omvatten Hallo IngestManifest-Id en Hallo activa-Id die Hallo IngestManifestAsset samen moeten worden gekoppeld voor het opnemen van grote hoeveelheden.

**HTTP-antwoord**

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


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Hallo IngestManifestFiles voor elk activum maken
Een IngestManifestFile vertegenwoordigt een werkelijke video of audio blob-object dat wordt geüpload als onderdeel van het opnemen van grote hoeveelheden voor een asset. Versleuteling gerelateerd eigenschappen zijn niet vereist tenzij Hallo asset een versleutelingsoptie wordt gebruikt. Hallo-voorbeeld gebruikt in deze sectie wordt gedemonstreerd StorageEncryption maken van een IngestManifestFile die worden gebruikt voor Hallo die Asset eerder hebt gemaakt.

**HTTP-antwoord**

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

### <a name="upload-hello-files-tooblob-storage"></a>Hallo bestanden tooBlob opslag uploaden
U kunt een clienttoepassing hoge snelheid kunnen uploaden Hallo asset bestanden toohello blob storage-container door Hallo BlobStorageUriForUpload eigenschap Hallo IngestManifest opgegeven Uri gebruiken. Een opmerkelijke hoge snelheid uploaden service [Aspera On Demand voor Azure-toepassing](http://go.microsoft.com/fwlink/?LinkId=272001).

### <a name="monitor-bulk-ingest-progress"></a>Monitor bulksgewijs voortgang opnemen
U kunt voortgang Hallo van Bulksgewijze bewerkingen voor een IngestManifest door Hallo statistieken eigenschap Hallo IngestManifest opnemen. Of eigenschap een complex type is [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). toopoll hello statistieken-eigenschap verzenden van een HTTP GET-aanvraag doorgeven Hallo IngestManifest-id.

## <a name="create-contentkeys-used-for-encryption"></a>ContentKeys gebruikt voor versleuteling maken
Als uw asset kan versleuteling gebruiken wilt, moet u Hallo ContentKey toobe gebruikt voor versleuteling voordat u Hallo assetbestanden maken. Storage Encryption moeten hello volgende eigenschappen worden opgenomen in de aanvraagtekst Hallo.

| De eigenschap body aanvraag | Beschrijving |
| --- | --- |
| Id |Hallo ContentKey-Id die we genereren onszelf met behulp van de volgende Hallo-indeling, ' nb:kid:UUID:<NEW GUID>'. |
| ContentKeyType |Dit is Hallo inhoudtype belangrijke als een geheel getal voor deze sleutel. Hallo waarde 1 voor versleuteling van opslag doorgegeven. |
| EncryptedContentKey |We maken een nieuwe inhoud sleutelwaarde die een (32 byte) 256-bits waarde. Hallo sleutel is gecodeerd met Hallo opslag versleuteling x.509-certificaat dat we uit Microsoft Azure Media Services ophalen door het uitvoeren van een HTTP GET-aanvraag voor Hallo GetProtectionKeyId en GetProtectionKey methoden. |
| ProtectionKeyId |Dit is protection sleutel-id voor Hallo opslag versleuteling X.509-certificaat dat gebruikt tooencrypt is Hallo onze inhoudssleutel. |
| ProtectionKeyType |Dit is Hallo versleutelingstype voor Hallo beveiliging sleutel die gebruikt tooencrypt hello inhoudssleutel is. Deze waarde is StorageEncryption(1) in ons voorbeeld. |
| Controlesom |Hallo MD5 berekende controlesom voor Hallo inhoudssleutel. Deze wordt berekend door Hallo inhoud Id met Hallo inhoudssleutel te versleutelen. Hallo voorbeeldcode laat zien hoe toocalculate Hallo controlesom. |

**HTTP-antwoord**

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

### <a name="link-hello-contentkey-toohello-asset"></a>Hallo ContentKey toohello Asset koppelen
Hallo ContentKey is gekoppeld tooone of meer elementen door een HTTP POST-aanvraag te verzenden. Hallo is volgende aanvraag een voorbeeld toolink Hallo voorbeeld ContentKey toohello voorbeeld actief op-id.

**HTTP-antwoord**

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

**HTTP-antwoord**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Volgende stappen

U kunt nu de geüploade assets coderen. Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.

U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen. Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

