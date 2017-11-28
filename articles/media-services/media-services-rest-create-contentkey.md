---
title: inhoud sleutels met REST aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate inhoud sleutels die veilige bieden toegang tot tooAssets.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95e9322b-168e-4a9d-8d5d-d7c946103745
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: cb3b74bdb72c43ab5b375c0376b6704f4a93bb8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="4ca67-103">Inhoud sleutels met REST maken</span><span class="sxs-lookup"><span data-stu-id="4ca67-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ca67-104">REST</span><span class="sxs-lookup"><span data-stu-id="4ca67-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="4ca67-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4ca67-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="4ca67-106">Media Services kunt u nieuwe toocreate en versleutelde activa leveren.</span><span class="sxs-lookup"><span data-stu-id="4ca67-106">Media Services enables you toocreate new and deliver encrypted assets.</span></span> <span data-ttu-id="4ca67-107">Een **ContentKey** biedt veilige toegang tooyour **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="4ca67-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="4ca67-108">Wanneer u een nieuwe asset maken (bijvoorbeeld voordat u [bestanden uploaden](media-services-rest-upload-files.md)), kunt u Hallo versleutelingsopties te volgen: **StorageEncrypted**, **CommonEncryptionProtected**, of **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="4ca67-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="4ca67-109">Als u activa tooyour clients leveren, kunt u [configureren voor de activa toobe dynamisch worden versleuteld](media-services-rest-configure-asset-delivery-policy.md) met een Hallo na twee versleutelingen: **DynamicEnvelopeEncryption** of  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="4ca67-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="4ca67-110">Versleutelde activa hebben die zijn gekoppeld aan toobe **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="4ca67-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="4ca67-111">Dit artikel wordt beschreven hoe toocreate een inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="4ca67-111">This article describes how toocreate a content key.</span></span>

<span data-ttu-id="4ca67-112">Hallo vindt hieronder u algemene stappen voor het genereren van inhoud sleutels die u wilt koppelen aan de activa die u toobe versleuteld wilt.</span><span class="sxs-lookup"><span data-stu-id="4ca67-112">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="4ca67-113">Willekeurig genereren een 16 bytes AES-sleutel (voor algemene en envelop versleuteling) of een 32-byte-AES-sleutel (voor versleuteling van opslag).</span><span class="sxs-lookup"><span data-stu-id="4ca67-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="4ca67-114">Dit is de inhoudssleutel Hallo voor uw asset, wat betekent alle bestanden die zijn gekoppeld dat met dat actief wordt moet toouse Hallo dezelfde inhoudssleutel tijdens het ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="4ca67-114">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="4ca67-115">Hallo aanroepen [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) en [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methoden tooget Hallo juist X.509-certificaat dat moet worden gebruikt tooencrypt de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="4ca67-115">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="4ca67-116">Codeer uw inhoud sleutel met de openbare sleutel Hallo Hallo X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="4ca67-116">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="4ca67-117">Media Services .NET SDK gebruikmaakt van RSA met OAEP bij het uitvoeren van Hallo-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="4ca67-117">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="4ca67-118">U ziet een voorbeeld in Hallo [EncryptSymmetricKeyData functie](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="4ca67-118">You can see an example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="4ca67-119">Een controlesomwaarde (gebaseerd op Hallo PlayReady AES-sleutels controlesom algoritme) berekend met behulp van Hallo sleutel-id en een inhoudssleutel maken.</span><span class="sxs-lookup"><span data-stu-id="4ca67-119">Create a checksum value (based on hello PlayReady AES key checksum algorithm) calculated using hello key identifier and content key.</span></span> <span data-ttu-id="4ca67-120">Zie voor meer informatie 'PlayReady AES controlesom sleutelalgoritme' sectie Hallo PlayReady-Header Object document Hallo zich [hier](http://www.microsoft.com/playready/documents/).</span><span class="sxs-lookup"><span data-stu-id="4ca67-120">For more information, see hello “PlayReady AES Key Checksum Algorithm” section of hello PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="4ca67-121">Hallo Hier volgt een voorbeeld van een .NET die wordt berekend met Hallo GUID deel van sleutel-id van Hallo Hallo-controlesom en Hallo inhoudssleutel wissen.</span><span class="sxs-lookup"><span data-stu-id="4ca67-121">hello following is a .NET example that calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

         public static string CalculateChecksum(byte[] contentKey, Guid keyId)
         {

            byte[] array = null;
            using (AesCryptoServiceProvider aesCryptoServiceProvider = new AesCryptoServiceProvider())
            {
                aesCryptoServiceProvider.Mode = CipherMode.ECB;
                aesCryptoServiceProvider.Key = contentKey;
                aesCryptoServiceProvider.Padding = PaddingMode.None;
                ICryptoTransform cryptoTransform = aesCryptoServiceProvider.CreateEncryptor();
                array = new byte[16];
                cryptoTransform.TransformBlock(keyId.ToByteArray(), 0, 16, array, 0);
            }
            byte[] array2 = new byte[8];
            Array.Copy(array, array2, 8);
            return Convert.ToBase64String(array2);
         }
