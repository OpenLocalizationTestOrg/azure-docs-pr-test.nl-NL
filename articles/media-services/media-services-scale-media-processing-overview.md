---
title: overzicht van aaaScaling verwerking van Media | Microsoft Docs
description: Dit onderwerp bevat een overzicht van het vergroten/verkleinen Media verwerken met Azure Media Services.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Overzicht van de verwerking van Media schalen
Deze pagina geeft een overzicht van hoe en waarom tooscale media verwerking. 

## <a name="overview"></a>Overzicht
Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt. U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**. Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type. Zie voor meer informatie, Hallo [gereserveerde eenheidstypen](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u opgeven tooprovision uw account met gereserveerde eenheden. het aantal ingerichte gereserveerde eenheden Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account. Bijvoorbeeld, als uw account vijf gereserveerde eenheden, heeft en vervolgens vijf media taken wordt gelijktijdig zo lang worden uitgevoerd als er zijn taken toobe verwerkt. de resterende taken Hallo wachttijd in wachtrij Hallo en wordt ophalen opgepikt sequentieel worden verwerkt wanneer een actieve taak is voltooid. Als een account heeft geen geen gereserveerde eenheden die zijn ingericht, zullen vervolgens taken worden opgepikt sequentieel worden verwerkt. In dit geval Hallo wachttijd tussen een taak is voltooid en hello naast een starten is afhankelijk Hallo beschikbaarheid van resources in Hallo-systeem.

## <a name="choosing-between-different-reserved-unit-types"></a>Kiezen tussen verschillende gereserveerde eenheidstypen
Hallo volgende tabel kunt u besluit bij de keuze tussen verschillende codering snelheid te koppelen. Ook biedt enkele benchmark gevallen en biedt SAS-URL's die u kunt toodownload video's op die u kunt uitvoeren van uw eigen tests:

| Scenario's | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Beoogde gebruiksscenario |Single-bitrate codering. <br/>Bestanden op SD of onder oplossingen, tijd niet gevoelige, lage kosten. |Single-bitrate en meerdere bitrate codering.<br/>Het normale gebruik voor zowel SD en HD codering. |Single-bitrate en meerdere bitrate codering.<br/>Volledige HD en 4K resolutie video's. Tijd die gevoelige en snellere reactietijd ook codering. |
| Benchmark |[Bestand voor invoer: 5 minuten lang 640x360p op 29,97 frames per seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Codering tooa single-bitrate MP4-bestand op Hallo dezelfde resolutie ongeveer 11 minuten in beslag neemt. |[Bestand voor invoer: 5 minuten lang 1280x720p op 29,97 frames per seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>Codering met 'Standaardinstelling H264 Single-Bitrate 720p' vooraf duurt ongeveer 5 minuten.<br/><br/>Codering met ' standaardinstelling H264 Multiple Bitrate 720p ' voorinstelling duurt ongeveer 11.5 minuten. |[Bestand voor invoer: 5 minuten lang 1920x1080p op 29,97 frames per seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>Codering met 'Standaardinstelling H264 Single-Bitrate 1080p' vooraf duurt ongeveer 2.7 minuten.<br/><br/>Codering met ' standaardinstelling H264 Multiple Bitrate 1080p ' voorinstelling duurt ongeveer 5.7 minuten. |

## <a name="considerations"></a>Overwegingen
> [!IMPORTANT]
> Bekijk de overwegingen in deze sectie beschreven.  
> 
> 

* Gereserveerde eenheden werkt voor alle media verwerking, met inbegrip van taken met behulp van Azure Media Indexer indexeren parallelizing.  Indexeringstaken worden echter niet sneller verwerkt met snellere gereserveerde eenheden, terwijl dit bij coderen wel het geval is.
* Als Hallo gedeeld met toepassingen, dat wil zeggen, zonder gereserveerde eenheden, en vervolgens uw taken coderen hebben dezelfde prestaties Hallo net als bij S1 RUs. Maar er is geen bovengrens toohello tijd uw taken in in de wachtrij staat besteden kunnen en op elk gewenst maximaal slechts één taak wordt uitgevoerd.
* Hallo volgende datacenters bieden geen Hallo **S2** gereserveerd eenheidstype: Brazilië-Zuid en India-West.
* Hallo volgende Datacenter biedt geen Hallo **S3** gereserveerd eenheidstype: India-West.

## <a name="billing"></a>Facturering

Er worden kosten in rekening gebracht op basis van het werkelijke aantal minuten dat gereserveerde media-eenheden worden gebruikt. Zie de sectie Veelgestelde vragen over Hallo Hallo voor een gedetailleerde uitleg [Media Services-prijzen](https://azure.microsoft.com/pricing/details/media-services/) pagina.   

## <a name="quotas-and-limitations"></a>Quota en beperkingen
Voor informatie over quota's en beperkingen en hoe tooopen een ondersteuningsticket zien [quota's en beperkingen](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Volgende stap
Hallo schalen media verwerken van de taak met een van deze technologieën bereiken: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

