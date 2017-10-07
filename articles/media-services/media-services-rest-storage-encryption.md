---
title: aaaEncrypting uw inhoud met storage encryption met AMS REST-API
description: Meer informatie over hoe tooencrypt uw inhoud met storage encryption met AMS REST-API's.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>Versleutelen van uw inhoud met versleuteling van opslag

Het is raadzaam tooencrypt inhoud lokaal met AES-256-bits codering en upload het tooAzure opslag waar deze wordt opgeslagen in rust versleuteld.

Dit artikel geeft een overzicht van de versleuteling van opslag AMS en ziet u hoe tooupload Hallo opslag versleutelde inhoud:

* Maak een inhoudssleutel.
* Maak een Asset. Hallo AssetCreationOption tooStorageEncryption ingesteld bij het maken van Hallo Asset.
  
     Versleutelde activa hebben toobe die zijn gekoppeld aan inhoud sleutels.
* Koppeling Hallo inhoud sleutel toohello asset.  
* Stel Hallo versleuteling gerelateerde parameters op Hallo AssetFile entiteiten.

## <a name="considerations"></a>Overwegingen 

Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor. Zie voor meer informatie [Asset leveringsbeleid configureren](media-services-rest-configure-asset-delivery-policy.md).

Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen. Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>Verbinding maken met tooMedia Services

Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.

## <a name="storage-encryption-overview"></a>Overzicht van de Storage-versleuteling
versleuteling van opslag Hallo AMS geldt **AES CTR** modus versleuteling toohello hele bestand.  AES-CTR modus is een blokcodering versleutelen van willekeurige lengtegegevens zonder dat nodig is voor de opvulling. Dit werkt door een teller blok met Hallo AES-algoritme en vervolgens XOR ing Hallo uitvoer van AES met Hallo gegevens tooencrypt te versleutelen of ontsleutelen.  Hallo prestatiemeteritem dat wordt gebruikt door het Hallo-waarde van Hallo InitializationVector toobytes 0 too7 van Hallo itemwaarde kopiëren is samengesteld en 8 bytes too15 van Hallo itemwaarde toozero zijn ingesteld. Van Hallo 16 bytes teller blok, 8 bytes too15 (dat wil zeggen Hallo minst significante bytes) worden gebruikt wanneer er een eenvoudige 64-bits geheel getal zonder teken die wordt verhoogd met één voor elke volgende blok van gegevens die worden verwerkt en wordt bewaard in de bytevolgorde netwerk. Let op: als dit geheel getal Hallo maximumwaarde (0xFFFFFFFFFFFFFFFF bereikt) deze vervolgens oplopend in stappen stelt Hallo blok teller toozero (8 bytes too15) zonder Hallo andere 64-bits van Hallo teller (dat wil zeggen 0 bytes too7).   Hello InitializationVector waarde voor een opgegeven sleutel-id voor elke inhoudssleutel uniek zijn voor elk bestand moeten in de volgorde toomaintain Hallo beveiliging Hallo AES CTR modus versleuteling, en bestanden moet minder zijn dan 2 ^ 64 blokken in lengte.  Dit is tooensure die een waarde van het prestatiemeteritem nooit is opnieuw met een opgegeven sleutel wordt gebruikt. Zie voor meer informatie over Hallo CTR modus [deze wikipagina](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Hallo term 'Nonce' in plaats van 'InitializationVector' hello wiki-artikel gebruikt).

Gebruik **Opslagversleuteling** tooencrypt versleutelde inhoud lokaal met AES-256-bits codering en upload het tooAzure opslag wordt bewaard in rust versleuteld. Automatisch worden beveiligd met storage encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset. Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest.

In de volgorde toodeliver een gecodeerde asset opslag, moet u beleid voor de levering van Hallo actief configureren zodat Media Services weet hoe u toodeliver uw inhoud wilt. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid (bijvoorbeeld, AES, common encryption of er wordt geen versleuteling).

## <a name="create-contentkeys-used-for-encryption"></a>ContentKeys gebruikt voor versleuteling maken
Versleutelde activa hebben toobe die zijn gekoppeld aan de versleutelingssleutel voor opslag. Hallo inhoud sleutel toobe gebruikt voor versleuteling voordat Hallo assetbestanden maken, moet u maken. Deze sectie wordt beschreven hoe toocreate een inhoudssleutel.

Hallo vindt hieronder u algemene stappen voor het genereren van inhoud sleutels die u wilt koppelen aan de activa die u toobe versleuteld wilt. 

1. Storage Encryption willekeurig een 32-byte AES-sleutel genereren. 
   
    Dit is de inhoudssleutel Hallo voor uw asset, wat betekent alle bestanden die zijn gekoppeld dat met dat actief wordt moet toouse Hallo dezelfde inhoudssleutel tijdens het ontsleutelen. 
