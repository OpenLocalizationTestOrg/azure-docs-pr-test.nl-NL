---
title: leveringsbeleid voor aaaConfiguring asset met Media Services REST-API | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooconfigure leveringsbeleid voor verschillende asset met Media Services REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Beleid voor de levering asset configureren
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Als u van plan activa toodeliver dynamisch worden versleuteld bent, stappen een Hallo Hallo Media Services content delivery werkstroom is leveringsbeleid voor assets configureren. Hallo-leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset toobe geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), al dan niet de gewenste toodynamically uw asset coderen en hoe (envelop of common encryption).

Dit onderwerp wordt beschreven waarom en hoe toocreate en beleid voor de levering asset configureren.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 
>
>Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.

U kunt ook verschillende beleidsregels toohello toepassen dezelfde asset. U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth Streaming en AES Envelope versleuteling tooMPEG toepassen DASH- en HLS. Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd. Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd. Vervolgens zijn alle protocollen toegestaan in Hallo wissen.

Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor. Bijvoorbeeld toodeliver uw asset versleuteld met Advanced Encryption Standard (AES) envelop versleutelingssleutel, stelt u het beleidstype hello te**DynamicEnvelopeEncryption**. versleuteling van opslag tooremove en stroom Hallo asset in Hallo wissen, stelt u Hallo beleidstype te**NoDynamicEncryption**. Voorbeelden van hoe tooconfigure deze beleidstypen volgen.

Afhankelijk van hoe u Hallo-leveringsbeleid voor Assets configureren die u zou kunnen toodynamically pakket worden dynamisch versleutelen en stream Hallo streaming protocollen te volgen: Smooth Streaming, HLS, MPEG DASH-streams.

Hallo volgende lijst bevat Hallo opgemaakt toostream Smooth, HLS, DASH te gebruiken.

Smooth Streaming:

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest

