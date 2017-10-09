---
title: aaa"uploaden van bestanden naar een Media Services-account met behulp van hello Azure-portal | Microsoft Docs'
description: "Deze zelfstudie leert u Hallo van bestanden zijn geüpload naar een Media Services-account met behulp van hello Azure-portal"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Bestanden uploaden naar een Media Services-account met behulp van hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 


In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset. Hallo Asset kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.) Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.


## <a name="upload-files"></a>Bestanden uploaden

>[!NOTE]
>Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund. Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.
>

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. Op Hallo **instellingen** blade, klikt u op **activa**.
   
    ![Bestanden uploaden](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Klik op Hallo **uploaden** knop.
   
    Hallo **videoasset uploaden** venster wordt weergegeven.
   
   > [!NOTE]
   > Er geldt geen beperking voor de bestandsgrootte.
   > 
   > 
4. Blader toohello gewenste video op uw computer, selecteert u deze en klik op OK.  
   
    Hallo uploaden wordt gestart en u kunt de voortgang Hallo onder Hallo bestandsnaam bekijken.  

Nadat het Hallo uploaden is voltooid, ziet u Hallo nieuwe asset weergegeven in Hallo **activa** venster. 

## <a name="next-steps"></a>Volgende stappen
U kunt nu de geüploade assets coderen. Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.

U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen. Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