2. Hallo aanroepen [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) en [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methoden tooget Hallo juist X.509-certificaat dat moet worden gebruikt tooencrypt de inhoudssleutel.
3. Codeer uw inhoud sleutel met de openbare sleutel Hallo Hallo X.509-certificaat. 
   
   Media Services .NET SDK gebruikmaakt van RSA met OAEP bij het uitvoeren van Hallo-versleuteling.  U ziet een voorbeeld van een .NET in Hallo [EncryptSymmetricKeyData functie](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Maak een controlesomwaarde berekend met behulp van Hallo sleutel-id en de inhoudssleutel. .NET-voorbeeld te volgen Hallo berekent Hallo controlesom met Hallo GUID deel van Hallo sleutel-id en Hallo inhoudssleutel wissen.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Hallo inhoudssleutel maken met Hallo **EncryptedContentKey** (geconverteerd toobase64-gecodeerde tekenreeks), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, en **controlesom** waarden die u in de vorige stappen hebt ontvangen.

    Storage Encryption moeten hello volgende eigenschappen worden opgenomen in de aanvraagtekst Hallo.

    De eigenschap body aanvraag    | Beschrijving
    ---|---
    Id | Hallo ContentKey-Id die we genereren onszelf met behulp van de volgende Hallo-indeling, ' nb:kid:UUID:<NEW GUID>'.
    ContentKeyType | Dit is Hallo inhoudtype belangrijke als een geheel getal voor deze sleutel. Hallo waarde 1 voor versleuteling van opslag doorgegeven.
    EncryptedContentKey | We maken een nieuwe inhoud sleutelwaarde die een (32 byte) 256-bits waarde. Hallo sleutel is gecodeerd met Hallo opslag versleuteling x.509-certificaat dat we uit Microsoft Azure Media Services ophalen door het uitvoeren van een HTTP GET-aanvraag voor Hallo GetProtectionKeyId en GetProtectionKey methoden. Zie bijvoorbeeld Hallo .NET-code te volgen: Hallo **EncryptSymmetricKeyData** methode gedefinieerd [hier](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Dit is protection sleutel-id voor Hallo opslag versleuteling X.509-certificaat dat gebruikt tooencrypt is Hallo onze inhoudssleutel.
    ProtectionKeyType | Dit is Hallo versleutelingstype voor Hallo beveiliging sleutel die gebruikt tooencrypt hello inhoudssleutel is. Deze waarde is StorageEncryption(1) in ons voorbeeld.
    Controlesom |Hallo MD5 berekende controlesom voor Hallo inhoudssleutel. Deze wordt berekend door Hallo inhoud Id met Hallo inhoudssleutel te versleutelen. Hallo voorbeeldcode laat zien hoe toocalculate Hallo controlesom.


### <a name="retrieve-hello-protectionkeyid"></a>Hallo ProtectionKeyId ophalen
Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo ProtectionKeyId, een certificaatvingerafdruk voor Hallo certificaat, moet u bij het versleutelen van uw inhoudssleutel. Voer deze stap toomake zeker dat u al Hallo geschikt certificaat op uw computer hebt.

Aanvraag:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Antwoord:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Hallo ProtectionKey voor Hallo ProtectionKeyId ophalen
Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo x.509-certificaat met behulp van Hallo ProtectionKeyId u hebt ontvangen in de vorige stap Hallo.

Aanvraag:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Antwoord:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a>Hallo inhoudssleutel maken
Nadat u hebt opgehaald Hallo X.509-certificaat en de openbare sleutel tooencrypt uw inhoud sleutel gebruikt, maakt u een **ContentKey** entiteit en stel de eigenschap dienovereenkomstig waarden.

Hallo-waarden moet in te stellen wanneer inhoud sleutel is van het type Hallo Hallo maken. Hallo-waarde is in geval van een versleuteling van opslag hello, '1'. 

Hallo volgende voorbeeld wordt getoond hoe toocreate een **ContentKey** met een **ContentKeyType** instellen voor versleuteling van opslag ('1') en Hallo **ProtectionKeyType** instellen te "0" tooindicate die Hallo beveiliging sleutel-Id is de vingerafdruk van Hallo x.509-certificaat.  

Aanvraag

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

Antwoord:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a>Maak een asset
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

    {"Name":"BigBuckBunny" "Options":1}

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
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a>Hallo ContentKey koppelen aan een Asset
Na het maken van Hallo ContentKey koppelen aan uw Asset Hallo $links bewerking te gebruiken, zoals wordt weergegeven in Hallo voorbeeld te volgen:

Aanvraag:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

Antwoord:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Een AssetFile maken
Hallo [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entiteit vertegenwoordigt een video of audio-bestand dat is opgeslagen in een blob-container. Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of meer assetbestanden bevatten. Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.

Houd er rekening mee dat Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten. Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.

Nadat u uw digitale media-bestand naar een blobcontainer uploadt, gaat u Hallo **samenvoegen** HTTP-aanvraag tooupdate hello AssetFile met informatie over uw mediabestand (niet weergegeven in dit onderwerp). 

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
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
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
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
