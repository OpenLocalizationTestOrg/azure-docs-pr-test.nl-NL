---
title: Pushmeldingen verzenden naar Chrome-apps met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe u met Azure Notification Hubs pushmeldingen verzendt naar een Chrome-app.
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
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="ebd9c-104">Pushmeldingen verzenden naar Chrome-apps met Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ebd9c-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="ebd9c-105">In dit onderwerp wordt beschreven hoe u met Azure Notification Hubs pushmeldingen naar een Chrome-app kunt verzenden in de context van de Google Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="ebd9c-106">In deze zelfstudie maken we een Chrome-app die pushmeldingen ontvangt via [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="ebd9c-107">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ebd9c-108">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ebd9c-109">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="ebd9c-110">De zelfstudie leidt u door deze eenvoudige stappen om pushmeldingen in te schakelen:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="ebd9c-111">Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="ebd9c-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="ebd9c-112">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="ebd9c-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="ebd9c-113">Uw Chrome-app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="ebd9c-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="ebd9c-114">Een pushmelding naar uw Chrome-app verzenden</span><span class="sxs-lookup"><span data-stu-id="ebd9c-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="ebd9c-115">Extra functionaliteit en mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="ebd9c-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="ebd9c-116">Pushmeldingen in een Chrome-app zijn geen algemene meldingen in de browser. Ze zijn specifiek voor het uitbreidbaarheidsmodel van de browser (Zie [Overzicht van Chrome-apps] voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="ebd9c-117">Chrome-apps kunnen niet alleen op de pc worden gebruikt, maar ook op mobiele apparaten (Android en iOS) via Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="ebd9c-118">Zie [Chrome-apps op mobiele apparaten] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="ebd9c-119">Het configureren van GCM en Azure Notification Hubs werkt op dezelfde manier als de configuratie voor Android, aangezien [Google Cloud Messaging voor Chrome] niet meer bestaat. Hetzelfde GCM ondersteunt nu Android-apparaten en Chrome-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="ebd9c-120"><a id="register"></a>Google Cloud Messaging inschakelen</span><span class="sxs-lookup"><span data-stu-id="ebd9c-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="ebd9c-121">Navigeer naar de [Google Cloud Console]-website, log in op uw Google-account en klik op vervolgens op de knop **Create Project** (Project maken).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="ebd9c-122">Geef een geschikte **Project Name** op en klik vervolgens op de knop **Create**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="ebd9c-123">Noteer het **Project Number** op de pagina **Projects** van het project dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="ebd9c-124">U gebruikt deze als de **GCM afzender-id** in de Chrome-app om uzelf te registreren bij GCM.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="ebd9c-125">Klik in het linkerdeelvenster op **API's & auth** en schuif omlaag. Klik op de wisselknop om **Google Cloud Messaging for Android** in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="ebd9c-126">U hoeft **Google Cloud Messaging for Chrome** niet in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="ebd9c-127">Klik in het linkerdeelvenster op **Credentials** > **Create New Key** > **Server Key** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="ebd9c-128">Noteer de waarde van de **API-sleutel** van de server.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="ebd9c-129">U configureert deze in de volgende stap in uw Notification Hub, zodat u puhmeldingen naar GCM kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="ebd9c-130"><a id="configure-hub"></a>Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="ebd9c-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="ebd9c-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="ebd9c-132">Selecteer in de blade **Instellingen** **Notification Services** en vervolgens **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="ebd9c-133">Voer de API-sleutel in en sla uw invoer op.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="ebd9c-135"><a id="connect-app"></a>Uw Chrome-app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="ebd9c-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="ebd9c-136">De Notification Hub is nu geconfigureerd voor GCM en u hebt de verbindingsreeksen om uw app te registreren voor het ontvangen en verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="ebd9c-137">LK</span><span class="sxs-lookup"><span data-stu-id="ebd9c-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="ebd9c-138">Een nieuwe Chrome-app maken</span><span class="sxs-lookup"><span data-stu-id="ebd9c-138">Create a new Chrome App</span></span>
<span data-ttu-id="ebd9c-139">Het onderstaande voorbeeld is gebaseerd op het [Chrome App GCM-voorbeeld] waarin op de aanbevolen manier een Chrome-app wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="ebd9c-140">We zullen de stappen bespreken die specifiek betrekking hebben op Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebd9c-141">We raden u aan de bron voor deze Chrome-app te downloaden vanaf [Chrome App Notification Hub Sample].</span><span class="sxs-lookup"><span data-stu-id="ebd9c-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="ebd9c-142">De Chrome-app wordt gemaakt via JavaScript en u kunt uw favoriete tekstverwerkingsprogramma hiervoor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="ebd9c-143">Hieronder ziet u hoe deze Chrome-app eruit komt te zien.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome-app][15]

