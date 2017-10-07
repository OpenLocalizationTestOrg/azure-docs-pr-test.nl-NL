---
title: AAA beheren snelheid en gelijktijdigheid van uw codering met Azure Media Services | Microsoft Docs
description: Dit artikel bevat een kort overzicht van hoe u de snelheid en gelijktijdigheid van uw codering taken/taken met Azure Media Services kunt beheren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="66a13-103">Snelheid en gelijktijdigheid van uw codering beheren</span><span class="sxs-lookup"><span data-stu-id="66a13-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="66a13-104">Dit artikel bevat een kort overzicht van hoe u de snelheid en gelijktijdigheid van uw codering taken/taken kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="66a13-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="66a13-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="66a13-105">Overview</span></span>

<span data-ttu-id="66a13-106">In Media Services een **gereserveerde eenheidstype** bepaalt Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="66a13-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="66a13-107">U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**.</span><span class="sxs-lookup"><span data-stu-id="66a13-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="66a13-108">Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type.</span><span class="sxs-lookup"><span data-stu-id="66a13-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="66a13-109">Hallo [codering eenheden schalen](media-services-scale-media-processing-overview.md) onderwerp bevat een tabel waarmee u de beslissing nemen bij de keuze tussen verschillende codering snelheid te koppelen.</span><span class="sxs-lookup"><span data-stu-id="66a13-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="66a13-110">Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden**.</span><span class="sxs-lookup"><span data-stu-id="66a13-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="66a13-111">het aantal ingerichte gereserveerde eenheden Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.</span><span class="sxs-lookup"><span data-stu-id="66a13-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="66a13-112">Bijvoorbeeld, als uw account vijf gereserveerde eenheden, heeft en vervolgens vijf media taken wordt gelijktijdig zo lang worden uitgevoerd als er zijn taken toobe verwerkt.</span><span class="sxs-lookup"><span data-stu-id="66a13-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="66a13-113">de resterende taken Hallo wachttijd in wachtrij Hallo en wordt ophalen opgepikt sequentieel worden verwerkt wanneer een actieve taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="66a13-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="66a13-114">Als een account heeft geen geen gereserveerde eenheden die zijn ingericht, zullen vervolgens taken worden opgepikt sequentieel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="66a13-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="66a13-115">In dit geval Hallo wachttijd tussen een taak is voltooid en hello naast een starten is afhankelijk Hallo beschikbaarheid van resources in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="66a13-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="66a13-116">Voor gedetailleerde informatie over en voorbeelden die tonen hoe tooscale codering eenheden, Zie [dit](media-services-scale-media-processing-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="66a13-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="66a13-117">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="66a13-117">Next step</span></span>

[<span data-ttu-id="66a13-118">Codering schaaleenheden</span><span class="sxs-lookup"><span data-stu-id="66a13-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="66a13-119">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="66a13-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="66a13-120">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="66a13-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

