---
title: aaaHow tooCreate een media processor met hello Azure Media Services SDK voor .NET | Microsoft Docs
description: Meer informatie over hoe een tooencode onderdeel van media processor toocreate indeling converteren, versleutelen of ontsleutelen van media-inhoud voor Azure Media Services. Codevoorbeelden zijn geschreven in C# en gebruiken van Hallo Media Services SDK voor .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Procedure: een exemplaar van de Processor Media
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overzicht
In Media Services die een Mediaprocessor een component die verantwoordelijk is voor een specifieke verwerkingstaak is, zoals de codering, versleutelen of ontsleutelen van media-inhoud-conversie-indeling. U doorgaans een Mediaprocessor maken tijdens het maken van een taak tooencode, versleutelen of Hallo-indeling van media-inhoud te converteren.

## <a name="azure-media-processors"></a>Azure media-processors 

Volgend onderwerp Hallo bevat overzichten van media processors:

* [Codering van media-processors](scenarios-and-availability.md#encoding-media-processors)
* [Analytics-mediaprocessoren](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Ophalen van Mediaprocessor

Hallo na methode toont hoe een exemplaar van de processor media tooget. Hallo-voorbeeld wordt ervan uitgegaan Hallo gebruik van een module-niveau variabele met de naam **_context** tooreference Hallo servercontext zoals beschreven in de sectie Hallo [hoe: verbinding maken met Services programmatisch tooMedia](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Volgende stappen
Als u weet hoe een exemplaar van de processor media tooget gaan toohello [hoe tooEncode een Asset](media-services-dotnet-encode-with-media-encoder-standard.md) onderwerp dat ziet u hoe toouse Hallo Media Encoder Standard tooencode een asset.

