---
title: Hoe een Mediaprocessor exemplaar met tooget REST aaa | Microsoft Docs
description: Meer informatie over hoe een tooencode onderdeel van media processor toocreate indeling converteren, versleutelen of ontsleutelen van media-inhoud voor Azure Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="4fee0-103">Hoe een exemplaar van de Processor Media tooget</span><span class="sxs-lookup"><span data-stu-id="4fee0-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fee0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4fee0-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="4fee0-105">REST</span><span class="sxs-lookup"><span data-stu-id="4fee0-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4fee0-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4fee0-106">Overview</span></span>
<span data-ttu-id="4fee0-107">In Media Services die een Mediaprocessor een component die verantwoordelijk is voor een specifieke verwerkingstaak is, zoals de codering, versleutelen of ontsleutelen van media-inhoud-conversie-indeling.</span><span class="sxs-lookup"><span data-stu-id="4fee0-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="4fee0-108">U doorgaans een Mediaprocessor maken tijdens het maken van een taak tooencode, versleutelen of Hallo-indeling van media-inhoud te converteren.</span><span class="sxs-lookup"><span data-stu-id="4fee0-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="4fee0-109">Azure media-processors</span><span class="sxs-lookup"><span data-stu-id="4fee0-109">Azure media processors</span></span> 

<span data-ttu-id="4fee0-110">Volgend onderwerp Hallo bevat overzichten van media processors:</span><span class="sxs-lookup"><span data-stu-id="4fee0-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="4fee0-111">Codering van media-processors</span><span class="sxs-lookup"><span data-stu-id="4fee0-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="4fee0-112">Analytics-mediaprocessoren</span><span class="sxs-lookup"><span data-stu-id="4fee0-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="4fee0-113">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4fee0-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="4fee0-114">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4fee0-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="4fee0-115">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="4fee0-115">Connect tooMedia Services</span></span>

<span data-ttu-id="4fee0-116">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4fee0-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="4fee0-117">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4fee0-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="4fee0-118">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="4fee0-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="4fee0-119">Ophalen van een Mediaprocessor</span><span class="sxs-lookup"><span data-stu-id="4fee0-119">Get a media processor</span></span>

<span data-ttu-id="4fee0-120">Hallo na REST-aanroep ziet u hoe tooget een Mediaprocessor-exemplaar met de naam (in dit geval **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="4fee0-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="4fee0-121">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="4fee0-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="4fee0-122">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="4fee0-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="4fee0-123">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="4fee0-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fee0-124">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="4fee0-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4fee0-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fee0-125">Next Steps</span></span>
<span data-ttu-id="4fee0-126">Als u weet hoe een exemplaar van de processor media tooget gaan toohello [hoe tooEncode een Asset](media-services-rest-get-started.md) onderwerp dat ziet u hoe toouse Hallo Media Encoder Standard tooencode een asset.</span><span class="sxs-lookup"><span data-stu-id="4fee0-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

