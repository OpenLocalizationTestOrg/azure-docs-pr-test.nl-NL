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
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="7a138-103">Versleutelen van uw inhoud met versleuteling van opslag</span><span class="sxs-lookup"><span data-stu-id="7a138-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="7a138-104">Het is raadzaam tooencrypt inhoud lokaal met AES-256-bits codering en upload het tooAzure opslag waar deze wordt opgeslagen in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7a138-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="7a138-105">Dit artikel geeft een overzicht van de versleuteling van opslag AMS en ziet u hoe tooupload Hallo opslag versleutelde inhoud:</span><span class="sxs-lookup"><span data-stu-id="7a138-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="7a138-106">Maak een inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-106">Create a content key.</span></span>
* <span data-ttu-id="7a138-107">Maak een Asset.</span><span class="sxs-lookup"><span data-stu-id="7a138-107">Create an Asset.</span></span> <span data-ttu-id="7a138-108">Hallo AssetCreationOption tooStorageEncryption ingesteld bij het maken van Hallo Asset.</span><span class="sxs-lookup"><span data-stu-id="7a138-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="7a138-109">Versleutelde activa hebben toobe die zijn gekoppeld aan inhoud sleutels.</span><span class="sxs-lookup"><span data-stu-id="7a138-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="7a138-110">Koppeling Hallo inhoud sleutel toohello asset.</span><span class="sxs-lookup"><span data-stu-id="7a138-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="7a138-111">Stel Hallo versleuteling gerelateerde parameters op Hallo AssetFile entiteiten.</span><span class="sxs-lookup"><span data-stu-id="7a138-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="7a138-112">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="7a138-112">Considerations</span></span> 

