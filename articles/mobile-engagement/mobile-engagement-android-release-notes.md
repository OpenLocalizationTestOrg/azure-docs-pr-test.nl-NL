---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a><span data-ttu-id="c45ff-103">Releaseopmerkingen</span><span class="sxs-lookup"><span data-stu-id="c45ff-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="c45ff-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="c45ff-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="c45ff-105">Herstel van een crash die zelden optreden kan bij het aanroepen van `EngagementAgentUtils.isInDedicatedEngagementProcess`, die ook wordt gebruikt door Hallo `EngagementApplication` klasse.</span><span class="sxs-lookup"><span data-stu-id="c45ff-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="c45ff-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="c45ff-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="c45ff-107">Android 8-ondersteuning (vorige versies van Hallo SDK niet in Android 8 werken).</span><span class="sxs-lookup"><span data-stu-id="c45ff-107">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="c45ff-108">Er is geen meer afhankelijkheid van ondersteuningsbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="c45ff-108">No more dependency on support library.</span></span>
* <span data-ttu-id="c45ff-109">Verwijder `EngagementFragmentActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="c45ff-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="c45ff-110">Vervaldatum te[achtergrond uitvoering limieten](https://developer.android.com/preview/features/background.html) op Android 8 logboeken op de achtergrond kunnen worden uitgesteld totdat Hallo gebruiker werkt met Hallo-apparaat, wordt dit een invloed hebben op campagne Push **geleverd** en **Systeemmelding weergegeven** statistieken als Hallo-apparaat is in de slaapstand wordt uitgesteld (Hallo melding nog wel weergegeven, wordt ring en Trillen in realtime zonder problemen).</span><span class="sxs-lookup"><span data-stu-id="c45ff-110">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="c45ff-111">Vervaldatum te[achtergrond locatie limieten](https://developer.android.com/preview/features/background-location-limits.html), Hallo realtime locatie op de achtergrond wordt niet vaak op Android 8 worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c45ff-111">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="c45ff-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="c45ff-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="c45ff-113">Herstel in-app-melding tekstkleuren op Android 7 toobe Hallo dezelfde als oudere versies van Android.</span><span class="sxs-lookup"><span data-stu-id="c45ff-113">Fix in-app notification text colors on Android 7 toobe hello same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="c45ff-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="c45ff-115">Er is geen meer Wi-Fi-vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="c45ff-115">No more WIFI lock.</span></span>
* <span data-ttu-id="c45ff-116">Herstel een impasse aangetroffen bij het aanroepen van getDeviceId voordat init (fout die is geïntroduceerd in 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="c45ff-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="c45ff-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="c45ff-118">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="c45ff-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="c45ff-120">Beveiliging: uitschakelen webtoegang weergave lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="c45ff-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="c45ff-121">Beveiliging: Verwijder `EngagementPreferenceActivity` klasse die uitgebreider is verouderd en niet-beveiligde `PreferenceActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="c45ff-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="c45ff-122">Beveiliging: reach activiteiten nu zijn gedocumenteerd toouse `exported="false"`, deze vlag kan ook worden gebruikt in eerdere versies van de SDK.</span><span class="sxs-lookup"><span data-stu-id="c45ff-122">Security: reach activities are now documented toouse `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="c45ff-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="c45ff-124">Hallo SDK is nu een licentie verleend onder MIT.</span><span class="sxs-lookup"><span data-stu-id="c45ff-124">hello SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="c45ff-125">Toestaan dat een aangepast apparaat-id opgeven bij het initialiseren SDK.</span><span class="sxs-lookup"><span data-stu-id="c45ff-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="c45ff-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="c45ff-127">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="c45ff-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="c45ff-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="c45ff-129">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="c45ff-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="c45ff-131">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="c45ff-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="c45ff-133">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="c45ff-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="c45ff-135">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="c45ff-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="c45ff-137">Nieuw model voor machtiging verwerken voor Android M.</span><span class="sxs-lookup"><span data-stu-id="c45ff-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="c45ff-138">Kunnen nu functies configureren voor locatie tijdens runtime in plaats van `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="c45ff-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="c45ff-139">Een machtiging fout oplossen: als u `ACCESS_FINE_LOCATION`, klikt u vervolgens `ACCESS_COARSE_LOCATION` niet meer nodig is.</span><span class="sxs-lookup"><span data-stu-id="c45ff-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="c45ff-140">Verbeteringen in stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="c45ff-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="c45ff-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="c45ff-142">Interne protocol wijzigingen toomake analyses en pushmeldingen betrouwbaarder.</span><span class="sxs-lookup"><span data-stu-id="c45ff-142">Internal protocol changes toomake analytics and push more reliable.</span></span>
* <span data-ttu-id="c45ff-143">Native pushberichten (GCM/ADM) is nu ook gebruikt voor in de app-meldingen zodat u Hallo native pushreferenties voor elk type pushcampagne moet configureren.</span><span class="sxs-lookup"><span data-stu-id="c45ff-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="c45ff-144">Grote afbeelding melding oplossen: ze zijn weergegeven alleen per 10 na wordt gepusht.</span><span class="sxs-lookup"><span data-stu-id="c45ff-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="c45ff-145">Herstel van een fout in de webweergave: Hallo standaard actie-URL is ook uitvoeren op een koppeling te klikken.</span><span class="sxs-lookup"><span data-stu-id="c45ff-145">Fix a bug in web view: clicking on a link was also executing hello default action URL.</span></span>
* <span data-ttu-id="c45ff-146">Los het vastlopen van een zeldzame gerelateerde toolocal opslagbeheer.</span><span class="sxs-lookup"><span data-stu-id="c45ff-146">Fix a rare crash related toolocal storage management.</span></span>
* <span data-ttu-id="c45ff-147">Los de dynamische configuratie tekenreeks management.</span><span class="sxs-lookup"><span data-stu-id="c45ff-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="c45ff-148">Bijwerken van de gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="c45ff-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="c45ff-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="c45ff-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="c45ff-150">Initiële versie van Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c45ff-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="c45ff-151">appId-configuratie wordt vervangen door de configuratie van een verbinding-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c45ff-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="c45ff-152">API-toosend verwijderd en willekeurige XMPP berichten ontvangen van willekeurige XMPP entiteiten.</span><span class="sxs-lookup"><span data-stu-id="c45ff-152">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="c45ff-153">API-toosend verwijderd en kunnen berichten tussen apparaten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c45ff-153">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="c45ff-154">Verbeterde beveiliging.</span><span class="sxs-lookup"><span data-stu-id="c45ff-154">Security improvements.</span></span>
* <span data-ttu-id="c45ff-155">Google Play en SmartAd bijhouden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c45ff-155">Google Play and SmartAd tracking removed.</span></span>

