---
title: Schaal streaming-eindpunten met de Azure portal | Microsoft Docs
description: Deze zelfstudie leert u de stappen voor het schalen van streaming-eindpunten met de Azure-portal.
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
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="ef735-103">Streaming-eindpunten schalen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef735-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="ef735-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ef735-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="ef735-105">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ef735-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ef735-106">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef735-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="ef735-107">**Premium**-streaming-eindpunten zijn geschikt voor geavanceerde workloads omdat er gebruik wordt gemaakt van toegewezen, schaalbare bandbreedtecapaciteit.</span><span class="sxs-lookup"><span data-stu-id="ef735-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="ef735-108">Klanten met een **Premium**-streaming-eindpunt krijgen standaard één streaming-eenheid (SU).</span><span class="sxs-lookup"><span data-stu-id="ef735-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="ef735-109">Het streaming-eindpunt kan worden geschaald door SU's toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ef735-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="ef735-110">Elke SU biedt extra bandbreedtecapaciteit voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ef735-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="ef735-111">Zie voor meer informatie over het streaming-eindpunttypen en CDN configuratie, de [Streaming-eindpunt overzicht](media-services-portal-manage-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ef735-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="ef735-112">Dit onderwerp bevat een streaming-eindpunt te schalen.</span><span class="sxs-lookup"><span data-stu-id="ef735-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="ef735-113">Zie [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107) (Informatie over Media Services-prijzen) voor informatie over prijzen.</span><span class="sxs-lookup"><span data-stu-id="ef735-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="ef735-114">Streaming eindpunten schalen</span><span class="sxs-lookup"><span data-stu-id="ef735-114">Scale streaming endpoints</span></span>

<span data-ttu-id="ef735-115">Als u wilt wijzigen van het aantal streaming-eenheden, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ef735-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="ef735-116">Selecteer uw Azure Media Services-account in [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ef735-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ef735-117">In de **instellingen** Selecteer **Streaming-eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="ef735-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="ef735-118">Klik op het streaming-eindpunt dat u wilt schalen.</span><span class="sxs-lookup"><span data-stu-id="ef735-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="ef735-119">U kunt alleen schalen **Premium** streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ef735-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="ef735-120">Verplaats de schuifregelaar om het aantal streaming-eenheden te geven.</span><span class="sxs-lookup"><span data-stu-id="ef735-120">Move the slider to specify the number of streaming units.</span></span>

    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="ef735-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef735-122">Next steps</span></span>
<span data-ttu-id="ef735-123">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="ef735-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef735-124">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ef735-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

