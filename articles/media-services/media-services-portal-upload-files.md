---
title: aaa"uploaden van bestanden naar een Media Services-account met behulp van hello Azure-portal | Microsoft Docs'
description: "Deze zelfstudie leert u Hallo van bestanden zijn geüpload naar een Media Services-account met behulp van hello Azure-portal"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="3710b-103">Bestanden uploaden naar een Media Services-account met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3710b-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3710b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3710b-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="3710b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3710b-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="3710b-106">REST</span><span class="sxs-lookup"><span data-stu-id="3710b-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="3710b-107">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3710b-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3710b-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3710b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="3710b-109">In Media Services uploadt u de digitale bestanden naar (of neemt u deze op in) een asset.</span><span class="sxs-lookup"><span data-stu-id="3710b-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="3710b-110">Hallo Asset kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.) Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="3710b-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="3710b-111">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="3710b-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="3710b-112">Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3710b-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="3710b-113">Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="3710b-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="3710b-114">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="3710b-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3710b-115">Op Hallo **instellingen** blade, klikt u op **activa**.</span><span class="sxs-lookup"><span data-stu-id="3710b-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Bestanden uploaden](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="3710b-117">Klik op Hallo **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="3710b-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="3710b-118">Hallo **videoasset uploaden** venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3710b-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3710b-119">Er geldt geen beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="3710b-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="3710b-120">Blader toohello gewenste video op uw computer, selecteert u deze en klik op OK.</span><span class="sxs-lookup"><span data-stu-id="3710b-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="3710b-121">Hallo uploaden wordt gestart en u kunt de voortgang Hallo onder Hallo bestandsnaam bekijken.</span><span class="sxs-lookup"><span data-stu-id="3710b-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="3710b-122">Nadat het Hallo uploaden is voltooid, ziet u Hallo nieuwe asset weergegeven in Hallo **activa** venster.</span><span class="sxs-lookup"><span data-stu-id="3710b-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3710b-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3710b-123">Next steps</span></span>
<span data-ttu-id="3710b-124">U kunt nu de geüploade assets coderen.</span><span class="sxs-lookup"><span data-stu-id="3710b-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="3710b-125">Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3710b-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="3710b-126">U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="3710b-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="3710b-127">Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3710b-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3710b-128">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="3710b-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3710b-129">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="3710b-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

