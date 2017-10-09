---
title: aaaGet gestart met Azure Mobile Engagement voor Cordova/Phonegap
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Cordova/Phonegap-apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Aan de slag met Azure Mobile Engagement voor Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app gebruiks- en verzenden push notifications toosegmented gebruikers van een mobiele toepassing ontwikkeld met Cordova.

In deze zelfstudie maken we een lege Cordova-app met een Mac en integreren we vervolgens de Mobile Engagement SDK. Deze app verzamelt analytische basisgegevens en ontvangt pushmeldingen via Apple Push Notification System (APNS) voor iOS en Google Cloud Messaging (GCM) voor Android. We implementeert deze tooan iOS of Android-apparaat voor het testen van. 

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started) voor meer informatie.
> 
> 

Deze zelfstudie vereist de volgende Hallo:

* XCode, dat u vanaf de Mac App Store installeren kunt (voor implementatie tooiOS)
* [Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (voor implementatie tooAndroid)
* Pushmeldingscertificaat (.p12), dat u kunt verkrijgen via Apple Dev Center voor APNS
* GCM-projectnummer, dat u kunt vinden in uw Google Developer-Console voor GCM
* [Cordova-invoegtoepassing voor Mobile Engagement](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> U kunt vinden Hallo broncode en hello Leesmij-bestand voor Hallo Cordova-invoegtoepassing op [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw Cordova-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie' hello minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. 

We gaan een eenvoudige app maken met Cordova toodemonstrate Hallo integratie:

### <a name="create-a-new-cordova-project"></a>Nieuw Cordova-project maken
1. Start *Terminal* -venster op uw Mac-computer en typ Hallo maakt u een nieuw Cordova-project uit Hallo standaardsjabloon te volgen. Zorg ervoor dat Hallo publicatie profiel u uiteindelijk gebruik toodeploy uw iOS-app 'com.mycompany.myapp' gebruikt als Hallo van App-ID. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Hallo tooconfigure na uw project voor uitvoeren **iOS** en voer deze in Hallo iOS-Simulator:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Hallo tooconfigure na uw project voor uitvoeren **Android** en voer deze in Hallo Android-emulator. Zorg ervoor dat de instellingen van uw Android SDK Emulator het doel als Google APIs (Google Inc.) met Hallo CPU / ABI als Google APIs ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Hallo invoegtoepassing Cordova Console toevoegen. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Hello Azure Mobile Engagement Cordova-invoegtoepassing installeren en tegelijkertijd Hallo waarden van variabelen tooconfigure Hallo-invoegtoepassing:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Android Reach Icon* : moet Hallo-naam van de resource Hallo zonder een extensie of drawable voorvoegsel (voorbeeld: mynotificationicon), en het Hallo-pictogrambestand moet worden gekopieerd naar uw android-project (platforms/android/res/drawable)

*iOS Reach Icon* : Hallo-naam van het Hallo-resource met de extensie moet zijn (bijvoorbeeld: mynotificationicon.png), en het Hallo-pictogrambestand moet worden toegevoegd aan uw iOS-project met XCode (via Hallo Menu toevoegen-bestanden)

## <a id="monitor"></a>Realtime-bewaking inschakelen
1. Bewerk in Hallo Cordova-project - **www/js/index.js** tooadd Hallo aanroep tooMobile Engagement toodeclare een nieuwe activiteit eenmaal Hallo *deviceReady* gebeurtenis is ontvangen.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Hallo-toepassing uitvoeren:
   
   * **Voor iOS**
     
       In `Terminal` venster start u uw app in een nieuw exemplaar van de Simulator door het uitvoeren van de volgende Hallo:
     
           cordova run ios
   * **Voor Android**
     
       In `Terminal` venster start u uw app in een nieuw exemplaar van de emulator door het uitvoeren van de volgende Hallo:
     
           cordova run android
3. U kunt in de logboeken van de console Hallo Hallo volgende zien:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract met uw gebruikers via Pushmeldingen en in-app-berichten in Hallo context van campagnes. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Pushreferenties configureren voor Mobile Engagement
tooallow Mobile Engagement toosend Pushmeldingen namens u, moet u deze toegang hebben tot tooyour certificaat voor Apple iOS of API-sleutel van GCM Server toogrant. 

1. Navigeer tooyour Mobile Engagement-portal. Zorg ervoor dat het Hallo-App wordt gebruikt voor dit project en klik vervolgens op Hallo **Engage** knop Hallo onderaan:
   
    ![][1]
2. U komt dan uit op de pagina instellingen Hallo in de Engagement-Portal. Klik op Hallo **Native Pushbericht** sectie:
   
    ![][2]
3. iOS-certificaat/API-sleutel GCM Server configureren
   
    **[iOS]**
   
    a. Selecteer uw .p12, upload het en typ uw wachtwoord:
   
    ![][3]
   
    **[Android]**
   
    a. Klik op Hallo bewerkingspictogram vóór **API-sleutel** in Hallo sectie GCM-instellingen in Hallo pop-up dat weergegeven wordt, Hallo GCM-serversleutel plakken en klikt u op **OK**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Pushmeldingen inschakelen in Hallo Cordova-app
Bewerken **www/js/index.js** tooadd Hallo aanroep tooMobile Engagement toorequest pushmeldingen en een handler te declareren:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Hallo-app uitvoeren
**[iOS]**

1. We gebruiken XCode toobuild en Hallo-app op Hallo apparaat tootest pushmeldingen implementeren omdat iOS alleen push notifications tooan daadwerkelijk apparaat toestaat. Ga toohello locatie waar uw Cordova-project wordt gemaakt en te navigeren**...\platforms\ios** locatie. Open Hallo systeemeigen .xcodeproj-bestand in XCode. 
2. Bouw en implementeer Hallo Cordova-app toohello iOS-apparaat met Hallo account Hallo inrichtingsprofiel die u zojuist hebt geüpload toohello Mobile Engagement-portal en App-Id die overeenkomt met de Hallo een die u hebt opgegeven tijdens het maken van Hallo Hallo-certificaat bevat met Hallo Cordova-app. U kunt Hallo uitchecken *bundel-id* in uw **Resources\*-info.plist** bestand in XCode toomatch deze. 
3. U ziet Hallo standaard iOS-pop op uw apparaat weergegeven die Hallo app vraagt toestemming toosend meldingen. Hallo-machtiging verlenen. 

**[Android]**

U kunt gewoon Hallo emulator toorun hello Android app gebruiken als GCM-meldingen op Hallo Android-emulator worden ondersteund. 

    cordova run android

## <a id="send"></a>Een melding tooyour app verzenden
We gaan nu een eenvoudige pushmeldingcampagne die stuurt een push-tooyour app uitgevoerd op Hallo apparaat maken:

1. Navigeer toohello **bereiken** tabblad in uw Mobile Engagement-portal
2. Klik op **nieuwe aankondiging** toocreate uw pushcampagne
   
    ![][6]
3. Invoer toocreate Geef uw campagne **[Android]**
   
   * Geef uw campagne een **naam**. 
   * Selecteer Hallo **Bezorgingstype** als *Systeemmelding* *eenvoudige*
   * Selecteer Hallo **leveringstijd** als *'Elke keer'*
   * Geef een **titel** voor de melding die als eerste regel in Hallo push Hallo.
   * Geef een **bericht** voor de melding die als de berichttekst Hallo fungeert. 
     
     ![][11]
4. Invoer toocreate Geef uw campagne **[iOS]**
   
   * Geef uw campagne een **naam**. 
   * Selecteer Hallo **leveringstijd** als *'alleen buiten app'*
   * Geef een **titel** voor de melding die als eerste regel in Hallo push Hallo.
   * Geef een **bericht** voor de melding die als de berichttekst Hallo fungeert. 
     
     ![][12]
5. Schuif naar beneden en selecteer in de Hallo sectie inhoud **alleen melding**
   
    ![][8]
6. [Optioneel] U kunt ook een actie-URL opgeven. Zorg ervoor dat deze gebruikmaakt van een URL-schema dat is opgegeven tijdens het Hallo-invoegtoepassing configureren **AZME\_OMLEIDEN\_URL** variabele bijvoorbeeld *myapp://test*.  
7. Instelling Hallo meest elementaire campagne mogelijk kunt u klaar bent. Nu Blader nogmaals naar beneden en klik op Hallo **maken** knop toosave uw campagne.
8. Ten slotte moet u uw campagne **activeren**.
   
    ![][10]
9. U ziet nu een pushmelding op het apparaat of de emulator als onderdeel van deze campagne. 

## <a id="next-steps"></a>Volgende stappen
[Overzicht van alle methoden beschikbaar met Cordova Mobile Engagement SDK](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

