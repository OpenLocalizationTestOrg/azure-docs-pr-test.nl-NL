---
title: aaaAzure RemoteApp netwerkbandbreedte - algemene richtlijnen | Microsoft Docs
description: Sommige Basisnetwerk bandbreedte richtlijnen voor uw Azure RemoteApp-collecties en apps te begrijpen.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="7ab86-103">Azure RemoteApp netwerkbandbreedte - algemene richtlijnen (als u niet kunt uw eigen testen)</span><span class="sxs-lookup"><span data-stu-id="7ab86-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7ab86-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="7ab86-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7ab86-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7ab86-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7ab86-106">Als u nog geen Hallo tijd of mogelijkheid toorun hello [netwerk bandbreedte tests](remoteapp-bandwidthtests.md) voor Azure RemoteApp Hier volgen enkele tamelijk algemene richtlijnen kunt u schatten netwerkbandbreedte per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7ab86-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="7ab86-107">Als u een combinatie van deze scenario's hebt, wordt niet aanbevolen iets kleiner zijn dan (of gelijk zijn aan) 10 MB/s zoals Hallo minimale netwerkbandbreedte voor moderne apps met Internet verbonden in een externe omgeving.</span><span class="sxs-lookup"><span data-stu-id="7ab86-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="7ab86-108">(Hoewel zoals besproken, dit wordt niet gegarandeerd dat een beter dan gemiddelde gebruikerservaring.)</span><span class="sxs-lookup"><span data-stu-id="7ab86-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="7ab86-109">Complexe PowerPoint, eenvoudige PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7ab86-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="7ab86-110">Azure RemoteApp komt het beste op 100 MB LAN.</span><span class="sxs-lookup"><span data-stu-id="7ab86-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="7ab86-111">Hallo op 10 MB/s-netwerkprofiel wanneer jitter hoger dan 120 ms meer dan 5% Hallo gebruiker is ziet een gemiddelde ervaring.</span><span class="sxs-lookup"><span data-stu-id="7ab86-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="7ab86-112">1 MB/s Hallo verschillende is ongeautomatiseerde verwerking - bijvoorbeeld in een diavoorstelling, Hallo gebruiker ziet mogelijk ook geen bewegende overgangen helemaal omdat frames worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7ab86-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="7ab86-113">Internet Explorer, gemengde PDF-, PDF, tekst</span><span class="sxs-lookup"><span data-stu-id="7ab86-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="7ab86-114">10 MB/s-netwerkprofiel is sluiten tooLAN in de meeste aspecten.</span><span class="sxs-lookup"><span data-stu-id="7ab86-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="7ab86-115">1 MB/s biedt een OK-ervaring, hoewel er mogelijk nog enkele jitter wanneer een gebruiker terwijl er installatiekopieën op het welkomstscherm zijn.</span><span class="sxs-lookup"><span data-stu-id="7ab86-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="7ab86-116">Flash-video (YouTube)</span><span class="sxs-lookup"><span data-stu-id="7ab86-116">Flash video (YouTube)</span></span>
<span data-ttu-id="7ab86-117">100 MB/s LAN biedt de beste ervaring Hallo terwijl 10 MB/s acceptabel (dat wil zeggen we blijven is van het Hallo-framesnelheid maar jitter toeneemt).</span><span class="sxs-lookup"><span data-stu-id="7ab86-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="7ab86-118">Jitter is 1 MB/s, zeer hoge en merkbare.</span><span class="sxs-lookup"><span data-stu-id="7ab86-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="7ab86-119">Word-typen (Word externe invoer)</span><span class="sxs-lookup"><span data-stu-id="7ab86-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="7ab86-120">Dit is een lage bandbreedte gebruiksscenario.</span><span class="sxs-lookup"><span data-stu-id="7ab86-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="7ab86-121">Om 256 KB/s bieden we een ervaring als LAN goed.</span><span class="sxs-lookup"><span data-stu-id="7ab86-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7ab86-122">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="7ab86-122">Learn more</span></span>
* [<span data-ttu-id="7ab86-123">Gebruik van netwerkbandbreedte Azure RemoteApp schatten</span><span class="sxs-lookup"><span data-stu-id="7ab86-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="7ab86-124">Azure RemoteApp - hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?</span><span class="sxs-lookup"><span data-stu-id="7ab86-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="7ab86-125">Azure RemoteApp - tseting uw gebruik van netwerkbandbreedte met enkele algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="7ab86-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

