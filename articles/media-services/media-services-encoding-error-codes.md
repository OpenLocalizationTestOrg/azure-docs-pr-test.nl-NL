---
title: Azure Media Services-foutcodes codering | Microsoft Docs
description: In dit onderwerp worden de foutcodes die kunnen worden geretourneerd voor het geval een fout tijdens het codering taak uitvoeren opgetreden is...
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
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="e2428-103">Foutcodes voor codering</span><span class="sxs-lookup"><span data-stu-id="e2428-103">Encoding error codes</span></span>

<span data-ttu-id="e2428-104">De volgende tabel bevat de foutcodes die kunnen worden geretourneerd voor het geval een fout tijdens de uitvoering van de taak voor codering opgetreden is.</span><span class="sxs-lookup"><span data-stu-id="e2428-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="e2428-105">Als u details van fouten in uw .NET-code, gebruikt de [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="e2428-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="e2428-106">Als u details van fouten in de REST-code, gebruikt de [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST-API.</span><span class="sxs-lookup"><span data-stu-id="e2428-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="e2428-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="e2428-107">ErrorDetail.Code</span></span> | <span data-ttu-id="e2428-108">Mogelijke oorzaken voor fout</span><span class="sxs-lookup"><span data-stu-id="e2428-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="e2428-109">Onbekend</span><span class="sxs-lookup"><span data-stu-id="e2428-109">Unknown</span></span> |<span data-ttu-id="e2428-110">Onbekende fout tijdens het uitvoeren van de taak</span><span class="sxs-lookup"><span data-stu-id="e2428-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="e2428-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="e2428-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="e2428-112">Categorie van fouten die betrekking heeft op fouten bij het downloaden van de invoer asset zoals namen van de beschadigde bestanden, nul lengte bestanden, onjuist opgemaakt enzovoort.</span><span class="sxs-lookup"><span data-stu-id="e2428-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="e2428-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="e2428-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="e2428-114">De categorie van fouten die betrekking heeft op problemen aan de kant van de service - voorbeeld netwerk of opslag fouten tijdens het downloaden.</span><span class="sxs-lookup"><span data-stu-id="e2428-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="e2428-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="e2428-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="e2428-116">Categorie van fouten waar de taak <see cref="MediaTask.PrivateData"/> (configuratie) is niet geldig, bijvoorbeeld de configuratie is niet een geldig systeem voorinstelling of bevat ongeldige XML.</span><span class="sxs-lookup"><span data-stu-id="e2428-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="e2428-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="e2428-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="e2428-118">De categorie van fouten tijdens het uitvoeren van de taak waar problemen binnen de invoer mediabestanden fout veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="e2428-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="e2428-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="e2428-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="e2428-120">Categorie van fouten waar de bestanden die worden geleverd door de Mediaprocessor kan niet worden verwerkt - media-indeling niet ondersteund of komt niet overeen met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="e2428-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="e2428-121">Bijvoorbeeld, probeert te produceren van een alleen audio-uitvoer van een activum met alleen video</span><span class="sxs-lookup"><span data-stu-id="e2428-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="e2428-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="e2428-122">ErrorProcessingTask</span></span> |<span data-ttu-id="e2428-123">De categorie van andere fouten die de Mediaprocessor tegenkomt tijdens het verwerken van de taak die niet aan de inhoud.</span><span class="sxs-lookup"><span data-stu-id="e2428-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="e2428-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="e2428-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="e2428-125">Categorie van fouten tijdens het uploaden van de uitvoerasset</span><span class="sxs-lookup"><span data-stu-id="e2428-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="e2428-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="e2428-126">ErrorCancelingTask</span></span> |<span data-ttu-id="e2428-127">Categorie van fouten voor fouten bij het annuleren van de taak</span><span class="sxs-lookup"><span data-stu-id="e2428-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="e2428-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="e2428-128">TransientError</span></span> |<span data-ttu-id="e2428-129">Categorie van fouten voor tijdelijke problemen (bv.</span><span class="sxs-lookup"><span data-stu-id="e2428-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="e2428-130">tijdelijke netwerkproblemen met Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="e2428-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="e2428-131">Voor hulp van de **Media Services** team, open een [ondersteunen ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="e2428-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e2428-132">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="e2428-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2428-133">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="e2428-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="e2428-134">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="e2428-134">Related articles</span></span>
* [<span data-ttu-id="e2428-135">Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen</span><span class="sxs-lookup"><span data-stu-id="e2428-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="e2428-136">Quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="e2428-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