<span data-ttu-id="7a138-113">Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren.</span><span class="sxs-lookup"><span data-stu-id="7a138-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="7a138-114">Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor.</span><span class="sxs-lookup"><span data-stu-id="7a138-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="7a138-115">Zie voor meer informatie [Asset leveringsbeleid configureren](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7a138-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="7a138-116">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7a138-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7a138-117">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7a138-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="7a138-118">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="7a138-118">Connect tooMedia Services</span></span>

<span data-ttu-id="7a138-119">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7a138-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="7a138-120">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a138-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7a138-121">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="7a138-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="7a138-122">Overzicht van de Storage-versleuteling</span><span class="sxs-lookup"><span data-stu-id="7a138-122">Storage encryption overview</span></span>
<span data-ttu-id="7a138-123">versleuteling van opslag Hallo AMS geldt **AES CTR** modus versleuteling toohello hele bestand.</span><span class="sxs-lookup"><span data-stu-id="7a138-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="7a138-124">AES-CTR modus is een blokcodering versleutelen van willekeurige lengtegegevens zonder dat nodig is voor de opvulling.</span><span class="sxs-lookup"><span data-stu-id="7a138-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="7a138-125">Dit werkt door een teller blok met Hallo AES-algoritme en vervolgens XOR ing Hallo uitvoer van AES met Hallo gegevens tooencrypt te versleutelen of ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="7a138-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="7a138-126">Hallo prestatiemeteritem dat wordt gebruikt door het Hallo-waarde van Hallo InitializationVector toobytes 0 too7 van Hallo itemwaarde kopiëren is samengesteld en 8 bytes too15 van Hallo itemwaarde toozero zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7a138-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="7a138-127">Van Hallo 16 bytes teller blok, 8 bytes too15 (dat wil zeggen Hallo minst significante bytes) worden gebruikt wanneer er een eenvoudige 64-bits geheel getal zonder teken die wordt verhoogd met één voor elke volgende blok van gegevens die worden verwerkt en wordt bewaard in de bytevolgorde netwerk.</span><span class="sxs-lookup"><span data-stu-id="7a138-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="7a138-128">Let op: als dit geheel getal Hallo maximumwaarde (0xFFFFFFFFFFFFFFFF bereikt) deze vervolgens oplopend in stappen stelt Hallo blok teller toozero (8 bytes too15) zonder Hallo andere 64-bits van Hallo teller (dat wil zeggen 0 bytes too7).</span><span class="sxs-lookup"><span data-stu-id="7a138-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="7a138-129">Hello InitializationVector waarde voor een opgegeven sleutel-id voor elke inhoudssleutel uniek zijn voor elk bestand moeten in de volgorde toomaintain Hallo beveiliging Hallo AES CTR modus versleuteling, en bestanden moet minder zijn dan 2 ^ 64 blokken in lengte.</span><span class="sxs-lookup"><span data-stu-id="7a138-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="7a138-130">Dit is tooensure die een waarde van het prestatiemeteritem nooit is opnieuw met een opgegeven sleutel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a138-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="7a138-131">Zie voor meer informatie over Hallo CTR modus [deze wikipagina](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Hallo term 'Nonce' in plaats van 'InitializationVector' hello wiki-artikel gebruikt).</span><span class="sxs-lookup"><span data-stu-id="7a138-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="7a138-132">Gebruik **Opslagversleuteling** tooencrypt versleutelde inhoud lokaal met AES-256-bits codering en upload het tooAzure opslag wordt bewaard in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7a138-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="7a138-133">Automatisch worden beveiligd met storage encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="7a138-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="7a138-134">Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest.</span><span class="sxs-lookup"><span data-stu-id="7a138-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="7a138-135">In de volgorde toodeliver een gecodeerde asset opslag, moet u beleid voor de levering van Hallo actief configureren zodat Media Services weet hoe u toodeliver uw inhoud wilt.</span><span class="sxs-lookup"><span data-stu-id="7a138-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="7a138-136">Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid (bijvoorbeeld, AES, common encryption of er wordt geen versleuteling).</span><span class="sxs-lookup"><span data-stu-id="7a138-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="7a138-137">ContentKeys gebruikt voor versleuteling maken</span><span class="sxs-lookup"><span data-stu-id="7a138-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="7a138-138">Versleutelde activa hebben toobe die zijn gekoppeld aan de versleutelingssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="7a138-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="7a138-139">Hallo inhoud sleutel toobe gebruikt voor versleuteling voordat Hallo assetbestanden maken, moet u maken.</span><span class="sxs-lookup"><span data-stu-id="7a138-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="7a138-140">Deze sectie wordt beschreven hoe toocreate een inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="7a138-141">Hallo vindt hieronder u algemene stappen voor het genereren van inhoud sleutels die u wilt koppelen aan de activa die u toobe versleuteld wilt.</span><span class="sxs-lookup"><span data-stu-id="7a138-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="7a138-142">Storage Encryption willekeurig een 32-byte AES-sleutel genereren.</span><span class="sxs-lookup"><span data-stu-id="7a138-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="7a138-143">Dit is de inhoudssleutel Hallo voor uw asset, wat betekent alle bestanden die zijn gekoppeld dat met dat actief wordt moet toouse Hallo dezelfde inhoudssleutel tijdens het ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="7a138-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="7a138-144">Hallo aanroepen [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) en [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methoden tooget Hallo juist X.509-certificaat dat moet worden gebruikt tooencrypt de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="7a138-145">Codeer uw inhoud sleutel met de openbare sleutel Hallo Hallo X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="7a138-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="7a138-146">Media Services .NET SDK gebruikmaakt van RSA met OAEP bij het uitvoeren van Hallo-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="7a138-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="7a138-147">U ziet een voorbeeld van een .NET in Hallo [EncryptSymmetricKeyData functie](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="7a138-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="7a138-148">Maak een controlesomwaarde berekend met behulp van Hallo sleutel-id en de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="7a138-149">.NET-voorbeeld te volgen Hallo berekent Hallo controlesom met Hallo GUID deel van Hallo sleutel-id en Hallo inhoudssleutel wissen.</span><span class="sxs-lookup"><span data-stu-id="7a138-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

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

1. <span data-ttu-id="7a138-150">Hallo inhoudssleutel maken met Hallo **EncryptedContentKey** (geconverteerd toobase64-gecodeerde tekenreeks), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, en **controlesom** waarden die u in de vorige stappen hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7a138-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="7a138-151">Storage Encryption moeten hello volgende eigenschappen worden opgenomen in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a138-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="7a138-152">De eigenschap body aanvraag</span><span class="sxs-lookup"><span data-stu-id="7a138-152">Request body property</span></span>    | <span data-ttu-id="7a138-153">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7a138-153">Description</span></span>
    ---|---
    <span data-ttu-id="7a138-154">Id</span><span class="sxs-lookup"><span data-stu-id="7a138-154">Id</span></span> | <span data-ttu-id="7a138-155">Hallo ContentKey-Id die we genereren onszelf met behulp van de volgende Hallo-indeling, ' nb:kid:UUID:<NEW GUID>'.</span><span class="sxs-lookup"><span data-stu-id="7a138-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="7a138-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="7a138-156">ContentKeyType</span></span> | <span data-ttu-id="7a138-157">Dit is Hallo inhoudtype belangrijke als een geheel getal voor deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="7a138-158">Hallo waarde 1 voor versleuteling van opslag doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="7a138-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="7a138-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="7a138-159">EncryptedContentKey</span></span> | <span data-ttu-id="7a138-160">We maken een nieuwe inhoud sleutelwaarde die een (32 byte) 256-bits waarde.</span><span class="sxs-lookup"><span data-stu-id="7a138-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="7a138-161">Hallo sleutel is gecodeerd met Hallo opslag versleuteling x.509-certificaat dat we uit Microsoft Azure Media Services ophalen door het uitvoeren van een HTTP GET-aanvraag voor Hallo GetProtectionKeyId en GetProtectionKey methoden.</span><span class="sxs-lookup"><span data-stu-id="7a138-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="7a138-162">Zie bijvoorbeeld Hallo .NET-code te volgen: Hallo **EncryptSymmetricKeyData** methode gedefinieerd [hier](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="7a138-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="7a138-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="7a138-163">ProtectionKeyId</span></span> | <span data-ttu-id="7a138-164">Dit is protection sleutel-id voor Hallo opslag versleuteling X.509-certificaat dat gebruikt tooencrypt is Hallo onze inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="7a138-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="7a138-165">ProtectionKeyType</span></span> | <span data-ttu-id="7a138-166">Dit is Hallo versleutelingstype voor Hallo beveiliging sleutel die gebruikt tooencrypt hello inhoudssleutel is.</span><span class="sxs-lookup"><span data-stu-id="7a138-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="7a138-167">Deze waarde is StorageEncryption(1) in ons voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7a138-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="7a138-168">Controlesom</span><span class="sxs-lookup"><span data-stu-id="7a138-168">Checksum</span></span> |<span data-ttu-id="7a138-169">Hallo MD5 berekende controlesom voor Hallo inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="7a138-170">Deze wordt berekend door Hallo inhoud Id met Hallo inhoudssleutel te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="7a138-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="7a138-171">Hallo voorbeeldcode laat zien hoe toocalculate Hallo controlesom.</span><span class="sxs-lookup"><span data-stu-id="7a138-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="7a138-172">Hallo ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="7a138-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="7a138-173">Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo ProtectionKeyId, een certificaatvingerafdruk voor Hallo certificaat, moet u bij het versleutelen van uw inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="7a138-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="7a138-174">Voer deze stap toomake zeker dat u al Hallo geschikt certificaat op uw computer hebt.</span><span class="sxs-lookup"><span data-stu-id="7a138-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="7a138-175">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="7a138-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="7a138-176">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="7a138-176">Response:</span></span>

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="7a138-177">Hallo ProtectionKey voor Hallo ProtectionKeyId ophalen</span><span class="sxs-lookup"><span data-stu-id="7a138-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="7a138-178">Hallo volgende voorbeeld ziet u hoe tooretrieve Hallo x.509-certificaat met behulp van Hallo ProtectionKeyId u hebt ontvangen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a138-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="7a138-179">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="7a138-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="7a138-180">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="7a138-180">Response:</span></span>

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

### <a name="create-hello-content-key"></a><span data-ttu-id="7a138-181">Hallo inhoudssleutel maken</span><span class="sxs-lookup"><span data-stu-id="7a138-181">Create hello content key</span></span>
<span data-ttu-id="7a138-182">Nadat u hebt opgehaald Hallo X.509-certificaat en de openbare sleutel tooencrypt uw inhoud sleutel gebruikt, maakt u een **ContentKey** entiteit en stel de eigenschap dienovereenkomstig waarden.</span><span class="sxs-lookup"><span data-stu-id="7a138-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="7a138-183">Hallo-waarden moet in te stellen wanneer inhoud sleutel is van het type Hallo Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7a138-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="7a138-184">Hallo-waarde is in geval van een versleuteling van opslag hello, '1'.</span><span class="sxs-lookup"><span data-stu-id="7a138-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="7a138-185">Hallo volgende voorbeeld wordt getoond hoe toocreate een **ContentKey** met een **ContentKeyType** instellen voor versleuteling van opslag ('1') en Hallo **ProtectionKeyType** instellen te "0" tooindicate die Hallo beveiliging sleutel-Id is de vingerafdruk van Hallo x.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="7a138-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="7a138-186">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="7a138-186">Request</span></span>

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

<span data-ttu-id="7a138-187">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="7a138-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="7a138-188">Maak een asset</span><span class="sxs-lookup"><span data-stu-id="7a138-188">Create an asset</span></span>
<span data-ttu-id="7a138-189">Hallo volgende voorbeeld wordt getoond hoe toocreate een asset.</span><span class="sxs-lookup"><span data-stu-id="7a138-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="7a138-190">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="7a138-190">**HTTP Request**</span></span>

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

<span data-ttu-id="7a138-191">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="7a138-191">**HTTP Response**</span></span>

<span data-ttu-id="7a138-192">Als dit lukt, wordt de volgende Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7a138-192">If successful, hello following is returned:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="7a138-193">Hallo ContentKey koppelen aan een Asset</span><span class="sxs-lookup"><span data-stu-id="7a138-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="7a138-194">Na het maken van Hallo ContentKey koppelen aan uw Asset Hallo $links bewerking te gebruiken, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a138-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="7a138-195">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="7a138-195">Request:</span></span>

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

<span data-ttu-id="7a138-196">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="7a138-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="7a138-197">Een AssetFile maken</span><span class="sxs-lookup"><span data-stu-id="7a138-197">Create an AssetFile</span></span>
<span data-ttu-id="7a138-198">Hallo [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entiteit vertegenwoordigt een video of audio-bestand dat is opgeslagen in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="7a138-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="7a138-199">Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of meer assetbestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="7a138-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="7a138-200">Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.</span><span class="sxs-lookup"><span data-stu-id="7a138-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="7a138-201">Houd er rekening mee dat Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten.</span><span class="sxs-lookup"><span data-stu-id="7a138-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="7a138-202">Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.</span><span class="sxs-lookup"><span data-stu-id="7a138-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="7a138-203">Nadat u uw digitale media-bestand naar een blobcontainer uploadt, gaat u Hallo **samenvoegen** HTTP-aanvraag tooupdate hello AssetFile met informatie over uw mediabestand (niet weergegeven in dit onderwerp).</span><span class="sxs-lookup"><span data-stu-id="7a138-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="7a138-204">**HTTP-aanvraag**</span><span class="sxs-lookup"><span data-stu-id="7a138-204">**HTTP Request**</span></span>

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

<span data-ttu-id="7a138-205">**HTTP-antwoord**</span><span class="sxs-lookup"><span data-stu-id="7a138-205">**HTTP Response**</span></span>

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
