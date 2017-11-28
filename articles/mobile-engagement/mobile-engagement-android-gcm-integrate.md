---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="da30d-103">Hoe tooIntegrate GCM met Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="da30d-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="da30d-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="da30d-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="da30d-105">Dit document is alleen nuttig als u al geïntegreerde Hallo module en plan toopush Google Play apparaten bereiken.</span><span class="sxs-lookup"><span data-stu-id="da30d-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="da30d-106">toointegrate Reach-campagnes in uw toepassing, lees eerst hoe tooIntegrate Engagement bereiken op Android.</span><span class="sxs-lookup"><span data-stu-id="da30d-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="da30d-107">Inleiding</span><span class="sxs-lookup"><span data-stu-id="da30d-107">Introduction</span></span>
<span data-ttu-id="da30d-108">Integratie van GCM, kunt uw toepassing toobe gepusht.</span><span class="sxs-lookup"><span data-stu-id="da30d-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="da30d-109">GCM-nettoladingen toohello SDK altijd gepusht bevatten Hallo `azme` sleutel in het Hallo-gegevensobject.</span><span class="sxs-lookup"><span data-stu-id="da30d-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="da30d-110">Dus als u GCM voor een ander doel in uw toepassing gebruiken, kunt u filteren op basis van die sleutel pushes.</span><span class="sxs-lookup"><span data-stu-id="da30d-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da30d-111">Alleen apparaten met Android 2.2 of hoger, met Google Play geïnstalleerd en met Google achtergrond verbinding ingeschakeld kan worden geactiveerd via GCM; u kunt echter integreren deze code veilig op niet-ondersteunde apparaten (alleen intents wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="da30d-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="da30d-112">Met API-sleutel een Google Cloud Messaging-project maken</span><span class="sxs-lookup"><span data-stu-id="da30d-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="da30d-113">SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="da30d-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="da30d-114">Het beheren van apparaat-registraties</span><span class="sxs-lookup"><span data-stu-id="da30d-114">Managing device registrations</span></span>
<span data-ttu-id="da30d-115">Elk apparaat een opdracht registratie toohello moet verzenden Google-servers, anders ze kunnen niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="da30d-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="da30d-116">Een apparaat kan ook Hef de registratie van GCM-meldingen (Hallo apparaat wordt automatisch verwijderd als toepassing hello wordt verwijderd).</span><span class="sxs-lookup"><span data-stu-id="da30d-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="da30d-117">Als u geen [Google Play-SDK] of u niet al verzend Hallo registratie opzet, kunt u Engagement Hallo apparaat automatisch voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="da30d-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="da30d-118">tooenable dit toevoegen Hallo tooyour na `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag:</span><span class="sxs-lookup"><span data-stu-id="da30d-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="da30d-119">Registratie-id toohello Engagement Push service communiceren en meldingen ontvangen</span><span class="sxs-lookup"><span data-stu-id="da30d-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="da30d-120">In de volgorde toocommunicate Hallo registratie-id van Hallo apparaat toohello Engagement Push service en de meldingen ontvangen, Hallo na tooyour toevoegen `AndroidManifest.xml` bestand binnen Hallo `<application/>` tag (zelfs als u apparaten registraties zelf beheren):</span><span class="sxs-lookup"><span data-stu-id="da30d-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="da30d-121">Zorg ervoor dat u hebt Hallo volgende machtigingen in uw `AndroidManifest.xml` (na Hallo `</application>` label).</span><span class="sxs-lookup"><span data-stu-id="da30d-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="da30d-122">Verleen Mobile Engagement toegang tooyour GCM-API-sleutel</span><span class="sxs-lookup"><span data-stu-id="da30d-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="da30d-123">Ga als volgt [in deze handleiding](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement toegang tooyour GCM-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="da30d-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google Play-SDK]:https://developers.google.com/cloud-messaging/android/start
