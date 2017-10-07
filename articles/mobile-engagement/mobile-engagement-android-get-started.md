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
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Aan de slag met Azure Mobile Engagement voor Android-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Android-toepassing.
Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement. U maakt een lege Android-app die basisgegevens verzamelt en pushmeldingen ontvangt via Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Vereisten
Voltooiing van deze zelfstudie vereist Hallo [Android Developer Tools](https://developer.android.com/sdk/index.html), waaronder Hallo Android Studio geïntegreerde ontwikkelomgeving en Hallo meest recente Android-platform.

Vereist ook Hallo [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete in deze zelfstudie, moet u een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started) voor meer informatie.
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Mobile Engagement instellen voor uw Android-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. U kunt een eenvoudige app maken met Android Studio toodemonstrate Hallo-integratie.

de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement Android SDK-integratie](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Een Android-project maken
1. Start **Android Studio**, en selecteer in het pop-upvenster Hallo **Start een nieuw Android Studio-project**.

    ![][1]
2. Geef een naam voor de app en het bedrijfsdomein op. Schrijf op wat u invult, omdat u deze gegevens later nodig hebt. Klik op **Volgende**.

    ![][2]
3. Selecteer de doel-vormfactor Hallo en API-niveau en klikt u op **volgende**.

   > [!NOTE]
   > Mobile Engagement vereist minimaal API-niveau 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Selecteer **Blank Activity** hier, namelijk alleen welkomstscherm voor deze app en klik op **volgende**.

    ![][4]
5. Ten slotte laat Hallo standaardwaarden en klik op **voltooien**.

    ![][5]

Android Studio maakt nu Hallo demo-app waarin we Mobile Engagement integreren.

### <a name="include-hello-sdk-library-in-your-project"></a>Hallo SDK-bibliotheek opnemen in uw project
1. Hallo downloaden [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).
2. Pak Hallo bestand tooa archiefmap op uw computer.
3. Hallo JAR-bibliotheek voor de huidige versie van deze SDK Hallo identificeren en toohello Klembord te kopiëren.

      ![][6]
4. Navigeer toohello **Project** sectie (1) en plak Hallo JAR in de map voor Hallo libs (2).

      ![][7]
5. tooload hello bibliotheek sync Hallo project.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Verbinding maken met uw app tooMobile back-end Engagement Hello verbindingsreeks
1. Kopieer Hallo volgende regels code in Hallo activiteit maken (moet worden uitgevoerd op één plek van uw toepassing, meestal Hallo belangrijkste activiteit). Voor deze voorbeeld-app openen up Hallo MainActivity onder src -> main -> java en voeg de volgende Hallo:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Hallo verwijzingen oplossen door op Alt + Enter te drukken of Hallo volgende importinstructies toe te voegen:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Ga terug toohello klassieke Azure-Portal in uw app **verbindingsgegevens** pagina en kopieer Hallo **verbindingsreeks**.

      ![][9]
4. Plak deze in Hallo `setConnectionString` parameter Hallo hele tekenreeks die wordt weergegeven in de volgende code Hallo vervangen:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Machtigingen en een servicedeclaratie toevoegen
1. Toevoegen van deze machtigingen toohello Manifest.xml van uw project direct vóór of na Hallo `<application>` tag:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare Hallo agent-service, voeg deze code tussen Hallo `<application>` en `</application>` tags:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. In de code Hallo u hebt geplakt, vervangt u `"<Your application name>"` Hallo label, die wordt weergegeven in Hallo **instellingen** menu waar u de services die worden uitgevoerd op Hallo-apparaat kunt zien. U kunt bijvoorbeeld Hallo woord 'Service' aan dat label toevoegen.

### <a name="send-a-screen-toomobile-engagement"></a>Een scherm tooMobile Engagement verzenden
toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn, moet u ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden.

Ga te**MainActivity.java** en Voeg na tooreplace Hallo basisklasse van Hallo **MainActivity** te**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Als de basisklasse niet *activiteit*, raadpleegt u [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) voor het tooinherit van verschillende klassen.
>
>

Hallo volgt regel voor dit eenvoudige voorbeeldscenario uitcommentariëren:

    // setSupportActionBar(toolbar);

Als u wilt dat tookeep hello `ActionBar` in uw app Zie [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Pushmeldingen en in-app-berichten inschakelen
Tijdens een campagne kunt u met Mobile Engagement met uw gebruikers communiceren en ze bereiken met pushmeldingen en in-app-berichten. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende sectie stelt u uw app tooreceive ze.

### <a name="copy-sdk-resources-in-your-project"></a>SDK-bronnen naar uw project kopiëren
1. Navigeer terug tooyour SDK downloaden van inhoud en kopieer Hallo **res** map.

    ![][10]
2. Ga terug tooAndroid Studio, selecteer Hallo **belangrijkste** map van uw projectbestanden en plak deze tooadd Hallo resources tooyour project.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Volgende stappen
Ga te[Android SDK](mobile-engagement-android-sdk-overview.md) tooget gedetailleerde kennis over Hallo SDK-integratie.

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
