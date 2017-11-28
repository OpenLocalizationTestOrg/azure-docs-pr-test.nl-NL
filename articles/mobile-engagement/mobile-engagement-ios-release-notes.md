---
title: Mobile Engagement iOS SDK-releaseopmerkingen aaaAzure | Microsoft Docs
description: Meest recente updates en procedures voor iOS SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="12697-103">Azure Mobile Engagement iOS SDK-releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="12697-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="12697-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="12697-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="12697-105">Vaste badges uitgeschakeld op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="12697-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="12697-106">Vaste waarschuwingen op 9 over API's niet aangeroepen in hoofdwachtrij XCode.</span><span class="sxs-lookup"><span data-stu-id="12697-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="12697-107">Een geheugenlek vast Reach polls.</span><span class="sxs-lookup"><span data-stu-id="12697-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="12697-108">Ondersteuning voor iOS verwijderd 6.X.</span><span class="sxs-lookup"><span data-stu-id="12697-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="12697-109">Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 7.</span><span class="sxs-lookup"><span data-stu-id="12697-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="12697-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="12697-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="12697-111">Verbeterde levering van het logboek op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="12697-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="12697-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="12697-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="12697-113">Vaste melding niet worden ondernomen op iOS-10-apparaten.</span><span class="sxs-lookup"><span data-stu-id="12697-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="12697-114">Afschaffen XCode 7.</span><span class="sxs-lookup"><span data-stu-id="12697-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="12697-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="12697-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="12697-116">Vaste aggregatie tussen technische logboeken en andere logboeken.</span><span class="sxs-lookup"><span data-stu-id="12697-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="12697-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="12697-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="12697-118">Vaste Hallo bug waar de leveringsfeedback is niet gemeld wanneer de app op de achtergrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="12697-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="12697-119">Voor optimale Hallo technische logboeken worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="12697-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="12697-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="12697-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="12697-121">Vaste bug op HTTP-aanvraag annulering waarmee toocrash soms wordt geleid.</span><span class="sxs-lookup"><span data-stu-id="12697-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="12697-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="12697-123">Vaste Hallo vertraging wanneer een nieuw app-exemplaar wordt geactiveerd door een melding met dieptekoppelingen</span><span class="sxs-lookup"><span data-stu-id="12697-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="12697-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="12697-125">Bitcode ingeschakeld in Hallo SDK toomake werkt deze met **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="12697-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="12697-126">Opgeloste gerelateerd tooin-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="12697-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="12697-127">Hallo-in-app-meldingen betrouwbaarder in geval van een laag energieniveau en andere dergelijke scenario's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12697-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="12697-128">Extra console-logboeken die worden gegenereerd door 3e partij bibliotheek verwijderd.</span><span class="sxs-lookup"><span data-stu-id="12697-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="12697-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="12697-130">Oplossingen voor iOS 9-compatibiliteit met een bibliotheek van derden oplossen.</span><span class="sxs-lookup"><span data-stu-id="12697-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="12697-131">Het is crashes veroorzaakt tijdens het verzenden van resultaten, toepassingsinformatie of extra gegevens worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="12697-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="12697-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="12697-133">Mobile Engagement gebruikt achtergrond-Pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="12697-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="12697-134">Ondersteuning voor iOS verwijderd 4.X.</span><span class="sxs-lookup"><span data-stu-id="12697-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="12697-135">Vanaf deze versie Hallo implementatiedoel van uw toepassing moet ten minste iOS 6.</span><span class="sxs-lookup"><span data-stu-id="12697-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="12697-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="12697-137">Hallo Mobile Engagement apparaat-id voor apparaten < iOS 6 is nu gebaseerd op een GUID die wordt gegenereerd tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="12697-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="12697-138">2.1.0 (04/24/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="12697-139">Toegevoegde Swift compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="12697-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="12697-140">Wanneer op een melding te klikken, uitgevoerd Hallo actie-URL nu is rechts nadat de toepassing hello wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="12697-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="12697-141">Toegevoegde ontbrekende headerbestand in de SDK-pakket.</span><span class="sxs-lookup"><span data-stu-id="12697-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="12697-142">Een probleem opgelost wanneer Hallo Mobile Engagement crash Rapportagefout is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="12697-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="12697-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="12697-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="12697-144">Initiële versie van Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="12697-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="12697-145">appId/sdkKey configuratie wordt vervangen door de configuratie van een verbinding-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="12697-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="12697-146">API-toosend verwijderd en willekeurige XMPP berichten ontvangen van willekeurige XMPP entiteiten.</span><span class="sxs-lookup"><span data-stu-id="12697-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="12697-147">API-toosend verwijderd en kunnen berichten tussen apparaten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="12697-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="12697-148">Verbeterde beveiliging.</span><span class="sxs-lookup"><span data-stu-id="12697-148">Security improvements.</span></span>
* <span data-ttu-id="12697-149">SmartAd bijhouden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="12697-149">SmartAd tracking removed.</span></span>