HLS:

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Voor instructies over hoe toopublish een asset en bouwen van een streaming-URL, Zie [bouwen van een streaming-URL](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Overwegingen
* U kunt een AssetDeliveryPolicy die zijn gekoppeld aan een asset, terwijl een (streaming) OnDemand-locator voor de activa bestaat niet verwijderen. Hallo-aanbeveling is tooremove Hallo beleid uit Hallo actief voordat Hallo beleid wordt verwijderd.
* Een streaming-locator kan niet worden gemaakt op een versleutelde actief opslag wanneer geen leveringsbeleid voor Assets is ingesteld.  Als Hallo Asset niet opslag versleuteld, kunt Hallo-systeem u een locator en stream Hallo-asset maken in Hallo wissen zonder een leveringsbeleid voor Assets.
* U kunt meerdere asset levering beleidsregels die zijn gekoppeld aan één element hebben maar u kunt alleen eenrichtingssessie toohandle een bepaalde AssetDeliveryProtocol opgeven.  Dit betekent dat als u toolink twee leveringsbeleid die Hallo AssetDeliveryProtocol.SmoothStreaming protocol die resulteren in een fout opgetreden probeert opgeeft omdat Hallo systeem welke niet weet u dat wilt tooapply wanneer een client een Smooth Streaming-aanvraag indient.
* Hebt u een asset met een bestaande streaming-locator, kan u een nieuw beleid toohello activum koppelen, ontkoppelen van een bestaand beleid uit Hallo actief of bijwerken van een leveringsbeleid Hallo asset gekoppeld.  U eerst tooremove Hallo streaming-locator hebben, Hallo beleid aanpassen en streaming-locator Hallo opnieuw maken.  U kunt Hallo dezelfde locatorId wanneer u opnieuw Hallo streaming maakt-locator, maar u moet ervoor zorgen dat niet toe leiden problemen voor clients dat omdat inhoud kan worden in het cachegeheugen van de oorsprong hello of een downstream CDN gebruiken.

>[!NOTE]

>Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen. Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Verbinding maken met tooMedia Services

Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.

## <a name="clear-asset-delivery-policy"></a>Leveringsbeleid voor Assets wissen
### <a id="create_asset_delivery_policy"></a>Leveringsbeleid voor Assets maken
Hallo volgende HTTP-aanvraag maakt een leveringsbeleid asset waarmee toonot toepassen dynamische versleuteling en toodeliver Hallo stream in een van volgende Hallo protocollen: MPEG DASH, HLS en Smooth Streaming-protocollen. 

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.   

Aanvraag:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Antwoord:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Koppeling asset met leveringsbeleid voor Assets
Hallo volgende HTTP-aanvraag koppelingen Hallo opgegeven toohello asset leveringsbeleid voor Assets op.

Aanvraag:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Antwoord:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption-leveringsbeleid voor Assets
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Inhoudssleutel van Hallo EnvelopeEncryption type maken en koppelen toohello asset
Wanneer u het leveringsbeleid DynamicEnvelopeEncryption opgeeft, moet u ervoor dat toolink toomake uw asset tooa-inhoudssleutel Hallo EnvelopeEncryption type. Zie voor meer informatie: [maken van een inhoudssleutel](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Levering-URL ophalen
Get Hallo levering URL voor Hallo opgegeven leveringsmethode van inhoud Hallo-sleutel in de vorige stap Hallo gemaakt. Een client gebruikt Hallo geretourneerd URL toorequest AES-sleutel of een PlayReady-licenties in volgorde tooplayback Hallo beveiligde inhoud.

Hallo type Hallo URL tooget opgeven in de hoofdtekst Hallo van Hallo HTTP-aanvraag. Als u uw inhoud met PlayReady beveiligt aanvragen van een Media Services PlayReady licentie overname URL, met behulp van 1 voor Hallo keyDeliveryType: {'keyDeliveryType': 1}. Als u uw inhoud met Hallo envelop versleuteling beveiligt, een URL voor het belangrijkste aanvragen door op te geven van 2 voor keyDeliveryType: {'keyDeliveryType': 2}.

Aanvraag:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Antwoord:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Leveringsbeleid voor Assets maken
Hallo volgende HTTP-aanvraag maakt Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische versleuteling (**DynamicEnvelopeEncryption**) toohello **HLS**protocol (in dit voorbeeld andere protocollen worden geblokkeerd van streaming). 

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.   

Aanvraag:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Antwoord:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Koppeling asset met leveringsbeleid voor Assets
Zie [koppeling asset met leveringsbeleid voor Assets](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption-leveringsbeleid voor Assets
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Inhoudssleutel van Hallo CommonEncryption type maken en koppelen toohello asset
Wanneer u het leveringsbeleid DynamicCommonEncryption opgeeft, moet u ervoor dat toolink toomake uw asset tooa-inhoudssleutel Hallo CommonEncryption type. Zie voor meer informatie: [maken van een inhoudssleutel](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Levering-URL ophalen
Hallo levering URL voor Hallo PlayReady leveringsmethode van gemaakt in de vorige stap Hallo Hallo-inhoudssleutel niet ophalen. Een client gebruikt Hallo URL toorequest een PlayReady-licenties in volgorde tooplayback Hallo beveiligde inhoud geretourneerd. Zie voor meer informatie [levering-URL ophalen](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Leveringsbeleid voor Assets maken
Hallo volgende HTTP-aanvraag maakt Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocol (in dit voorbeeld andere protocollen worden geblokkeerd van streaming). 

Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.   

Aanvraag:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Als u uw inhoud met Widevine DRM tooprotect wilt, bijwerken Hallo AssetDeliveryConfiguration waarden toouse WidevineLicenseAcquisitionUrl (die Hallo waarde heeft van 7) en geef Hallo-URL van een service voor het leveren van licenties. U kunt Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Bijvoorbeeld: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Bij het versleutelen met Widevine, zou u alleen kunnen toodeliver met STREEPJES zijn. Zorg ervoor dat toospecify streepje (2) in Hallo asset leveringsprotocol.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Koppeling asset met leveringsbeleid voor Assets
Zie [koppeling asset met leveringsbeleid voor Assets](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>Typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Hallo beschrijft volgende enum waarden die u voor Hallo asset leveringsprotocol instellen kunt.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Hallo beschrijft volgende enum waarden die u voor Hallo asset bezorgingstype beleid instellen kunt.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Hallo beschrijft volgende enum waarden kunt u tooconfigure Hallo leveringsmethode van Hallo inhoud sleutel toohello client.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

Hallo na enum beschrijft waarden kunt u tooget specifieke configuratie van tooconfigure sleutels die worden gebruikt voor een leveringsbeleid voor Assets instellen.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

