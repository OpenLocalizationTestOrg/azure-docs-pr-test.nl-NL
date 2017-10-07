---
title: aaaSend push notifications tooChrome apps met Azure Notification Hubs | Microsoft Docs
description: Meer informatie over hoe toouse Azure Notification Hubs toosend push-meldingen tooa Chrome-App.
services: notification-hubs
keywords: mobiele pushmeldingen,pushmeldingen,pushmelding,pushmeldingen chroom
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Verzenden push notifications tooChrome apps met Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Dit onderwerp leest u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Chrome-App wordt weergegeven in de context Hallo Hallo Google Chrome-browser. In deze zelfstudie maken we een Chrome-app die pushmeldingen ontvangt via [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F) voor meer informatie.
> 
> 

Hallo-zelfstudie leert u deze basisstappen tooenable pushmeldingen verzenden:

* [Google Cloud Messaging inschakelen](#register)
* [Uw Notification Hub configureren](#configure-hub)
* [Verbinding maken met uw Chrome-App toohello notification hub](#connect-app)
* [Een push notification tooyour Chrome-App verzenden](#send)
* [Extra functionaliteit en mogelijkheden](#next-steps)

> [!NOTE]
> Chrome app pushmeldingen zijn niet algemeen in de browser meldingen: ze zijn het uitbreidbaarheidsmodel van specifieke toohello browser (Zie [overzicht van Chrome-Apps] voor meer informatie). Bovendien toohello bureaublad browser Chrome-apps uitvoeren op mobiele apparaten (Android en iOS) via Apache Cordova. Zie [Chrome-Apps op mobiele apparaten] toolearn meer.
> 
> 

Identieke tooconfiguring voor Android, aangezien configureren van GCM en Azure Notification Hubs is [Google Cloud Messaging voor Chrome] is afgeschaft en Hallo hetzelfde GCM ondersteunt nu Android-apparaten en Chrome-exemplaren.

## <a id="register"></a>Google Cloud Messaging inschakelen
1. Navigeer toohello [Google Cloud Console] website, meld u aan met de referenties van uw Google-account en klik vervolgens op Hallo **Project maken** knop. Geef een geschikte **projectnaam**, en klik vervolgens op Hallo **maken** knop.
   
       ![Google Cloud Console - Create Project][1]
2. Maak een notitie van Hallo **projectnummer** op Hallo **projecten** pagina voor het Hallo-project dat u zojuist hebt gemaakt. U gebruikt deze als Hallo **GCM afzender-ID** in Hallo Chrome-App tooregister bij GCM.
   
       ![Google Cloud Console - Project Number][2]
3. Klik in het linkerdeelvenster Hallo **API's & auth**, en schuif omlaag en klikt u op Hallo wisselknop tooenable **Google Cloud Messaging for Android**. U hebt geen tooenable **Google Cloud Messaging voor Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. Klik in het linkerdeelvenster Hallo **referenties** > **Create New Key** > **serversleutel** > **maken**.
   
       ![Google Cloud Console - Credentials][4]
5. Maak een notitie van Hallo server **API-sleutel**. U configureert deze in uw notification hub vervolgens tooenable het toosend push notifications tooGCM.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Uw Notification Hub configureren
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   In Hallo **instellingen** blade Selecteer **Notification Services** en vervolgens **Google (GCM)**. Voer Hallo API-sleutel en opslaan.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Verbinding maken met uw Chrome-App toohello notification hub
Uw notification hub is nu geconfigureerd toowork bij GCM en u Hallo verbinding tekenreeksen tooregister uw app tooboth ontvangen en verzenden van pushmeldingen hebt. LK

### <a name="create-a-new-chrome-app"></a>Een nieuwe Chrome-app maken
Hallo onderstaand voorbeeld is gebaseerd op Hallo [Chrome App GCM-voorbeeld] en maakt gebruik van Hallo aanbevolen toocreate manier een Chrome-App. We wordt Hallo stappen specifiek gerelateerde tooAzure Notification Hubs gemarkeerd. 

> [!NOTE]
> Het is raadzaam Hallo bron te downloaden voor deze Chrome-App van [Chrome App Notification Hub Sample].
> 
> 

Hallo Chrome-App wordt gemaakt via JavaScript en u kunt een van uw favoriete tekstverwerkingsprogramma gebruiken voor het maken van deze. Hieronder ziet u hoe deze Chrome-app eruit komt te zien.

![Google Chrome-app][15]

1. Maak een map en geef deze de naam `ChromePushApp`. Hallo-naam is natuurlijk willekeurig - als u een andere naam gebruikt, controleert u of dat u Hallo pad in Hallo vereiste codesegmenten vervangen.
2. Hallo downloaden [crypto-js library] in Hallo-map die u hebt gemaakt in de tweede stap Hallo. Deze bibliotheekmap bevat twee submappen: `components` en `rollups`.
3. Maak een `manifest.json`-bestand. Alle Chrome-Apps worden ondersteund door een manifestbestand met Hallo app metagegevens en de meeste alle machtigingen die zijn verleend toohello app wanneer Hallo gebruiker deze installeert.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Kennisgeving Hallo `permissions` element, dat aangeeft dat deze Chrome-App kunnen tooreceive pushmeldingen van GCM zal zijn. Het moet ook hello Azure Notification Hubs URI waar Hallo Chrome-App een REST-aanroep tooregister maakt opgeven.
    Onze voorbeeldapp gebruikt ook een pictogrambestand `gcm_128.png`, dat zich bevindt op Hallo-bron die opnieuw wordt gebruikt van Hallo originele GCM-voorbeeld. U kunt het vervangen door voor de installatiekopie die past bij de Hallo [pictogram criteria](https://developer.chrome.com/apps/manifest/icons).
4. Maken van een bestand met de naam `background.js` Hello code te volgen:
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    Dit is Hallo-bestand dat Hallo Chrome-App venster HTML verschijnt (**register.html**) en definieert ook Hallo handler **messageReceived** toohandle Hallo binnenkomende pushberichten.
5. Maken van een bestand met de naam `register.html` -Hiermee definieert u Hallo UI Hallo Chrome-App. 
   
   > [!NOTE]
   > In dit voorbeeld werken we met **CryptoJS v3.1.2**. Als u een andere versie van het Hallo-bibliotheek hebt gedownload, controleert u of u vervangen door de juiste versie in Hallo Hallo `src` pad.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Maken van een bestand met de naam `register.js` met Hallo-code hieronder. Dit bestand bevat Hallo script achter `register.html`. Chrome-Apps staan geen inline-uitvoeringen, zodat u beschikt over toocreate een afzonderlijke back-up-script voor de gebruikersinterface.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    Hallo bovenstaande script heeft Hallo belangrijke parameters te volgen:
   
   * **Window.OnLoad** Hallo knop gebeurtenissen Hallo twee knoppen op Hallo UI definieert. Een registreert bij GCM en Hallo andere maakt gebruik van Hallo registratie-ID die na de registratie bij GCM tooregister met Azure Notification Hubs wordt geretourneerd.
   * **updateLog** Hallo-functie waarmee we eenvoudige logboekmogelijkheden van toohandle is.
   * **registerWithGCM** Hallo eerste knop handler, waardoor Hallo `chrome.gcm.register` aanroep tooGCM tooregister Hallo huidige Chrome-App-exemplaar.
   * **registerCallback** Hallo callback-functie die wordt aangeroepen wanneer Hallo GCM-registratie aanroep retourneert is.
   * **registerWithNH** Hallo tweede knop handler, waardoor wordt geregistreerd bij Notification Hubs. Het ophalen van `hubName` en `connectionString` (welke Hallo-gebruiker is opgegeven) en knutselen Hallo Notification Hubs registratie REST API-aanroep.
   * **splitConnectionString** en **generateSaSToken** zijn hulpprogramma Hallo JavaScript-uitvoering van een SaS-token maken proces, dat moet worden gebruikt in alle REST-API-aanroepen. Zie [Algemene begrippen](http://msdn.microsoft.com/library/dn495627.aspx) voor meer informatie.
   * **sendNHRegistrationRequest** is Hallo-functie die een HTTP REST aanroepen tooAzure Notification Hubs.
   * **registrationPayload** definieert Hallo registratie van de XML-nettolading. Zie [REST-API maken voor de registratie van NH] voor meer informatie. We bijwerken Hallo registratie-ID in het met we van GCM ontvangen.
   * **client** is een exemplaar van **XMLHttpRequest** gebruiken we toomake Hallo HTTP POST-aanvraag. Opmerking werken wij Hallo `Authorization` header met `sasToken`. Als deze aanroep is voltooid, wordt dit exemplaar van de Chrome-app geregistreerd bij Azure Notification Hubs.

Hallo algemene mapstructuur voor de voor dit project moet eruitzien als dit: ![Google Chrome-App - mapstructuur][21]

### <a name="set-up-and-test-your-chrome-app"></a>Uw Chrome-app instellen en testen
1. Open uw Chrome-browser. Open **Chrome-extensies** en schakel **Modus voor ontwikkelaars** in.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Klik op **uitgepakte extensie laden** en navigeer toohello map waar u Hallo bestanden hebt gemaakt. U kunt eventueel ook Hallo **Chrome Apps & Extensions Developer hulpprogramma**. Dit hulpprogramma is een Chrome-App zelf (geïnstalleerd via Hallo Chrome Web Store) en biedt geavanceerde mogelijkheden voor foutopsporing voor de ontwikkeling van uw Chrome-App.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Als Hallo Chrome-App wordt gemaakt zonder fouten, ziet u uw App weergegeven.
   
       ![Google Chrome - Chrome App Display][18]
4. Voer Hallo **projectnummer** dat u eerder hebt ontvangen van Hallo **Google Cloud Console** als Hallo afzender-ID en klik op **registreren bij GCM**. U moet het Hallo-bericht ziet **registratie bij GCM is voltooid.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Voer uw **Notification Hub-naam** en Hallo **DefaultListenSharedAccessSignature** die u hebt verkregen in eerder Hallo-portal en klik op **registreren bij Azure Notification Hub**. U moet het Hallo-bericht ziet **registratie van Notification Hub gelukt!** en details op Hallo van Hallo registratie-antwoord dat hello Azure Notification Hubs registratie bevat-id.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Een melding tooyour Chrome-App verzenden
Voor testdoeleinden sturen we Chrome-pushmeldingen met een .NET-consoletoepassing. 

> [!NOTE]
> U kunt pushmeldingen verzenden via Notification Hubs vanuit elke back-end via de openbare <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST-interface</a>. Bekijk onze [portal met documentatie](https://azure.microsoft.com/documentation/services/notification-hubs/) voor meer platformonafhankelijke voorbeelden.
> 
> 

1. In Visual Studio van Hallo **bestand** selecteert u **nieuw** en vervolgens **Project**. Klik onder **Visual C#** op **Windows** en **Console Application** en klik vervolgens op **OK**.  Hiermee maakt u een nieuw consoletoepassingsproject.
2. Van Hallo **extra** menu, klikt u op **Library Package Manager** en vervolgens **Package Manager Console**. Hallo Package Manager-Console worden weergegeven.
3. Uitvoeren in het consolevenster hello, Hallo volgende opdracht:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Open `Program.cs` en voeg de volgende Hallo `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
5. In Hallo `Program` klasse, Hallo volgende methode toe te voegen:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Zorg ervoor dat u de verbindingsreeks Hallo met **volledige** toegang niet **luisteren** toegang. Hallo **luisteren** verbindingsreeks toegang verleent geen machtigingen toosend pushmeldingen.
   > 
   > 
6. Hallo volgende roept Hallo toevoegen `Main` methode:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Zorg ervoor dat Chrome wordt uitgevoerd en Voer Hallo-consoletoepassing.
8. U ziet de volgende Hallo melding op uw bureaublad.
   
       ![Google Chrome - Notification][13]
9. U ziet ook al uw meldingen via Hallo Chrome-meldingen venster in Hallo taakbalk (in Windows) als Chrome wordt uitgevoerd.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> U hoeft niet toohave Hallo Chrome-App uitgevoerd of openen in browser hello (Hoewel Hallo Chrome-browser zelf moet worden uitgevoerd). U kunt ook een geconsolideerde weergave van al uw meldingen ophalen in het venster van Hallo Chrome-meldingen.
> 
> 

## <a name="next-steps"> </a>Volgende stappen
Zie [Overzicht van Notification Hubs] voor meer informatie.

tootarget specifieke gebruikers, Raadpleeg toohello [Azure Notification Hubs gebruikers waarschuwen] zelfstudie. 

Als u uw gebruikers op belangengroepen toosegment wilt, voert u Hallo [Azure Notification Hubs voor belangrijk nieuws] zelfstudie.

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Overzicht van Notification Hubs]: notification-hubs-push-notification-overview.md
[overzicht van Chrome-Apps]: https://developer.chrome.com/apps/about_apps
[Chrome App GCM-voorbeeld]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome-Apps op mobiele apparaten]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[REST-API maken voor de registratie van NH]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js library]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging voor Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs gebruikers waarschuwen]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs voor belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
