---
title: aaaUpload bestanden naar een Azure Media Services-account van Azure StorSimple | Microsoft Docs
description: Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager. Hallo artikel bevat ook koppelingen tootutorials die laten hoe u zien gegevens van StorSimple tooextract en upload het als activa tooan Azure Media Services-account.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Bestanden vanuit Azure StorSimple uploaden naar een Azure Media Services-account

Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager. Hallo artikel bevat ook koppelingen tootutorials die laten hoe u zien tooextract gegevens van StorSimple en deze gegevens te uploaden als activa tooan Azure Media Services (AMS)-account.

> 
> [!NOTE]
> Azure StorSimple Data Manager bevindt zich momenteel in Private Preview. 
> 

## <a name="overview"></a>Overzicht

In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset. Hallo Asset kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.) Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) cloudopslag gebruikt als een uitbreiding van Hallo on-premises-oplossing en automatisch gegevens over Hallo lokale opslag en cloud-opslag lagen. Hallo StorSimple-apparaat dedupes en uw gegevens te comprimeren voordat deze toohello cloud waardoor het zeer efficiënte voor het verzenden van grote bestanden toohello cloud worden verzonden. Hallo [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service biedt API's die u tooextract gegevens van StorSimple inschakelen en op te geven als AMS activa.

## <a name="get-started"></a>Aan de slag

1. [Een Media Services-account maken](media-services-portal-create-account.md) waarnaar tootransfer Hallo activa.
2. Aanmelden voor de preview van Data Manager, zoals beschreven in Hallo [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artikel.
3. Maak een StorSimple Data Manager-account.
4. Maak een taak voor gegevenstransformatie die bij uitvoering gegevens extraheert van een StorSimple-apparaat en deze als assets overbrengt naar een AMS-account. 

    Wanneer Hallo-taak gestart wordt, wordt een opslagwachtrij gemaakt. Deze wachtrij wordt gevuld met berichten over getransformeerde blobs wanneer deze gereed zijn. Hallo-naam van deze wachtrij is hetzelfde als de naam van de taakdefinitie Hallo HALLO hallo. U kunt deze wachtrij toodetermine wanneer asset is klaar te maken en de gewenste bewerking toorun voor Media Services voor het aanroepen. Bijvoorbeeld, kunt u deze wachtrij tootrigger een Azure-functie met Hallo benodigde Media Services-code.

## <a name="see-also"></a>Zie ook

[Gebruik de .net SDK Hallo tootrigger taken in Hallo Data Manager](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Volgende stappen

U kunt nu de geüploade assets coderen. Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.
