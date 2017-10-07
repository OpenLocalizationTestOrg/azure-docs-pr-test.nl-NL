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
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="2edfb-103">Wijzigingstype Hallo gereserveerde eenheid</span><span class="sxs-lookup"><span data-stu-id="2edfb-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2edfb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2edfb-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="2edfb-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2edfb-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="2edfb-106">REST</span><span class="sxs-lookup"><span data-stu-id="2edfb-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="2edfb-107">Java</span><span class="sxs-lookup"><span data-stu-id="2edfb-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2edfb-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2edfb-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2edfb-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2edfb-109">Overview</span></span>

<span data-ttu-id="2edfb-110">Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2edfb-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="2edfb-111">U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**.</span><span class="sxs-lookup"><span data-stu-id="2edfb-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="2edfb-112">Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type.</span><span class="sxs-lookup"><span data-stu-id="2edfb-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="2edfb-113">Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden** (RUs).</span><span class="sxs-lookup"><span data-stu-id="2edfb-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="2edfb-114">het aantal ingerichte RUs Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.</span><span class="sxs-lookup"><span data-stu-id="2edfb-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="2edfb-115">RU's werken voor het parallel verwerken van alle media, waaronder indexeringstaken via Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="2edfb-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="2edfb-116">Indexeringstaken worden echter niet sneller verwerkt met snellere gereserveerde eenheden, terwijl dit bij coderen wel het geval is.</span><span class="sxs-lookup"><span data-stu-id="2edfb-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2edfb-117">Zorg ervoor dat tooreview hello [overzicht](media-services-scale-media-processing-overview.md) onderwerp tooget meer informatie over het schalen van media onderwerp verwerken.</span><span class="sxs-lookup"><span data-stu-id="2edfb-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="2edfb-118">Mediaverwerking schalen</span><span class="sxs-lookup"><span data-stu-id="2edfb-118">Scale media processing</span></span>
<span data-ttu-id="2edfb-119">toochange hello gereserveerde eenheid type en Hallo aantal gereserveerde eenheden Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2edfb-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="2edfb-120">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="2edfb-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2edfb-121">In Hallo **instellingen** Selecteer **gereserveerde Media-eenheden**.</span><span class="sxs-lookup"><span data-stu-id="2edfb-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="2edfb-122">toochange hello aantal gereserveerde eenheden voor Hallo gereserveerde eenheidstype hebt geselecteerd, gebruikt u Hallo **geleverd Media-eenheden** schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="2edfb-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="2edfb-123">Hallo toochange **gereserveerde EENHEIDSTYPE**, drukt u op S1, S2 of S3.</span><span class="sxs-lookup"><span data-stu-id="2edfb-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Pagina processors](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="2edfb-125">Druk op Hallo knop toosave uw wijzigingen hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2edfb-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="2edfb-126">Hallo nieuwe gereserveerde eenheden zijn toegewezen wanneer u op opslaan.</span><span class="sxs-lookup"><span data-stu-id="2edfb-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2edfb-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2edfb-127">Next steps</span></span>
<span data-ttu-id="2edfb-128">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="2edfb-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2edfb-129">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2edfb-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

