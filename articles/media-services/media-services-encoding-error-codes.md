---
title: aaaAzure Media Services-codering foutcodes | Microsoft Docs
description: In dit onderwerp worden de foutcodes die kunnen worden geretourneerd voor het geval is een fout opgetreden tijdens de uitvoering van de taak codering Hallo...
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="29cfb-103">Foutcodes voor codering</span><span class="sxs-lookup"><span data-stu-id="29cfb-103">Encoding error codes</span></span>

<span data-ttu-id="29cfb-104">Hallo bevat volgende tabel de foutcodes die kunnen worden geretourneerd voor het geval is een fout opgetreden tijdens de uitvoering van de taak codering Hallo.</span><span class="sxs-lookup"><span data-stu-id="29cfb-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="29cfb-105">Foutdetails tooget in uw code .NET gebruiken Hallo [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="29cfb-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="29cfb-106">Foutdetails tooget in uw code REST gebruiken Hallo [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST-API.</span><span class="sxs-lookup"><span data-stu-id="29cfb-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="29cfb-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="29cfb-107">ErrorDetail.Code</span></span> | <span data-ttu-id="29cfb-108">Mogelijke oorzaken voor fout</span><span class="sxs-lookup"><span data-stu-id="29cfb-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="29cfb-109">Onbekend</span><span class="sxs-lookup"><span data-stu-id="29cfb-109">Unknown</span></span> |<span data-ttu-id="29cfb-110">Onbekende fout tijdens het Hallo-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="29cfb-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="29cfb-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="29cfb-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="29cfb-112">Categorie van fouten die betrekking heeft op fouten bij het downloaden van de invoer asset zoals namen van de beschadigde bestanden, nul lengte bestanden, onjuist opgemaakt enzovoort.</span><span class="sxs-lookup"><span data-stu-id="29cfb-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="29cfb-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="29cfb-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="29cfb-114">De categorie van fouten die betrekking heeft op problemen op Hallo servicezijde - voorbeeld netwerk of opslag fouten tijdens het downloaden.</span><span class="sxs-lookup"><span data-stu-id="29cfb-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="29cfb-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="29cfb-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="29cfb-116">Categorie van fouten waar de taak <see cref="MediaTask.PrivateData"/> (configuratie) is niet geldig, bijvoorbeeld Hallo configuratie is niet een geldig systeem voorinstelling of bevat ongeldige XML.</span><span class="sxs-lookup"><span data-stu-id="29cfb-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="29cfb-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="29cfb-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="29cfb-118">De categorie van fouten tijdens het Hallo-uitvoering van Hallo-taak als er problemen binnen Hallo invoer mediabestanden fout veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="29cfb-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="29cfb-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="29cfb-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="29cfb-120">Categorie van fouten waar Mediaprocessor Hallo Hallo-bestanden opgegeven kan niet worden verwerkt - media-indeling niet ondersteund of komt niet overeen met de Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="29cfb-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="29cfb-121">Bijvoorbeeld, probeert tooproduce alleen audio-uitvoer van een activum met alleen video</span><span class="sxs-lookup"><span data-stu-id="29cfb-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="29cfb-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="29cfb-122">ErrorProcessingTask</span></span> |<span data-ttu-id="29cfb-123">Categorie van andere fouten die Hallo Mediaprocessor aangetroffen tijdens het verwerken van Hallo van Hallo-taak die niet-verwante toocontent zijn.</span><span class="sxs-lookup"><span data-stu-id="29cfb-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="29cfb-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="29cfb-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="29cfb-125">Categorie van fouten tijdens het uploaden van de uitvoerasset Hallo</span><span class="sxs-lookup"><span data-stu-id="29cfb-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="29cfb-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="29cfb-126">ErrorCancelingTask</span></span> |<span data-ttu-id="29cfb-127">Categorie van fouten toocover fouten tijdens een poging de toocancel Hallo taak</span><span class="sxs-lookup"><span data-stu-id="29cfb-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="29cfb-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="29cfb-128">TransientError</span></span> |<span data-ttu-id="29cfb-129">Categorie van fouten toocover problemen van voorbijgaande aard (bv.</span><span class="sxs-lookup"><span data-stu-id="29cfb-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="29cfb-130">tijdelijke netwerkproblemen met Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="29cfb-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="29cfb-131">tooget hulp van Hallo **Media Services** team, open een [ondersteunen ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="29cfb-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="29cfb-132">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="29cfb-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="29cfb-133">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="29cfb-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="29cfb-134">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="29cfb-134">Related articles</span></span>
* [<span data-ttu-id="29cfb-135">Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen</span><span class="sxs-lookup"><span data-stu-id="29cfb-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="29cfb-136">Quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="29cfb-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