1. <span data-ttu-id="ebd9c-145">Maak een map en geef deze de naam `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="ebd9c-146">De naam is natuurlijk willekeurig. Als u een andere naam gebruikt, moet u het pad in de vereiste codesegmenten vervangen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="ebd9c-147">Download [crypto-js library] in de map die u in de tweede stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="ebd9c-148">Deze bibliotheekmap bevat twee submappen: `components` en `rollups`.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="ebd9c-149">Maak een `manifest.json`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="ebd9c-150">Alle Chrome-apps worden ondersteund door een manifestbestand met de metagegevens van de app en alle machtigingen die worden verleend aan de app wanneer de gebruiker de app installeert.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
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
   
    <span data-ttu-id="ebd9c-151">Let op het `permissions`-element, dat aangeeft dat deze Chrome-app pushmeldingen van GCM kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="ebd9c-152">Ook moet hierin de Azure Notification Hubs URI worden opgegeven waarin de Chrome-app een REST-aanroep doet voor de registratie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="ebd9c-153">Onze voorbeeldapp gebruikt ook een pictogrambestand `gcm_128.png`, dat zich bevindt op de bronlocatie die opnieuw wordt gebruikt van het originele GCM-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="ebd9c-154">U kunt het vervangen door een andere afbeelding die voldoet aan de [vereisten voor een pictogram](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="ebd9c-155">Maak een bestand met de naam `background.js` met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
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
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="ebd9c-156">Dit is het bestand dat wordt weergegeven in de html van de Chrome-app (**register.html**). Hierin wordt ook de handler **messageReceived** voor binnenkomende pushberichten gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="ebd9c-157">Maak een bestand met de naam `register.html`. Hiermee definieert u de gebruikersinterface van de Chrome-app.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ebd9c-158">In dit voorbeeld werken we met **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="ebd9c-159">Als u een andere versie van de bibliotheek hebt gedownload, moet u de versie in het `src`-pad vervangen door de juiste versie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
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
6. <span data-ttu-id="ebd9c-160">Maak een bestand met de naam `register.js` met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="ebd9c-161">Dit bestand definieert het script achter `register.html`.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="ebd9c-162">Chrome-apps ondersteunen geen inline-uitvoeringen. U moet dus een afzonderlijke back-up van het script maken voor uw gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
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
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
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
   
          // Update the payload with the registration ID obtained earlier.
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
   
    <span data-ttu-id="ebd9c-163">Het bovenstaande script heeft de volgende belangrijke parameters:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="ebd9c-164">**Window.onload** definieert wat er gebeurt als op de twee knoppen in de gebruikersinterface wordt gedrukt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="ebd9c-165">Met de ene knop wordt de registratie bij GCM uitgevoerd en de andere maakt gebruik van de registratie-id die na de registratie bij GCM van Azure Notification Hubs wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="ebd9c-166">**updateLog** is de functie waarmee we eenvoudige logboekmogelijkheden kunnen afhandelen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="ebd9c-167">**registerWithGCM** is de eerste handler voor de knop, waardoor `chrome.gcm.register` GCM wordt aangeroepen om het huidige exemplaar van de Chrome-app te registreren.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="ebd9c-168">**registerCallback** is de callbackfunctie die wordt aangeroepen wanneer de aanroep van de GCM-registratie wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="ebd9c-169">**registerWithNH** is de tweede handler voor de knop, waardoor wordt geregistreerd bij Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="ebd9c-170">Deze ontvangt `hubName` en `connectionString` (door de gebruiker opgegeven) en stelt de REST-API-aanroep samen voor registratie bij Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="ebd9c-171">**splitConnectionString** en **generateSaSToken** zijn hulpprogramma's voor het uitvoeren van de implementatie van JavaScript van een SaS-token, dat in alle REST-API-aanroepen moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="ebd9c-172">Zie [Algemene begrippen](http://msdn.microsoft.com/library/dn495627.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="ebd9c-173">**sendNHRegistrationRequest** is de functie die een HTTP REST-aanroep naar Azure Notification Hubs maakt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="ebd9c-174">**registrationPayload** definieert de XML-nettolading van de registratie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="ebd9c-175">Zie [REST-API maken voor de registratie van NH] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="ebd9c-176">We werken de registratie-id hierin bij met de informatie die we van GCM ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="ebd9c-177">**client** is een exemplaar van **XMLHttpRequest** die we gebruiken voor het maken van de HTTP POST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="ebd9c-178">Let op: de `Authorization`-header wordt bijgewerkt met `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="ebd9c-179">Als deze aanroep is voltooid, wordt dit exemplaar van de Chrome-app geregistreerd bij Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="ebd9c-180">De algehele mappenstructuur voor dit project moet er als volgt uitzien: ![Google Chrome-app - mappenstructuur][21]</span><span class="sxs-lookup"><span data-stu-id="ebd9c-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="ebd9c-181">Uw Chrome-app instellen en testen</span><span class="sxs-lookup"><span data-stu-id="ebd9c-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="ebd9c-182">Open uw Chrome-browser.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-182">Open your Chrome browser.</span></span> <span data-ttu-id="ebd9c-183">Open **Chrome-extensies** en schakel **Modus voor ontwikkelaars** in.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="ebd9c-184">Klik op **Uitgepakte extensie laden** en navigeer naar de map waarin u de bestanden hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="ebd9c-185">U kunt eventueel ook het **hulpprogramma Chrome Apps& Extensions Developer** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="ebd9c-186">Dit hulpprogramma is zelf een Chrome-app (geïnstalleerd via de Chrome Web Store) en biedt geavanceerde mogelijkheden voor foutopsporing tijdens de ontwikkeling van uw Chrome-app.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="ebd9c-187">Als de Chrome-app foutloos is gemaakt, wordt uw app weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="ebd9c-188">Voer het **projectnummer** in dat u eerder hebt ontvangen van de **Google Cloud Console** als de afzender-id en klik op **Registreren bij GCM**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="ebd9c-189">Het volgende bericht wordt weergegeven: **Registratie bij GCM is voltooid.**</span><span class="sxs-lookup"><span data-stu-id="ebd9c-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="ebd9c-190">Voer de **Naam van de Notification Hub** en de **DefaultListenSharedAccessSignature** in die u eerder hebt ontvangen van de portal en klik op **Registreren bij Azure Notification Hub**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="ebd9c-191">Als het goed is, wordt het volgende bericht weergegeven: **Registratie van Notification Hub gelukt!**,</span><span class="sxs-lookup"><span data-stu-id="ebd9c-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="ebd9c-192">evenals de details van het registratie-antwoord dat de registratie-id van Azure Notification Hubs bevat.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="ebd9c-193"><a name="send"></a>Een melding naar uw Chrome-app verzenden</span><span class="sxs-lookup"><span data-stu-id="ebd9c-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="ebd9c-194">Voor testdoeleinden sturen we Chrome-pushmeldingen met een .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebd9c-195">U kunt pushmeldingen verzenden via Notification Hubs vanuit elke back-end via de openbare <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST-interface</a>.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="ebd9c-196">Bekijk onze [portal met documentatie](https://azure.microsoft.com/documentation/services/notification-hubs/) voor meer platformonafhankelijke voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="ebd9c-197">Klik in Visual Studio in het menu **File** (Bestand) op **New** (Nieuw) en vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="ebd9c-198">Klik onder **Visual C#** op **Windows** en **Console Application** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="ebd9c-199">Hiermee maakt u een nieuw consoletoepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="ebd9c-200">Klik in het menu **Tools** op **Library Package Manager** en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="ebd9c-201">Hiermee wordt Package Manager Console weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="ebd9c-202">Voer de volgende opdracht uit in het consolevenster:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="ebd9c-203">Open `Program.cs` en voeg de volgende `using` instructie toe:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="ebd9c-204">Voeg in de klasse `Program` de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="ebd9c-205">Zorg ervoor dat u de verbindingsreeks met het toegangsrecht **Full** (Volledig) gebruikt, dus niet **Listen** (Luisteren).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="ebd9c-206">Met de verbindingsreeks met het toegangsrecht **Listen** kunnen geen pushmeldingen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="ebd9c-207">Voeg de volgende aanroepen toe aan de methode `Main`:</span><span class="sxs-lookup"><span data-stu-id="ebd9c-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="ebd9c-208">Zorg ervoor dat Chrome wordt uitgevoerd en start de consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="ebd9c-209">De volgende meldingspop-up wordt op uw bureaublad weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="ebd9c-210">U kunt ook al uw meldingen zien in het venster Chrome-meldingen in de taakbalk (in Windows) als Chrome wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="ebd9c-211">Hiervoor hoeft u de Chrome-app niet te starten of te openen in de browser (de Chrome-browser zelf moet wel worden uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="ebd9c-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="ebd9c-212">U kunt ook een geconsolideerde weergave van al uw meldingen bekijken in het venster Chrome-berichten.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="ebd9c-213"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebd9c-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="ebd9c-214">Zie [Overzicht van Notification Hubs] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="ebd9c-215">Zie de zelfstudie [Azure Notification Hubs Gebruikers waarschuwen] om specifieke gebruikers te bereiken.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="ebd9c-216">Zie [Azure Notification Hubs voor belangrijk nieuws] als u gebruikers wilt indelen op belangengroep.</span><span class="sxs-lookup"><span data-stu-id="ebd9c-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

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
<span data-ttu-id="ebd9c-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="ebd9c-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="ebd9c-218">[Google Cloud Console]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="ebd9c-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="ebd9c-219">[Overzicht van Notification Hubs]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="ebd9c-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="ebd9c-220">[Overzicht van Chrome-apps]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="ebd9c-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="ebd9c-221">[Chrome App GCM-voorbeeld]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="ebd9c-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="ebd9c-222">[Chrome-apps op mobiele apparaten]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="ebd9c-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="ebd9c-223">[REST-API maken voor de registratie van NH]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="ebd9c-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="ebd9c-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="ebd9c-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="ebd9c-225">[Google Cloud Messaging voor Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="ebd9c-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="ebd9c-226">[Azure Notification Hubs Gebruikers waarschuwen]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="ebd9c-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="ebd9c-227">[Azure Notification Hubs voor belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="ebd9c-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
