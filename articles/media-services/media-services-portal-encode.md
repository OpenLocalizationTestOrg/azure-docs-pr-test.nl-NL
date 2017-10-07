---
title: een asset met Media Encoder Standard met hello Azure-portal aaaEncode | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een activum met Media Encoder Standard met hello Azure-portal-codering.
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
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Een asset met Media Encoder Standard met hello Azure-portal coderen
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 
> 

Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming tooyour clients leveren. Media Services ondersteunt de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare uw video's voor adaptive bitrate streaming, moet u tooencode de bron-video in multi-bitrate-bestanden. Moet u Hallo **Media Encoder Standard** encoder tooencode uw video's.  

Media Services biedt ook dynamische pakketten zodat u toodeliver uw multi-bitrate MP4s in de volgende streaming-indelingen Hallo: MPEG DASH, HLS, Smooth Streaming, zonder dat u toore-pakket in een van deze streaming-indelingen hoeft. Met dynamische pakketten hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.

tootake profiteren van dynamische pakketten hoeft u tooencode uw bronbestand in een set multi-bitrate MP4-bestanden (Hallo coderingsstappen worden uitgelegd later in deze sectie).

tooscale media verwerking, Zie [dit](media-services-portal-scale-media-processing.md) onderwerp.

## <a name="encode-with-hello-azure-portal"></a>Codeer Hello Azure-portal
Deze sectie beschrijft Hallo mogelijke stappen tooencode uw inhoud met Media Encoder Standard.

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. In Hallo **instellingen** Selecteer **activa**.  
3. In Hallo **activa** venster, selecteer Hallo asset dat u tooencode wilt.
4. Druk op Hallo **coderen** knop.
5. In Hallo **een asset coderen** venster, selecteer Hallo 'Media Encoder Standard' processor en een standaardinstelling. Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen. Als u van plan toocontrol welke codering definitie wordt gebruikt bent, houd hiermee rekening: het is belangrijk tooselect Hallo voorinstelling die het meest geschikt is voor uw invoervideo. Bijvoorbeeld, als u weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kan u Hallo ' standaardinstelling H264 Multiple Bitrate 1080p ' vooraf ingestelde. Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.
   
   Voor eenvoudiger beheer hebt u een optie bewerken Hallo-naam van de uitvoerasset hello en Hallo-naam van Hallo-taak.
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Kies **Maken**.

## <a name="next-step"></a>Volgende stap
U kunt de voortgang codering taak Hello Azure-portal, zoals beschreven in [dit](media-services-portal-check-job-progress.md) artikel.  

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

