---
title: aaaGet gestart met Android-Apps Azure Mobile Engagement
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor Android-apps.
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="0a2f1-103">Aan de slag met Azure Mobile Engagement voor Android-apps</span><span class="sxs-lookup"><span data-stu-id="0a2f1-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="0a2f1-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="0a2f1-105">Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="0a2f1-106">U maakt een lege Android-app die basisgegevens verzamelt en pushmeldingen ontvangt via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a2f1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0a2f1-107">Prerequisites</span></span>
<span data-ttu-id="0a2f1-108">Voltooiing van deze zelfstudie vereist Hallo [Android Developer Tools](https://developer.android.com/sdk/index.html), waaronder Hallo Android Studio geïntegreerde ontwikkelomgeving en Hallo meest recente Android-platform.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="0a2f1-109">Vereist ook Hallo [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a2f1-110">toocomplete in deze zelfstudie, moet u een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="0a2f1-111">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0a2f1-112">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="0a2f1-113">Mobile Engagement instellen voor uw Android-app</span><span class="sxs-lookup"><span data-stu-id="0a2f1-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="0a2f1-114">Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="0a2f1-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="0a2f1-115">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="0a2f1-116">U kunt een eenvoudige app maken met Android Studio toodemonstrate Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="0a2f1-117">de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement Android SDK-integratie](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="0a2f1-118">Een Android-project maken</span><span class="sxs-lookup"><span data-stu-id="0a2f1-118">Create an Android project</span></span>
1. <span data-ttu-id="0a2f1-119">Start **Android Studio**, en selecteer in het pop-upvenster Hallo **Start een nieuw Android Studio-project**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="0a2f1-120">Geef een naam voor de app en het bedrijfsdomein op.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-120">Provide an app name and company domain.</span></span> <span data-ttu-id="0a2f1-121">Schrijf op wat u invult, omdat u deze gegevens later nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="0a2f1-122">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="0a2f1-123">Selecteer de doel-vormfactor Hallo en API-niveau en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a2f1-124">Mobile Engagement vereist minimaal API-niveau 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="0a2f1-125">Selecteer **Blank Activity** hier, namelijk alleen welkomstscherm voor deze app en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="0a2f1-126">Ten slotte laat Hallo standaardwaarden en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="0a2f1-127">Android Studio maakt nu Hallo demo-app waarin we Mobile Engagement integreren.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="0a2f1-128">Hallo SDK-bibliotheek opnemen in uw project</span><span class="sxs-lookup"><span data-stu-id="0a2f1-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="0a2f1-129">Hallo downloaden [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="0a2f1-130">Pak Hallo bestand tooa archiefmap op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="0a2f1-131">Hallo JAR-bibliotheek voor de huidige versie van deze SDK Hallo identificeren en toohello Klembord te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="0a2f1-132">Navigeer toohello **Project** sectie (1) en plak Hallo JAR in de map voor Hallo libs (2).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="0a2f1-133">tooload hello bibliotheek sync Hallo project.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="0a2f1-134">Verbinding maken met uw app tooMobile back-end Engagement Hello verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="0a2f1-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="0a2f1-135">Kopieer Hallo volgende regels code in Hallo activiteit maken (moet worden uitgevoerd op één plek van uw toepassing, meestal Hallo belangrijkste activiteit).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="0a2f1-136">Voor deze voorbeeld-app openen up Hallo MainActivity onder src -> main -> java en voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="0a2f1-137">Hallo verwijzingen oplossen door op Alt + Enter te drukken of Hallo volgende importinstructies toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="0a2f1-138">Ga terug toohello klassieke Azure-Portal in uw app **verbindingsgegevens** pagina en kopieer Hallo **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="0a2f1-139">Plak deze in Hallo `setConnectionString` parameter Hallo hele tekenreeks die wordt weergegeven in de volgende code Hallo vervangen:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="0a2f1-140">Machtigingen en een servicedeclaratie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0a2f1-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="0a2f1-141">Toevoegen van deze machtigingen toohello Manifest.xml van uw project direct vóór of na Hallo `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="0a2f1-142">toodeclare Hallo agent-service, voeg deze code tussen Hallo `<application>` en `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="0a2f1-143">In de code Hallo u hebt geplakt, vervangt u `"<Your application name>"` Hallo label, die wordt weergegeven in Hallo **instellingen** menu waar u de services die worden uitgevoerd op Hallo-apparaat kunt zien.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="0a2f1-144">U kunt bijvoorbeeld Hallo woord 'Service' aan dat label toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="0a2f1-145">Een scherm tooMobile Engagement verzenden</span><span class="sxs-lookup"><span data-stu-id="0a2f1-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="0a2f1-146">toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn, moet u ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="0a2f1-147">Ga te**MainActivity.java** en Voeg na tooreplace Hallo basisklasse van Hallo **MainActivity** te**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="0a2f1-148">Als de basisklasse niet *activiteit*, raadpleegt u [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) voor het tooinherit van verschillende klassen.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="0a2f1-149">Hallo volgt regel voor dit eenvoudige voorbeeldscenario uitcommentariëren:</span><span class="sxs-lookup"><span data-stu-id="0a2f1-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="0a2f1-150">Als u wilt dat tookeep hello `ActionBar` in uw app Zie [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f1-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="0a2f1-151">App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="0a2f1-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="0a2f1-152">Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="0a2f1-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="0a2f1-153">Tijdens een campagne kunt u met Mobile Engagement met uw gebruikers communiceren en ze bereiken met pushmeldingen en in-app-berichten.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="0a2f1-154">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="0a2f1-155">Hallo volgende sectie stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="0a2f1-156">SDK-bronnen naar uw project kopiëren</span><span class="sxs-lookup"><span data-stu-id="0a2f1-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="0a2f1-157">Navigeer terug tooyour SDK downloaden van inhoud en kopieer Hallo **res** map.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="0a2f1-158">Ga terug tooAndroid Studio, selecteer Hallo **belangrijkste** map van uw projectbestanden en plak deze tooadd Hallo resources tooyour project.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="0a2f1-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a2f1-159">Next steps</span></span>
<span data-ttu-id="0a2f1-160">Ga te[Android SDK](mobile-engagement-android-sdk-overview.md) tooget gedetailleerde kennis over Hallo SDK-integratie.</span><span class="sxs-lookup"><span data-stu-id="0a2f1-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
