---
title: aaaAdd Pushmeldingen tooApache Cordova-App met Azure Mobile Apps | Microsoft Docs
description: Meer informatie over hoe Azure Mobile Apps-toosend toouse push-meldingen tooyour Apache Cordova-app.
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Push notifications tooyour Apache Cordova-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overzicht
In deze zelfstudie maakt toevoegen u push notifications toohello [Apache Cordova snel starten] project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.

Als u geen gebruik Hallo gedownload serverproject snel starten, moet u push notification-uitbreidingspakket Hallo. Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][1].

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie bevat informatie over een Apache Cordova-toepassing die is ontwikkeld met Visual Studio 2015 die wordt uitgevoerd op Hallo Google Android-Emulator, een Android-apparaat, een Windows-apparaat en een iOS-apparaat.

toocomplete deze zelfstudie hebt u nodig:

* Een PC met [Visual Studio Community 2015] [ 2] of hoger.
* [Visual Studio Tools voor Apache Cordova][4].
* Een [actief Azure-account][3].
* Een voltooide [snel starten van Apache Cordova] [ 5] project.
* (Android) Een [Google-account] [ 6] met een geverifieerde e-mailadres.
* (iOS) Een [Apple Developer Program-lidmaatschap] [ 7] en een iOS-apparaat (iOS-Simulator biedt geen ondersteuning voor pushmeldingen).
* (Windows) Een [Windows Store-ontwikkelaarsaccount] [ 8] en een Windows 10-apparaat.

## <a name="configure-hub"></a>Een notification hub configureren
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Bekijk een video waarin de stappen in deze sectie][9]

## <a name="update-hello-server-project"></a>Hallo serverproject bijwerken
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Uw Cordova-app wijzigen
Zorg ervoor dat uw Apache Cordova-app-project is gereed toohandle pushmeldingen installeren Hallo Cordova push-invoegtoepassing plus de platform-specifieke pushservices.

#### <a name="update-hello-cordova-version-in-your-project"></a>Hallo Cordova-versie in uw project te werken.
Werk de Hallo clientproject als uw project een Apache Cordova-versie die ouder zijn dan v6.1.1 gebruikt. tooupdate hello project:

* Met de rechtermuisknop op `config.xml` tooopen Hallo configuration designer.
* Selecteer Hallo Platforms tabblad.
* Kies 6.1.1 in Hallo **Cordova CLI** in het tekstvak.
* Kies **bouwen**, klikt u vervolgens **Build Solution** tooupdate Hallo project.

#### <a name="install-hello-push-plugin"></a>Hallo push-invoegtoepassing installeren
Apache Cordova-toepassingen verwerken niet systeemeigen apparaat- of -mogelijkheden.  Deze mogelijkheden worden geleverd door invoegtoepassingen die zijn gepubliceerd op [npm] [ 10] of op GitHub.  Hallo `phonegap-plugin-push` invoegtoepassing gebruikte toohandle netwerk pushmeldingen is.

U kunt Hallo push-invoegtoepassing installeren in een van de volgende manieren:

**Hallo vanaf de opdrachtprompt:**

Hallo volgende opdracht uitvoeren:

    cordova plugin add phonegap-plugin-push

**Uit vanuit Visual Studio:**

1. Open in Solution Explorer Hallo `config.xml` bestand Klik **Plugins** > **aangepaste**, selecteer **Git** als de installatiebron, voer dan `https://github.com/phonegap/phonegap-plugin-push`als Hallo bron.

   ![][img1]

2. Klik op Hallo pijl volgende toohello installatiebron.
3. In **SENDER_ID**, hebt u al een numerieke project-ID voor Hallo Google Developer-Console-project, u kunt u deze hier toevoegen. Anders, voer een aanduidingswaarde van de tijdelijke, zoals 777777.  Als u voor Android ontwikkelt, kunt u deze waarde in config.xml later bijwerken.
4. Klik op **Add**.

