---
title: Een asset met Media Encoder Standard met de Azure-portal coderen | Microsoft Docs
description: Deze zelfstudie leert u de stappen voor het coderen van een activum met Media Encoder Standard met de Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a>Een asset met Media Encoder Standard met de Azure-portal coderen
> [!NOTE]
> U hebt een Azure-account nodig om deze zelfstudie te voltooien. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 
> 

Wanneer er met Azure Media Services wordt gewerkt, wordt er meestal een Adaptive Bitrate Streaming aan uw clients geleverd. Media Services ondersteunt de volgende Adaptive Bitrate Streaming-technologieën: HLS (HTTP Live Streaming), Smooth Streaming en MPEG DASH. Als u video's wilt voorbereiden voor Adaptive Bitrate Streaming, moet u de bronvideo coderen in multi-bitrate-bestanden. Gebruik het coderingsprogramma **Media Encoder Standard** om de video's te coderen.  

Media Services biedt ook dynamische pakketten zodat u kunt uw multi-bitrate MP4s in de volgende streaming-indelingen leveren: MPEG DASH, HLS, Smooth Streaming, zonder dat u opnieuw verpakken in een van deze streaming-indelingen hoeft. Voor dynamische pakketten hoeft u voor slechts één opslagindeling de bestanden op te slaan en hiervoor te betalen. Media Services bouwt en levert de juiste reactie op basis van aanvragen van een client.

Als u gebruik wilt maken van dynamische pakketten, moet u het bronbestand coderen in een set multi-bitrate MP4-bestanden (de coderingsstappen worden verderop in deze sectie uitgelegd).

Als u wilt schalen verwerking van de media, Zie [dit](media-services-portal-scale-media-processing.md) onderwerp.

## <a name="encode-with-the-azure-portal"></a>Coderen met de Azure-portal
In deze sectie wordt beschreven hoe u uw inhoud codeert met Media Encoder Standard.

1. Selecteer uw Azure Media Services-account in [Azure Portal](https://portal.azure.com/).
2. Selecteer in het venster **Instellingen** de optie **Assets**.  
3. Selecteer in het venster **Assets** de asset die u wilt coderen.
4. Klik op de knop **Coderen**.
5. Selecteer in het venster **Een asset coderen** de processor Media Encoder Standard en een standaardinstelling. Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen. Als u wilt bepalen welke standaardinstelling voor versleuteling wordt gebruikt, moet u er rekening mee houden dat het belangrijk is de standaardinstelling te selecteren die het meest geschikt is voor uw invoervideo. Als u bijvoorbeeld weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kunt u de standaardinstelling H264 Multiple Bitrate 1080p gebruiken. Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.
   
   Voor eenvoudiger beheer kunt u de naam van de uitvoerasset en de naam van de taak bewerken.
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Kies **Maken**.

## <a name="next-step"></a>Volgende stap
U kunt de voortgang codering taak met de Azure portal, zoals beschreven in [dit](media-services-portal-check-job-progress.md) artikel.  

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

