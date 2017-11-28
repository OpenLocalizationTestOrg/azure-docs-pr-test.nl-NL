---
title: aaaUpload bestanden naar een Azure Media Services-account van Azure StorSimple | Microsoft Docs
description: Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager. Hallo artikel bevat ook koppelingen tootutorials die laten hoe u zien gegevens van StorSimple tooextract en upload het als activa tooan Azure Media Services-account.
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
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="45d7e-104">Bestanden vanuit Azure StorSimple uploaden naar een Azure Media Services-account</span><span class="sxs-lookup"><span data-stu-id="45d7e-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="45d7e-105">Dit artikel geeft een kort overzicht van Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="45d7e-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="45d7e-106">Hallo artikel bevat ook koppelingen tootutorials die laten hoe u zien tooextract gegevens van StorSimple en deze gegevens te uploaden als activa tooan Azure Media Services (AMS)-account.</span><span class="sxs-lookup"><span data-stu-id="45d7e-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="45d7e-107">Azure StorSimple Data Manager bevindt zich momenteel in Private Preview.</span><span class="sxs-lookup"><span data-stu-id="45d7e-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="45d7e-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="45d7e-108">Overview</span></span>

<span data-ttu-id="45d7e-109">In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset.</span><span class="sxs-lookup"><span data-stu-id="45d7e-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="45d7e-110">Hallo Asset kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.) Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="45d7e-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="45d7e-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) cloudopslag gebruikt als een uitbreiding van Hallo on-premises-oplossing en automatisch gegevens over Hallo lokale opslag en cloud-opslag lagen.</span><span class="sxs-lookup"><span data-stu-id="45d7e-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="45d7e-112">Hallo StorSimple-apparaat dedupes en uw gegevens te comprimeren voordat deze toohello cloud waardoor het zeer efficiënte voor het verzenden van grote bestanden toohello cloud worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="45d7e-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="45d7e-113">Hallo [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service biedt API's die u tooextract gegevens van StorSimple inschakelen en op te geven als AMS activa.</span><span class="sxs-lookup"><span data-stu-id="45d7e-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="45d7e-114">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="45d7e-114">Get started</span></span>

1. <span data-ttu-id="45d7e-115">[Een Media Services-account maken](media-services-portal-create-account.md) waarnaar tootransfer Hallo activa.</span><span class="sxs-lookup"><span data-stu-id="45d7e-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="45d7e-116">Aanmelden voor de preview van Data Manager, zoals beschreven in Hallo [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="45d7e-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="45d7e-117">Maak een StorSimple Data Manager-account.</span><span class="sxs-lookup"><span data-stu-id="45d7e-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="45d7e-118">Maak een taak voor gegevenstransformatie die bij uitvoering gegevens extraheert van een StorSimple-apparaat en deze als assets overbrengt naar een AMS-account.</span><span class="sxs-lookup"><span data-stu-id="45d7e-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="45d7e-119">Wanneer Hallo-taak gestart wordt, wordt een opslagwachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45d7e-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="45d7e-120">Deze wachtrij wordt gevuld met berichten over getransformeerde blobs wanneer deze gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="45d7e-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="45d7e-121">Hallo-naam van deze wachtrij is hetzelfde als de naam van de taakdefinitie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="45d7e-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="45d7e-122">U kunt deze wachtrij toodetermine wanneer asset is klaar te maken en de gewenste bewerking toorun voor Media Services voor het aanroepen.</span><span class="sxs-lookup"><span data-stu-id="45d7e-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="45d7e-123">Bijvoorbeeld, kunt u deze wachtrij tootrigger een Azure-functie met Hallo benodigde Media Services-code.</span><span class="sxs-lookup"><span data-stu-id="45d7e-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="45d7e-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="45d7e-124">See also</span></span>

[<span data-ttu-id="45d7e-125">Gebruik de .net SDK Hallo tootrigger taken in Hallo Data Manager</span><span class="sxs-lookup"><span data-stu-id="45d7e-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="45d7e-126">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="45d7e-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="45d7e-127">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="45d7e-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="45d7e-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45d7e-128">Next steps</span></span>

<span data-ttu-id="45d7e-129">U kunt nu de geüploade assets coderen.</span><span class="sxs-lookup"><span data-stu-id="45d7e-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="45d7e-130">Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="45d7e-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
