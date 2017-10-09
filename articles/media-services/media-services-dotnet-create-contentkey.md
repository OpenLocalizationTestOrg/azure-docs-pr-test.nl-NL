---
title: aaaCreate ContentKeys met .NET
description: Meer informatie over hoe toocreate inhoud sleutels die veilige bieden toegang tot tooAssets.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a>ContentKeys maken met .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Media Services kunt u toocreate en versleutelde activa leveren. Een **ContentKey** biedt veilige toegang tooyour **Asset**s. 

Wanneer u een nieuwe asset maken (bijvoorbeeld voordat u [bestanden uploaden](media-services-dotnet-upload-files.md)), kunt u Hallo versleutelingsopties te volgen: **StorageEncrypted**, **CommonEncryptionProtected**, of **EnvelopeEncryptionProtected**. 

Als u activa tooyour clients leveren, kunt u [configureren voor de activa toobe dynamisch worden versleuteld](media-services-dotnet-configure-asset-delivery-policy.md) met een Hallo na twee versleutelingen: **DynamicEnvelopeEncryption** of  **DynamicCommonEncryption**.

Versleutelde activa hebben die zijn gekoppeld aan toobe **ContentKey**s. Dit artikel wordt beschreven hoe toocreate een inhoudssleutel.

> [!NOTE]
> Bij het maken van een nieuwe **StorageEncrypted** met behulp van asset Hallo Media Services .NET SDK hello **ContentKey** automatisch wordt gemaakt en gekoppeld aan Hallo asset.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Hallo-waarden moet in te stellen wanneer een inhoud maken sleutel Hallo inhoudtype belangrijke is. Kies een van de volgende waarden Hallo. 

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

## <a id="envelope_contentkey"></a>Het type envelop ContentKey maken
Hallo maakt volgende codefragment een inhoudssleutel van Hallo envelop versleutelingstype. Vervolgens wordt Hallo sleutel gekoppeld aan de opgegeven asset Hallo.

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

Aanroep

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Het algemene type ContentKey maken
Hallo maakt volgende codefragment een inhoudssleutel van algemene versleutelingstype Hallo. Vervolgens wordt Hallo sleutel gekoppeld aan de opgegeven asset Hallo.

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
Aanroep

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

