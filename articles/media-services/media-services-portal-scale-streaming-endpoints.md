---
title: streaming-eindpunten Hello Azure-portal aaaScale | Microsoft Docs
description: Deze zelfstudie leert u Hallo van streaming-eindpunten Hello Azure-portal te schalen.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="72258-103">Schaal streaming-eindpunten Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="72258-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="72258-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="72258-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="72258-105">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="72258-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="72258-106">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72258-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="72258-107">**Premium**-streaming-eindpunten zijn geschikt voor geavanceerde workloads omdat er gebruik wordt gemaakt van toegewezen, schaalbare bandbreedtecapaciteit.</span><span class="sxs-lookup"><span data-stu-id="72258-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="72258-108">Klanten met een **Premium**-streaming-eindpunt krijgen standaard één streaming-eenheid (SU).</span><span class="sxs-lookup"><span data-stu-id="72258-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="72258-109">Hallo streaming-eindpunt kan worden uitgebreid door SUs toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="72258-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="72258-110">Elke SU biedt extra bandbreedte capaciteit toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="72258-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="72258-111">Zie voor meer informatie over het streaming-eindpunttypen en CDN configuratie Hallo [Streaming-eindpunt overzicht](media-services-portal-manage-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="72258-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="72258-112">Dit onderwerp wordt beschreven hoe tooscale een streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="72258-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="72258-113">Zie [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107) (Informatie over Media Services-prijzen) voor informatie over prijzen.</span><span class="sxs-lookup"><span data-stu-id="72258-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="72258-114">Streaming eindpunten schalen</span><span class="sxs-lookup"><span data-stu-id="72258-114">Scale streaming endpoints</span></span>

<span data-ttu-id="72258-115">toochange hello aantal streaming-eenheden, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="72258-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="72258-116">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="72258-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="72258-117">In Hallo **instellingen** Selecteer **Streaming-eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="72258-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="72258-118">Klik op Hallo streaming-eindpunt dat u wilt dat tooscale.</span><span class="sxs-lookup"><span data-stu-id="72258-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="72258-119">U kunt alleen schalen **Premium** streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="72258-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="72258-120">Verplaats Hallo schuifregelaar toospecify Hallo aantal streaming-eenheden.</span><span class="sxs-lookup"><span data-stu-id="72258-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="72258-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72258-122">Next steps</span></span>
<span data-ttu-id="72258-123">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="72258-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="72258-124">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="72258-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

