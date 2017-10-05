---
title: Bestanden vanuit Azure StorSimple uploaden naar een Azure Media Services-account | Microsoft Docs
description: Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager. Het artikel bevat ook koppelingen naar zelfstudies die laten zien hoe u gegevens extraheert uit StorSimple en deze vervolgens als assets uploadt naar een Azure Media Services-account.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 636d55c15aa383208ffb39d5224123831af962c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="c73ac-104">Bestanden vanuit Azure StorSimple uploaden naar een Azure Media Services-account</span><span class="sxs-lookup"><span data-stu-id="c73ac-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="c73ac-105">Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="c73ac-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="c73ac-106">Dit artikel bevat ook koppelingen naar zelfstudies die laten zien hoe u gegevens extraheert uit StorSimple en deze gegevens vervolgens als assets uploadt naar een AMS-account (Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="c73ac-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="c73ac-107">Azure StorSimple Data Manager bevindt zich momenteel in Private Preview.</span><span class="sxs-lookup"><span data-stu-id="c73ac-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="c73ac-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c73ac-108">Overview</span></span>

<span data-ttu-id="c73ac-109">In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset.</span><span class="sxs-lookup"><span data-stu-id="c73ac-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="c73ac-110">De asset kan video, audio, afbeeldingen, verzamelingen van miniaturen, tekstsporen en ondertitelingsbestanden (en de metagegevens voor deze bestanden) bevatten. Zodra de bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in de cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="c73ac-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="c73ac-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) gebruikt cloudopslag als een uitbreiding van de on-premises oplossing en verdeelt gegevens automatisch over de on-premises opslag en de cloudopslag.</span><span class="sxs-lookup"><span data-stu-id="c73ac-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="c73ac-112">Het StorSimple-apparaat ontdubbelt en comprimeert uw gegevens voordat deze naar de cloud worden verzonden, zodat grote bestanden zeer efficiënt in de cloud kunnen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c73ac-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="c73ac-113">De [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)-service biedt API's waarmee u gegevens kunt extraheren uit StorSimple om deze vervolgens als AMS-assets te presenteren.</span><span class="sxs-lookup"><span data-stu-id="c73ac-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="c73ac-114">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c73ac-114">Get started</span></span>

1. <span data-ttu-id="c73ac-115">[Maak een Media Services-account](media-services-portal-create-account.md) waarnaar u de assets wilt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="c73ac-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="c73ac-116">Geef u op voor de preview van Data Manager, zoals wordt beschreven in het artikel [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c73ac-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="c73ac-117">Maak een StorSimple Data Manager-account.</span><span class="sxs-lookup"><span data-stu-id="c73ac-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="c73ac-118">Maak een taak voor gegevenstransformatie die bij uitvoering gegevens extraheert van een StorSimple-apparaat en deze als assets overbrengt naar een AMS-account.</span><span class="sxs-lookup"><span data-stu-id="c73ac-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="c73ac-119">Op het moment dat de taak wordt gestart, wordt er een opslagwachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c73ac-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="c73ac-120">Deze wachtrij wordt gevuld met berichten over getransformeerde blobs wanneer deze gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="c73ac-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="c73ac-121">De naam van deze wachtrij is hetzelfde als de naam van de taakdefinitie.</span><span class="sxs-lookup"><span data-stu-id="c73ac-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="c73ac-122">U kunt deze wachtrij gebruiken om te bepalen wanneer een asset gereed is en vervolgens de gewenste Media Services-bewerking aanroepen om een bewerking op de asset uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c73ac-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="c73ac-123">U kunt deze wachtrij bijvoorbeeld om een Azure-functie te activeren waarin de benodigde Media Services-code is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c73ac-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="c73ac-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c73ac-124">See also</span></span>

<span data-ttu-id="c73ac-125">[Use the .Net SDK to initiate data transformation (Private Preview)](../storsimple/storsimple-data-manager-dotnet-jobs.md) (Gegevenstransformatie starten met de SDK voor .NET (Private Preview))</span><span class="sxs-lookup"><span data-stu-id="c73ac-125">[Use the .Net SDK to trigger jobs in the Data Manager](../storsimple/storsimple-data-manager-dotnet-jobs.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c73ac-126">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c73ac-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c73ac-127">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c73ac-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c73ac-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c73ac-128">Next steps</span></span>

<span data-ttu-id="c73ac-129">U kunt nu de geüploade assets coderen.</span><span class="sxs-lookup"><span data-stu-id="c73ac-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="c73ac-130">Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c73ac-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
