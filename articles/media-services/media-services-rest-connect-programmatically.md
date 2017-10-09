---
title: aaaConnecting tooMedia Services-Account met REST-API | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooconnect tooMedia Services met behulp REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Verbinding maken met tooMedia Services-Account met Media Services REST-API
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Dit onderwerp beschrijft hoe een programmatische verbinding tooMicrosoft Azure Media Services tijdens het programmeren met tooobtain Hallo REST API voor Media Services.

Twee dingen zijn vereist bij het openen van Microsoft Azure Media Services: een toegangstoken die is verstrekt door Azure Access Control-Services (ACS) en het Hallo-URI van Media Services zelf. U kunt een wijze die u wilt dat bij het maken van deze aanvragen, zolang u Geef de juiste headerwaarden hello en in Hallo toegangstoken correct bij het aanroepen van in Media Services gebruiken.

Hallo stappen te volgen beschrijven de meest voorkomende werkstroom Hallo wanneer met behulp van Hallo REST API voor Media Services tooconnect tooMedia Services:

1. Ophalen van een toegangstoken 
2. Verbinding maken met toohello Media Services-URI 
   
   > [!NOTE]
   > Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.
   > U kunt ook een HTTP/1.1 200-antwoord dat Hallo beschrijving van de ODATA-API-metagegevens bevat ontvangen.
   > 
   > 
3. De volgende API-aanroepen na toohello nieuwe URL. 
   
    Bijvoorbeeld, als nadat u hebt geprobeerd tooconnect, u hebt verkregen Hallo volgende:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    U moet de volgende API-aanroepen toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ boeken.

    >[!NOTE]
    >Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

## <a name="access-control-address"></a>Adres Access control
Media Services-adres is https://wamsprodglobal001acs.accesscontrol.windows.net, met uitzondering van China Noord regio, waar deze https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn is.

## <a name="getting-an-access-token"></a>Ophalen van een toegangstoken
tooaccess Media Services rechtstreeks via Hallo REST-API, een toegangstoken ophalen uit ACS en deze gebruiken tijdens elke HTTP-aanvraag die u in Hallo-service aanbrengt. Dit token is vergelijkbaar tooother tokens die worden geleverd door ACS op basis van de toegang tot claims die zijn opgegeven in Hallo-header van een HTTP-aanvraag en met Hallo OAuth-v2-protocol. U hoeft niet alle andere vereiste onderdelen voor tooMedia Services rechtstreeks verbinding te maken.

Hallo volgende voorbeeld ziet Hallo HTTP-aanvraag-header en tooretrieve instantie gebruikt een token.

**Koptekst**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Hoofdtekst**:

U moet tooprove hello client_id en client_secret waarden in de hoofdtekst Hallo van deze aanvraag; client_id en client_secret komen overeen respectievelijk toohello AccountName en AccountKey waarden. Deze waarden worden tooyou geleverd door Media Services bij het instellen van uw account. 

Houd er rekening mee dat Hallo AccountKey voor uw Media Services-account URL-codering moet (Zie [procent codering](http://tools.ietf.org/html/rfc3986#section-2.1) wanneer deze worden gebruikt als Hallo client_secret waarde in het token verzoek om toegang.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Bijvoorbeeld: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hallo volgende voorbeeld ziet Hallo HTTP-antwoord met Hallo access token in Hallo antwoordtekst.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> Het verdient aanbeveling toocache Hallo 'access_token' en 'expires_in' waarden tooan externe opslag. Hallo token gegevens kan later worden opgehaald uit het Hallo-opslag en opnieuw worden gebruikt voor uw Media Services REST API-aanroepen. Dit is vooral nuttig voor scenario's waarbij Hallo token kan veilig worden gedeeld tussen meerdere processen en computers.
> 
> 

Zorg ervoor dat toomonitor Hallo 'expires_in'-waarde van Hallo toegang token en de REST-API-aanroepen bijwerken met nieuwe tokens, indien nodig.

### <a name="connecting-toohello-media-services-uri"></a>Verbinding maken met toohello Media Services-URI
Hallo basis-URI voor Media Services is https://media.windows.net/. U moet eerst verbinding maakt met toothis URI en als u een 301 omleiding terug in het antwoord krijgt, moet u volgende aanroepen toohello nieuwe URI. Gebruik bovendien niet alle logica automatisch omleiden, volgen in uw aanvragen. HTTP-termen en instanties van de aanvraag niet doorgestuurd toohello nieuwe URI.

Houd er rekening mee dat Hallo hoofdmap URI voor het uploaden en downloaden van bestanden van de Asset is https://yourstorageaccount.blob.core.windows.net/ waarbij opslagaccountnaam Hallo Hallo hetzelfde abonnement dat u tijdens de installatie van uw Media Services-account gebruikt.

Hallo volgende voorbeeld ziet u HTTP-aanvraag toohello Media Services hoofdmap URI (https://media.windows.net/). Hallo aanvraag haalt een 301 omleiding terug in het antwoord. Hallo volgend verzoek maakt gebruik van Hallo nieuwe URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**HTTP-aanvraag**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**HTTP-antwoord**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP-aanvraag** (met behulp van nieuwe URI Hallo):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP-antwoord**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Als u eenmaal Hallo nieuwe Hallo URI die de URI die moet worden gebruikt toocommunicate met Media Services. 
> 
> 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

