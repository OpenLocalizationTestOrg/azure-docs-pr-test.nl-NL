---
title: Pushmeldingen toevoegen aan de Apache Cordova-App met Azure Mobile Apps | Microsoft Docs
description: Informatie over het Azure Mobile Apps gebruiken voor het verzenden van pushmeldingen aan uw Apache Cordova-app.
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="85ffd-103">Pushmeldingen toevoegen aan uw Apache Cordova-app</span><span class="sxs-lookup"><span data-stu-id="85ffd-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="85ffd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="85ffd-104">Overview</span></span>
<span data-ttu-id="85ffd-105">In deze zelfstudie hebt toevoegen u pushmeldingen aan het project [Apache Cordova snel starten] zodat een pushmelding wordt verzonden naar het apparaat telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="85ffd-106">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="85ffd-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="85ffd-107">Zie voor meer informatie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="85ffd-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="85ffd-108"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="85ffd-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="85ffd-109">Deze zelfstudie bevat informatie over een Apache Cordova-toepassing die is ontwikkeld met Visual Studio 2015 die wordt uitgevoerd op de Google Android-Emulator, een Android-apparaat, een Windows-apparaat en een iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85ffd-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="85ffd-110">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="85ffd-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="85ffd-111">Een PC met [Visual Studio Community 2015] [ 2] of hoger.</span><span class="sxs-lookup"><span data-stu-id="85ffd-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="85ffd-112">[Visual Studio Tools voor Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="85ffd-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="85ffd-113">Een [actief Azure-account][3].</span><span class="sxs-lookup"><span data-stu-id="85ffd-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="85ffd-114">Een voltooide [snel starten van Apache Cordova] [ 5] project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="85ffd-115">(Android) Een [Google-account] [ 6] met een geverifieerde e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="85ffd-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="85ffd-116">(iOS) Een [Apple Developer Program-lidmaatschap] [ 7] en een iOS-apparaat (iOS-Simulator biedt geen ondersteuning voor pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="85ffd-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="85ffd-117">(Windows) Een [Windows Store-ontwikkelaarsaccount] [ 8] en een Windows 10-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85ffd-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="85ffd-118"><a name="configure-hub"></a>Een notification hub configureren</span><span class="sxs-lookup"><span data-stu-id="85ffd-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="85ffd-119">[Bekijk een video waarin de stappen in deze sectie][9]</span><span class="sxs-lookup"><span data-stu-id="85ffd-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="85ffd-120">Het serverproject bijwerken</span><span class="sxs-lookup"><span data-stu-id="85ffd-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="85ffd-121"><a name="add-push-to-app"></a>Uw Cordova-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="85ffd-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="85ffd-122">Zorg ervoor dat uw Apache Cordova-app-project is gereed om te verwerken pushmeldingen door het installeren van de Cordova-invoegtoepassing push plus de platform-specifieke pushservices.</span><span class="sxs-lookup"><span data-stu-id="85ffd-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="85ffd-123">Werk de Cordova-versie in uw project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="85ffd-124">Werk het clientproject als uw project een Apache Cordova-versie die ouder zijn dan v6.1.1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="85ffd-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="85ffd-125">Het project bijwerken:</span><span class="sxs-lookup"><span data-stu-id="85ffd-125">To update the project:</span></span>

* <span data-ttu-id="85ffd-126">Met de rechtermuisknop op `config.xml` openen van de configuration designer.</span><span class="sxs-lookup"><span data-stu-id="85ffd-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="85ffd-127">Selecteer het tabblad Platforms.</span><span class="sxs-lookup"><span data-stu-id="85ffd-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="85ffd-128">Kies 6.1.1 in de **Cordova CLI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="85ffd-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="85ffd-129">Kies **bouwen**, klikt u vervolgens **Build Solution** bijwerken van het project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="85ffd-130">De push-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="85ffd-130">Install the push plugin</span></span>
<span data-ttu-id="85ffd-131">Apache Cordova-toepassingen verwerken niet systeemeigen apparaat- of -mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="85ffd-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="85ffd-132">Deze mogelijkheden worden geleverd door invoegtoepassingen die zijn gepubliceerd op [npm] [ 10] of op GitHub.</span><span class="sxs-lookup"><span data-stu-id="85ffd-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="85ffd-133">De `phonegap-plugin-push` invoegtoepassing wordt gebruikt voor het afhandelen van pushmeldingen netwerk.</span><span class="sxs-lookup"><span data-stu-id="85ffd-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="85ffd-134">U kunt de push-invoegtoepassing installeren in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="85ffd-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="85ffd-135">**Vanaf de opdrachtprompt:**</span><span class="sxs-lookup"><span data-stu-id="85ffd-135">**From the command-prompt:**</span></span>

<span data-ttu-id="85ffd-136">Voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="85ffd-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="85ffd-137">**Uit vanuit Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="85ffd-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="85ffd-138">Open in Solution Explorer de `config.xml` bestand Klik **Plugins** > **aangepaste**, selecteer **Git** als de installatiebron, voer dan `https://github.com/phonegap/phonegap-plugin-push`als de bron.</span><span class="sxs-lookup"><span data-stu-id="85ffd-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="85ffd-139">Klik op de pijl naast de installatiebron.</span><span class="sxs-lookup"><span data-stu-id="85ffd-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="85ffd-140">In **SENDER_ID**, hebt u al een numerieke project-ID voor het project Google Developer-Console, u kunt u deze hier toevoegen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="85ffd-141">Anders, voer een aanduidingswaarde van de tijdelijke, zoals 777777.</span><span class="sxs-lookup"><span data-stu-id="85ffd-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="85ffd-142">Als u voor Android ontwikkelt, kunt u deze waarde in config.xml later bijwerken.</span><span class="sxs-lookup"><span data-stu-id="85ffd-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="85ffd-143">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="85ffd-143">Click **Add**.</span></span>

<span data-ttu-id="85ffd-144">De push-invoegtoepassing is nu geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="85ffd-145">De apparaat-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="85ffd-145">Install the device plugin</span></span>
<span data-ttu-id="85ffd-146">Volg dezelfde procedure die u gebruikt voor het installeren van de push-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="85ffd-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="85ffd-147">De apparaat-invoegtoepassing toevoegen in de lijst van de invoegtoepassingen Core (Klik op **Plugins** > **Core** te vinden).</span><span class="sxs-lookup"><span data-stu-id="85ffd-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="85ffd-148">U moet deze invoegtoepassing om de platformnaam te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="85ffd-149">Registreer uw apparaat op opstarten van de toepassing</span><span class="sxs-lookup"><span data-stu-id="85ffd-149">Register your device on application start-up</span></span>
<span data-ttu-id="85ffd-150">We in eerste instantie opnemen minimale code voor Android.</span><span class="sxs-lookup"><span data-stu-id="85ffd-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="85ffd-151">De app uit te voeren op iOS- of Windows 10 later wijzigen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="85ffd-152">Voeg een aanroep naar **registerForPushNotifications** tijdens de callback voor de aanmelding of aan de onderkant van de **onDeviceReady** methode:</span><span class="sxs-lookup"><span data-stu-id="85ffd-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="85ffd-153">In dit voorbeeld ziet aanroepen **registerForPushNotifications** nadat verificatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="85ffd-154">U kunt aanroepen `registerForPushNotifications()` zo vaak als nodig is.</span><span class="sxs-lookup"><span data-stu-id="85ffd-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="85ffd-155">Toevoegen van de nieuwe **registerForPushNotifications** methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="85ffd-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="85ffd-156">(Android) Vervang in de bovenstaande code `Your_Project_ID` project met de numerieke ID voor uw app uit de [Google Developer-Console][18].</span><span class="sxs-lookup"><span data-stu-id="85ffd-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="85ffd-157">(Optioneel) Configureren en uitvoeren van de app voor Android</span><span class="sxs-lookup"><span data-stu-id="85ffd-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="85ffd-158">Deze sectie om in te schakelen pushmeldingen voor Android worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="85ffd-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="85ffd-159"><a name="enable-gcm"></a>Inschakelen van Firebase Cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="85ffd-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="85ffd-160">Omdat we het Google Android-platform in eerste instantie ontwikkelt, moet u de Firebase Cloud Messaging inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="85ffd-161"><a name="configure-backend"></a>De backend voor mobiele Apps voor het verzenden van push-aanvragen via van FCM configureren</span><span class="sxs-lookup"><span data-stu-id="85ffd-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="85ffd-162">Configureer uw Cordova-app voor Android</span><span class="sxs-lookup"><span data-stu-id="85ffd-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="85ffd-163">Open config.xml in uw Cordova-app en vervang `Your_Project_ID` project met de numerieke ID voor uw app uit de [Google Developer-Console][18].</span><span class="sxs-lookup"><span data-stu-id="85ffd-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="85ffd-164">Index.js openen en bijwerken van de code voor het gebruik van uw numerieke project-ID.</span><span class="sxs-lookup"><span data-stu-id="85ffd-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="85ffd-165"><a name="configure-device"></a>Uw Android-apparaat voor USB-foutopsporing configureren</span><span class="sxs-lookup"><span data-stu-id="85ffd-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="85ffd-166">Voordat u uw toepassing op uw Android-apparaat implementeren kunt, moet u de USB-foutopsporing inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="85ffd-167">Voer de volgende stappen uit op uw Android-telefoon:</span><span class="sxs-lookup"><span data-stu-id="85ffd-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="85ffd-168">Ga naar **instellingen** > **over telefoon**, tikt u op de **Build-nummer** totdat modus voor ontwikkelaars (ongeveer zeven maal) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="85ffd-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="85ffd-169">Terug in de **instellingen** > **opties voor ontwikkelaars** inschakelen **USB-foutopsporing**, uw Android-telefoon vervolgens verbinding met het ontwikkelen PC met een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="85ffd-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="85ffd-170">We hebben getest dit met behulp van een Google-Nexus 5 X-apparaat met Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="85ffd-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="85ffd-171">De technieken zijn echter algemene binnen een moderne Android release.</span><span class="sxs-lookup"><span data-stu-id="85ffd-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="85ffd-172">Installeer Google Play-Services</span><span class="sxs-lookup"><span data-stu-id="85ffd-172">Install Google Play Services</span></span>
<span data-ttu-id="85ffd-173">De push-invoegtoepassing is afhankelijk van Android Google Play Services voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="85ffd-174">Klik in Visual Studio **extra** > **Android** > **Android SDK Manager**, vouw de **extra's** map, en controleer het vak om ervoor te zorgen dat elk van de volgende SDK's is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="85ffd-175">Android 2.3 of hoger</span><span class="sxs-lookup"><span data-stu-id="85ffd-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="85ffd-176">Google-opslagplaats revisie 27 of hoger</span><span class="sxs-lookup"><span data-stu-id="85ffd-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="85ffd-177">Google Play Services 9.0.2 of hoger</span><span class="sxs-lookup"><span data-stu-id="85ffd-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="85ffd-178">Klik op **pakketten installeren** en wacht totdat de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="85ffd-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="85ffd-179">De huidige vereiste bibliotheken worden vermeld in de [phonegap-invoegtoepassing-push-installatie documentatie][19].</span><span class="sxs-lookup"><span data-stu-id="85ffd-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="85ffd-180">Pushmeldingen testen in de app voor Android</span><span class="sxs-lookup"><span data-stu-id="85ffd-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="85ffd-181">U kunt nu test pushmeldingen door het uitvoeren van de app en het invoegen van items in de takentabel.</span><span class="sxs-lookup"><span data-stu-id="85ffd-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="85ffd-182">U kunt van hetzelfde apparaat of van een tweede apparaat testen, zolang u de dezelfde back-end gebruikt.</span><span class="sxs-lookup"><span data-stu-id="85ffd-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="85ffd-183">Test uw Cordova-app op het Android-platform in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="85ffd-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="85ffd-184">**Op een fysiek apparaat:** uw Android-apparaat koppelen aan uw ontwikkelcomputer waarop een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="85ffd-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="85ffd-185">In plaats van **Google Android-Emulator**, selecteer **apparaat**.</span><span class="sxs-lookup"><span data-stu-id="85ffd-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="85ffd-186">Visual Studio implementeert de toepassing op het apparaat en vervolgens de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="85ffd-187">U kunt vervolgens met de toepassing op het apparaat werken.</span><span class="sxs-lookup"><span data-stu-id="85ffd-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="85ffd-188">De ontwikkeling-ervaring te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="85ffd-188">Improve your development experience.</span></span>  <span data-ttu-id="85ffd-189">Scherm, zoals toepassingen delen [Mobizen] [ 20] kan u helpen bij het ontwikkelen van een Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="85ffd-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="85ffd-190">Het scherm van uw Android aan een webbrowser projecteert Mobizen op uw PC.</span><span class="sxs-lookup"><span data-stu-id="85ffd-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="85ffd-191">**Op een Android-emulator:** er zijn extra configuratiestappen vereist wanneer u gebruikmaakt van een emulator.</span><span class="sxs-lookup"><span data-stu-id="85ffd-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="85ffd-192">Zorg ervoor dat u implementeert op een virtueel apparaat met Google APIs ingesteld als doel, zoals wordt weergegeven in de Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="85ffd-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="85ffd-193">Als u wilt gebruiken een snellere x86 emulator u [Installeer het stuurprogramma HAXM] [ 11] en configureren van de emulator om dit te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85ffd-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="85ffd-194">Een Google-account toevoegen aan de Android-apparaat door te klikken op **Apps** > **instellingen** > **account toevoegen**, volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="85ffd-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="85ffd-195">Voer de todolist-app als voordat en een nieuwe taak invoegen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="85ffd-196">Dit moment wordt een pictogram weergegeven in het systeemvak.</span><span class="sxs-lookup"><span data-stu-id="85ffd-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="85ffd-197">U kunt de meldingenlijst om weer te geven van de volledige tekst van de melding openen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="85ffd-198">(Optioneel) Configureren en uitvoeren op iOS</span><span class="sxs-lookup"><span data-stu-id="85ffd-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="85ffd-199">Deze sectie is voor het uitvoeren van de Cordova-project op iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="85ffd-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="85ffd-200">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="85ffd-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="85ffd-201">Installeren en uitvoeren van de iOS externe build-agent op een Mac- of cloud service</span><span class="sxs-lookup"><span data-stu-id="85ffd-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="85ffd-202">Voordat u een Cordova-app voor iOS met Visual Studio uitvoeren kunt, gaat u door de stappen in de [iOS Setup Guide] [ 12] wilt installeren en uitvoeren van de externe build-agent.</span><span class="sxs-lookup"><span data-stu-id="85ffd-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="85ffd-203">Zorg ervoor dat u de app voor iOS kunt samenstellen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="85ffd-204">De stappen in de setup guide zijn vereist om te bouwen voor iOS vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85ffd-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="85ffd-205">Als u een Mac niet hebt, kunt u voor iOS met de externe build-agent op een service, zoals MacInCloud samenstellen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="85ffd-206">Zie voor meer informatie [uitvoeren van uw iOS-app in de cloud][21].</span><span class="sxs-lookup"><span data-stu-id="85ffd-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="85ffd-207">XCode 7 of hoger is vereist voor de push-invoegtoepassing in iOS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85ffd-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="85ffd-208">De ID te gebruiken als uw App-ID vinden</span><span class="sxs-lookup"><span data-stu-id="85ffd-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="85ffd-209">Voordat u uw app voor pushmeldingen, open config.xml in uw Cordova-app registreren, vindt de `id` kenmerk waarde in het element widget en kopiëren voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="85ffd-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="85ffd-210">In het volgende XML-bestand, de ID is `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="85ffd-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="85ffd-211">Deze id later gebruiken bij het maken van een App-ID op van Apple developer portal.</span><span class="sxs-lookup"><span data-stu-id="85ffd-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="85ffd-212">Als u een andere App-ID in de portal voor ontwikkelaars maakt, moet u rekening houden met een paar extra stappen verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="85ffd-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="85ffd-213">De ID in het element widget moet overeenkomen met de App-ID op de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="85ffd-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="85ffd-214">De app voor pushmeldingen op Apple developer-portal te registreren</span><span class="sxs-lookup"><span data-stu-id="85ffd-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="85ffd-215">Bekijk een video van vergelijkbare stappen</span><span class="sxs-lookup"><span data-stu-id="85ffd-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="85ffd-216">Configureren van Azure om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="85ffd-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="85ffd-217">Controleren of uw App-ID overeenkomt met uw Cordova-app</span><span class="sxs-lookup"><span data-stu-id="85ffd-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="85ffd-218">Als de App-ID die u hebt gemaakt in uw ontwikkelaarsaccount Apple al overeenkomt met de ID van het element widget in config.xml, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="85ffd-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="85ffd-219">Als de id's niet overeenkomen, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="85ffd-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="85ffd-220">Verwijder de map platforms van uw project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="85ffd-221">Verwijder de map plugins van uw project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="85ffd-222">Verwijder de map node_modules van uw project.</span><span class="sxs-lookup"><span data-stu-id="85ffd-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="85ffd-223">Bijwerken van het kenmerk id van het element widget in config.xml om de App-ID die u hebt gemaakt in uw Apple Developer-Account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85ffd-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="85ffd-224">Bouw het project opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="85ffd-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="85ffd-225">Pushmeldingen testen in uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="85ffd-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="85ffd-226">Controleer of in Visual Studio **iOS** is geselecteerd als het implementatiedoel en kies vervolgens **apparaat** uit te voeren op het verbonden iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85ffd-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="85ffd-227">U kunt uitvoeren op een iOS-apparaat is verbonden met uw PC met iTunes.</span><span class="sxs-lookup"><span data-stu-id="85ffd-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="85ffd-228">De iOS-Simulator biedt geen ondersteuning voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="85ffd-229">Druk op de **uitvoeren** knop of **F5** in Visual Studio om het project bouwen en starten van de app in een iOS-apparaat, klik vervolgens op **OK** pushmeldingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="85ffd-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85ffd-230">De app vraagt om bevestiging voor pushmeldingen tijdens de eerste keer uitvoert.</span><span class="sxs-lookup"><span data-stu-id="85ffd-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="85ffd-231">Typ een taak in de app en klik vervolgens op het plusteken (+) pictogram.</span><span class="sxs-lookup"><span data-stu-id="85ffd-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="85ffd-232">Controleer of u een melding wordt ontvangen en klik op OK om af te sluiten van de melding.</span><span class="sxs-lookup"><span data-stu-id="85ffd-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="85ffd-233">(Optioneel) Configureren en uitvoeren in Windows</span><span class="sxs-lookup"><span data-stu-id="85ffd-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="85ffd-234">Deze sectie is voor het uitvoeren van de Apache Cordova-app-project op Windows 10-apparaten (de PhoneGap-push-invoegtoepassing wordt ondersteund op Windows 10).</span><span class="sxs-lookup"><span data-stu-id="85ffd-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="85ffd-235">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="85ffd-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="85ffd-236">Uw Windows-app voor pushmeldingen registreren met WNS</span><span class="sxs-lookup"><span data-stu-id="85ffd-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="85ffd-237">Als u de Store-opties in Visual Studio, selecteer een Windows doel in de lijst met oplossing platformen, zoals **Windows x64** of **Windows x86** (voorkomen **Windows AnyCPU** voor pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="85ffd-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="85ffd-238">[Bekijk een video van gelijksoortige stappen][13]</span><span class="sxs-lookup"><span data-stu-id="85ffd-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="85ffd-239">De notification hub configureren voor WNS</span><span class="sxs-lookup"><span data-stu-id="85ffd-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="85ffd-240">Configureer uw Cordova-app om ondersteuning voor pushmeldingen voor Windows</span><span class="sxs-lookup"><span data-stu-id="85ffd-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="85ffd-241">Open de configuration designer (met de rechtermuisknop op config.xml en selecteer **ontwerper**), selecteer de **Windows** tabblad en kies **Windows 10** onder  **Windows doel versie**.</span><span class="sxs-lookup"><span data-stu-id="85ffd-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="85ffd-242">Ter ondersteuning van push meldingen in uw standaard (debug) bouwt, open build.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="85ffd-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="85ffd-243">Kopieer de "release"-configuratie aan uw configuratie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="85ffd-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="85ffd-244">Nadat de update, moet de build.json bevatten de volgende code:</span><span class="sxs-lookup"><span data-stu-id="85ffd-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="85ffd-245">De app bouwen en te controleren of er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="85ffd-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="85ffd-246">Uw client-app moet zich nu registreren voor de meldingen van de back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="85ffd-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="85ffd-247">Herhaal deze sectie voor elke Windows-project in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="85ffd-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="85ffd-248">Pushmeldingen testen in uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="85ffd-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="85ffd-249">In Visual Studio, zorg ervoor dat een Windows-platform is geselecteerd als het implementatiedoel zoals **Windows x64** of **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="85ffd-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="85ffd-250">Als u wilt uitvoeren op een Windows 10-computer die als host fungeert voor Visual Studio, kies **lokale Machine**.</span><span class="sxs-lookup"><span data-stu-id="85ffd-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="85ffd-251">Druk op de knop uitvoeren op het project bouwen en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="85ffd-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="85ffd-252">Typ een naam voor een nieuwe taken in de app en klik vervolgens op het plusteken (+) pictogram toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="85ffd-253">Controleer of dat er een melding wordt ontvangen wanneer het item is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="85ffd-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="85ffd-254"><a name="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85ffd-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="85ffd-255">Meer informatie over [Notification Hubs] [ 17] voor meer informatie over pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="85ffd-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="85ffd-256">Als u dit nog niet hebt gedaan, blijven de zelfstudie door [Authentication toevoegen] [ 14] aan uw Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="85ffd-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="85ffd-257">Informatie over het gebruik van de SDK's.</span><span class="sxs-lookup"><span data-stu-id="85ffd-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="85ffd-258">[Apache Cordova-SDK][15]</span><span class="sxs-lookup"><span data-stu-id="85ffd-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="85ffd-259">[ASP.NET-Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="85ffd-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="85ffd-260">[Server-SDK voor node.js][16]</span><span class="sxs-lookup"><span data-stu-id="85ffd-260">[Node.js Server SDK][16]</span></span>

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
