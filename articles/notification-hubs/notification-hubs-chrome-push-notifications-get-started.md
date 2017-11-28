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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="44173-104">Verzenden push notifications tooChrome apps met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="44173-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="44173-105">Dit onderwerp leest u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Chrome-App wordt weergegeven in de context Hallo Hallo Google Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="44173-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="44173-106">In deze zelfstudie maken we een Chrome-app die pushmeldingen ontvangt via [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="44173-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="44173-107">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="44173-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="44173-108">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="44173-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="44173-109">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44173-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="44173-110">Hallo-zelfstudie leert u deze basisstappen tooenable pushmeldingen verzenden:</span><span class="sxs-lookup"><span data-stu-id="44173-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="44173-111">Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="44173-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="44173-112">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="44173-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="44173-113">Verbinding maken met uw Chrome-App toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="44173-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="44173-114">Een push notification tooyour Chrome-App verzenden</span><span class="sxs-lookup"><span data-stu-id="44173-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="44173-115">Extra functionaliteit en mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="44173-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="44173-116">Chrome app pushmeldingen zijn niet algemeen in de browser meldingen: ze zijn het uitbreidbaarheidsmodel van specifieke toohello browser (Zie [overzicht van Chrome-Apps] voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="44173-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="44173-117">Bovendien toohello bureaublad browser Chrome-apps uitvoeren op mobiele apparaten (Android en iOS) via Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="44173-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="44173-118">Zie [Chrome-Apps op mobiele apparaten] toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="44173-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="44173-119">Identieke tooconfiguring voor Android, aangezien configureren van GCM en Azure Notification Hubs is [Google Cloud Messaging voor Chrome] is afgeschaft en Hallo hetzelfde GCM ondersteunt nu Android-apparaten en Chrome-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="44173-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="44173-120"><a id="register"></a>Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="44173-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="44173-121">Navigeer toohello [Google Cloud Console] website, meld u aan met de referenties van uw Google-account en klik vervolgens op Hallo **Project maken** knop.</span><span class="sxs-lookup"><span data-stu-id="44173-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="44173-122">Geef een geschikte **projectnaam**, en klik vervolgens op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="44173-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="44173-123">Maak een notitie van Hallo **projectnummer** op Hallo **projecten** pagina voor het Hallo-project dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44173-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="44173-124">U gebruikt deze als Hallo **GCM afzender-ID** in Hallo Chrome-App tooregister bij GCM.</span><span class="sxs-lookup"><span data-stu-id="44173-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="44173-125">Klik in het linkerdeelvenster Hallo **API's & auth**, en schuif omlaag en klikt u op Hallo wisselknop tooenable **Google Cloud Messaging for Android**.</span><span class="sxs-lookup"><span data-stu-id="44173-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="44173-126">U hebt geen tooenable **Google Cloud Messaging voor Chrome**.</span><span class="sxs-lookup"><span data-stu-id="44173-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="44173-127">Klik in het linkerdeelvenster Hallo **referenties** > **Create New Key** > **serversleutel** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="44173-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="44173-128">Maak een notitie van Hallo server **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="44173-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="44173-129">U configureert deze in uw notification hub vervolgens tooenable het toosend push notifications tooGCM.</span><span class="sxs-lookup"><span data-stu-id="44173-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="44173-130"><a id="configure-hub"></a>Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="44173-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="44173-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="44173-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="44173-132">In Hallo **instellingen** blade Selecteer **Notification Services** en vervolgens **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="44173-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="44173-133">Voer Hallo API-sleutel en opslaan.</span><span class="sxs-lookup"><span data-stu-id="44173-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="44173-135"><a id="connect-app"></a>Verbinding maken met uw Chrome-App toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="44173-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="44173-136">Uw notification hub is nu geconfigureerd toowork bij GCM en u Hallo verbinding tekenreeksen tooregister uw app tooboth ontvangen en verzenden van pushmeldingen hebt.</span><span class="sxs-lookup"><span data-stu-id="44173-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="44173-137">LK</span><span class="sxs-lookup"><span data-stu-id="44173-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="44173-138">Een nieuwe Chrome-app maken</span><span class="sxs-lookup"><span data-stu-id="44173-138">Create a new Chrome App</span></span>
<span data-ttu-id="44173-139">Hallo onderstaand voorbeeld is gebaseerd op Hallo [Chrome App GCM-voorbeeld] en maakt gebruik van Hallo aanbevolen toocreate manier een Chrome-App.</span><span class="sxs-lookup"><span data-stu-id="44173-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="44173-140">We wordt Hallo stappen specifiek gerelateerde tooAzure Notification Hubs gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="44173-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="44173-141">Het is raadzaam Hallo bron te downloaden voor deze Chrome-App van [Chrome App Notification Hub Sample].</span><span class="sxs-lookup"><span data-stu-id="44173-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="44173-142">Hallo Chrome-App wordt gemaakt via JavaScript en u kunt een van uw favoriete tekstverwerkingsprogramma gebruiken voor het maken van deze.</span><span class="sxs-lookup"><span data-stu-id="44173-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="44173-143">Hieronder ziet u hoe deze Chrome-app eruit komt te zien.</span><span class="sxs-lookup"><span data-stu-id="44173-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome-app][15]

1. <span data-ttu-id="44173-145">Maak een map en geef deze de naam `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="44173-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="44173-146">Hallo-naam is natuurlijk willekeurig - als u een andere naam gebruikt, controleert u of dat u Hallo pad in Hallo vereiste codesegmenten vervangen.</span><span class="sxs-lookup"><span data-stu-id="44173-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="44173-147">Hallo downloaden [crypto-js library] in Hallo-map die u hebt gemaakt in de tweede stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="44173-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="44173-148">Deze bibliotheekmap bevat twee submappen: `components` en `rollups`.</span><span class="sxs-lookup"><span data-stu-id="44173-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="44173-149">Maak een `manifest.json`-bestand.</span><span class="sxs-lookup"><span data-stu-id="44173-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="44173-150">Alle Chrome-Apps worden ondersteund door een manifestbestand met Hallo app metagegevens en de meeste alle machtigingen die zijn verleend toohello app wanneer Hallo gebruiker deze installeert.</span><span class="sxs-lookup"><span data-stu-id="44173-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
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
   
    <span data-ttu-id="44173-151">Kennisgeving Hallo `permissions` element, dat aangeeft dat deze Chrome-App kunnen tooreceive pushmeldingen van GCM zal zijn.</span><span class="sxs-lookup"><span data-stu-id="44173-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="44173-152">Het moet ook hello Azure Notification Hubs URI waar Hallo Chrome-App een REST-aanroep tooregister maakt opgeven.</span><span class="sxs-lookup"><span data-stu-id="44173-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="44173-153">Onze voorbeeldapp gebruikt ook een pictogrambestand `gcm_128.png`, dat zich bevindt op Hallo-bron die opnieuw wordt gebruikt van Hallo originele GCM-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="44173-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="44173-154">U kunt het vervangen door voor de installatiekopie die past bij de Hallo [pictogram criteria](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="44173-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="44173-155">Maken van een bestand met de naam `background.js` Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="44173-155">Create a file called `background.js` with hello following code:</span></span>
   
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
   
    <span data-ttu-id="44173-156">Dit is Hallo-bestand dat Hallo Chrome-App venster HTML verschijnt (**register.html**) en definieert ook Hallo handler **messageReceived** toohandle Hallo binnenkomende pushberichten.</span><span class="sxs-lookup"><span data-stu-id="44173-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="44173-157">Maken van een bestand met de naam `register.html` -Hiermee definieert u Hallo UI Hallo Chrome-App.</span><span class="sxs-lookup"><span data-stu-id="44173-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="44173-158">In dit voorbeeld werken we met **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="44173-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="44173-159">Als u een andere versie van het Hallo-bibliotheek hebt gedownload, controleert u of u vervangen door de juiste versie in Hallo Hallo `src` pad.</span><span class="sxs-lookup"><span data-stu-id="44173-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
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
6. <span data-ttu-id="44173-160">Maken van een bestand met de naam `register.js` met Hallo-code hieronder.</span><span class="sxs-lookup"><span data-stu-id="44173-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="44173-161">Dit bestand bevat Hallo script achter `register.html`.</span><span class="sxs-lookup"><span data-stu-id="44173-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="44173-162">Chrome-Apps staan geen inline-uitvoeringen, zodat u beschikt over toocreate een afzonderlijke back-up-script voor de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="44173-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
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
   
    <span data-ttu-id="44173-163">Hallo bovenstaande script heeft Hallo belangrijke parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="44173-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="44173-164">**Window.OnLoad** Hallo knop gebeurtenissen Hallo twee knoppen op Hallo UI definieert.</span><span class="sxs-lookup"><span data-stu-id="44173-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="44173-165">Een registreert bij GCM en Hallo andere maakt gebruik van Hallo registratie-ID die na de registratie bij GCM tooregister met Azure Notification Hubs wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="44173-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="44173-166">**updateLog** Hallo-functie waarmee we eenvoudige logboekmogelijkheden van toohandle is.</span><span class="sxs-lookup"><span data-stu-id="44173-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="44173-167">**registerWithGCM** Hallo eerste knop handler, waardoor Hallo `chrome.gcm.register` aanroep tooGCM tooregister Hallo huidige Chrome-App-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="44173-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="44173-168">**registerCallback** Hallo callback-functie die wordt aangeroepen wanneer Hallo GCM-registratie aanroep retourneert is.</span><span class="sxs-lookup"><span data-stu-id="44173-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="44173-169">**registerWithNH** Hallo tweede knop handler, waardoor wordt geregistreerd bij Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="44173-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="44173-170">Het ophalen van `hubName` en `connectionString` (welke Hallo-gebruiker is opgegeven) en knutselen Hallo Notification Hubs registratie REST API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="44173-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="44173-171">**splitConnectionString** en **generateSaSToken** zijn hulpprogramma Hallo JavaScript-uitvoering van een SaS-token maken proces, dat moet worden gebruikt in alle REST-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="44173-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="44173-172">Zie [Algemene begrippen](http://msdn.microsoft.com/library/dn495627.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44173-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="44173-173">**sendNHRegistrationRequest** is Hallo-functie die een HTTP REST aanroepen tooAzure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="44173-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="44173-174">**registrationPayload** definieert Hallo registratie van de XML-nettolading.</span><span class="sxs-lookup"><span data-stu-id="44173-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="44173-175">Zie [REST-API maken voor de registratie van NH] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44173-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="44173-176">We bijwerken Hallo registratie-ID in het met we van GCM ontvangen.</span><span class="sxs-lookup"><span data-stu-id="44173-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="44173-177">**client** is een exemplaar van **XMLHttpRequest** gebruiken we toomake Hallo HTTP POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44173-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="44173-178">Opmerking werken wij Hallo `Authorization` header met `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="44173-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="44173-179">Als deze aanroep is voltooid, wordt dit exemplaar van de Chrome-app geregistreerd bij Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="44173-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="44173-180">Hallo algemene mapstructuur voor de voor dit project moet eruitzien als dit: ![Google Chrome-App - mapstructuur][21]</span><span class="sxs-lookup"><span data-stu-id="44173-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="44173-181">Uw Chrome-app instellen en testen</span><span class="sxs-lookup"><span data-stu-id="44173-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="44173-182">Open uw Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="44173-182">Open your Chrome browser.</span></span> <span data-ttu-id="44173-183">Open **Chrome-extensies** en schakel **Modus voor ontwikkelaars** in.</span><span class="sxs-lookup"><span data-stu-id="44173-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="44173-184">Klik op **uitgepakte extensie laden** en navigeer toohello map waar u Hallo bestanden hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44173-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="44173-185">U kunt eventueel ook Hallo **Chrome Apps & Extensions Developer hulpprogramma**.</span><span class="sxs-lookup"><span data-stu-id="44173-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="44173-186">Dit hulpprogramma is een Chrome-App zelf (geïnstalleerd via Hallo Chrome Web Store) en biedt geavanceerde mogelijkheden voor foutopsporing voor de ontwikkeling van uw Chrome-App.</span><span class="sxs-lookup"><span data-stu-id="44173-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="44173-187">Als Hallo Chrome-App wordt gemaakt zonder fouten, ziet u uw App weergegeven.</span><span class="sxs-lookup"><span data-stu-id="44173-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="44173-188">Voer Hallo **projectnummer** dat u eerder hebt ontvangen van Hallo **Google Cloud Console** als Hallo afzender-ID en klik op **registreren bij GCM**.</span><span class="sxs-lookup"><span data-stu-id="44173-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="44173-189">U moet het Hallo-bericht ziet **registratie bij GCM is voltooid.**</span><span class="sxs-lookup"><span data-stu-id="44173-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="44173-190">Voer uw **Notification Hub-naam** en Hallo **DefaultListenSharedAccessSignature** die u hebt verkregen in eerder Hallo-portal en klik op **registreren bij Azure Notification Hub**.</span><span class="sxs-lookup"><span data-stu-id="44173-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="44173-191">U moet het Hallo-bericht ziet **registratie van Notification Hub gelukt!**</span><span class="sxs-lookup"><span data-stu-id="44173-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="44173-192">en details op Hallo van Hallo registratie-antwoord dat hello Azure Notification Hubs registratie bevat-id.</span><span class="sxs-lookup"><span data-stu-id="44173-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="44173-193"><a name="send"></a>Een melding tooyour Chrome-App verzenden</span><span class="sxs-lookup"><span data-stu-id="44173-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="44173-194">Voor testdoeleinden sturen we Chrome-pushmeldingen met een .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="44173-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="44173-195">U kunt pushmeldingen verzenden via Notification Hubs vanuit elke back-end via de openbare <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST-interface</a>.</span><span class="sxs-lookup"><span data-stu-id="44173-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="44173-196">Bekijk onze [portal met documentatie](https://azure.microsoft.com/documentation/services/notification-hubs/) voor meer platformonafhankelijke voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44173-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="44173-197">In Visual Studio van Hallo **bestand** selecteert u **nieuw** en vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="44173-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="44173-198">Klik onder **Visual C#** op **Windows** en **Console Application** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="44173-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="44173-199">Hiermee maakt u een nieuw consoletoepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="44173-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="44173-200">Van Hallo **extra** menu, klikt u op **Library Package Manager** en vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="44173-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="44173-201">Hallo Package Manager-Console worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="44173-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="44173-202">Uitvoeren in het consolevenster hello, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44173-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="44173-203">Open `Program.cs` en voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="44173-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="44173-204">In Hallo `Program` klasse, Hallo volgende methode toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="44173-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="44173-205">Zorg ervoor dat u de verbindingsreeks Hallo met **volledige** toegang niet **luisteren** toegang.</span><span class="sxs-lookup"><span data-stu-id="44173-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="44173-206">Hallo **luisteren** verbindingsreeks toegang verleent geen machtigingen toosend pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="44173-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="44173-207">Hallo volgende roept Hallo toevoegen `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="44173-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="44173-208">Zorg ervoor dat Chrome wordt uitgevoerd en Voer Hallo-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="44173-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="44173-209">U ziet de volgende Hallo melding op uw bureaublad.</span><span class="sxs-lookup"><span data-stu-id="44173-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="44173-210">U ziet ook al uw meldingen via Hallo Chrome-meldingen venster in Hallo taakbalk (in Windows) als Chrome wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="44173-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="44173-211">U hoeft niet toohave Hallo Chrome-App uitgevoerd of openen in browser hello (Hoewel Hallo Chrome-browser zelf moet worden uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="44173-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="44173-212">U kunt ook een geconsolideerde weergave van al uw meldingen ophalen in het venster van Hallo Chrome-meldingen.</span><span class="sxs-lookup"><span data-stu-id="44173-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="44173-213"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44173-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="44173-214">Zie [Overzicht van Notification Hubs] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44173-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="44173-215">tootarget specifieke gebruikers, Raadpleeg toohello [Azure Notification Hubs gebruikers waarschuwen] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="44173-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="44173-216">Als u uw gebruikers op belangengroepen toosegment wilt, voert u Hallo [Azure Notification Hubs voor belangrijk nieuws] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="44173-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

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
