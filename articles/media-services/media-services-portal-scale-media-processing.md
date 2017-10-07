---
title: aaaScale media verwerken met behulp van Azure-portal Hallo | Microsoft Docs
description: Deze zelfstudie leert u Hallo van vergroten/verkleinen media verwerken met behulp van hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Wijzigingstype Hallo gereserveerde eenheid
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Overzicht

Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt. U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**. Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type.

Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden** (RUs). het aantal ingerichte RUs Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.

>[!NOTE]
>RU's werken voor het parallel verwerken van alle media, waaronder indexeringstaken via Azure Media Indexer. Indexeringstaken worden echter niet sneller verwerkt met snellere gereserveerde eenheden, terwijl dit bij coderen wel het geval is.

> [!IMPORTANT]
> Zorg ervoor dat tooreview hello [overzicht](media-services-scale-media-processing-overview.md) onderwerp tooget meer informatie over het schalen van media onderwerp verwerken.
> 
> 

## <a name="scale-media-processing"></a>Mediaverwerking schalen
toochange hello gereserveerde eenheid type en Hallo aantal gereserveerde eenheden Hallo te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. In Hallo **instellingen** Selecteer **gereserveerde Media-eenheden**.
   
    toochange hello aantal gereserveerde eenheden voor Hallo gereserveerde eenheidstype hebt geselecteerd, gebruikt u Hallo **geleverd Media-eenheden** schuifregelaar.
   
    Hallo toochange **gereserveerde EENHEIDSTYPE**, drukt u op S1, S2 of S3.
   
    ![Pagina processors](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Druk op Hallo knop toosave uw wijzigingen hebt opgeslagen.
   
    Hallo nieuwe gereserveerde eenheden zijn toegewezen wanneer u op opslaan.

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

