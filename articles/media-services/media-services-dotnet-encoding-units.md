---
title: aaaScale media verwerken door toe te voegen codering eenheden - Azure |  Microsoft Docs
description: Meer informatie over hoe toohow tooadd codering eenheden met .NET
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="2e1e8-103">Hoe tooscale codering met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2e1e8-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e1e8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2e1e8-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="2e1e8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2e1e8-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="2e1e8-106">REST</span><span class="sxs-lookup"><span data-stu-id="2e1e8-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="2e1e8-107">Java</span><span class="sxs-lookup"><span data-stu-id="2e1e8-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2e1e8-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2e1e8-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2e1e8-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2e1e8-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2e1e8-110">Zorg ervoor dat tooreview hello [overzicht](media-services-scale-media-processing-overview.md) onderwerp tooget meer informatie over het schalen van media onderwerp verwerken.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="2e1e8-111">toochange hello gereserveerde eenheid type en Hallo aantal gereserveerde eenheden met .NET SDK codering Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e1e8-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="2e1e8-112">Een Ondersteuningsticket openen</span><span class="sxs-lookup"><span data-stu-id="2e1e8-112">Opening a Support Ticket</span></span>
<span data-ttu-id="2e1e8-113">Standaard elke Media Services-account tooup too25 kunt schalen codering en 5 On Demand gereserveerde Streaming-eenheden.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="2e1e8-114">U kunt een hogere limiet aanvragen door een ondersteuningsticket openen.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="2e1e8-115">Een ondersteuningsticket opent</span><span class="sxs-lookup"><span data-stu-id="2e1e8-115">Open a support ticket</span></span>
<span data-ttu-id="2e1e8-116">een ondersteuningsticket tooopen Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e1e8-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="2e1e8-117">Klik op [ondersteuning krijgen](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="2e1e8-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="2e1e8-118">Als u niet bent aangemeld, wordt u na vragen aan gebruiker tooenter worden uw referenties.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="2e1e8-119">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-119">Select your subscription.</span></span>
3. <span data-ttu-id="2e1e8-120">Selecteer onder ondersteuning voor type 'Technical'.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="2e1e8-121">Klik op 'Ticket maken'.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="2e1e8-122">Selecteer "Azure Media Services' in de lijst met producten voor Hallo die wordt weergegeven op de volgende pagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="2e1e8-123">Selecteer een 'probleemtype' die geschikt is voor uw probleem.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="2e1e8-124">Klik op Doorgaan.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-124">Click Continue.</span></span>
8. <span data-ttu-id="2e1e8-125">Volg de instructies op de volgende pagina en Geef details over uw probleem.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="2e1e8-126">Klik op verzenden tooopen Hallo ticket.</span><span class="sxs-lookup"><span data-stu-id="2e1e8-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2e1e8-127">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="2e1e8-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2e1e8-128">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2e1e8-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