Hallo push-invoegtoepassing is nu geïnstalleerd.

#### <a name="install-hello-device-plugin"></a>Hallo apparaat invoegtoepassing installeren
Volg dezelfde Hallo procedure tooinstall Hallo push-invoegtoepassing die wordt gebruikt.  Hallo apparaat invoegtoepassing uit Hallo Core plugins lijst toevoegen (Klik op **Plugins** > **Core** toofind deze). U moet de naam van deze invoegtoepassing tooobtain Hallo platform.

#### <a name="register-your-device-on-application-start-up"></a>Registreer uw apparaat op opstarten van de toepassing
We in eerste instantie opnemen minimale code voor Android. Later wijzigen Hallo app toorun op iOS- of Windows 10.

1. Voeg een aanroep te**registerForPushNotifications** tijdens het Hallo-retouraanroep voor Hallo aanmelding of onderin Hallo Hallo **onDeviceReady** methode:

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    In dit voorbeeld ziet aanroepen **registerForPushNotifications** nadat verificatie is geslaagd.  U kunt aanroepen `registerForPushNotifications()` zo vaak als nodig is.

2. Toevoegen van nieuwe Hallo **registerForPushNotifications** methode als volgt:

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) Vervang in Hallo voorafgaand aan code, `Your_Project_ID` project met Hallo numerieke ID voor uw app uit de [Google Developer-Console][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Optioneel) Configureren en uitvoeren van Hallo-app voor Android
Deze sectie tooenable pushmeldingen voor Android worden voltooid.

