---
title: Inhoud sleutels maken met REST | Microsoft Docs
description: Informatie over het maken van de inhoud van de sleutels die beveiligde toegang tot bedrijfsmiddelen bieden.
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
ms.openlocfilehash: ece09277d26fafb7c0eebf62730031c4dc01bfe0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="d9f0c-103">Inhoud sleutels met REST maken</span><span class="sxs-lookup"><span data-stu-id="d9f0c-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9f0c-104">REST</span><span class="sxs-lookup"><span data-stu-id="d9f0c-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="d9f0c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d9f0c-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="d9f0c-106">Media Services kunt u nieuwe maken en versleutelde activa leveren.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-106">Media Services enables you to create new and deliver encrypted assets.</span></span> <span data-ttu-id="d9f0c-107">Een **ContentKey** biedt veilige toegang tot uw **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="d9f0c-108">Wanneer u een nieuwe asset maken (bijvoorbeeld voordat u [bestanden uploaden](media-services-rest-upload-files.md)), kunt u de volgende versleutelingsopties: **StorageEncrypted**, **CommonEncryptionProtected**, of **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="d9f0c-109">Als u activa aan uw clients leveren, kunt u [configureren voor bedrijfsmiddelen die dynamisch worden versleuteld](media-services-rest-configure-asset-delivery-policy.md) met een van de volgende twee versleutelingen: **DynamicEnvelopeEncryption** of **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="d9f0c-110">Versleutelde activa hebben moeten worden gekoppeld aan **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="d9f0c-111">In dit artikel wordt beschreven hoe een inhoudssleutel maken.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-111">This article describes how to create a content key.</span></span>

<span data-ttu-id="d9f0c-112">Hieronder vindt u algemene stappen voor het genereren van inhoud sleutels die u wilt koppelen aan de activa die u wilt worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-112">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="d9f0c-113">Willekeurig genereren een 16 bytes AES-sleutel (voor algemene en envelop versleuteling) of een 32-byte-AES-sleutel (voor versleuteling van opslag).</span><span class="sxs-lookup"><span data-stu-id="d9f0c-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="d9f0c-114">Dit is de inhoudssleutel voor uw asset, wat betekent dat alle bestanden die zijn gekoppeld aan dat actief moet dezelfde inhoud sleutel gebruiken tijdens het ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-114">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="d9f0c-115">Roep de [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) en [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methoden voor het ophalen van het juiste X.509-certificaat dat moet worden gebruikt om uw inhoud sleutel te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-115">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="d9f0c-116">Codeer uw inhoud sleutel met de openbare sleutel van het X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-116">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="d9f0c-117">Media Services .NET SDK gebruikmaakt van RSA met OAEP bij het uitvoeren van de codering.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-117">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="d9f0c-118">U ziet een voorbeeld in de [EncryptSymmetricKeyData functie](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="d9f0c-118">You can see an example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="d9f0c-119">Een controlesomwaarde (op basis van het algoritme PlayReady AES-sleutel controlesom) berekend met behulp van de sleutel-id en een inhoudssleutel maken.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-119">Create a checksum value (based on the PlayReady AES key checksum algorithm) calculated using the key identifier and content key.</span></span> <span data-ttu-id="d9f0c-120">Zie voor meer informatie de sectie 'PlayReady AES controlesom sleutelalgoritme' van het Object van de Header PlayReady document zich [hier](http://www.microsoft.com/playready/documents/).</span><span class="sxs-lookup"><span data-stu-id="d9f0c-120">For more information, see the “PlayReady AES Key Checksum Algorithm” section of the PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="d9f0c-121">Hier volgt een voorbeeld van een .NET waarmee de controlesom met de GUID-deel van de sleutel-id en de wissen inhoudssleutel wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-121">The following is a .NET example that calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

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
5. <span data-ttu-id="d9f0c-122">Maak de inhoudssleutel met de **EncryptedContentKey** (geconverteerd naar base64-gecodeerde tekenreeks), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, en **controlesom** waarden die u in de vorige stappen hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-122">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="d9f0c-123">Koppel de **ContentKey** entiteit met uw **Asset** entiteit via de $links-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-123">Associate the **ContentKey** entity with your **Asset** entity through the $links operation.</span></span>

<span data-ttu-id="d9f0c-124">Houd er rekening mee dat in dit onderwerp wordt het AES-sleutel genereren, het versleutelen van de sleutel en het berekenen van de controlesom niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-124">Note that this topic does not show how to generate an AES key, encrypt the key, and calculate the checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="d9f0c-125">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d9f0c-126">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d9f0c-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="d9f0c-127">Verbinding met Media Services maken</span><span class="sxs-lookup"><span data-stu-id="d9f0c-127">Connect to Media Services</span></span>

<span data-ttu-id="d9f0c-128">Zie voor meer informatie over de verbinding maken met de AMS API [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d9f0c-128">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d9f0c-129">Na het correct verbinding maakt met https://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-129">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d9f0c-130">U moet de volgende aanroepen naar de nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-130">You must make subsequent calls to the new URI.</span></span>

## <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="d9f0c-131">De ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="d9f0c-131">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="d9f0c-132">Het volgende voorbeeld laat zien hoe de ProtectionKeyId, de vingerafdruk van een certificaat voor het certificaat dat moet u bij het versleutelen van uw inhoudssleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-132">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="d9f0c-133">Voer deze stap uit om ervoor te zorgen dat u al het juiste certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-133">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="d9f0c-134">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="d9f0c-135">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-135">Response:</span></span>

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

## <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="d9f0c-136">De ProtectionKey voor de ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="d9f0c-136">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="d9f0c-137">Het volgende voorbeeld laat zien hoe voor het ophalen van het X.509-certificaat met behulp van de ProtectionKeyId dat u in de vorige stap hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-137">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="d9f0c-138">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="d9f0c-139">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-139">Response:</span></span>

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

## <a name="create-the-contentkey"></a><span data-ttu-id="d9f0c-140">De ContentKey maken</span><span class="sxs-lookup"><span data-stu-id="d9f0c-140">Create the ContentKey</span></span>
<span data-ttu-id="d9f0c-141">Nadat u hebt opgehaald van het X.509-certificaat en de openbare sleutel voor het versleutelen van uw inhoud sleutel gebruikt, maakt u een **ContentKey** entiteit en stel de eigenschap dienovereenkomstig waarden.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-141">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="d9f0c-142">Een van de waarden die u wanneer instellen moet de inhoud maken sleutel is van het type.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-142">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="d9f0c-143">Kies een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-143">Choose from one of the following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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


<span data-ttu-id="d9f0c-144">Het volgende voorbeeld ziet u het maken van een **ContentKey** met een **ContentKeyType** ingesteld voor de versleuteling van opslag ('1') en de **ProtectionKeyType** ingesteld op '0' om aan te geven dat de sleutel beveiliging Id de vingerafdruk van het X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="d9f0c-144">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="d9f0c-145">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="d9f0c-145">Request</span></span>

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


<span data-ttu-id="d9f0c-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-146">Response:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="d9f0c-147">De ContentKey koppelen aan een Asset</span><span class="sxs-lookup"><span data-stu-id="d9f0c-147">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="d9f0c-148">Na het maken van de ContentKey koppelen aan uw Asset met behulp van de bewerking $links, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-148">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="d9f0c-149">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-149">Request:</span></span>

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

<span data-ttu-id="d9f0c-150">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="d9f0c-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="d9f0c-151">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="d9f0c-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9f0c-152">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d9f0c-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

