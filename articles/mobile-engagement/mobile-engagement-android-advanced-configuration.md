---
title: aaaAdvanced configuratie voor Azure Mobile Engagement Android SDK
description: Hierin wordt beschreven Hallo geavanceerde configuratieopties, met inbegrip van Hallo Android Manifest met Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="134c4-103">Geavanceerde configuratie voor Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="134c4-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="134c4-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="134c4-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="134c4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="134c4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="134c4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="134c4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="134c4-107">Android</span><span class="sxs-lookup"><span data-stu-id="134c4-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="134c4-108">Deze procedure wordt beschreven hoe tooconfigure verschillende configuratieopties voor Azure Mobile Engagement Android-apps.</span><span class="sxs-lookup"><span data-stu-id="134c4-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="134c4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="134c4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="134c4-110">Machtigingsvereisten</span><span class="sxs-lookup"><span data-stu-id="134c4-110">Permission Requirements</span></span>
<span data-ttu-id="134c4-111">Sommige opties vereisen specifieke machtigingen, die hier worden weergegeven voor de referentie- en in de regel in een specifieke functie Hallo.</span><span class="sxs-lookup"><span data-stu-id="134c4-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="134c4-112">Toevoegen van deze machtigingen toohello AndroidManifest.xml van uw project direct vóór of na Hallo `<application>` label.</span><span class="sxs-lookup"><span data-stu-id="134c4-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="134c4-113">Hallo machtiging code moet toolook zoals Hallo volgende, waarbij u de juiste machtiging Hallo van de volgende tabel Hallo invullen.</span><span class="sxs-lookup"><span data-stu-id="134c4-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="134c4-114">Machtiging</span><span class="sxs-lookup"><span data-stu-id="134c4-114">Permission</span></span> | <span data-ttu-id="134c4-115">Wanneer gebruikt</span><span class="sxs-lookup"><span data-stu-id="134c4-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="134c4-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="134c4-116">INTERNET</span></span> |<span data-ttu-id="134c4-117">Vereist.</span><span class="sxs-lookup"><span data-stu-id="134c4-117">Required.</span></span> <span data-ttu-id="134c4-118">Voor eenvoudige rapportage</span><span class="sxs-lookup"><span data-stu-id="134c4-118">For basic reporting</span></span> |
| <span data-ttu-id="134c4-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="134c4-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="134c4-120">Vereist.</span><span class="sxs-lookup"><span data-stu-id="134c4-120">Required.</span></span> <span data-ttu-id="134c4-121">Voor eenvoudige rapportage</span><span class="sxs-lookup"><span data-stu-id="134c4-121">For basic reporting</span></span> |
| <span data-ttu-id="134c4-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="134c4-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="134c4-123">Vereist.</span><span class="sxs-lookup"><span data-stu-id="134c4-123">Required.</span></span> <span data-ttu-id="134c4-124">tooshow van Hallo meldingen center na opnieuw opstarten van apparaat</span><span class="sxs-lookup"><span data-stu-id="134c4-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="134c4-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="134c4-125">WAKE_LOCK</span></span> |<span data-ttu-id="134c4-126">Aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="134c4-126">Recommended.</span></span> <span data-ttu-id="134c4-127">Schakelt het verzamelen van gegevens bij gebruik van Wi-Fi of als het scherm is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="134c4-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="134c4-128">TRILLEN</span><span class="sxs-lookup"><span data-stu-id="134c4-128">VIBRATE</span></span> |<span data-ttu-id="134c4-129">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="134c4-129">Optional.</span></span> <span data-ttu-id="134c4-130">Trillingen ingeschakeld wanneer er worden meldingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="134c4-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="134c4-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="134c4-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="134c4-132">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="134c4-132">Optional.</span></span> <span data-ttu-id="134c4-133">Hiermee kunt Android grote afbeelding melding</span><span class="sxs-lookup"><span data-stu-id="134c4-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="134c4-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="134c4-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="134c4-135">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="134c4-135">Optional.</span></span> <span data-ttu-id="134c4-136">Hiermee kunt Android grote afbeelding melding</span><span class="sxs-lookup"><span data-stu-id="134c4-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="134c4-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="134c4-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="134c4-138">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="134c4-138">Optional.</span></span> <span data-ttu-id="134c4-139">Rapportage van realtime locatie kunt</span><span class="sxs-lookup"><span data-stu-id="134c4-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="134c4-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="134c4-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="134c4-141">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="134c4-141">Optional.</span></span> <span data-ttu-id="134c4-142">Schakelt op basis van een GPS-locatie rapportage</span><span class="sxs-lookup"><span data-stu-id="134c4-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="134c4-143">Vanaf Android M [sommige machtigingen worden beheerd tijdens runtime](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="134c4-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="134c4-144">Als u al ``ACCESS_FINE_LOCATION``, hoeft u geen tooalso gebruiken ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="134c4-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="134c4-145">Android Manifest configuratieopties</span><span class="sxs-lookup"><span data-stu-id="134c4-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="134c4-146">Foutrapportage</span><span class="sxs-lookup"><span data-stu-id="134c4-146">Crash report</span></span>
<span data-ttu-id="134c4-147">foutenrapporten toodisable, voeg deze code tussen Hallo `<application>` en `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="134c4-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="134c4-148">Burst drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="134c4-148">Burst threshold</span></span>
<span data-ttu-id="134c4-149">Standaard Hallo Engagement servicerapporten Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="134c4-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="134c4-150">Als uw rapport toepassingslogboeken vaak verschillen, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base ('burst modus' genoemd).</span><span class="sxs-lookup"><span data-stu-id="134c4-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="134c4-151">dus, voeg deze code tussen Hallo toodo `<application>` en `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="134c4-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="134c4-152">Burst-modus enigszins verhoogt de batterij Hallo maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken).</span><span class="sxs-lookup"><span data-stu-id="134c4-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="134c4-153">De drempelwaarde burst mag niet langer zijn dan 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="134c4-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="134c4-154">Sessietime-out</span><span class="sxs-lookup"><span data-stu-id="134c4-154">Session timeout</span></span>
 <span data-ttu-id="134c4-155">U kunt een activiteit beëindigen door Hallo drukken **Start** of **terug** sleutel telefonisch instelling Hallo inactief of door te gaan naar een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="134c4-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="134c4-156">Standaard wordt een sessie tien seconden na het einde van de laatste activiteit Hallo beëindigd.</span><span class="sxs-lookup"><span data-stu-id="134c4-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="134c4-157">Zo voorkomt u een sessie-splitsing van elke gebruiker tijd hello wordt afgesloten en retourneert toohello toepassing snel, dat kan gebeuren wanneer Hallo gebruiker opneemt in een afbeelding controleert een melding, enzovoort. U kunt deze parameter toomodify.</span><span class="sxs-lookup"><span data-stu-id="134c4-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="134c4-158">dus, voeg deze code tussen Hallo toodo `<application>` en `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="134c4-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="134c4-159">Melden van logboek uitschakelen</span><span class="sxs-lookup"><span data-stu-id="134c4-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="134c4-160">Met behulp van een methodeaanroep van</span><span class="sxs-lookup"><span data-stu-id="134c4-160">Using a method call</span></span>
<span data-ttu-id="134c4-161">Als u Engagement toostop logboeken verzenden wilt, kunt u bellen:</span><span class="sxs-lookup"><span data-stu-id="134c4-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="134c4-162">Deze aanroep is permanent: een gedeelde voorkeuren-bestand wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="134c4-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="134c4-163">Als bij het aanroepen van deze functie Engagement actief is, kan een minuut voor Hallo service toostop duren.</span><span class="sxs-lookup"><span data-stu-id="134c4-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="134c4-164">Maar deze won't start Hallo-service op alle Hallo volgende keer dat u de toepassing hello starten.</span><span class="sxs-lookup"><span data-stu-id="134c4-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="134c4-165">U kunt reporting opnieuw door het aanroepen van dezelfde functie met Hallo logboek inschakelen `true`.</span><span class="sxs-lookup"><span data-stu-id="134c4-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="134c4-166">Integratie in uw eigen`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="134c4-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="134c4-167">In plaats van deze functie aanroept, kunt u deze instelling ook integreren rechtstreeks in uw bestaande `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="134c4-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="134c4-168">U kunt Engagement toouse uw voorkeuren bestand (met de gewenste modus Hallo) configureren in Hallo `AndroidManifest.xml` het bestand met `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="134c4-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="134c4-169">Hallo `engagement:agent:settings:name` sleutel is de naam van de gebruikte toodefine Hallo van Hallo gedeelde voorkeurenbestand.</span><span class="sxs-lookup"><span data-stu-id="134c4-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="134c4-170">Hallo `engagement:agent:settings:mode` sleutel gebruikte toodefine Hallo modus van Hallo gedeelde voorkeurenbestand is.</span><span class="sxs-lookup"><span data-stu-id="134c4-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="134c4-171">Gebruik dezelfde Hallo-modus als in uw `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="134c4-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="134c4-172">Hallo-modus moet worden doorgegeven als een getal: als u een combinatie van constante vlaggen in uw code gebruikt, controleert u Hallo totale waarde.</span><span class="sxs-lookup"><span data-stu-id="134c4-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="134c4-173">Engagement altijd gebruikt Hallo `engagement:key` Booleaanse sleutel binnen Hallo voorkeurenbestand voor het beheren van deze instelling.</span><span class="sxs-lookup"><span data-stu-id="134c4-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="134c4-174">Hallo volgende voorbeeld van `AndroidManifest.xml` toont Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="134c4-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="134c4-175">Vervolgens kunt u toevoegen een `CheckBoxPreference` in de indeling van uw voorkeur zoals Hallo volgt:</span><span class="sxs-lookup"><span data-stu-id="134c4-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