#### <a name="enable-gcm"></a>Inschakelen van Firebase Cloud-berichten
Aangezien we Hallo Google Android-platform in eerste instantie ontwikkelt, moet u de Firebase Cloud Messaging inschakelen.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Hallo mobiele App back-end toosend push-aanvragen via FCM configureren
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configureer uw Cordova-app voor Android
Open config.xml in uw Cordova-app en vervang `Your_Project_ID` project met Hallo numerieke ID voor uw app uit Hallo [Google Developer-Console][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Index.js openen en bijwerken Hallo code toouse uw numerieke project-ID.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Uw Android-apparaat voor USB-foutopsporing configureren
Voordat u uw toepassing tooyour Android-apparaat implementeren kunt, moet u tooenable USB-foutopsporing.  Voer de volgende stappen uit op uw Android-telefoon:

1. Ga te**instellingen** > **over telefoon**, tikt u op Hallo **Build-nummer** totdat modus voor ontwikkelaars (ongeveer zeven maal) is ingeschakeld.
2. Terug in de **instellingen** > **opties voor ontwikkelaars** inschakelen **USB-foutopsporing**, sluit uw Android-telefoon tooyour ontwikkeling PC met een USB-kabel.

We hebben getest dit met behulp van een Google-Nexus 5 X-apparaat met Android 6.0 (Marshmallow).  Hallo technieken zijn echter algemene binnen een moderne Android release.

#### <a name="install-google-play-services"></a>Installeer Google Play-Services
Hallo push-invoegtoepassing is afhankelijk van Android Google Play Services voor pushmeldingen.

1. Klik in Visual Studio **extra** > **Android** > **Android SDK Manager**, vouw Hallo **extra's** map- en controle Hallo vak toomake ervoor dat elk van de volgende SDK's Hallo is geïnstalleerd.

   * Android 2.3 of hoger
   * Google-opslagplaats revisie 27 of hoger
   * Google Play Services 9.0.2 of hoger

2. Klik op **pakketten installeren** en wachten op Hallo installatie toocomplete.

Hallo huidige vereist bibliotheken worden vermeld in Hallo [phonegap-invoegtoepassing-push-installatie documentatie][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Pushmeldingen testen in Hallo-app voor Android
U kunt nu pushmeldingen testen door het uitvoeren van app en invoegen items in de takentabel Hallo Hallo. U kunt testen van Hallo hetzelfde apparaat of van een tweede apparaat dezelfde hello, zolang u back-end. Test uw Cordova-app op Hallo Android-platform in een van de volgende manieren Hallo:

* **Op een fysiek apparaat:** koppelen van uw Android-apparaat tooyour ontwikkelcomputer met een USB-kabel.  In plaats van **Google Android-Emulator**, selecteer **apparaat**. Visual Studio Hallo toepassing toohello apparaat implementeert en vervolgens wordt de toepassing hello uitgevoerd.  U kunt vervolgens met de toepassing hello op Hallo apparaat werken.

  De ontwikkeling-ervaring te verbeteren.  Scherm, zoals toepassingen delen [Mobizen] [ 20] kan u helpen bij het ontwikkelen van een Android-toepassing.  Uw webbrowser voor Android scherm tooa projecteert Mobizen op uw PC.

* **Op een Android-emulator:** er zijn extra configuratiestappen vereist wanneer u gebruikmaakt van een emulator.

    Zorg ervoor dat u tooa virtueel apparaat met Google APIs ingesteld als doel hello, zoals wordt weergegeven in Hallo Android Virtual Device (AVD) manager implementeert.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Als u een snellere x86 toouse wilt emulator u [hello HAXM stuurprogramma installeren] [ 11] en configureer Hallo emulator toouse deze.

    Een apparaat toohello Android van Google-account toevoegen door te klikken op **Apps** > **instellingen** > **account toevoegen**, volg de aanwijzingen Hallo.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Hallo todolist-app als voordat uitvoeren en een nieuwe taak invoegen. Dit moment wordt een pictogram weergegeven in het systeemvak Hallo. U kunt Hallo melding lade tooview Hallo volledige tekst van melding Hallo openen.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Optioneel) Configureren en uitvoeren op iOS
Deze sectie is voor het uitvoeren van Hallo Cordova-project op iOS-apparaten. Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Agent installeren en uitvoeren Hallo iOS externe te ontwikkelen op een Mac- of cloud service
Voordat u een Cordova-app voor iOS met Visual Studio uitvoeren kunt, stappen doorlopen die Hallo in Hallo [iOS Setup Guide] [ 12] tooinstall en Voer Hallo externe agent te ontwikkelen.

Zorg ervoor dat u Hallo-app voor iOS kunt samenstellen. Hallo zijn stappen in de handleiding voor het instellen van Hallo vereiste toobuild voor iOS vanuit Visual Studio. Als u een Mac niet hebt, kunt u voor iOS met de Hallo externe build-agent op een service, zoals MacInCloud samenstellen. Zie voor meer informatie [uw iOS-app uitvoeren in de cloud Hallo][21].

> [!NOTE]
> XCode 7 of hoger is vereist toouse Hallo push-invoegtoepassing op iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Hallo-ID toouse vinden als uw App-ID
Voordat u uw app voor pushmeldingen registreert, opent u config.xml in uw Cordova-app, Hallo zoeken `id` kenmerkwaarde in Hallo widget-element en kopiëren voor later gebruik. In de Hallo XML te volgen, Hallo-ID is `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Deze id later gebruiken bij het maken van een App-ID op van Apple developer portal. Als u een andere App-ID op Hallo developer-portal maakt, moet u rekening houden met een paar extra stappen verderop in deze zelfstudie. Hallo-ID in het element widget moet overeenkomen met de Hallo App-ID op Hallo-portal voor ontwikkelaars.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Hallo-app voor pushmeldingen op Apple developer-portal te registreren
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Bekijk een video van vergelijkbare stappen](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Azure toosend-pushmeldingen configureren
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Controleren of uw App-ID overeenkomt met uw Cordova-app
Als Hallo App-ID die u hebt gemaakt in uw ontwikkelaarsaccount Apple al overeenkomt met Hallo-ID van Hallo widget element in config.xml, kunt u deze stap overslaan. Als Hallo-id's niet overeenkomen, voert u Hallo stappen te volgen:

1. Hallo platforms map verwijderen van uw project.
2. Hallo plugins map verwijderen van uw project.
3. Hallo node_modules map verwijderen van uw project.
4. Hallo-id-kenmerk van Hallo widget element in config.xml toouse Hallo App-ID die u hebt gemaakt in uw Apple Developer-Account bijwerken.
5. Bouw het project opnieuw op.

##### <a name="test-push-notifications-in-your-ios-app"></a>Pushmeldingen testen in uw iOS-app
1. Controleer of in Visual Studio **iOS** is geselecteerd als het implementatiedoel Hallo en kies vervolgens **apparaat** toorun op het verbonden iOS-apparaat.

    U kunt uitvoeren op een iOS-apparaat aansluit tooyour PC met iTunes. Hallo iOS-Simulator biedt geen ondersteuning voor pushmeldingen.

2. Druk op Hallo **uitvoeren** knop of **F5** in Visual Studio toobuild Hallo-project en start Hallo-app in een iOS-apparaat en klik vervolgens op **OK** tooaccept pushmeldingen.

   > [!NOTE]
   > Hallo app vraagt om bevestiging voor pushmeldingen tijdens Hallo voor het eerst uitvoert.

3. Typ een taak in Hallo-app, en klik op Hallo plusteken (+) pictogram.
4. Controleer of dat een melding wordt ontvangen en klik vervolgens op OK toodismiss Hallo melding.

## <a name="optional-configure-and-run-on-windows"></a>(Optioneel) Configureren en uitvoeren in Windows
Deze sectie is voor het uitvoeren van Hallo Apache Cordova-app-project op Windows 10-apparaten (Hallo PhoneGap push-invoegtoepassing wordt ondersteund op Windows 10). Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Uw Windows-app voor pushmeldingen registreren met WNS
toouse hello Store opties in Visual Studio, selecteer een doel Windows hello oplossing Platforms lijst zoals **Windows x64** of **Windows x86** (voorkomen **Windows AnyCPU** voor pushmeldingen).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Bekijk een video van gelijksoortige stappen][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Hallo notification hub configureren voor WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Uw pushmeldingen voor Cordova-app toosupport Windows configureren
Open Hallo configuration designer (met de rechtermuisknop op config.xml en selecteer **ontwerper**), selecteer Hallo **Windows** tabblad en kies **Windows 10** onder **Windows doel versie**.

toosupport pushmeldingen in uw standaard (debug) bouwt, open build.json-bestand. Kopieer de "release" configuratie tooyour foutopsporing configuratie.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Nadat de update hello, moeten Hallo build.json Hallo na code bevatten:

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Hallo-app bouwen en te controleren of er geen fouten. Uw client-app moet zich nu registreren voor Hallo meldingen van de back-end van Hallo mobiele App. Herhaal deze sectie voor elke Windows-project in uw oplossing.

#### <a name="test-push-notifications-in-your-windows-app"></a>Pushmeldingen testen in uw Windows-app
Zorg ervoor dat een Windows-platform, zoals Hallo implementatie TARGET is geselecteerd in Visual Studio **Windows x64** of **Windows x86**. Kies toorun Hallo-app op een Windows 10-computer die als host fungeert voor Visual Studio **lokale Machine**.

Druk op Hallo knop toobuild Hallo project uitvoeren en Hallo-app te starten.

Typ een naam voor een nieuwe stukje in Hallo-app en klik op Hallo plusteken (+) pictogram tooadd deze.

Controleer of dat er een melding wordt ontvangen wanneer Hallo item wordt toegevoegd.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Notification Hubs] [ 17] toolearn over pushmeldingen.
* Als u dit nog niet hebt gedaan, gaat u verder Hallo zelfstudie door [Authentication toevoegen] [ 14] tooyour Apache Cordova-app.

Meer informatie over hoe toouse Hallo SDK's.

* [Apache Cordova-SDK][15]
* [ASP.NET-Server SDK][1]
* [Server-SDK voor node.js][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
