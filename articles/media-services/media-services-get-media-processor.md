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
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="9c2f3-104">Procedure: een exemplaar van de Processor Media</span><span class="sxs-lookup"><span data-stu-id="9c2f3-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c2f3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9c2f3-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="9c2f3-106">REST</span><span class="sxs-lookup"><span data-stu-id="9c2f3-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9c2f3-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9c2f3-107">Overview</span></span>
<span data-ttu-id="9c2f3-108">In Media Services die een Mediaprocessor een component die verantwoordelijk is voor een specifieke verwerkingstaak is, zoals de codering, versleutelen of ontsleutelen van media-inhoud-conversie-indeling.</span><span class="sxs-lookup"><span data-stu-id="9c2f3-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="9c2f3-109">U doorgaans een Mediaprocessor maken tijdens het maken van een taak tooencode, versleutelen of Hallo-indeling van media-inhoud te converteren.</span><span class="sxs-lookup"><span data-stu-id="9c2f3-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="9c2f3-110">Azure media-processors</span><span class="sxs-lookup"><span data-stu-id="9c2f3-110">Azure media processors</span></span> 

<span data-ttu-id="9c2f3-111">Volgend onderwerp Hallo bevat overzichten van media processors:</span><span class="sxs-lookup"><span data-stu-id="9c2f3-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="9c2f3-112">Codering van media-processors</span><span class="sxs-lookup"><span data-stu-id="9c2f3-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="9c2f3-113">Analytics-mediaprocessoren</span><span class="sxs-lookup"><span data-stu-id="9c2f3-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="9c2f3-114">Ophalen van Mediaprocessor</span><span class="sxs-lookup"><span data-stu-id="9c2f3-114">Get Media Processor</span></span>

<span data-ttu-id="9c2f3-115">Hallo na methode toont hoe een exemplaar van de processor media tooget.</span><span class="sxs-lookup"><span data-stu-id="9c2f3-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="9c2f3-116">Hallo-voorbeeld wordt ervan uitgegaan Hallo gebruik van een module-niveau variabele met de naam **_context** tooreference Hallo servercontext zoals beschreven in de sectie Hallo [hoe: verbinding maken met Services programmatisch tooMedia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9c2f3-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="9c2f3-117">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="9c2f3-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9c2f3-118">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="9c2f3-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9c2f3-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c2f3-119">Next Steps</span></span>
<span data-ttu-id="9c2f3-120">Als u weet hoe een exemplaar van de processor media tooget gaan toohello [hoe tooEncode een Asset](media-services-dotnet-encode-with-media-encoder-standard.md) onderwerp dat ziet u hoe toouse Hallo Media Encoder Standard tooencode een asset.</span><span class="sxs-lookup"><span data-stu-id="9c2f3-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