5. <span data-ttu-id="4ca67-122">Hallo inhoudssleutel maken met Hallo **EncryptedContentKey** (geconverteerd toobase64-gecodeerde tekenreeks), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, en **controlesom** waarden die u in de vorige stappen hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4ca67-122">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="4ca67-123">Koppelen Hallo **ContentKey** entiteit met uw **Asset** entiteit via Hallo $links bewerking.</span><span class="sxs-lookup"><span data-stu-id="4ca67-123">Associate hello **ContentKey** entity with your **Asset** entity through hello $links operation.</span></span>

<span data-ttu-id="4ca67-124">Houd er rekening mee dat in dit onderwerp niet weergegeven wordt hoe toogenerate AES-sleutel Hallo sleutel te versleutelen en Hallo controlesom berekenen.</span><span class="sxs-lookup"><span data-stu-id="4ca67-124">Note that this topic does not show how toogenerate an AES key, encrypt hello key, and calculate hello checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="4ca67-125">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4ca67-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="4ca67-126">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4ca67-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="4ca67-127">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="4ca67-127">Connect tooMedia Services</span></span>

<span data-ttu-id="4ca67-128">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4ca67-128">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="4ca67-129">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4ca67-129">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="4ca67-130">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="4ca67-130">You must make subsequent calls toohello new URI.</span></span>

## <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="4ca67-131">Hallo ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="4ca67-131">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="4ca67-132">Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo ProtectionKeyId, een certificaatvingerafdruk voor Hallo certificaat, moet u bij het versleutelen van uw inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="4ca67-132">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="4ca67-133">Voer deze stap toomake zeker dat u al Hallo geschikt certificaat op uw computer hebt.</span><span class="sxs-lookup"><span data-stu-id="4ca67-133">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="4ca67-134">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="4ca67-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="4ca67-135">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="4ca67-135">Response:</span></span>

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

## <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="4ca67-136">Hallo ProtectionKey voor Hallo ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="4ca67-136">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="4ca67-137">Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo x.509-certificaat met behulp van Hallo ProtectionKeyId u hebt ontvangen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ca67-137">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="4ca67-138">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="4ca67-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="4ca67-139">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="4ca67-139">Response:</span></span>

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

## <a name="create-hello-contentkey"></a><span data-ttu-id="4ca67-140">Hallo ContentKey maken</span><span class="sxs-lookup"><span data-stu-id="4ca67-140">Create hello ContentKey</span></span>
<span data-ttu-id="4ca67-141">Nadat u hebt opgehaald Hallo X.509-certificaat en de openbare sleutel tooencrypt uw inhoud sleutel gebruikt, maakt u een **ContentKey** entiteit en stel de eigenschap dienovereenkomstig waarden.</span><span class="sxs-lookup"><span data-stu-id="4ca67-141">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="4ca67-142">Hallo-waarden moet in te stellen wanneer inhoud sleutel is van het type Hallo Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="4ca67-142">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="4ca67-143">Kies een van de volgende waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ca67-143">Choose from one of hello following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }


<span data-ttu-id="4ca67-144">Hallo volgende voorbeeld wordt getoond hoe toocreate een **ContentKey** met een **ContentKeyType** instellen voor versleuteling van opslag ('1') en Hallo **ProtectionKeyType** instellen te "0" tooindicate die Hallo beveiliging sleutel-Id is de vingerafdruk van Hallo x.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="4ca67-144">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="4ca67-145">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="4ca67-145">Request</span></span>

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


<span data-ttu-id="4ca67-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="4ca67-146">Response:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="4ca67-147">Hallo ContentKey koppelen aan een Asset</span><span class="sxs-lookup"><span data-stu-id="4ca67-147">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="4ca67-148">Na het maken van Hallo ContentKey koppelen aan uw Asset Hallo $links bewerking te gebruiken, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4ca67-148">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="4ca67-149">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="4ca67-149">Request:</span></span>

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

<span data-ttu-id="4ca67-150">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="4ca67-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="4ca67-151">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="4ca67-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4ca67-152">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="4ca67-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

