---
title: aaaGet gestart met Azure Mobile Engagement voor Xamarin.Android
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Xamarin.Android-Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Aan de slag met Azure Mobile Engagement voor Xamarin.Android-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Xamarin.Android-toepassing.
Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement. U maakt een lege Xamarin.Android-app die basisgegevens verzamelt en pushmeldingen ontvangt via Google Cloud Messaging (GCM).

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

Deze zelfstudie vereist de volgende Hallo:

* [Xamarin Studio](http://xamarin.com/studio). U kunt ook Visual Studio gebruiken met Xamarin, maar deze zelfstudie gebruikt Xamarin Studio. Zie [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installatie voor Visual Studio en Xamarin) voor installatie-instructies.
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. 

We gaan een eenvoudige app maken met Xamarin Studio toodemonstrate Hallo-integratie.

### <a name="create-a-new-xamarinandroid-project"></a>Een nieuw Xamarin.Android-project maken
1. Start **Xamarin Studio** te gaan**bestand** -> **nieuw** -> **oplossing** 
   
    ![][1]
2. Selecteer **Android-App** zorgt u ervoor Hallo geselecteerde taal **C#** en klik op **volgende**.
   
    ![][2]
3. Vul Hallo **Appnaam** en Hallo **organisatie-id**. Zorg ervoor dat toocheckmark **Google Play Services** en klik vervolgens op **volgende**. 
   
    ![][3]
4. Update Hallo **projectnaam**, **oplossingsnaam** en **locatie** indien nodig, en klik op **maken**.
   
    ![][4]

Xamarin Studio maakt Hallo-app waarin we Mobile Engagement gaan integreren. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Klik met de rechtermuisknop op Hallo **pakketten** map in Hallo Solution en selecteer **pakketten toevoegen...**
   
    ![][5]
2. Zoeken naar Hallo **Microsoft Azure Mobile Engagement Xamarin SDK** en toe te voegen tooyour oplossing.  
   
    ![][6]
3. Open **MainActivity.cs** en voeg de volgende Hallo using-instructies:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. In Hallo `OnCreate` methode toevoegen Hallo tooinitialize Hallo verbinding met de back-end van Mobile Engagement te volgen. Zorg ervoor dat tooadd uw **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Machtigingen en een servicedeclaratie toevoegen
1. Open Hallo **Manifest.xml** bestand in map Hallo-eigenschappen. Selecteer het tabblad Source zodat u Hallo XML-bron direct kunt bijwerken.
2. Toevoegen van deze machtigingen toohello Manifest.xml (dat zich bevindt onder Hallo **eigenschappen** map) van uw project direct vóór of na Hallo `<application>` tag:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Voeg de volgende Hallo tussen Hallo `<application>` en `</application>` tags toodeclare Hallo agent-service:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. In de code Hallo u zojuist hebt geplakt, vervangt u `"<Your application name>"` in Hallo label. Dit wordt weergegeven in Hallo **instellingen** menu waar gebruikers de services die worden uitgevoerd op Hallo apparaat kunnen zien. U kunt bijvoorbeeld Hallo woord 'Service' aan dat label toevoegen.

### <a name="send-a-screen-toomobile-engagement"></a>Een scherm tooMobile Engagement verzenden
U moet ten minste één scherm toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen Hallo gebruikers actief zijn. Om dit te doen-Zorg ervoor dat Hallo `MainActivity` neemt over van `EngagementActivity` in plaats van `Activity`.

    public class MainActivity : EngagementActivity

Als u niet kunt overnemen van `EngagementActivity`, moet u vervolgens de methode `.StartActivity` en `.EndActivity` toevoegen in respectievelijk `OnResume` en `OnPause`.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract met en uw gebruikers met pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
